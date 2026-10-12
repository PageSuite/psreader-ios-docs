<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserPreviousTapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O32replicaPageBrowserPreviousTappedyAeC07ReplicaB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.replicaPageBrowserPreviousTapped(_:)"
}
-->

# EventChannel.AnalyticsEvent.replicaPageBrowserPreviousTapped(_:)

Fires when the user taps the Previous button in the replica page browser / bottom navigation bar.

```
case replicaPageBrowserPreviousTapped(ReplicaEventContext)
```

## Parameters

`context`

The `ReplicaEventContext` for this event.

## Discussion

Only the legacy replica reader sends this event.