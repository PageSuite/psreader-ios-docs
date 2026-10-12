<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/advertDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV14advertDelegateAA06AdvertE0_pSgvp"
  },
  "title" : "advertDelegate"
}
-->

# advertDelegate

Optional delegate that supplies advert banners and can replace the
rendering of advert pages.

```
var advertDelegate: AdvertDelegate?
```

## Discussion

Without it, the reader shows no banners. Advert pages still render
with the built-in web view, except Google Ad Manager pages, which
stay blank.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Advertisements>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/AdvertDelegate``