<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/SettingsMenuItem/init(title:image:role:handler:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader16SettingsMenuItemV5title5image4role7handlerACSS_So7UIImageCSgAC4RoleOyAA0bC7ContextCYbScMYcctcfc"
  },
  "title" : "init(title:image:role:handler:)"
}
-->

# init(title:image:role:handler:)

Creates a settings menu item.

```
init(title: String, image: UIImage? = nil, role: Role = .normal, handler: @escaping @MainActor (SettingsMenuContext) -> Void)
```

## Parameters

`title`

The item’s title.

`image`

An icon shown before the title. Defaults to `nil`.

`role`

How the item is styled. Defaults to [`SettingsMenuItem.Role.normal`](/documentation/PSReader/SettingsMenuItem/Role-swift.enum/normal).

`handler`

Called on the main thread when the item is tapped.