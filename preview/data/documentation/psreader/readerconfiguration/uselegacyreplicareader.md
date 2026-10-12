<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration/useLegacyReplicaReader",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV016useLegacyReplicaB0Sbvp"
  },
  "title" : "useLegacyReplicaReader"
}
-->

# useLegacyReplicaReader

When `true`, uses the legacy replica reader instead of the modern implementation.

```
var useLegacyReplicaReader: Bool
```

## Discussion

Defaults to `true`. Will default to `false` in a future release.

> Important: The modern reader is the recommended implementation. The legacy
> reader will be removed in a future major release.