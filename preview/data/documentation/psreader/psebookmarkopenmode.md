<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEBookmarkOpenMode",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19PSEBookmarkOpenModeO"
  },
  "title" : "PSEBookmarkOpenMode"
}
-->

# PSEBookmarkOpenMode

How a bookmark should resolve to an edition source when opened.

```
enum PSEBookmarkOpenMode
```

## Topics

### Modes

[`PSEBookmarkOpenMode.preferSourceEdition`](/documentation/PSReader/PSEBookmarkOpenMode/preferSourceEdition)

Open the bookmark’s original edition when it can be opened
(downloaded, or online), falling back to the bookmarks edition
otherwise.

[`PSEBookmarkOpenMode.alwaysBookmarksEdition`](/documentation/PSReader/PSEBookmarkOpenMode/alwaysBookmarksEdition)

Always open the synthesized bookmarks edition, regardless of the
source edition’s availability.

