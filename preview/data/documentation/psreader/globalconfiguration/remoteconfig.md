<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/GlobalConfiguration/remoteConfig",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19GlobalConfigurationV12remoteConfigAA05PSAppE0CSgvp"
  },
  "title" : "remoteConfig"
}
-->

# remoteConfig

The app configuration from the PageSuite portal, which some reader
features read their settings from.

```
var remoteConfig: PSAppConfig?
```

## Discussion

Most apps leave it `nil`. A carousel with a dynamic archive loads the
configuration for its shortcode and uses that instead of this value,
and so does
[`init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)`](/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)).
The other prebuilt screens, including a [`FeedReaderViewController`](/documentation/PSReader/FeedReaderViewController)
that your own lists open, use this value. Without it, these features
go without their portal settings:

- in-article adverts;
- advert pages served through a third-party ad loader;
- article widgets;
- the masthead logo in templated pages, when your ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/assetDelegate``
  doesn’t supply one.

If your editions use any of them, load the configuration with
[`AppConfigService`](/documentation/PSReader/AppConfigService) and set it here.

A custom UI doesn’t read this property: it passes the configuration
to [`open(edition:openingPage:application:)`](/documentation/PSReader/PSEditionReaderViewController/open(edition:openingPage:application:)),
and its reader takes the masthead logo from the reader’s media
delegate, not the configuration. See
[Passing the App Configuration](/documentation/PSReader/Hosting-the-Reader#Passing-the-App-Configuration).

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Configuring-the-Prebuilt-UI#The-App-Configuration>