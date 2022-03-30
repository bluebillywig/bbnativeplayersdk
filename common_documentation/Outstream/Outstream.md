
# Outstream in the Native SDK


## Outstream

When creating a player view, you supply a json embed URL and (optionally) an options dictionary. 
The json URL is similar to Blue Billywig&rsquo;s standard outstream embed URL. Its only difference is the .json extension, e.g.: 
`https://demo.bbvms.com/a/native_sdk_outstream.json` .  

A helper function exists for constructing it:

    BBNativePlayer.createJsonEmbedUrl(baseUrl: "https://demo.bbvms.com", appIndicator: "a", appId: "native_sdk_outstream")

If the outstream ad needs to start collapsed and/or collapse on end, as per the adunit&rsquo;s (root-) settings, this has to be allowed explicitly via embed option &lsquo;allowCollapseExpand&rsquo; = true.
Furthermore, the enclosing view needs to be unconstrained in the vertical direction; 
`android:layout_height="wrap_content"` and at most one of `app:layout_constraintTop`, `app:layout_constraintBottom` .

Some applications may require the ad's media dimensions. Therefore, upon receiving `didTriggerAdLoaded`, the properties adMediaWidth &amp; adMediaHeight can be retrieved, either directly from the player view via `getApiProperty`, or from the player API.  

Other options that are relevant to pass in:

- adsystem_buid: app bundle id
- adsystem_rdid: resettable device identifier
- adsystem_idtype: identifier type ("idfa" for iOS, "adid" for Android)
- adsystem_is_lat: limit ad tracking (Boolean)
- adsystem_ppid: publisher-provided id

### End screen

When the outstream ad doesn't collapse on end, an end screen will be shown. The end screen will either show a placeholder or a companion ad.
The companion ad must exist in the VAST and be of type mediumRectangle with the size 300 x 250. If there is no companion ad a placeholder will be shown.

The following AdUnit properties will be used to draw the end screen:

- 'Placeholder background color'
- 'Placeholder text' - text displayed
- 'Placeholder text color' - text color (will default to black or white (depending on the background color) if text color is not set)

*Note:* on iOS the placeholder is not tappable as the iOS IMA SDK doesn't expose the clickthrough url of the original ad. Set your placeholder text accordingly.
### Unsupported

Some of the features of our web-based outstream offering are not (yet) supported in Native. For instance: 

- Mouse-in action &amp; Mouse-out action
- Passback code
- Placement options, incl. &lsquo;Wait for CMP response&rsquo;
- Prebid


## Pseudo-outstream

*Click-To-Play &amp; Ad-Only-AutoPlay*

Again, when creating a player view, you supply a json embed URL and (optionally) an options dictionary. 
The json URL is similar to Blue Billywig’s standard player embed URL. Its only difference is the .json extension, e.g.: 
`https://demo.bbvms.com/p/default_standard/c/2431946.json` .  

Thus, it supports various content types (clip, playlist, project), and playout configurations.  

A helper function exists for constructing it:

    BBNativePlayer.createJsonEmbedUrl(baseUrl: "https://demo.bbvms.com", appIndicator: "p", appId: "default_standard", contentIndicator: "c", contentId: "2431946")

Other options that are relevant:

- adsystem_buid: app bundle id
- adsystem_rdid: resettable device identifier
- adsystem_idtype: identifier type ("idfa" for iOS, "adid" for Android)
- adsystem_is_lat: limit ad tracking (Boolean)
- adsystem_ppid: publisher-provided id

### Unsupported

Some of the features of our web-based player offering are not (yet) supported in Native. For instance:

- Sticky options (Float, etc.)

