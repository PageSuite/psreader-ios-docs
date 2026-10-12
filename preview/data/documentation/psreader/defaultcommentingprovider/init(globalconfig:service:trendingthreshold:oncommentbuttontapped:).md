<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/DefaultCommentingProvider/init(globalConfig:service:trendingThreshold:onCommentButtonTapped:)",
  "metadataVersion" : "0.1.0",
  "role" : "Initializer",
  "symbol" : {
    "kind" : "Initializer",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader25DefaultCommentingProviderC12globalConfig7service17trendingThreshold21onCommentButtonTappedAcA19GlobalConfigurationV_AA0C7Service_pSiyAA10PSEArticleC_AA7PSEPageCAA16PSEEditionSource_pSo16UIViewControllerCtcSgtcfc"
  },
  "title" : "init(globalConfig:service:trendingThreshold:onCommentButtonTapped:)"
}
-->

# init(globalConfig:service:trendingThreshold:onCommentButtonTapped:)

Creates a new commenting provider using global SDK settings.

```
convenience init(globalConfig: GlobalConfiguration, service: any CommentingService, trendingThreshold: Int = 100, onCommentButtonTapped: ((PSEArticle, PSEPage, PSEEditionSource, UIViewController) -> Void)? = nil)
```

## Parameters

`globalConfig`

The global configuration to derive styling from.

`service`

The data service (e.g. [`CoralCommentingService`](/documentation/PSReader/CoralCommentingService)).

`trendingThreshold`

Comment count threshold for the trending icon.
Defaults to `100`.

`onCommentButtonTapped`

Called when a comment button is tapped.

## Discussion

Pulls [`brandColor`](/documentation/PSReader/GlobalConfiguration/brandColor) and
[`secondaryFont`](/documentation/PSReader/GlobalConfiguration/secondaryFont) from the provided configuration.