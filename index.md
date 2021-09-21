# Native Player SDK

## Design Philosophy

The SDK has three main structures; two classes and an interface.  

The *BBNativePlayer* class only has static factory functions for creating the views that do the actual work.  
The *BBNativePlayerView* class, which extends the platform’s core UI View class (iOS: UIView, Android: View), is what you place in your layout. 
It offers an API to control the player (`callApiMethod`) and get/set player properties (`getApiProperty`/`setApiProperty`).  
Finally, if needed, you make your own implementation of the 
*BBPlayerViewDelegate* interface and assign it to the player view in order to respond to events.

## Android

[Getting Started](/bbnativeplayersdk/android_documentation/Getting%20Started/GettingStarted.html "Android Getting Started")  
[Android SDK Reference](/bbnativeplayersdk/android/latest "Android SDK Reference")  
[Android Demo App](https://github.com/bluebillywig/bbnativeplayersdk-demo "Android Demo App")  

## iOS

[Getting Started](/bbnativeplayersdk/ios_documentation/Getting%20Started/GettingStarted.html "iOS Getting Started")  
[iOS SDK Reference](/bbnativeplayersdk/ios/latest "iOS SDK Reference")  
[iOS Demo App](https://github.com/bluebillywig/bbnativeplayerkit-demo "iOS Demo App")  
