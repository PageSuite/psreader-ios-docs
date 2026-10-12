<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/audioDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV13audioDelegateAA05AudioE0_pSgvp"
  },
  "title" : "audioDelegate"
}
-->

# audioDelegate

Delegate responsible for providing audio features. Off (`nil`) by default.

```
var audioDelegate: AudioDelegate?
```

## Discussion

Set it to a [`DefaultTextToSpeechProvider`](/documentation/PSReader/DefaultTextToSpeechProvider) to add a listen button to
the reader.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Text-to-Speech>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultTextToSpeechProvider``