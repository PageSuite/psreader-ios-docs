<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuContext/present(_:animated:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SettingsMenuContextC7present_8animated10completionySo16UIViewControllerC_SbyycSgtF"
  },
  "title" : "present(_:animated:completion:)"
}
-->

# present(_:animated:completion:)

Presents a view controller, such as a confirmation alert, over the
settings menu.

```
@MainActor func present(_ viewController: UIViewController, animated: Bool = true, completion: (() -> Void)? = nil)
```

## Parameters

`viewController`

The view controller to present.

`animated`

Whether to animate the presentation. Defaults to `true`.

`completion`

Called after the presentation finishes.

## Discussion

Popovers and action sheets point at the tapped item.