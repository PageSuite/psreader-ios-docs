<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24FeedReaderViewControllerC12globalConfig06readerG027latestEditionForPublication15publicationName15publishedDomain11openingPageAcA19GlobalConfigurationV_AA0cT0VSgS2SSgAoC07OpeningR0OSgtcfc"
  },
  "title" : "init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:)"
}
-->

# init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:)

Opens the latest edition for a publication.

```
@MainActor convenience init(globalConfig: GlobalConfiguration, readerConfig: ReaderConfiguration? = nil, latestEditionForPublication publicationGUID: String, publicationName: String? = nil, publishedDomain: String? = nil, openingPage: OpeningPage? = nil)
```

## Parameters

`globalConfig`

The global SDK configuration.

`readerConfig`

Optional reader appearance configuration. Defaults to the global theme.

`publicationGUID`

The publication GUID to fetch the latest edition for.

`publicationName`

Optional display name for the publication.

`publishedDomain`

Optional base domain used for loading edition content.

`openingPage`

Optional page to open to on launch.