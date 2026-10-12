<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareDelegate/isShareable(page:inEdition:inPublished:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareDelegateP11isShareable4page9inEdition0G9PublishedSbAA7PSEPageC_AA10PSEEditionCAA12PSEPublishedCtF"
  },
  "title" : "isShareable(page:inEdition:inPublished:)"
}
-->

# isShareable(page:inEdition:inPublished:)

Determines if a page within an edition is shareable.

```
func isShareable(page: PSEPage, inEdition edition: PSEEdition, inPublished published: PSEPublished) -> Bool
```

## Parameters

`page`

The page currently being viewed.

`edition`

The edition containing the page.

`published`

The published object for the edition.

## Return Value

`true` if the page is shareable; otherwise, `false`.

## Discussion

The default implementation returns whether
[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/shareContext(forPage:inEdition:inPublished:)) returns a context.
Implement this method when building a context is expensive: the reader
asks on every page turn.