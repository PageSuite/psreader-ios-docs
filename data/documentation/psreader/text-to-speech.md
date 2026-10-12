<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Text-to-Speech",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Text-to-Speech"
}
-->

# Text-to-Speech

Read articles aloud in the prebuilt reader with the SDK’s text-to-speech
provider, or bring your own voice, text, and audio controls.

## Overview

The prebuilt reader can read the article on screen aloud: a listen button
in its navigation bar starts the article and opens playback controls.
Building a custom UI? See [Adding a Listen Button](/documentation/PSReader/Adding-a-Listen-Button).

Set the SDK’s text-to-speech provider as the global configuration’s audio
delegate to switch it on:

```swift
var globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
globalConfig.audioDelegate = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(globalConfig: globalConfig)
)
```

Every prebuilt reader then has the listen button, whether the carousel
opened the reader or one of your own screens did.

![The text-to-speech overlay reading an article aloud.](images/com.pagesuite.PSReader/tts-overlay~dark@2x.png)

The provider offers audio on pages that carry exactly one article in
[`articles`](/documentation/PSReader/PSEPage/articles), as an article page does, and reads that article.
Pages with several articles or none get no listen button. The default
synthesizer renders the whole article before playback starts, so the
overlay shows a loading state first.

Audio runs through an [`AudioDelegate`](/documentation/PSReader/AudioDelegate), which says whether a page can
play, starts playback when the user taps listen, and hears when the page
changes. [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) is the one the SDK ships, built
from layers you can replace one at a time:

- **Controls.** The provider’s overlay, an ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlay``, has play and
  pause, 15-second skips, a progress bar the user can scrub, and elapsed
  and remaining times. ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration`` styles it.
- **Synthesizer.** A ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechSynthesizer`` turns text into audio.
  ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechSynthesizer`` uses the system’s
  `AVSpeechSynthesizer`.
- **Formatter.** A ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechArticleFormatter`` turns an article into
  the text to speak. ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechArticleFormatter`` reads the
  headline, subheadline, and byline, then the body’s paragraphs and
  headings, with the HTML removed.
- **Audio session.** An ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider`` activates the shared
  `AVAudioSession` before playback and deactivates it afterwards.

> Replica: The audio delegate serves replica editions only when
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` is `false`. The replica
> reader that setting selects shows the same listen button, overlay, and
> banner, and calls the delegate’s replica methods;
> ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider`` reads article spreads. The legacy replica
> reader, the default, doesn’t use the audio delegate.

## Styling the Overlay

[`AudioOverlayConfiguration`](/documentation/PSReader/AudioOverlayConfiguration) styles the default overlay. It starts from
your [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration); change what you need before you create the
provider:

```swift
var overlayConfig = AudioOverlayConfiguration(globalConfig: globalConfig)
overlayConfig.brandColor = .systemIndigo
overlayConfig.backgroundColor = .secondarySystemBackground
overlayConfig.titleLabel.font = UIFont(name: "Georgia-Bold", size: 20) ?? .boldSystemFont(ofSize: 20)
overlayConfig.titleLabel.pointSize = 20
overlayConfig.elapsedLabel.font = .monospacedDigitSystemFont(ofSize: 12, weight: .regular)
overlayConfig.remainingLabel.font = .monospacedDigitSystemFont(ofSize: 12, weight: .regular)

let textToSpeech = DefaultTextToSpeechProvider(configuration: overlayConfig)
```

|Property                                                                                                                                                                                        |Styles                                                                                                                                                                                                                                                                                                                                                      |Starts as                               |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------|
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/brandColor``                                                                                                    |The play, pause, and skip buttons and the progress bar                                                                                                                                                                                                                                                                                                      |The global brand color                  |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/backgroundColor``                                                                                               |The overlay’s background, when it isn’t Liquid Glass                                                                                                                                                                                                                                                                                                        |The SDK’s background color              |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/titleLabel``                                                                                                    |The title                                                                                                                                                                                                                                                                                                                                                   |The global primary font, bold, 18 points|
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/subtitleLabel``                                                                                                 |The line under the title                                                                                                                                                                                                                                                                                                                                    |The global primary font, 14 points      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/elapsedLabel``, ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/remainingLabel``|The times under the progress bar                                                                                                                                                                                                                                                                                                                            |The global primary font, 12 points      |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/assetDelegate``                                                                                                 |The ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName/play``, ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName/pause``, ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName/goBackward15``, and ``doc://com.pagesuite.PSReader/documentation/PSReader/ImageResourceName/goForward15`` icons|The global asset delegate               |
|``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlayConfiguration/liquidGlassPolicy``                                                                                             |Whether the overlay uses Liquid Glass on iOS 26 and later                                                                                                                                                                                                                                                                                                   |The global policy                       |

A label’s `pointSize` sets its size, whatever size its `font` has.

The title and subtitle are fixed strings, not the article’s headline:
“Text to Speech” and “Listen to the article below.” Change them, the
loading and error text, and the listen button’s title through
[`LocalizedStringKey.audioOverlayTitle`](/documentation/PSReader/LocalizedStringKey/audioOverlayTitle),
[`LocalizedStringKey.audioOverlaySubtitle`](/documentation/PSReader/LocalizedStringKey/audioOverlaySubtitle),
[`LocalizedStringKey.audioOverlayLoading`](/documentation/PSReader/LocalizedStringKey/audioOverlayLoading),
[`LocalizedStringKey.audioOverlayError`](/documentation/PSReader/LocalizedStringKey/audioOverlayError), and [`LocalizedStringKey.listen`](/documentation/PSReader/LocalizedStringKey/listen);
see [Localization](/documentation/PSReader/Localization). The listen button’s icon is
[`ImageResourceName.listen`](/documentation/PSReader/ImageResourceName/listen); see [Theming](/documentation/PSReader/Theming).

## Choosing a Voice

[`DefaultTextToSpeechSynthesizer`](/documentation/PSReader/DefaultTextToSpeechSynthesizer) speaks with a standard system voice for
its [`language`](/documentation/PSReader/DefaultTextToSpeechSynthesizer/language), English unless you pass
another language code. For a higher-quality voice, such as one from a cloud
text-to-speech service, implement [`TextToSpeechSynthesizer`](/documentation/PSReader/TextToSpeechSynthesizer) and pass it
to the provider. Formatting, controls, and the audio session stay as they
are:

```swift
struct CloudSynthesizer: TextToSpeechSynthesizer {

    func synthesize(string: String, completion: @escaping (Result<URL, Error>) -> Void) {
        // Send the text to your service, save the audio it returns,
        // and pass back the file's URL.
        CloudVoice.shared.synthesize(string, completion: completion)
    }
}

let textToSpeech = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(globalConfig: globalConfig),
    speechSynthesizer: CloudSynthesizer()
)
```

- **Any URL `AVPlayer` plays.** The provider plays the result with
  `AVPlayer`, so a local file and a streamable remote URL both work.
- **Any queue.** Call `completion` from whichever queue suits you; the
  provider moves to the main queue itself.
- **Errors.** A failure puts the overlay in its error state.
- **Caching.** The provider asks again each time it starts an article
  afresh, including one it played earlier, so cache the audio if your
  service charges per request. The built-in synthesizer keeps its most
  recent result.

Each of the provider’s parameters after `configuration` defaults to the
SDK’s own part, so pass only the parts you replace.

## Changing the Spoken Text

Implement [`TextToSpeechArticleFormatter`](/documentation/PSReader/TextToSpeechArticleFormatter) to control what’s read, for
example to drop boilerplate or add a sign-off. Starting from the default
formatter’s output is often enough:

```swift
struct SignOffFormatter: TextToSpeechArticleFormatter {

    private let standard = DefaultTextToSpeechArticleFormatter()

    func format(article: PSEArticle) throws -> String {
        let text = try standard.format(article: article)
        return text + "\n\nYou've been listening to The Daily Example."
    }
}

let textToSpeech = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(globalConfig: globalConfig),
    articleFormatter: SignOffFormatter()
)
```

To build the text yourself, the default formatter’s sources are
[`headline`](/documentation/PSReader/PSEArticle/headline), [`subheadline`](/documentation/PSReader/PSEArticle/subheadline), [`byline`](/documentation/PSReader/PSEArticle/byline),
and [`story`](/documentation/PSReader/PSEArticle/story), the body as HTML. Return plain text: the
synthesizer reads whatever it gets. A formatter that throws puts the
overlay in its error state.

> Replica: With ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` set to
> `false`, replica articles keep the default formatter’s text unless you
> also implement `format(article:)` for the legacy `PSArticle`.

## Managing the Audio Session

[`DefaultAudioSessionProvider`](/documentation/PSReader/DefaultAudioSessionProvider) sets the shared `AVAudioSession` to the
`.playback` category just before an article’s audio starts, and deactivates
the session when the provider lets that article go. The `.playback`
category keeps speech audible with the Ring/Silent switch set to silent; to
keep playing after the user leaves your app, also add the Audio background
mode to it. [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) pauses for interruptions, such
as a phone call, and resumes afterwards when the system allows it.

Implement [`AudioSessionProvider`](/documentation/PSReader/AudioSessionProvider) to set the session up differently, for
example to lower other apps’ audio instead of stopping it:

```swift
import AVFoundation

struct DuckingAudioSessionProvider: AudioSessionProvider {

    func setupAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws {
        let session = AVAudioSession.sharedInstance()
        try session.setCategory(.playback, mode: .spokenAudio, options: .duckOthers)
        try session.setActive(true)
    }

    func deactivateAudioSession(for article: PSEArticle, inEdition source: PSEEditionSource) throws {
        try AVAudioSession.sharedInstance().setActive(false, options: .notifyOthersOnDeactivation)
    }
}

let textToSpeech = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(globalConfig: globalConfig),
    audioSessionProvider: DuckingAudioSessionProvider()
)
```

An error thrown from setup puts the overlay in its error state; errors from
deactivation are ignored.

> Replica: With ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` set to
> `false`, replica playback keeps the default session unless you also
> implement
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider/setupAudioSession(for:inReplicaEdition:)`` and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider/deactivateAudioSession(for:inReplicaEdition:)``.

## Changing Audio for One Reader

Configurations copy the delegate when you create them (see
[Configuring the Prebuilt UI](/documentation/PSReader/Configuring-the-Prebuilt-UI)), so set it on the global configuration
first. To change audio for one reader, set
[`audioDelegate`](/documentation/PSReader/ReaderConfiguration/audioDelegate) on that reader’s configuration, to
a different delegate or to `nil` to turn audio off. That’s the
`readerConfig` of a carousel section or prebuilt screen, or the reader
configuration you pass to [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController):

```swift
// A carousel section without audio
var archiveConfig = ArchiveConfiguration(globalConfig: globalConfig)
archiveConfig.readerConfig.audioDelegate = nil

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE", config: archiveConfig)
    ]
)

// A reader for a Spanish-language publication
var readerConfig = ReaderConfiguration(globalConfig: globalConfig)
readerConfig.audioDelegate = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(globalConfig: globalConfig),
    speechSynthesizer: DefaultTextToSpeechSynthesizer(language: "es")
)

let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    readerConfig: readerConfig,
    latestEditionForPublication: "PUBLICATION_GUID"
)
```

## Following Page Changes

The prebuilt reader calls
[`didChangeTo(page:inEdition:inPublished:)`](/documentation/PSReader/AudioDelegate/didChangeTo(page:inEdition:inPublished:)) each time a page
settles, including when it settles on the page it was already showing, and
again with a `nil` page when its screen is dismissed.

[`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) ties playback to the article:

- While the settled page’s article is the one playing, playback continues.
- When the reader settles on a page whose article isn’t the one playing, or
  that has none, or reports no page at all, the provider lets the article
  go: playback stops and the audio session is deactivated.
- Coming back to the article later and tapping listen starts it again from
  the beginning.

A delegate of your own gets the same calls: pause, stop, or update your
banner there. The method is optional.

## Overlays and Banners

An [`AudioDelegate`](/documentation/PSReader/AudioDelegate) offers playback controls in two ways, and can use both:

- **Overlay.** ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)`` returns an
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioOverlay`` each time the user taps listen, and the prebuilt reader
  presents it. Return `nil` to present nothing, for example when the tap
  starts playback in your banner.
- **Banner.** ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/audioBannerViewController()`` returns an
  ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioBannerViewController`` that stays at the bottom of the reader as
  the user turns pages. The prebuilt reader asks for it once for each
  edition it opens, so return a new one each time.

[`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) uses the overlay and returns no banner.

In the prebuilt reader, the overlay slides down from under the navigation
bar and dims the page in compact widths, such as on iPhone. In regular
widths, and wherever the navigation bar uses Liquid Glass (iOS 26 and
later), it opens as a popover from the listen button, 240 points tall and
up to 500 wide. Tapping outside closes it.

For an overlay of your own design, subclass [`AudioOverlay`](/documentation/PSReader/AudioOverlay) and return it
from your own delegate; [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) always returns its
own. When the prebuilt reader presents the overlay as a popover,
[`viewWillAppear(_:)`](/documentation/PSReader/AudioOverlay/viewWillAppear(_:)) and [`viewWillDisappear(_:)`](/documentation/PSReader/AudioOverlay/viewWillDisappear(_:))
highlight its listen button, so call `super` if you override them.

![A persistent audio banner shown with the reader.](images/com.pagesuite.PSReader/tts-banner@2x.png)

A banner’s [`isFloating`](/documentation/PSReader/AudioBannerViewController/isFloating) decides where it sits:

- `true`: the banner floats over the bottom of the pages, just above any
  bottom advert banner, and the reader insets its content by the banner’s
  height so nothing hides behind it.
- `false`: the banner sits below the reader and any bottom advert banner,
  and the reader gets shorter to make room.

```swift
final class NowPlayingBanner: UIViewController, AudioBannerViewController {

    var isFloating: Bool { true }

    override func viewDidLoad() {
        super.viewDidLoad()
        // Build compact controls: play and pause, progress, the article's title.
    }
}
```

The banner’s height decides whether it shows. Give its view a height
through Auto Layout to show it, and collapse the height to zero to hide it;
the SDK never tells it to appear or disappear, so drive it from your own
audio state. The banner can reach the bottom edge of the screen, so lay out
its controls against its `safeAreaLayoutGuide`.

## Writing Your Own Audio Delegate

Implement [`AudioDelegate`](/documentation/PSReader/AudioDelegate) when the default provider’s player doesn’t fit:
your own player or “now playing” banner, lock-screen controls (the default
provider publishes no Now Playing information), or a different rule for
which pages can play. The SDK’s formatter and synthesizer still work on
their own. This delegate plays through the app’s player and shows its
controls in a banner instead of an overlay:

```swift
final class BannerAudioDelegate: AudioDelegate {

    private let formatter = DefaultTextToSpeechArticleFormatter()
    private let synthesizer = DefaultTextToSpeechSynthesizer()
    private let player = AppAudioPlayer.shared   // your player; the banner observes it

    func isListenable(page: PSEPage, inEdition source: PSEEditionSource) -> Bool {
        page.articles?.count == 1
    }

    func playAudio(for page: PSEPage, inEdition source: PSEEditionSource) -> AudioOverlay? {
        guard let article = page.articles?.first,
              let text = try? formatter.format(article: article) else { return nil }

        synthesizer.synthesize(string: text) { [player] result in
            guard case .success(let url) = result else { return }
            DispatchQueue.main.async {
                player.play(url, title: article.headline ?? "")
            }
        }
        return nil   // no overlay: the banner shows the controls
    }

    func audioBannerViewController() -> AudioBannerViewController? {
        NowPlayingBanner()
    }

    func didChangeTo(page: PSEPage?, inEdition edition: PSEEdition, inPublished published: PSEPublished) {
        if page == nil {
            player.stop()   // the reader closed; otherwise keep playing across pages
        }
    }
}
```

Set it wherever you’d set [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider). The prebuilt
reader asks [`isListenable(page:inEdition:)`](/documentation/PSReader/AudioDelegate/isListenable(page:inEdition:)) about each page
it moves to, to show or hide its listen button, and calls
[`playAudio(for:inEdition:)`](/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)) with the current page when the
user taps the button. In a double-page spread, that’s the page that
represents the spread.

> Replica: A delegate of your own offers no audio in replica editions
> unless it also implements
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/isListenable(spread:inReplicaEdition:)`` and
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/playAudio(forSpread:inReplicaEdition:)``, plus
> ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioDelegate/didChangeTo(spread:inReplicaEdition:)`` if it follows
> page changes. Only the replica reader that
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader`` set to `false` selects
> calls them; the legacy replica reader never uses the audio delegate.

## Topics

### Text-to-Speech Provider

[`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider)

A complete text-to-speech implementation providing ready-to-use audio functionality.

### Styling the Overlay

[`AudioOverlayConfiguration`](/documentation/PSReader/AudioOverlayConfiguration)

Configuration structure for customizing the appearance of audio overlays.

### Voices and Spoken Text

[`TextToSpeechSynthesizer`](/documentation/PSReader/TextToSpeechSynthesizer)

Protocol for synthesizing text into speech audio.

[`DefaultTextToSpeechSynthesizer`](/documentation/PSReader/DefaultTextToSpeechSynthesizer)

Default implementation of text-to-speech synthesis using the system’s TTS capabilities.

[`TextToSpeechArticleFormatter`](/documentation/PSReader/TextToSpeechArticleFormatter)

Protocol for formatting articles into text suitable for speech synthesis.

[`DefaultTextToSpeechArticleFormatter`](/documentation/PSReader/DefaultTextToSpeechArticleFormatter)

Default implementation of text-to-speech article formatting.

### Audio Sessions

[`AudioSessionProvider`](/documentation/PSReader/AudioSessionProvider)

Protocol for managing audio session lifecycle and interruption handling.

[`DefaultAudioSessionProvider`](/documentation/PSReader/DefaultAudioSessionProvider)

Default implementation of audio session management.

### Custom Playback Controls

[`AudioDelegate`](/documentation/PSReader/AudioDelegate)

Delegate protocol used to provide audio playback functionality within the SDK.

[`AudioOverlay`](/documentation/PSReader/AudioOverlay)

A custom view controller designed for presenting audio playback interfaces as overlays.

[`AudioBannerViewController`](/documentation/PSReader/AudioBannerViewController)

A view controller used to present persistent audio controls as a banner.

