<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/SectionItem",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC11SectionItemO"
  },
  "title" : "CarouselViewController.SectionItem"
}
-->

# CarouselViewController.SectionItem

Defines the top level of paging sections in the carousel.

```
enum SectionItem
```

## Overview

The carousel supports three section patterns:

- **Single section**: One content source per top-level tab (``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/SectionItem/section(_:)``).
- **Subsections**: Multiple content sources grouped under one top-level tab (``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/SectionItem/subsections(_:_:)``).
- **Dynamic archive**: Content loaded remotely from a shortcode (``doc://com.pagesuite.PSReader/documentation/PSReader/CarouselViewController/SectionItem/dynamicArchive(_:shortcode:config:)``).

> SeeAlso: <doc://com.pagesuite.PSReader/documentation/PSReader/Setting-Up-the-Carousel>

## Topics

### Loading Sections From the Portal

[`CarouselViewController.SectionItem.dynamicArchive(_:shortcode:config:)`](/documentation/PSReader/CarouselViewController/SectionItem/dynamicArchive(_:shortcode:config:))

A dynamic archive that loads publications for the given shortcode.

### Defining Sections Yourself

[`CarouselViewController.SectionItem.section(_:)`](/documentation/PSReader/CarouselViewController/SectionItem/section(_:))

A single section with the given [`CarouselViewController.Content`](/documentation/PSReader/CarouselViewController/Content).

[`CarouselViewController.SectionItem.subsections(_:_:)`](/documentation/PSReader/CarouselViewController/SectionItem/subsections(_:_:))

Multiple subsections with the given section name and [`CarouselViewController.Content`](/documentation/PSReader/CarouselViewController/Content).

