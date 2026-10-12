<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventSubscriber/analytics(event:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15EventSubscriberP9analytics5eventyAA0B7ChannelC09AnalyticsB0O_tF"
  },
  "title" : "analytics(event:)"
}
-->

# analytics(event:)

Called when an analytics event fires in the SDK.

```
func analytics(event: EventChannel.AnalyticsEvent)
```

## Discussion

The SDK always calls it on the main thread.