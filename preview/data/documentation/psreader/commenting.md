<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Commenting",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Commenting"
}
-->

# Commenting

Switch on comment buttons and counts in the prebuilt reader, and open
your commenting platform when users tap them.

## Overview

The prebuilt reader draws commenting’s entry points and leaves the
conversation to your app. On an article with commenting enabled, it pins
a comment button labeled with the article’s comment count to the foot of
the page, and calls your code when the user taps it.
Building a custom UI? See [Adding Comment Buttons](/documentation/PSReader/Adding-Comment-Buttons).

Set a commenting provider as the global configuration’s commenting
delegate to switch it on. This one connects to
[Coral](https://coralproject.net/):

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.commentingDelegate = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: CoralCommentingService(domain: "talk.example.com"),
    onCommentButtonTapped: { article, page, source, viewController in
        // Present the article's comment thread from viewController.
    }
)
```

![An article page with its comment button and tooltip, with callouts for each.](images/com.pagesuite.PSReader/commenting-button-annotated@2x.png)

Every edition a prebuilt reader opens then shows commenting, whether
the carousel opened it or one of your own screens did:

- As the edition opens, the reader clears the provider’s cache and
  prefetches counts for all its articles.
- Article pages show the footer button, and a second button in the
  byline where the article’s template includes a commenting widget. The
  article tooltip appears once, above the first footer button the reader
  sees.
- The content browser shows each article’s count beside a comment icon,
  with a trending icon once the count reaches the provider’s trending
  threshold. Its tooltip appears once, above the first count fully in view
  when the list comes to rest.

The reader adds the buttons for the first article on each templated page;
PDF pages don’t show them.

Four types divide the work:

- ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingService`` talks to your commenting backend. It decides which
  articles take comments, gives each a stable identifier, and fetches
  counts.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate`` adds the UI: the button, the tap, a count cache,
  the trending threshold, and onboarding tooltips.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider`` is a ready-made delegate that wraps any
  service. It caches counts, styles the button with your accent color and
  font, shows each tooltip once, and forwards taps to its
  ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider/onCommentButtonTapped`` closure.
- ``doc://com.pagesuite.PSReader/documentation/PSReader/CoralCommentingService`` is a service for Coral. It reads the
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSECoralCommenting`` identifiers the backend sends with each article.
  For another backend, write your own service (see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Commenting#Writing-a-Commenting-Service>).

> Replica: Commenting is a feature of editions on PageSuite’s current
> system. Legacy replica editions show no comment buttons, counts, or
> tooltips.

## Presenting the Comment Thread

[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) calls
[`onCommentButtonTapped`](/documentation/PSReader/DefaultCommentingProvider/onCommentButtonTapped) when the user taps a
footer or byline button, with these values:

|Parameter       |Type                                                                    |Description                                                          |
|----------------|------------------------------------------------------------------------|---------------------------------------------------------------------|
|`article`       |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle``      |The article to show comments for.                                    |
|`page`          |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage``         |The page the article is on.                                          |
|`source`        |``doc://com.pagesuite.PSReader/documentation/PSReader/PSEEditionSource``|The open edition.                                                    |
|`viewController`|`UIViewController`                                                      |The reader page that was tapped. Present your comment thread from it.|

With Coral, the article’s [`coralCommenting`](/documentation/PSReader/PSEArticleMetadata/coralCommenting) holds
what your Coral embed needs: [`assetId`](/documentation/PSReader/PSECoralCommenting/assetId) identifies
the comment stream, [`publicUrl`](/documentation/PSReader/PSECoralCommenting/publicUrl) is the URL Coral
associates with it, and [`enabled`](/documentation/PSReader/PSECoralCommenting/enabled) says whether
commenting is on.

```swift
globalConfig.commentingDelegate = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: CoralCommentingService(domain: "talk.example.com"),
    onCommentButtonTapped: { article, page, source, viewController in
        guard let assetID = article.metadata?.coralCommenting?.assetId else { return }

        let comments = CoralCommentsViewController(assetID: assetID)
        viewController.present(comments, animated: true)
    }
)
```

`CoralCommentsViewController` stands for your own Coral screen. The SDK
doesn’t include one.

### Linking Back to an Article

To bring the user back to an article later, from a comment history or a
notification about a reply, save `source.published.editionGUID` and
`page.pageguid` when they open the thread. Those two values reopen the
article: pass the page as the opening page.

```swift
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    publicationGUID: "PUBLICATION_GUID",
    editionGUID: editionGUID,
    openingPage: .page(guid: pageGUID)
)
reader.modalPresentationStyle = .fullScreen
present(reader, animated: true)
```

[Routing Links and Notifications](/documentation/PSReader/Presenting-the-Prebuilt-Reader#Routing-Links-and-Notifications)
shows the whole flow, from a notification to the open page.

## Writing a Commenting Service

To connect a backend other than Coral, adopt [`CommentingService`](/documentation/PSReader/CommentingService). All
four methods are required:

```swift
class MyCommentingService: CommentingService {

    func isCommentingEnabled(article: PSEArticle, inEdition source: PSEEditionSource) -> Bool {
        article.articleguid != nil
    }

    func articleIdentifier(for article: PSEArticle) -> String? {
        article.articleguid
    }

    func fetchCommentCount(forArticle article: PSEArticle,
                           inEdition source: PSEEditionSource,
                           completion: @escaping (Result<Int, Error>) -> Void) {
        guard let id = articleIdentifier(for: article) else {
            completion(.failure(CommentingError.noIdentifier))
            return
        }
        CommentsAPI.count(forID: id, completion: completion)
    }

    func prefetchCommentCounts(forArticles articles: [PSEArticle],
                               inEdition source: PSEEditionSource,
                               completion: ((Result<[String: Int], Error>) -> Void)?) {
        let ids = articles.compactMap { articleIdentifier(for: $0) }
        CommentsAPI.counts(forIDs: ids) { result in
            completion?(result)
        }
    }
}
```

`CommentsAPI` stands for your backend client. Pass the service to
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) in place of [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService).

- **The identifier is the cache key.** Return the same value for an
  article every time. Key the prefetch results by it, too: the provider
  stores each returned count under its key. An article without an
  identifier gets no count.
- **Prefetch arrives filtered.** The provider passes only articles that
  have an identifier and commenting enabled, and skips the call when none
  qualify.
- **Call back on any queue.** The provider delivers your results on the
  main queue.

## Changing Commenting for One Reader

Configurations copy the delegate when you create them (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)), so set it on the global configuration
first. To change commenting for one reader, set
[`commentingDelegate`](/documentation/PSReader/ReaderConfiguration/commentingDelegate) on that reader’s
configuration, to a different provider or to `nil` to turn commenting
off. That’s the `readerConfig` of a carousel section or prebuilt screen,
or the reader configuration you pass to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
// A carousel section without commenting
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.commentingDelegate = nil

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig)
    ]
)

// A reader whose comments live on another Coral site
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.commentingDelegate = DefaultCommentingProvider(
    globalConfig: globalConfig,
    service: CoralCommentingService(domain: "talk.example.org"),
    onCommentButtonTapped: { article, page, source, viewController in
        // Present the article's comment thread from viewController.
    }
)

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

## Customizing the Button

[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) returns a [`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton): a
full-width strip with a keyline along the top and a bordered pill
holding the label, in the provider’s accent color and its font, bold at
16 points. The `globalConfig:` initializer takes those from
[`brandColor`](/documentation/PSReader/GlobalConfiguration/brandColor) and
[`secondaryFont`](/documentation/PSReader/GlobalConfiguration/secondaryFont). To change the button’s shape or
type, subclass the provider and override
[`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/DefaultCommentingProvider/commentButton(forArticle:inEdition:onTap:)):

```swift
final class BrandedCommentingProvider: DefaultCommentingProvider {

    override func commentButton(
        forArticle article: PSEArticle,
        inEdition source: PSEEditionSource,
        onTap: @escaping () -> Void
    ) -> (any CommentingButtonView)? {
        let button = DefaultCommentingButton(
            text: LocalizationManager.shared.localizedString(for: .commentButtonFooter(commentCount: nil)),
            foregroundColor: accentColor,
            font: .systemFont(ofSize: 16, weight: .semibold),
            pillIdealWidth: 280,
            pillTopPadding: 20,
            pillBottomPadding: 20
        )
        button.onTap = onTap
        return button
    }
}
```

The reader replaces the label once the count arrives, so set its text
through the localization keys (see
[Localization](/documentation/PSReader/Commenting#Localization)), not here. Return `nil` to leave an
article without a footer button.

For a button of your own, adopt [`CommentingButtonView`](/documentation/PSReader/CommentingButtonView) on a `UIView`:
call [`onTap`](/documentation/PSReader/CommentingButtonView/onTap) when it’s tapped, and show the text
the reader passes to [`updateText(_:)`](/documentation/PSReader/CommentingButtonView/updateText(_:)). The reader
pins the button full width to the bottom of the page, insets the page
above it, and slides it away with the reader’s chrome as the page scrolls.

## Tooltips

[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) introduces commenting with two popovers:

- **Article tooltip**, above the footer button the first time an article
  page with one is on screen.
- **Content browser tooltip**, above the first comment count fully in view
  when the prebuilt content browser’s list comes to rest.

Each appears once per install. The provider remembers in `UserDefaults`
that a tooltip has appeared and returns `nil` from then on.

Change the text through the localization keys. To change the look,
override
[`articleCommentTooltipViewController(inEdition:)`](/documentation/PSReader/DefaultCommentingProvider/articleCommentTooltipViewController(inEdition:))
or
[`contentBrowserCommentTooltipViewController(inEdition:)`](/documentation/PSReader/DefaultCommentingProvider/contentBrowserCommentTooltipViewController(inEdition:)),
and track the shown state yourself, as the provider does:

```swift
final class BrandedCommentingProvider: DefaultCommentingProvider {

    override func articleCommentTooltipViewController(inEdition source: PSEEditionSource) -> UIViewController? {
        let shownKey = "articleCommentTooltipShown"
        guard !UserDefaults.standard.bool(forKey: shownKey) else { return nil }

        let tooltip = DefaultCommentTooltipViewController(
            text: LocalizationManager.shared.localizedString(for: .commentArticleTooltip),
            font: .preferredFont(forTextStyle: .subheadline),
            foregroundColor: .white,
            backgroundColor: accentColor
        )
        tooltip.onAppear = { UserDefaults.standard.set(true, forKey: shownKey) }
        return tooltip
    }
}
```

The reader asks for the article tooltip each time such a page appears, so
returning `nil` is how a tooltip stays dismissed. Return `nil` always to
turn a tooltip off.

## Localization

Commenting’s labels come from four [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey) cases:

|Key                                                                                                          |Default text                                                            |Where                  |
|-------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|-----------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/commentButtonFooter(commentCount:)``|“View comments”, or “View comments (%lld)” with a count                 |Footer button          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/commentButtonByline(commentCount:)``|“Comment”, “1 comment”, or “%lld comments”                              |Byline button          |
|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/commentArticleTooltip``             |“Get involved with community discussion here.”                          |Article tooltip        |
|``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/commentContentBrowserTooltip``      |“Today’s paper now has comments. Get involved in community discussions.”|Content browser tooltip|

Translate or reword them with a String Catalog, or through a
[`LocalizationManager`](/documentation/PSReader/LocalizationManager) subclass. See [Localization](/documentation/PSReader/Localization).

## Trending Threshold and Icons

The prebuilt content browser shows a trending icon beside an article’s
count once the count reaches
[`trendingThreshold`](/documentation/PSReader/DefaultCommentingProvider/trendingThreshold), 100 by default. Pass
`trendingThreshold:` to either initializer, or set the property later.

Both content browser icons come from your [`AssetDelegate`](/documentation/PSReader/AssetDelegate):
[`ImageResourceName.comment`](/documentation/PSReader/ImageResourceName/comment) for the count and
[`ImageResourceName.trending`](/documentation/PSReader/ImageResourceName/trending) for the trending icon. See [Theming](/documentation/PSReader/Theming).

## Cache Strategy

[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) keeps comment counts in memory.
[`CommentingCacheStrategy`](/documentation/PSReader/CommentingCacheStrategy) sets how
[`fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)`](/documentation/PSReader/CommentingDelegate/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:))
uses them:

|Strategy                                                                                     |Behavior                                                                              |
|---------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingCacheStrategy/preferCache``  |Returns a cached count at once, on the calling queue; fetches only on a cache miss.   |
|``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingCacheStrategy/preferNetwork``|Always fetches and updates the cache. Falls back to a cached count if the fetch fails.|

The prebuilt reader uses `.preferCache` in the content browser, where a
screen of cells wants counts at once, and `.preferNetwork` for the
article’s buttons, where the count should be fresh. Each time it opens an
edition it calls [`clearCache()`](/documentation/PSReader/CommentingDelegate/clearCache()) and refills the
cache with
[`prefetchCommentCounts(forArticles:inEdition:completion:)`](/documentation/PSReader/CommentingService/prefetchCommentCounts(forArticles:inEdition:completion:)).

## Implementing the Delegate Directly

To replace the caching, button, and tooltip logic wholesale, adopt
[`CommentingDelegate`](/documentation/PSReader/CommentingDelegate) yourself. It extends [`CommentingService`](/documentation/PSReader/CommentingService), so
build on your service:

```swift
final class MyCommentingDelegate: MyCommentingService, CommentingDelegate {

    let trendingThreshold = 50

    func fetchCommentCount(forArticle article: PSEArticle,
                           inEdition source: PSEEditionSource,
                           cacheStrategy: CommentingCacheStrategy,
                           completion: @escaping (Result<Int, Error>) -> Void) {
        // No cache here, so both strategies fetch.
        fetchCommentCount(forArticle: article, inEdition: source) { result in
            DispatchQueue.main.async { completion(result) }
        }
    }

    func clearCache() {}

    func commentButton(forArticle article: PSEArticle,
                       inEdition source: PSEEditionSource,
                       onTap: @escaping () -> Void) -> (any CommentingButtonView)? {
        let button = CommentsButton()   // your CommentingButtonView
        button.onTap = onTap
        return button
    }

    func commentButtonTapped(forArticle article: PSEArticle,
                             onPage page: PSEPage,
                             inEdition source: PSEEditionSource,
                             from viewController: UIViewController) {
        viewController.present(CommentsViewController(article: article), animated: true)
    }
}
```

Call the cache-strategy fetch’s completion on the main queue: the
prebuilt content browser updates its cells straight from it. The two
tooltip methods are optional; leave them out and no tooltips appear.

> Tip: Subclassing ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider`` and overriding one method
> is usually simpler. Adopt the protocol only to replace the caching,
> button, or tooltip logic entirely.

## Topics

### Switching On Commenting

[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider)

A ready-made [`CommentingDelegate`](/documentation/PSReader/CommentingDelegate) that wraps any [`CommentingService`](/documentation/PSReader/CommentingService).

[`CoralCommentingService`](/documentation/PSReader/CoralCommentingService)

A [`CommentingService`](/documentation/PSReader/CommentingService) implementation for
[Coral Talk](https://coralproject.net/).

### Connecting Another Backend

[`CommentingService`](/documentation/PSReader/CommentingService)

Data provider protocol for fetching comment counts from a backend.

### Customizing the Button and Tooltips

[`CommentingButtonView`](/documentation/PSReader/CommentingButtonView)

A custom view that acts as a comment button within the reader.

[`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton)

A pill-shaped comment button with a border and centered text label.

[`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController)

A popover tooltip view controller with a text label and close button.

### Caching Comment Counts

[`CommentingCacheStrategy`](/documentation/PSReader/CommentingCacheStrategy)

Controls how [`fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:)`](/documentation/PSReader/CommentingDelegate/fetchCommentCount(forArticle:inEdition:cacheStrategy:completion:))
resolves comment counts against the local cache.

### Replacing the Provider

[`CommentingDelegate`](/documentation/PSReader/CommentingDelegate)

Extends [`CommentingService`](/documentation/PSReader/CommentingService) with UI responsibilities for the commenting system.

