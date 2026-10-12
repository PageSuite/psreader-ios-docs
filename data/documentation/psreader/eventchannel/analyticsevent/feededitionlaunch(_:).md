<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionLaunch(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O17feedEditionLaunchyAeC04FeedfB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.feedEditionLaunch(_:)"
}
-->

# EventChannel.AnalyticsEvent.feedEditionLaunch(_:)

Fires when an edition is launched from the archive.

```
case feedEditionLaunch(FeedEditionEventContext)
```

## Parameters

`context`

The `FeedEditionEventContext` for this event.
Its page spread is the page the reader opened
on.