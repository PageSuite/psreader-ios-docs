<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionTextSizeChange(_:oldValue:newValue:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O25feedEditionTextSizeChangeyAeC04FeedfB7ContextV_AA010PSEArticlegH0OAJtcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.feedEditionTextSizeChange(_:oldValue:newValue:)"
}
-->

# EventChannel.AnalyticsEvent.feedEditionTextSizeChange(_:oldValue:newValue:)

Fires when the user changes the article text size.

```
case feedEditionTextSizeChange(FeedEditionEventContext, oldValue: PSEArticleTextSize, newValue: PSEArticleTextSize)
```

## Parameters

`context`

The `FeedEditionEventContext` for this event.

`oldValue`

The previous text size.

`newValue`

The new text size.