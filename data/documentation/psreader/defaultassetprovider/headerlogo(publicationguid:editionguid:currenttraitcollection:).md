<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultAssetProvider/headerLogo(publicationGUID:editionGUID:currentTraitCollection:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegatePAAE10headerLogo15publicationGUID07editionG022currentTraitCollection10Foundation3URLVSgSSSg_SSSo07UITraitK0CSgtF::SYNTHESIZED::s:8PSReader20DefaultAssetProviderV"
  },
  "title" : "headerLogo(publicationGUID:editionGUID:currentTraitCollection:)"
}
-->

# headerLogo(publicationGUID:editionGUID:currentTraitCollection:)

Returns `nil`, so the splash screen for replica editions shows no
logo.

```
func headerLogo(publicationGUID: String?, editionGUID: String, currentTraitCollection: UITraitCollection? = nil) -> URL?
```

## Parameters

`publicationGUID`

The GUID of the publication, if available.

`editionGUID`

The GUID of the edition being opened.

`currentTraitCollection`

The current trait collection.

## Return Value

`nil`.