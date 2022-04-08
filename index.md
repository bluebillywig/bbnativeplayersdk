# Native Player SDK

## Design Philosophy

The SDK has three main structures; two classes and an interface.  

The *BBNativePlayer* class only has static factory functions for creating the views that do the actual work.  
The *BBNativePlayerView* class, which extends the platform’s core UI View class (iOS: UIView, Android: View), is what you place in your layout. 
It offers an API to control the player (`callApiMethod`) and get/set player properties (`getApiProperty`/`setApiProperty`).  
Finally, if needed, you make your own implementation of the 
*BBPlayerViewDelegate* interface and assign it to the player view in order to respond to events.  

When creating a player view, you supply a json embed URL and (optionally) an options dictionary. The json URL is similar to Blue Billywig's standard embed URL. Its only difference is the .json extension, e.g. `https://demo.bbvms.com/p/default_standard/c/2431946.json` . Thus, it supports various content types (clip, playlist, project), and playout configurations.

## Android

[Getting Started](android_documentation/Getting%20Started/GettingStarted.html "Android Getting Started")  
[Android SDK Reference](/bbnativeplayersdk/android/latest "Android SDK Reference")  
[Android Demo App](https://github.com/bluebillywig/bbnativeplayersdk-demo "Android Demo App")  

## iOS

[Getting Started](ios_documentation/Getting%20Started/GettingStarted.html "iOS Getting Started")  
[iOS SDK Reference](/bbnativeplayersdk/ios/latest "iOS SDK Reference")  
[iOS Demo App](https://github.com/bluebillywig/bbnativeplayerkit-demo "iOS Demo App")  
&ensp;[Know How: Adding a close button to the modal player view](ios_documentation/Know%20How/Adding%20a%20close%20button%20to%20the%20modal%20player%20view.html "special topics")  
&ensp;[Know How: How to enable ChromeCast](ios_documentation/Know%20How/How%20to%20enable%20ChromeCast.html "special topics")  
&ensp;[Know How: How to enable picture in picture and Airplay](ios_documentation/Know%20How/How%20to%20enable%20picture%20in%20picture%20and%20Airplay.html "special topics")  

## Common

[Outstream](common_documentation/Outstream/Outstream.html "Outstream")  
