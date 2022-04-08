# How to enable ChromeCast

To enable the built-in ChromeCast functionality:  (as of version 7.76)
Add the following key and values to your Info.plist

    <key>NSBonjourServices</key>
    <array>
    <string>_googlecast._tcp</string>
    <string>ABCD1234._googlecast._tcp</string>
    </array>

Where "ABCD1234" is your appId. 

The fastest way to find this string is to put in:
----._googlecast._tcp
Then run your app and embed a player
Look for the Log line `"....._googlecast._tcp is missing in values associated with the key NSBonjourServices in info.plist"`
This will tell you the String that is missing. Change it into that.


Add the following key/strings to your plist:

    <key>NSBluetoothAlwaysUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>
    <key>NSBluetoothPeripheralUsageDescription</key>
    <string>${PRODUCT_NAME} uses Bluetooth to discover nearby Cast devices.</string>	
    <key>NSMicrophoneUsageDescription</key>
    <string>${PRODUCT_NAME} uses microphone access to listen for ultrasonic tokens
    when pairing with nearby Cast devices.</string>

## CastButton
To use the ChromeCast button in your app (eg as a NavigationItem) use the player api to get the UIButton.
*example:*

    if let castButton = bbPlayerView?.player.createChromeCastButton {
    castButton.tintColor = UIColor.black
    navigationItem.rightBarButtonItem = UIBarButtonItem(customView: castButton)
    }

## ChromeCast MiniControls
To use the ChromeCastMiniControls in your app (eg at the bottom of your view) use the player api to get UIView.
*example:*

    if let chromeCastMiniControlsView = bbPlayerView?.player.getChromeCastMiniControlsView {
    self.view.addSubview(chromeCastMiniControlsView)
    chromeCastMiniControlsView.translatesAutoresizingMaskIntoConstraints = false
    chromeCastMiniControlsView.leftAnchor.constraint(equalTo: self.view.leftAnchor).isActive = true
    chromeCastMiniControlsView.bottomAnchor.constraint(equalTo:  self.view.safeAreaLayoutGuide.bottomAnchor).isActive = true
    chromeCastMiniControlsView.widthAnchor.constraint(equalTo: self.view.widthAnchor).isActive = true
    chromeCastMiniControlsView.heightAnchor.constraint(equalToConstant: 75).isActive = true
    }


If you want to show the Chromecast MiniControls within the player:
- use the `showChromeCastMiniControlsInPlayer` option when creating the player:

*example:*

    bbPlayerView = BBNativePlayer.createPlayerView(uiViewController: self, frame: view.frame, jsonUrl: "https://demo.bbvms.com/p/default/c/4146866.json", options: ["showChromeCastMiniControlsInPlayer": true])


If you want a player **without** ChromeCast functionality:

- disable the cast-button in the playout settings
- use the "noChromeCast" option when creating the player:

*example:*

    bbPlayerView = BBNativePlayer.createPlayerView(uiViewController: self, frame: view.frame, jsonUrl: "https://demo.bbvms.com/p/default/c/4146866.json", options: ["noChromeCast": true])


*Note:*
Players with "autoPlay" will never auto-cast.
Players with "InView - Play" actions will never auto-cast.
