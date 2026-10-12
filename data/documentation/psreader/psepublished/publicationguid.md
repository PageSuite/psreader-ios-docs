<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/publicationGUID",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)publicationGUID"
  },
  "title" : "publicationGUID"
}
-->

# publicationGUID

GUID of the publication the backend files this edition’s content
under, read from the catalog payload.

```
@objc var publicationGUID: String
```

## Discussion

It can differ from the publication GUID you fetched the catalog with,
so don’t use it to identify the publication. Read [`applicationGUID`](/documentation/PSReader/PSEPublished/applicationGUID)
instead; when that’s empty, use the publication GUID you already
hold. Fall back to this property only as a last resort.