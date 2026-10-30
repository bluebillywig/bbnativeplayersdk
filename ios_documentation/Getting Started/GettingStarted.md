
# Getting Started

&ensp;*with Native Player SDK for iOS*

## 1. Create a new Xcode project

In Xcode, create a new iOS project using Objective-C or Swift. Use BBNativePlayerExample as the project name.

## 2. Add the BlueBillywigNativePlayerKit-iOS to the Xcode project

> **Note**
> CocoaPods: version 8.64 is the last version on CocoaPods and gets no further updates. Move to Swift Package Manager; [the migration guide](https://support.bluebillywig.com/native-sdk/ios-sdk-cocoapods-to-swift-package-manager/) has the steps.

### 2a. Installing the BlueBillywigNativePlayerKit using Swift Package Manager

Swift Package Manager (SPM) is integrated into Xcode and packages can be added directly to a project through the Xcode UI. For more information on adding packages, see the [Apple documentation](https://developer.apple.com/documentation/xcode/adding-package-dependencies-to-your-app). The package needs iOS 14.0 or later. It brings the shared module, Google IMA, Google User Messaging Platform and Google Cast, so you do not add those yourself.

> **Note**
> The names of buttons and menu items may vary slightly between Xcode versions.

1. In Xcode, go to **File > Add Package Dependencies**.
2. In the search field, enter the URL of the BlueBillywigNativePlayerKit: `https://github.com/bluebillywig/bbnativeplayerkit-cocoapod`. This shows the **bbnativeplayerkit-cocoapod** package.
3. Set **Dependency Rule** to **Exact Version** and enter 8.63.0 or a later version. A new SDK version can contain breaking changes even when only the middle number goes up. See the [list of versions](https://github.com/bluebillywig/bbnativeplayerkit-cocoapod/releases).
4. Click **Add Package**. Xcode downloads the package and its dependencies, which may take some time.
5. Xcode lists the two products of the package. Pick one:
   - `BlueBillywigNativePlayerKit-iOS`: Google Cast with Bluetooth.
   - `BlueBillywigNativePlayerKit-iOS-NoBluetooth`: Google Cast without Bluetooth.

   Set **Add to Target** to your app target for the product you pick, and to **None** for the other one.

> **Note**
> Add exactly one product, never both. Each one contains its own copy of Google Cast. If your app uses Google Cast without Bluetooth, pick the `-NoBluetooth` product.

The name **bbnativeplayerkit-cocoapod** dates from when CocoaPods was the first dependency manager we supported. The repository is the Swift package with the compiled BBNativePlayerKit framework.

### 2b. Add the Google Cast keys to your Info.plist

    <key>NSLocalNetworkUsageDescription</key>
    <string>${PRODUCT_NAME} needs local area network access for google chromecast device discovery.</string>
    <key>NSBonjourServices</key>
    <array>
    <string>_lnp._tcp</string>
    <string>_googlecast._tcp</string>
    <string>_1F61A3A5._googlecast._tcp</string>
    </array>
    <key>NSBluetoothAlwaysUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>
    <key>NSBluetoothPeripheralUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>${PRODUCT_NAME} uses microphone access to listen for ultrasonic tokens
    when pairing with nearby Cast devices.</string>

Please change the the strings starting with "${PRODUCT_NAME}" so they are appropriate for your app.
If you use the `BlueBillywigNativePlayerKit-iOS-NoBluetooth` product, omit the Bluetooth strings.

## 3. Import the BBNativePlayerKit

Next, add the BBNativePlayerKit framework to the ViewController using an import statement beneath the existing imports.

    import UIKit
    import BBNativePlayerKit
    import bbnativeshared

    class ViewController: UIViewController {

## 4. Create a BBNativePlayerView

In the ViewOnLoad method in the ViewController add the following code to create a BBPlayerView and add it to the current view. Use your own embed url as jsonUrl parameter

    private var bbPlayerView: BBNativePlayerView? = nil

    override func viewDidLoad() {
        super.viewDidLoad()

        // create player view using the embed url
        bbPlayerView = BBNativePlayer.createPlayerView(uiViewController: self, frame: view.frame, jsonUrl: "https://bb.dev.bbvms.com/p/default/c/1092747.json")

        // add player to the view
        view.addSubview(bbPlayerView!)

        // use constraints to place and size the player view
        bbPlayerView?.translatesAutoresizingMaskIntoConstraints = false
        bbPlayerView?.leftAnchor.constraint(equalTo: view.safeAreaLayoutGuide.leftAnchor).isActive = true
        bbPlayerView?.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor, constant: 0 ).isActive = true
        bbPlayerView?.widthAnchor.constraint(equalTo: view.safeAreaLayoutGuide.widthAnchor).isActive = true
        bbPlayerView?.heightAnchor.constraint(equalToConstant: view.safeAreaLayoutGuide.layoutFrame.width * 9/16).isActive = true
    }

## 5. Implement the BBNativePlayerViewDelegate

    override func viewDidLoad() {
        .
        .
        .
        .
        // set class to delegate of player view
        bbPlayerView?.delegate = self
    }

## 6. Implement BBNativePlayerViewDelegate to receive all API events

We will implement the delegate in an extension. You don't have to use an extension but it keeps your code organized<br />Just a few methods are implemented here as an example. See the documentation for a full list.

    extension ViewController: BBNativePlayerViewDelegate {
        func bbNativePlayerView(didTriggerPlaying playerView: BBNativePlayerView) {
            print("Blue Billlywig Player: didTriggerPlaying")
        }

        func bbNativePlayerView(didTriggerPause playerView: BBNativePlayerView) {
            print("Blue Billlywig Player: didTriggerPause")
        }
    }

## 8. Build and run the project

For more information and example code, check out our demo app at [https://github.com/bluebillywig/bbnativeplayerkit-demo](https://github.com/bluebillywig/bbnativeplayerkit-demo)
