<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuContext/dismissReader(animated:completion:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19SettingsMenuContextC13dismissReader8animated10completionySb_yycSgtF"
  },
  "title" : "dismissReader(animated:completion:)"
}
-->

# dismissReader(animated:completion:)

Closes the settings menu and the reader beneath it, returning to
whatever opened the reader.

```
@MainActor func dismissReader(animated: Bool = true, completion: (() -> Void)? = nil)
```

## Parameters

`animated`

Whether to animate the dismissal. Defaults to `true`.

`completion`

Called after the reader closes.