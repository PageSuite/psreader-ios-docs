<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEAdvertProvider/custom(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17PSEAdvertProviderO6customyACSScACmF"
  },
  "title" : "PSEAdvertProvider.custom(_:)"
}
-->

# PSEAdvertProvider.custom(_:)

A provider the SDK doesn’t know, carrying the page’s advert type
lowercased, for example `custom("freestar")`; match it with a
lowercase literal. These pages have no
built-in rendering: supply a view controller through
[`AdvertDelegate`](/documentation/PSReader/AdvertDelegate) or [`PSEditionReaderViewController.AdvertDelegate`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol),
built from [`thirdPartyAdvertConfig`](/documentation/PSReader/PSEPage/thirdPartyAdvertConfig), or the reader leaves
the page out.

```
case custom(String)
```