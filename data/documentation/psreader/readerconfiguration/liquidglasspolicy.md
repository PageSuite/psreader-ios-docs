<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderConfiguration/liquidGlassPolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ReaderConfigurationV17liquidGlassPolicyAA06LiquideF0Ovp"
  },
  "title" : "liquidGlassPolicy"
}
-->

# liquidGlassPolicy

Liquid Glass policy applied to the reader interface.

```
var liquidGlassPolicy: LiquidGlassPolicy
```

## Discussion

Controls adoption of the iOS 26+ Liquid Glass effect within reader views
that do not have their own configuration points. For example, alerts.
Defaults to the value from `GlobalConfiguration` and can be overridden
here for finer control.