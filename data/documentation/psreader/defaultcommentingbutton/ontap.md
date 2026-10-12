<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingButton/onTap",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader23DefaultCommentingButtonC5onTapyycSgvp"
  },
  "title" : "onTap"
}
-->

# onTap

Called when the user taps the button.

```
@MainActor var onTap: (() -> Void)?
```

## Discussion

The SDK supplies this closure through
[`commentButton(forArticle:inEdition:onTap:)`](/documentation/PSReader/CommentingDelegate/commentButton(forArticle:inEdition:onTap:));
[`DefaultCommentingProvider`](/documentation/PSReader/DefaultCommentingProvider) assigns it for you.