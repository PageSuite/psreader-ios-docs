<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEdition/applicationguid",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEEdition(py)applicationguid"
  },
  "title" : "applicationguid"
}
-->

# applicationguid

GUID of the publication this edition belongs to, when the
edition payload includes it.

```
@objc var applicationguid: String?
```

## Discussion

The property keeps the identifier’s historical name; it holds the
publication GUID. On the catalog entry, read
[`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID) instead.