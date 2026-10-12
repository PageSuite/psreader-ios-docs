<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/ButtonConfiguration/dismissButton(size:insets:position:tintColor:image:)",
  "metadataVersion" : "0.1.0",
  "role" : "Type Method",
  "symbol" : {
    "kind" : "Type Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19ButtonConfigurationV07dismissB04size6insets8position9tintColor5imageACSo6CGSizeV_So12UIEdgeInsetsVAC8PositionOSo7UIColorCSgSo7UIImageCSgtFZ"
  },
  "title" : "dismissButton(size:insets:position:tintColor:image:)"
}
-->

# dismissButton(size:insets:position:tintColor:image:)

Creates a preconfigured dismiss button suitable for use with [`DismissHeaderViewController`](/documentation/PSReader/DismissHeaderViewController).

```
static func dismissButton(size: CGSize = CGSize(width: 16, height: 16), insets: UIEdgeInsets = .zero, position: Position = .leading(), tintColor: UIColor? = nil, image: UIImage? = nil) -> ButtonConfiguration
```

## Parameters

`size`

The size of the dismiss button (default is 16x16 points).

`insets`

Edge insets applied around the button.

`position`

Positioning details for the dismiss button (default is `.leading`).

`tintColor`

Optional tint color applied to the button’s icon.

`image`

Optional custom image used for the dismiss button.
If omitted, the default icon provided by the SDK is used.

## Return Value

A fully configured `ButtonConfiguration` instance for a dismiss button.

## Discussion

This convenience initializer provides a sensible default appearance and positioning
for dismiss buttons, but all parameters can be overridden as needed.