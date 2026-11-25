<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentTooltipViewController/init(text:font:preferredWidth:foregroundColor:backgroundColor:eyebrow:title:accentColor:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader35DefaultCommentTooltipViewControllerC4text4font14preferredWidth15foregroundColor010backgroundL07eyebrow5title06accentL0ACSS_So6UIFontC14CoreFoundation7CGFloatVSo7UIColorCSgASSSSgAtStcfc"
  },
  "title" : "init(text:font:preferredWidth:foregroundColor:backgroundColor:eyebrow:title:accentColor:)"
}
-->

# init(text:font:preferredWidth:foregroundColor:backgroundColor:eyebrow:title:accentColor:)

Creates a new tooltip view controller.

```
@MainActor init(text: String, font: UIFont, preferredWidth: CGFloat = 320, foregroundColor: UIColor? = nil, backgroundColor: UIColor? = nil, eyebrow: String? = nil, title: String? = nil, accentColor: UIColor? = nil)
```

## Parameters

`text`

The tooltip message to display.

`font`

The typeface. The message uses it at 14 points, the title
in bold at 18, and the short label at 11.

`preferredWidth`

The preferred popover width. Default `320`.

`foregroundColor`

The title and close-button color. Default: the
SDK’s primary label color.

`backgroundColor`

The tooltip background color. Default: the SDK’s
background color.

`eyebrow`

The short label above the title, or `nil` for none.

`title`

The title, or `nil` for none.

`accentColor`

The short label’s color. Default: the SDK’s tertiary
label color.

## Discussion

The tooltip is laid out like the reader’s onboarding walkthrough: a
short label, a title, the message, and a close button. The SDK draws
the bubble and its arrow around it.