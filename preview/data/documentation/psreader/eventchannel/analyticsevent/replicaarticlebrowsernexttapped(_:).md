<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleBrowserNextTapped(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O31replicaArticleBrowserNextTappedyAeC07ReplicafB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.replicaArticleBrowserNextTapped(_:)"
}
-->

# EventChannel.AnalyticsEvent.replicaArticleBrowserNextTapped(_:)

Fires when the user taps the Next button in the replica article browser / bottom navigation bar.

```
case replicaArticleBrowserNextTapped(ReplicaArticleEventContext)
```

## Parameters

`context`

The `ReplicaArticleEventContext` for this event.

## Discussion

Only the legacy replica reader sends this event.