<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingButton",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)DefaultCommentingButton"
  },
  "title" : "DefaultCommentingButton"
}
-->

# DefaultCommentingButton

A pill-shaped comment button with a border and centered text label.

```
@MainActor class DefaultCommentingButton
```

## Overview

Returned by [`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/DefaultCommentingProvider/commentButton(forArticle:inEdition:onTap:)).
Displays a rounded pill with a 1 px border, a separator keyline at the top,
and a centered text label. The button is full-width and positioned at the
bottom of the article view by the SDK.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CommentingButtonView``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/DefaultCommentingProvider``

## Topics

### Creating a Button

[`init(text:foregroundColor:font:pillIdealWidth:pillHorizontalMargin:pillTopPadding:pillBottomPadding:labelVerticalPadding:labelHorizontalPadding:)`](/documentation/PSReader/DefaultCommentingButton/init(text:foregroundColor:font:pillIdealWidth:pillHorizontalMargin:pillTopPadding:pillBottomPadding:labelVerticalPadding:labelHorizontalPadding:))

Creates a new comment button.

### Handling Taps

[`onTap`](/documentation/PSReader/DefaultCommentingButton/onTap)

Called when the user taps the button.

### Updating the Label

[`updateText(_:)`](/documentation/PSReader/DefaultCommentingButton/updateText(_:))

Replaces the button’s label text.

