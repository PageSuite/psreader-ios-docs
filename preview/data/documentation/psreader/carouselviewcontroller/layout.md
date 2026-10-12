<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CarouselViewController/Layout",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader22CarouselViewControllerC6LayoutO"
  },
  "title" : "CarouselViewController.Layout"
}
-->

# CarouselViewController.Layout

Describes how a dynamic archive lays out a group of publications, as
set in the PageSuite portal.

```
enum Layout
```

## Overview

The carousel reads the layout from the portal’s configuration; no
carousel API takes it.

## Topics

### Layouts

[`CarouselViewController.Layout.single`](/documentation/PSReader/CarouselViewController/Layout/single)

Each publication in the group gets its own archive page.

[`CarouselViewController.Layout.kiosk`](/documentation/PSReader/CarouselViewController/Layout/kiosk)

The group’s publications share one page: a grid of publications,
each linking to its archive.

### Reading a Layout From the Portal

[`init(string:)`](/documentation/PSReader/CarouselViewController/Layout/init(string:))

Creates a `Layout` from a string value.

