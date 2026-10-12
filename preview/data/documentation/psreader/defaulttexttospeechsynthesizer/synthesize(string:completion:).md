<!--
{
  "availability" : [
    "iOS: 13.0.0 -",
    "iPadOS: 13.0.0 -",
    "macCatalyst: 13.0.0 -"
  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultTextToSpeechSynthesizer/synthesize(string:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30DefaultTextToSpeechSynthesizerV10synthesize6string10completionySS_ys6ResultOy10Foundation3URLVs5Error_pGctF"
  },
  "title" : "synthesize(string:completion:)"
}
-->

# synthesize(string:completion:)

Synthesizes text using the system’s text-to-speech engine.

```
func synthesize(string: String, completion: @escaping (Result<URL, any Error>) -> Void)
```

## Parameters

`string`

The text to synthesize into speech.

`completion`

Completion handler providing the synthesized audio URL on success
or an error on failure.

## Discussion

This implementation uses the SDK’s shared `TTSSynthesizer` to convert text
into speech audio in the specified language.