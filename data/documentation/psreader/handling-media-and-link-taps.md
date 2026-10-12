<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Handling-Media-and-Link-Taps",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Handling Media and Link Taps"
}
-->

# Handling Media and Link Taps

Respond to taps on the images, videos, embeds, hotspots, and links in the pages your own reader screen hosts.

## Overview

The prebuilt reader opens links in a Safari view controller, article
images in a gallery, and embeds in a sheet. [`PSEditionReaderViewController`](/documentation/PSReader/PSEditionReaderViewController)
does none of that itself. It covers PDF hotspots with the standard
overlays and opens a few kinds of link through the system. Every other
tap goes to your reader screen: media taps reach the reader’s
[`PSEditionReaderViewController.MediaDelegate`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol), and links arrive as
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification).

Using the prebuilt UI? See [Media and Links](/documentation/PSReader/Media-and-Links).

In `ReaderScreenViewController`, the reader screen from
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader), make the screen the reader’s media delegate.
In `hostReader()`, with the other delegates, add:

```swift
reader.mediaDelegate = self
```

Then conform in an extension, in the same file as the class, with the
methods for what you present:

```swift
extension ReaderScreenViewController: PSEditionReaderViewController.MediaDelegate {

    func didTapMedia(atIndex index: Int, in media: [PSEMedia]) {
        // An image or video in an article: open your gallery at that item.
    }

    func didTapReplacedEmbed(atIndex index: Int, originalHTML: String, type: PSEmbedType) {
        // The button that stands in for a third-party embed: show the embed.
    }
}
```

Every method has a default, so leave out the ones you don’t need. The
sections below fill in each one, and [Opening Links](/documentation/PSReader/Handling-Media-and-Link-Taps#Opening-Links) adds the link
observer. The reader holds its media delegate weakly, so the screen,
which owns the reader, is a good fit. In Swift 6 language mode, mark the
conformance `@preconcurrency`; see [Swift 6 Language Mode](/documentation/PSReader/Hosting-the-Reader#Swift-6-Language-Mode).

The delegate also changes how pages render. The reader swaps third-party
embeds for buttons only when it has a media delegate, so implement
[`didTapReplacedEmbed(atIndex:originalHTML:type:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapReplacedEmbed(atIndex:originalHTML:type:))
whenever you set one. Without a delegate, the reader leaves embeds inline
in the article, ignores image and template media taps, and loads article
HTML without the page’s base URL. PDF hotspots get the standard overlays
either way.

## Opening a Gallery

A tap on an article’s image calls
[`didTapMedia(atIndex:in:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapMedia(atIndex:in:))
with the page’s whole media list: [`PSEMedia`](/documentation/PSReader/PSEMedia) values holding each
[`PSEImage`](/documentation/PSReader/PSEImage) and [`PSEVideo`](/documentation/PSReader/PSEVideo), plus the page’s adverts. The index is the
tapped item’s position in that list. Build your gallery from the images
and videos, and start it at the tapped one:

```swift
func didTapMedia(atIndex index: Int, in media: [PSEMedia]) {
    guard let source else {
        return
    }

    var items: [GalleryItem] = []
    var startIndex = 0

    for (offset, item) in media.enumerated() {
        if offset == index {
            startIndex = items.count
        }

        switch item {
        case .image(let image):
            items.append(.image(candidates: image.URLs,
                                caption: image.imagecaption,
                                credit: image.imagecredit))
        case .video(let video):
            items.append(.video(video))
        default:
            break   // Adverts.
        }
    }

    let gallery = GalleryViewController(items: items, startIndex: startIndex, source: source)
    present(gallery, animated: true)
}
```

`GalleryItem` and `GalleryViewController` stand for your own UI. An
image’s [`URLs`](/documentation/PSReader/PSEImage/URLs) are candidates in order of preference: resolve
them through the source’s [`resourceManager`](/documentation/PSReader/PSEEditionSource/resourceManager), as in
[Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser), so downloaded editions load from disk.

## Playing Videos

Videos reach your gallery as [`PSEMedia.video(_:)`](/documentation/PSReader/PSEMedia/video(_:)) items. A [`PSEVideo`](/documentation/PSReader/PSEVideo)
has no playable URL: it names the video on your video platform, and you
resolve it to a stream with that platform’s SDK or playback API.
[Playing Videos](/documentation/PSReader/Media-and-Links#Playing-Videos) describes its properties and shows an
`AVPlayerViewController` that resolves the stream as it plays; use the
same code in your gallery.

## Handling Template Media

Some article templates render their own media objects, such as slideshows
and videos, and report taps on them to
[`didTapMediaObject(_:in:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapMediaObject(_:in:))
as a [`PSEMediaObject`](/documentation/PSReader/PSEMediaObject). The prebuilt reader ignores these taps. To handle
them, present the images, or play the video it names by its
[`brightcoveID`](/documentation/PSReader/PSEMediaObject/brightcoveID):

```swift
func didTapMediaObject(_ mediaObject: PSEMediaObject, in page: PSEPage) {
    guard let source else {
        return
    }

    if let images = mediaObject.images, !images.isEmpty {
        let items = images.map {
            GalleryItem.image(candidates: $0.URLs, caption: $0.imagecaption, credit: $0.imagecredit)
        }
        present(GalleryViewController(items: items, startIndex: 0, source: source), animated: true)
    } else if let videoID = mediaObject.brightcoveID {
        playVideo(videoID: videoID)
    }
}
```

`playVideo(videoID:)` stands for your video platform’s player.

## Showing Third-Party Embeds

The reader replaces each Twitter, Instagram, or TikTok post, and each
`<iframe>` and `<embed>` element, in article text with a button labeled
with the [`LocalizedStringKey.tapToOpenEmbed`](/documentation/PSReader/LocalizedStringKey/tapToOpenEmbed) string, so third-party
content loads only when the user asks for it. A tap calls
[`didTapReplacedEmbed(atIndex:originalHTML:type:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapReplacedEmbed(atIndex:originalHTML:type:))
with the embed’s original HTML and its [`PSEmbedType`](/documentation/PSReader/PSEmbedType).

The HTML is the embed’s element alone, without the script that loads its
platform’s widget, so add that script when you present it:

```swift
func didTapReplacedEmbed(atIndex index: Int, originalHTML: String, type: PSEmbedType) {
    let script = switch type {
    case .twitter:        #"<script async src="https://platform.twitter.com/widgets.js"></script>"#
    case .instagram:      #"<script async src="https://www.instagram.com/embed.js"></script>"#
    case .tiktok:         #"<script async src="https://www.tiktok.com/embed.js"></script>"#
    default:              ""
    }

    present(EmbedViewController(html: originalHTML + script), animated: true)
}
```

`EmbedViewController` stands for your own web view screen.

## Customizing Hotspot Overlays

The reader asks
[`mediaOverlay(for:in:superview:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/mediaOverlay(for:in:superview:))
for the overlay to lay over each PDF hotspot. The default returns the
standard overlays: [`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay) for `link` hotspots and
[`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay) for `article` hotspots. Other types get none.

When you implement the method, `nil` leaves a hotspot without an overlay,
so return
[`defaultMediaOverlay(for:in:superview:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/defaultMediaOverlay(for:in:superview:))
for the hotspots you don’t customize:

```swift
func mediaOverlay(for mediaObject: PSEMediaObject, in page: PSEPage, superview: UIView) -> PSEMediaOverlay? {
    guard let videoID = mediaObject.brightcoveID else {
        return defaultMediaOverlay(for: mediaObject, in: page, superview: superview)
    }
    return InlineVideoOverlay(page: page, mediaObject: mediaObject, videoID: videoID)
}
```

`InlineVideoOverlay` is a [`PSEMediaOverlay`](/documentation/PSReader/PSEMediaOverlay) subclass that plays a video
hotspot inline while its page is on screen.
[Custom Hotspot Overlays](/documentation/PSReader/Media-and-Links#Custom-Hotspot-Overlays) builds it, and explains the
overlay’s lifecycle and how its taps coexist with double-tap zoom.

## Opening Links

The reader opens some links itself and posts
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification) for the rest,
with the `URL` under [`linkTappedURLKey`](/documentation/PSReader/PSEditionReaderViewController/linkTappedURLKey):

|Tapped                                                                                                     |What the reader does                                                                                                                                                                                                                      |
|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|A link in an article or other templated page                                                               |Opens `mailto:` links through the system. Posts the notification for every other URL, `tel:` and `sms:` included, and for a template’s `window.open` calls.                                                                               |
|A `link` hotspot                                                                                           |Jumps within the edition for a `pagejump://` target. Posts the notification for `http` and `https` URLs, adding `https://` to a target without a scheme. Opens any other scheme, such as `mailto:`, `tel:`, or `sms:`, through the system.|
|An `article` hotspot                                                                                       |Jumps to the article’s page.                                                                                                                                                                                                              |
|An advert page’s clickthrough                                                                              |Posts the notification, `window.open` calls included. This applies to the built-in advert rendering.                                                                                                                                      |
|A link on an external web page (``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isExternal``)|Follows the link inside the page. Opens `mailto:` links and links to PDF files through the system.                                                                                                                                        |

Links in the notification open only once you observe it. Observe it
while your reader screen is on screen, with no `object` filter, since
content links post it without a sender. In the class, add:

```swift
override func viewDidAppear(_ animated: Bool) {
    super.viewDidAppear(animated)

    // The reader leaves most links for the app to open, and posts them
    // app-wide. Follow them only while this screen is on screen.
    NotificationCenter.default.addObserver(
        self,
        selector: #selector(linkTapped),
        name: PSEditionReaderViewController.linkTappedNotification,
        object: nil
    )
}

override func viewDidDisappear(_ animated: Bool) {
    super.viewDidDisappear(animated)

    NotificationCenter.default.removeObserver(
        self,
        name: PSEditionReaderViewController.linkTappedNotification,
        object: nil
    )
}
```

And in an extension, open each link by its scheme. Add
`import SafariServices` at the top of the file:

```swift
extension ReaderScreenViewController {

    /// Opens a link the user tapped in the edition: web links in Safari
    /// inside the app, and anything else, such as `tel:`, through the
    /// system.
    @objc private func linkTapped(_ notification: Notification) {
        guard let url = notification.userInfo?[PSEditionReaderViewController.linkTappedURLKey] as? URL else {
            return
        }

        switch url.scheme?.lowercased() {
        case "http", "https":
            present(SFSafariViewController(url: url), animated: true)
        default:
            // Safari view controllers take only web URLs.
            UIApplication.shared.open(url)
        }
    }
}
```

The sample app’s reader screen does the same. To report link taps to
your analytics, see
[Reporting Shares, Searches, and Links](/documentation/PSReader/Reporting-Analytics#Reporting-Shares-Searches-and-Links).

Hotspot jumps reach your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) with a
[`PageJumpNavigationSource`](/documentation/PSReader/PageJumpNavigationSource) that carries the page the jump started from,
which a back button can return to; see [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

## Supplying Template Details

Two more methods feed article templates.
[`baseURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/baseURL(for:)) is the base
URL a page’s HTML loads against, by default the page’s own
[`baseURL`](/documentation/PSReader/PSEPage/baseURL); return your publication’s website for pages that
have none. The built-in advert rendering tries it first too, for advert
content’s web origin (see
[Giving Third-Party Adverts an Origin](/documentation/PSReader/Handling-Advert-Pages#Giving-Third-Party-Adverts-an-Origin)).
[`editionLogoURL(for:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/editionLogoURL(for:)) is
the logo image URL for templates that show one, by default none; the
prebuilt reader returns the publication’s header logo.

## Topics

### Third-Party Embeds

[`PSEmbedType`](/documentation/PSReader/PSEmbedType)

The kind of third-party embed a placeholder stands in for, as reported
by [`didTapReplacedEmbed(atIndex:originalHTML:type:)`](/documentation/PSReader/PSEditionReaderViewController/MediaDelegate-swift.protocol/didTapReplacedEmbed(atIndex:originalHTML:type:)).

