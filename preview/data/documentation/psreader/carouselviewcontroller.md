<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)CarouselViewController"
  },
  "title" : "CarouselViewController"
}
-->

# CarouselViewController

The primary view controller provided by the SDK for presenting digital publication
content through an intuitive carousel interface.

```
@MainActor class CarouselViewController
```

## Overview

`CarouselViewController` serves as the central UI component of the SDK, offering
users seamless navigation between multiple content sources such as archives of
editions on PageSuite’s current system, legacy replica editions, bookmarked
content, and downloaded editions.

The interface supports two levels of paging, sections and subsections, with
horizontal ribbons, allowing quick and intuitive browsing through publications.

The view controller can be configured via a [`CarouselConfiguration`](/documentation/PSReader/CarouselConfiguration) object.
Utilize this configuration to align the visual presentation, navigation behavior,
theming, branding, and various delegate interactions (e.g., sharing, paywalls,
advertisements, and media playback).

The content in the carousel can be:

- An archive of editions on PageSuite’s current system (classic PDF or
  responsive).
- An archive of legacy replica editions.
- A dynamic archive loaded from an app shortcode.
- Local bookmarks.
- Local downloads.

## Usage

The recommended approach uses a **dynamic archive** that loads content from a
shortcode configured in the PageSuite portal:

```swift
let globalConfig = GlobalConfiguration(
    apiKey: "API_KEY",
    accountGUID: "ACCOUNT_GUID"
)

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .dynamicArchive("Editions", shortcode: "SHORTCODE")
    ]
)

present(carousel, animated: true)
```

You can also configure sections manually to combine multiple content sources:

```swift
let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [
        .subsections("Editions", [
            .init(name: "Daily", type: .feedArchive(guid: "DAILY_GUID")),
            .init(name: "Weekend", type: .feedArchive(guid: "WEEKEND_GUID"))
        ]),
        .section(.init(name: "Bookmarks", type: .bookmarks(type: .all))),
        .section(.init(name: "Downloads", type: .downloads(type: .all)))
    ]
)
```

The carousel relies on the call to [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:))
your app makes at launch; see [Initialize the SDK](/documentation/PSReader/Getting-Started#Initialize-the-SDK).

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Getting-Started>

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration``

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselConfiguration``

## Topics

### Creating a Carousel

[`init(globalConfig:carouselConfig:header:sections:)`](/documentation/PSReader/CarouselViewController/init(globalConfig:carouselConfig:header:sections:))

Creates a `CarouselViewController` with the given config and content.

### Defining Sections

[`CarouselViewController.SectionItem`](/documentation/PSReader/CarouselViewController/SectionItem)

Defines the top level of paging sections in the carousel.

[`CarouselViewController.Content`](/documentation/PSReader/CarouselViewController/Content)

Describes a section or subsection page.

[`CarouselViewController.ContentType`](/documentation/PSReader/CarouselViewController/ContentType)

Describes the content type of a section or subsection page.

[`CarouselViewController.Layout`](/documentation/PSReader/CarouselViewController/Layout)

Describes how a dynamic archive lays out a group of publications, as
set in the PageSuite portal.

### Updating the Carousel

[`refreshDynamicArchives(completion:)`](/documentation/PSReader/CarouselViewController/refreshDynamicArchives(completion:))

Refreshes the publication lists in dynamic archives. Updates subsections if needed.

[`setRibbonLayout(section:subsectionAlignment:)`](/documentation/PSReader/CarouselViewController/setRibbonLayout(section:subsectionAlignment:))

Re-lays the section and subsection ribbons for a new width class without
rebuilding the carousel.

