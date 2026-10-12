<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AssetDelegate/headerLogo(publicationGUID:editionGUID:currentTraitCollection:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13AssetDelegateP10headerLogo15publicationGUID07editionG022currentTraitCollection10Foundation3URLVSgSSSg_SSSo07UITraitK0CSgtF"
  },
  "title" : "headerLogo(publicationGUID:editionGUID:currentTraitCollection:)"
}
-->

# headerLogo(publicationGUID:editionGUID:currentTraitCollection:)

Provides a URL to a custom logo / masthead for a replica edition.
Used in the splash screen for replica readers.

```
func headerLogo(publicationGUID: String?, editionGUID: String, currentTraitCollection: UITraitCollection?) -> URL?
```

## Parameters

`publicationGUID`

The GUID of the publication, if available.

`editionGUID`

The GUID of the edition being opened.

`currentTraitCollection`

The current trait collection, used to select a dark mode logo variant if available.

## Return Value

A URL pointing to the custom header logo image, or `nil` to omit the logo.