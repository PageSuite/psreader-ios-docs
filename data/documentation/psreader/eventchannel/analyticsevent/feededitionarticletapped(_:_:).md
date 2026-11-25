<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EventChannel/AnalyticsEvent/feedEditionArticleTapped(_:_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12EventChannelC09AnalyticsB0O24feedEditionArticleTappedyAeA10PSEArticleC_AC04FeedfB7ContextVtcAEmF"
  },
  "title" : "EventChannel.AnalyticsEvent.feedEditionArticleTapped(_:_:)"
}
-->

# EventChannel.AnalyticsEvent.feedEditionArticleTapped(_:_:)

Fires when the user taps an article on a page and the reader
jumps to it.

```
case feedEditionArticleTapped(PSEArticle, FeedEditionEventContext)
```

## Parameters

`article`

The `PSEArticle` that was tapped.

`context`

The `FeedEditionEventContext` for this event.
Its page spread is the spread on screen,
and its page is the page the user tapped
the article on.