<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/TextToSpeechArticleFormatter/format(article:)-5lfuw",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader28TextToSpeechArticleFormatterP6format7articleSSAA10PSEArticleC_tKF"
  },
  "title" : "format(article:)"
}
-->

# format(article:)

Formats an article’s content for text-to-speech synthesis.

```
func format(article: PSEArticle) throws -> String
```

## Parameters

`article`

The article to format for speech synthesis.

## Return Value

A formatted string ready for text-to-speech processing.

## Discussion

This method converts the article’s structured content into a clean text string
optimized for speech synthesis. The implementation should handle HTML cleanup,
text formatting, and any other processing needed to create natural-sounding narration.

> Throws: An error if the article cannot be formatted properly.