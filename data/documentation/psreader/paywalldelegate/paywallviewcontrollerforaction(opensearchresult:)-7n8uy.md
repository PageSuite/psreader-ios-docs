<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallDelegate/paywallViewControllerForAction(openSearchResult:)-7n8uy",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader15PaywallDelegatePAAE30paywallViewControllerForAction16openSearchResultAA0beF0_pSgAA0jK0V_tF"
  },
  "title" : "paywallViewControllerForAction(openSearchResult:)"
}
-->

# paywallViewControllerForAction(openSearchResult:)

Returns `nil`, so search results open without a paywall.

```
@MainActor func paywallViewControllerForAction(openSearchResult result: SearchResult) -> PaywallViewController?
```

## Parameters

`result`

The search result the user tapped.

## Return Value

`nil`.

## Discussion

Results from legacy replica editions don’t use this method: the
reader that opens them asks
`PaywallDelegate/paywallViewControllerForAction(openReplicaEdition:)`
instead.