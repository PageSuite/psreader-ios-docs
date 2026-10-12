<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/init(service:accentColor:fontFamily:trendingThreshold:onCommentButtonTapped:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC7service11accentColor10fontFamily17trendingThreshold21onCommentButtonTappedAcA0C7Service_p_So7UIColorCSo6UIFontCSiyAA10PSEArticleC_AA7PSEPageCAA16PSEEditionSource_pSo16UIViewControllerCtcSgtcfc"
  },
  "title" : "init(service:accentColor:fontFamily:trendingThreshold:onCommentButtonTapped:)"
}
-->

# init(service:accentColor:fontFamily:trendingThreshold:onCommentButtonTapped:)

Creates a new commenting provider with explicit styling.

```
init(service: any CommentingService, accentColor: UIColor, fontFamily: UIFont, trendingThreshold: Int = 100, onCommentButtonTapped: ((PSEArticle, PSEPage, PSEEditionSource, UIViewController) -> Void)? = nil)
```

## Parameters

`service`

The data service (e.g. [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService)).

`accentColor`

The accent color for interactive elements.

`fontFamily`

The base font family. The SDK adapts weight and size.

`trendingThreshold`

Comment count threshold for the trending icon.
Defaults to `100`.

`onCommentButtonTapped`

Called when a comment button is tapped.