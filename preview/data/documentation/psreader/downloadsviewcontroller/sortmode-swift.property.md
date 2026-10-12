<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DownloadsViewController/sortMode-swift.property",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23DownloadsViewControllerC8sortModeAC04SortF0Ovp"
  },
  "title" : "sortMode"
}
-->

# sortMode

The current sort mode for displaying downloaded editions.

```
@MainActor var sortMode: SortMode { get set }
```

## Discussion

In the carousel, users change this from the subsection ribbon’s menu;
on its own, the screen has no menu.
Both programmatic changes and user selections are persisted to UserDefaults
and restored automatically on subsequent launches.