<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublishedDate/init(date:editions:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16PSEPublishedDateC4date8editionsACSS_SayAA0B0CGSgtcfc"
  },
  "title" : "init(date:editions:)"
}
-->

# init(date:editions:)

Creates a date group from a date string and the editions published
on it.

```
init(date: String = "", editions: [PSEPublished]? = nil)
```

## Parameters

`date`

The calendar date as a string.

`editions`

The editions published on that date.

## Discussion

Use it when you assemble archive groups yourself rather than taking
them from [`FeedEditionService`](/documentation/PSReader/FeedEditionService).