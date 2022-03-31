
# Getting Started 

&ensp;*with Native Player SDK for Android*
## 1. Create a new Android project

In Android studio, create a new Android project and select "Empty Activity". Select the language of your choice, for this example we will be using kotlin. Use BBNativePlayerExample as the project name.  

## 2. Add the bbnativeplayersdk dependency

Add com.bluebillywig.bbnativeplayersdk:bbnativeplayersdk:&lt;version&gt; to the app/build.gradle:

    plugins {
        id 'com.android.application'
        id 'kotlin-android'
    }
    
    android { ... }
    
    dependencies {
        ....
        implementation 'com.bluebillywig.bbnativeplayersdk:bbnativeplayersdk:&lt;version&gt;'
        ....
    }

For build.gradle.kts this would be:

    plugins {
        id("com.android.application")
        kotlin("android")
    }
    
    android { ... }
    
    dependencies {
        ....
        implementation("com.bluebillywig.bbnativeplayersdk:bbnativeplayersdk:&lt;version&gt;")
        ....
    }

Now wait until the gradle sync has finished.

## 3. Import the bbnativeplayersdk

Next, add the bbnativeplayersdk framework to the MainActivity using an import statement beneath the existing imports.
### Java

    package com.bluebillywig.bbnativeplayerexample;
    ...
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayer;
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayerView;

### Kotlin

    package com.bluebillywig.bbnativeplayerexample;
    ...
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayer
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayerView

## 4. Setup a (Linear)Layout

Next, add a LinearLayout in the parent layout in activity_main.xml.
    &lt;LinearLayout
            android:id="@+id/player_container"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:orientation="vertical"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"/&gt;

## 5. Create a BBNativePlayerView

In the onCreate method in the MainActivity add the following code to create a BBPlayerView and add it to the current view. Use your own embed url as jsonUrl parameter
### Java

    package com.bluebillywig.bbnativeplayerexample;
    
    import androidx.appcompat.app.AppCompatActivity;
    
    import android.os.Bundle;
    import android.widget.LinearLayout;
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayer;
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayerView;
    
    public class MainActivity extends AppCompatActivity {
        private LinearLayout playerContainer;
        private BBNativePlayerView playerView;

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            playerContainer = findViewById(R.id.player_container);

            playerView = BBNativePlayer.Companion.createPlayerView(this, "https://demo.bbvms.com/p/native_sdk_inoutview/c/4256635.json", null);
        
        playerContainer.addView(playerView);
        }
    }

### Kotlin

    package com.bluebillywig.bbnativeplayersdk_test

    import android.os.Bundle
    import android.widget.LinearLayout
    import androidx.appcompat.app.AppCompatActivity
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayer
    import com.bluebillywig.bbnativeplayersdk.BBNativePlayerView

    class MainActivity : AppCompatActivity() {
        private lateinit var playerContainer: LinearLayout
        private var playerView: BBNativePlayerView? = null

        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)
            setContentView(R.layout.activity_main)

            playerContainer = findViewById&lt;LinearLayout&gt;(R.id.player_container)

            playerView = BBNativePlayer.createPlayerView(this, "https://demo.bbvms.com/p/native_sdk_inoutview/c/4256635.json")
        
        playerContainer.addView(playerView)
        }
    }

## 5. Implement the BBNativePlayerViewDelegate

For java this will ask if you would want to implement all methods in the BBNativePlayerViewDelegate, just say yes.
### Java

    public class MainActivity extends AppCompatActivity implements BBNativePlayerViewDelegate {
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            ....
            playerView.delegate = this
        }
    }

### Kotlin

    class MainActivity : AppCompatActivity(), BBNativePlayerViewDelegate {
        override fun onCreate(savedInstanceState: Bundle?) {
            ....
            playerView.setDelegate(this);
        }
    }

## 6. Implement BBNativePlayerViewDelegate to receive all API events

Just a few methods are implemented here as an example. See the documentation for a full list.
### Java

    public class MainActivity extends AppCompatActivity implements BBNativePlayerViewDelegate {
        ...
        @Override
        public void didTriggerPlaying(view: BBPlayerView) {
            Log.println(Log.INFO, "MainActivity", "Blue Billlywig Player: didTriggerPlay");
        }

        @Override
        public void didTriggerPause(view: BBPlayerView) {
            Log.println(Log.INFO, "MainActivity", "Blue Billlywig Player: didTriggerPause");
        }
        ...
    }

### Kotlin

    class MainActivity : AppCompatActivity(), BBNativePlayerViewDelegate {
        ...
        override fun didTriggerPlaying(view: BBPlayerView) {
            Log.println(Log.INFO, "MainActivity", "Blue Billywig Player: didTriggerPlaying")
        }

        override fun didTriggerPause(view: BBPlayerView) {
            Log.println(Log.INFO, "MainActivity", "Blue Billywig Player: didTriggerPause")
        }
        ...
    }

## 8. Build and run the project

For more information and example code, check out our demo app at [https://github.com/bluebillywig/bbnativeplayersdk-demo](https://github.com/bluebillywig/bbnativeplayersdk-demo "bbnativeplayersdk-demo")

## 9. Testing with snapshot version

For example: `com.bluebillywig.bbnativeplayersdk:bbnativeplayersdk:&lt;version&gt;-SNAPSHOT`  

To test with a snapshot version with Android gradle plugin 4.2.2 and gradle version 6.7.1  

Edit the root build.gradle(.kts) file and add:

    allprojects {
        repositories {
            ...
            maven {
                url "https://s01.oss.sonatype.org/content/repositories/snapshots"
                (or .kts)
                url = "https://s01.oss.sonatype.org/content/repositories/snapshots"
            }
        }
    }

To test with a snapshot version with Android gradle plugin 7.0 and gradle version 7.02 (and above)  

Edit the root settings.gradle(.kts) file and add:

    dependencyResolutionManagement {
        ...
        repositories {
            ...
            maven {
                url "https://s01.oss.sonatype.org/content/repositories/snapshots"
                (or .kts)
                url = "https://s01.oss.sonatype.org/content/repositories/snapshots"
            }
        }
    }
