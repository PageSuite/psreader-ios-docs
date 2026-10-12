<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/WebReaderShareProvider/init(urlMask:shortCode:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22WebReaderShareProviderC7urlMask9shortCodeACSSSg_SStcfc"
  },
  "title" : "init(urlMask:shortCode:)"
}
-->

# init(urlMask:shortCode:)

Initializes a new web reader share provider.

```
init(urlMask: String?, shortCode: String)
```

## Parameters

`urlMask`

The host of your own web reader domain, without
`https://`, such as `reader.example.com`; `nil` links to
PageSuite’s web reader.

`shortCode`

Your app’s shortcode. The parameter is spelled
`shortCode`; the rest of the SDK says `shortcode`.