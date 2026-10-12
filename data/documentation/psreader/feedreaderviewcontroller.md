<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/FeedReaderViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)FeedReaderViewController"
  },
  "title" : "FeedReaderViewController"
}
-->

# FeedReaderViewController

A standalone view controller for displaying an edition on PageSuite’s
current system, classic PDF or responsive.

```
@MainActor class FeedReaderViewController
```

## Overview

Use this view controller to embed the prebuilt reader within your app’s
interface. Each initializer corresponds to a different way of identifying
which edition to open — by a known published object, by publication, by
edition GUID, or by shortcode.

## Usage

```swift
let reader = FeedReaderViewController(
    globalConfig: globalConfig,
    publicationGUID: "PUBLICATION_GUID",
    editionGUID: "EDITION_GUID"
)

reader.modalPresentationStyle = .fullScreen
self.present(reader, animated: true)
```

To open editions in it from your own screens, see
[Presenting the Prebuilt Reader](/documentation/PSReader/Presenting-the-Prebuilt-Reader).

The reader takes your app configuration from the `globalConfig` you
create it with: its [`remoteConfig`](/documentation/PSReader/GlobalConfiguration/remoteConfig), as it is at
that moment. A [`ReaderConfiguration`](/documentation/PSReader/ReaderConfiguration) doesn’t carry one. The shortcode
initializer loads the configuration itself unless `remoteConfig` is
already the one for that shortcode.

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArchiveViewController``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ReaderConfiguration``

## Topics

### Opening an Edition

[`init(globalConfig:readerConfig:published:openingPage:)`](/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:published:openingPage:))

Opens a known published edition directly.

[`init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:)`](/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:latestEditionForPublication:publicationName:publishedDomain:openingPage:))

Opens the latest edition for a publication.

[`init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:)`](/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:publicationGUID:publicationName:editionGUID:publishedDomain:openingPage:))

Opens a specific edition within a publication.

[`init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:)`](/documentation/PSReader/FeedReaderViewController/init(globalConfig:readerConfig:shortcode:editionGUID:openingPage:))

Opens an edition by GUID using a shortcode to resolve the application configuration.

### Choosing the Opening Page

[`FeedReaderViewController.OpeningPage`](/documentation/PSReader/FeedReaderViewController/OpeningPage)

Specifies which page to open when the reader launches.

