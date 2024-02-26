
# Getting Started 

&ensp;*with Native Player SDK for iOS*

## 1. Create a new Xcode project

In Xcode, create a new iOS project using Objective-C or Swift. Use BBNativePlayerExample as the project name.  

## 2. Add the BlueBillywigNativePlayerKit-iOS to the Xcode project

### 2a. Installing the BlueBillywigNativePlayerKit using CocoaPods

CocoaPods is a dependency manager for Xcode projects and is the recommended method for installing the BlueBillywigNativePlayerKit. For more information on installing or using CocoaPods, see the [CocoaPods documentation](https://guides.cocoapods.org/). Once you have CocoaPods installed, use the following instructions to install the IMA SDK:  

In the same directory as your BBNativePlayerExample.xcodeproject file, create a text file called Podfile, and add the following configuration:  

    platform :ios, '12.0'

    target 'BBNativePlayerExample' do
    # Pods for bbnativeplayerkit-demo
    pod 'BlueBillywigNativePlayerKit-iOS', '~>7.98'
    end

From the directory that contains the Podfile, run:
`pod install --repo-update`

This will install the pod 'BlueBillywigNativePlayerKit-iOS' and dependencies, you should see something like this:

`Installing BlueBillywigNativePlayerKit-iOS (0.1.1)`
`Installing BlueBillywigNativeShared-iOS (0.1.1)`
`Installing GoogleAds-IMA-iOS-SDK (3.13.0)`
`Installing google-cast-sdk-dynamic-ios-bb (4.7.0)`

Verify that the installation was successful by opening the BBNativePlayerExample.xcworkspace file and confirming that it contains two projects: BBNativePlayerExample and Pods (the dependencies installed by CocoaPods).
If there is a problem installing or updating the pods use this command:
`pod cache clean --all; rm -rf Podfile.lock Pods; pod install --repo-update`  

### 2b. Installing the BlueBillywigNativePlayerKit using Swift Package Manager

Swift Package Manager (SPM) is a tool for managing Swift packages. It is integrated into Xcode and packages can be added directly to a project through the Xcode UI. For more information on installing packages or using SPM within Xcode, see the [Apple documentation](https://developer.apple.com/documentation/xcode/adding-package-dependencies-to-your-app). Once a new project is created or an existing project is opened in Xcode, use the following steps to add the BlueBillywigNativePlayerKit:

> **Note**
> The following instructions apply to Xcode 14.3.1. In other Xcode versions the names of buttons or menu items may vary slightly.

In Xcode navigate to **File > Add Packages...**. A new window should open with a list of Apple Swift Packages. In the top right corner of the window a search bar should be located containing the following text: _Search or Enter Package URL_. In this search bar enter the URL to the BlueBillywigNativePlayerKit (https://github.com/bluebillywig/bbnativeplayerkit-cocoapod). This will show the **bbnativeplayerkit-cocoapod** package instead of the list of Apple Swift Packages.

> **Note**
> The **bbnativeplayerkit-cocoapod** repository name references CocoaPods. This is due to CocoaPods being the first dependency management tool that was supported. The repository contains the compiled BBNativePlayerKit framework and is not limited to CocoaPods only.

Select the **bbnativeplayerkit-cocoapod** package and below the search bar the general information of the package will appear. Click on the dropdown box next to **Dependency Rule** to select which type of version(s) to use.

> **Note**
> It is strongly recommended to use the **Exact Version** rule as the BlueBillywigNativePlayerKit versions may not exactly follow [Semantic Versioning](https://semver.org/). Click [here](https://github.com/bluebillywig/bbnativeplayerkit-cocoapod/releases) for the list of BBNativePlayerKit versions.

In the text box that appears next to the dropdown box enter the version of the BlueBillywigNativePlayerKit to use. Click on the dropdown box next to **Add to Project** and select a project.

The **Add Package** button in the bottom right corner of the window should now no longer be disabled. Click on this button to include the BlueBillywigNativePlayerKit to the project.

A new window should open showing the progress of downloading/processing the package and its dependencies. This may take some time to complete.

### 2c. Because the framework might use the GoogleCast framework you have to put the following key/strings to your plist

&ensp;**(Apple obligates you to do this if the code reference is there even if you don't want to use ChromeCast)**

    <key>NSBonjourServices</key>
    <array>
    <string>_googlecast._tcp</string>
    <string>ABCD1234._googlecast._tcp</string>
    </array>
    <key>NSBluetoothAlwaysUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>
    <key>NSBluetoothPeripheralUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>    
    <key>NSMicrophoneUsageDescription</key>
    <string>${PRODUCT_NAME} uses microphone access to listen for ultrasonic tokens
    when pairing with nearby Cast devices.</string>

Where "ABCD1234" is your appId. 

The fastest way to find this string is to put in:
----._googlecast._tcp
Then run your app and embed a player
Look for the Log line "....._googlecast._tcp is missing in values associated with the key NSBonjourServices in info.plist"
This will tell you the String that is missing. Change it into that.

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
