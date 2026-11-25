<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/canRenderAdvertPage(_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader29PSEditionReaderViewControllerC14AdvertDelegateP09canRenderF4PageySbAA7PSEPageCF"
  },
  "title" : "canRenderAdvertPage(_:)"
}
-->

# canRenderAdvertPage(_:)

Whether [`advertViewController(forPage:)`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/advertViewController(forPage:)) serves a third-party
advert page that has no built-in rendering: a Google Ad Manager
page, or a [`PSEAdvertProvider.custom(_:)`](/documentation/PSReader/PSEAdvertProvider/custom(_:)) one such as Freestar
or a provider only your app knows.

```
func canRenderAdvertPage(_ page: PSEPage) -> Bool
```

## Discussion

The reader asks once per such page when the edition opens, and
leaves out every page that neither the built-in rendering nor
your delegate can render, so the user pages past it instead of
seeing a blank page. Pages the built-in rendering covers aren’t
asked about, and without a delegate such pages are always left
out.

The default implementation asks [`advertViewController(forPage:)`](/documentation/PSReader/PSEditionReaderViewController/AdvertDelegate-swift.protocol/advertViewController(forPage:))
and returns whether it supplied a view controller, which is
discarded without being shown; that view controller must not
request an ad before
[`advertPageInView()`](/documentation/PSReader/PSEAdvertContentViewController/advertPageInView()), as the
contract already requires. Implement this method to answer
without building one.