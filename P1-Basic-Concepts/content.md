---
title: Basic concepts of a side scroller
slug: basic-concepts
---

If you have never built a side scroller before, this introduction will help you understand the basic concepts. There are different ways we can approach this, it may seem most obvious to fly the player through the world and follow the player.  However, it is quite common for the player to be static and the world to move like a conveyor belt.

You will learn to implement the following:

*   A physics controlled bunny
*   Dynamic obstacle object generation and removal
*   Animation and actions
*   World scrolling
*   Implement physics collision detection
*   Create your own custom button class

#Create a new project

If you haven't already, it's time to make a SpriteKit project in Xcode for Hoppy Bunny!

> [action]
> The first step is to create a new SpriteKit Xcode project, open Xcode and select `Create a new Xcode project`. You then need to select `iOS > Application > Game` as shown below:
>
> ![Select New game project](../Tutorial-Images/xcode_new_project.png)

#Adding artwork

> [action]
> After the project is created, you should [download our art pack for this game](https://github.com/MakeSchool-Tutorials/Hoppy-Bunny-SpriteKit-Swift/raw/master/assets.zip). Next we will add the art pack you just downloaded to your Xcode project by first unpacking the archive. Select `Assets.xcassets` in your Xcode project, then select the asset files you downloaded and drag them into Xcode as shown below:
>
> ![Dragging assets into project](../Tutorial-Images/xcode_add_artwork.png)

#Asset Scale

Now would be a great time to touch on asset scale, you may have noticed when you select an asset you are presented with
*1x 2x 3x Scale* options and by default they will be set to *1x Scale*.  

Have a look at this [Device resolution guide](http://www.paintcodeapp.com/news/ultimate-guide-to-iphone-resolutions)

In particular look at the *Rendered Pixels* section and notice the reference to scale factor.  Our assets were designed for 2x resolution devices.

> [action]
> Ensure you have the *Assets.xcassets* selected in the *Project Navigator* and then select each asset file and drag them from *1z* to *2x*
>
> You can remove the spaceship asset, we will not be using it.

#Summary
Great, you've setup a basic project and added the artwork. In the next section it's time to start building our game.
