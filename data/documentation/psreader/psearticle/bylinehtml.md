<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticle/bylineHTML",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEArticle(py)bylineHTML"
  },
  "title" : "bylineHTML"
}
-->

# bylineHTML

Byline as HTML for template rendering. Authors that have an email are wrapped in a
`<a href="mailto:…">` so the article template’s `.author a` rule colors them; authors
without an email stay as plain text. `byline`/`author` remain plain text for analytics,
audio, bookmarks and TTS — only this property carries markup.

```
@objc var bylineHTML: String?
```