<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/replicaPageBrowserNextTapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O28replicaPageBrowserNextTappedyAeC07ReplicaB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.replicaPageBrowserNextTapped(_:)"
}
-->

# EventChannel.AnalyticsEvent.replicaPageBrowserNextTapped(_:)

Fires when the user taps the Next button in the replica page browser / bottom navigation bar.

```
case replicaPageBrowserNextTapped(ReplicaEventContext)
```

## Parameters

`context`

The `ReplicaEventContext` for this event.

## Discussion

Only the legacy replica reader sends this event.