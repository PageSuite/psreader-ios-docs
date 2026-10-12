<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchResult/formattedSnippet(font:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12SearchResultV16formattedSnippet4fontSo18NSAttributedStringCSgSo6UIFontC_tF"
  },
  "title" : "formattedSnippet(font:)"
}
-->

# formattedSnippet(font:)

Returns the [`snippet`](/documentation/PSReader/SearchResult/snippet) as an attributed string with matched terms in bold.

```
func formattedSnippet(font: UIFont) -> NSAttributedString?
```

## Parameters

`font`

The base font for the snippet text. Bold segments use
the bold variant of this font.

## Return Value

A formatted attributed string, or `nil` if [`snippet`](/documentation/PSReader/SearchResult/snippet) is `nil`.

## Discussion

The search API returns snippets with `<b>...</b>` tags wrapping matched
terms. This method parses those tags and returns an `NSAttributedString`
with bold styling applied using the provided font.

Use this to display formatted search snippets in UIKit (`UILabel`,
`UITextView`) or bridge to SwiftUI via `AttributedString`.