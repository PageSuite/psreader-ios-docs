<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/applyPageFilter(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC15applyPageFilteryySbAA7PSEPageCcF"
  },
  "title" : "applyPageFilter(_:)"
}
-->

# applyPageFilter(_:)

Leaves the pages `keeps` declines out of the spreads, so a user
pages past them as if they weren’t there. [`pages`](/documentation/PSReader/PSEEdition/pages) and page
numbering stay as published.

```
func applyPageFilter(_ keeps: @escaping (PSEPage) -> Bool)
```

## Parameters

`keeps`

Returns whether a page stays in the spreads.
Called once per page each time the filtered spreads are rebuilt.

## Discussion

The reader applies this when it opens the edition, and again
whenever its advert delegate changes, with a predicate that leaves
out third-party advert pages neither the built-in rendering nor the
delegate can render; see
[`canRenderAdvertPage(_:)`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/canRenderAdvertPage(_:)).
A filter you apply yourself is replaced at those points. Pages that
fail [`isSupportedPage(_:)`](/documentation/PSReader/PSEEdition/isSupportedPage(_:)) are left out at parse time regardless.

The spreads as built are kept, so each call filters from the full
set and a source that builds its own spreads keeps them. A page left
out of a double spread leaves its partner alone in the spread.