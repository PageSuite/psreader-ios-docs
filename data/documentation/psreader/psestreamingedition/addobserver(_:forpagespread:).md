<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/addObserver(_:forPageSpread:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC11addObserver_13forPageSpreadyAA07PSEPagehE0_p_AA0iH0OtF"
  },
  "title" : "addObserver(_:forPageSpread:)"
}
-->

# addObserver(_:forPageSpread:)

Starts reporting a spread’s download state to an observer.

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
as downloads progress, all on the main queue.