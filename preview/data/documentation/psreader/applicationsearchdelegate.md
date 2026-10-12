<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ApplicationSearchDelegate",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25ApplicationSearchDelegateC"
  },
  "title" : "ApplicationSearchDelegate"
}
-->

# ApplicationSearchDelegate

A [`SearchDelegate`](/documentation/PSReader/SearchDelegate) that derives search publications from a `PSAppConfig`
or fetches one lazily from a shortcode.

```
class ApplicationSearchDelegate
```

## Overview

Use this when you need search functionality outside of the carousel, such as
when presenting search from a reader’s settings menu.

```swift
// From a shortcode (fetches application lazily on first search)
let delegate = ApplicationSearchDelegate(shortcode: "SHORTCODE", readerConfig: readerConfig)

// From an existing application
let delegate = ApplicationSearchDelegate(application: app, readerConfig: readerConfig)
```

To set up the prebuilt search screen, see [Search](/documentation/PSReader/Search).

## Topics

### Creating a Search Delegate

[`init(shortcode:readerConfig:)`](/documentation/PSReader/ApplicationSearchDelegate/init(shortcode:readerConfig:))

Creates a search delegate that fetches the application from a shortcode on first use.

[`init(application:readerConfig:)`](/documentation/PSReader/ApplicationSearchDelegate/init(application:readerConfig:))

Creates a search delegate from an existing application.

### Supplying Publications

[`searchPublications(completion:)`](/documentation/PSReader/ApplicationSearchDelegate/searchPublications(completion:))

Provides a searchable publication for each publication in the archive
of the `PSAppConfig`.

### Opening Results

[`searchReaderConfiguration(for:)`](/documentation/PSReader/ApplicationSearchDelegate/searchReaderConfiguration(for:))

Returns the reader configuration for opening results from a
publication.

