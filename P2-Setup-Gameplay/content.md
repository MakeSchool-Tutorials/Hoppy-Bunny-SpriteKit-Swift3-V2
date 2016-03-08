---
title: Set up the Gameplay scene
slug: setup-gameplay
---

Let's get started setting up our game scene, SpritKit Scene Editor is a powerful Xcode tool that let's us visually layout our scene.

#Set the stage

> [action]
> Select *GameScene.sks* from the *Project navigator*:
>
> It's helpful to see the scene size, zoom out so you can see the yellow border which represents the scene size. Select `Editor / Zoom Out` or use the shortcut shown.
>
> ![Adjusting GameScene size](../Tutorial-Images/xcode_gamescene_size.png)
>
> Next modify the size parameters as shown in the *Attributes inspector panel*

Remember the device resolution guide in the previous chapter? We will be using a common design points size of 320 x 480, this gives us a nice portrait suited to our artwork.  You may wondered what about the other devices?

Thankfully SpriteKit has you covered and will automatically scale the view to fit the other devices.

> [info]
> If your curious have a look through the code in *GameViewController.swift*.  In particular:
>
```
/* Set the scale mode to scale to fit the window */
scene.scaleMode = .AspectFill
```
>
> If you `highlight` *scaleMode* and look at the *Quick Help inspector* panel you can find out more about the scaling options available.
>

#Add the background image

> [action]
> Select *Show the media library* in the *Library pane* Add the background image by dragging `background` onto the stage:
>
> ![Adding background image](../Tutorial-Images/xcode_gamescene_add_background.png)
>
> We want to centre the background on the screen, you can do this by manually modifying the position as shown to *160, 240* which is exactly half of our size values. Or you can drag around the background and place it by hand.
>
> When you add an object to the game scene this way, a *Color Sprite* object is added to the scene and the texture property is pre populated with the image you select from the media library.  

<!--  -->

> [info]
> A really handy feature is to use node snapping, *Hold down shift* while dragging your object and you will notice it will snap against existing scene objects.  Try moving it around and you will notice it will snap to the left hand edge of the scene, giving you that perfect center point position.
>

#Add the ground image

> [action]
> Now scroll through the media library and add the ground image by dragging it onto the stage:
>
> ![Adding the ground image](../Tutorial-Images/xcode_gamescene_add_ground.png)
>
> For position use the values shown `(160,32)` or anywhere you think looks good, it's your game!

You'll notice the ground image extends beyond the screen border. Don't worry about it, the important part is the ground texture repeats seamlessly.  This will come in handy for scrolling.

#Add the clouds image

> [action]
> Add the clouds to the scene:
>
> ![Adding the clouds](../Tutorial-Images/xcode_gamescene_add_clouds.png)
>
> For position use the values shown `(160, 385)`, or any other value you think looks good. Enjoy this creative freedom. ;)

#Creating the Bunny Scene

Now you're going to create a new *SpriteKit Scene File* for the bunny and animate it.

> [info]
> We will be referring to this file type as *SKS-File* for convenience.

<!--  -->

> [action]
> Create a new *SKS-File* by selecting `File > New > File`:
>
> ![Selecting the SKS File](../Tutorial-Images/xcode_add_sks.png)
>
> Because bunnies are heroes.
>
> ![Creating the SKS File](../Tutorial-Images/xcode_add_sks_hero.png)
>)

#Add the bunny

> [action]
> Ensure *Hero.sks* is selected in *Project navigator*.
> Add *bunny1* to the scene:
>
> ![Adding the bunny character](../Tutorial-Images/xcode_add_bunny_hero_scene.png)
>
> You may not be able to see the bunny, if not zoom out the scene, center your view on the bunny and zoom back in.
> We want to reference the bunny in code later on, so set the *name* to `hero`.
>

<!--  -->

> [info]
> Personally I dislike having the default scene size and yellow border when we are only dealing with a single asset.
> I think it looks better if you click anywhere other than the bunny and modify the scene size (as you did with the *GameScene*
> to `(0,0)`

#Animate the bunny

The animation action you are about to add will be 0.5 seconds long and loop forever.

> [action]
> First, select the *Object library* panel and scroll down until you find the *AnimateWithTextures Action* and drag this
> to the start of the bunny *timeline* as shown:
>
> ![Adding the animation action](../Tutorial-Images/xcode_hero_add_action.png)
>
> Next, modify the duration to be `0.5`, although feel free to play with this value.
> Now time to add the animation frames, click on the action in the *timeline* then click on the *Media library* panel.
> Next drag `bunny1` and `bunny2` into the *Textures* box as shown:
>
> ![Adding the animation frames](../Tutorial-Images/xcode_hero_add_action_frames.png)
>
> Before we play the animation, let's make it loop.  Click on the *Circular arrow* in the bottom left of the action in your timeline
> as shown and select the `Infinity` symbol.
>
> ![Loop animation option](../Tutorial-Images/xcode_hero_action_loop.png)
>
> ![Loop animation forever](../Tutorial-Images/xcode_hero_animation_action_loop.png)
>
> Finally let's see the bunny in action! Click *Animate* in the *timeline* and watch that bunny go.
>
> ![Preview the animation](../Tutorial-Images/xcode_timeline_animate.png)
>

#Summary

The game is already starting to take shape:
* You learnt to build the foundation for your game scene using the visual SpriteKit Scene Editor.
* You've created the hero of our game and setup a sprite frame animation.

Next chapter we will be adding physics to our world.
