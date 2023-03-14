# 2053 Lab Assignment #5: Rotation and Lights 

In this lab assignment, you will gain experience with game object rotation in multiple axes, as well as using different light types.

## Due: 5pm, Tuesday, March 21, 2023

Invite link: [Invite](https://classroom.github.com/a/qOKpf9wK)
See video example of completed assignment on Teams

## Background
Right-click all links and open in a new tab. Review the following materials (just for the specified parts of the larger document) before you get started:
 - [Step 8 of Lighting Tutorial: Ambient Lighting](https://learn.unity.com/tutorial/introduction-to-lighting-and-rendering#5c7f8528edbc2a002053b52f)
 - [Step 9 of Lighting Tutorial: Light Types](https://learn.unity.com/tutorial/introduction-to-lighting-and-rendering#5c7f8528edbc2a002053b530)
 - [LookAt](https://unity3d.com/learn/tutorials/topics/scripting/look)

## 1. Preliminary Steps
 - a) Your scene should start with a custom Skybox. You have been provided with a bunch of Skyboxes (see the folder in Assets). Choose a skybox you like and drag and drop it into your Scene.
 - b) Import the JET 3D model into a Models folder in Assets to the game scene. Change the name of the 3D game object to “Jet”. In inspector, move the object’s position to <10,0,0> and rotate the object 90 degrees about Y-Axis.
 - c) Set the camera to be a child of the aircraft, and position it appropriately so it follows the aircraft.
 - d) Create a new script for “Jet” object with name "JetController”, and copy and paste the following code. Carefully read and understand the code.
 
```csharp
public class JetController : MonoBehaviour {
    float circleRadius;
    float circleSpeed;
    float circleAngle;
    float selfRotationSpeed;
    Vector3 lastDirection;

     void Start () {
        circleRadius = 10;
        circleSpeed = 0.5f;
        circleAngle = 0;
        selfRotationSpeed = 100;

        lastDirection = new Vector3(1, 0, 0);
        lastDirection.Normalize();
    }

    void Update() {

        circleAngle += circleSpeed * Time.deltaTime;
        circleAngle = circleAngle % (2*Mathf.PI);

        float newPositionX = circleRadius * (float)Mathf.Cos(circleAngle);
        float newPositionZ = circleRadius * (float)Mathf.Sin(circleAngle);

        Vector3 newPosition = new Vector3(newPositionX, transform.position.y, newPositionZ);
        Vector3 newDirection = newPosition - transform.position;

        newDirection.Normalize();

        float rotationAngle = -Vector3.Angle(lastDirection, newDirection);
        transform.Rotate(Vector3.up, rotationAngle, Space.World);
        transform.Rotate(Vector3.forward, selfRotationSpeed * Time.deltaTime, Space.Self);

        transform.position = newPosition;
        lastDirection = newDirection;
    }
}
```
  - e) Run the program and observe how the Jet object moves along a circular path. It rotates around Space.World as it moves around the circle (counterclockwise around the scene), and rotates around its own forward axis (Space.Self, does a barrel roll).
  - f) Finally, make some adjustments to the project's lighting setup:
    + Open the Lighting settings: Window -> Rendering ->Lighting
    + Next change the Environment Lighting -> "Source" to "color"
    + And, set the Ambient Color to Black.
    + Run the program again to see the changes to the lighting. You can keep the Lighting settings window open and flip back and forth while running the game.

## 2. Requirements
 - a) Make the following changes to the program to make the Jet object's movement around the circular path and self-rotation controlled by the keyboard keys:
    + Pressing the “up” key, the Jet will go forward along the circular path. You will probably want to move all logic to a new function (e.g., TranslateJet()), and just leave the key press check in Update().
    + Pressing the “left” or “right” keys, the object will roll left or right.
    + Be sure to test your program after the change. 
    + Hint: Only one line of the code is responsible for rolling the Jet, the other lines are for moving forward around the circle.
    + Note that your plane may "jump" on the first frame. If you force the plane to do an iteration of translation at the start, this should resolve the issue.

 - b) Add 3 obstacles on your Jet's path. 
     + Each one should require your airplane to rotate differently.
     + Hint: A trick to find good positions for your obstacles is to do the following: 
       - run your game, get the Jet on the circular path and then pause your game, at a position and rotation you would like for your obstacle.
       - Go to your Jet and copy its transform values (In the Inspector, click the gear on Transform and "Copy Component"). 
       - Stop the game and go your Obstacle's Transform and paste in the values (click the gear on Transform and "Paste Component Values")
       - Now your Obstacle will start in this position. 
    
 - c) Add in collision handling.
     + When a collision happens (because the Jet is not oriented properly to fit through the gap of the obstacle) the Jet should not be able to fly forward; however, it should be able to rotate. 
     + Add a BoxCollider to your Jet, increase the size of the Collider so that it is pretty close to the size of the Jet (it doesn't have to be perfect).
         * Remember to set the isTrigger check-box on your Jet.
         * Hint: use OnTriggerStay and OnTriggerExit, to set a flag noting whether forward movement is allowed.

 - d) There will be countdown time for going around the whole circle path. If the player takes more than the time limit, the player loses the game.
 - e) You should let the play go several rounds. Make each later round have shorter time limit to make it more difficult.
     + You may find your jet's path "drifts" over time, so that it is unable to pass through the obstacles on the second or third round. This comes from small integration issues piling up over time. The following code snippet can solve it if placed near the end the Update function, but you will also need to declare and initialize the variables:
     ```csharp
        if(circleAngle < 1 && !reset){
            transform.rotation = Quaternion.Euler(new Vector3(0,0,transform.localEulerAngles[2]));
            newPosition = new Vector3(10,0,0);
            newDirection = new Vector3(0,0,0);
            circleAngle = 0;
            reset = true;
            //You may also want to reset the timer in here
        }
        if(circleAngle > 1){
            reset = false;
        }
     ```
 - f) In addition to the above game play, you need to add and allow control over the following lighting options during game playing.
     + Pressing the “a” key to toggle the colors of the ambient light between red and black.
         * See the Unity Reference for: [ RenderSettings.ambientSkyColor](https://docs.unity3d.com/ScriptReference/RenderSettings-ambientSkyColor.html)
         *  ``` RenderSettings.ambientSkyColor = Color.black;```

     + Pressing the “d” key will toggle the directional light on or off. (enable/disable component)
         * Your scene should already have a directional light.
         * You may optionally change the settings and position of your directional light.
         
     + Create a new point light that has a green color. Pressing the “p” key to toggle it on or off.
         * Make sure the point light can reach 50% of game scene. 

         
     + Create a spot light with a blue color. Put it in the center of the game scene. Make the light rotate to always cover the moving aircraft object. Press "s" key to toggle the light on or off.
         * See: [Transform.LookAt](https://docs.unity3d.com/ScriptReference/Transform.LookAt.html)

     
     + Hint: For all of the above lights, you may need to adjust the parameters to make sure that they work appropriately (e.g., Intensity and Range). Remember to check the Scene view while your game is running to see the location and behaviour of your lights.   

 - g) Finish it all off
     + Add in Text elements (see Lab Assignment #4) to display a message when the game ends. This could be in a GameController script (but you can also just have a really messy JetController script).
     + Remember to add in an 'r' to restart the game, which can be pressed at any time.
     + Make sure that you meet all other game requirements!
     + Test and submit!

## Test and Submit
### Build and Test on Your Platform
 - Remember to save your scene.
 - Remember to put your scene in the scenes folder
 - Remember to "commit" and then "push" everything to GitHub
 - Remember you can be extra sure that everything works by cloning your completed code and opening it as a new project in Unity. Does it work the same as when you submitted it?