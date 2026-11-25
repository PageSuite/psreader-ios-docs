<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEThirdPartyAdvertConfig/targeting(forSection:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25PSEThirdPartyAdvertConfigC9targeting10forSectionSDyS2SGSSSg_tF"
  },
  "title" : "targeting(forSection:)"
}
-->

# targeting(forSection:)

The targeting with the page tokens resolved: `{{{SECTION}}}` becomes
the lowercased section (spaces replaced by the config’s
`replaceSpaceWithCharacterInSection` when it has one) and
`{{{PAGETYPE}}}` becomes `e-edition`, as the hosted loaders do.

```
func targeting(forSection section: String?) -> [String : String]
```

## Parameters

`section`

The page’s [`section`](/documentation/PSReader/PSEPage/section).