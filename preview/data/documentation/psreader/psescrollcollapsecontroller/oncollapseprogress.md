<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEScrollCollapseController/onCollapseProgress",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27PSEScrollCollapseControllerC02onC8Progressy14CoreFoundation7CGFloatVcSgvp"
  },
  "title" : "onCollapseProgress"
}
-->

# onCollapseProgress

Reports collapse progress (0 = expanded … 1 = collapsed) per frame in every
mode: interactive scrubs track the finger, and non-interactive settles (release,
programmatic show/hide) are driven by a display link that scrubs the same
animator — so this fires from the same write that moves the chrome, keeping
consumers in sync by construction. Only invoked when the value actually changes,
so steady-state scrolling (fully expanded or fully collapsed) publishes nothing.

```
@MainActor var onCollapseProgress: ((CGFloat) -> Void)?
```