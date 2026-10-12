<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/cachedData(for:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC10cachedData3for10Foundation0E0VSgSS_tF"
  },
  "title" : "cachedData(for:)"
}
-->

# cachedData(for:)

Returns the resource’s bytes if it has already downloaded.

```
func cachedData(for hash: String) -> Data?
```

## Parameters

`hash`

The resource reference, as it appears in the
edition’s content.

## Return Value

The downloaded data, or `nil` when the resource isn’t in
the edition’s cache yet.