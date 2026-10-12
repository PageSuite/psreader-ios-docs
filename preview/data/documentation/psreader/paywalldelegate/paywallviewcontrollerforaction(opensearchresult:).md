<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegateP30paywallViewControllerForAction16openSearchResultAA0beF0_pSgAA0jK0V_tF"
  },
  "title" : "paywallViewControllerForAction(openSearchResult:)"
}
-->

# paywallViewControllerForAction(openSearchResult:)

Provides a paywall view controller displayed when attempting to open
an edition from a search result.

```
@MainActor func paywallViewControllerForAction(openSearchResult result: SearchResult) -> PaywallViewController?
```

## Parameters

`result`

The search result the user tapped.

## Return Value

A configured `PaywallViewController`, or `nil` if no paywall is needed.

## Discussion

By default, this method returns `nil` (no paywall). Override to restrict access
to search result content. The [`SearchResult`](/documentation/PSReader/SearchResult) provides edition and publication
identifiers that can be used to determine whether access should be gated.