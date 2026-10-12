<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/AudioOverlayConfiguration/liquidGlassPolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25AudioOverlayConfigurationV17liquidGlassPolicyAA06LiquidfG0Ovp"
  },
  "title" : "liquidGlassPolicy"
}
-->

# liquidGlassPolicy

Liquid Glass policy for the audio overlay.

```
var liquidGlassPolicy: LiquidGlassPolicy
```

## Discussion

Controls adoption of the iOS 26+ Liquid Glass effect within audio overlay
surfaces. Defaults to the value from `GlobalConfiguration` and can be
overridden here for finer control.