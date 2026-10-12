<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:published:openingPage:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24FeedReaderViewControllerC12globalConfig06readerG09published11openingPageAcA19GlobalConfigurationV_AA0cM0VSgAA12PSEPublishedCAC07OpeningK0OSgtcfc"
  },
  "title" : "init(globalConfig:readerConfig:published:openingPage:)"
}
-->

# init(globalConfig:readerConfig:published:openingPage:)

Opens a known published edition directly.

```
@MainActor convenience init(globalConfig: GlobalConfiguration, readerConfig: ReaderConfiguration? = nil, published: PSEPublished, openingPage: OpeningPage? = nil)
```

## Parameters

`globalConfig`

The global SDK configuration.

`readerConfig`

Optional reader appearance configuration. Defaults to the global theme.

`published`

The published edition object to display.

`openingPage`

Optional page to open to on launch.