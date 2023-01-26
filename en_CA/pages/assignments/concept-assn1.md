# CS2053 -- Concept Assignment 1

## Due: 5pm, Feb 7, 2023

## Repo Setup
Click here to start your repository for this assignment: [Concept Assignment Link](https://classroom.github.com/a/yighRNOU)
You'll get a repository that contains a copy of this very markdown file. Clone the repository as normal, and open the concept-assn1.md file in Visual Studio Code (or your editor of choice).

## Instructions 
Write your answers the file below and commit and push, back up to GitHub, when you are finished. Simply type your answers in the space provide. You can edit this directly on GitHub if you like, too. If you need help with Markdown, see: <https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet>

## Questions 
Answer the following questions related to contents of Chapters 1-4 of the “Game Programming Algorithms and Techniques” book, the contents of our lecture and the contents of the Unity manual.

1. Provide pseudo-code similar to the pseudo code found in the book (and slides) for Pac Man but do it for the first level of the classic game Pong! See a video of [Pong! here](https://www.youtube.com/watch?v=it0sf4CMDeM) to remind yourself.

2. We've talked about three different event functions in Unity: Update, FixedUpdate, and LastUpdate.
   
    a. *When are each of the three functions executed? How does this relate to the game loop?*


    b. *Give an example of something that might occur in each of the three functions*


    c. *Can we control how often each of these functions occur, and if so, how?*


3. In 2D game graphics, explain why buffering is commonly used. Next, explain a reason why someone might want to disable buffering.


4. What is the difference between a tilemap and a tileset?

5. Assume two game objects ```gameObject1``` and ```gameObject2``` in a 2D game.**
- a) Assume that ```gameObject1.position``` is at (2, 2) and ```gameObject2.position``` is at (8, 8), what is the vector that points from ```gameObject1``` to ```gameObject2```?

- b) Write code to calculate direction from ```gameObject1```’s position to ```gameObject2```’s position using vector calculations.
    + Note that direction must be a normalized vector.

6. You are coding a top-down 2D game with stereo sound. In a cut-scene you are scripting and explosion occurs. You must determine whether to play the sound in the right or left speaker depending on where the explosion has occurred relative to the character. Describe how you can solve this problem using vector math. Provide formulas to help explain your answer.

7. The following is the algorithm of Phong Reflection Model:

```csharp
    // Vector3 N = normal of surface
    // Vector3 eye = position of camera
    // Vector3 pos = position on surface
    // float a = specular power (shininess)
    Vector3 V = Normalize(eye – pos) // FROM surface TO camera
    Vector3 Phong = AmbientColor
    foreach Light light in scene
        if light affects surface
            Vector3 L = Normalize(light.pos – pos)
            Phong += DiffuseColor * DotProduct(N, L)
            Vector3 R = Normalize(Reflect(-L, N)) // Reflect –L about N
            Phong += SpecularColor * pow(DotProduct(R, V), a)
        end
    end
```

a. In ```Phong += DiffuseColor * DotProduct(N, L)```, what is the meaning of ```DotProduct(N, L)```? Why do we need to multiply the value of ```DotProduct(N, L)``` with ```DiffuseColor```? For a directional light without a light source position, what is the L vector?

b) For ```Phong += SpecularColor * pow(DotProduct(R, V), a)```, what is the meaning of ```DotProduct(R, V)```? Why we need to multiply value of ```pow(DotProduct(R, V), a)``` with ```SpecularColor```?


8. Consider the following vectors: 
$\vec{a}$ = &lt;3,4,2&gt;,
    $\vec{b}$  = &lt;6,8,0&gt;
and the scalar value $s = 2$

    Calculate each of the following: 

    - a) $\vec{a}$ + $\vec{b}$
    - b) $s$ $\cdot$ $\vec{b}$
    - c) $\vec{a} \times \vec{b}$
    - d) $\vec{a}$ $\cdot$ $\vec{b}$


9. Create a world transform matrix that translates by &lt;3,4,2&gt; and rotates it 90° about the x-axis.
