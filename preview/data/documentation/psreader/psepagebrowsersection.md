<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEPageBrowserSection",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEPageBrowserSection"
  },
  "title" : "PSEPageBrowserSection"
}
-->

# PSEPageBrowserSection

A section grouping used to build a sectioned page-browser UI.

```
@objc class PSEPageBrowserSection
```

## Overview

Read an edition’s sections from [`pageBrowserSections`](/documentation/PSReader/PSEEdition/pageBrowserSections). To
build a page browser from them, see [Building a Page Browser](/documentation/PSReader/Building-a-Page-Browser).

## Topics

### Display

[`title`](/documentation/PSReader/PSEPageBrowserSection/title)

The section’s title, for display in a page browser.

[`color`](/documentation/PSReader/PSEPageBrowserSection/color)

The section’s theme color, taken from the edition’s section of the
same name, as comma-separated red, green, and blue components from 0
to 255 (for example `0,0,0`); `nil` when there’s none.

### Position

[`num`](/documentation/PSReader/PSEPageBrowserSection/num)

The index in [`pages`](/documentation/PSReader/PSEEdition/pages) of the section’s first page.

