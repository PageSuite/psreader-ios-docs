<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPublished/useCustomEditionName",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPublished(py)useCustomEditionName"
  },
  "title" : "useCustomEditionName"
}
-->

# useCustomEditionName

Whether the publisher chose to label this edition by its [`name`](/documentation/PSReader/PSEPublished/name)
rather than its date.

```
@objc var useCustomEditionName: Bool
```

## Discussion

When `true`, show [`name`](/documentation/PSReader/PSEPublished/name) where you’d otherwise show a formatted
edition date.