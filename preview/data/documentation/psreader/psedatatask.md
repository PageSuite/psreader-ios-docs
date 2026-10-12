<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEDataTask",
  "metadataVersion" : "0.1.0",
  "role" : "Protocol",
  "symbol" : {
    "kind" : "Protocol",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader11PSEDataTaskP"
  },
  "title" : "PSEDataTask"
}
-->

# PSEDataTask

A cancellable in-flight resource fetch, as returned by
[`dataTask(for:completion:)`](/documentation/PSReader/PSEEditionResourceManager/dataTask(for:completion:)).

```
protocol PSEDataTask
```

## Overview

The fetch is already running when you receive it; there’s nothing to
start.

`URLSessionDataTask` conforms, so network-backed resource managers can
return their session tasks directly.

## Topics

### Canceling

[`cancel()`](/documentation/PSReader/PSEDataTask/cancel())

Cancels the fetch. The task’s completion may not be called.

