<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/EditionDateFormatter/string(for:)-6flyk",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20EditionDateFormatterP6string3forSSAA9PSEditionC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Provides a formatted string representation for the given legacy
replica edition.

```
func string(for edition: PSEdition) -> String
```

## Parameters

`edition`

The [`PSEdition`](/documentation/PSReader/PSEdition) to format.

## Return Value

A formatted string for the edition.

## Discussion

You may choose to format editions based on their publish date,
edition names, or any custom naming strategy suitable for your publication.
The default formats the edition’s [`publishDate`](/documentation/PSReader/PSEdition/publishDate).