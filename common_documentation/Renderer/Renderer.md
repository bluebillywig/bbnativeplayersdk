
# Renderer in the Native SDK


## Renderer

When creating a renderer view via BBNativeRenderer.createRendererView, you supply a json embed URL and (optionally) an options dictionary. 
The json URL is similar to Blue Billywig&rsquo;s standard renderer embed URL. Its only difference is the .json extension, e.g.: 
`https://demo.bbvms.com/r/native_sdk_outstream.json` .  

A helper function exists for constructing it:

    BBNativeRenderer.createJsonEmbedUrl(baseUrl: "https://demo.bbvms.com", appIndicator: "r", appId: "native_sdk_outstream")

In order to bootstrap the renderer, your base class should implement didTriggerApiReady and set itself as the player view delegate:

    rendererView.playerViewDelegate = this / self

Then, in didTriggerApiReady, it can call the renderer's bootstrap function, which takes as arguments a config dictionary {code, vastXml}, an element reserved for future use, and an optional playoutOverrides dictionary. 

After construction, you place the renderer view in your view hierarchy.



Some applications may require the ad's media dimensions. Therefore, upon receiving `didTriggerAdLoaded`, the properties adMediaWidth &amp; adMediaHeight can be retrieved, either directly from the player view via `getApiProperty`, or from the player API.  

Other options that are relevant to pass in:

- adsystem_buid: app bundle id
- adsystem_rdid: resettable device identifier
- adsystem_idtype: identifier type ("idfa" for iOS, "adid" for Android)
- adsystem_is_lat: limit ad tracking (Boolean)
- adsystem_ppid: publisher-provided id

### End screen

When the renderer doesn't collapse on end, an end screen will be shown. The end screen will either show a placeholder or a companion ad.
The companion ad must exist in the VAST and be of type mediumRectangle with the size 300 x 250. If there is no companion ad a placeholder will be shown.

The following AdUnit properties will be used to draw the end screen:

- 'Placeholder background color'
- 'Placeholder text' - text displayed
- 'Placeholder text color' - text color (will default to black or white (depending on the background color) if text color is not set)

*Note:* on iOS the placeholder is not tappable as the iOS IMA SDK doesn't expose the clickthrough url of the original ad. Set your placeholder text accordingly.

### Unsupported

Some of the features of our web-based renderer offering are not (yet) supported in Native. For instance: 

- Mouse-in action &amp; Mouse-out action
- Passback code
- Placement options, incl. &lsquo;Wait for CMP response&rsquo;
- Prebid

