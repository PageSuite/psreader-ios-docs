<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmark/editionSource(mode:onProgress:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSEBookmarkO13editionSource4mode10onProgressAA010PSEEditionD0_p6source_AA7PSEPageCSg11openingPagetAA0B8OpenModeO_ySfcSgtYaKF"
  },
  "title" : "editionSource(mode:onProgress:)"
}
-->

# editionSource(mode:onProgress:)

Convenience overload that opens against all currently saved bookmarks.

```
func editionSource(mode: PSEBookmarkOpenMode = .preferSourceEdition, onProgress: ((Float) -> Void)? = nil) async throws -> (source: PSEEditionSource, openingPage: PSEPage?)
```