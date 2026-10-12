<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechSynthesizer",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30DefaultTextToSpeechSynthesizerV"
  },
  "title" : "DefaultTextToSpeechSynthesizer"
}
-->

# DefaultTextToSpeechSynthesizer

Default implementation of text-to-speech synthesis using the system’s TTS capabilities.

```
struct DefaultTextToSpeechSynthesizer
```

## Overview

This synthesizer provides a standard implementation using the SDK’s built-in
text-to-speech system. It uses `AVSpeechSynthesizer` and a standard (non premium) voice.
To use a higher quality voice, you must provide your own implementation.

The default synthesizer handles caching, voice selection, and audio file generation.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/TextToSpeechSynthesizer``

## Topics

### Creating a Synthesizer

[`init(language:)`](/documentation/PSReader/DefaultTextToSpeechSynthesizer/init(language:))

Creates a new text-to-speech synthesizer for the specified language.

[`language`](/documentation/PSReader/DefaultTextToSpeechSynthesizer/language)

The language code for speech synthesis (e.g., “en” for English, “es” for Spanish).

### Synthesizing Speech

[`synthesize(string:completion:)`](/documentation/PSReader/DefaultTextToSpeechSynthesizer/synthesize(string:completion:))

Synthesizes text using the system’s text-to-speech engine.

