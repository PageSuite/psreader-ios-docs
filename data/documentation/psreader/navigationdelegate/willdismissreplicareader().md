<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/NavigationDelegate/willDismissReplicaReader()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18NavigationDelegateP24willDismissReplicaReaderyyF"
  },
  "title" : "willDismissReplicaReader()"
}
-->

# willDismissReplicaReader()

Called when the legacy replica reader closes.

```
@MainActor func willDismissReplicaReader()
```

## Discussion

The modern replica reader doesn’t call it. Implement this method to
handle any cleanup after the legacy reader closes, such as restoring the
previous UI state or tracking analytics.