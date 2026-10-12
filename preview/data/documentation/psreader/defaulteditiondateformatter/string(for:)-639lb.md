<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultEditionDateFormatter/string(for:)-639lb",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DefaultEditionDateFormatterV6string3forSSAA9PSEditionC_tF"
  },
  "title" : "string(for:)"
}
-->

# string(for:)

Formats the edition’s [`publishDate`](/documentation/PSReader/PSEdition/publishDate) with
[`dateFormatter`](/documentation/PSReader/DefaultEditionDateFormatter/dateFormatter).

```
func string(for edition: PSReader.PSEdition) -> String
```

## Parameters

`edition`

The legacy replica edition to format.

## Return Value

A formatted string for the edition, or `"-"` if no date is available.