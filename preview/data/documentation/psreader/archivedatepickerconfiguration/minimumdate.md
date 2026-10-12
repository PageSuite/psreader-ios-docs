<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveDatePickerConfiguration/minimumDate",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader30ArchiveDatePickerConfigurationV07minimumC010Foundation0C0VSgvp"
  },
  "title" : "minimumDate"
}
-->

# minimumDate

Optional minimum selectable date. Users will not be able to select dates earlier than this.

```
var minimumDate: Date?
```

## Discussion

If left as `nil`, the date will be unbounded meaning the user can also
select further back than what may be deemed reasonable.