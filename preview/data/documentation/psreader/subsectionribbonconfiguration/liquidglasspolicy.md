<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SubsectionRibbonConfiguration/liquidGlassPolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29SubsectionRibbonConfigurationV17liquidGlassPolicyAA06LiquidfG0Ovp"
  },
  "title" : "liquidGlassPolicy"
}
-->

# liquidGlassPolicy

Liquid Glass policy for the subsection ribbon.

```
var liquidGlassPolicy: LiquidGlassPolicy
```

## Discussion

Controls adoption of the iOS 26+ Liquid Glass effect for the ribbon UI.
In the Liquid Glass appearance the subsection ribbon floats above the archive
view content, allowing the content to scroll under it. Defaults to the value
from `GlobalConfiguration` and can be overridden here for finer control.