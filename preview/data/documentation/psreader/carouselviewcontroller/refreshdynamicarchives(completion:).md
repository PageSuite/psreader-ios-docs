<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/refreshDynamicArchives(completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC22refreshDynamicArchives10completionyySbcSg_tF"
  },
  "title" : "refreshDynamicArchives(completion:)"
}
-->

# refreshDynamicArchives(completion:)

Refreshes the publication lists in dynamic archives. Updates subsections if needed.

```
@MainActor func refreshDynamicArchives(completion: ((Bool) -> Void)? = nil)
```

## Parameters

`completion`

Optional completion handler with boolean success flag.

## Discussion

Only sections created with
[`CarouselViewController.SectionItem.dynamicArchive(_:shortcode:config:)`](/documentation/PSReader/CarouselViewController/SectionItem/dynamicArchive(_:shortcode:config:)) refresh. Static
sections configured with [`CarouselViewController.SectionItem.section(_:)`](/documentation/PSReader/CarouselViewController/SectionItem/section(_:)) or
[`CarouselViewController.SectionItem.subsections(_:_:)`](/documentation/PSReader/CarouselViewController/SectionItem/subsections(_:_:)) stay as they are.