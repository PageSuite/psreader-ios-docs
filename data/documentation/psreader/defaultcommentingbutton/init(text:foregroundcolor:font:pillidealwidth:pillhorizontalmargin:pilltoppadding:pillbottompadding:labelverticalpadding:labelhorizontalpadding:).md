<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingButton/init(text:foregroundColor:font:pillIdealWidth:pillHorizontalMargin:pillTopPadding:pillBottomPadding:labelVerticalPadding:labelHorizontalPadding:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23DefaultCommentingButtonC4text15foregroundColor4font14pillIdealWidth0I16HorizontalMargin0I10TopPadding0i6BottomO0013labelVerticalO00qlO0ACSS_So7UIColorCSo6UIFontC14CoreFoundation7CGFloatVA5Stcfc"
  },
  "title" : "init(text:foregroundColor:font:pillIdealWidth:pillHorizontalMargin:pillTopPadding:pillBottomPadding:labelVerticalPadding:labelHorizontalPadding:)"
}
-->

# init(text:foregroundColor:font:pillIdealWidth:pillHorizontalMargin:pillTopPadding:pillBottomPadding:labelVerticalPadding:labelHorizontalPadding:)

Creates a new comment button.

```
@MainActor init(text: String, foregroundColor: UIColor, font: UIFont, pillIdealWidth: CGFloat = 320, pillHorizontalMargin: CGFloat = 32, pillTopPadding: CGFloat = 16, pillBottomPadding: CGFloat = 16, labelVerticalPadding: CGFloat = 12, labelHorizontalPadding: CGFloat = 32)
```

## Parameters

`text`

The initial button text.

`foregroundColor`

The border and text color.

`font`

The label font.

`pillIdealWidth`

The preferred pill width. The pill shrinks if the
container less margins is narrower than `pillIdealWidth`. Default `320`.

`pillHorizontalMargin`

Minimum leading and trailing inset from the
container edges. Default `32`.

`pillTopPadding`

Top comment pill padding. Default `16`.

`pillBottomPadding`

Bottom comment pill padding. Default `16`.

`labelVerticalPadding`

Top and bottom label padding. Default `12`.

`labelHorizontalPadding`

Leading and trailing label padding. Default `32`.