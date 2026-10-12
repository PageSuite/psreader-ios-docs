<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchViewController/init(globalConfig:searchConfig:delegate:dismissible:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20SearchViewControllerC12globalConfig06searchF08delegate11dismissibleAcA19GlobalConfigurationV_AA0bK0VSgAA0B8Delegate_pSbtcfc"
  },
  "title" : "init(globalConfig:searchConfig:delegate:dismissible:)"
}
-->

# init(globalConfig:searchConfig:delegate:dismissible:)

Initializes a new standalone search view controller.

```
@MainActor init(globalConfig: GlobalConfiguration, searchConfig: SearchConfiguration? = nil, delegate: SearchDelegate, dismissible: Bool = false)
```

## Parameters

`globalConfig`

The global SDK configuration supplying defaults for fonts, colors, delegates, and credentials.

`searchConfig`

Optional custom configuration for the search view appearance and behavior.
Defaults to settings inherited from `globalConfig` if not explicitly provided.

`delegate`

A [`SearchDelegate`](/documentation/PSReader/SearchDelegate) that provides the list of searchable publications
and reader configurations for opening results.

`dismissible`

Whether to show a dismiss button. Defaults to `false`.