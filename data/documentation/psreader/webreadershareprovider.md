<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/WebReaderShareProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22WebReaderShareProviderC"
  },
  "title" : "WebReaderShareProvider"
}
-->

# WebReaderShareProvider

A [`ShareDelegate`](/documentation/PSReader/ShareDelegate) that shares links to pages in PageSuite’s web reader.

```
class WebReaderShareProvider
```

## Overview

Each link opens the edition in the web reader at the shared page, in any
browser. Use it on its own or as the web reader provider in a
[`ShareProvider`](/documentation/PSReader/ShareProvider) policy.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ArticleLinkShareProvider``

## Topics

### Creating a Share Provider

[`init(urlMask:shortCode:)`](/documentation/PSReader/WebReaderShareProvider/init(urlMask:shortCode:))

Initializes a new web reader share provider.

### Building Web Reader Links

[`urlMask`](/documentation/PSReader/WebReaderShareProvider/urlMask)

The host of your own web reader domain, such as
`reader.example.com`, or `nil` for PageSuite’s web reader.

[`shortCode`](/documentation/PSReader/WebReaderShareProvider/shortCode)

Your app’s shortcode, which web reader links include.

### Sharing Feed Pages

[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/WebReaderShareProvider/shareContext(forPage:inEdition:inPublished:))

Provides a `ShareContext` linking directly to content within the web reader.

[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/WebReaderShareProvider/isShareable(page:inEdition:inPublished:))

Determines shareability based on the presence of necessary identifiers.

### Replica Editions

[`shareContext(forSpread:inReplicaEdition:)`](/documentation/PSReader/WebReaderShareProvider/shareContext(forSpread:inReplicaEdition:))

Provides a `ShareContext` for replica page spreads.

[`isShareable(spread:inReplicaEdition:)`](/documentation/PSReader/WebReaderShareProvider/isShareable(spread:inReplicaEdition:))

Determines shareability for replica page spreads.
Always `true`: pages link to the replica web reader, and articles to
their article view there.

