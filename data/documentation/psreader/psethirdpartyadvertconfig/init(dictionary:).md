<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEThirdPartyAdvertConfig/init(dictionary:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25PSEThirdPartyAdvertConfigC10dictionaryACSDySSypG_tcfc"
  },
  "title" : "init(dictionary:)"
}
-->

# init(dictionary:)

Creates a configuration from a third-party advert config.

```
init(dictionary: [String : Any])
```

## Parameters

`dictionary`

The advert config. Properties whose keys are
missing keep their defaults.

## Discussion

Pass an advert page’s [`advertConfig`](/documentation/PSReader/PSEPage/advertConfig), or use
[`thirdPartyAdvertConfig`](/documentation/PSReader/PSEPage/thirdPartyAdvertConfig):

```swift
if let config = page.thirdPartyAdvertConfig, let adUnitId = config.adUnitId {
    // request adUnitId with config.sizes and config.targeting(forSection: page.section)
}
```