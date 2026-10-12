<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Using-the-SDK-With-AI-Agents",
  "metadataVersion" : "0.1.0",
  "role" : "article",
  "title" : "Using the SDK With AI Agents"
}
-->

# Using the SDK With AI Agents

Point your coding agent at the SDK’s documentation and give it the rules that matter.

## Overview

Every page of this documentation is also published as Markdown. Give your
agent two start pages: the root, and the hub for the side your app uses,
the prebuilt UI or a custom UI.

```
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader.md
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/prebuilt-ui.md
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/custom-ui.md
```

Then paste the rules below into the file it reads at the start of every
session. It will work from the current API rather than from what it
remembers of older PageSuite SDKs.

## Find the Markdown

The pages sit under `data/documentation/psreader/`, named after their
titles and symbols:

```
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader.md
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/getting-started.md
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/feededitionservice.md
https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/feededitionservice/published(foreditionguid:).md
```

Links inside the Markdown point at the web pages, for example
`/documentation/PSReader/FeedEditionService/published(forEditionGUID:)`,
and some appear as `doc://com.pagesuite.PSReader/documentation/PSReader/…`
references. To fetch the Markdown for either, drop any `#fragment`, take
the path from `/documentation/` onward, lowercase it, add `.md`, and put
it under `data/`:

```
/documentation/PSReader/FeedEditionService/published(forEditionGUID:)
→ data/documentation/psreader/feededitionservice/published(foreditionguid:).md

/documentation/PSReader/Choosing-an-Integration#Mixing-Prebuilt-and-Custom-UI
→ data/documentation/psreader/choosing-an-integration.md
```

A manifest lists every page by identifier and title, so an agent can find
a page by name:

```
https://pagesuite.github.io/psreader-ios-docs/PSReader-markdown-manifest.json
```

Its `documents` array holds one entry per page, with the page’s
`identifier` (the `/documentation/PSReader/…` path), `title`, and
`documentType` (`symbol` or `article`). It doesn’t give file paths; apply
the rule above to an identifier to get one.

**A type’s members.** A type’s Markdown page may not list its members. To
find them, take the manifest identifiers that start with the type’s
identifier followed by a slash: for [`FeedEditionService`](/documentation/PSReader/FeedEditionService), every
identifier that starts with `/documentation/PSReader/FeedEditionService/`.

**Suffixed names.** When two symbols would share a path, DocC adds a
suffix to tell them apart: the kind, as in `scrolldelegate-swift.protocol`
beside `scrolldelegate-swift.property`, or a short hash, as in
`removebookmark(_:)-5vc38`. Overloads get hashes, and so does a protocol
method’s **default implementation**, the version a protocol extension
supplies when you don’t implement the method yourself:
`paywallviewcontrollerforaction(downloadfeededition:)` is the requirement,
and `…(downloadfeededition:)-740ka` its default implementation, both
titled the same in the manifest. One very long name, an initializer of
[`GlobalConfiguration`](/documentation/PSReader/GlobalConfiguration), is also cut short and ends in `-vp9z`.

Links carry these suffixes, so the rule works on them. A path you build
from a symbol’s name can miss, though; look the name up in the manifest,
which lists the suffixed identifiers. The long initializer is the
exception both ways: its links and its manifest identifier give the full
name. For it, or whenever a page is missing, fetch the type’s page as
JSON, with `.json` in place of `.md`: its `references` give each member’s
`url`, suffix included, and the rule applies to that.

## Know How the Docs Are Organized

The docs have a shared trunk and one hub per side:

- **The root** holds what both sides need: getting started, choosing a
  side, identifiers, edition platforms, the edition model, and the
  release notes. Each hub lists its common tasks, such as opening an
  edition from a link, with links to the guide sections that cover them.
- **The Prebuilt UI hub** covers setting up and customizing the SDK’s
  screens. Its feature pages are named for the feature: Sharing,
  Bookmarks, Search, Paywalls.
- **The Custom UI hub** covers building your own screens on the core SDK.
  Its feature pages are named for what you build: “Adding a Share
  Button”, “Building a Search Screen”, “Gating Editions Behind a
  Paywall”, “Handling Advert Pages”, “Reporting Analytics”.

Each feature has one page per side, and the two don’t mix: a prebuilt
page configures a screen the SDK draws, and a custom page builds the same
feature into your own. Custom UI code builds on one host class,
`ReaderScreenViewController`, defined in [Hosting the Reader](/documentation/PSReader/Hosting-the-Reader); every
custom feature page adds to that class rather than defining its own.

## Add the SDK Rules to Your Agent’s Instructions

Most coding agents read a Markdown file of project instructions at the
start of every session, such as `AGENTS.md` or `CLAUDE.md` at the root of
your repository. Paste this section into yours, and pick the side your
app uses in the first rule:

```markdown
## PageSuite PSReader SDK

This app shows digital newspaper and magazine editions with PageSuite's
PSReader SDK.

- This app uses <the prebuilt UI | a custom UI>. Stay on that side unless
  asked to change.
- Before writing SDK code, read the docs. Start at
  https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader.md
  and at this app's hub:
  - prebuilt UI: https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/prebuilt-ui.md
  - custom UI: https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/custom-ui.md
- Every page is Markdown. For a link to `/documentation/PSReader/<Path>`
  (or `doc://…/documentation/PSReader/<Path>`), drop any `#fragment`, then
  fetch `https://pagesuite.github.io/psreader-ios-docs/data/documentation/psreader/<path>.md`
  with the path lowercased. If a page is missing, DocC suffixed its name
  (`-swift.protocol`, a hash such as `-5vc38`, or `-vp9z` on a long name
  it cut short). Kind and hash suffixes appear in the manifest's
  identifiers; a name cut short doesn't, so fetch the type's page with
  `.json` in place of `.md` and use the member's `url` from
  `references`. A protocol method can have two pages with the
  same title: the requirement and, with a hash, its default
  implementation.
- https://pagesuite.github.io/psreader-ios-docs/PSReader-markdown-manifest.json
  lists every page's identifier and title. To list a type's members, take
  the identifiers that start with the type's identifier followed by `/`.
- Check every type and signature in the docs; older PageSuite SDKs had
  different APIs.
- Feature pages come in pairs; read the one for this app's side. Prebuilt
  UI pages are named for the feature (Sharing, Bookmarks, Paywalls).
  Custom UI pages are named for what you build (Adding a Share Button,
  Building a Search Screen, Gating Editions Behind a Paywall, Handling
  Advert Pages, Reporting Analytics). Each hub lists common tasks, such
  as opening an edition from a link, with links to the sections that
  cover them.
- The SDK is one module: `import PSReader`. Never `import PSReaderUI`.
- Call `PSReader.initialize(apiKey:)` once at app launch, on both sides,
  and don't wait for it: the SDK waits for it where it needs to.
- Prebuilt UI: `CarouselViewController`, or single screens such as
  `ArchiveViewController` and `FeedReaderViewController`, all configured
  through one `GlobalConfiguration`. For lists of your own, fetch
  editions with `FeedEditionService` and open the one the user taps in
  `FeedReaderViewController`.
- The app configuration (`GlobalConfiguration.remoteConfig`, or the
  reader's `open(edition:openingPage:application:)`) is rarely needed: a
  dynamic archive loads it itself. Otherwise, when you have a shortcode,
  load it with `AppConfigService` and
  set it if your editions might use what reads it: in-article adverts,
  article widgets, advert pages from a third-party ad loader, and, in the
  prebuilt reader, the masthead logo in templated pages. When in doubt,
  set it. A custom UI's reader takes that logo from its media delegate's
  `editionLogoURL(for:)` instead (none by default).
- Custom UI: `FeedEditionService`, `PSEPublished.openEditionSource()`, and
  `PSEditionReaderViewController`. Build on the `ReaderScreenViewController`
  class from the Hosting the Reader page, and add each feature to it as
  its page shows; don't define a second host or conform to the reader's
  delegates again. Never present or push `PSEditionReaderViewController`
  on its own.
- Every edition on PageSuite's current system, classic PDF included,
  works with both sides. API names that say "feed" (`FeedEditionService`,
  `FeedReaderViewController`, `.feedArchive`) mean that system, not a
  format. "Replica" means PageSuite's legacy system, which only the
  prebuilt UI shows; use `.replicaArchive` only with a replica
  publication GUID. The exceptions, `isReplicaEdition()` and
  `feedEditionReplicaView`, mean the classic PDF look.
- The publication GUID is spelled `applicationGUID` on `PSEPublished`
  (empty on an edition from `published(forEditionGUID:)`) and
  `applicationId` on `SearchResult`. Model property names are frozen,
  casing included (`pageguid`, `articleguid`); don't rename or wrap them.
- Read API keys and GUIDs from configuration, never from source code. In
  code and examples, use placeholders such as "API_KEY", "ACCOUNT_GUID"
  and "PUBLICATION_GUID", and ask for real values.
- Prefer the `async` APIs.
```

## Ask for One Step at a Time

Agents do best with a task that matches one guide. For example:

- Prebuilt UI: “Add a carousel for shortcode SHORTCODE as the app’s root
  screen, following Setting Up the Carousel.”
- Prebuilt UI: “Add a Help row to the reader’s settings menu, following
  Add a Row to the Reader Settings.”
- Both, mixed: “List the latest editions of publication PUBLICATION_GUID
  with FeedEditionService, and open the one I tap in
  FeedReaderViewController.”
- Custom UI: “Add the ReaderScreenViewController from Hosting the Reader,
  and open it from my archive list.”
- Custom UI: “Add a share button to ReaderScreenViewController, following
  Adding a Share Button.”

Naming the guide steers the agent to the right page. The common tasks
each hub lists, such as opening an edition from a link, make good single
tasks.

## Check the Agent’s Work

Build and run the result with a real edition, then review the code for
the mistakes agents tend to make with this SDK:

- **Invented API.** A method that doesn’t exist, or one from an older SDK
  (`PSReaderViewController`, `import PSReaderUI`). The build catches most
  of these; search the docs for the rest.
- **The wrong side’s page.** Prebuilt configuration, such as a
  ``doc://com.pagesuite.PSReader/documentation/PSReader/GlobalConfiguration`` delegate, in a custom UI, where nothing reads
  it; or a custom page’s code rebuilt around a prebuilt screen.
- **A second reader host.** In a custom UI, a new view controller that
  hosts the reader, or a second conformance to the reader’s delegates,
  instead of an addition to `ReaderScreenViewController`.
- **A bare reader.** `PSEditionReaderViewController` presented or pushed
  directly, instead of hosted inside a screen of yours.
- **Missing initialization.** No `PSReader.initialize(apiKey:)` call at
  launch, or a request at launch that doesn’t await it first.
- **Replica confusion.** A classic PDF title treated as “replica”, for
  example a publication GUID in a `.replicaArchive` section, or a custom
  UI avoided because the edition is a PDF. See
  <doc://com.pagesuite.PSReader/documentation/PSReader/Edition-Platforms#Historic-API-Names>.
- **Committed secrets.** A real API key or GUID in source code or in a
  prompt you’ll share.
- **Swallowed errors.** `try?` or an empty `catch` where your app should
  show an error state.