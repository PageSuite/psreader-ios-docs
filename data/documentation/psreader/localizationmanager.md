<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/LocalizationManager",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader19LocalizationManagerC"
  },
  "title" : "LocalizationManager"
}
-->

# LocalizationManager

Provides localized strings.

```
class LocalizationManager
```

## Overview

This class is designed to be used as a singleton. The static shared object
is used throughout the SDK to localize content.

`LocalizationManager` uses `NSLocalizedString` to map default values to
localized strings. See [`LocalizedStringKey`](/documentation/PSReader/LocalizedStringKey) for each key’s default value.
This means you can use a string catalog or a strings file to provide
localized strings.

You may also replace the shared object with a `LocalizationManager` subclass
to override the default behavior.

To translate or reword the prebuilt UI’s strings, see
[Localization](/documentation/PSReader/Localization).

## Topics

### Supplying Strings

[`shared`](/documentation/PSReader/LocalizationManager/shared)

Shared singleton object.
Replace this value at runtime to use your own localization manager.

[`localizedString(for:)`](/documentation/PSReader/LocalizationManager/localizedString(for:))

Returns a localized version of the string identified by the given key.

[`init()`](/documentation/PSReader/LocalizationManager/init())

Public initializer for subclassing.

