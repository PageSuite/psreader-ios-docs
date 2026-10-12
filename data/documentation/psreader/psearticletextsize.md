<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEArticleTextSize",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader18PSEArticleTextSizeO"
  },
  "title" : "PSEArticleTextSize"
}
-->

# PSEArticleTextSize

The user-selectable text size for templated article pages.

```
enum PSEArticleTextSize
```

## Overview

The selection is global and persists across launches. Changing it does
not re-render pages that are already on screen — call
[`reloadPageContent()`](/documentation/PSReader/PSEditionReaderViewController/reloadPageContent()) on any open reader
afterwards. Only pages whose [`hasResizableText`](/documentation/PSReader/PSEPage/hasResizableText) is `true`
respond; PDF and advert pages are unaffected (use that flag to decide
whether to offer a text-size control for the current page).

```swift
PSEArticleTextSize.current = .large
reader.reloadPageContent()
```

The four sizes scale article text from roughly 0.85× ([`PSEArticleTextSize.small`](/documentation/PSReader/PSEArticleTextSize/small)) through
1× ([`PSEArticleTextSize.medium`](/documentation/PSReader/PSEArticleTextSize/medium), the default) to 2× ([`PSEArticleTextSize.extraLarge`](/documentation/PSReader/PSEArticleTextSize/extraLarge)).

## Topics

### Reading the User’s Choice

[`current`](/documentation/PSReader/PSEArticleTextSize/current)

The current selection, or [`PSEArticleTextSize.medium`](/documentation/PSReader/PSEArticleTextSize/medium) when the user has never chosen.

### Sizes

[`PSEArticleTextSize.small`](/documentation/PSReader/PSEArticleTextSize/small)

The smallest size: article templates scale text by 0.85.

[`PSEArticleTextSize.medium`](/documentation/PSReader/PSEArticleTextSize/medium)

The default size: article templates scale text by 1.

[`PSEArticleTextSize.large`](/documentation/PSReader/PSEArticleTextSize/large)

A larger size: article templates scale text by 1.5.

[`PSEArticleTextSize.extraLarge`](/documentation/PSReader/PSEArticleTextSize/extraLarge)

The largest size: article templates scale text by 2.

