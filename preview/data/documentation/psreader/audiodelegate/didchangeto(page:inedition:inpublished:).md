<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioDelegate/didChangeTo(page:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AudioDelegateP11didChangeTo4page9inEdition0H9PublishedyAA7PSEPageCSg_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "didChangeTo(page:inEdition:inPublished:)"
}
-->

# didChangeTo(page:inEdition:inPublished:)

Called when the user navigates to a different page.

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

Use this method to handle audio state changes when users navigate between pages.
For example, you might pause current audio playback or update persistent banner state.

Note: A default implementation is provided that does nothing.