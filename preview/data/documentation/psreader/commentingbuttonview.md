<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CommentingButtonView",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader20CommentingButtonViewP"
  },
  "title" : "CommentingButtonView"
}
-->

# CommentingButtonView

A custom view that acts as a comment button within the reader.

```
@MainActor protocol CommentingButtonView : UIView
```

## Overview

Implement this protocol to provide a custom comment button appearance.
The SDK manages tap handling — store the `onTap` closure and invoke it
when the user taps the button.

[`DefaultCommentingButton`](/documentation/PSReader/DefaultCommentingButton) provides a ready-made pill-shaped button
that conforms to this protocol.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingButton``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingDelegate/commentButton(forArticle:inEdition:onTap:)``

## Topics

### Handling Taps

[`onTap`](/documentation/PSReader/CommentingButtonView/onTap)

Closure provided by the SDK for handling tap events.

### Updating the Label

[`updateText(_:)`](/documentation/PSReader/CommentingButtonView/updateText(_:))

Updates the button’s displayed text.

