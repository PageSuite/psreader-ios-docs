<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/shareDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV13shareDelegateAA05ShareE0_pvp"
  },
  "title" : "shareDelegate"
}
-->

# shareDelegate

Delegate that decides which pages can be shared and what the share sheet offers.

```
var shareDelegate: ShareDelegate
```

## Discussion

The default, a [`ShareProvider`](/documentation/PSReader/ShareProvider) with the `.onlyArticleLink()` policy,
shares article links on article pages that carry one.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider``