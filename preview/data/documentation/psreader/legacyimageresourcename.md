<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LegacyImageResourceName",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23LegacyImageResourceNameO"
  },
  "title" : "LegacyImageResourceName"
}
-->

# LegacyImageResourceName

Enumeration of asset identifiers used specifically by the legacy reader.

```
enum LegacyImageResourceName
```

## Overview

Implement `AssetDelegate` to provide custom assets, replacing the legacy reader’s default images.

## Topics

### Getting the Built-In Image

[`defaultImage()`](/documentation/PSReader/LegacyImageResourceName/defaultImage())

Returns the UIImage associated with the legacy asset name.

### Reader Navigation Bar

[`LegacyImageResourceName.readerBack`](/documentation/PSReader/LegacyImageResourceName/readerBack)

The back button that closes the reader.

[`LegacyImageResourceName.pageBrowserInactive`](/documentation/PSReader/LegacyImageResourceName/pageBrowserInactive)

The page browser button while the page browser is closed.

[`LegacyImageResourceName.pageBrowserActive`](/documentation/PSReader/LegacyImageResourceName/pageBrowserActive)

The page browser button while the page browser is open.

[`LegacyImageResourceName.share`](/documentation/PSReader/LegacyImageResourceName/share)

The share button.

[`LegacyImageResourceName.print`](/documentation/PSReader/LegacyImageResourceName/print)

The print button.

[`LegacyImageResourceName.bookmarkInactive`](/documentation/PSReader/LegacyImageResourceName/bookmarkInactive)

The bookmark button when the current page or article isn’t
bookmarked.

[`LegacyImageResourceName.bookmarkActive`](/documentation/PSReader/LegacyImageResourceName/bookmarkActive)

The bookmark button when the current page or article is bookmarked.

[`LegacyImageResourceName.singlePageMode`](/documentation/PSReader/LegacyImageResourceName/singlePageMode)

The page-mode button while the reader shows double-page spreads;
tapping it switches to single pages.

[`LegacyImageResourceName.doublePageMode`](/documentation/PSReader/LegacyImageResourceName/doublePageMode)

The page-mode button while the reader shows single pages; tapping it
switches to double-page spreads.

[`LegacyImageResourceName.puzzle`](/documentation/PSReader/LegacyImageResourceName/puzzle)

The puzzles button.

[`LegacyImageResourceName.showNavigationBar`](/documentation/PSReader/LegacyImageResourceName/showNavigationBar)

The expand button, which hides the navigation bars to show pages full
screen.

### Article Navigation Bar

[`LegacyImageResourceName.articlePopOverBack`](/documentation/PSReader/LegacyImageResourceName/articlePopOverBack)

The close button in the navigation bar of an article opened from a
page.

[`LegacyImageResourceName.textSizeInactive`](/documentation/PSReader/LegacyImageResourceName/textSizeInactive)

The text size button while the text size controls are closed.

[`LegacyImageResourceName.textSizeActive`](/documentation/PSReader/LegacyImageResourceName/textSizeActive)

The text size button in an article’s navigation bar while the text
size controls are open.

[`LegacyImageResourceName.textToSpeechInactive`](/documentation/PSReader/LegacyImageResourceName/textToSpeechInactive)

The text-to-speech button while the text-to-speech controls are
closed.

[`LegacyImageResourceName.textToSpeechActive`](/documentation/PSReader/LegacyImageResourceName/textToSpeechActive)

The text-to-speech button in an article’s navigation bar while the
text-to-speech controls are open.

