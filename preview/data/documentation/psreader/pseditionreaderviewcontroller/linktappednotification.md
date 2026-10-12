<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/linkTappedNotification",
  "metadataVersion" : "0.1.0",
  "role" : "Type Property",
  "symbol" : {
    "kind" : "Type Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC22linkTappedNotificationSo18NSNotificationNameavpZ"
  },
  "title" : "linkTappedNotification"
}
-->

# linkTappedNotification

Posted when the user taps a link inside edition content — an article
hyperlink, a link hotspot, or a link out of an advert page.

```
@MainActor static let linkTappedNotification: Notification.Name
```

## Discussion

The reader does not present links itself (it only opens `mailto:`
links directly). Observe this notification and present the URL
however your app prefers — a Safari view controller for web links,
for example. The tapped `URL` arrives in `userInfo` under
[`linkTappedURLKey`](/documentation/PSReader/PSEditionReaderViewController/linkTappedURLKey).