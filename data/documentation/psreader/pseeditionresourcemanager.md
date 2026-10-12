<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEEditionResourceManager",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25PSEEditionResourceManagerP"
  },
  "title" : "PSEEditionResourceManager"
}
-->

# PSEEditionResourceManager

Resolves an edition’s resource references (page PDFs, images, templates)
to concrete locations or data.

```
protocol PSEEditionResourceManager
```

## Overview

Every [`PSEEditionSource`](/documentation/PSReader/PSEEditionSource) supplies a resource manager; the reader routes
all page-asset lookups through it. The default implementation resolves
against the edition’s local cache directory and falls back to plain HTTP
for absolute URLs — provide your own only when assets live somewhere the
default cannot reach.

## Topics

### Resolving Resources

[`resolveURL(resource:)`](/documentation/PSReader/PSEEditionResourceManager/resolveURL(resource:))

Returns a `URL` (local file or remote) for the resource, or `nil` if
it cannot be resolved.

[`resolve(resource:)`](/documentation/PSReader/PSEEditionResourceManager/resolve(resource:))

Returns a resolved path or URL string for the resource, or `nil` if
the resource is not available through this manager.

### Fetching Resources

[`cachedData(for:)`](/documentation/PSReader/PSEEditionResourceManager/cachedData(for:))

Returns locally cached bytes for the resource, or `nil` when nothing
is cached.

[`dataTask(for:completion:)`](/documentation/PSReader/PSEEditionResourceManager/dataTask(for:completion:))

Starts an asynchronous fetch for the resource. Return `nil` when the
resource cannot be fetched (the reader then treats it as missing).

