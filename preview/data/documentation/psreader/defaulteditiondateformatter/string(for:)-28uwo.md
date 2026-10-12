<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-28uwo",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA12PSEPublishedC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter), or its [`datePublished`](/documentation/PSReader/PSEPublished/datePublished) when it has
no edition date.

```
func string(for published: PSReader.PSEPublished) -> String
```

## Parameters

`published`

The edition to format.

## Return Value

A formatted string for the published edition, or `"-"` if no date is available.