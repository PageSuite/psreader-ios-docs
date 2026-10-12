<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Adding-Comment-Buttons",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Adding Comment Buttons"
}
-->

# Adding Comment Buttons

Show comment buttons and counts on the articles in your own reader screen, with the SDK’s commenting provider.

## Overview

The reader draws comment buttons itself. On an article page,
[`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController) pins a comment button to the foot of the
page, adds one to the byline where the article’s template has a
commenting widget, labels them with the comment count, and introduces
them with a tooltip. It asks its commenting delegate for each of these,
so your reader screen becomes that delegate and forwards each call to a
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider), as the prebuilt reader does.

Using the prebuilt UI? See [Commenting](/documentation/PSReader/Commenting).

Add the provider to `ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), as a stored property, so it lives as long as
the screen does:

```swift
private let commenting = DefaultCommentingProvider(
    service: CoralCommentingService(domain: "talk.example.com"),
    accentColor: .systemBlue,
    fontFamily: .systemFont(ofSize: 16),
    onCommentButtonTapped: { article, page, source, viewController in
        // Present the article's comment thread from viewController.
    }
)
```

The provider is the prebuilt UI’s own: it counts comments through a
service, caches the counts, styles the button in your accent color and
font, and shows each tooltip once. [Commenting](/documentation/PSReader/Commenting) explains the provider
and the Coral service, and how to write a service for another backend.
[Presenting the Comment Thread](/documentation/PSReader/Commenting#Presenting-the-Comment-Thread) shows what the tap closure
receives.

## Forwarding the Reader’s Commenting Delegate

In `hostReader()`, with the other delegates, make the screen the reader’s
commenting delegate:

```swift
reader.commentingDelegate = self
```

The reader holds its commenting delegate weakly, which is why the screen,
owner of both the reader and the provider, is the delegate. The reader’s
[`PSEditionReaderViewController.CommentingDelegate`](/documentation/PSReader/PSEditionReaderViewController/CommentingDelegate-swift.protocol) is a
smaller protocol than the prebuilt UI’s [`CommentingDelegate`](/documentation/PSReader/CommentingDelegate): it has no
edition parameter, and a count is optional. Conform in an extension, in
the same file as the class, and forward each call to the provider with
the screen’s `source`:

```swift
extension ReaderScreenViewController: PSEditionReaderViewController.CommentingDelegate {

    func isCommentingEnabled(article: PSEArticle) -> Bool {
        guard let source else {
            return false
        }
        return commenting.isCommentingEnabled(article: article, inEdition: source)
    }

    func commentButtonView(forArticle article: PSEArticle, onTap: @escaping () -> Void) -> UIView? {
        guard let source else {
            return nil
        }
        return commenting.commentButton(forArticle: article, inEdition: source, onTap: onTap)
    }

    func commentButtonTapped(forArticle article: PSEArticle, onPage page: PSEPage, from viewController: UIViewController) {
        guard let source else {
            return
        }
        commenting.commentButtonTapped(forArticle: article, onPage: page, inEdition: source, from: viewController)
    }

    func fetchCommentCount(forArticle article: PSEArticle, completion: @escaping (Int?) -> Void) {
        guard let source else {
            return completion(nil)
        }
        commenting.fetchCommentCount(forArticle: article, inEdition: source, cacheStrategy: .preferNetwork) { result in
            completion(try? result.get())
        }
    }

    func articleCommentTooltipViewController() -> UIViewController? {
        guard let source else {
            return nil
        }
        return commenting.articleCommentTooltipViewController(inEdition: source)
    }
}
```

The reader asks only once an edition is open, so `source` is always set
by then. In Swift 6 language mode, mark the conformance
`@preconcurrency`; see [Swift 6 Language Mode](/documentation/PSReader/Hosting-the-Reader#Swift-6-Language-Mode). The buttons’ counts use `.preferNetwork`, as in the prebuilt
reader, so the count on the page is fresh; if the fetch fails, the
provider falls back to the count it cached.

## Prefetching Counts

The prebuilt reader clears the provider’s cache and prefetches the
edition’s counts each time it opens an edition. In `show(_:at:)`, add:

```swift
commenting.clearCache()
let articles = (source.edition.pages ?? []).flatMap { $0.articles ?? [] }
commenting.prefetchCommentCounts(forArticles: articles, inEdition: source, completion: nil)
```

The provider passes its service only the articles that take comments, in
one call. The cache it fills answers your page browser at once (see
[Showing Counts in Your Page Browser](/documentation/PSReader/Adding-Comment-Buttons#Showing-Counts-in-Your-Page-Browser)); the buttons on the page
fetch their own counts either way.

## What the Reader Draws

The reader offers commenting for the first article on each templated page
whose `isCommentingEnabled(article:)` returns `true`. PDF pages show no
buttons.

- **The footer button** is the view your delegate returns. The reader pins
  it full width to the bottom of the page and insets the page above it.
  With a ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEScrollCollapseController`` attached, it slides away with your
  chrome; see <doc://com.pagesuite.PSReader/documentation/PSReader/Hosting-the-Reader#Collapsing-Chrome-on-Scroll>.
- **The byline button** appears in templates with a commenting widget. The
  template draws it, and the reader sets its text.
- **The labels** change as each count arrives, through the commenting
  localization keys (see <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting#Localization>). The reader
  relabels the footer button only if it adopts ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingButtonView``,
  as ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingButton`` does.
- **The tooltip** appears as a popover above the footer button once the
  page is in view. The provider returns it only until it has been seen.

A tap on either button reaches `commentButtonTapped`, and through it the
provider’s [`onCommentButtonTapped`](/documentation/PSReader/DefaultCommentingProvider/onCommentButtonTapped). To change
the button or the tooltip, pass a subclass of the provider; see
[Customizing the Button](/documentation/PSReader/Commenting#Customizing-the-Button) and [Tooltips](/documentation/PSReader/Commenting#Tooltips).

## Showing Counts in Your Page Browser

The prebuilt content browser lists each article’s comment count, with a
trending icon once the count reaches the provider’s
[`trendingThreshold`](/documentation/PSReader/DefaultCommentingProvider/trendingThreshold). To do the same in your
page browser (see [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser)), ask the same provider
with `.preferCache`, which answers from the prefetched counts at once:

```swift
extension ReaderScreenViewController {

    func showCommentCount(of article: PSEArticle, in cell: ArticleCell) {
        cell.article = article
        cell.commentsView.isHidden = true

        guard let source, commenting.isCommentingEnabled(article: article, inEdition: source) else {
            return
        }

        let threshold = commenting.trendingThreshold
        commenting.fetchCommentCount(forArticle: article, inEdition: source, cacheStrategy: .preferCache) { result in
            // A count that wasn't cached arrives later, maybe after the cell was reused.
            guard cell.article === article, let count = try? result.get() else {
                return
            }
            cell.countLabel.text = "\(count)"
            cell.trendingIcon.isHidden = count < threshold
            cell.commentsView.isHidden = false
        }
    }
}
```

`ArticleCell` stands for your page browser’s cell. The prebuilt content
browser introduces its counts with a second tooltip, above the first count
fully in view once the list comes to rest. Present the provider’s
[`contentBrowserCommentTooltipViewController(inEdition:)`](/documentation/PSReader/CommentingDelegate/contentBrowserCommentTooltipViewController(inEdition:))
the same way; like the article tooltip, it returns `nil` once seen. A
popover adapts to a sheet in compact widths, so keep it a popover through
its delegate:

```swift
extension ReaderScreenViewController: UIPopoverPresentationControllerDelegate {

    func showCommentTooltip(above countView: UIView) {
        guard let source,
              let tooltip = commenting.contentBrowserCommentTooltipViewController(inEdition: source) else {
            return
        }

        tooltip.modalPresentationStyle = .popover
        if let popover = tooltip.popoverPresentationController {
            popover.sourceView = countView
            popover.sourceRect = countView.bounds
            popover.permittedArrowDirections = .down
            popover.delegate = self
        }
        present(tooltip, animated: true)
    }

    func adaptivePresentationStyle(for controller: UIPresentationController,
                                   traitCollection: UITraitCollection) -> UIModalPresentationStyle {
        .none
    }
}
```

## Linking Back to an Article

To bring the user back to an article later, from a comment history or a
notification about a reply, save `source.published.editionGUID` and
`page.pageguid` when they open the thread. Resolve the edition GUID with
[`published(forEditionGUID:)`](/documentation/PSReader/FeedEditionService/published(forEditionGUID:)), and open your reader
screen with `ReaderScreenViewController(published:openingPageGUID:)`;
[Routing Links and Notifications](/documentation/PSReader/Opening-an-Edition#Routing-Links-and-Notifications) shows the code.

## Commenting Without the Provider

The reader’s protocol doesn’t need the SDK’s provider. To use your own
backend and views throughout, implement its five methods directly:

- Return a view adopting ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingButtonView`` from
  `commentButtonView(forArticle:onTap:)`, and call `onTap` when it’s
  tapped, so the reader can relabel it with counts. Any other view keeps
  its own text. Return `nil` for no footer button.
- Call the `fetchCommentCount` completion with `nil` when there’s no
  count, from any queue; the reader moves to the main queue itself.
- Return `nil` from `articleCommentTooltipViewController()` for no
  tooltip, and keep returning `nil` once the user has seen yours: the
  reader asks each time an article page with a button appears.