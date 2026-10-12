<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration/init(globalConfig:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV12globalConfigAcA06GlobalC0V_tcfc"
  },
  "title" : "init(globalConfig:)"
}
-->

# init(globalConfig:)

Initializes a new reader configuration, inheriting defaults from the provided global configuration.

```
init(globalConfig: GlobalConfiguration)
```

## Parameters

`globalConfig`

The global SDK configuration supplying defaults for fonts, colors, and delegate implementations.

## Discussion

This ensures consistency of fonts, colors, branding, and delegate behaviors across the SDK.