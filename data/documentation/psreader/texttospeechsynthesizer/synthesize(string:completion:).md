<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/TextToSpeechSynthesizer/synthesize(string:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23TextToSpeechSynthesizerP10synthesize6string10completionySS_ys6ResultOy10Foundation3URLVs5Error_pGctF"
  },
  "title" : "synthesize(string:completion:)"
}
-->

# synthesize(string:completion:)

Synthesizes text into an audio file.

```
func synthesize(string: String, completion: @escaping (Result<URL, Error>) -> Void)
```

## Parameters

`string`

The text to convert to speech.

`completion`

A completion handler called with the result of synthesis.
On success, provides a `URL` to the generated audio file.
On failure, provides an `Error` describing what went wrong.

## Discussion

This method converts the provided text string into speech audio and returns
the location of the generated audio file through the completion handler.

The synthesis process is typically asynchronous, use the completion callback
to return the result.