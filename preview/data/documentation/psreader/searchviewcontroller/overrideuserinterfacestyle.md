<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SearchViewController/overrideUserInterfaceStyle",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)SearchViewController(py)overrideUserInterfaceStyle"
  },
  "title" : "overrideUserInterfaceStyle"
}
-->

# overrideUserInterfaceStyle

Forces the search screen into light or dark mode.

```
@MainActor override var overrideUserInterfaceStyle: UIUserInterfaceStyle { get set }
```

## Discussion

The controller passes the value on to the content it embeds, so the
whole screen takes the style. The default, `.unspecified`, follows the
surrounding view hierarchy.