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

Returns `nil`: the reader’s onboarding walkthrough introduces the
comment bar, so the default provider shows no tooltip of its own in
the article view. Override to show one, for example a
[`DefaultCommentTooltipViewController`](/documentation/PSReader/DefaultCommentTooltipViewController).

```
@MainActor func articleCommentTooltipViewController(inEdition source: PSEEditionSource) -> UIViewController?
```