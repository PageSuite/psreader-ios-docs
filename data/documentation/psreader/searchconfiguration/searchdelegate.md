<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchConfiguration/searchDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SearchConfigurationV14searchDelegateAA0bE0_pSgvp"
  },
  "title" : "searchDelegate"
}
-->

# searchDelegate

The delegate that provides searchable publications and reader configurations.

```
var searchDelegate: SearchDelegate?
```

## Discussion

When non-nil, the search option is enabled in the reader’s settings menu.

In carousel-based setups, a default delegate is provided automatically if
this is left `nil`. For standalone view controllers, you must set this
explicitly using [`ApplicationSearchDelegate`](/documentation/PSReader/ApplicationSearchDelegate) or a custom implementation.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ApplicationSearchDelegate``