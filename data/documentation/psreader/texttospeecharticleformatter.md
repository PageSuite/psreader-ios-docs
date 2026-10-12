<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/TextToSpeechArticleFormatter",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader28TextToSpeechArticleFormatterP"
  },
  "title" : "TextToSpeechArticleFormatter"
}
-->

# TextToSpeechArticleFormatter

Protocol for formatting articles into text suitable for speech synthesis.

```
protocol TextToSpeechArticleFormatter
```

## Overview

Implementations of this protocol convert article content into clean, readable text
that can be processed by text-to-speech systems. The formatter handles tasks such as
removing HTML markup, formatting headings, and preparing content for audio narration.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechArticleFormatter``

## Topics

### Formatting Articles

[`format(article:)`](/documentation/PSReader/TextToSpeechArticleFormatter/format(article:)-5lfuw)

Formats an article’s content for text-to-speech synthesis.

### Replica Editions

[`format(article:)`](/documentation/PSReader/TextToSpeechArticleFormatter/format(article:)-82qmw)

Formats a replica article’s content for text-to-speech synthesis.

