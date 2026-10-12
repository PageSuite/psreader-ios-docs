<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/paywallDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV15paywallDelegateAA07PaywallE0_pSgvp"
  },
  "title" : "paywallDelegate"
}
-->

# paywallDelegate

Optional delegate used for handling paywall interactions within the SDK. Without it, paywalls are not displayed.

```
var paywallDelegate: PaywallDelegate?
```

## Discussion

The prebuilt UI asks it for a paywall screen before it opens or
downloads an edition, or opens a search result.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Paywalls>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/PaywallDelegate``