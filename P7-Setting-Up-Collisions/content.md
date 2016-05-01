---
title: Setting up collisions
slug: setting-up-collisions
---

You are going to set up collision handling so that your game finally becomes as frustrating as *Flappy Bird*. Any good game needs to be unforgivingly savage and frustrating, right?

I would recommend you have a look at Apple's documentation on the subject of [Working with Collisions and Contacts.](https://developer.apple.com/library/ios/documentation/GraphicsAnimation/Conceptual/SpriteKit_PG/Physics/Physics.html#//apple_ref/doc/uid/TP40013043-CH6-SW14) It can be a little bit confusing when you first start, so don't worry if you don't understand everything at once.

In the setup of collisions you are going to use the *Scene Editor* as much as possible, in later tutorials you will expand this knowledge implementing physics setup in code.

#Obstacle physics

The current obstacle has no physics bodies, let's fix that.

> [action]
> Open *Obstacle.sks*, make the following changes to both **carrots** and the invisible **goal** section.
> Enable physics by setting the *Body Type* to `Bounding rectangle` and uncheck the subsequent 4 boxes.
>
> ![Carrot physics](../Tutorial-Images/xcode_spritekit_obstacle_physics_collision_properties.png)
>
> Set the *Category Mask* to `2` and the *Contact Mask* to `1`
>
> One little tweak for the invisible goal sprite, set the *Category Mask* to `8`.
>

#Physics Categories

Every physics body in a scene can be assigned up to 32 different categories, each corresponding to a bit in a 32 bit mask.
You notice those really big numbers, they are the integer value of `2` to the power `32` which represents every bit in the 32 bit mask being 1, this also means that this body will collide with **every** other body and is the default behavior.

Think about separating your *Categories* into logical groups, for example:

- 1 - Player
- 2 - Obstacle
- 4 - Ground
- 8 - Goal Sensor

The *Contact Mask* allows you to define which physics bodies you want to be informed of when a collision takes place.  This would be useful when the bunny hits a carrot, you don't want the bunny to bounce off the carrot, you want the bunny to die at this point and fall from the sky.  You are setting the *Contact Mask* to `1` so the SpriteKit physics engine will inform you of this.

The **goal** is a slightly different case, you want to be informed when the bunny has entered into the goal zone so you can increase the players score.  However, you don't want the bunny to physically collide, as you want the bunny to pass through as if nothing is there.  You want to behave like a *Sensor*, a type of physics body that is used only for contact detection without physically affecting the body. This will be covered in more detail shortly.

#Bunny physics

> [action]
> Open *Hero.sks* and take a `click` on the bunny.
> Set *Category Mask* to `1`, *Collision Mask* to `7` and the *Contact Mask* to `4294967295` this is 2^32.
>
> ![Bunny physics](../Tutorial-Images/xcode_spritekit_bunny_physics_properties.png)
>


The *Collision Mask* is set to `7` as you only want the bunny to physically collide with *Categories* `1+2+4` e.g. `Player,Obstacle,Ground`.  You don't want to collide with `8` which is the goal sensor, otherwise the bunny will never be able to pass through the first obstacle.  
The *Contact Mask* has been set to 2^32 the max value and lets the physics engine know that you want to be informed if our bunny contacts any other physics body.

#Ground physics

You need to setup the ground sprite physics, do you think you can tackle this yourself?
Check back if you don't remember the *Category Mask* value we decided to use.  What value do you think you'll need for the *Contact Mask?*

> [solution]
> Open  *GameScene.sks* and modify both **ground** sprites.
> Set *Category Mask* to `4` and *Contact Mask* to `1`, you want to be informed if the bunny has hit the ground.
>
> ![Ground physics](../Tutorial-Images/xcode_spritekit_ground_physics_properties.png)
>

Run your game... The bunny will now collide with the obstacles yet thankfully be able to flap through the goal gap.  Well if you're good enough :]

#Physics Contact Delegate

If the bunny collides with the ground, an obstacle or passes through the goal of an obstacle, you want to know about.  Next you will implement the *Physics Contact Delegate* so your code will be informed whenever one of these collision contacts takes place.

> [action]
> Open *GameScene.swift*, you need to declare that the *GameScene* class will implement the *SKPhysicsContactDelegate* protocol methods.
> To learn more about *Protocols* and *Delegates* please check out our [Swift Concepts Guide](https://www.makeschool.com/tutorials/swift-concepts-explained).
>
> You declare that a class is implementing this protocol in Swift by appending *CKPhysicsContactDelegate* after the class' super class *SKScene*, separated by a comma, as shown:
>
```
class GameScene: SKScene, SKPhysicsContactDelegate {
```
>

##Delegate Support

The *GameScene* class is now ready to implement the contact delegate, first you should inform the delegate which class will take responsibility for handling the messages.   You should assign *GameScene* as the collision delegate.

> [action]
> Add the following code to the `didMoveToView(..)` method:
>
```
/* Set physics contact delegate */
physicsWorld.contactDelegate = self
```

Finally, you can implement the *didBeginContact* method that will be called whenever a collision takes place that you want to know about e.g. The ones with a *contactMask* of `1`.

> [action]
> Add this new method to the *GameScene* class:
>
```
func didBeginContact(contact: SKPhysicsContact) {
  /* Hero touches anything, game over */
  print("TODO: Add contact code")
}
```
>

Run the game... Any time you collide with the ground, a carrot or a goal sensor the *TODO* message will be logged to the console.

#Game over

Instead of simply showing a message in the console, it would be nice to think about the game over scenario.

This might consist of:

- The bunny falling to ground
- The game Scene shakes
- A restart game button

##Adding a button

There is no easy way to add a button in SpriteKit so you will need to get creative and create our own solution.  Only joking, we've kindly provided a starting point for you with a custom class called *MSButtonNode*.

> [action]
> ![Download MSButtonNode.swift](https://github.com/MakeSchool-Tutorials/Hoppy-Bunny-SpriteKit-Swift/raw/master/MSButtonNode.swift) and drag this file into your project.

<!-- -->

> [action]
> Add the *restart_button.png* to your scene.
> Set the *Name* to `buttonRestart`, set the *Z Position* to `10`, you want to ensure this UI (User Interface) element sits on top of everything visually.
>
> ![Restart button properties](../Tutorial-Images/xcode_spritekit_restart_properties.png)
>
> To turn this sprite into a custom button, you need to change the class to be an instance of `MSButtonNode` instead of `SKSpriteNode`, you can use the *Custom class* panel to change this by setting the *Custom Class* to `MSButtonNode`
>
> ![Restart button custom class](../Tutorial-Images/xcode_spritekit_restart_custom_class.png)
>

Can you setup a code connection for this button?

> [solution]
> Open *GameScene.swift*, add a property for the button to the *GameScene* class:
>
```
/* UI Connections */
var buttonRestart: MSButtonNode!
```
>
> When you connect this node you need to ensure the node is downcast to the `MSButtonNode` class.
> Add the following to the `didMoveToView(..)` method.
>
```
/* Set UI connections */
buttonRestart = self.childNodeWithName("buttonRestart") as! MSButtonNode
```
>

##Selection handler

The code connection is ready, if you run the game you can touch the button, it looks like it was touched yet nothing happens.  You need to add some code to be executed upon user touch.

> [action]
> Add the following code after the code connection:
>
```
/* Setup restart button selection handler */
buttonRestart.selectedHandler = {
>
  /* Grab reference to our SpriteKit view */
  let skView = self.view as SKView!
>
  /* Load Game scene */
  let scene = GameScene(fileNamed:"GameScene") as GameScene!
>
  /* Ensure correct aspect mode */
  scene.scaleMode = .AspectFill
>
  /* Restart game scene */
  skView.presentScene(scene)
>
}
```
>

This code loads in a fresh copy of the *GameScene.sks*, ensures the correct *scaleMode* is applied and then replaces the current scene with this fresh *GameScene*. You can find this code in `GameViewController.swift` and how the *GameScene* is initially loaded when the game starts.

##Hide the button

Great you have a button, as it's bang in the middle of the screen it might be an idea to hide it once the game is in-play.

> [action]
> Add the following code after the selection handler setup.
>
```
/* Hide restart button */
buttonRestart.state = .MSButtonNodeStateHidden
```
>

You want the button to be visible when the bunny dies, let's look at how we implement our game over scenario.
It would be really useful to know the current state of the game.  Has the game started, is the player dead e.t.c ?

#Game State

State management is a great way to do this, just look intp the `MSButtonNode` code above.  A `state` property is used to track if the button is `Active,Hidden or Selected`.

For the *GameScene* class it would be great to know if the game state is either `Active` or `GameOver`.  

When this `GameOver` state applies you want to:

- Kill the bunny
- Stop the world scrolling
- Show the restart button
- Ignore any touch other than the button

An *Enumeration* is a great way to setup a custom state type.

> [action]
> Add the following `Enumeration` to the top of *GameScene.swift*:
>
```
enum GameSceneState {
    case Active, GameOver
}
```
>
> To track the state you need to add a `gameState` property to the *GameScene* class.
> Set the default to `Active`
>
```
/* Game management */
var gameState: GameSceneState = .Active
```
>

#Bunny death

Great you now have some rudimentary game management in place, time to kill the bunny!

> [action]
> Replace the `didBeginContact(...)` method as shown:
>
```
func didBeginContact(contact: SKPhysicsContact) {
  /* Hero touches anything, game over */
>
  /* Ensure only called while game running */
  if gameState != .GameSceneStateActive { return }
>
  /* Change game state to game over */
  gameState = .GameSceneStateGameOver
>
  /* Stop any new angular velocity being applied */
  hero.physicsBody?.allowsRotation = false
>
  /* Reset angular velocity */
  hero.physicsBody?.angularVelocity = 0
>
  /* Stop hero flapping animation */
  hero.removeAllActions()
>
  /* Show restart button */
  buttonRestart.state = .MSButtonNodeStateActive
}
```

Notice the check of the **gameState** to ensure that the code will not be called more than once, when the player has died.  The bunnies physics are effectively disabled by stopping `rotation`, reseting `angularVelocity` and removing the flapping asprite frame animation with the use of `removeAllActions()` method.  The button is then activated and presented to the player  with a simple `MSButtonNodeStateActive` state change.

Run the game... When the player dies the button should appear and you can restart play.  

#Shutting down the world

It's not perfect yet as the bunny will still respond every so slightly to touch and the world will continue to scroll by.

To disable scrolling and touch, you can once again make use of the *gameState* property.

> [action]
> Add the following to the very top of the `update(...)` method:
>
```
/* Skip game update if game no longer active */
if gameState != .GameSceneStateActive { return }
```
>

Can you figure out how to disable touch?

> [solution]
> Add the following to the top of the `touchesBegan(...)` method:
>
```
/* Disable touch if game state is not active */
if gameState != .GameSceneStateActive { return }
```

Run the game... Death truly should be final for our bunny.

#Death actions

It would look better if the bunny fell face first upon hitting an obstacle.  A powerful way to do achieve this is using *SKActions*, you've already used actions to setup the the flappy animation frames.

> [action]
> Add the following code after you stopped the hero's actions with the `removeAllActions()` method in `didBeginContact(...)`:
>
```
/* Create our hero death action */
let heroDeath = SKAction.runBlock({
>
    /* Put our hero face down in the dirt */
    self.hero.zRotation = CGFloat(-90).degreesToRadians()
})
>
/* Run action */
hero.runAction(heroDeath)
```
>

The `runBlock` action lets you define your own custom action and in this case, manually rotate the bunny face down. You need to wrap this in an action to ensure it is executed at the correct **step** in the **rendering loop**.  You could also achieve this with *overriding* the `didSimulatePhysics` step and applying this rotation.  However, it's kind of awkward to do and cleaner to wrap in an *SKAction*.

Run the game... The bunny should be face down now upon any collision. It's all about those little bits of polish :]

#Shake it

It would be nice to add an old school style Star Trek camera shake to emphasize the impact.  This time you will create your own *GameEffects.sks* **SpriteKit Action file**, this enables you to store multiple effects that can be reused on any node.


> [action]
> Create a new *SpriteKit Action* file called `GameEffects`:
>
> ![Create New Action file](../Tutorial-Images/xcode_create_skaction.png)
>
> ![Add SpriteKit Action file GameEffects](../Tutorial-Images/xcode_create_skaction_file.png)
>
> Add your first *Action*, name it `Shake`
> ![Add New Action](../Tutorial-Images/xcode_spritekit_add_new_action.png)
>
> Now you have an empty action timeline ready for some actions, drag across the *Move action* from the *Object Library*.  Set the *Duration* to `0.2` seconds.
>
> ![Add Move Action](../Tutorial-Images/xcode_spritekit_action_add_move.png)
>
> **Sadly it does not yet seem possible (As of Xcode 7.2.1) to preview this action on the scene from within the scene editor :[**
>
> Copy and paste this action two times and then modify all three actions as follows.
>
> Set *Timing Function* to `Ease In`, set *Offset* to `(8,2)`
> Set *Timing Function* to  `Ease Out`, set *Offset* to `(-4,-2)`
> Set *Timing Function* to `Ease Out`, set *Offset* to `(4,2)`
>

##Shake all the nodes

Time to try this out in our code, you don't need to worry about loading the file itself, SpriteKit will automatically load any SpriteKit related resources and cache them at runtime :]

> [action]
> Open *GameScene.swift* and add the following code after the death action.
>
```
/* Load the shake action resource */
let shakeScene:SKAction = SKAction.init(named: "Shake")!
>  
/* Loop through all nodes  */
for node in self.children {
>      
    /* Apply effect each ground node */
    node.runAction(shakeScene)
}
```
> The effect can not be applied directly to the *GameScene*, so you need to loop through all the child nodes in the
scene and apply them individually.  Thankfully it is straight forward to do so.

Run the game...  When the bunny dies the screen should give a short shake.

> [info]
> I encourage you to make this effect as crazy as you like, experimentation is the best way to learn what works.  Often it's the happy little accidents lead you onto something awesome.

#Physics tweaking

You may have noticed the game is a little difficult, perhaps too difficult.  It feels like the bunny falls too hard initially and applying the touch impulse doesn't feel quite right.

> [action]
> Open *Hero.sks*, click on the bunny and navigate down to the physics properties, notice the *Initial Velocity* property.  Set this to `(0,400)`.  This should give the player a much need reaction time cushion when the game first runs.
> ![Bunny Physics Tweaks](../Tutorial-Images/xcode_spritekit_bunny_physics_tweaks.png)
>

When the bunny is falling and the player touches the screen, the touch feels a little sluggish.  This is due to the cumulative downward velocity generated by the bunny's fall.  If you reset the vertical velocity at the point of touch this might make it feel more responsive.

> [action]
> Open *GameScene.swift*, add the following in the `touchesBegan(...)` method after the `gameState` check:
>
```
/* Reset velocity, helps improve response against cumulative falling velocity */
hero.physicsBody?.velocity = CGVectorMake(0, 0)
```
>

Run the game... That little change has made the core mechanic feel much more satisfying :]

> [info]
> Bonus tip for making it so far:  You've added a lot of code and your formatting may be getting a little, well ugly.  
> Thankfully there is an easy way to tidy up your code with *Re-Indent*
> Open *GameScene.swift* then select all your code with *Cmd+a*, then press *Ctrl+i* to Re-Indent.
>

#Summary

Wow, a lot of ground has been covered in this chapter:

- Understanding the principles of SpriteKit physics collision and contact masking
- Implementing the `SKPhysicsContactDelegate` so you are informed of collision conacts.
- Creating your own custom button class
- Implementing a simple game state manager
- Running a custom *SKAction* and creating reusable *SKActions* visually
- Tweaking core mechanics, making the gameplay feel just right.

Next up, it wouldn't be a game without a scoring mechanism for the player.
