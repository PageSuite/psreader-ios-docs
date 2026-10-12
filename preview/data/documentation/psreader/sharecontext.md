<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ShareContext",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader12ShareContextV"
  },
  "title" : "ShareContext"
}
-->

# ShareContext

A structure encapsulating information used to present shareable content.

```
struct ShareContext
```

## Overview

This structure is typically provided by implementing a custom [`ShareDelegate`](/documentation/PSReader/ShareDelegate).
It contains shareable content like URLs, images, or text, intended for use
with the iOS share sheet (`UIActivityViewController`).

```swift
let context = ShareContext(
    activityItems: [URL(string: "https://example.com/article")!],
    subject: "Check out this article"
)
```

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Sharing>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/ShareDelegate``

## Topics

### Creating a Share Context

[`init(activityItems:applicationActivities:subject:)`](/documentation/PSReader/ShareContext/init(activityItems:applicationActivities:subject:))

Initializes a new share context with provided items and optional subject and activities.

### Share Sheet Contents

[`activityItems`](/documentation/PSReader/ShareContext/activityItems)

Items to be shared, such as URLs, images, or text.

[`applicationActivities`](/documentation/PSReader/ShareContext/applicationActivities)

Optional additional activities to include when presenting the sharing UI.

[`subject`](/documentation/PSReader/ShareContext/subject)

An optional subject line for sharing activities (e.g., emails).

