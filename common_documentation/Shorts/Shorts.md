
# Shorts in the Native SDK
*(as of v8.21.0)*

## Embedding

When creating a shorts view via `BBNativeShorts.createShortsView`, you supply a json embed URL and (optionally) an options dictionary. 
The json URL can be acquired from the OVP, by choosing Embed type 'JSON' in the Preview & Embed window, e.g.: 
`https://demo.bbvms.com/sh/58.json` .  

Also, a helper function exists for constructing it:

    BBNativeShorts.createJsonEmbedUrl(baseUrl: "https://demo.bbvms.com", appIndicator: "sh", appId: "58")

In the OVP, you can choose between three display formats; 'Full screen', 'Player only', and 'Shelf'. The first two render the same on mobile web, hence native doesn't differentiate between them either. However, in native, other than on web, the display format is selected via an option:

- &lsquo;displayFormat&rsquo;: "list" for Shelf, or "player" for Player only.

Currently, there are no other relevant options.


If the Shorts Shelf needs to be responsive with respect to its height, the **enclosing view** needs to be unconstrained in the vertical direction, viz.: 
### Android
`android:layout_height="wrap_content"` and at most one of `app:layout_constraintTop`, `app:layout_constraintBottom` .
### iOS
`heightAnchor.constraint(...).isActive = false` and at most one of  
`topAnchor.constraint(...).isActive = true`, `bottomAnchor.constraint(...).isActive = true` .


## Unsupported

Some of the features of our web-based Shorts offering are not (yet) supported in native. For instance: 

- Advanced Sharing
- First ad position

