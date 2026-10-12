<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/replicaArticleTextSizeChange(_:oldValue:newValue:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O28replicaArticleTextSizeChangeyAeC07ReplicafB7ContextV_14CoreFoundation7CGFloatVAKtcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.replicaArticleTextSizeChange(_:oldValue:newValue:)"
}
-->

# EventChannel.AnalyticsEvent.replicaArticleTextSizeChange(_:oldValue:newValue:)

Fires when replica popover article text size preference is changed.

```
case replicaArticleTextSizeChange(ReplicaArticleEventContext, oldValue: CGFloat, newValue: CGFloat)
```

## Parameters

`context`

The `ReplicaArticleEventContext` for this event.

`oldValue`

The previous text size value.

`newValue`

The new text size value.