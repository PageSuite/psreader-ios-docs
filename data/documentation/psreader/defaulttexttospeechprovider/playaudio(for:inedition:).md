<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/playAudio(for:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC9playAudio3for9inEditionAA0H7OverlayCSgAA7PSEPageC_AA16PSEEditionSource_ptF"
  },
  "title" : "playAudio(for:inEdition:)"
}
-->

# playAudio(for:inEdition:)

Creates and returns an audio overlay for the specified page.

```
func playAudio(for page: PSEPage, inEdition source: PSEEditionSource) -> AudioOverlay?
```

## Parameters

`page`

The page containing the article to play.

`source`

The edition source containing the page.

## Return Value

An `AudioOverlay` ready for presentation, or `nil` if the page
doesn’t contain any articles.

## Discussion

This method creates a complete audio interface as a transient overlay.
The overlay includes playback controls, progress indicators, and article
information, all styled according to the provider’s configuration.