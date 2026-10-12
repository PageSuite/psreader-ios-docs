<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSESection",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSESection"
  },
  "title" : "PSESection"
}
-->

# PSESection

A named section of an edition (news, sport, …) grouping its articles.

```
@objc class PSESection
```

## Overview

Build section navigation from [`sections`](/documentation/PSReader/PSEEdition/sections) and jump with
[`scrollTo(section:source:)`](/documentation/PSReader/PSEditionReaderViewController/scrollTo(section:source:)).

## Topics

### Identity

[`sectionguid`](/documentation/PSReader/PSESection/sectionguid)

Unique identifier of the section (lowercase by contract).

### Display

[`name`](/documentation/PSReader/PSESection/name)

The section’s display name.

[`color`](/documentation/PSReader/PSESection/color)

The section’s theme color, as comma-separated red, green, and blue
components from 0 to 255 (for example `0,0,0`).

[`logourl`](/documentation/PSReader/PSESection/logourl)

URL of the section’s logo image.

### Content

[`coverpage`](/documentation/PSReader/PSESection/coverpage)

GUID of the page the section starts on.

[`articles`](/documentation/PSReader/PSESection/articles)

The articles belonging to the section.

