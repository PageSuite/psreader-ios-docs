<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EditionDateFormatter/string(for:)-3u5s",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20EditionDateFormatterP6string3forSSAA12PSEPublishedC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Provides a formatted string representation for the given edition.

```
func string(for published: PSEPublished) -> String
```

## Parameters

`published`

The `PSEPublished` object to format.

## Return Value

A formatted string for the edition.

## Discussion

You may choose to format editions based on their dates, edition
names, or any custom naming strategy suitable for your publication.
The default formats the edition’s [`editionDate`](/documentation/PSReader/PSEPublished/editionDate), the
issue date on the masthead, and falls back to
[`datePublished`](/documentation/PSReader/PSEPublished/datePublished) when there’s none.