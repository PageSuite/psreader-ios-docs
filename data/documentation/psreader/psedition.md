<!--
{
  "availability" : [

  ],
  "documentType" : "symbol",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/PSEdition",
  "metadataVersion" : "0.1.0",
  "role" : "Class",
  "symbol" : {
    "kind" : "Class",
    "modules" : [
      "PSReader"
    ],
    "preciseIdentifier" : "c:@M@PSReader@objc(cs)PSEdition"
  },
  "title" : "PSEdition"
}
-->

# PSEdition

An edition on PageSuite’s legacy replica system.

```
@objc class PSEdition
```

## Overview

Only the prebuilt UI shows legacy replica editions, so you meet this
type in its replica callbacks: [`PaywallDelegate`](/documentation/PSReader/PaywallDelegate) passes the edition
the user is opening or downloading, [`AdvertDelegate`](/documentation/PSReader/AdvertDelegate) the edition its
banners appear in, [`EditionDateFormatter`](/documentation/PSReader/EditionDateFormatter) the edition to label in
archives and on the downloads screen, and the `replica…` events on
[`EventChannel`](/documentation/PSReader/EventChannel) the edition they concern. Read its identity, name and
publish date.

Editions on PageSuite’s current system are [`PSEPublished`](/documentation/PSReader/PSEPublished) values
instead. See [Edition Platforms](/documentation/PSReader/Edition-Platforms).

## Topics

### Identifying the Edition

[`id`](/documentation/PSReader/PSEdition/id)

The edition’s GUID.

[`publicationGUID`](/documentation/PSReader/PSEdition/publicationGUID)

The GUID of the publication the edition belongs to.

[`publicationName`](/documentation/PSReader/PSEdition/publicationName)

The name of the publication the edition belongs to.

### Describing the Edition

[`name`](/documentation/PSReader/PSEdition/name)

The name of the edition.

[`publishDate`](/documentation/PSReader/PSEdition/publishDate)

The date the edition was published.

