<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/NavigationDelegate/willPresentReplicaReader()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18NavigationDelegateP24willPresentReplicaReaderyyF"
  },
  "title" : "willPresentReplicaReader()"
}
-->

# willPresentReplicaReader()

Called just before a replica edition opens, in either the modern or the
legacy replica reader.

```
@MainActor func willPresentReplicaReader()
```

## Discussion

Implement this method to perform any necessary setup before the replica
reader appears, such as updating UI elements or tracking analytics.