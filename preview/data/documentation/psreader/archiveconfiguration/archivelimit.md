<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArchiveConfiguration/archiveLimit",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20ArchiveConfigurationV12archiveLimitSiSgvp"
  },
  "title" : "archiveLimit"
}
-->

# archiveLimit

Maximum number of editions displayed in the archive.

```
var archiveLimit: Int?
```

## Discussion

Defaults to `nil`, which uses the default limit for the edition type
(unbounded for archives of editions on PageSuite’s current system, 30
editions for legacy replica archives).

> Note: Dynamic archives ignore this value. They use the archive limit
> configured in the PageSuite portal, falling back to the edition-type
> default when none is configured.