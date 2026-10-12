<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Media-and-Links",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Media and Links"
}
-->

# Media and Links

Play videos and customize PDF hotspots in the prebuilt reader, which opens
the images, embeds, and links in edition pages itself.

## Overview

The prebuilt reader handles the interactive content in edition pages: it
opens links, shows article images in a gallery, and follows the hotspots
on PDF pages. Building a custom UI? See
[Handling Media and Link Taps](/documentation/PSReader/Handling-Media-and-Link-Taps).

Two things need your app: video playback, because the SDK has no video
player, and overlays for hotspots the reader doesn’t handle. Both come
from a [`MediaDelegate`](/documentation/PSReader/MediaDelegate). Pass it when you create your global
configuration, and every prebuilt reader uses it:

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID",
    mediaDelegate: AppMedia()
)
```

`AppMedia` is built in [Playing Videos](/documentation/PSReader/Media-and-Links#Playing-Videos) and
[Custom Hotspot Overlays](/documentation/PSReader/Media-and-Links#Custom-Hotspot-Overlays).

The reader treats each kind of interactive content like this:

- **Links.** Web links open in a Safari view controller over the
  reader. <doc://com.pagesuite.PSReader/documentation/PSReader/Media-and-Links#Links> covers every kind of link.
- **Images and videos.** Tapping an article’s image opens a full-screen
  gallery of the page’s images and videos, starting at the one tapped.
  Videos play only through your delegate.
- **Third-party embeds.** Twitter, Instagram, and TikTok posts, and
  `<iframe>` and `<embed>` elements, in article text appear as a button
  labeled with the ``doc://com.pagesuite.PSReader/documentation/PSReader/LocalizedStringKey/tapToOpenEmbed`` string, so
  third-party content loads only when the user asks for it. The button
  opens the embed in a sheet.
- **PDF hotspots.** Tappable regions of PDF pages, listed in
  ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/mediaObjects`` as ``doc://com.pagesuite.PSReader/documentation/PSReader/PSEMediaObject`` values. A `link` hotspot
  follows its target, an `article` hotspot jumps to the article’s page,
  and other types do nothing unless you add an overlay.
- **Template media.** Taps on the slideshows and videos that some
  article templates render themselves have no effect.

![The prebuilt reader's full-screen gallery showing the first of an article's two images, with its caption and a page indicator.](images/com.pagesuite.PSReader/media-reader-gallery@2x.png)

## Playing Videos

The SDK doesn’t include a video player, and a [`PSEVideo`](/documentation/PSReader/PSEVideo) has no playable
URL. It names the video on its video platform: [`videoID`](/documentation/PSReader/PSEVideo/videoID) is the
video’s ID there, and [`videoAccountID`](/documentation/PSReader/PSEVideo/videoAccountID) and
[`videoAccountPolicy`](/documentation/PSReader/PSEVideo/videoAccountPolicy) identify the account that hosts it, such as
a Brightcove account ID and policy key. Resolve them to a stream with your
platform’s SDK or playback API. [`videoImageURLs`](/documentation/PSReader/PSEVideo/videoImageURLs) lists the
poster image, and [`videoCaption`](/documentation/PSReader/PSEVideo/videoCaption) holds the caption.

Return a player from
[`videoViewController(for:presentingFrom:)`](/documentation/PSReader/MediaDelegate/videoViewController(for:presentingFrom:)). The gallery
embeds the view controller in place of the video’s poster, so return it at
once and load the stream inside it:

```swift
import AVKit
import PSReader

struct AppMedia: MediaDelegate {

    func videoViewController(for video: PSEVideo, presentingFrom: UIViewController) -> UIViewController? {
        guard let videoID = video.videoID else {
            return nil
        }

        let playerViewController = AVPlayerViewController()

        Task {
            // Your video platform's playback lookup.
            guard let streamURL = try? await VideoPlatform.streamURL(
                videoID: videoID,
                accountID: video.videoAccountID,
                policyKey: video.videoAccountPolicy
            ) else {
                return
            }
            playerViewController.player = AVPlayer(url: streamURL)
        }

        return playerViewController
    }
}
```

Return `nil` for a video you can’t play: the gallery shows the poster
image and an error alert instead. Without a [`MediaDelegate`](/documentation/PSReader/MediaDelegate), every video
behaves that way.

> Replica: Replica editions open in the legacy replica reader, which
> doesn’t call ``doc://com.pagesuite.PSReader/documentation/PSReader/MediaDelegate``. Neither videos nor custom hotspot
> overlays apply to them.

## Custom Hotspot Overlays

By default, the reader covers `link` hotspots with a
[`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay) and `article` hotspots with a
[`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay), matching the type case-insensitively. Hotspots
of any other type, video hotspots included, get no overlay and do nothing
when tapped.

![A PDF page in the prebuilt reader with its five article hotspots highlighted, and callouts naming the page's media objects and the article overlay. The highlights are for illustration; these hotspots have no visible background or border.](images/com.pagesuite.PSReader/media-pdf-hotspots-annotated@2x.png)

Subclass [`PSEMediaOverlay`](/documentation/PSReader/PSEMediaOverlay) to handle another type or to change the look.
The base initializer applies the hotspot’s background and border, the
reader sizes the view to the hotspot, and [`isInView()`](/documentation/PSReader/PSEMediaOverlay/isInView())
and [`isOutOfView()`](/documentation/PSReader/PSEMediaOverlay/isOutOfView()) fire as the hotspot’s page becomes
current and stops being current. This overlay plays a video hotspot inline
while its page is on screen:

```swift
import AVFoundation
import PSReader

final class InlineVideoOverlay: PSEMediaOverlay {
    private let player = AVPlayer()
    private let playerLayer = AVPlayerLayer()

    init(page: PSEPage, mediaObject: PSEMediaObject, videoID: String) {
        super.init(page: page, mediaObject: mediaObject)
        playerLayer.player = player
        layer.addSublayer(playerLayer)

        Task { [player] in
            // Your video platform's playback lookup.
            guard let streamURL = try? await VideoPlatform.streamURL(videoID: videoID) else {
                return
            }
            player.replaceCurrentItem(with: AVPlayerItem(url: streamURL))
        }
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func layoutSubviews() {
        super.layoutSubviews()
        playerLayer.frame = bounds
    }

    // The reader calls these as the hotspot's page comes and goes.
    override func isInView() {
        player.play()
    }

    override func isOutOfView() {
        player.pause()
    }
}
```

Return the overlay from your delegate’s
[`pdfMediaOverlay(for:in:superview:)`](/documentation/PSReader/MediaDelegate/pdfMediaOverlay(for:in:superview:)). Returning `nil`
keeps the built-in overlay, so return `nil` for every hotspot you don’t
customize:

```swift
extension AppMedia {
    func pdfMediaOverlay(for mediaObject: PSEMediaObject, in page: PSEPage, superview: UIView) -> PSEMediaOverlay? {
        guard let videoID = mediaObject.brightcoveID else {
            return nil
        }
        return InlineVideoOverlay(page: page, mediaObject: mediaObject, videoID: videoID)
    }
}
```

The `superview` argument is the page view the reader adds the overlay to.
The built-in overlays make their taps wait for its double-tap gesture
recognizers to fail, so double-tap zoom keeps working over a hotspot. Do
the same if your overlay responds to taps.

## Changing Media Handling for One Reader

Configurations copy the delegate when you create them (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)), so set it on the global configuration
first. To give one reader a different delegate, or none, set
[`mediaDelegate`](/documentation/PSReader/ReaderConfiguration/mediaDelegate) on that reader’s configuration: the
`readerConfig` of a carousel section or prebuilt screen, or the reader
configuration you pass to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
// A carousel section whose readers don't play videos
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.mediaDelegate = nil

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig)
    ]
)

// A reader with media handling of its own
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.mediaDelegate = KioskMedia()

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

## Links

The prebuilt reader opens every link itself:

|Tapped                                                                                                     |What the prebuilt reader does                                                                                                                                                                                                                    |
|-----------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|A link in an article or other templated page                                                               |Opens `http` and `https` URLs in a Safari view controller, and `mailto:` links through the system. Any other URL, `tel:` and `sms:` included, opens in an in-app web view. A template’s `window.open` calls work the same way.                   |
|A `link` hotspot                                                                                           |Jumps within the edition for a `pagejump://` target. Opens `http` and `https` URLs in a Safari view controller, adding `https://` to a target without a scheme. Opens any other scheme, such as `mailto:`, `tel:`, or `sms:`, through the system.|
|An `article` hotspot                                                                                       |Jumps to the article’s page.                                                                                                                                                                                                                     |
|An advert page’s clickthrough                                                                              |Opens `http` and `https` URLs in a Safari view controller, and any other URL in an in-app web view, `window.open` calls included. This applies to the built-in advert rendering.                                                                 |
|A link on an external web page (``doc://com.pagesuite.PSReader/documentation/PSReader/PSEPage/isExternal``)|Follows the link inside the page. Opens `mailto:` links and links to PDF files through the system.                                                                                                                                               |

Before the reader presents a link in a Safari view controller or an
in-app web view, it posts
[`linkTappedNotification`](/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification), with the `URL`
under [`linkTappedURLKey`](/documentation/PSReader/PSEditionReaderViewController/linkTappedURLKey); the prebuilt
reader observes it while it’s visible and presents the URL. Your
app can observe it too, for analytics say, but shouldn’t present anything,
since the reader already does.

> Replica: Replica editions open in the legacy replica reader, which
> handles their links itself; the table above doesn’t apply to them.

## Topics

### Media Delegate

[`MediaDelegate`](/documentation/PSReader/MediaDelegate)

Defines methods to provide custom media functionality.

### Hotspot Overlays

[`PSEMediaOverlay`](/documentation/PSReader/PSEMediaOverlay)

A view the reader lays over a page’s media hotspot region.

[`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay)

The standard overlay for `link`-type hotspots: a tap follows the
hotspot’s `target`.

[`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay)

The standard overlay for `article`-type hotspots: a tap jumps the reader
to the linked article’s page.

