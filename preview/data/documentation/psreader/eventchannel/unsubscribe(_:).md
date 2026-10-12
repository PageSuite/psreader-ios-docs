<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/unsubscribe(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC11unsubscribeyyAA0B10Subscriber_pF"
  },
  "title" : "unsubscribe(_:)"
}
-->

# unsubscribe(_:)

Unsubscribe to analytics events.

```
func unsubscribe(_ subscriber: EventSubscriber)
```

## Parameters

`subscriber`

The `EventSubscriber` that will no longer receive events.

## Discussion

Call it from the main thread.