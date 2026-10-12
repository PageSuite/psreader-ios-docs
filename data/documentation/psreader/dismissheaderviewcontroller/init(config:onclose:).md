<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DismissHeaderViewController/init(config:onClose:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27DismissHeaderViewControllerC6config7onCloseAcA19ButtonConfigurationV_yycSgtcfc"
  },
  "title" : "init(config:onClose:)"
}
-->

# init(config:onClose:)

Creates a dismiss header.

```
@MainActor init(config: ButtonConfiguration = .dismissButton(), onClose: (() -> Void)? = nil)
```

## Parameters

`config`

Appearance and positioning of the close button. Defaults to
[`dismissButton(size:insets:position:tintColor:image:)`](/documentation/PSReader/ButtonConfiguration/dismissButton(size:insets:position:tintColor:image:)).

`onClose`

Optional handler invoked when the button is tapped. When
`nil`, the header calls `dismiss(animated:)` on itself.