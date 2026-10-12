<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24FeedReaderViewControllerC12globalConfig06readerG015publicationGUID0I4Name07editionJ015publishedDomain11openingPageAcA19GlobalConfigurationV_AA0cR0VSgS2SSgSSApC07OpeningP0OSgtcfc"
  },
  "title" : "init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:)"
}
-->

# init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:)

Opens a specific edition within a publication.

```
@MainActor convenience init(globalConfig: GlobalConfiguration, readerConfig: ReaderConfiguration? = nil, publicationGUID: String, publicationName: String? = nil, editionGUID: String, publishedDomain: String? = nil, openingPage: OpeningPage? = nil)
```

## Parameters

`globalConfig`

The global SDK configuration.

`readerConfig`

Optional reader appearance configuration. Defaults to the global theme.

`publicationGUID`

The publication GUID containing the edition.

`publicationName`

Optional display name for the publication.

`editionGUID`

The GUID of the specific edition to open.

`publishedDomain`

Optional base domain used for loading edition content.

`openingPage`

Optional page to open to on launch.