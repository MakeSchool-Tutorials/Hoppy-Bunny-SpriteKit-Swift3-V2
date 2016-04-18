---
title: "What you have learned"
slug: what-you-learned
---

Congrats again on finishing *Hoppy Bunny* and building your first iPhone game!

At this point you have been introduced to many concepts in iOS game development. Most of these concepts will be reviewed and further explained in later tutorials so you'll get a chance to revisit them later :)

Let's take a look at what you have learned so far.

![The game](../cover.png)

At the beginning of the Hoppy Bunny tutorials you learned how to create a new SpriteKit game project in Xcode.

##Setting Up the Gameplay Scene

- **Importing assets**: You can drag assets directly into the `Assets.xcassets` folder in the *Project Navigator*.

- **Setting the scene**: Adding assets to build the game scene and setting the *Z-Position* to ensure the correct draw order.

- **Creating a new SKS**: SpriteKit Scene files or SKSs can be created to contain custom scene objects.

- **Sprite frame action animations**: You can create sprite frame animations in the Timeline, using *SKActions* such as *AnimateWithTextures*.

##Letting the Bunny Fall

- **Static physics bodies**: Static physics bodies never move. They are great for ground and obstacles.

- **Dynamic physics bodies**: Dynamic physics bodies can be affected by gravity and other forces.

- **SKS Reference Nodes**: SKS files can be added to other SKS files via reference nodes. This will allow you to reuse game elements.

##Adding Controls and Tuning Physics

- **Gravity property**: The gravitational constant of the physics engine can be set through the attributes panel for the Scene.

- **Class code connections**: Class code connections can be used to set a custom class for a node, like `MSButtonNode`

- **Variable Code connections**: Code connections allow you to access SpriteKit Scene objects in code. They are created in the Scene Editor and completed in the *Scenes* class file using the format `var connectionName: ConnectionType!`.

- **Touch input**: Touches can be received by a node if you set `userInteractionEnabled` to `true` and override `touchBegan`.

- **Update loop**: Update loops are called between every frame. They can be created by overriding `update`.

- **Impulses**: `applyImpulse` adds directly to the velocity property of a physics body. `applyAngularImpulse` adds directly to the angular velocity property of a physics body.

##Scrolling the World

- **Implementing a conveyor belt**: You implemented a conveyor belt system by moving *Scrolling Layer* nodes with child objects attached such as Obstacles and ground.

- **Looping elements**: The ground was looped once it went off screen. You added a second ground image so that at least one full ground was always visible.

##Adding Obstacles

- **Endless generation**: You generated obstacles using a timer so that there was one always waiting just off screen. Once an obstacle left the screen, you removed it.

- **Random placement**: When you generated an obstacle, you randomized it's y-position value.

##Setting Up Collisions

- **Physics sensors**: Physics sensors detect and trigger collision events but do you physically affect the collisions. It's as if the physics bodies can pass through other physics bodies. These are useful for trigger events.

- **Contact delegate**: You implement a contact delegate so your class can receive collision events from the physics engine.

- **Game state**: It is useful to have a game state to manage the game e.g Active or Game Over

##Implementing Scoring

- **Goals using physics sensor**: Physics sensor goals were placed between obstacles so you can use the `didBeginContact` delegate method to detect when a player passed an obstacle.

- **Updating a label**: Converting numerical points scoring to a string for display via a label.

##Solution

[Download Sushi Neko](https://github.com/MakeSchool-Tutorials/Hoppy-Bunny-SpriteKit-Swift-Solution).

[GitHub](https://static.makegameswith.us/gamernews_images/TVZ2mTmQpl/labtocat.png)
