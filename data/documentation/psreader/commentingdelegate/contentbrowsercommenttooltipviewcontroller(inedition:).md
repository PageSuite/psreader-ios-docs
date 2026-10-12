<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingDelegate/contentBrowserCommentTooltipViewController(inEdition:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18CommentingDelegateP42contentBrowserCommentTooltipViewController9inEditionSo06UIViewI0CSgAA16PSEEditionSource_p_tF"
  },
  "title" : "contentBrowserCommentTooltipViewController(inEdition:)"
}
-->

# contentBrowserCommentTooltipViewController(inEdition:)

Returns a view controller to present as a popover tooltip anchored to
commenting icons in the content browser.

```
@MainActor func contentBrowserCommentTooltipViewController(inEdition source: PSEEditionSource) -> UIViewController?
```

## Parameters

`source`

The current edition.

## Return Value

A view controller to present as a popover, or `nil`.

## Discussion

The SDK presents the returned view controller as a popover above the
comment count of the first fully visible cell that shows one. Return
`nil` to show no tooltip.

Note: A default implementation is provided that returns `nil`.