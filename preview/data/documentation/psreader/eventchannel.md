<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC"
  },
  "title" : "EventChannel"
}
-->

# EventChannel

Singleton class responsible for analytics reporting.

```
final class EventChannel
```

## Overview

All analytics events flow through the `EventChannel` singleton. Conform to
the `EventSubscriber` protocol and subscribe to begin receiving analytics
events.

To report the prebuilt UI’s events to your analytics, see
[Analytics](/documentation/PSReader/Analytics). A custom UI gets only download and bookmark events from
it; see [Reporting Analytics](/documentation/PSReader/Reporting-Analytics).

## Topics

### Subscribing

[`shared`](/documentation/PSReader/EventChannel/shared)

The shared singleton object.

[`subscribe(_:)`](/documentation/PSReader/EventChannel/subscribe(_:))

Subscribe to analytics events.

[`unsubscribe(_:)`](/documentation/PSReader/EventChannel/unsubscribe(_:))

Unsubscribe to analytics events.

### Events

[`EventChannel.AnalyticsEvent`](/documentation/PSReader/EventChannel/AnalyticsEvent)

An analytics event and any relevant context associated with the event.

### Event Contexts

[`EventChannel.FeedEditionEventContext`](/documentation/PSReader/EventChannel/FeedEditionEventContext)

Context object for the events of editions on PageSuite’s current
system.

[`EventChannel.CarouselEventContext`](/documentation/PSReader/EventChannel/CarouselEventContext)

Context object for carousel events.

[`EventChannel.SearchEventContext`](/documentation/PSReader/EventChannel/SearchEventContext)

Context object for search events.

### Replica Editions

[`EventChannel.ReplicaEventContext`](/documentation/PSReader/EventChannel/ReplicaEventContext)

Context object for replica events.

[`EventChannel.ReplicaArticleEventContext`](/documentation/PSReader/EventChannel/ReplicaArticleEventContext)

Context object for replica article events.

