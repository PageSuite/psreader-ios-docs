<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/initialize(apiKey:)",
  "metadataVersion" : "0.1.0",
  "role" : "Function",
  "symbol" : {
    "kind" : "Function",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10initialize6apiKeySbSS_tYaF"
  },
  "title" : "initialize(apiKey:)"
}
-->

# initialize(apiKey:)

Initializes the SDK with your API key, returning when it finishes.

```
@discardableResult func initialize(apiKey: String) async -> Bool
```

## Parameters

`apiKey`

Your PageSuite API key.

## Return Value

Whether PageSuite accepted the key.

## Discussion

Most apps call [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) at launch without
waiting. Use this form when code of yours needs to know that
initialization has finished.