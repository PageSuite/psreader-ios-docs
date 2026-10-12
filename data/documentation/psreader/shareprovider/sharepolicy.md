<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareProvider/SharePolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader13ShareProviderC0B6PolicyO"
  },
  "title" : "ShareProvider.SharePolicy"
}
-->

# ShareProvider.SharePolicy

Defines the sharing strategy used by the SDK.

```
enum SharePolicy
```

## Overview

Used to configure the SDK’s share functionality, selecting between sharing links
to the web based reader or direct links to articles hosted externally
(such as a publisher’s website).

If sharing is disabled, no sharing functionality will be provided by the SDK.

> Tip: The default ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration`` uses `.onlyArticleLink()` when no
> explicit share delegate is provided.

## Topics

### Sharing Links

[`ShareProvider.SharePolicy.preferWebReader(webProvider:articleLinkProvider:)`](/documentation/PSReader/ShareProvider/SharePolicy/preferWebReader(webProvider:articleLinkProvider:))

Prefers sharing links to the web reader but falls back to direct
article links if web reader links are unavailable.

[`ShareProvider.SharePolicy.preferArticleLink(webProvider:articleLinkProvider:)`](/documentation/PSReader/ShareProvider/SharePolicy/preferArticleLink(webProvider:articleLinkProvider:))

Prefers sharing direct links to articles on the publisher’s website but
falls back to the web reader when article links are unavailable.

[`ShareProvider.SharePolicy.onlyWebReader(webProvider:)`](/documentation/PSReader/ShareProvider/SharePolicy/onlyWebReader(webProvider:))

Shares exclusively to the web reader.

[`ShareProvider.SharePolicy.onlyArticleLink(articleLinkProvider:)`](/documentation/PSReader/ShareProvider/SharePolicy/onlyArticleLink(articleLinkProvider:))

Shares only direct article links to content on the publisher’s website.

### Turning Sharing Off

[`ShareProvider.SharePolicy.disabled`](/documentation/PSReader/ShareProvider/SharePolicy/disabled)

Completely disables sharing functionality within the SDK.
When this policy is active, the SDK won’t display any share options.

