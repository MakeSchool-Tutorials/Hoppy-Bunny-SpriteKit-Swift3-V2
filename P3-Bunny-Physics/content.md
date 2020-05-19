---
title: You've got to let the bunny fly!
slug: bunny-physics
---

Time to setup physics for your game world and game play objects.

# SpriteKit Physics

You will be using the powerful physics engine built into SpriteKit, thankfully it's as easy as ticking a box to enable physics for each of our game objects.
I recommend you have a read of [Apple's Physics Documentation](https://developer.apple.com/documentation/spritekit#2242739) as physics plays a key role in many games, a game may not even appear to be physics based yet will often use physics for collision detection as this on its own is a powerful feature.

## Make the ground static

> [action]
> Open `GameScene.sks` and select the `ground` node, ensure the *Attributes inspector* is open and scroll down until you see the *Physics Definition* option.
> Set the *Body Type* to `Bounding rectangle`, which will present you will the additional physics properties.
> Set the body to be `static` by unchecking `dynamic`, there is no need for it to rotation so uncheck `Allows Rotation`, there is also no need for it to be affected by gravity, so deselect `Affected By Gravity`.
>
> ![Create the static ground physics body](../Tutorial-Images/xcode_ground_physics.png)
>

## Enable bunny physics

> [action]
> Open `Hero.sks` and select the `Bunny` sprite. Find the physics definition section and Set *Body Type* to `Bounding circle`.
> You should notice a faint circle around the bunny to show the physics body.
> Next check the following boxes *Dynamic*, *Allow Rotation* and *Affected By Gravity*. (By default they should all be checked).
>
> Set *Friction* to `0`. This will prevent the Bunny from sliding along the ground, this will help as the tutorial progresses.
>
> ![Enabling bunny physics](../Tutorial-Images/xcode_hero_physics.png)
>

<!--  -->

> [info]
> You might wonder why we only used a circle for our bunny physics definition.  When it comes to physics, less is always more, physics can be intensive on mobile devices and you want to simplify life as much as possible for the physics engine.
> Circles provide the best performance and if you can get away with just a circle then use it, the trick is using the most efficient shape for the job at hand.
>

## Adding the bunny to the world

> [action]
> To add the bunny to the game, drag the `Hero.sks` file into the scene. This will automatically create a *Reference node*  pointing to the `Hero.sks`
>
> ![Enabling bunny physics](../Tutorial-Images/xcode_add_reference_node_hero.png)
>
> Set the position to `(80, 280)`.
>

<!--  -->

> [info]
> Often *Reference nodes* are not displayed properly when initially placed into a scene, a quick *Save* of the scene should rectify this.

## Gravity

If you click outside of our *GameScene* white box and check the *Attributes inspector* you will see our physics world will default to approximate Earth's gravity `-9.8`.
![GameScene Gravity](../Tutorial-Images/xcode_gamescene_gravity.png)

> [info]
> Also notice the *Debug Drawing* options in the inspector, the *Show Physics Boundaries* is handy to check that your physics is where you think it should be. This creates the faint blue outlines.

## Adding the crystals

> [action]
> Let's add some pretty crystals above the ground to complete the visual appeal of *Hoppy Bunny Swift* by dragging `bg_crystals.png` into the scene from the Media Library:
>
> ![Adding crystals](../Tutorial-Images/xcode_add_crystals.png)
>
> Snap it top the top of *ground* by setting the *Position* to `(160, 155)`.


# Check your progress

Let's check that gravity is running correctly, SpriteKit Scene editor allows you to check this without having to run the game. Select `Animate` in `GameScene.sks` as you did before in `Hero.sks`:

**You should see the animated hero succumb to the gravity and fall to the ground.** If it doesn't please go back and double check your work so far :]

> [action]
> Before you hit that `Run`, you need to clear out the default project template code.
> Open `GameScene.swift` and replace with the following:
>
```
import SpriteKit
import GameplayKit
>
class GameScene: SKScene {
    override func didMove(to view: SKView) {
        /* Setup your scene here */
    }
>
    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        /* Called when a touch begins */
    }
>
    override func update(_ currentTime: TimeInterval) {
        /* Called before each frame is rendered */
    }
}
```
>

##Action
Now it's time to hit `Run` and see your game running in action.

![Run Project](../Tutorial-Images/xcode-simulator-11.png)

#Z Position

Argghh, it looks weird, the bunny is behind the crystals!

![Z Position issues](../Tutorial-Images/simulator_zorder_before.png)

In SpriteKit there is no implied object rendering order, so all objects are rendered by default at a *Z-Position* of `0`.
So if your bunny is at the same position as the crystals, you will have unpredictable rendering results.

*Wait, so what is Z Position?*

Z-Position or Z-Order defines the render ordering for overlapping 2d objects.

![Z Position Example](../Tutorial-Images/zorder.png)

Rectangle B is drawn after rectangle A. The result is rectB is drawn “above” rectA. RectB is said to have higher *Z-Position* than rectA.

You can easily set the *Z-Position* of your sprites in the *Attributes inspector*:

![Modify Z Position](../Tutorial-Images/xcode_zorder_modify.png)

> [action]
> Keep it logical, imagine you are painting a scene, work from the back to the front. Set the z position of the `crystals` and `ground` to `0`. Set the `clouds` to z position `1`. Last put our `bunny` on top of everything with a value of `2`.
>
> **Run the project again and it should look perfect now.**
>
> ![Z Position Fixed](../Tutorial-Images/xcode_zorder_fixed.png)

# Summary

It's coming along nicely now, so what did you learn?

- Added basic physics to the game
- Learned how to use a reference node
- Used **Z-Position** to layer your sprites
- Finally got to run the game

Next chapter you will be adding player controls to the hero.
