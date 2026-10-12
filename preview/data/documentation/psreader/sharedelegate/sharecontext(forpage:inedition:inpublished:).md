<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareDelegate/shareContext(forPage:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareDelegateP12shareContext7forPage9inEdition0H9PublishedAA0bE0VSgAA7PSEPageC_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "shareContext(forPage:inEdition:inPublished:)"
}
-->

# shareContext(forPage:inEdition:inPublished:)

Provides the sharing context for a specific page.

```
func shareContext(forPage page: PSEPage, inEdition edition: PSEEdition, inPublished published: PSEPublished) -> ShareContext?
```

## Parameters

`page`

The page to share.

`edition`

The edition containing the page.

`published`

The publication context of the page.

## Return Value

A `ShareContext` object containing the items to share,
or `nil` if the page is not shareable.