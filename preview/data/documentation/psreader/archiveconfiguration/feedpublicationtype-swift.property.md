<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/feedPublicationType-swift.property",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV19feedPublicationTypeAC04FeedeF0Ovp"
  },
  "title" : "feedPublicationType"
}
-->

# feedPublicationType

The backend that serves this archive’s editions when filtering by
[`datePicker`](/documentation/PSReader/ArchiveConfiguration/datePicker).

```
var feedPublicationType: FeedPublicationType
```

## Discussion

Defaults to [`ArchiveConfiguration.FeedPublicationType.app`](/documentation/PSReader/ArchiveConfiguration/FeedPublicationType-swift.enum/app). Legacy replica archives ignore this value.

> Note: Dynamic archives set this value from each publication’s type
> configured in the PageSuite portal.