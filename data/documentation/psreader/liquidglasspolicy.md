<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LiquidGlassPolicy",
  "metadataVersion" : "0.1.0",
  "role" : "Enumeration",
  "symbol" : {
    "kind" : "Enumeration",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader17LiquidGlassPolicyO"
  },
  "title" : "LiquidGlassPolicy"
}
-->

# LiquidGlassPolicy

A policy describing how the SDK adopts the iOS Liquid Glass UI effect.

```
enum LiquidGlassPolicy
```

## Overview

Use this type to control whether the SDK applies the Liquid Glass appearance
on devices running iOS 26 or later. This policy acts as a global preference,
and may be overridden by more granular configuration objects.

The Liquid Glass effect is only available at runtime on iOS 26+ devices,
and will not be applied if the host application opts into design compatibility
using the `"UIDesignRequiresCompatibility"` Info.plist key.

The default policy is `.automatic`, which enables Liquid Glass when supported.
Set this to `.disabled` to prevent use of the effect even on capable systems.

For the prebuilt UI’s other appearance settings, see [Theming](/documentation/PSReader/Theming).

> SeeAlso: ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration/liquidGlassPolicy``

## Topics

### Policies

[`LiquidGlassPolicy.automatic`](/documentation/PSReader/LiquidGlassPolicy/automatic)

Use the Liquid Glass effect on iOS 26+ when supported by both the system
and the host application’s design compatibility settings.

[`LiquidGlassPolicy.disabled`](/documentation/PSReader/LiquidGlassPolicy/disabled)

Prevent use of the Liquid Glass effect in all cases, even when the
system supports it. Intended for applications that require a
consistent UI appearance across all OS versions.

