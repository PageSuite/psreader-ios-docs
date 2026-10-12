<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ImageResourceName",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17ImageResourceNameO"
  },
  "title" : "ImageResourceName"
}
-->

# ImageResourceName

An enumeration of asset identifiers used by the SDK’s UI components.

```
enum ImageResourceName
```

## Overview

Each case represents a customizable icon or image in the SDK. Implement
[`AssetDelegate`](/documentation/PSReader/AssetDelegate) to override any of these defaults with your own assets.
Call [`defaultImage()`](/documentation/PSReader/ImageResourceName/defaultImage()) on any case to retrieve the SDK’s built-in image.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Theming>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AssetDelegate``

## Topics

### Getting the Built-In Image

[`defaultImage()`](/documentation/PSReader/ImageResourceName/defaultImage())

Returns the SDK’s built-in image for the asset.

### Reader Navigation Bar

[`ImageResourceName.dismiss`](/documentation/PSReader/ImageResourceName/dismiss)

Back/dismiss button in the reader navigation bar.

[`ImageResourceName.dismissGlass`](/documentation/PSReader/ImageResourceName/dismissGlass)

Back/dismiss button styled for Liquid Glass navigation bars (iOS 26+).

[`ImageResourceName.dismissArticle`](/documentation/PSReader/ImageResourceName/dismissArticle)

Close button shown when dismissing an article popover back to the PDF page.

[`ImageResourceName.listen`](/documentation/PSReader/ImageResourceName/listen)

Text-to-speech listen button in the reader navigation bar.

[`ImageResourceName.share`](/documentation/PSReader/ImageResourceName/share)

Share button in the reader navigation bar.

[`ImageResourceName.bookmark`](/documentation/PSReader/ImageResourceName/bookmark)

Inactive bookmark icon indicating the current page is not bookmarked.

[`ImageResourceName.bookmarked`](/documentation/PSReader/ImageResourceName/bookmarked)

Active bookmark icon indicating the current page is bookmarked.

[`ImageResourceName.settings`](/documentation/PSReader/ImageResourceName/settings)

Reader settings button in the navigation bar.

### Reader Settings Menu

[`ImageResourceName.textSize`](/documentation/PSReader/ImageResourceName/textSize)

Text size adjustment button in the reader navigation bar.

[`ImageResourceName.search`](/documentation/PSReader/ImageResourceName/search)

Search icon in the reader settings menu.

[`ImageResourceName.settingsReader`](/documentation/PSReader/ImageResourceName/settingsReader)

Reader/edition icon in the reader settings menu.

[`ImageResourceName.fitToWidth`](/documentation/PSReader/ImageResourceName/fitToWidth)

Toggle button for switching to fit-to-width page display mode.

[`ImageResourceName.doublePageMode`](/documentation/PSReader/ImageResourceName/doublePageMode)

Toggle button for switching to double page spread mode.

[`ImageResourceName.settingsDataUsage`](/documentation/PSReader/ImageResourceName/settingsDataUsage)

Data usage icon in the reader settings menu.

[`ImageResourceName.download`](/documentation/PSReader/ImageResourceName/download)

Download icon on the download rows of the reader’s Data Settings
screen.

[`ImageResourceName.deleteData`](/documentation/PSReader/ImageResourceName/deleteData)

Delete icon used for clearing edition data in the settings menu.

### Content Browser

[`ImageResourceName.comment`](/documentation/PSReader/ImageResourceName/comment)

Comment icon in content browser.

[`ImageResourceName.trending`](/documentation/PSReader/ImageResourceName/trending)

Trending comment icon in content browser.

### Audio Overlay

[`ImageResourceName.play`](/documentation/PSReader/ImageResourceName/play)

Play button for audio playback controls.

[`ImageResourceName.pause`](/documentation/PSReader/ImageResourceName/pause)

Pause button for audio playback controls.

[`ImageResourceName.goBackward15`](/documentation/PSReader/ImageResourceName/goBackward15)

Skip backward 15 seconds button in the audio playback overlay.

[`ImageResourceName.goForward15`](/documentation/PSReader/ImageResourceName/goForward15)

Skip forward 15 seconds button in the audio playback overlay.

### Archive Date Picker

[`ImageResourceName.calendar`](/documentation/PSReader/ImageResourceName/calendar)

Calendar icon used in the archive date picker.

