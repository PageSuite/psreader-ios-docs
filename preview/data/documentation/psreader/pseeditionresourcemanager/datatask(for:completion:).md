<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEditionResourceManager/dataTask(for:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25PSEEditionResourceManagerP8dataTask3for10completionAA07PSEDataF0_pSgSS_y10Foundation4DataVSgctF"
  },
  "title" : "dataTask(for:completion:)"
}
-->

# dataTask(for:completion:)

Starts an asynchronous fetch for the resource. Return `nil` when the
resource cannot be fetched (the reader then treats it as missing).

```
func dataTask(for resource: String, completion: @escaping (Data?) -> Void) -> PSEDataTask?
```