<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEScrollCollapseController/addAnimation(id:_:)",
  "metadataVersion" : "0.1.0",
  "role" : "Instance Method",
  "symbol" : {
    "kind" : "Instance Method",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "s:8PSReader27PSEScrollCollapseControllerC12addAnimation2id_yyXl_yAC5StateOctF"
  },
  "title" : "addAnimation(id:_:)"
}
-->

# addAnimation(id:_:)

Registers a chrome animation. The block runs inside the collapse
animator with the target state — set your chrome’s collapsed or
expanded appearance in it. `id` is held weakly and groups animations
for removal; animations whose id deallocates are dropped.

```
@MainActor func addAnimation(id: AnyObject, _ block: @escaping (State) -> Void)
```