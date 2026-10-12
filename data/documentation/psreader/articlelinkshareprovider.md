<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ArticleLinkShareProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader24ArticleLinkShareProviderC"
  },
  "title" : "ArticleLinkShareProvider"
}
-->

# ArticleLinkShareProvider

A [`ShareDelegate`](/documentation/PSReader/ShareDelegate) providing direct article links on the publication’s website.

```
class ArticleLinkShareProvider
```

## Overview

This provider generates links directly to individual articles hosted on the
publisher’s website.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/WebReaderShareProvider``

## Topics

### Creating a Share Provider

[`init()`](/documentation/PSReader/ArticleLinkShareProvider/init())

Initializes a new instance of `ArticleLinkShareProvider`.

### Sharing Feed Pages

[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ArticleLinkShareProvider/shareContext(forPage:inEdition:inPublished:))

Provides a `ShareContext` linking directly to the article URL on the publisher’s website.

[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/ArticleLinkShareProvider/isShareable(page:inEdition:inPublished:))

Determines whether an article-based page is shareable.
A page is shareable if it has exactly one article with a valid external share URL.

### Replica Editions

[`shareContext(forSpread:inReplicaEdition:)`](/documentation/PSReader/ArticleLinkShareProvider/shareContext(forSpread:inReplicaEdition:))

Provides a `ShareContext` for replica article spreads only.

[`isShareable(spread:inReplicaEdition:)`](/documentation/PSReader/ArticleLinkShareProvider/isShareable(spread:inReplicaEdition:))

Determines shareability for replica page spreads.
Only article spreads with a valid share link are shareable.

