# Lab Assignment #1: Extended Roll-A-Ball Game

In this first lab assignment we will take two weeks. This will allow us to make sure that you are set up and you can work through any technical problems. And, for you to get used to following the written instructions *carefully*.

The lab assignment will consist of two parts. In part 1, to be completed by **January 17** you will complete an introductory tutorial. In part 2, you will extend the work you have done and improve your game. You will submit both part 1 and Part 2 by **January 24** on GitHub.

## Unity uses C# not Java

Java and C# are so close we will not cover the differences in class formally, you are expected to pick up on this on your own. Students have had no problem making this transition in past years. However, here is a great reference on [C# for Java Developers](https://nerdparadise.com/programming/csharpforjavadevs) that covers the main differences, it is worth skimming this before you go any further.

## Part 1 - to be completed January 18
The goal of first lab is to get every one acquainted with Unity and the lab environment. There will be nothing to submit for Part 1.

First, you will need to initiate the project by following the GitHub invitation link, cloning it to your local computer and opening it in Unity. See [Instructions for Working with GitHub](https://ismithbwr.github.io/en_CA/#!pages/CS2053-working-with-git.md).

GitHub Invitation: [Assignment 1](https://classroom.github.com/a/0UXUKSlD)

Once you have opened up your project in Unity, complete the [Roll-A-Ball Tutorial](https://learn.unity.com/project/roll-a-ball). 

**Note: Watch but do not complete the steps in the very first video ("Setting up the Game"), since you do this by cloning the repo from GitHub and opening it in Unity. Also, you do not need to complete the steps in the final section ("Building the Game"). Instead you will submit your project on GitHub. ALWAYS double check that your repo is pushed successfully to GitHub (open it in a browser and refresh the page), and feel free to push often**

## Updates to Tutorial
Some parts of the tutorial are slightly different due to it being recorded on a different unity version. I have noted down the differences and adjustments that I noticed when following along with Unity 2021.3.14.

Part 1: Setting up the Game
- Template is called 3D URP
- "Layout" is under the Window tab
- Toolbar may be in Scene window
- Light color is under Emission->Filter

Part 2: Moving the Player
- Installing Input System Package -> Select "Unity Registry," not "All Packages"
- Don't change Architecture under build settings (keep Intel 64-bit)
- Intellisense in VS Code may not work:
    - (In Unity Editor) Edit->Preferences->External Tools->External Script Editor = Visual Studio Code
   - Close VS Code, open the script again

Part 3: Moving the Camera
- May need to explicitly declare GameObject player as public

Part 5: Creating Collectibles
- You may want to make a parent for each collectible (and put all parents under another parent class) so that it will have its axis along the world frame, making it easier to drag along the ground (whereas each pickup object has a rotated axis)


## Lab Part 2 - Coming Soon!

### Test and Submit
- Playtesting is an essential part of game development. Play your game... a lot. Does it work all the time? If not, see if you can fix any problems. Give your self enough time to ask questions on Teams, if you are stuck.
- Once you are happy with your work. Save it in Unity and then Commit and Push it to GitHub by following the [instructions on the course website](https://ismithbwr.github.io/en_CA/#!pages/CS2053-working-with-git.md).