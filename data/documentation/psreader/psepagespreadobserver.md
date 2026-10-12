<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageSpreadObserver",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21PSEPageSpreadObserverP"
  },
  "title" : "PSEPageSpreadObserver"
}
-->

# PSEPageSpreadObserver

Receives per-spread download state changes from a [`PSEPageSpreadSource`](/documentation/PSReader/PSEPageSpreadSource).

```
protocol PSEPageSpreadObserver : AnyObject
```

## Topics

### Observing Spread State

[`observedPageSpread(_:stateDidUpdate:)`](/documentation/PSReader/PSEPageSpreadObserver/observedPageSpread(_:stateDidUpdate:))

Called when the observed spread’s asset state changes.

