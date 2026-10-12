<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DownloadsViewController/additionalSafeAreaInsets",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)DownloadsViewController(py)additionalSafeAreaInsets"
  },
  "title" : "additionalSafeAreaInsets"
}
-->

# additionalSafeAreaInsets

Extra insets the downloads grid keeps clear, on top of the safe area.

```
@MainActor override var additionalSafeAreaInsets: UIEdgeInsets { get set }
```

## Discussion

Set this when you embed the screen in a container that covers part of
it, such as your own tab bar. Setting it re-lays out the grid. This
also makes the insets work when the controller is hosted in a SwiftUI
paging `TabView`, where UIKit alone doesn’t apply them.