---
title: Implementing points
slug: implementing-points
---

Now that the player can die, you should implement the very last step: scoring points.

#Adding the score label

> [action]
> Drag a label object into the *GameScene.sks*, change the *Name* to `scoreLabel` and change the font to something you like and will be easy for the player to read. I went for `Helvetica Neue, Bold, 72`. Set the *Z Position* to `10` we want to ensure it's always in the foreground.
> ![Add label](../Tutorial-Images/xcode_spritekit_add_score_label.png)
>
> Position it somewhere clear and easy to read like near top of the screen.
>

<!-- -->

> [info]
> If you are having difficulty moving the *scoreLabel* or just want finer control over node placement in general here is a nice tip:
> You can use the *Arrow Keys* to move any node a pixel at a time or hold *Shift + Arrow Keys* to move in a bigger step.
>

Can you add a code connection in *GameScene.swift* for `scoreLabel`?

> [solution]
> First you need to add a property for the scoreLabel, let's call it `scoreLabel`:
>
```
var scoreLabel: SKLabelNode!
```
>
> Next use the `childNodeWithName(...)` method to find the object in the scene and connect. Remember the node type will be `SKLabel`.
> Add the following after the `buttonRestart` connection.
>
```
scoreLabel = self.childNodeWithName("scoreLabel") as! SKLabelNode
```

Great the connection has been made, if you did it yourself, fist bump the person nearest to you.

We will want the *scoreLabel* to show our game score.  However, as it stands there is no way to track this, let's add a score counter.

> [action]
> Ensure *GameScene.swift* is open and add a new property called `points` to the *GameScene* class as shown:
>
```
var points = 0
```
>

When the game starts we want to ensure the label is reset to the correct value of `0`, let's make that happen.


> [action]
> Add the following code to the bottom of the `didMoveToView(...)` method:
>
```
/* Reset Score label */
scoreLabel.text = String(points)
```
> *String(...)* is great for converting a number quickly into a string representation. We will be reusing this snippet when it comes to updating the score.

The next part takes a little bit of extra work, as it stands if the bunny collides with anything it will trigger our death sequence. So we need some way of knowing if this was a collision between the bunny and the goal. One way would be to compare the *categoryMask* remember this:

- 1 - Player
- 2 - Obstacle
- 4 - Ground
- 8 - Goal Sensor

However in this one we will use the *name* of the node.

> [action]
> Open *Obstacle.sks* and set the *Goal* sprite's *name* to `goal`
> Next open *GameScene.swift* and add this code to the start of the `didBeginContact(...)` method, before the `gameState` check.
>
```
/* Get references to bodies involved in collision */
let contactA:SKPhysicsBody = contact.bodyA
let contactB:SKPhysicsBody = contact.bodyB
>
/* Get references to the physics body parent nodes */
let nodeA = contactA.node!
let nodeB = contactB.node!
>
/* Did our hero pass through the 'goal'? */
if nodeA.name == "goal" || nodeB.name == "goal" {
>    
  /* Increment points */
  points += 1
>  
  /* Update score label */
  scoreLabel.text = String(points)
>  
  /* We can return now */
  return
}
```

When a collision takes place between two bodies the information is stored in a *SKPhysicsContact* object.  We can use this to find out more information about the collision, so first we grab a reference to the *SKPhysicsBodies*.  However, you may have a custom class with your own properties and need to access that, so we can go up a level and get a reference to the parent node of the body.
With the reference to the node we can check for the *Name* of `goal`. We can then update the players *points* and use that to update
our label.  Straight after that we *return* from the `didBeginContact(...)` method, otherwise the player will suffer a needless death.

Run the project... With a bit of skill you should be able to pass through the goal and get a point. You can always make the goal area bigger for testing ;)

Congratulations! Now you should see the complete game previewed at the beginning of this tutorial. You should have learned a lot along the way, especially regarding Swift and collision detection.
