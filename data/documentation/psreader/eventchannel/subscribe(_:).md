<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/subscribe(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC9subscribeyyAA0B10Subscriber_pF"
  },
  "title" : "subscribe(_:)"
}
-->

# subscribe(_:)

Subscribe to analytics events.

```
func subscribe(_ subscriber: EventSubscriber)
```

## Parameters

`subscriber`

The `EventSubscriber` that will receive events.

## Discussion

The `EventChannel` does not retain the subscriber, instead it maintains
a weak reference. It is not necessary to explicitly unsubscribe.

> Note: Call this method from the main thread.