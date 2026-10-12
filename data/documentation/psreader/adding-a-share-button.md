<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Adding-a-Share-Button",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Adding a Share Button"
}
-->

# Adding a Share Button

Add a share button to your own reader screen that shares the page in view, using the share providers the prebuilt reader uses.

## Overview

The prebuilt reader has a share button that offers a link to the page in
view. Its share logic works on core models, so your reader screen can
use it unchanged: a [`ShareProvider`](/documentation/PSReader/ShareProvider) decides whether a page can be
shared and builds what to share, and you add the button and present the
share sheet.

Using the prebuilt UI? See [Sharing](/documentation/PSReader/Sharing).

Add a provider and the button to `ReaderScreenViewController`, the
reader screen from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader):

```swift
private let sharing = ShareProvider(sharePolicy: .preferArticleLink(
    webProvider: WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")
))

private lazy var shareButton = UIBarButtonItem(
    image: UIImage(systemName: "square.and.arrow.up"),
    style: .plain,
    target: self,
    action: #selector(shareTapped)
)
```

The policy picks between web reader links, which open the page in
PageSuite’s web reader, and article links, which open the story on the
publisher’s website. `.onlyWebReader(webProvider:)` and
`.onlyArticleLink()` share one kind of link,
`.preferWebReader(webProvider:)` and `.preferArticleLink(webProvider:)`
fall back to the other kind, and `.disabled` shares nothing.
[Choosing a Share Policy](/documentation/PSReader/Sharing#Choosing-a-Share-Policy) compares them, including the pages
each one can share. To share web reader links from every page, create the
provider with `.onlyWebReader(webProvider:)` instead:

```swift
private let sharing = ShareProvider(sharePolicy: .onlyWebReader(
    webProvider: WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")
))
```

## Showing the Button on Shareable Pages

In `addChrome()`, put the button in the navigation bar, disabled until
the first page settles:

```swift
shareButton.isEnabled = false
navigationItem.rightBarButtonItems = (navigationItem.rightBarButtonItems ?? []) + [shareButton]
```

Whether a page can be shared depends on the policy. With
`.onlyArticleLink()`, for example, only article pages with a share link
can. In `updateChrome()`, ask the provider about each page the reader
settles on:

```swift
if let source {
    shareButton.isEnabled = sharing.isShareable(
        page: page,
        inEdition: source.edition,
        inPublished: source.published
    )
}
```

Like the bookmark button in [Adding a Bookmark Button](/documentation/PSReader/Adding-a-Bookmark-Button), the button
disables rather than disappearing, so the bar keeps its layout.

## Presenting the Share Sheet

Add the action in an extension, in the same file as the class. On a tap,
ask the provider for the page’s [`ShareContext`](/documentation/PSReader/ShareContext), and present the share
sheet with its items, activities, and subject:

```swift
extension ReaderScreenViewController {

    @objc private func shareTapped() {
        guard let source,
              let page = reader.currentPage(),
              let context = sharing.shareContext(
                  forPage: page,
                  inEdition: source.edition,
                  inPublished: source.published
              ) else {
            return
        }

        let sheet = UIActivityViewController(
            activityItems: context.activityItems.map { SharedItem($0, subject: context.subject) },
            applicationActivities: context.applicationActivities
        )
        sheet.popoverPresentationController?.barButtonItem = shareButton   // iPad
        present(sheet, animated: true)
    }
}
```

The share sheet takes a subject, which mail uses, only from an item
source. `SharedItem` wraps each item to supply one:

```swift
final class SharedItem: NSObject, UIActivityItemSource {
    let item: Any
    let subject: String?

    init(_ item: Any, subject: String?) {
        self.item = item
        self.subject = subject
    }

    func activityViewControllerPlaceholderItem(_ controller: UIActivityViewController) -> Any {
        item
    }

    func activityViewController(_ controller: UIActivityViewController,
                                itemForActivityType type: UIActivity.ActivityType?) -> Any? {
        item
    }

    func activityViewController(_ controller: UIActivityViewController,
                                subjectForActivityType type: UIActivity.ActivityType?) -> String {
        subject ?? ""
    }
}
```

The prebuilt UI’s share events don’t fire from your button, so report
the share yourself; [Reporting Shares, Searches, and Links](/documentation/PSReader/Reporting-Analytics#Reporting-Shares-Searches-and-Links)
shows where.

## Using Your Own Share Logic

Any [`ShareDelegate`](/documentation/PSReader/ShareDelegate) works behind your button, not only
[`ShareProvider`](/documentation/PSReader/ShareProvider): call its
[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/isShareable(page:inEdition:inPublished:)) and
[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/shareContext(forPage:inEdition:inPublished:)) the same
way. [Writing a Custom Share Delegate](/documentation/PSReader/Sharing#Writing-a-Custom-Share-Delegate) shows one that tags
each link for the publisher’s web analytics.

## Printing

The prebuilt reader adds a Print action to its share sheet. That action
isn’t part of the share context, and the SDK has no print helper for a
custom UI yet, so build printing from public pieces. PDF pages print
from the files the reader is showing: each page’s
[`contenturl`](/documentation/PSReader/PSEPage/contenturl) names its PDF, and the source’s
[`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager) returns the file’s data. This works
for streamed and downloaded editions alike, since a page on screen has
already been fetched.

Add a print button the same way as the share button, with the action
`printPages`, and enable it in `updateChrome()` when `page.isPDF` is
`true`. Then add the action to the extension:

```swift
@objc private func printPages() {
    guard let source, let (spread, _) = reader.currentPageSpread() else {
        return
    }

    // The PDF of each page on screen, from the edition's storage.
    let pdfs = spread.nonAdvertPages().filter(\.isPDF).compactMap { page in
        page.contenturl.flatMap { source.resourceManager.cachedData(for: $0) }
    }
    guard !pdfs.isEmpty, UIPrintInteractionController.isPrintingAvailable else {
        return
    }

    let printInfo = UIPrintInfo.printInfo()
    printInfo.jobName = source.published.name

    let printer = UIPrintInteractionController.shared
    printer.printInfo = printInfo
    printer.printingItems = pdfs
    printer.present(animated: true)
}
```

To offer printing in the share sheet instead, wrap the same code in a
`UIActivity` subclass and pass it with the context’s
`applicationActivities`.

Templated pages, such as articles, have no PDF. The prebuilt reader
prints them from the page’s [`highRes`](/documentation/PSReader/PSEPage/highRes) image, and from the
extra images [`pagesInImage`](/documentation/PSReader/PSEPage/pagesInImage) describes when there are several.
Those are web addresses, so printing a templated page this way needs a
connection, even in a downloaded edition.