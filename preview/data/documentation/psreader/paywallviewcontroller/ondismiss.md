<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PaywallViewController/onDismiss",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Property",
  "symbol" : {
    "kind" : "Instance Property",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader21PaywallViewControllerP9onDismissySbcSgvp"
  },
  "title" : "onDismiss"
}
-->

# onDismiss

A continuation callback invoked upon completion of the paywall
interaction, signalling whether the SDK should grant access to the
requested content.

```
@MainActor var onDismiss: ((Bool) -> Void)? { get set }
```

## Discussion

The SDK sets this property before presenting your view controller and
then waits on it — the originating action (opening or downloading an
edition, tapping a search result) only resumes once you invoke the
closure. Pass `true` if the user obtained access (e.g., subscription
confirmed), or `false` if access was denied or the user canceled.
Invoke it exactly once per presentation.

This callback is independent of presentation: invoking it does **not**
dismiss the view controller, and dismissing the view controller does
not invoke it. Your view controller is responsible for calling
`dismiss(animated:)`.