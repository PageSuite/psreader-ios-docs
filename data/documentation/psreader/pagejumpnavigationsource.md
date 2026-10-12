<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PageJumpNavigationSource",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24PageJumpNavigationSourceV"
  },
  "title" : "PageJumpNavigationSource"
}
-->

# PageJumpNavigationSource

The scroll-source token the reader passes when a media overlay or link
triggers a jump to a page.

```
struct PageJumpNavigationSource
```

## Topics

### Reading the Jump

[`targetPageGUID`](/documentation/PSReader/PageJumpNavigationSource/targetPageGUID)

The GUID of the page the jump targets. Look the page up to inspect
it, for example to check whether the jump lands on an article.

[`sourcePage`](/documentation/PSReader/PageJumpNavigationSource/sourcePage)

The page whose content triggered the jump, or `nil` when unknown.

[`mediaObject`](/documentation/PSReader/PageJumpNavigationSource/mediaObject)

The hotspot that triggered the jump, or `nil` when the jump didn’t
come from a hotspot. The reader tags page jumps from
[`PSEMediaArticleOverlay`](/documentation/PSReader/PSEMediaArticleOverlay) and [`PSEMediaLinkOverlay`](/documentation/PSReader/PSEMediaLinkOverlay) taps, which
set it.

### Tagging Your Own Jumps

[`init(sourcePage:mediaObject:targetPageGUID:)`](/documentation/PSReader/PageJumpNavigationSource/init(sourcePage:mediaObject:targetPageGUID:))

Creates a page-jump token.

