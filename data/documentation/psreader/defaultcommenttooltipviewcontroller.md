<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentTooltipViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)DefaultCommentTooltipViewController"
  },
  "title" : "DefaultCommentTooltipViewController"
}
-->

# DefaultCommentTooltipViewController

A popover tooltip view controller with a text label and close button.

```
@MainActor class DefaultCommentTooltipViewController
```

## Overview

Returned by [`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) for both the article view and
content browser tooltip positions. The SDK presents it as a
`UIPopoverPresentationController` popover anchored to the relevant
commenting UI element.

Set [`onAppear`](/documentation/PSReader/DefaultCommentTooltipViewController/onAppear) to be notified when the tooltip is actually displayed.
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) uses this to persist the “shown” state in
`UserDefaults`.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``

## Topics

### Creating a Tooltip

[`init(text:font:preferredWidth:foregroundColor:backgroundColor:)`](/documentation/PSReader/DefaultCommentTooltipViewController/init(text:font:preferredWidth:foregroundColor:backgroundColor:))

Creates a new tooltip view controller.

### Responding to Appearance

[`onAppear`](/documentation/PSReader/DefaultCommentTooltipViewController/onAppear)

Called when the tooltip appears on screen (`viewDidAppear`).

