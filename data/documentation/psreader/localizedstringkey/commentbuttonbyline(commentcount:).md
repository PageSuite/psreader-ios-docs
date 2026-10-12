<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LocalizedStringKey/commentButtonByline(commentCount:)",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18LocalizedStringKeyO19commentButtonBylineyACSiSg_tcACmF"
  },
  "title" : "LocalizedStringKey.commentButtonByline(commentCount:)"
}
-->

# LocalizedStringKey.commentButtonByline(commentCount:)

Comment button label in article byline.
Default value: `"Comment"` when count is nil, `"1 comment"` when count is 1,
`"%lld comments"` otherwise.

```
case commentButtonByline(commentCount: Int?)
```