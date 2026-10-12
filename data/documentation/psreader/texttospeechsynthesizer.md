<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/TextToSpeechSynthesizer",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23TextToSpeechSynthesizerP"
  },
  "title" : "TextToSpeechSynthesizer"
}
-->

# TextToSpeechSynthesizer

Protocol for synthesizing text into speech audio.

```
protocol TextToSpeechSynthesizer
```

## Overview

Implementations of this protocol convert formatted text strings into audio files
that can be played back through the audio system. The synthesizer handles the
conversion from text to speech and provides the resulting audio as a URL.

> Tip: The built-in ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechSynthesizer`` uses `AVSpeechSynthesizer`
> with a standard (non-premium) voice. For higher quality voices, provide a custom
> implementation using a cloud TTS service.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechSynthesizer``

## Topics

### Synthesizing Speech

[`synthesize(string:completion:)`](/documentation/PSReader/TextToSpeechSynthesizer/synthesize(string:completion:))

Synthesizes text into an audio file.

