<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEThirdPartyAdvertConfig/targeting",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25PSEThirdPartyAdvertConfigC9targetingSDyS2SGvp"
  },
  "title" : "targeting"
}
-->

# targeting

Key-value targeting for the request, from the config’s `targeting`
value. Accepts either an object or the web reader’s list of
`[key, value]` pairs. Values may carry the `{{{SECTION}}}` and
`{{{PAGETYPE}}}` tokens the hosted loaders substitute; see
[`targeting(forSection:)`](/documentation/PSReader/PSEThirdPartyAdvertConfig/targeting(forSection:)).

```
var targeting: [String : String]
```