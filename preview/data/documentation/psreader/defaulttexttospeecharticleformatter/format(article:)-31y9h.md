<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechArticleFormatter/format(article:)-31y9h",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader35DefaultTextToSpeechArticleFormatterV6format7articleSSAA9PSArticleC_tKF"
  },
  "title" : "format(article:)"
}
-->

# format(article:)

Formats an article using the default formatting rules.

```
func format(article: PSArticle) throws -> String
```

## Parameters

`article`

The article to format for speech synthesis.

## Return Value

A formatted string optimized for text-to-speech.

## Discussion

This implementation uses the SDK’s built-in `TTSArticleFormatter` to process
article content into speech-ready text.

> Throws: An error if the article content cannot be processed.