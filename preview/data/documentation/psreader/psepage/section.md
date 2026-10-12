<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPage/section",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPage(py)section"
  },
  "title" : "section"
}
-->

# section

The section this page belongs to. This value serves as both the
section’s display name and the match key for
[`scrollTo(sectionGUID:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(sectionGUID:source:))
(compared case-insensitively).

```
@objc var section: String?
```