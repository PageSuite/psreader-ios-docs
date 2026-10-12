<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/isListenable(page:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC12isListenable4page9inEditionSbAA7PSEPageC_AA16PSEEditionSource_ptF"
  },
  "title" : "isListenable(page:inEdition:)"
}
-->

# isListenable(page:inEdition:)

Determines if a page can be read aloud using text-to-speech.

```
func isListenable(page: PSEPage, inEdition source: PSEEditionSource) -> Bool
```

## Parameters

`page`

The page to evaluate for TTS capability.

`source`

The edition source containing the page.

## Return Value

`true` if the page has exactly one article; otherwise, `false`.

## Discussion

This implementation considers pages with exactly one article as listenable.
Pages with no articles or multiple articles are not supported by this provider.