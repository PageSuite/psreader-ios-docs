<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ReaderNavigationBarConfiguration/liquidGlassPolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader32ReaderNavigationBarConfigurationV17liquidGlassPolicyAA06LiquidgH0Ovp"
  },
  "title" : "liquidGlassPolicy"
}
-->

# liquidGlassPolicy

Liquid Glass policy for the reader navigation bar.

```
var liquidGlassPolicy: LiquidGlassPolicy
```

## Discussion

Controls adoption of the iOS 26+ Liquid Glass effect for navigation bar.
The Liquid Glass navigation bar allows content to fill the entire view,
with the bar floating above. Defaults to the value from `GlobalConfiguration`
and can be overridden here for finer control.