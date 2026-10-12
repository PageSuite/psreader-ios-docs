<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareProvider",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareProviderC"
  },
  "title" : "ShareProvider"
}
-->

# ShareProvider

A composite share provider allowing multiple share strategies to be chained.
Configure this provider to choose preferred or fallback sharing behaviors.

```
class ShareProvider
```

## Quick Start

`ShareProvider` is the recommended way to configure sharing. Choose a
[`ShareProvider.SharePolicy`](/documentation/PSReader/ShareProvider/SharePolicy) that matches your needs:

```swift
// Share direct article links (default behavior)
let share = ShareProvider(sharePolicy: .onlyArticleLink())

// Share web reader links with article link fallback
let webProvider = WebReaderShareProvider(urlMask: nil, shortCode: "SHORTCODE")
let share = ShareProvider(sharePolicy: .preferWebReader(webProvider: webProvider))

// Disable sharing entirely
let share = ShareProvider(sharePolicy: .disabled)
```

Building your own reader screen? [Adding a Share Button](/documentation/PSReader/Adding-a-Share-Button) uses the
same provider behind your own button.

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareProvider/SharePolicy``

## Topics

### Creating a Share Provider

[`init(sharePolicy:)`](/documentation/PSReader/ShareProvider/init(sharePolicy:))

Initializes a new instance with the given sharing policy.

[`ShareProvider.SharePolicy`](/documentation/PSReader/ShareProvider/SharePolicy)

Defines the sharing strategy used by the SDK.

### Sharing Feed Pages

[`shareContext(forPage:inEdition:inPublished:)`](/documentation/PSReader/ShareProvider/shareContext(forPage:inEdition:inPublished:))

Provides the first valid share context from the configured providers.

[`isShareable(page:inEdition:inPublished:)`](/documentation/PSReader/ShareProvider/isShareable(page:inEdition:inPublished:))

Determines shareability by checking the configured providers.

### Replica Editions

[`shareContext(forSpread:inReplicaEdition:)`](/documentation/PSReader/ShareProvider/shareContext(forSpread:inReplicaEdition:))

Provides the first valid share context from the configured providers for replica spreads.

[`isShareable(spread:inReplicaEdition:)`](/documentation/PSReader/ShareProvider/isShareable(spread:inReplicaEdition:))

Determines shareability by checking the configured providers for replica spreads.

