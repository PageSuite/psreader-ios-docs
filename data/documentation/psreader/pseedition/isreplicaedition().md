<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/isReplicaEdition()",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader10PSEEditionC16isReplicaEditionSbyF"
  },
  "title" : "isReplicaEdition()"
}
-->

# isReplicaEdition()

Whether the edition is a classic PDF edition, whose PDF pages pair
into double spreads, rather than a responsive one.

```
func isReplicaEdition() -> Bool
```

## Discussion

The check looks at the edition’s cover: the first page that isn’t an
article page or an HTML or PDF advert must be a PDF page.