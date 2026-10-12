<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/TextToSpeechArticleFormatter/format(article:)-82qmw",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader28TextToSpeechArticleFormatterP6format7articleSSAA9PSArticleC_tKF"
  },
  "title" : "format(article:)"
}
-->

# format(article:)

Formats a replica article’s content for text-to-speech synthesis.

```
func format(article: PSArticle) throws -> String
```

## Parameters

`article`

The replica article to format for speech synthesis.

## Return Value

A formatted string ready for text-to-speech processing.

## Discussion

The default implementation returns the text that
[`DefaultTextToSpeechArticleFormatter`](/documentation/PSReader/DefaultTextToSpeechArticleFormatter) produces for the article.

> Throws: An error if the article cannot be formatted properly.