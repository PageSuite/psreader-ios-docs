<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/articleCommentTooltipViewController(inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC35articleCommentTooltipViewController9inEditionSo06UIViewI0CSgAA16PSEEditionSource_p_tF"
  },
  "title" : "articleCommentTooltipViewController(inEdition:)"
}
-->

# articleCommentTooltipViewController(inEdition:)

Returns a [`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController) for the article view.

```
@MainActor func articleCommentTooltipViewController(inEdition source: PSEEditionSource) -> UIViewController?
```

## Discussion

Returns `nil` if the tooltip has already been presented (tracked via
`UserDefaults`). The flag is set when the tooltip’s `viewDidAppear` fires.