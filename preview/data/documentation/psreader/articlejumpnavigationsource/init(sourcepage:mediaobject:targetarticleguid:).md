<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArticleJumpNavigationSource/init(sourcePage:mediaObject:targetArticleGUID:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27ArticleJumpNavigationSourceV10sourcePage11mediaObject06targetB4GUIDAcA7PSEPageCSg_AA08PSEMediaI0CSgSStcfc"
  },
  "title" : "init(sourcePage:mediaObject:targetArticleGUID:)"
}
-->

# init(sourcePage:mediaObject:targetArticleGUID:)

Creates an article-jump token.

```
init(sourcePage: PSEPage? = nil, mediaObject: PSEMediaObject? = nil, targetArticleGUID: String)
```

## Parameters

`sourcePage`

The page whose content triggered the jump.

`mediaObject`

The hotspot that triggered the jump, if any.

`targetArticleGUID`

The GUID of the article the jump targets.

## Discussion

The reader creates these for its own jumps. Create one yourself only
to pass as the `source` of a `scrollTo` call, so your
[`PSEditionReaderViewController.ScrollDelegate`](/documentation/PSReader/PSEditionReaderViewController/ScrollDelegate-swift.protocol) handles a jump you
trigger the same way as the reader’s.