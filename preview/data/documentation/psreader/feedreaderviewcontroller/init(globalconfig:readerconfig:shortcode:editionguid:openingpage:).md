<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24FeedReaderViewControllerC12globalConfig06readerG09shortcode11editionGUID11openingPageAcA19GlobalConfigurationV_AA0cO0VSgS2SAC07OpeningM0OSgtcfc"
  },
  "title" : "init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)"
}
-->

# init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)

Opens an edition by GUID using a shortcode to resolve the application configuration.

```
@MainActor convenience init(globalConfig: GlobalConfiguration, readerConfig: ReaderConfiguration? = nil, shortcode: String, editionGUID: String, openingPage: OpeningPage? = nil)
```

## Parameters

`globalConfig`

The global SDK configuration.

`readerConfig`

Optional reader appearance configuration. Defaults to the global theme.

`shortcode`

The application shortcode used to resolve configuration.

`editionGUID`

The GUID of the edition to open.

`openingPage`

Optional page to open to on launch.

## Discussion

If the global configuration’s remote config already matches the given shortcode,
the resolved application is used directly. Otherwise, the shortcode is used to
fetch the application configuration from the server.