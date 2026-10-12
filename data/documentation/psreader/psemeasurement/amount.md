<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEMeasurement/amount",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEMeasurement(py)amount"
  },
  "title" : "amount"
}
-->

# amount

The measurement’s value as text, such as `1194`.

```
@objc var amount: String?
```

## Discussion

The backend may send a number or a string; either way it’s stored as
a string, so parse it before doing arithmetic.