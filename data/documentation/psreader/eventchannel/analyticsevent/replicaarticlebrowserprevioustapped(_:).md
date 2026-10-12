<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserPreviousTapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O35replicaArticleBrowserPreviousTappedyAeC07ReplicafB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.replicaArticleBrowserPreviousTapped(_:)"
}
-->

# EventChannel.AnalyticsEvent.replicaArticleBrowserPreviousTapped(_:)

Fires when the user taps the Previous button in the replica article browser / bottom navigation bar.

```
case replicaArticleBrowserPreviousTapped(ReplicaArticleEventContext)
```

## Parameters

`context`

The `ReplicaArticleEventContext` for this event.

## Discussion

Only the legacy replica reader sends this event.