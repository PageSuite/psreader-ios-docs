<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Adding-a-Listen-Button",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Adding a Listen Button"
}
-->

# Adding a Listen Button

Add a listen button to your own reader screen that reads the article in view aloud, with the SDK’s text-to-speech provider.

## Overview

The prebuilt reader shows a listen button on pages with one article. A
tap reads the article aloud and opens playback controls.
[`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) does everything but the button, on core
models, so your reader screen can use it unchanged: you add the button,
tell the provider which page is on screen, and present the controls it
returns.

Using the prebuilt UI? See [Text-to-Speech](/documentation/PSReader/Text-to-Speech).

Add a provider and the button to `ReaderScreenViewController`, the
reader screen from [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader):

```swift
private let textToSpeech = DefaultTextToSpeechProvider(
    configuration: AudioOverlayConfiguration(
        globalConfig: GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")
    )
)

private lazy var listenButton = UIBarButtonItem(
    image: UIImage(systemName: "headphones"),
    style: .plain,
    target: self,
    action: #selector(listenTapped)
)
```

Keep one provider for the life of the screen: it holds the article that’s
playing. [`AudioOverlayConfiguration`](/documentation/PSReader/AudioOverlayConfiguration) takes the controls’ starting fonts,
colors, and icons from a [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), which you can create
just for it; see [Styling the Controls](/documentation/PSReader/Adding-a-Listen-Button#Styling-the-Controls).

## Showing the Button on Listenable Pages

In `addChrome()`, put the button in the navigation bar, disabled until
the first page settles:

```swift
listenButton.isEnabled = false
navigationItem.rightBarButtonItems = (navigationItem.rightBarButtonItems ?? []) + [listenButton]
```

In `updateChrome()`, report each page the reader settles on to the
provider, and enable the button when the provider can read the page. It
can read a page that carries exactly one article in
[`articles`](/documentation/PSReader/PSEPage/articles), as an article page does:

```swift
if let source {
    textToSpeech.didChangeTo(page: page, inEdition: source.edition, inPublished: source.published)
    listenButton.isEnabled = textToSpeech.isListenable(page: page, inEdition: source)
}
```

Reporting the page also keeps playback in step with the reader. When the
reader settles on a page whose article isn’t the one playing, the
provider lets the article go: playback stops and the audio session is
deactivated. [Following Page Changes](/documentation/PSReader/Text-to-Speech#Following-Page-Changes) has the details.

## Starting Playback

Add the action in an extension, in the same file as the class. On a tap,
ask the provider for the page’s overlay. The call starts the article,
and the overlay holds its controls: play and pause, 15-second skips, a
progress bar the user can scrub, and elapsed and remaining times. It
arrives sized to fit them and stays a popover in compact widths, so a
popover from your button suits iPhone and iPad alike:

```swift
extension ReaderScreenViewController {

    @objc private func listenTapped() {
        guard let source,
              let page = reader.currentPage(),
              let overlay = textToSpeech.playAudio(for: page, inEdition: source) else {
            return
        }

        overlay.modalPresentationStyle = .popover
        overlay.popoverPresentationController?.barButtonItem = listenButton
        present(overlay, animated: true)
    }
}
```

The default synthesizer renders the whole article before playback starts,
so the overlay shows a loading state first. Closing the overlay doesn’t
stop playback, and tapping the button again on the same article brings
back its controls rather than starting over.

## Stopping When the Screen Closes

The prebuilt reader reports no page when its screen goes away, which
stops playback. Do the same in your screen’s class:

```swift
override func viewWillDisappear(_ animated: Bool) {
    super.viewWillDisappear(animated)

    if let source, isMovingFromParent || isBeingDismissed || parent?.isBeingDismissed == true {
        textToSpeech.didChangeTo(page: nil, inEdition: source.edition, inPublished: source.published)
    }
}
```

## Styling the Controls

The overlay takes its brand color, primary font, icons, and Liquid Glass
policy from the [`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration) you give its configuration. Pass
your own to match your chrome, then adjust any
[`AudioOverlayConfiguration`](/documentation/PSReader/AudioOverlayConfiguration) property:

```swift
private let textToSpeech: DefaultTextToSpeechProvider = {
    var overlayConfig = AudioOverlayConfiguration(
        globalConfig: GlobalConfiguration(
            apiKey: "API_KEY",
            accountGUID: "ACCOUNT_GUID",
            primaryFont: UIFont(name: "Georgia", size: 14) ?? .systemFont(ofSize: 14),
            brandColor: .systemIndigo
        )
    )
    overlayConfig.backgroundColor = .secondarySystemBackground
    return DefaultTextToSpeechProvider(configuration: overlayConfig)
}()
```

[Styling the Overlay](/documentation/PSReader/Text-to-Speech#Styling-the-Overlay) lists every property, and the
localization keys for the overlay’s text. Your button is yours to design;
to match the prebuilt reader’s, use its icon and title. In `addChrome()`:

```swift
listenButton.image = ImageResourceName.listen.defaultImage()
listenButton.accessibilityLabel = LocalizationManager.shared.localizedString(for: .listen)
```

## Changing the Voice, Text, or Audio Session

The provider’s other parts change exactly as they do in the prebuilt
reader: pass your own to its initializer, and it uses the SDK’s part for
each one you leave out.

- A ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechSynthesizer`` for another voice, such as a cloud
  service’s; see <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech#Choosing-a-Voice>.
- A ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechArticleFormatter`` to change what’s read; see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech#Changing-the-Spoken-Text>.
- An ``doc://com.pagesuite.PSReader/documentation/PSReader/AudioSessionProvider`` to set up the audio session differently,
  for example to lower other apps’ audio; see
  <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech#Managing-the-Audio-Session>.

## Using Your Own Audio Delegate

Any [`AudioDelegate`](/documentation/PSReader/AudioDelegate) works behind your button, not only
[`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider): call its
[`isListenable(page:inEdition:)`](/documentation/PSReader/AudioDelegate/isListenable(page:inEdition:)),
[`playAudio(for:inEdition:)`](/documentation/PSReader/AudioDelegate/playAudio(for:inEdition:)), and
[`didChangeTo(page:inEdition:inPublished:)`](/documentation/PSReader/AudioDelegate/didChangeTo(page:inEdition:inPublished:)) the same way.
Present the overlay when `playAudio` returns one; a delegate that returns
`nil` plays without one. Nothing in a custom UI asks for
[`audioBannerViewController()`](/documentation/PSReader/AudioDelegate/audioBannerViewController()), so put a delegate’s own
controls wherever your screen has room.
[Writing Your Own Audio Delegate](/documentation/PSReader/Text-to-Speech#Writing-Your-Own-Audio-Delegate) shows a delegate
that plays through the app’s player.