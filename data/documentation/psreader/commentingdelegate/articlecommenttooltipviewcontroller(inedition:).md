<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate/articleCommentTooltipViewController(inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP35articleCommentTooltipViewController9inEditionSo06UIViewH0CSgAA16PSEEditionSource_p_tF"
  },
  "title" : "articleCommentTooltipViewController(inEdition:)"
}
-->

# articleCommentTooltipViewController(inEdition:)

Returns a view controller to present as a popover tooltip above the
comment button in the article view.

```
@MainActor func articleCommentTooltipViewController(inEdition source: PSEEditionSource) -> UIViewController?
```

## Parameters

`source`

The current edition.

## Return Value

A view controller to present as a popover, or `nil`.

## Discussion

The SDK presents the returned view controller as a popover anchored
above the comment button. Return `nil` to show no tooltip.

Note: A default implementation is provided that returns `nil`.