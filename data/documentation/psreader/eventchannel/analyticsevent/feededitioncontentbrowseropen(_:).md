<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionContentBrowserOpen(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O29feedEditionContentBrowserOpenyAeC04FeedfB7ContextVcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.feedEditionContentBrowserOpen(_:)"
}
-->

# EventChannel.AnalyticsEvent.feedEditionContentBrowserOpen(_:)

Fires when the user opens the reader’s contents browser.

```
case feedEditionContentBrowserOpen(FeedEditionEventContext)
```

## Parameters

`context`

The `FeedEditionEventContext` for this event.
Its page spread is the spread the reader was
showing when the browser opened.