<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareDelegateP"
  },
  "title" : "ShareDelegate"
}
-->

# ShareDelegate

Delegate protocol used to provide sharing functionality within the SDK.

```
protocol ShareDelegate
```

## Overview

The reader asks its share delegate whether the current page can be
shared, which shows or hides the Share button, and for the items to hand
the share sheet when the user taps it.

> Tip: Most integrations should use the built-in ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider`` with a
> ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider/SharePolicy`` rather than implementing `ShareDelegate`
> directly. Implement this protocol only if you need fully custom sharing logic.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareContext``

## Topics

### Sharing Feed Pages

[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/shareContext(forPage:inEdition:inPublished:))

Provides the sharing context for a specific page.

[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/ShareDelegate/isShareable(page:inEdition:inPublished:))

Determines if a page within an edition is shareable.

### Replica Editions

[`shareContext(forSpread:inReplicaEdition:)`](/documentation/PSReader/ShareDelegate/shareContext(forSpread:inReplicaEdition:))

Provides the sharing context for a replica page spread.

[`isShareable(spread:inReplicaEdition:)`](/documentation/PSReader/ShareDelegate/isShareable(spread:inReplicaEdition:))

Determines if a replica page spread is shareable.

