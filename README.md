# Spin-the-Bottle-Game-in-Android-Studio

## Aim:
 To create a multiplayer Spin the Bottle game for Android where one player spins the bottle, and the selected player is determined by the direction in which the bottle spins.
 
## Procedure:
1.Create a New Project: Set up a new Android project in Android Studio using Java as the programming language.

2.Pre-Task Setup: Add the bottle image to the drawable folder and modify the colors.xml file to customize the app's color scheme.

3.Design Activity Layout: Define the UI layout in the activity_main.xml file, including a TextView for the title and an ImageView for the bottle.

4.Implement Spin Functionality: Write the logic in the MainActivity.java file to handle bottle spinning. This involves generating a random rotation direction and animating the bottle accordingly.

5.Handle Animation: Use RotateAnimation to animate the bottle's rotation based on the generated random direction.

6.Ensure Smooth Animation: Set up animation listeners to manage the animation lifecycle and ensure smooth spinning behavior.

7.Test the Application: Run the application on an Android device or emulator to verify that the spin functionality works as expected.

## Program:
```
created by : Sudharsanam R K
```
## colors.xml: 
This file, located in the res/values directory of the Android project, defines color resources that can be referenced throughout the application's layout and code. It helps maintain consistency in the app's visual appearance by centralizing color definitions.
```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <!-- Primary color for the app's toolbar and other UI elements -->
    <color name="colorPrimary">#6200EE</color>
    
    <!-- Dark variant of the primary color, used for status bar and app bar -->
    <color name="colorPrimaryDark">#3700B3</color>
    
    <!-- Accent color used for highlighting and emphasis -->
    <color name="colorAccent">#03DAC5</color>
    
    <!-- Custom color for the background, here represented as green -->
    <color name="green">#0F9D58</color>
</resources>
```
## activity_main.xml:
This file, defines the layout of the main activity UI using XML markup. This file specifies the TextView for the title and the ImageView for the bottle.
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/green" <!-- Set background color to green -->
    tools:context=".MainActivity">

    <!-- TextView to display the game title -->
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="40dp"
        android:fontFamily="cursive"
        android:text="GFG Spin the Bottle" <!-- Set text to "GFG Spin the Bottle" -->
        android:textSize="40dp" /> <!-- Set text size to 40dp -->

    <!-- ImageView for the bottle with onClick attribute to trigger spin -->
    <ImageView
        android:id="@+id/bottle" <!-- Set ID for referencing in Java code -->
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:layout_centerInParent="true" <!-- Center the ImageView horizontally and vertically -->
        android:onClick="spinBottle" <!-- Set onClick method to "spinBottle" -->
        android:src="@drawable/bottle" /> <!-- Set image source to "bottle.png" -->

</RelativeLayout>
```

## MainActivity.java:
This file contains the Java code for the main activity of the Android application. This file implements the spin functionality, including generating random rotation directions and handling animation.
```java
import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.RotateAnimation;
import android.widget.ImageView;

import androidx.appcompat.app.AppCompatActivity;

import java.util.Random;

public class MainActivity extends AppCompatActivity {

    private ImageView bottle; // ImageView for the bottle
    private Random random = new Random(); // Random object for generating random numbers
    private int lastDirection; // Variable to store the last rotation direction
    private boolean spinning; // Flag to indicate if the bottle is currently spinning

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottle = findViewById(R.id.bottle); // Initialize bottle ImageView
    }

    // onClick method for spinning the bottle
    public void spinBottle(View view) {
        // Check if the bottle is not currently spinning
        if (!spinning) {
            // Generate a random angle between 0 and 1800 degrees
            int angle = random.nextInt(1800);

            // Calculate the pivot point for rotation (center of the bottle)
            float pivotX = bottle.getWidth() / 2f;
            float pivotY = bottle.getHeight() / 2f;

            // Create a RotateAnimation to rotate the bottle
            Animation rotateAnimation = new RotateAnimation(
                    lastDirection, angle, pivotX, pivotY); // From last direction to new angle
            rotateAnimation.setDuration(2500); // Animation duration (2.5 seconds)
            rotateAnimation.setFillAfter(true); // Keep the final rotation state after animation

            // Set an animation listener to handle animation events
            rotateAnimation.setAnimationListener(new Animation.AnimationListener() {
                @Override
                public void onAnimationStart(Animation animation) {
                    spinning = true; // Set spinning flag to true when animation starts
                }

                @Override
                public void onAnimationEnd(Animation animation) {
                    spinning = false; // Set spinning flag to false when animation ends
                }

                @Override
                public void onAnimationRepeat(Animation animation) {
                    // Not used, but required to implement AnimationListener interface
                }
            });

            // Update the last direction to the new angle
            lastDirection = angle;

            // Start the rotation animation for the bottle
            bottle.startAnimation(rotateAnimation);
        }
    }
}
```

## Output:
![image](https://github.com/SudharsanamRK/Spin-the-Bottle-Game-in-Android-Studio/assets/115523484/7cfdf4cc-6f8a-4097-ab9f-4a42deb6d980)

## Result:
The Spin the Bottle Android application allows users to spin a virtual bottle, with the selected player determined by the direction of the bottle's spin. The app provides a simple and interactive multiplayer game experience on Android devices.
