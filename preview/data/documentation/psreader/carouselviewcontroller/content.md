<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/Content",
  "metadataVersion" : "0.1.0",
  "role" : "Structure",
  "symbol" : {
    "kind" : "Structure",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC7ContentV"
  },
  "title" : "CarouselViewController.Content"
}
-->

# CarouselViewController.Content

Describes a section or subsection page.

```
struct Content
```

## Overview

```swift
let section = Content(name: "Daily", type: .feedArchive(guid: "DAILY_GUID"))
```

## Topics

### Creating a Section Page

[`init(name:type:)`](/documentation/PSReader/CarouselViewController/Content/init(name:type:))

Creates a `Content` object with the given name and type.

### Reading a Section Page

[`name`](/documentation/PSReader/CarouselViewController/Content/name)

The name of the section or subsection page. This is displayed in the
section or subsection ribbon.

[`type`](/documentation/PSReader/CarouselViewController/Content/type)

The [`CarouselViewController.ContentType`](/documentation/PSReader/CarouselViewController/ContentType) of the section or subsection page.

