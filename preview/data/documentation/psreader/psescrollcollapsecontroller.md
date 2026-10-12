<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEScrollCollapseController",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEScrollCollapseController"
  },
  "title" : "PSEScrollCollapseController"
}
-->

# PSEScrollCollapseController

Drives collapse-on-scroll chrome (navigation bars, toolbars) from one or
more scroll views.

```
@MainActor final class PSEScrollCollapseController
```

## Overview

Register animation blocks with [`addAnimation(id:_:)`](/documentation/PSReader/PSEScrollCollapseController/addAnimation(id:_:)) — each receives
the target [`PSEScrollCollapseController.State`](/documentation/PSReader/PSEScrollCollapseController/State-swift.enum) and moves your chrome accordingly — then let the
controller observe scrolling. Assign it to
[`scrollCollapseController`](/documentation/PSReader/PSEditionReaderViewController/scrollCollapseController) and the reader
attaches every page’s scroll view for you; attach additional scroll views
with [`attach(delegateOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(delegateOf:)) or [`attach(panGestureOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(panGestureOf:)). Downward
scrolling collapses, upward scrolling reveals, and drags scrub the
transition interactively.

For a reader screen whose bars collapse as the user scrolls, see
[Hosting the Reader](/documentation/PSReader/Hosting-the-Reader).

## Topics

### Animating Your Chrome

[`addAnimation(id:_:)`](/documentation/PSReader/PSEScrollCollapseController/addAnimation(id:_:))

Registers a chrome animation. The block runs inside the collapse
animator with the target state — set your chrome’s collapsed or
expanded appearance in it. `id` is held weakly and groups animations
for removal; animations whose id deallocates are dropped.

[`removeAnimations(withID:)`](/documentation/PSReader/PSEScrollCollapseController/removeAnimations(withID:))

Removes the animations registered under `id`.

[`removeAllAnimations()`](/documentation/PSReader/PSEScrollCollapseController/removeAllAnimations())

Removes every registered animation.

[`onCollapseProgress`](/documentation/PSReader/PSEScrollCollapseController/onCollapseProgress)

Reports collapse progress (0 = expanded … 1 = collapsed) per frame in every
mode: interactive scrubs track the finger, and non-interactive settles (release,
programmatic show/hide) are driven by a display link that scrubs the same
animator — so this fires from the same write that moves the chrome, keeping
consumers in sync by construction. Only invoked when the value actually changes,
so steady-state scrolling (fully expanded or fully collapsed) publishes nothing.

### Showing and Hiding

[`state`](/documentation/PSReader/PSEScrollCollapseController/state-swift.property)

The chrome’s current (or animating-toward) state.

[`PSEScrollCollapseController.State`](/documentation/PSReader/PSEScrollCollapseController/State-swift.enum)

Whether the tracked chrome is shown or hidden.

[`show(animationDuration:)`](/documentation/PSReader/PSEScrollCollapseController/show(animationDuration:))

Expands the chrome programmatically.

[`hide(animationDuration:)`](/documentation/PSReader/PSEScrollCollapseController/hide(animationDuration:))

Collapses the chrome programmatically.

[`showIfNeeded(animationDuration:)`](/documentation/PSReader/PSEScrollCollapseController/showIfNeeded(animationDuration:))

Expands the chrome if it is currently collapsed.

[`hideIfNeeded(animationDuration:)`](/documentation/PSReader/PSEScrollCollapseController/hideIfNeeded(animationDuration:))

Collapses the chrome if it is currently expanded.

### Tracking Scroll Views

[`attach(delegateOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(delegateOf:))

Tracks a scroll view by becoming its `delegate`. Use when nothing
else needs the delegate; otherwise use [`attach(panGestureOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(panGestureOf:)).

[`attach(panGestureOf:)`](/documentation/PSReader/PSEScrollCollapseController/attach(panGestureOf:))

Tracks a scroll view through its pan gesture and offset observation,
leaving `delegate` free for your own use.

[`detach(scrollView:)`](/documentation/PSReader/PSEScrollCollapseController/detach(scrollView:))

Stops tracking a scroll view attached with either `attach` method.

[`collapseEngagementDistance`](/documentation/PSReader/PSEScrollCollapseController/collapseEngagementDistance)

Points of downward scroll to ignore before a collapse begins.
Zero (the default) starts collapsing immediately.

