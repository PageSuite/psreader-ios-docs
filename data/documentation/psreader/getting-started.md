<!--
{
  "documentType" : "article",
  "framework" : "PSReader",
  "identifier" : "/documentation/PSReader/Getting-Started",
  "metadataVersion" : "0.1.0",
  "role" : "collectionGroup",
  "title" : "Getting Started"
}
-->

# Getting Started

Install the SDK, initialize it, and continue with the prebuilt UI or a custom UI.

## Overview

Add the PSReader package to your app, then initialize the SDK with your
API key in your app delegate, at launch:

```swift
import PSReader
import UIKit

@main
final class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(
        _ application: UIApplication,
        didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
    ) -> Bool {
        PSReader.initialize(apiKey: "API_KEY")
        return true
    }
}
```

The snippets in these docs put your first screen in the window your
scene delegate creates. Xcode’s App template gives you a scene delegate
and names it in Info.plist’s Application Scene Manifest; this is the
minimal version:

```swift
import UIKit

final class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(
        _ scene: UIScene,
        willConnectTo session: UISceneSession,
        options connectionOptions: UIScene.ConnectionOptions
    ) {
        guard let windowScene = scene as? UIWindowScene else { return }

        let window = UIWindow(windowScene: windowScene)
        window.rootViewController = UIViewController()   // Your first screen; see below.
        window.makeKeyAndVisible()
        self.window = window
    }
}
```

Everything the SDK offers, from the prebuilt carousel to the core SDK’s
page renderer, is in the one `PSReader` module. Once it’s initialized,
continue with [Prebuilt UI](/documentation/PSReader/Prebuilt-UI) or [Custom UI](/documentation/PSReader/Custom-UI);
[Choose Prebuilt or Custom UI](/documentation/PSReader/Getting-Started#Choose-Prebuilt-or-Custom-UI) shows where each one starts.

## Requirements

- iOS 13 or later.
- An API key and an account GUID from PageSuite, plus either a shortcode
  or the publication GUIDs of the titles you’ll show. <doc://com.pagesuite.PSReader/documentation/PSReader/Identifiers>
  explains each one.

## Install the SDK

The SDK is a binary framework, `PSReader.xcframework`. It depends on the
Apryse SDK, which renders PDF pages.

**Swift Package Manager**

1. In Xcode, choose File > Add Package Dependencies.
1. Enter `https://github.com/PageSuite/psreader-swift-package.git`.
1. Choose Exact Version as the dependency rule, and enter the version.
1. Add the `PSReaderSDK` product to your app target.

The package brings in the Apryse SDK for you. In a `Package.swift`:

```swift
.package(url: "https://github.com/PageSuite/psreader-swift-package.git", exact: "26.8.0")

// In your target's dependencies:
.product(name: "PSReaderSDK", package: "psreader-swift-package")
```

**CocoaPods**

The pod is `PSReaderUI2`, in PageSuite’s specs repository. Add the Apryse
pods from their podspecs:

```ruby
source 'https://github.com/PageSuite/psreader-specs.git'
source 'https://cdn.cocoapods.org/'

target 'YourApp' do
  use_frameworks!

  pod 'PDFTron', podspec: 'https://www.pdftron.com/downloads/ios/cocoapods/xcframeworks/pdftron/11.5.0.85515.podspec'
  pod 'PDFTronTools', podspec: 'https://www.pdftron.com/downloads/ios/cocoapods/xcframeworks/pdftron-tools/11.5.0.85515.podspec'
  pod 'PSReaderUI2', '26.8.0'
end
```

Either way, your code imports one module: `import PSReader`.

**Manual Installation**

Drag these frameworks into your project, and set each one to **Embed &
Sign** in your app target’s General settings:

- `PSReader.xcframework`
- `PDFNet.xcframework` and `Tools.xcframework`, from the Apryse SDK

The SDK is tested against Apryse 11.5.0.85515. Use that version if you
add Apryse yourself.

A clean build of your app shows a few deprecation warnings about
`UIMenuController`, from the headers of Apryse’s Tools framework. They
come from Apryse’s code, not yours, and don’t affect the reader.

**Versions**

Versions follow the calendar, as **year.month.patch**: `26.1.0` is the
first January 2026 release. They don’t follow semantic versioning, so a
release can change the API without a major version bump. Pin an exact
version, and read the [Change Log](/documentation/PSReader/Change-Log) before you move to a new one.

## Initialize the SDK

Call [`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:)) once, at launch, as the snippet
above does, and carry on: there’s no need to wait for it or to pass a
completion. It sets your API key and prepares the PDF engine in the
background, and the SDK waits for it wherever it needs to, on both
sides. Calling it again is harmless.

Always pass your key. With `nil`, the default, the call only prepares
the PDF engine: it sets no key, and calls `completion` at once with
`false`. [`initialize(apiKey:)`](/documentation/PSReader/initialize(apiKey:)) is the same call as an `async`
function.

## Choose Prebuilt or Custom UI

With the SDK initialized, decide who builds the interface. Both sides
show every edition on PageSuite’s current system, classic PDF and
responsive alike, and one app can use both.

**The prebuilt UI** is a complete reader app you configure and brand.
These lines, in your scene delegate in place of the placeholder root
view controller, show your publications’ archives and open editions in
the prebuilt reader:

```swift
let globalConfig = GlobalConfiguration(apiKey: "API_KEY", accountGUID: "ACCOUNT_GUID")

let carousel = CarouselViewController(
    globalConfig: globalConfig,
    sections: [.dynamicArchive("Editions", shortcode: "SHORTCODE")]
)
window.rootViewController = carousel
```

Continue with [Prebuilt UI](/documentation/PSReader/Prebuilt-UI).

**A custom UI** is your own interface on the core SDK. You fetch the
catalog, open an edition, and host the SDK’s page renderer in screens you
design. It starts with a request like this one:

```swift
let service = FeedEditionService(accountGUID: "ACCOUNT_GUID")
let latest = try await service.latestEdition(publicationGUID: "PUBLICATION_GUID")
```

Continue with [Custom UI](/documentation/PSReader/Custom-UI).

Not sure which fits? [Choosing an Integration](/documentation/PSReader/Choosing-an-Integration) compares them, and
[Building a Reader App](/documentation/PSReader/Building-a-Reader-App) runs both in one sample project. To set up a
coding agent first, see [Using the SDK With AI Agents](/documentation/PSReader/Using-the-SDK-With-AI-Agents).

## Prepare for App Store Submission

**Export compliance.** The SDK uses no non-standard encryption and doesn’t
affect your export compliance answers.

**Privacy.** The SDK collects no private information and doesn’t affect
your privacy answers.

**Info.plist keys.** The SDK renders PDF pages with the Apryse library,
which needs these usage descriptions in your app’s Info.plist. Word them
for your app:

```xml
<key>NSCameraUsageDescription</key>
<string>This will allow you to use the image from your camera.</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>This will allow you to add images to your photo library.</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>This will allow you to create signatures and annotations from images in your photo library.</string>
<key>NSBluetoothAlwaysUsageDescription</key>
<string>This will allow us to detect if an Apple Pencil is paired, enabling palm rejection and the ability to scroll with one finger while annotating.</string>
<key>NSBluetoothPeripheralUsageDescription</key>
<string>This will allow us to detect if an Apple Pencil is paired, enabling palm rejection and the ability to scroll with one finger while annotating.</string>
```

See the [Apryse iOS integration guide](https://docs.apryse.com/ios/guides/get-started/integration?tab=spm)
for details.

## Topics

### Initializing the SDK

[`initialize(apiKey:)`](/documentation/PSReader/initialize(apiKey:))

Initializes the SDK with your API key, returning when it finishes.

[`initialize(apiKey:completion:)`](/documentation/PSReader/initialize(apiKey:completion:))

Initializes the SDK with your API key.

