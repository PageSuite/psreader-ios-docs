<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEGAMAdvertConfig/init(dictionary:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEGAMAdvertConfigC10dictionaryACSDySSypG_tcfc"
  },
  "title" : "init(dictionary:)"
}
-->

# init(dictionary:)

Creates a configuration from a Google Ad Manager advert config.

```
init(dictionary: [String : Any])
```

## Parameters

`dictionary`

The advert config. Properties whose keys are
missing keep their defaults.

## Discussion

Pass a Google Ad Manager advert page’s [`advertConfig`](/documentation/PSReader/PSEPage/advertConfig):

```swift
if page.advertProvider == .googleAdManager {
    let config = PSEGAMAdvertConfig(dictionary: page.advertConfig ?? [:])
}
```