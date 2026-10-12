<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/BookmarksViewController/init(globalConfig:bookmarksConfig:type:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23BookmarksViewControllerC12globalConfig09bookmarksF04typeAcA19GlobalConfigurationV_AA0bJ0VSgAJ12BookmarkTypeVtcfc"
  },
  "title" : "init(globalConfig:bookmarksConfig:type:)"
}
-->

# init(globalConfig:bookmarksConfig:type:)

Initializes a new standalone bookmarks view controller.

```
@MainActor init(globalConfig: GlobalConfiguration, bookmarksConfig: BookmarksConfiguration? = nil, type: BookmarksConfiguration.BookmarkType)
```

## Parameters

`globalConfig`

The global SDK configuration supplying defaults for fonts, colors, delegates, and credentials.

`bookmarksConfig`

Optional custom configuration for the bookmarks view appearance and behavior.
Defaults to settings inherited from `globalConfig` if not explicitly provided.

`type`

Specifies which types of bookmarkable content should be displayed. This can be useful for
displaying different types of bookmarks in dedicated views.