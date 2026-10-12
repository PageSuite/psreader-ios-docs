<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Sharing",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Sharing"
}
-->

# Sharing

Let users share the page or article in view from the prebuilt reader’s
share button.

## Overview

The prebuilt reader has a share button that hands a link to the page or
article in view to the system share sheet. Building a custom UI? See
[Adding a Share Button](/documentation/PSReader/Adding-a-Share-Button).

Pass a share delegate when you create your global configuration. Every
prebuilt reader shares through it, whether the carousel opened it or one
of your own screens did. This one shares the story on your website from
an article page, and the page in PageSuite’s web reader from any other
page:

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    shareDelegate: ShareProvider(sharePolicy: .preferArticleLink(
        webProvider: WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")
    ))
)
```

![The share sheet presented from the reader.](images/com.pagesuite.PSReader/share-sheet@2x.png)

The reader shows its share button only on pages the delegate can share.
On a double-page spread it asks about the spread’s reference page, which
prefers editorial content to an advert. A tap presents the share sheet
with the link, a Copy Link action ([`CopyLinkActivity`](/documentation/PSReader/CopyLinkActivity), whose title isn’t
localized), and a Print action (see [Printing](/documentation/PSReader/Sharing#Printing)), and reports a share
event (see [Sharing](/documentation/PSReader/Analytics#Sharing)).

The delegate is a [`ShareDelegate`](/documentation/PSReader/ShareDelegate). [`ShareProvider`](/documentation/PSReader/ShareProvider) is the one most
apps need: it shares under a policy you choose from the SDK’s two kinds
of link.

## Choosing a Share Policy

Two kinds of link are built in:

- **Web reader links** open the page in PageSuite’s web reader, in any
  browser. ``doc://com.pagesuite.PSReader/documentation/PSReader/WebReaderShareProvider`` builds them from your shortcode and
  the edition’s and page’s GUIDs. Its initializer spells the parameter
  `shortCode:`, with a capital C, where the rest of the SDK says
  `shortcode:`.
- **Article links** open the story on the publisher’s website.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/ArticleLinkShareProvider`` shares an article’s
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEArticle/sharelink``, when the publisher’s content provides one.

A [`ShareProvider.SharePolicy`](/documentation/PSReader/ShareProvider/SharePolicy) says which of them [`ShareProvider`](/documentation/PSReader/ShareProvider)
uses, and in what order. The provider shares the first link it gets, and
a page is shareable when any of them can share it:

|Policy                            |Shares                                   |Share button shows on          |
|----------------------------------|-----------------------------------------|-------------------------------|
|`.onlyArticleLink()`              |Article links                            |Article pages with a share link|
|`.preferArticleLink(webProvider:)`|Article links, otherwise web reader links|Every page                     |
|`.onlyWebReader(webProvider:)`    |Web reader links                         |Every page                     |
|`.preferWebReader(webProvider:)`  |Web reader links, otherwise article links|Every page                     |
|`.disabled`                       |Nothing                                  |No page                        |

An article link needs a single-article page whose [`type`](/documentation/PSReader/PSEPage/type) is
`templateArticle` and whose article has a [`sharelink`](/documentation/PSReader/PSEArticle/sharelink). A web
reader link needs the page’s [`pageguid`](/documentation/PSReader/PSEPage/pageguid) and the edition’s
[`editionguid`](/documentation/PSReader/PSEEdition/editionguid); `.preferWebReader` falls back to the article
link only when one of those is missing.

Without a share delegate of your own, the prebuilt UI uses
`.onlyArticleLink()`. It’s the default of [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration)‘s
`shareDelegate` parameter, and of [`init(sharePolicy:)`](/documentation/PSReader/ShareProvider/init(sharePolicy:)).
Classic PDF pages have no article link, so by default they can’t be
shared; choose a policy with a web reader link to share them:

```swift
let webReader = WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")

// Article pages share the story on your website; other pages, the web reader.
let preferArticles = ShareProvider(sharePolicy: .preferArticleLink(webProvider: webReader))

// Every page shares its web reader link.
let webReaderOnly = ShareProvider(sharePolicy: .onlyWebReader(webProvider: webReader))

// No sharing: the share button never shows.
let noSharing = ShareProvider(sharePolicy: .disabled)
```

> Replica: The legacy replica reader, which opens replica editions unless
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` is `false`, doesn’t use
> the share delegate. It builds its share messages from
> ``doc://com.pagesuite.PSReader/documentation/PSReader/LegacyReaderConfiguration/shareTemplater-swift.property``. In the
> current reader, the providers share replica editions too:
> ``doc://com.pagesuite.PSReader/documentation/PSReader/WebReaderShareProvider`` shares every page and article, and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ArticleLinkShareProvider`` only articles whose `shareLink` is set,
> never PDF pages.

## Using Your Own Web Reader Domain

[`WebReaderShareProvider`](/documentation/PSReader/WebReaderShareProvider) links to `reader.pagesuite.com` unless you give
it a `urlMask`. If your web reader runs on a domain of your own, pass its
host, without `https://`:

```swift
let webReader = WebReaderShareProvider(urlMask: "reader.example.com", shortCode: "SHORTCODE")
```

Links then read
`https://reader.example.com/shortcode/SHORTCODE/edition/EDITION_GUID?page=PAGE_GUID`,
and their subject names the publication, the edition, and the page’s
[`pageLabel`](/documentation/PSReader/PSEPage/pageLabel).

> Replica: For replica editions, the provider links to the replica web
> reader at `edition.pagesuite.com`. A `urlMask` replaces both hosts, so if
> your replica titles use another domain, give their readers a provider of
> their own.

## Changing Sharing for One Reader

Configurations copy the delegate when you create them (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)), so set it on the global configuration
first. To change how one reader shares, set
[`shareDelegate`](/documentation/PSReader/ReaderConfiguration/shareDelegate) on that reader’s configuration: the
`readerConfig` of a carousel section or prebuilt screen, or the reader
configuration you pass to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
// A carousel section whose editions can't be shared
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.shareDelegate = ShareProvider(sharePolicy: .disabled)

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig)
    ]
)

// A reader that shares web reader links only
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.shareDelegate = ShareProvider(sharePolicy: .onlyWebReader(
    webProvider: WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")
))

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

## Writing a Custom Share Delegate

Implement [`ShareDelegate`](/documentation/PSReader/ShareDelegate) when no policy does what you need. A share
delegate makes two decisions for the page in view:
[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/isShareable(page:inEdition:inPublished:)) says whether
it can be shared at all, and
[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/shareContext(forPage:inEdition:inPublished:)) says what
to share, as a [`ShareContext`](/documentation/PSReader/ShareContext): the items, any extra activities for the
sheet, and a subject line for Mail and other activities that use one.

For editions on PageSuite’s current system, a delegate needs only
`shareContext`; the other methods have defaults. This delegate shares
article pages only, and tags each link for the publisher’s web analytics:

```swift
struct TaggedArticleShareDelegate: ShareDelegate {

    func shareContext(
        forPage page: PSEPage,
        inEdition edition: PSEEdition,
        inPublished published: PSEPublished
    ) -> ShareContext? {
        guard page.type == "templateArticle",
              let article = page.articles?.first,
              let link = article.sharelink,
              var components = URLComponents(string: link) else {
            return nil
        }

        components.queryItems = (components.queryItems ?? []) + [
            URLQueryItem(name: "utm_source", value: "ios_app")
        ]
        guard let url = components.url else { return nil }

        return ShareContext(
            activityItems: [url],
            applicationActivities: [CopyLinkActivity()],
            subject: article.headline
        )
    }
}
```

Assign it wherever a provider would go: globally, or on one reader’s
configuration.

The default `isShareable` returns whether `shareContext` returns a
context. The reader asks on every page turn, so implement it as well if
building a context is expensive. Keep [`CopyLinkActivity`](/documentation/PSReader/CopyLinkActivity) in your
activities for the Copy Link action, or use an activity of your own for a
localized title. To keep a built-in policy and only adjust its result,
wrap a [`ShareProvider`](/documentation/PSReader/ShareProvider) and edit the context it returns.

> Replica: To share replica editions in the current reader, also implement
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate/shareContext(forSpread:inReplicaEdition:)``, and
> optionally ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate/isShareable(spread:inReplicaEdition:)``. They
> receive the legacy `PSReplicaPageSpread` (`.single`,
> `.double(left:right:)`, or `.article` for an article opened from a page)
> and its `PSReplicaEdition`. By default they share nothing, so replica
> pages show no share button.

## Printing

The share sheet offers a Print action alongside your context’s items. It
prints the editorial pages in view: classic PDF pages from their PDF, and
article and section pages from the rendered article or the page’s image.
The reader’s settings menu has a Print row too, so printing doesn’t
depend on sharing: with `.disabled`, users still print from settings.

> Replica: In the current reader, replica editions print from the settings
> menu only. The legacy replica reader adds Print to its own share sheet.

## Topics

### Share Policies

[`ShareProvider`](/documentation/PSReader/ShareProvider)

A composite share provider allowing multiple share strategies to be chained.
Configure this provider to choose preferred or fallback sharing behaviors.

[`WebReaderShareProvider`](/documentation/PSReader/WebReaderShareProvider)

A [`ShareDelegate`](/documentation/PSReader/ShareDelegate) that shares links to pages in PageSuite’s web reader.

[`ArticleLinkShareProvider`](/documentation/PSReader/ArticleLinkShareProvider)

A [`ShareDelegate`](/documentation/PSReader/ShareDelegate) providing direct article links on the publication’s website.

### Custom Share Delegates

[`ShareDelegate`](/documentation/PSReader/ShareDelegate)

Delegate protocol used to provide sharing functionality within the SDK.

[`ShareContext`](/documentation/PSReader/ShareContext)

A structure encapsulating information used to present shareable content.

[`CopyLinkActivity`](/documentation/PSReader/CopyLinkActivity)

A share sheet activity that copies a shared URL to the pasteboard.

