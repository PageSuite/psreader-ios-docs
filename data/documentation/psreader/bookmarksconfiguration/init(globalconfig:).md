<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/BookmarksConfiguration/init(globalConfig:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22BookmarksConfigurationV12globalConfigAcA06GlobalC0V_tcfc"
  },
  "title" : "init(globalConfig:)"
}
-->

# init(globalConfig:)

Initializes a new bookmarks configuration using defaults from the provided global SDK configuration.

```
init(globalConfig: GlobalConfiguration)
```

## Parameters

`globalConfig`

The global SDK configuration containing default fonts, colors, and delegate implementations.

## Discussion

Fonts, colors, placeholder visuals, and behaviors are inherited from the global configuration
to maintain visual and behavioral consistency across SDK components.