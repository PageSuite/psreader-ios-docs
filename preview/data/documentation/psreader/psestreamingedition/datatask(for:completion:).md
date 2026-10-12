<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEStreamingEdition/dataTask(for:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEStreamingEditionC8dataTask3for10completionAA07PSEDataE0_pSgSS_y10Foundation4DataVSgctF"
  },
  "title" : "dataTask(for:completion:)"
}
-->

# dataTask(for:completion:)

Queues a download of an edition resource, ahead of the reader’s own
page downloads.

```
func dataTask(for hash: String, completion: @escaping (Data?) -> Void) -> PSEDataTask?
```

## Parameters

`hash`

The resource reference, as it appears in the edition’s
content.

`completion`

Called on the main queue with the resource’s data, or
`nil` when the download fails or the edition has no such file.

## Return Value

A task that cancels the queued download.