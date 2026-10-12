<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechProvider/didChangeTo(page:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultTextToSpeechProviderC09didChangeD04page9inEdition0J9PublishedyAA7PSEPageCSg_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "didChangeTo(page:inEdition:inPublished:)"
}
-->

# didChangeTo(page:inEdition:inPublished:)

Handles page navigation by managing audio player state.

```
func didChangeTo(page: PSEPage?, inEdition edition: PSEEdition, inPublished published: PSEPublished)
```

## Parameters

`page`

The new page being displayed, or `nil` if no specific page is active.

`edition`

The edition containing the page.

`published`

The published object for the edition.

## Discussion

When the user navigates to a different page, this method checks if the
currently playing audio corresponds to the new page. If not, it clears
the current player to stop playback and free resources.