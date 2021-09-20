# Native player documentation

## Design Philosophy

The SDK has three main structures; two classes and an interface. 
The BBNativePlayer class only has static factory functions for creating the views that do the actual work. 
The BBNativePlayerView class, which extends the platform’s core UI View class (iOS: UIView, Android: View), is what you place in your layout. 
It offers an API to control the player (callApiMethod) and get/set player properties (getApiProperty/setApiProperty).
Finally, if needed, you make your own implementation of the 
BBPlayerViewDelegate interface and assign it to the player view in order to respond to events.

## Android

Go to [Android documentation](/bbnativeplayersdk/android/latest "Android documentation")

## iOS

Go to [iOS documentation](/bbnativeplayersdk/ios/latest "iOS documentation")
