<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventSubscriber",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15EventSubscriberP"
  },
  "title" : "EventSubscriber"
}
-->

# EventSubscriber

A type that listens to analytics events broadcast from an `EventChannel`.

```
protocol EventSubscriber : AnyObject
```

## Overview

An instance of this protocol can subscribe to analytics events via the
shared `EventChannel` singleton.

## Topics

### Receiving Events

[`analytics(event:)`](/documentation/PSReader/EventSubscriber/analytics(event:))

Called when an analytics event fires in the SDK.

