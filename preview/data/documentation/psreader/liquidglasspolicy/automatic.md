<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LiquidGlassPolicy/automatic",
  "metadataVersion" : "0.1.0",
  "role" : "Case",
  "symbol" : {
    "kind" : "Case",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17LiquidGlassPolicyO9automaticyA2CmF"
  },
  "title" : "LiquidGlassPolicy.automatic"
}
-->

# LiquidGlassPolicy.automatic

Use the Liquid Glass effect on iOS 26+ when supported by both the system
and the host application’s design compatibility settings.

```
case automatic
```

## Discussion

On unsupported OS versions or when compatibility mode is required,
this policy gracefully falls back to a standard appearance.