<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/initialize(apiKey:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Function",
  "symbol" : {
    "kind" : "Function",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10initialize6apiKey10completionySSSg_ySbcSgtF"
  },
  "title" : "initialize(apiKey:completion:)"
}
-->

# initialize(apiKey:completion:)

Initializes the SDK with your API key.

```
func initialize(apiKey: String? = nil, completion: ((Bool) -> Void)? = nil)
```

## Parameters

`apiKey`

Your PageSuite API key. With `nil`, the default, the call
only prepares the PDF engine: it sets no key, and calls
`completion` at once with `false`.

`completion`

Called when initialization finishes, with whether
PageSuite accepted the key. It may run on any thread.

## Discussion

Call it once, at launch, and carry on: there’s no need to wait for it.
It sets your key and prepares the PDF engine in the background, and the
SDK waits for it wherever it needs to. Calling it again is harmless.