<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/datePicker",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV10datePickerAA0b4DateeC0VSgvp"
  },
  "title" : "datePicker"
}
-->

# datePicker

Optional configuration for displaying a date picker to filter archived editions.

```
var datePicker: ArchiveDatePickerConfiguration?
```

## Discussion

Archives of editions on PageSuite’s current system load the selected
month from the backend identified by
[`feedPublicationType`](/documentation/PSReader/ArchiveConfiguration/feedPublicationType-swift.property).

> Note: When this is `nil`, dynamic archives show the date picker for
> publications with it enabled in the PageSuite portal, starting from
> the archive’s configured start date. A configuration set here applies
> to every publication in the dynamic archive instead.