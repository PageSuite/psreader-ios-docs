<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/advertViewController(forAdvertPage:inPublished:edition:)-9x0bc",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegatePAAE20advertViewController03forB4Page11inPublished7editionAA016PSEAdvertContenteF0_pSgAA7PSEPageC_AA12PSEPublishedCAA10PSEEditionCtF"
  },
  "title" : "advertViewController(forAdvertPage:inPublished:edition:)"
}
-->

# advertViewController(forAdvertPage:inPublished:edition:)

Default implementation returning `nil` — advert pages use the SDK’s
built-in webview rendering.

```
@MainActor func advertViewController(forAdvertPage page: PSEPage, inPublished published: PSEPublished, edition: PSEEdition) -> PSEAdvertContentViewController?
```