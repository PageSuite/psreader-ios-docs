<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AdvertDelegate/canRenderAdvertPage(_:inPublished:edition:)-54ng2",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader14AdvertDelegatePAAE09canRenderB4Page_11inPublished7editionSbAA7PSEPageC_AA12PSEPublishedCAA10PSEEditionCtF"
  },
  "title" : "canRenderAdvertPage(_:inPublished:edition:)"
}
-->

# canRenderAdvertPage(_:inPublished:edition:)

Default implementation — the delegate can render the page if
`advertViewController(forAdvertPage:inPublished:edition:)` supplies
a view controller for it. The view controller is discarded.

```
@MainActor func canRenderAdvertPage(_ page: PSEPage, inPublished published: PSEPublished, edition: PSEEdition) -> Bool
```