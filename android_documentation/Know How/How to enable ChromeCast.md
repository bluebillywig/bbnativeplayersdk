# How to enable ChromeCast

## ChromeCast Button
To use the ChromeCast button in your app (e.g. as a NavigationItem) use the player factory to create the MediaRouteButton.
*example:*

    val castButton = BBPlayerView.createChromeCastButton(context)

Even if you're not using it, you should create one in your the MainActivity, otherwise players in Fragments might have their cast button disabled.
*example:*

    val dummy = BBPlayerView.createChromeCastButton(context)


## ChromeCast MiniControls
To use the ChromeCastMiniControls in your app (eg at the bottom of your view) use the player factory to get the ChromecastMiniControlsView.
*example:*

    val chromeCastMiniControlsView = BBPlayerView.getChromeCastMiniControlsView(context)

If you want to show the Chromecast MiniControls within the player:
- use the `showChromeCastMiniControlsInPlayer` option when creating the player:

*example:*

    bbPlayerView = BBNativePlayer.createPlayerView(this, "https://demo.bbvms.com/p/default/c/4146866.json", mapOf("showChromeCastMiniControlsInPlayer" to true))


If you want a player **without** ChromeCast functionality, either:

- disable the cast-button in the playout settings, or
- use the "noChromeCast" option when creating the player:

*example:*

    bbPlayerView = BBNativePlayer.createPlayerView(this, "https://demo.bbvms.com/p/default/c/4146866.json", mapOf("noChromeCast" to true))


*Note:*
Players with "autoPlay" will never auto-cast.
Players with "InView - Play" actions will never auto-cast.
