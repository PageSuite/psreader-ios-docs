<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/CopyLinkActivity",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)CopyLinkActivity"
  },
  "title" : "CopyLinkActivity"
}
-->

# CopyLinkActivity

A share sheet activity that copies a shared URL to the pasteboard.

```
class CopyLinkActivity
```

## Overview

The built-in share providers add this activity to every [`ShareContext`](/documentation/PSReader/ShareContext)
they create. Add it to [`applicationActivities`](/documentation/PSReader/ShareContext/applicationActivities) in your own
share contexts to offer the same **Copy Link** action. The activity
appears in the share sheet’s action row when the activity items include a
`URL`, and copies the first URL’s absolute string to the general
pasteboard.

## Topics

### Activity Details

[`activityTitle`](/documentation/PSReader/CopyLinkActivity/activityTitle)

The title the share sheet shows for the activity, “Copy Link”.

[`activityType`](/documentation/PSReader/CopyLinkActivity/activityType)

The activity’s type, with the raw value `copyLink`.

