---
title: "What you have learned"
slug: what-you-learned
---

Congrats again on finishing *Hoppy Bunny* and building your first iPhone game!

At this point you have been introduced to many concepts in iOS game development. Most of these concepts will be reviewed and further explained in later tutorials so you'll get a chance to revisit them later :)

Let's take a look at what you have learned so far.

![The game](../cover.png)

###Creating a New Project

At the beginning of the Hoppy Bunny tutorials you learned how to create a new SpriteBuilder project and set it up with Cocos2D.

###Setting Up the Gameplay Scene

* **Importing assets**: You can drag assets directly into the resources pane on the left panel of SpriteBuilder.

* **Changing device orientation**: Device orientation for a project can be set in SpriteBuilder's project settings.

* **Setting up a background**: Backgrounds should be positioned relative to an edge (the edge you choose depends on the asset) and the anchor point should be set to the same edge as the asset is positioned to.

* **Creating a new CCB**: Interface files or CCBs can be created to contain custom objects based on CCNode and its subclasses.

* **Sprite frame animations**: You can animate CCSprites by setting keyframes to change the sprite frame at set times on the animation timeline. Chain a timeline to itself to repeat the animation endlessly.

###Letting the Bunny Fall

* **Static physics bodies**: Static physics bodies never move. They are great for ground and obstacles.

* **Dynamic physics bodies**: Dynamic physics bodies can be affected by gravity and other forces.

* **SKS Reference Nodes**: SKS files can be added to other SKS files via reference nodes. This will allow you to reuse game elements.

###Adding Controls and Tuning Physics

* **Gravity property**: The gravitational constant of the physics engine can be set through the attributes panel for the Scene.

* **Class code connections**: Class code connections can be used to set a custom class for a node, like `MSButtonNode`

* **Variable Code connections**: Code connections allow you to access SpriteKit Scene objects in code. They are created in the Scene Editor and completed in the *Scenes* class file using the format `var connectionName: ConnectionType!`.

* **Touch input**: Touches can be received by a node if you set `userInteractionEnabled` to `true` and override `touchBegan`.

* **Update loop**: Update loops are called between every frame. They can be created by overriding `update`.

* **Impulses**: `applyImpulse` adds directly to the velocity property of a physics body. `applyAngularImpulse` adds directly to the angular velocity property of a physics body.

###Scrolling the World

* **Implementing a conveyor belt**: We implemented a conveyor belt system by moving *Scrolling Layer* nodes with our child objects attached such as Obstacles and ground.

* **Looping elements**: The ground was looped once it went off screen. We added a second ground image so that at least one full ground was always visible.

###Adding Obstacles

* **Endless generation**: We generated enough obstacles so that there was one waiting just off screen. Once one left the screen behind the bunny, we removed it and added a new one off screen.

* **Random placement**: When we generated an obstacle, we randomized it's y-position value. This worked because the obstacles asset was larger than the screen height (so we part of it was always off screen).

* **Controlling draw order**: You can control the placement of objects added in code by modifying the *Z Position* value. The node's draw order controls the objects draw order.

###Setting Up Collisions

* **Physics sensors**: Physics sensors detect and trigger collision events but do you resolve the collisions. It's as if the physics bodies can pass through other physics bodies. These are useful for trigger events.

* **Contact delegate**: You implement a contact delegate so your class can receive collision events from the physics engine.

* **Game over**: It is useful to have a game over state or boolean to stop the game loop and ignore touches after a game over.

###Implementing Points

* **Goals using physics sensor**: Physics sensor goals were placed between obstacles so you can use a collision begin handler to detect when a player passed an obstacle.

* **Updating a label**: Converting numerical points scoring to a string for display via a label.

###Solution

The solution to this [tutorial is available on GitHub](https://github.com/MakeSchool/Hoppy-Bunny-SpriteKit-Swift).

![Github lab cat](../Tutorial-Images/labtocat.png)
