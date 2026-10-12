<!--
{
  "availability" : [
    "iOS: 15.0.0 -",
    "iPadOS: 15.0.0 -",
    "macCatalyst: 15.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSLegacyBridgedEdition/addObserver(_:forPageSpread:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22PSLegacyBridgedEditionC11addObserver_13forPageSpreadyAA07PSEPageiF0_p_AA0jI0OtF"
  },
  "title" : "addObserver(_:forPageSpread:)"
}
-->

# addObserver(_:forPageSpread:)

Starts reporting a spread’s state to an observer, and starts preparing
the spread’s page files.

```
func addObserver(_ observer: PSEPageSpreadObserver, forPageSpread pageSpread: PSEPageSpread)
```

## Parameters

`observer`

The observer to notify. The edition holds it weakly.

`pageSpread`

The spread to observe.

## Discussion

The observer first receives the spread’s current state, then updates
as its pages become ready or fail, all on the main queue.