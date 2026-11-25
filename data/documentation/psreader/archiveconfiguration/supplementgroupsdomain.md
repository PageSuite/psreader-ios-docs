<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/supplementGroupsDomain",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV22supplementGroupsDomainSSvp"
  },
  "title" : "supplementGroupsDomain"
}
-->

# supplementGroupsDomain

Base URL of the API that lists the publication groups named as a
feed archive’s supplements.

```
var supplementGroupsDomain: String
```

## Discussion

Defaults to `"https://rest.api.pagesuite.app"`. Set it only if your
publication’s groups are served elsewhere.

> Note: Dynamic archives set this value to the publication’s published
> domain when the PageSuite portal configures one, as they do
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveConfiguration/publishedDomain``.