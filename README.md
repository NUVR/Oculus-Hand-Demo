# Oculus Hand Demo

A working demo of a grabbable sphere object and the Oculus Avatar SDK prefabs.

## Installation

Requires:

-   Unity 2018.2.9
-   Oculus Integration from the Unity Asset Store

## Preview

![Preview](demo.gif)

## Design Process

-   Open up Unity
    -   This takes a little while so do that before anything else. Be sure to open the project
-   Download the Unity packages from https://developer.oculus.com/downloads/unity/
    -   Download Oculus Avatar SDK and Oculus Platform SDK
    -   Inside the Unity folder of each of these archives, drop the unitypackage file into Unity’s Project tab
-   In the Unity Asset Store, search for “Oculus Integration” and download, import
    -   Click on “Go ahead” if you see the prompt
    -   If prompted to update and restart, restart Unity! Otherwise, you will run into problems with tracking (like phasing through the floor, I had this happen several times!)
-   In the SampleScene
    -   Right click, create a 3D Object > Plane
        -   Set position coordinates to 0, 0, 0
-   Right click, create a 3D Object > Cube
    -   Set y-coordinate to 0.5
-   In the Project tab
    -   Right click on Assets, create a Material. Name it “Cube”
    -   Set the Albedo color to whatever you’ve like. This is the color of the cube we just created
    -   Drag the material onto the 3D cube in the scene
    -   This is going to serve as our table for the object we wish to grab
-   In the SampleScene
    -   Right click, create a 3D Object > Sphere
        -   Set the y-coordinate position to 0.6
        -   Set scale to 0.2 for all 3
    -   Add a Rigidbody to this object so that it gets affected by gravity and movement
-   Click Edit > Project Settings > Player
    -   Under the XR Settings tab, turn on “Virtual Reality Supported”
    -   At this stage, if you were to click “Run”, you can look around in your world using the Oculus
-   Inside Assets > Oculus > VR > Prefabs
    -   Add the OVRPlayerController to the scene
    -   Set the position to X: -2, Y: 1
    -   This lets us move our avatar around using the joysticks on the left and right hands
-   Inside Assets > Oculus > Avatar > Content > Prefabs
    -   Open up OVR PlayerController > OVRCameraRig > TrackingSpace and drop the LocalAvatar
    -   This lets you see your hands
    -   We can change the material of the hands by opening LocalAvatar and modifying hand_left or hand_right. Let’s drag our Cube material onto hand_left_renderPart
-   Making things grabbable!
    -   Now, we need to add the OVR Grabber script to our Left and Right Hand Anchors
    -   Select both LeftHandAnchor and RightHandAnchor at the same time and click “Add Component”.
    -   Search OVR Grabber (or navigate to Oculus > VR > Scripts > Util)
    -   Click “Add Component” and search for “Sphere Collider”. Toggle “Is Trigger” on
    -   In the Rigidbody section, toggle “Use Gravity” off and “Is Kinematic” on. This is required for grabbing to work
    -   Click on each anchor and drag the object from the scene over to the setting in the OVR Grabber script that says “Grip Transform”
        -   This is where grabbed objects will transform to
    -   Open the “Grab Volumes” tab and set the size to 1. This is where we specify a grab collider. Here, we also want to drag the object from the scene.
    -   For each respective hand, also set the “Controller” to L Touch or R Touch
        -   This is the button that triggers grabbing
-   Make the sphere grabbable
    -   Click on the sphere object and “Add Component” > OVR Grabbable. Make sure this script is turned on. It loads off by default
    -   This is where you can specify things like what position the object should be when it gets grabbed, how the object should face, etc.
