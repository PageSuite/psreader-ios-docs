<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/isListenable(page:inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP12isListenable4page9inEditionSbAA7PSEPageC_AA16PSEEditionSource_ptF"
  },
  "title" : "isListenable(page:inEdition:)"
}
-->

# isListenable(page:inEdition:)

Determines if a page within an edition supports audio playback.

```
func isListenable(page: PSEPage, inEdition source: PSEEditionSource) -> Bool
```

## Parameters

`page`

The page currently being evaluated for audio capability.

`source`

The edition source containing the page.

## Return Value

`true` if the page supports audio playback; otherwise, `false`.

## Discussion

Use this method to control which pages display audio controls or functionality.
This is called by the SDK to determine whether to show audio-related UI elements.