https://arcade.makecode.com/beta#tutorial:github:comander227/shark-attack-part-2-custom-tutorial/Custom-Tutorial-FF-Part2


```template
namespace SpriteKind {
    export const Decoration = SpriteKind.create()
}
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim left`,
    200,
    true
    )
})
info.onCountdownEnd(function () {
    game.over(true)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim right`,
    200,
    true
    )
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy(effects.disintegrate, 100)
    info.changeScoreBy(1)
})
let myFood: Sprite = null
let myDecor: Sprite = null
let mySprite: Sprite = null
scene.setBackgroundColor(8)
scene.setBackgroundImage(assets.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(15)
for (let index = 0; index < 10; index++) {
    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)
    myDecor.setPosition(randint(0, 160), 96)
}
animation.runImageAnimation(
mySprite,
assets.animation`swim right`,
200,
true
)
game.onUpdateInterval(2100, function () {
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5, 115))
    myFood.vx = -75
})
```

# Feeding Frenzy Extra Credit

## Controlling the Lasers

**Now let's give the shark lasers!**
---

- :game: To make the shark fire a laser each time you press the (A) button, open the ``||controller:Controller||`` category and drag ``||controller:on [A] button [pressed]||`` container into an empty area of the workspace.

```blocks
// @highlight
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
})
```

## Adding the Lasers

- :paper plane: From ``||sprites:Sprites||`` drag ``||variables:set [projectile] to projectile [ ] from [mySprite] with vx [50] vy [50]||`` into the empty  ``||controller:on [A] button [pressed]||``.
- :mouse pointer: To send your lasers moving quickly toward the right side, change the ``||sprites:vx||`` (horizontal [__*velocity*__](#veloc "speed in a given direction")) value to **200**.
- :mouse pointer: Set the ``||sprites:vy||`` (vertical velocity) value to **0** so the lasers don't move up or down.

```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    // @highlight
    let projectile = sprites.createProjectileFromSprite(img``, mySprite, 200, 0)
})
```
## Assigning Our Laser Sprite 

**Set lasers to FUN!**
---

- :mouse pointer: Click on the gray square to open the image editor, then toggle to **My Assets** to choose the **laser** sprite.

```blocks
let mySprite: Sprite = null
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    // @highlight
    let projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
})
```

## Test Your Lasers

**🎮 Time to play with your laser shark 🎮**
---

Take a look at your game window and move your shark around while pressing the (A) button.  Are your lasers working?



## Give Me Something to Shoot

**🕓 Timing is everything 🕗**
---

- :circle: Let's add a container for code that will run every 2.5 seconds.
- :circle: From the  ``||game:Game||`` category, drag ``||game:on game update every [500] ms||`` into an empty area of the workspace.
- :mouse pointer: Click inside the text box and ignore the dropdown menu.  You'll want to use your keyboard to change **500** to **2500**.

```blocks
//@highlight
game.onUpdateInterval(2500, function () {
})
```

## Establishing Our Enemy
**Make some enemies**
---

- :paper plane: From ``||sprites:Sprites||``, drag ``||variables: set [mySprite2] to sprite [ ] of kind [Player]||`` into the empty ``||game:on game update every [2500] ms||`` container.
- :mouse pointer: To rename this to **myEnemy**, click **mySprite2** to open a dropdown menu and choose ``||variables:Rename variable...||``. Enter **myEnemy** and click **Ok**.
- :mouse pointer: Change the kind from **Player** to **Enemy**.

```blocks
game.onUpdateInterval(2500, function () {
// @highlight
    let myEnemy = sprites.create(img``, SpriteKind.Enemy)
})
```

## Assigning Our Enemy Sprite

- :mouse pointer: Click the gray box inside the ``||variables: set [myEnemy] to sprite [ ] of kind [Enemy]||`` block and toggle to **My Assets** to choose the **enemy** submarine, then click **Done**.

```blocks
game.onUpdateInterval(2500, function () {
// @highlight
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
})
```

## Setting the Spawn Point for Our Enemy

**Location, Location, Location!**

It's time to tell the new enemy sprites where to spawn.
---

- :paper plane: From ``||sprites:Sprites||``, drag a ``||sprites:set [mySprite] position to x [0] y [0]||`` block into **the end** of the ``||game:on game update every [2500] ms||``  container.

- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:myEnemy||``.

```blocks
game.onUpdateInterval(2500, function () {
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    //@highlight
    myEnemy.setPosition(0, 0)
})
```

## Positioning the Spawn Point

**Let's start all of the enemies at the furthest edge of the screen.**
(This means you'll need to set the **x** value to the full width of the screen.)
---

- :tree:From the ``||scene:Scene||`` category, drag ``||scene:screen width||`` into the **x** value of the ``||sprites:set [mySprite] position to x [0] y [0]||`` block.

```blocks
game.onUpdateInterval(2500, function () {
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    //@highlight
     myEnemy.setPosition(scene.screenWidth(), 0)
})
```


## Randomizing the Enemy Spawn Point

**Shake up the enemy**
Let's start the submarine at a random height to keep things interesting.
---

- :calculator: From ``||math:Math||`` grab  ``||math:pick random [0] to [10]||``  and snap it in to replace the **y** value of **0**.

- :mouse pointer: Change the random values to go from a min of **0** (the very top of the screen) to a max of **120** (the very bottom of the screen).

```blocks
game.onUpdateInterval(2500, function () {
let mySprite: Sprite = null
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    //@highlight
     myEnemy.setPosition(scene.screenWidth(), randint(0, 120))
})
```


## Making My Enemy Move

**Enemies on the move**
---

- :paper plane: Send your enemies after the shark by adding the ``||sprites:set [myEnemy] follow [mySprite]||`` block to **the end** of the ``||game:on game update every [2500] ms||`` container where ``||variables:myEnemy||`` is made.

- :mouse pointer: Click the plus sign (**+**) to the right of the ``||sprites:set [myEnemy] follow [mySprite]||`` block and set the enemy speed to **30** so it doesn't attack too fast.

```blocks
game.onUpdateInterval(2500, function () {
let mySprite: Sprite = null
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
     myEnemy.setPosition(scene.screenWidth(), randint(0, 120))
     // @highlight
    myEnemy.follow(mySprite, 30)
})
```


## Enemies Attack

**☠️On a dangerous path ☠️**
To subtract hitpoints when the enemy reaches the shark, we'll need a container to run code whenever the two overlap.
---

- :paper plane: From ``||sprites:Sprites||``, drag an ``||sprites:on [sprite] of kind [Player] overlaps [otherSprite] of kind [Player]||`` container into an empty area of the workspace.
- :mouse pointer: Change the second **kind** from **Player** to **Enemy**.


```blocks
//@highlight
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
})
```
## Destroy On Impact

To keep the submarine from attacking again and again, we need to destroy it before removing a life from the player.
---

- :paper plane: From ``||sprites:Sprites||``, drag ``||sprites:destroy [mySprite]||`` into the empty **on overlaps** container.

- :mouse pointer: Grab the ``||variables:otherSprite||`` value from the title of the **on overlaps** block and drag it in to replace ``||variables:mySprite||``.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    //@highlight
    otherSprite.destroy()
})
```


## Lose A Life


- :id card: From ``||info:Info||``, grab ``||info:change life by [-1]||`` and snap it below the ``||sprites:destroy [otherSprite]||`` block.

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    otherSprite.destroy()
    //@highlight
    info.changeLifeBy(-1)
})
```

## Shake Things Up

- :tree: For more fun, make the camera shake on impact by adding a ``||scene:camera shake by [4] pixels for [500] ms||`` block (from the ``||scene:Scene||`` category) beneath ``||info:change life by [-1]||``.

```blocks
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeLifeBy(-1)
    //@highlight
    scene.cameraShake(4, 500)
})
```

## Game Over on Life Zero
- :id card: Add an ``||info:on life zero||`` container to your workspace from the ``||info:info||`` category. 
- :circle: Add a ``||game:game over||`` block to the ``||info:on life zero||`` container. 
- :mouse pointer: Set the value to Lose and feel free to add an effect by clicking the + button.

```blocks
info.onLifeZero(function () {
    game.over(false)
})
```   

## Destroying Our Enemy
- :paper plane: Add another ``||sprites:on sprite of kind Player overlaps otherSprite of kind Player||`` container from the ``||sprites:Sprites||`` category. 
- :mouse pointer: Change the sprite kind from **Player** to **Projectile**.
- :mouse pointer: Change the otherSprite kind from **Player** to **Enemy**.

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
})
```

## Removing the Laser Sprite
- :paper plane: Add a ``||sprites: destroy mySprite||`` block from the ``||sprites:Sprites||`` category to the ``||sprites:on Overlap||`` container. 
- :mouse pointer: Replace ``||variables:mySprite||`` with the local ``||variables:sprite||`` variable.
- :mouse pointer: Open the effects (**+**) and set it to disintegrate. 
- :mouse pointer: Change the value from **500** to **100**.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
//@highlight
sprite.destroy(effects.disintegrate,100)
})
```

## Removing the Enemy Sprite
- :mouse pointer: **Right click** on the ``||sprites:destroy sprite||`` block and select **duplicate**.
- :mouse pointer: Add that block to the container.
- :mouse pointer: Replace ``||variables:sprite||`` with the local ``||variables:otherSprite||``.
- :mouse pointer: Add the same effect used for when the Enemy runs into the shark.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
sprite.destroy(effects.disintegrate,100)
//@highlight
otherSprite.destroy(effects.bubbles,100)
})
```

## Scoring Points
- :id card: Add an ``||info:change score by 1||`` block from the ``||info:Info||`` category to the container. 
- :mouse pointer: Change the value of **1** to **3**.

```blocks
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
sprite.destroy(effects.disintegrate,100)
otherSprite.destroy(effects.bubbles,100)
//@highlight
info.changeScoreBy(3)
})
```



## Spit It Out

**💥 Spitting Lasers Animation 💥**
The shark always spits lasers toward the right edge, so let's give it an appropriate animation!
---


- :sync: From ``||animation:Animation||``, drag ``||animation:animate [mySprite]||`` into **the bottom** of the existing ``||controller:on [A] button [pressed]||`` container that contains the code for the laser projectile.

- :mouse pointer: Click the gray box and toggle to **My Assets** to choose the **shooting shark** animation, then click **Done**.

```blocks
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
    //@highlight
    animation.runImageAnimation(
    myEnemy,
    assets.animation`shooting shark`,
    50,
    true
    )
})
```

## And On and On

**🔁 And do it AGAIN 🔁**

---

- :sync: The same animation block can be used to add a wiggle to your fish and bubbles to your sub!  Try it on your own!

- :mouse pointer: 💡 Just make sure to change ``||variables:mySprite||`` to ``||variables:myFood||`` or ``||variables:myEnemy||`` or things won't look quite right!

```blocks
game.onUpdateInterval(2500, function () {
    let myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    myEnemy.setPosition(scene.screenWidth(), randint(5, 115))
    myEnemy.follow(mySprite, 30)
    animation.runImageAnimation(
    myEnemy,
    assets.animation`animated enemy`,
    50,
    true
    )
})
game.onUpdateInterval(2100, function () {
    let myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5, 115))
    myFood.vx = -75
    animation.runImageAnimation(
    myFood,
    assets.animation`animated food`,
    200,
    true
    )
})
```

## Adding a PowerUp
**We are going to create a function to provide the chance for the subs to drop a PowerUp.**
---

- :chevron down: Open the Advanced section of the toolbox and click on the Function category.
- :function: Click on the ``||functions: Make A Function||`` button.
- :function: Name the Function PowerUp
- :function: Add a Sprite parameter to your function by clicking on the **sprite** button in the parameter list.
- :mouse pointer: Name it **ESprite**.

![Creating Functions](/static/lessons/block-out/creating-functions.gif)

```blocks
function PowerUp (ESprite:Sprite){
}
```

## Destroying the Enemy
- :paper plane: Add a ``||sprites:destroy mySprite||`` block from the ``||sprites:Sprites||`` category to the newly created function.
- :mouse pointer: Drag the local ``||variables:ESprite||`` variable and replace the ``||variables:mySprite||`` variable.
- :mouse pointer: Set the effects (**+**) to the same as what you have when the laser destroys the sub. 
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
function PowerUp (ESprite:Sprite){
//@highlight
ESprite.destroy(effects.bubbles,100)
}
```

## Setting Up the PowerUp Logic
- :random: Add an ``||logic:if then loop||`` from the ``||logic:Logic||`` category to your function under the ``||sprites:destroy ESprite||`` block.

```blocks
function PowerUp (ESprite:Sprite){
ESprite.destroy(effects.bubbles,100)
//@highlight
if (true){
}
}
```

## Setting Up the PowerUp Drop Chance
- :calculator: Add a ``||math: % chance||`` diamond from the ``||math:Math||`` category to the ``||logic:if then loop||``.
- :mouse pointer: Change the value from **0** to **25**.

```blocks
function PowerUp (ESprite:Sprite){
ESprite.destroy(effects.bubbles,100)
//@highlight
if (Math.percentChance(25)){
}
}
```

## Spawning Our Powerup
- :paper plane Add a ``||sprites:set mySprite [] of kind Player||`` block from the ``||sprites:Sprites||`` category.
- :mouse pointer Rename the sprite from ``||variables:mySprite||`` to ``||variables:myPowerup||`` by **right clicking** on the block and choosing the **Rename Variable** option.
- :mouse pointer: Set the **myPowerup** sprite to the kind of **Powerup** by clicking on the kind and selecting **create new**.

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}

function PowerUp (ESprite:Sprite){
ESprite.destroy(effects.bubbles,100)
if (Math.percentChance(25)){
//@highlight
let myPowerup = sprites.create(img``,SpriteKind.Powerup)
}
}
```

## Assigning Our PowerUp A Sprite
- :paint brush: Click on the gray sprite box. 
- :mouse pointer: Open up the **my Assets** tab.
- :mouse pointer: Click on the shark **fin** image. 

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}

function PowerUp (ESprite:Sprite){
ESprite.destroy(effects.bubbles,100)
if (Math.percentChance(25)){
//@highlight
let myPowerup = sprites.create(assets.image`fin`,SpriteKind.Powerup)
}
}
```

## Positioning Our Powerup Horizontally
- :paper plane: Add a ``||sprites:set mySprite x ()||`` blocks from the ``||sprites:Sprites||`` category into the ``||logic:if then container||``. 
- :bars:Change ``||variables:mySprite||`` to ``||variables:myPowerup||``.
- :paper plane: Grab a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category and place it over the value space.
- :mouse pointer: Drag the local ``||variables:ESprite||`` and replace ``||variables:mySprite||``.

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}


function PowerUp (ESprite: Sprite) {
    ESprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)) {
        let myPowerup = sprites.create(assets.image`fin`, SpriteKind.Powerup)
        //@highlight
        myPowerup.x = ESprite.x
    }
}
```

## Positioning our Powerup Vertically

- :mouse pointer: Right click on the ``||sprites:set myPowerup x||`` block and duplicate it.
- :mouse pointer: Add the duplicated block to your ``||logic:if then container||``.
- :mouse pointer: Change the **x** values to **y** values. 

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}



function PowerUp (ESprite: Sprite) {
    ESprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)) {
        let myPowerup = sprites.create(assets.image`fin`, SpriteKind.Powerup)
        myPowerup.x = ESprite.x
       //@highlight
        myPowerup.y = ESprite.y
    }
}
```

## Adding A vy Value to Our Powerup
- :paper plane: Grab another ``||sprites:set mySprite x ()||`` block from the ``||sprites:Sprites||`` category.
- :bars: Change ``||variables:mySprite||`` to ``||variables:myPowerup||``.
- :paper plane: Change ``||sprites:x||`` to ``||sprites:vy||``.
- :mouse pointer: Change the value **0** to **-25**.

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}



function PowerUp (ESprite: Sprite) {
    ESprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)) {
       let myPowerup = sprites.create(assets.image`fin`, SpriteKind.Powerup)
        myPowerup.x = ESprite.x
        myPowerup.y = ESprite.y
        //@highlight
        myPowerup.vy = -25
    }
}
```

## Replacing Outdated Code
- :mouse pointer: Find the ``||sprites:on Overlap||`` container for when your laser impacts the enemy sub.
- :mouse pointer: Delete the ``||sprites:destroy otherSprite||`` block.
- :mouse pointer: Add a ``||functions: Call Powerup||`` block. 
- :mouse pointer: Replace the ``||variables:mySprite||`` with the local ``||variables:otherSprite||`` variable.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}
function PowerUp (ESprite: Sprite) {
    ESprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)) {
       let myPowerup = sprites.create(assets.image`fin`, SpriteKind.Powerup)
        myPowerup.x = ESprite.x
        myPowerup.y = ESprite.y
    
        myPowerup.vy = -25
    }
}
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprite.destroy()
    info.changeScoreBy(3)
    //@highlight
    PowerUp(otherSprite)
})
```

## Making Our Powerup Do Something
- :paper plane: Drag a new ``||sprites:on Overlap||`` container from the ``||sprites:Sprites||`` category to the workspace.
- :mouse pointer: Change the second Sprite Kind from **Player** to **Powerup**.

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}
//@highlight
sprites.onOverlap(SpriteKind.Player, SpriteKind.Powerup, function (sprite, otherSprite) {
    
})
```

## Removing our PowerUp on Contact
- :paper plane: Add a ``||sprites:destroy mySprite||`` block from the ``||sprites:Sprites||`` category to the new ``||sprites:on Overlap||`` container.
- :mouse pointer: Drag the local ``||variables:otherSprite||`` to replace the ``||variables:mySprite||`` variable. 
- :mouse pointer: Feel free to change the destroy effect.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}

sprites.onOverlap(SpriteKind.Player, SpriteKind.Powerup, function (sprite, otherSprite) {
    //@highlight
    otherSprite.destroy(effects.bubbles, 100)  
})
```

## Adding Bonuses
- :id card: Add an ``||info:change life by -1||`` block from the ``||info:Info||`` category to the ``||sprites:on Overlap||`` container. 
- :mouse pointer: Change the value **-1** to **1**.
- :id card: Add an ``||info: change score by 1||`` block from the ``||info:Info||`` category to you ``||sprites:on Overlap||`` container.
- :mouse pointer: Change the value **1** to **5**.

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}

sprites.onOverlap(SpriteKind.Player, SpriteKind.Powerup, function (sprite, otherSprite) {
    otherSprite.destroy(effects.bubbles, 100)
    info.changeLifeBy(1)
    info.changeScoreBy(5)
})
```

## Resetting the Countdown
- :id card: Add a ``||info:start countdown 10 (s)||`` block from the ``||info:Info||`` category to the ``||sprites:on Overlap||`` container.
- :mouse pointer: Change the value of **10** to **15**

```blocks
namespace SpriteKind {
    export const Powerup = SpriteKind.create()
}

sprites.onOverlap(SpriteKind.Player, SpriteKind.Powerup, function (sprite, otherSprite) {
    otherSprite.destroy(effects.bubbles, 100)
    info.changeLifeBy(1)
    info.changeScoreBy(5)
    //@highlight
    info.startCountdown(15)
})
```


## Finale

**WOW!**
Look at the game you've created!  Make sure to give it a try in the game window before moving on.

---

When you're happy, click **Done** to complete the project and be able to share it with your friends.

```block
namespace SpriteKind {
    export const Decoration = SpriteKind.create()
    export const PowerUp = SpriteKind.create()
}
controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    animation.runImageAnimation(
    mySprite,
    assets.animation`shooting shark`,
    50,
    false
    )
    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
})
controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim left`,
    200,
    true
    )
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function (sprite, otherSprite) {
    otherSprite.destroy(effects.bubbles, 100)
    info.changeLifeBy(1)
    info.changeScoreBy(5)
    info.startCountdown(15)
})
info.onCountdownEnd(function () {
    game.over(true)
})
info.onLifeZero(function () {
    game.over(false)
})
controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim right`,
    200,
    true
    )
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {
    otherSprite.destroy(effects.disintegrate, 100)
    info.changeScoreBy(1)
})
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {
    sprite.destroy()
    info.changeScoreBy(3)
    Powerup(otherSprite)
})
function Powerup (mySprite: Sprite) {
    mySprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)) {
        myPowerup = sprites.create(assets.image`fin`, SpriteKind.PowerUp)
        myPowerup.x = mySprite.x
        myPowerup.y = mySprite.y
        myPowerup.vy = -25
    }
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {
    otherSprite.destroy()
    info.changeLifeBy(-1)
    scene.cameraShake(4, 500)
})
let myFood: Sprite = null
let myEnemy: Sprite = null
let myPowerup: Sprite = null
let projectile: Sprite = null
let myDecor: Sprite = null
let mySprite: Sprite = null
scene.setBackgroundColor(8)
scene.setBackgroundImage(assets.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(15)
for (let index = 0; index < 10; index++) {
    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)
    myDecor.setPosition(randint(0, 160), 96)
}
animation.runImageAnimation(
mySprite,
assets.animation`swim right`,
200,
true
)
game.onUpdateInterval(2500, function () {
    myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    myEnemy.setPosition(scene.screenWidth(), randint(0, 120))
    myEnemy.follow(mySprite, 30)
})
game.onUpdateInterval(2100, function () {
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5, 115))
    myFood.vx = -75
})
```



```assetjson
{
  "README.md": " ",
  "assets.json": "",
  "images.g.jres": "{\n    \"~I/xlSOb!:ehNE!zTIaq\": {\n        \"data\": \"hwQkABAAAAAAwAwAAAD/AADAyw8A//sAAMC7+/+8+wAAALy7zLsPAAAA3L3L+wAAAADA3bsPAAAAAAD8yw8AAAAAAPDMDwAAAAAA8MzMAAAAAADPzLwMAAAAAM/M3AwAAADwzMy8zQAAAPDMzMzNAAAA8MzMzN0M/wDPu8vM3f+//7+7u8z9+7/LvLu7y7/73Lu8y7y7u/3cvby8u7vb+8DNvMu8u7sPAMy8vLsR/AwA8Ly7ERERDAAAv/sfHBEMAAC/+x/MEQwAAL+7ERMcDAAAv7sRM/MAAAC/uxEc8wAAAL+7EcwPAAAA8Lsb/AAAAADwy7sPAAAAAAC/+wAAAAAAAP8PAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"shark\"\n    },\n    \"]uSp,Yb2U]iY\": {\n        \"data\": \"hwQQABAAAAAAAAAAAP8AAAAAAADMRA8AAAAAwERE9AAAAABMRET0AAAAwERERPQAAADcRERP1A8AzERBRERBD8DNRBQREUQPwM1ERExMRA/AzURETPRED8DNTUT0/8QMwN0cRERE3AwAzMwREf3bDAAAAMz0/8wAAAAAwEREDwAAAADA/P8PAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"food\"\n    },\n    \"?]c;BAWx@CPp7,Xc!||y\": {\n        \"data\": \"hwQQADAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGaIiAAAAAAAAAAAAAAAAAAAAAAAiAAAYFV3dwgAAAAAAAAAAAAAAAAAAAAAaAgAVmdmdocAAAAAAAAAAAAAAAAAAAAAgIaIZ1d3Z3YAAAAAAAAAAAAAAAAAAAAAAGhmdmWId2cAAAAAAAAAAAAAAAAAAAAAAIB2VYhoZogAAAAAAAAAAAAAAAAAAAAAAABghmZmhgAAAAAAAAAAAAAAAAAAAAAAAAAAAIiICAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"decoration\"\n    },\n    \"=NL1D;jj+wTeW(}r0(uZ\": {\n        \"data\": \"hwQMAAwAAAAAAAAFAAAAAAAAAAIAAAAAAAAAAAAAAAAAAFBSAAAAAAAAUFIAAAAAAABQUgAAAAAAAFBSAAAAAAAAUFIAAAAAAABQUgAAAAAAAFBSAAAAAAAAAAIAAAAAAAAAAAAAAAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"laser\"\n    },\n    \"Ik6joQcYX!hh)DS[|_?1\": {\n        \"data\": \"hwSgAHgAAAAAAAAAAAAAAADQCQ0AANAAAAAAAAAAAAAAAAAAALAAAAAAAAAAAPD/3d3N293d3d3d3bzc3d29u7u7u8sAAAAAAAAAAAAA3Q0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPD/3d3N293d3d3du9vd3d3d3d3dzbsAAADdAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/H93Ny93d3d3d3d3d3d3d3d3d3cwAAADZAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/3NHdu93d3d3d3d3d3d3d3d3d3c0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzNHdvdvd3d3d3d3d3d3d3d293c0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/zNHd3bvd3d3d3d3d3d3d3d29270AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzBzd3b3d3d3d3d3d3d3d3d3d270AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAzBzR3d3b3d3d3d3d3d3d3d3du70AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADAzMzR3d3L3d3d3d3d3d3d3d3dvb0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMwR3d3N3d3d3d3d293d3d3dvbsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzc0d3d3d3d3R3R3N3d3d3dzbsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzMHd3d3d3d3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzMHNHd3d3d3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzBHd3d3d3d3d3d3d3d3d3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzBzR3d3d3d3d3d3d3d3d3bwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMwR3d3d3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMwc0d3d3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMzMEd3d3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADLzMzMzMzMHdHd3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDMzMzMzMzM3BHd3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDMzMzMzMzMzBzR3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMwd3d3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMwcEd3d3d3d3d3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMy8G9Hd3d3d3d3dvbsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMzM+x3d3d3d3d3dvb8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMzMu9/R3d3d3d3dvbwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMDMzMzMzMzMzMzMvP8f0d3d3d3dvbwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzPvPEd3d3d3dvbwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzLzPHN3d3d3dvb8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzLzPzN3d3d3dy7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzLz/zNzd3d3dy7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMzMzMzMzMzMzMzMzLz/zPz93d3du78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMzMzMzMzMzMzMzMzMz/zMz/393d+7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMzMzMzMzMzMzMzMzMz7zMz839+9y7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMzMzMzMzMzMzMzMzMz8z8zM/9+9y78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMz8z8zM/N+9y7wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMy8z8zM/P+9y7wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMz8zM/Py9y7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzM/8zMzPy9+9sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzM/8zMzPy/u9sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMz8+8zMzPz/v90AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMz8+8zMzPzfv90AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzM+8zMzPzf/90AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzM+8zMzPzf/90AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzM/8zMzPzf/90AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzM+8/MzP/fvd8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzM+8/MzP/d3d8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzM+8/MzP/R3d8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMu8/MzP8c3d0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzM/8/M/P8c3f0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMv8zM/P8f3f0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMvMzMzP8f0f0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzMzMzMzP/P0f0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzMz8zMzP/PEf0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMz8zMzP//H/8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMvMzMzMzMzMzMzMzMzMz8zMzP////8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMvMzMzMzMzMzMzMzMzMz8zMzP////8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMvMzMzMzMzMzMzMzMzMz8zMzP///9wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALvMzMzMzMzMzMzMzMzMzMzMzP///9wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALzMzMzMzMzMzMzMzMzMzMzMzPz//9wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALDMzMzMzMzMzMzMzMzMz8zMzPz///0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALDLzMzMzMzMzMzMzMzMz8zMzPz///0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADLzMzMzMzMzMzMzMz8zMzMzPz///0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMzMzMzMzMz8zMzMzPz//9wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMzMzMzMzMz8zMzMzPz//9wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADLzMzMzMzMzMzMzMzPzMzMzPz//98AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAC7zMzMzMzMzMzMzPzPzMzMzPz//98AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwzMzMzMzMzMzMzPzMzMzMzPz//98AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwzMzMzMzMzMzMzPzMzMzMzPz//88AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwzMzMzMzMzMzMzPzMzMzMzPz//88AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAy8zMzMzMzMzMzM/MzMzMzMz//88AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzM/MzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMzMzMzMzMzM/M/MzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzM/MzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMvMzMzMzMzM/MzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMvMzMzMzMzM/8zMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADMzMzMzMzMz8zMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALDMzMzMzMz8zMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALDLzMzMzMz8zMzMzMzMzMz//78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADLzMzMzMzPzMzMzMzMzMz//78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAC7zMzMzMzPzMzMzMzMzMz//78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwzMzMzPzMzMzMzMzMzMz//78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwzMzM/MzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwy8z8/8zMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAy8z/zMzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAy//MzMzMzMzMzMzMzPz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP/MzMzMzMzMzMzMzPz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzPz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwz8zMzMzMzMzMzMzMzPz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzMzMzMzP////8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzMzMzMzMzMzMzMzP////8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDMzMzMzMzMzMzMzMzMzP////8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzMzMzPz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAM/MzMzMzMzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz///8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz///0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzPz///sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzPz///sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzPz///sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz/3/sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3QAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz/3/sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADQAA0AAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz/3/sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADQ2Q0AAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz/3/sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3QAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzMzMz/3/sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAwMzMzMzMzMzMzMzMzMzMzMz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzMz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzMz//78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8MzMzMzMzMzMzMzMzMzMzMz/v78AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzMz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzPz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzPz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzPz/v7sAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMzMzMzMzMzMzMzMzMzMzPz//70AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsMvMzMzMzMzMzMzMzMzMzPz//bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALvMzMzMzMzMzMzMzMzMzPz//bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAMvMzMzMzMzMzMzMzMzMzPzf/70AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAL/MzMzMzMzMzMzMzMzMzP//zf0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDLzMzMzMzMzMzMzMzMzP//3/8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDLzMzMzMzMzMzMzMzMzP/f3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDLzMzMzMzMzMzMzMzM/P/d3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPC/zMzMzMzMzMzMzMzM/P/d3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzMzMzMzMzMzMzM///d3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADPzMzMzMzMzMzMzMz8///d3b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzMzMz////f/b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzMzPz/393d/b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzMzP//39393b8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzM/P//393//70AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzM/P//3/3f3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMzM////3d3d3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzMz8///93d3d3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzMzP//39393d293b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzM/P/fvbz93d3b3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzM/9zdvNv93b3b3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMz8/93du9393b3d3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMz/3N29u93d3b3d3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzMzf3d27u93d3bzd3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzPzd3b37u93d3bvd3b0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzMzN/d3bvf293d3cvd3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwzMzM3N3du8zd3d3d3cvd3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwy8zM3d27y9zd3d3dvcvd3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwv8zP3d27zNzd3d3dvfzd3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAz8zc3d3L/Nzd3d3dvc/d3dsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAz/zd3b3LzN3d3d3dvczd3dsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAz9/d3bvMz93d3d3dvczd3dsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAz93dvcv8z93d3d3dy8/d3dsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3929u8z83N3d3d3du9zd3dsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADw3d27y8zM3d3dvd3dvdzdvdsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADf3b27zMzd3d3dvdzdu9zdvdsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADf3bu73d3d3d3du929y93d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPDdvbvb3d3d3d3dz9293N3d3bsAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAANDdvbvd3d3d3d3d/N293N3d3csAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAN/du9vd3bu73d3d/N3N3d3d3csAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8N3du9vd0cvLu7vMz93d3d3dvcsAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3QAAAAAAAAAAAAAAAAAAAAAA8N29u93d0d3dvczM3N3d3d3du98AAAAAAAAAAAAAAAAAAAAAAAAAAAAA2QAAAAAAAAAAAAAAAAAAAAAA0N29u93d0d3d3d3d3d3d3d29y98AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3929293d3d3d3d3d3d3d3d3LzN8AAAAAAAAAAAAA3Q0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA3d29293d3d3dvbvb3b3b3bvP/NwAAAAAAAAAAADQwA0AANAAAAAAAAAAAAAAAAAAALAAAAAAAAAAAAAA0d293d3d3d27u7u7u7u7u7vMz9w=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"ocean1\"\n    },\n    \"q=voYSOp1V?b{:\": {\n        \"data\": \"hwSgAHgAAAAAAAAAAAAAAACgamZqpmpmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamqqqGb2amaGYAAAAAAAAAAACgamZqZmpmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaqqKb2aqaGYAAAAAAAAAAACgamZqZmqmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamqqqKb2aKZmYAAAAAAAAAAAAAamZqZmqmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmqqaKb2aKZmYAAAAAAAAAAAAAqmZqZmqmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmqqqGb2aGZmYAAAAAAAAAAAAAqmZqZmqmZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmpqqKZmaGZmYAAAAAAAAAAAAAqmZqZmqmZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmpqqKZmaGZmYAAAAAAAAAAAAAoGqmZmqmZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmpqaKZmb6Zm8AAAAAAAAAAAAAoKqmZmqmZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZqqGb2b69m8AAAAAAAAAAAAAAKqmZqamZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmqK/2b69mYAAAAAAAAAAAAAAKCqZqamaqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZqqK9mb69mYAAAAAAAAAAAAAAACgqqZmaqZqZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZqaK+Gb69oYAAAAAAAAAAAAAAAAAqqpmamZqamamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZqaq+G//9oYAAAAAAAAAAAAAAAAAqqpqamZqamamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmaqaG+P9oYAAAAAAAAAAAAAAAAAAKqqamZqamamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmaqaG+P9oYAAAAAAAAAAAAAAAAAAKCqqmZqamamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmaqaG+P9oYAAAAAAAAAAAAAAAAAAACvqmZqpmamZmamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmaqaG+P9mgAAAAAAAAAAAAAAAAAAACgqmqqpmamZmqmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaG+P9mgAAAAAAAAAAAAAAAAAAAAAoKqqpmamZmqmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaG+P9mgAAAAAAAAAAAAAAAAAAAAAAKCqpmamZmqmamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaG+P9mgAAAAAAAAAAAAAAAAAAAAAAACqqmamZmpmamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaG+P9mYAAAAAAAAAAAAAAAAAAAAAAACgqmqmZmpmamZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmamaG+PhmYAAAAAAAAAAAAAAAAAAAAAAAAA8KqmZmpmamZmZmZmZmZmZmZmZmZmZmZqZmZmZmZmZmZmZmamaG+PhmYAAAAAAAAAAAAAAAAAAAAAAAAAAKqqaqZmamZmZmZmZmZmZmZmZmZmZqZqZmZmZmZmZmZmZmamaG+KiGYAAAAAAAAAAAAAAAAAAAAAAAAAAKCqaqZmpqZmamZmZmZmZmZmZmZmZqZmZmZmZmZmZmZmZmamaG+Kb2YAAAAAAAAAAAAAAAAAAAAAAAAAAACqaqZmpqZmamZmZmZmZmZmZmZmZqZmZmZmZmZmZmZmZmamaG+Kb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqqZmpqZmamZmZmZmamZmqmZmZqZmZmZmZmZmZmZmZmamaG+qb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoKpqpmZqqmZmZmZm+mZm+mZmZqZmZmZmZmZmZmZmZmam+G+mb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKpmpmZqpmZmZmZmamZmamZmZqZmZmZmZmZmZmZmZmam+mamb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCqpmpqpmZmZmZmamZmamZmZqZmZmZmZmZmZmZmZmZm+mamb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgampqpmamZmZmamZmamZmZqZmZmZmZmZmZmZmZmZmimaob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqmpqpmamZmpmamZmZmZmZqZmZmZmZmZmZmZmZmZmimaob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoGqqpmpmampmamZmZmZmZqZmZqZmZmZmZmZmZmZmimaIb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCqZmpmaqZmZmZmZmZmZqZmZqZmZmZmZmZmZmZmimaob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACqZmpmaqZmZmZmZmZmZqZmZqZmZmZmZmZmZmZmimaob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgampmaqZmZmZmZmZmZqZmZqZmZmZmZmZmZmZmimaob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAampmaqb2ZmZmZmZmZqZmZqZmZmZmZmZmZmZmimb4Zm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqqpmaqb2ZmZmamZmZqZmZqZmZmZmZmZmZmZmimb4Zm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8GpmpqZqZmZmamZmZqZmZqZmZmZmZmZmZmZmiob4Zo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKBmpmZqZmZmamZmZqZmZqZmZmZmZmZmZmZmiob6b48AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABqpmZqpmZmamZmZqZmZqZmZmZmZmZmZmZmioaKZo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgqmpqpmpmamZmZqZmZqZmZmZmZmZmZmZmioaKZo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqmZqZmpmamZmZqZvZqZmZmZmZmZmZmZmioaGZo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoGpqZvpmamZmZqZvZqZmZmZmZmZmZmZmqoaGZo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8KqqZvpmamZmZmZvZqZmZmZmZmZmZmZmpoaGZo8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCqampmZmZmZmZmZqZmZmZmZmZmZmZmpoaGZm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACvZqpmZmZmZmZmZqZmZmZmZmZmZmZmpoaKZm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAb6amZqZmZmZmZqZmZmZmZmZmZmZmpoaKZm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAr6amZqZmZmZmZqZmZmZmZmZmZmZmpvaKpm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoKqmaqZmZmZmZqZmZmZmZmZmZmZmpvaKpm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKpmaqZmZmZmZqZmZmZmZmZmZmZmpviKpm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKBqaqZmZmZmZqZmZmZmZmZmZmZmpviKpm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKCqaqZmZmZmZqZmZmZmZmZmZmZmpviKpm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwaqZmZmZmZqZmZmZmZmZmZmZmpviKhm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwaqZmZmZmZqZmZmZmZmZmZmZmpvj/pmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqqZmZmZmZqZmZmZmZmZmZmZmpoj/pmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAr6ZmZmZmZqZmZmZqZmZmZmZmpoj/pmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8GpqZqZmZqZmZmZqZmZmZmZmpoj/j2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGpqZqZmZqZmZmZqZmZmZmZmpoj/b4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKpqZqZmZqZmZmZqZmZmZmZmpoj4b4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKBqZqZmZqZmZmZqZmZqZmZmpoj4b4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPBqpqZmZqZvZmZqZmZqZmZmpoj4r4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCqpqZmZqZvZmZqZmZqZmZmpoj4r4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCvpqZmZmZqZmZqZmZqZmZmpoj4r4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACvpqZmZmZqZmZqZmZqZmZmhoj4r4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACvpqZmZmZqZmZqZmZqZmZmioj49oYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgpmpqZmZqZmZqZmZqZmZmioj49oYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwampqZmZqZmZqZmZqZmZmioj4poYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAampqZmZqZmZqZmZqZmZmioj4+oYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAqmpqZmZqZmZqZmZqZmamioj4+oYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAYGZqZmZqZmZqZmZqZmamhoaI+oYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoGqqZmZqZmZqZmZqZmamhoaI+mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGqmZmZqZmamZmb6Zmamho+I+mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGqmZmZqZmamZmb6Zmamho+I+mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKqmZqZqZmamZmb6Zmamhv+I+mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAK+mZqZqZmamZmamZmamhv9o9mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKCqpmZqZmamZmamZmamhv9o9mgAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPBqqmZqZmamZmamZmamhv9o9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPBqqmZqZmamZmamZmamhv9o9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPBqqmZqZmamZmamZmamhv9o9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACqpmpqZmamZmqmZmamhv9o9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/ZmqqZmamZmqmZmampv9oj2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgZmqmZmamZqamZmampv9oj2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwZmqmZmamZqamZmampv9ob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAZmqmZmamZqamZmamiv9ob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoGqmZmZmaqamZmaqav9ob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAoKqmamZmaqamZmb6av9ob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALoKpmamZmaqamZmb6av9ob2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAG9mampmaqamZmb6av+Ib2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAKpmaqpmaqamZmZqav+Pb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAKBqaqpmaqamZmaqaq+Ib2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACqaqpmaqZqaqaq+v+Ib28AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACvZqpmamZqaqZqav+IZm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACgaqZmamZqaqZqav+IZm8AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAq6amamZqaqZqaq+I9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsKamamZqaqZqaqiI9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAu29qampqaqZq9q+I9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAu29mampqaqZm+q+I9mYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABmampqaqZmaq+Ib2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAAAAAAAAACgaqZqaqpmaq+Ib2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwaqZqaqpm+q+Gb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADwqqZqamqm+q+Gb4YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8Gpqamqm/6+Gb2gAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwsAAAAAAA8Kqqamqm/6+Gj2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAAAAAAAKBmamqmb6+Gj2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAAAAAAAKBqaqqm/6+Gb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAC7AAAACqaqam9q+Gb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAsAAADwaqaq/6+Gb2YAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAsAAAD7aqZqiq+GZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAL/6b6/6iGZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/6qv/2r2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD6/2+Gr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP+v/2r2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAP/4+Gr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPD/j2r2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAAAAAAC7uwAAAAD/j2r4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwCwAAAPD4j2r4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwCwAAAPCAj2r4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAuwAAAAAAAAAAC7uwAAsAD7qGb4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALALAAAAAAAAAAC7uwAAALv4r2b4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALu7AAAAAAAAAAC7sAAAALvwr2b4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALu7AAAAAAAAAAAAAAAAAAD/r2b4ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALALAAAAAAAAAAAAAAAAAAD/r2ZvZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPD4qGZvZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/qGZvZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAC7AAAAAAAAAAAI/waoZvZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAsAAAAAAAAAAPDwaob/ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAsAAAAAAAuwAPD/aob6ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALALAACPZob6ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALALAPCvZob6ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCvZob6ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA+vZohqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPCqZmhqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8IhqZmhqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAgGhmhmhqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAAAAAAAAAAAAA8GZmhmZqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwuwsAAAAAr2pmhmZqZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAuwAAALDwr2ZmaKZmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAuwAAALugamZmaKZmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwuwsAAA+qZmaGZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwuwsA8K9qZmZoZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwuwvwYGpmZoZmZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAuwD/qmZmhmhmZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACwAAAAAAAABqZmZmiGZmZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8A9qZmaGaGZmZqb2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAsAAL/2ZmZmaIZmZmZqr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAALvwYGZmZoZoZmZmZqr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPtvZmZmZohmZmZmZmr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA/29mZmZmiGZmZmZmZmr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/b2ZmZmaGaGZmZmZmZmr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD2BmZmZmZoZoZmZmZmZmpmr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAPD/ZmZmZmZmhohmZmZmZmZmpmr2ZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/9mZmZmZmaIaGZmZmZmZmamqmpmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/////r6pmZmZmhohoZmZmZmZmZmamqmpmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA+qqqpqZmZmZoaIaGZmZmZmZmZmZqaqqmpmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAD/D6ZqZmZmZmaIiIhmZmZmZmZmZmZmZqqqqmZmZmYAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAADw/2ZmZmZmZmZmhohoZmZmZmZmZmZmZmZmpqaqpmpmZmYAAAAAAAAAAAAAAAAAAAAAAAD///AP/2b//2//b2ZmZmZmhoiIiGZmZmZmZmZmZmZmZmZmpqqqpmpmZmYAAAAAAAAAAAAAAAAAAACqqvCv/2ZmZmZmZmZmZmZmZmaGaGZmZmZmZmZmZmZmZmZmZmZmpqpqpmZmZmYAAAAAAAAAAAAAAAAAAABqZmpmZmpmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmZmampmZmZmZmY=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"ocean2\"\n    },\n    \"c^#HB{wS5hM[\": {\n        \"data\": \"hwQeABAAAAAAAAAAAAAAAAAAAACwsLAAAAAAALCwsAAAAAAAAAsLAAAAAAAAsAAAAAAAAACwAAAAAAAAAP//AAAAAADwREQPAAAAAE9FRA8AAAD/VERE9AAAAF9FVUT0AAAAX1XMRfQAAP9VxZlc9AAAX1XFkVz0DwBfVVXMVfT8/19VVVVV9AAAX1VVXFXEAADw9MXJVfQAAPD/VFxF9AAAAPBUVUX/AAAA8FtcRQ8AAADwz8lFDwAAAABfXEQPAAAAAF9V9AAAAAAAT0T0AAAAAADwRM8AAAAAAAD/AAAAAAAAC/8AAAAAAAC7u7sAAAAAAAD/sAA=\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"enemy\"\n    },\n    \"image1\": {\n        \"data\": \"hwQQABAAAAAAAAAAALzMDAAA+7/AVVTFAMD1X8tFVcUAwFVVVbRVxQAAzDxVRcvFAMBmxlNFRMwAbMw8VUXLxcDGVVVVRFXFwMP1X7y7VcXAM/zPw7VVxcAzM2bDVcQMbDMzYzPMTAQ8NjNjM7PEzMA8M2Mzs1XFAMAzzDMMy8wAAMzMzAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"snail\"\n    },\n    \"image2\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA8A/wAAAAAAD/+/8AAAAAAP+7zAAAAAAAz73LAAAAAADP3csAAAAAAPDczAAAAAAA8M/MAAAAAAAA/88AAAAAAAAA/wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"fin\"\n    },\n    \"anim3\": {\n        \"namespace\": \"myAnimations.\",\n        \"id\": \"anim3\",\n        \"mimeType\": \"application/mkcd-animation\",\n        \"data\": \"MzIwMDFlMDAxMDAwMDUwMDAwMDAwMDAwMDAwMDAwY2YwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwOTAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDVmNTVmNTBmMDAwMDAwMDAwMDAwMDAwMDAwZjBmZjU1NTU0NTBmMDAwMDAwMDA5MDAwMDAwMDAwZjA1NTU1NTVmNWZmZmYwMDAwMDAwMDAwMDAwMDAwNGY1NTU1NTU1NTQ0ZmJmZjBmYjAwYmIwMGIwMGYwNTQ1NGNjNTVjNTU1YzU1NWY0MDAwYjAwYjAwMDRmNDVjNTE5NWM5YzVjOWM1YzQ0ZmZmYmIwMGJiYjRmNDRjNTk5NWNjNTU1YzU1NTQ0ZmZmYjAwYjAwMDRmNDQ1NGNjNTU1NTU1NTU0NGY0MDAwYmIwMGIwMGYwNDQ0NDU1NTU1NTQ0NDRmNGNmMDBiYjAwMDAwMDAwZmY0NDQ0NDQ0NGY0ZmYwZjAwMDAwMDAwMDAwMDAwZjBmZmZmZmZmY2ZmMDAwMDAwMDAwMDAwMDkwMDAwMDAwMDAwY2YwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwOTAwMDAwMDAwMDAwMDVmNTVmNTBmMDAwMDAwMDAwMDAwMDAwMDAwZjBmZjU1NTU0NTBmMDAwMDAwMDAwMDAwMDAwMDAwZjA1NTU1NTVmNWZmZmYwMDAwMDAwMGIwMDAwMDAwNGY1NTU1NTU1NTQ0ZmJmZjBmMDAwMDAwMGIwMGYwNTQ1NGNjNTVjNTU1YzU1NWY0YjAwYjAwYjAwMDRmNDVjNTE5NWM5YzVjOWM1YzQ0ZmZmYmIwMGJiYjRmNDRjNTk5NWNjNTU1YzU1NTQ0ZmZmYjAwYjAwMDRmNDQ1NGNjNTU1NTU1NTU0NGY0MDBiYjAwMGIwMGYwNDQ0NDU1NTU1NTQ0NDRmNGNmMDAwMGIwMDAwMDAwZmY0NDQ0NDQ0NGY0ZmYwZjAwMDAwMDAwMDAwMDAwZjBmZmZmZmZmY2ZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwY2YwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDA5MDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDVmNTVmNTBmMDAwMDAwMDAwMDAwMDAwMDAwZjBmZjU1NTU0NTBmMDAwMDAwMDAwMDkwMDAwMDAwZjA1NTU1NTVmNWZmZmYwMDAwMDAwMDAwMDAwMDAwNGY1NTU1NTU1NTQ0ZmJmZjBmMDAwMGIwMGIwMGYwNTQ1NGNjNTVjNTU1YzU1NWY0MDAwMDAwYjAwMDRmNDVjNTE5NWM5YzVjOWM1YzQ0ZmZmYmIwMGJiYjRmNDRjNTk5NWNjNTU1YzU1NTQ0ZmZiYjAwYjAwMDRmNDQ1NGNjNTU1NTU1NTU0NGY0MDAwMGIwMGIwMGYwNDQ0NDU1NTU1NTQ0NDRmNGNmMDAwMDAwMDAwMDAwZmY0NDQ0NDQ0NGY0ZmYwZjAwMDAwMDAwMDAwMDAwZjBmZmZmZmZmY2ZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwY2YwMDAwMDAwMDAwOTAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDkwMDAwMDAwMDVmNTVmNTBmMDAwMDAwMDAwMDAwMDAwMDAwZjBmZjU1NTU0NTBmMDAwMDAwMDAwMDAwMDAwMDAwZjA1NTU1NTVmNWZmZmYwMDAwMDAwMGIwMDAwMDAwNGY1NTU1NTU1NTQ0ZmJmZjBmMDAwMDAwMGIwMGYwNTQ1NGNjNTVjNTU1YzU1NWY0MDAwMDAwYjAwMDRmNDVjNTE5NWM5YzVjOWM1YzQ0ZmZiYmIwMGJiYjRmNDRjNTk5NWNjNTU1YzU1NTQ0ZmZmYjAwYjAwMDRmNDQ1NGNjNTU1NTU1NTU0NGY0MDAwMDAwMGIwMGYwNDQ0NDU1NTU1NTQ0NDRmNGNmMDAwMGIwMDAwMDAwZmY0NDQ0NDQ0NGY0ZmYwZjAwMDAwMDAwMDAwMDAwZjBmZmZmZmZmY2ZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwY2YwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDkwMDAwMDAwMDAwMDAwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDVmNTVmNTBmMDAwMDAwMDAwMDAwMDAwMDAwZjBmZjU1NTU0NTBmMDAwMDAwMDAwMDAwMDAwMDAwZjA1NTU1NTVmNWZmZmYwMDAwMDAwMGIwMDAwMDAwNGY1NTU1NTU1NTQ0ZmJmZjBmMDAwMDAwMGIwMGYwNTQ1NGNjNTVjNTU1YzU1NWY0MDBiYjAwYjAwMDRmNDVjNTE5NWM5YzVjOWM1YzQ0ZmZmYmIwMGJiYjRmNDRjNTk5NWNjNTU1YzU1NTQ0ZmZmYjAwYjAwMDRmNDQ1NGNjNTU1NTU1NTU0NGY0YjAwYjAwMGIwMGYwNDQ0NDU1NTU1NTQ0NDRmNGNmMDAwMGIwMDAwMDAwZmY0NDQ0NDQ0NGY0ZmYwZjAwMDAwMDAwMDAwMDAwZjBmZmZmZmZmY2ZmMDAwMDAwMDAwMA==\",\n        \"displayName\": \"animated enemy\"\n    },\n    \"anim4\": {\n        \"namespace\": \"myAnimations.\",\n        \"id\": \"anim4\",\n        \"mimeType\": \"application/mkcd-animation\",\n        \"data\": \"YzgwMDEwMDAxMDAwMDQwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGNjY2MwMDAwMDAwMDAwY2NkZGRkMGMwMDAwMDBjMGNjY2NkYzBjMDAwMDAwY2M0NDQ0Y2QwYzAwMDBjMGQ0NDQ0NDE0MGNjYzAwNGM0NDQxNDRkNGMxYzRjMDQ0NDQ0MTQ0NDRjMWM0NGY0NDQ0NDE0NDQ0NDFmNDRmNDQ0ZmMxNGM0NGYxZjQ0ZjQ0NDQ0MWY0NDRmZGY0ZjA0NDQ0YzFmNGQ0ZmZmZjAwZmZkNDQ0ZmZjNGNmMDAwMDAwZmY0NDQ0ZGNjYjAwMDAwMDAwZmZmZmRkY2QwMDAwMDAwMDAwMDBjYzBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYzBjY2NjMDAwMDAwMDAwMGRjZGRkZDBjMDAwMDAwMDBjY2NjZGMwYzAwMDAwMGMwNDQ0NGNkMGMwMDAwMDBkYzQ0NDQxNDBjMDAwMGMwNDQ0MTQ0NDRjMTAwMDA0YzQ0MTQ0NDQ0YzFjY2MwNDQ0NDE0Y2M0NDQxYzRjMDQ0NDQxNDQ0NGZmMWY0NGY0NGY0MTQ0YzRmZmRmNDRmNDQ0NDE0ZjQ0ZmZmZjRmMDQ0NDQ0MTQ0YzRjYmZmMDBmZmRmNDQ0NGRjY2QwMDAwMDBmMGZmZmZjYzBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBjY2NjMDAwMDAwMDAwMGNjZGRkZDBjMDAwMDAwYzBjY2NjZGMwYzAwMDAwMGNjNDQ0NGNkMGNjYzAwYzBkNDQ0NDQxNGNjYzQwMDRjNDQ0MTQ0ZDRjMWY0YzA0NDQ0NDE0NDQ0NDFmNDRmNDQ0NDExZmM0NGYxZjQ0ZjQ0NGZjMWY0NDRmMWY0NGY0NDQ0NDFmNDQ0ZmRmZmYwNDQ0NGMxNGNkNGZmMDAwMGZmZDQ0NDQ0YzQwZjAwMDAwMGZmNDQ0NGRjY2IwMDAwMDAwMGZmZmZkZGNkMDAwMDAwMDAwMDAwY2MwYzAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGMwY2MwYzAwMDAwMDAwYzBkY2RkY2QwMDAwMDBjMGNjY2NkY2NkMDAwMGMwY2M0NDQ0Y2RjY2NjMDA0YzE0NDQ0NDE0Y2NmNGMwNDQ0NDQxNDRkNGYxZjQ0ZjQ0NDQ0MTQ0NDRmMWY0NGZmNDQ0NDFmYzQ0NDFmNDRmNDQ0NGMxZjQ0NGYxZmZmMDQ0NDQ0MWY0NDRmZDAwMDA0ZjE0YzQ0Y2Q0MGYwMDAwZjA0ZDQ0NDRjNDBmMDAwMDAwZmY0NDQ0ZGNjYjAwMDAwMDAwZmZmZmRkY2QwMDAwMDAwMDAwMDBjYzBjMDA=\",\n        \"displayName\": \"animated food\"\n    },\n    \"anim2\": {\n        \"namespace\": \"myAnimations.\",\n        \"id\": \"anim2\",\n        \"mimeType\": \"application/mkcd-animation\",\n        \"data\": \"YzgwMDIwMDAxMDAwMDQwMDAwMDAwMDAwMDAwMGMwZmNmZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGMwZGNiZGZjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwY2NkZGJiMGYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBjZmJjY2IwZjAwMDAwMDAwMDAwMDAwMDAwMGYwZmZmZmNjY2NjY2ZmMDAwMDAwMDBjMGNjMDAwMGYwYmZiYmJiYmJiY2JiY2JmZjBmMDBjMGJjY2IwMDAwYmZiYmJiYmJjYmNiYmJiYmNjZmMwZmRjYmIwYzAwZmZiYmJiYmJmZmJiYmNiY2JiY2NjY2ZjZGNiYjBmMDBiZmJjYmIxMWZmYjFiY2JiYmJjY2NjZmNiZmZiMDAwMGJmYmIxMTExMTExMWJiYmJjYmNjY2NjY2JiZmMwMDAwZjAxYjExMzNjYzExYmJiYmNjY2NjY2NjY2NmYzAwMDAwMGNmY2MxMzFjMTFiYmNiY2NjY2RiZmJiZmNiMGYwMDAwZjAxY2MzMTFjMWJiZmJkY2RkY2QwY2YwYmIwZjAwMDAwMGNmY2MxMWYxZGJiYmNjY2QwYzAwMDBiZmZiMDAwMDAwMDAwMGNjY2NjZmJkY2IwYzAwMDAwMGYwZmYwMDAwMDAwMDAwMDAwMGYwZmZmZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYzBmY2ZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBkY2JkZmIwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBjMGRkYmIwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGNmYmNjYjBmMDAwMDAwMDAwMGMwY2MwMDAwZmZmZmZmY2NjY2NjZmYwMDAwMDAwMGMwYmNjYjAwZmZiYmJiYmJiYmJiYmJjYmZmMGYwMDAwZGNiYjBjZmZiYmJiYmJiYmNiY2JiYmJiY2NmYzBmYzBkZGJiMGZiZmJjYmJiYmZmYmJiY2JjYmJjY2NjZmNmZmJkZmIwMGJmYmIxMTExZmZiMWJjYmNiYmNjY2NjY2JjYmJmYzAwZjAxYjExMTExMWIxYmJiYmNiY2NjY2NjY2NjYmZjMDAwMGNmY2MzM2NjMTFiYmJiY2NjY2NjY2NmZmJmY2IwZjAwZjAxYzEzMWMxMWJiY2JjY2NjZGJjYjAwZjBiYjBmMDAwMDNmYzMxMWMxYmJmYmRkZGRjZDBjMDAwMGJmZmIwMDAwZjAxZjExZjFkYmJiZGZjZDBjMDAwMDAwZjBmZjAwMDAwMGMwY2NjY2JmYmRmYjBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBmZmZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZjZmYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGNjZGRmYjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGMwZGJiZGZmMDAwMDAwMDBjMGNjMDAwMDAwMDAwMDAwY2ZiY2NiMGYwMDAwMDAwMGJjY2IwMDAwZjBmZmZmZmZjY2NjY2NmZjAwMDAwMGMwYmQwYzAwZjBjZmJiYmJiYmJiYmJiYmNiZmYwZjAwYzBiZDBmMDBjZmJiYmJiYmJiY2JiYmJiYmJjY2ZjMGZkY2ZiMDAwMGJmYmNiYmZiYmZiYmJjYmNiYmNjY2NmY2RmZmMwMDAwYmYxYjExZjFiZmJiYmNiY2JiY2NjY2NjYmJmYzAwMDBmMDFiMTExMTExYjFjYmJiY2JjY2NjY2NiY2NiMGYwMDAwY2ZjYzMzYmMxMWJiYmJjY2NjY2NmY2ZmYmIwZjAwMDBmMDFjMTMxYzExYmJjYmNjY2NkYmNiMDBiZmZiMDAwMDAwM2ZjMzExYzFiYmNjZGRkZGJkMGMwMGYwZmYwMDAwMDBmMDFmMTFmMWJkY2JkY2JkY2MwMDAwMDAwMDAwMDAwMDAwYzBjY2NjZGZiYmZiY2MwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBmMGZmZmYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGMwZmNmZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZGNiZGZiMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYzBkZGJiMGYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBjZmJjY2IwZjAwMDAwMDAwMDBjMGNjMDAwMGZmZmZmZmNjY2NjY2ZmMDAwMDAwMDBjMGJjY2IwMGZmYmJiYmJiYmJiYmJiY2JmZjBmMDAwMGRjYmIwY2ZmYmJiYmJiYmJjYmNiYmJiYmNjZmMwZmMwZGRiYjBmYmZiY2JiYmJmZmJiYmNiY2JiY2NjY2ZjZmZiZGZiMDBiZmJiMTExMWZmYjFiY2JjYmJjY2NjY2NiY2JiZmMwMGYwMWIxMTExMTFiMWJiYmJjYmNjY2NjY2NjY2JmYzAwMDBjZmNjMzNjYzExYmJiYmNjY2NjY2NjZmZiZmNiMGYwMGYwMWMxMzFjMTFiYmNiY2NjY2RiY2IwMGYwYmIwZjAwMDAzZmMzMTFjMWJiZmJkZGRkY2QwYzAwMDBiZmZiMDAwMGYwMWYxMWYxZGJiYmRmY2QwYzAwMDAwMGYwZmYwMDAwMDBjMGNjY2NiZmJkZmIwYzAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwZmZmZjAwMDAwMDAwMDAwMDAw\",\n        \"displayName\": \"swim left\"\n    },\n    \"anim1\": {\n        \"namespace\": \"myAnimations.\",\n        \"id\": \"anim1\",\n        \"mimeType\": \"application/mkcd-animation\",\n        \"data\": \"YzgwMDIwMDAxMDAwMDQwMDAwMDAwMDAwMDAwMDAwZmZjZjBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBjZmRiY2QwYzAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwYmJkZGNjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiY2NiZmMwMDAwMDAwMDAwMDBjYzBjMDAwMDAwMDBmZmNjY2NjY2ZmZmYwZjAwMDAwMGJjY2IwYzAwZjBmZmJjYmJjYmJiYmJiYmZiMGYwMDAwYzBiYmNkZjBjZmNjYmJiYmJjYmNiYmJiYmJmYjAwMDBmMGJiY2RjZmNjY2NiYmNiY2JiYmZmYmJiYmJiZmYwMDAwYmZmYmNmY2NjY2JiYmJjYjFiZmYxMWJiY2JmYjAwMDBjZmJiY2NjY2NjYmNiYmJiMTExMTExMTFiYmZiMDAwMGNmY2NjY2NjY2NjY2JiYmIxMWNjMzMxMWIxMGYwMGYwYmNmYmJmYmRjY2NjYmNiYjExYzEzMWNjZmMwMDAwZjBiYjBmYzBkY2RkY2RiZmJiMWMxMTNjYzEwZjAwMDBiZmZiMDAwMGMwZGNjY2JiYmQxZjExY2NmYzAwMDAwMGZmMGYwMDAwMDBjMGJjZGJmY2NjY2MwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZmZjBmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBmZmNmMGMwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGJmZGJjZDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiYmRkMGMwMDAwMDAwMDAwY2MwYzAwMDAwMDAwMDBmMGJjY2JmYzAwMDAwMDAwMDBiY2NiMGMwMDAwMDAwMGZmY2NjY2NjZmZmZmZmMDAwMGMwYmJjZDAwMDBmMGZmYmNiYmJiYmJiYmJiYmJmZjAwZjBiYmRkMGNmMGNmY2NiYmJiYmNiY2JiYmJiYmJiZmYwMGJmZGJmZmNmY2NjY2JiY2JjYmJiZmZiYmJiY2JmYjAwY2ZiYmNiY2NjY2NjYmJjYmNiMWJmZjExMTFiYmZiMDBjZmJjY2NjY2NjY2NiY2JiYmIxYjExMTExMWIxMGZmMGJjZmJmZmNjY2NjY2NjYmJiYjExY2MzM2NjZmMwMGYwYmIwZjAwYmNiZGNjY2NiY2JiMTFjMTMxYzEwZjAwYmZmYjAwMDBjMGRjZGRkZGJmYmIxYzExM2NmMzAwMDBmZjBmMDAwMDAwYzBkY2ZkYmJiZDFmMTFmMTBmMDAwMDAwMDAwMDAwMDAwMGMwYmZkYmZiY2NjYzBjMDAwMDAwMDAwMDAwMDAwMDAwMDBmZmZmMGYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGZmY2YwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYmZkZGNjMDAwMDAwMDAwMDAwMDBjYzBjMDAwMDAwMDBmZmRiYmQwYzAwMDAwMDAwMDAwMGJjY2IwMDAwMDAwMGYwYmNjYmZjMDAwMDAwMDAwMDAwYzBkYjBjMDAwMDAwZmZjY2NjY2NmZmZmZmYwZjAwMDBmMGRiMGMwMGYwZmZiY2JiYmJiYmJiYmJiYmZjMGYwMDAwYmZjZGYwY2ZjY2JiYmJiYmJjYmJiYmJiYmJmYzAwMDBjZmZkY2ZjY2NjYmJjYmNiYmJmYmJmYmJjYmZiMDAwMGNmYmJjY2NjY2NiYmNiY2JiYmZiMWYxMWIxZmIwMGYwYmNjYmNjY2NjY2JjYmJiYzFiMTExMTExYjEwZjAwZjBiYmZmY2ZjY2NjY2NiYmJiMTFjYjMzY2NmYzAwMDBiZmZiMDBiY2JkY2NjY2JjYmIxMWMxMzFjMTBmMDAwMGZmMGYwMGMwZGJkZGRkY2NiYjFjMTEzY2YzMDAwMDAwMDAwMDAwMDBjY2RiY2RiY2RiMWYxMWYxMGYwMDAwMDAwMDAwMDAwMDAwY2NiZmJiZmRjY2NjMGMwMDAwMDAwMDAwMDAwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZjZjBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBiZmRiY2QwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwYmJkZDBjMDAwMDAwMDAwMGNjMGMwMDAwMDAwMDAwZjBiY2NiZmMwMDAwMDAwMDAwYmNjYjBjMDAwMDAwMDBmZmNjY2NjY2ZmZmZmZjAwMDBjMGJiY2QwMDAwZjBmZmJjYmJiYmJiYmJiYmJiZmYwMGYwYmJkZDBjZjBjZmNjYmJiYmJjYmNiYmJiYmJiYmZmMDBiZmRiZmZjZmNjY2NiYmNiY2JiYmZmYmJiYmNiZmIwMGNmYmJjYmNjY2NjY2JiY2JjYjFiZmYxMTExYmJmYjAwY2ZiY2NjY2NjY2NjYmNiYmJiMWIxMTExMTFiMTBmZjBiY2ZiZmZjY2NjY2NjY2JiYmIxMWNjMzNjY2ZjMDBmMGJiMGYwMGJjYmRjY2NjYmNiYjExYzEzMWMxMGYwMGJmZmIwMDAwYzBkY2RkZGRiZmJiMWMxMTNjZjMwMDAwZmYwZjAwMDAwMGMwZGNmZGJiYmQxZjExZjEwZjAwMDAwMDAwMDAwMDAwMDBjMGJmZGJmYmNjY2MwYzAwMDAwMDAwMDAwMDAwMDAwMDAwZmZmZjBmMDAwMDAwMDAwMDAw\",\n        \"displayName\": \"swim right\"\n    },\n    \"WRHzQ06n]_D#g\": {\n        \"namespace\": \"[XxxVj.\",\n        \"id\": \"WRHzQ06n]_D#g\",\n        \"mimeType\": \"application/mkcd-animation\",\n        \"data\": \"NjQwMDI0MDAxMDAwMDYwMDAwMDAwMDAwMDAwMDAwZmZjZjBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYmZkYmNkMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiYmRkMGMwMDAwMDAwMDAwMDAwMGNjMGMwMDAwMDAwMDAwZjBiY2NiZmMwMDAwMDAwMDAwMDAwMGJjY2IwYzAwMDAwMDAwZmZjY2NjY2NmZmZmZmYwMDAwMDAwMGMwYmJjZDAwMDBmMGZmYmNiYmJiYmJiYmJiYmJmZjAwMDAwMGYwYmJkZDBjZjBjZmNjYmJiYmJjYmNiYmJiYmJiYmZmMDAwMDAwYmZkYmZmY2ZjY2NjYmJjYmNiYmJmZmJiYmJjYmZiMDAwMDAwY2ZiYmNiY2NjY2NjYmJjYmNiMWJmZjExMTFiYmZiMDAwMDAwY2ZiY2NjY2NjY2NjYmNiYmJiMWIxMTExMTFiMTBmMDAwMGYwYmNmYmZmY2NjY2NjY2NiYmJiMTFjYzMzY2NmYzAwMDAwMGYwYmIwZjAwYmNiZGNjY2NiY2JiMTFjMTMxYzEwZjAwMDAwMGJmZmIwMDAwYzBkY2RkZGRiZmJiMWMxMTNjZjMwMDAwMDAwMGZmMGYwMDAwMDBjMGRjZmRiYmJkMWYxMWYxMGYwMDAwMDAwMDAwMDAwMDAwMDAwMGMwYmZkYmZiY2NjYzBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZmZjBmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZjZjBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYmZkYmNkMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiYmRkMGMwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiY2NiZmNmZmZmMGYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZjY2JjYmJiYmJiZmJmZjAwMDAwMGNjY2MwYzAwMDBmMGZmYmNiYmJiYmJiYmJiYmJiYjBmMDAwMGJjYmJjZDAwZjBjZmNjYmJiYmJjYmNmZmJiYmJjYjBiMDAwMGMwYmJkZGZjY2ZjY2NjYmJjYmNiYmJmZjExMTFiYjBiMDAwMDAwYmZkYmNiY2NjY2NjYmJjYmNiMWIxMTExMTFiMTBmMDAwMDAwY2ZiYmNjY2NjY2NjYmNiYmJiMWJjMTMzY2NmYzAwMDAwMDAwY2ZiY2ZmY2NjY2NjY2NiYmJiMTFjYzMxYzEwZjAwMDAwMGYwYmNmYjAwYmNiZGNjY2NiY2JiMTExMTNjZjMwMDAwMDAwMGYwYmIwZjAwYzBkY2RkZGRiZmJiMWMxMWYxMGYwMDAwMDAwMGJmZmIwMDAwMDBjMGRjZmRiYmJkMWZjYzBjMDAwMDAwMDAwMGZmMGYwMDAwMDAwMGMwYmZkYmZiY2MwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZmZmZjBmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwZmZjYzAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwYmJkZDBjMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwYmZkYmZkZmZmZmZmZmYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwY2ZjYmJmYmJiYmJiYmIwZjAwMDAwMDAwMDAwMDAwMDBmMGZmY2ZiY2ZiYmYxMWMxYmIwZjAwMDAwMGNjY2MwYzAwZjBjZmNjYmJiYmZiMWYxMTExYjEwZjAwMDAwMGJjYmJjZDAwY2ZjY2JjY2JjYmJiMTEzM2NjZjEwMDAwMDAwMGMwYmJkZGZjY2NjY2JjYmNiY2JiYzEzMWMxZmMwMDAwMDAwMDAwYmZkYmNiY2NjY2JjYmNiY2JiMTExMTExMGYwMDAwMDAwMDAwY2ZiYmNjY2NjY2NjYmJiYjFiMTExMTExMGYwMDAwMDAwMDAwY2ZiY2ZmY2NjY2NjYmNiYjFiMTExMWYxMDAwMDAwMDAwMGYwYmNmYmMwZGJjYmNjY2NiYmNiMTExMTBjMDAwMDAwMDAwMGYwYmIwZjAwZGNkZGRkZmRiYmNiMTFjYzAwMDAwMDAwMDAwMGJmZmIwMDAwYzBkY2RkYmZkYmZiY2YwMDAwMDAwMDAwMDAwMGZmMGYwMDAwMDBjMGZjYmJiZDBmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGYwZmZmZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBmMGZmY2MwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBmMGJiYmJmY2ZmZmZmZmZmMDAwMDAwMDAwMDAwMDAwMDAwMDAwMGJmZmZiZmJiYmJiYmJiMGYwMDAwMDAwMDAwMDAwMDAwMDAwMGZmYmJiYmZmMWIxMWJiMGYwMDAwMDAwMDAwMDAwMDAwMDBmZmJjYmJiYmZmMTExMWIxMGYwMDAwMDAwMDAwMDAwMDAwZjBjY2JjYmNiYzFiYzFjYzFjMGYwMDAwMDAwMGNjY2MwYzAwY2ZjY2NiY2JiYjFiMWMxY2ZjMDAwMDAwMDAwMGJjZGJjZGZjY2NjY2NiY2JiYjFiMzNjMzAwMDAwMDAwMDAwMGMwYmNkZGNiY2NjY2JiYmJiYjFiM2MzMzBjMDAwMDAwMDAwMDAwY2NiYmNjY2NjY2JjYmJiYjExMWMzMzBjMDAwMDAwMDAwMDAwY2ZiY2ZmY2NjY2NjYmJiYjExYzExM2NjMDAwMDAwMDAwMDAwY2ZmY2MwYmJjY2NjYmNiYjFjMTExMWMxMDAwMDAwMDAwMGYwYmNmYjAwZGNkZGRkYmZiYjFjMTFjMTBjMDAwMDAwMDAwMGYwYmIwZjAwYzBkZGZkYmJiZGZmY2MwYzAwMDAwMDAwMDAwMGJmZmIwMDAwMDBjY2JmZGJmYjAwMDAwMDAwMDAwMDAwMDAwMGZmMGYwMDAwMDAwMGZmZmYwZjAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBmZmNmMGMwMGZmZmZmZjBmMDAwMDAwMDAwMDAwMDAwMDAwMDBiZmJiY2JmZmJiYmJiYmZiMDAwMDAwMDAwMDAwMDAwMDAwMDBmMGZiYmZiYmJiMTFiMWZiMDAwMDAwMDAwMDAwMDAwMDAwMDBmMGJmYmJmYjFmMTExMWZiMDAwMDAwMDAwMDAwMDAwMDAwZjBjZmJiYmJmYjFmY2NjY2YxMDAwMDAwMDAwMDAwMDAwMDAwY2ZjY2NiY2JiYmMxYzFjMWZmMDAwMDAwMDAwMGNjY2MwY2YwY2NiY2JjYmNiYjMxMzNjYzBmMDAwMDAwMDAwMGJjZGJjZGNmY2NiY2JjYmNiYmMxMzNjMzAwMDAwMDAwMDAwMGMwYmNkZGNjY2NiY2JiYmJiYmMxMzNjMzAwMDAwMDAwMDAwMDAwY2NiYmNjY2NjY2JiYmIxYmMxMzNjMzAwMDAwMDAwMDAwMDAwY2ZiY2NmY2NjY2JjYmIxYmMxMzFjMzBjMDAwMDAwMDAwMDAwY2ZmY2JjY2JjY2NjYmJjYjExM2NjMTBjMDAwMDAwMDAwMGYwYmNmYmMwZGRkZGZkYmJjYjExMTExMTBjMDAwMDAwMDAwMGYwYmIwZjAwZGNkZGJmZGJmYjExMTFjYzAwMDAwMDAwMDAwMGJmZmIwMDAwYzBmY2JiYmRmZmNmY2MwMDAwMDAwMDAwMDAwMGZmMGYwMDAwMDBmMGZmZmYwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBmZmNmMGMwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBiYmRiY2QwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDAwMDBiZmJiZGRmY2ZmZmYwZjAwMDAwMGNjY2MwYzAwMDAwMGZmY2ZiYmJiYmJiYmJiYmJmYjBmMDAwMGJjYmJjZDAwMDBmZmNjYmNiYmJiYmNiY2JiYmJiYmZiMGYwMGMwYmJkZGZjZmZjY2NjYmNiYmNiYmJiY2JiYmJiYmJiZmIwMDAwYmZkYmNiY2NjY2NjYmNiYmNiY2JiYmJiYmJiYmJiYmMwZjAwY2ZiYmNjY2NjY2NjY2NiYmJiY2JiYmZmYmZiYmJiYmIwZjAwY2ZiY2ZmYmNjY2NjY2NiY2JiY2JiYmZmMWYxMWIxZmIwZmYwYmNmYjAwY2NiYmNiY2NjY2JjYmIxYjExMTExMTExZmYwMGJmZmIwZjAwMDBjY2JjZGRiZmJiYmQxMWMxY2NjY2NjMDAwMGZmMGYwMDAwMDAwMGMwZmNiYmRiZmJjY2NjY2MwMDAwMDAwMDAwMDAwMDAwMDAwMDAwZjBmZmZmMGYwMDAwMDAwMDAwMDAwMA==\",\n        \"displayName\": \"shooting shark\"\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myImages\"\n    }\n}",
  "images.g.ts": "// Auto-generated code. Do not edit.\nnamespace myImages {\n\n    helpers._registerFactory(\"image\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"~I/xlSOb!:ehNE!zTIaq\":\n            case \"shark\":return img`\n..............fffcc.................\n..............fbbddc................\n...............fbbddc...............\nccc............fcbbccf..............\ncbbcc.........ffccccccffffff........\n.cbbdc.....fffcbbbbbbbbbbbbbff......\n.fbbddc..ffcccbbbbcbcbbbbbbbbbff....\n..fbbdfffcccccbbbcbcbbffbbbbbcbf....\n..fcbbbcccccccbbbcbcb1ff1111bbbf....\n..fccbcccccccccbbbbbb11111111bf.....\n.fcbbfffccccccccbbbb11cc33cccf......\n.fbbf...cbdbcccccbbb111c131cf.......\nfbbf.....ccdddddfbbbc111c33f........\nfff........ccddfbbdbf1111ff.........\n.............cfbbdbfccccc...........\n..............fffff.................\n`;\n            case \"]uSp,Yb2U]iY\":\n            case \"food\":return img`\n. . . . . . . . . . . . . . . . \n. . . . . . . c c c c c . . . . \n. . . . . . c d d d d d c . . . \n. . . . . . c c c c c d c . . . \n. . . . . c 4 4 4 4 d c c . . . \n. . . . c d 4 4 4 4 4 1 c . . . \n. . . c 4 4 1 4 4 4 4 4 1 c . . \n. . c 4 4 4 4 1 4 4 4 4 1 c c c \n. c 4 4 4 4 4 1 c c 4 4 1 4 4 c \n. c 4 4 4 4 4 1 4 4 f 4 1 f 4 f \nf 4 4 4 4 f 4 1 c 4 f 4 d f 4 f \nf 4 4 4 4 4 4 1 4 f f 4 f f 4 f \n. f 4 4 4 4 1 4 4 4 4 c b c f f \n. . f f f d 4 4 4 4 c d d c . . \n. . . . . f f f f f c c c . . . \n. . . . . . . . . . . . . . . . \n`;\n            case \"?]c;BAWx@CPp7,Xc!||y\":\n            case \"decoration\":return img`\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n................\n.....88.........\n.....868........\n......868.......\n.......868......\n.......866......\n.......8676.....\n......67656.....\n.....656758.....\n....65775868....\n....65656868....\n....87678868....\n....87678668....\n....87677668....\n....8776768.....\n.....87678......\n......8768......\n`;\n            case \"=NL1D;jj+wTeW(}r0(uZ\":\n            case \"laser\":return img`\n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . 5 5 5 5 5 5 5 . . \n5 2 . 2 2 2 2 2 2 2 2 . \n. . . 5 5 5 5 5 5 5 . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n. . . . . . . . . . . . \n`;\n            case \"Ik6joQcYX!hh)DS[|_?1\":\n            case \"ocean1\":return img`\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n..d9............................................................................................................................................................\n..dd............................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\nd..............................................................................................................................................................d\n9d............................................................................................................................................................d.\n.d............................................................................................................................................................dc\ndd............................................................................................................................................................dd\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\nd..............................................................................................................................................................d\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n...........................................................................................................................................................d9...\n...........................................................................................................................................................dd...\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n.......................................................................................................dd.......................................................\n......................................................................................................d.9d......................................................\n......................................................................................................d.dd......................................................\n.......................................................................................................dd.......................................................\nb..............................................................................................................................................................b\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n...................................ffffffffffccbbcbbccbb........................................................................................................\n...........................ffffccccccccccccccccccccccccbbbbc....................................................................................................\nff.................ffcccccccccccccccccccccccccccccccccccccbbbb..................................................................................................\nffff.ff..ffffcccccbccccccccccccccccccccccccccccccccccccccccccbbccbb.............................................................................................\nffffffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccbbbb..........................................................................................\nddfcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccb......................................................................................fd1\ndd1dcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc.b.....................ffffffffffccbbfbbbbbb......................................ffdddd\nddd111ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccbb................fffccccccccccccccccccccbbbf..................................fdddddd\ndddddd11cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc.bb............fccccccccccccccccccccccccbcbffff............................fdddddddd\nddddddd111ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccbbb.........fccccccccccccccccccccccccccccbbbfff........................ffddddddddd\ncccdddddd1dcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccbbbb....ffccccccccccccccccccccccccccccccccbccffffffffffffffffff.....fddddddbbbbb\nbbbbdddddd1dcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccbbb..fccccccccccccccccccccccccccccccccccccccccccccccccccccbffffffdddddbbbbbbd\nddcbbdddddd11ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccc.fccccccccccccccccccccccccccccccccccccccccccccccccccccccbccccddddbbbbbbddd\nddddbbdddddd11cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfddddbbbbbddddd\ndddddbbdddddd11ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccfddddbbbbddddddd\ndddddddbbddddd11ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfcccccccccccccccccccccccccccccccccccccccccccccccccccccccccfcddddbbbbdddddddd\nddddddddccddddd11ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccddddbbbbddddddddd\ndddddddddddddddd11dccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfcccccccccccccccccccccccccccccccccccccccccccccccccccccccccddddddbbcdddd111ddd\nddddddddddddddddd11dccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccddddddbbccdddddddddd\ndddddddddddddddddd11cccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfdddddbbcccdddbbddddd\nddddddddddddddddddd11ccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfccccccccccccccccccccccccccccccccccccccccccccccccccccccccfdddddbbccccdddbcddddd\ndddddddddddddddddddd1dcccccccccccccccccccccccccccccccccccccccccccccccccccccccccffcccccccccccccccccccccccccccccccccccccccccccccccccccccccffdddbbbbccccddddbbddddb\nddddddddddddddddddddd11bcccccccccccccccccccccccccccccccccccccccccccccccccccccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccffddddbbcccffcddddbcddddb\ndbdddddddddddddddddddd1bbbcccccccccccccccccccccccccccccccccccccccccccccccccffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccffcdddbbcccffcddddddbddddb\ndbdddddddddddddddddddd11fbbcccccccccccccccccccccccccccccccccccccccccccccffffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccfffddddbccfcccdddddddbbddbb\ncbddddddddddddddddddddd1dffbccccccccccccccccccccccccccccccccccccccccccfffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffcddddbccccddddddddddbcddbb\nbddddddddd1ddddddddddddd1dffbbbbccccccccccccccccccccccccccccccccccffffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffddddbbcdddddddddddddbcddbb\ncddddddddd1dddddddddddddd1fffffffbcccccccccccccccccccccccccccccccffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffdddbbfddddddddddddddccddbb\ndddddddddddddddddddddddddd1cccffffffbcccffccccccccccccccccccccfffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffdddbbfdddddddddddddddccdddb\ndddddddddbcddddddddddddddd11ccccccffffffbbbbfbbbbffccfffffccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfffdcbbbbbddddddddddbfccfcdddb\nddddddddddddddddddddddddddd11cccccccccffffffffffbfbbccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffffdbbbbbbdddddddddbbbcffcddddb\nddddddddddddddddddddddddddddddcccccccccccccccfffffcccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfffffdcbddddddddddddddcdddddddddb\ndddddddddddddddddddddddddddddddfccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffffffdbddddddddddddddddddddddddbb\nddddddddddddddddddddddddddddddddfccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffffffdddddddddddddddddddddddddddbb\nbddddddddddddddddddddddddddddddfffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccffffffffffffddddddddddddddbbbcdddddb\nbdddddddddddddddddddddddddddddddfffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfffffffddddddddddddddddbbdbbccddddddb\nbdddddddddddddddddddddddddddddddddffffcccccccccccffccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccccfffffdddddddddddddddbbbbbcbbbcddddddddb\nbddddddddddddddddddddddddddddddddffffccccccccffffffffffffffccccccccccccccccccccccccccccccfffccccccccccccccccccccccccccffffffffdddddddddddcbbbbcfccfcccddddddddbb\nbdddddddddddddddddddddddddddddddddddffffffffffffffffffffffffffffffffffcccccccccccccccffffffffcccccfffccccccccccfffffffffffffffdddfddddbbbbbcccfccccdddddddddddbb\nbddddddddddddddddddddddddddddddddddddddfffffffd1ccfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffddddfddffdddbbddddddddddddddddddddddbfc\nbdddbbdddddddddddddddddddddddddddbbbbbbbfddddddd1111ccfffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffdffdddddddffdddbdddddddddddddddddddddddbccc\nbddddbbbdddddddddddddddddddddbbbbbbbbbbbfffffdddddd111fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffddfdfddddddddfddddddddddddddddddddddddddbbccf\nbcdddddbbbcddddddddddddbbbbbbccbfcccccfbbbfffbddddddd11ffffffffffffffffffffffffffffffffffffffffffffffdddddbbfbbbbbffffcddddddffdfdddddddddddddddddddbbddddbbccfc\nbbcddddddbbbbfcbbbbbbbbbfcccfbbfbbfccbbbdddddfffddddddfffcccdddccffffffffffffffffffffffffffffffffdbbbbbbbbbbffbbbbdbbddfffffffffdddddddddddbbbbbbbbbbbbbbbbfffcc\ncbcccbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbdddddddddddffffffffdddfffdddddcccfffffffbbbbffffffffffffffffffffffffbbbbbbbbbbbbffbbbbbbbbbbbbbbbbbbbbbbbdddddddbbcccddddd\n`;\n            case \"q=voYSOp1V?b{:\":\n            case \"ocean2\":return img`\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\n................................................................................................................................................................\naaa.............................................................................................................................................................\naaaaaaa.........................................................................................................................................................\n6666aaaaa.......................................................................................................................................................\n6666666aaa......................................................................................................................................................\n66666666aaa.....................................................................................................................................................\naaaaaaa666a.....................................................................................................................................................\n6666666aaaaa....................................................................................................................................................\n66666666666aaa..................................................................................................................................................\na6666666666aaa..................................................................................................................................................\naaaaaaaaa666aaa.................................................................................................................................................\n666666666aaaaaaa................................................................................................................................................\n6666666666666aaaf.............................................................................................................................................aa\n66aaaaaaaaa666aaaa............................................................................................................................................a6\n6666666666aaaaaaaa............................................................................................................................................a6\n666666666666666aaaa...........................................................................................................................................a6\naaaaa666666666666aa............................................................................................................................................a\n66666aaaaaaa666666aa..........................................................................................................................................f6\n66666666666aaaaaaaaaa........................................................................................................................................ff6\n66666666666666666aaaaa.......................................................................................................................................fa6\n666666666666aaaa6666aa.......................................................................................................................................ff6\n6666666666666666aaaaaaf......................................................................................................................................ff6\n666666666666666666666aaa......................................................................................................................................6a\n6666666666666666666666aaa....................................................................................................................................f66\n66666666666666666666666aaa...................................................................................................................................f66\n666666666666aaaaaaaaaaaaaa....................................................................................................................................66\n66666666666666666666666aaaa..................................................................................................................................f66\n66666666666666666666666666aa.................................................................................................................................f66\n66666666666666666aaaaaa6666aa................................................................................................................................666\n66666666666666666666666aaaaaaf...............................................................................................................................666\n666666666666666666666666666a6a...............................................................................................................................f66\n6666666666666666aaaa666666666aa..............................................................................................................................f66\n6666666666666666666aaaaa666666aa.............................................................................................................................f66\n666666666666666666666666aaaaaa6aa............................................................................................................................f66\n66666666666666666666666666666aaaa............................................................................................................................f66\n666666666666666666666666aaa666666f...........................................................................................................................666\n666666666666666666666666666aaaaaaaa..........................................................................................................................f66\n66666666666666666666666666666666aaaa........................................................................................................................ff66\n666666666666666666666666aaaa6666666aaa......................................................................................................................ff66\n666666666666666666666666666aaaaaa6666af.....................................................................................................................f666\n66666666666666666666666666666666aaaaaaa.....................................................................................................................6666\n6666666666666666666666666666666666666a6a....................................................................................................................6666\n6666666666666666666666666666666666666666a..................................................................................................................f6666\n666666666666666666666666666666aa666666666a.................................................................................................................f6666\n66666666666666666666666666666666aaaaaa666aa................................................................................................................f6666\n66666666666666666666666666666666666666aaaaaaf...............................................................................................................6666\n6666666666666666666666666666666aa66666666a6aa.............................................................................................................f66666\n666666666666666666666666666666666aaaaaa66666af.............................................................................................................a6666\n66666666666666666666666666666666666666aaaaaaaaf..........................................................................................................faa6666\n666666666666666666666666666666666666ff666666aaa..........................................................................................................fa66686\n66666666666666666666666666aaaaaaa666666666666a6ff........................................................................................................fa66686\n666666666666666666666666666f666666666666aa666666aa.......................................................................................................fa66866\n66666666666666666666666666666666666666666aaaaaa66aa......................................................................................................fa66866\n6666666666666666666666666666666666666666666ff6aaaaaaa....................................................................................................fa66866\n666666666666666666666666666666666666666666666666666aa....................................................................................................fa66866\n66666666666666666666666666666666666666666666666aaa66aff..................................................................................................f666866\n66666666666666666666666666aaaaa666666aaaaaaaa6666aaaaaaaf...............................................................................................ff666866\n66666666666666666666666666af666666666666666666666666666aaf...............................................................................................a668866\n666666666666666666666666666666666666666666666666666666666aaa..........................................................b.bb..............................fa668666\n66666666666666666666666666666666666666666666666aaaaaaaaaa66aafff.......................................................bbbb............................ffa668666\n666666666666666666666666666666666666666666666666666666666aaaaaafff.....................................................bbbb............................f66688666\n66666666666666666666666666666666666666666666666666666666666666aaaaaf..................................................b.bb.............................f66686666\n6666666666666666666666666666666666666666666666666666666666666666666aaa.........................................................................b......f666686666\n6666666666666666666666666666666666666666666666666666666666666aaaaaa66a6a...........................b...................................................666686666\n666666666666666666666666666666666666666666666666666666666666666666aaaa6aaaaf...........................................................b...............666686666\n66666666666666666666666aaaaaaaaaaaaaaaaaaaaa6666666666666aaaaaaaaa66666666aaafff......................................................................6666886666\n6666666666666666666666aa666666666666666666fff666666666666666666666aaaaaa6666aaaaaf.....b.............................................................f6666866666\n66666666666666666666666666666666666666666666666666666666666666666666666aaaaaa666afaf....bb.............b...........b.................................f6666866666\n66666666666666666666666666666666666666666666666666666666666666666666666666666aaa66666...................bb...................b......................ff6666866666\n6666666666666666666666666666666666666666666666666666666666666666666666666666aaaaa6666aaa...............b......................bb.................b..f66668666666\n66666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaafa....................................bb..................bbf66668666666\n66666666666666666666666666666666aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa66666666666aa6666666666aa6aa..................................b....................bf666668666666\n6666666666666666666666666666666666666666666666666666666666666ffaaaaaaaaaaaaaaaaaaa66666666aaf....................................................b.f666688666666\n666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaa6666aaa..........................................b..bbb....f6666686666666\n66666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaa6ab.bb........b.............................bbbbbbb..f.6666686666666\n6666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666abbb.........bb...........................bbbbbbb.ff66666866666666\n6666666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaa666ff.........bb...........................b..bbb..f666666866666666\n66666666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaa66........b......................................666668866666666\n66666666666666666666666666666666666666666666666666666666aaaaaaaaaaaaaaaa666666666666666666666666a66................b..bbb.....................faa666668666666666\n666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaaaaa666666666aa666aff.............bbbbbb....................ff66666686666666666\n6666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaaaaaaaaa.............bbbbb......................a66666886666666666\n66666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666aff...........b..bbb...................f6a66666866666666666\n66666666666666666666666666666666666666666666666666666666666666666666666666666666aa66666666666666aaa666aa.......................b..........bffa666668666666666666\n6666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaa6666666aaa6aaa......................bb.......bb.a6666688666666666666\n666666666666666666666666666666666666666666666666666666666666aaaaaaaaaaaaaaa6666666666666666aaaaaaaaaaaaa6aa.bb..................bb.........aa6666886666666666666\naaa666666666666666666666666666666666666666666666666666666666666666666666fffaaaaaaaaaaaaaaaa666666666666a66aff..................b.........faa66668866666666666666\naaaaa66666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaaaaaaaaaafff........................ffa66668866666666666666a\na6aaaaaa66666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666666ff.......b..............f8faa666688666666666666aaa6\naaa6aaa6aaa6666666666666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaa6666afff.....bb....f.....f.886a666668666666666666a6aaa\naaaaaaaaa6aaa666666666666666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaa6666aaaaaaafff.ff.bb..f.8ff.ff.f866666668666666666666aaaaa6\n6aaa6aaa6aaaaaaaa66666666666666666666666666666666666666666666666666666666666666666666aaaaaaaaaaaa6666666666aaaf6f8ff8.b8.ff8f..fffffaa66666686666666666666aaaaa6\n888888888888aaaaaaaaaaaaaaaaa6666666666666666666666666666666666666666aaaaaaaaaaaaaaaaafff6aa666666666aaaaaaa6fafaffff8ffffffffff8aaaa6666668666666666666aaaaaa66\nfffff666ff688888888888888888aaaaaaaaaaaaaaaa666666666666666666666aaaaa66666666666666aaaaaaaaaaaa6aaaaaffff6faff8f8ffff8ffff88aaa666666666886666666666666aaaa6666\n666666666ffff66666666666666fff8888888888888aaaaaaaaaaaaaaaaaaaaa88888888888888888aaa8666666f6666ff66ffff6fff8fffff8888aaaaaaa6666666668886666666666666aaaaaaaaa6\n666666666666ffffffffffffffff66666666666666666666668888888888888888888866fffffffffffffffffffffff8fffffffffffff8aaaaaaaa666666666666688886666666666aaaaaaaaaa6aa66\n666666666666666666666666666666666666668888888888fffffff8888888888888888888ffffffffffffffffafffaaaaaaaaaaaaaaaa666666666666666888888866666aaaaaaaaaa6666666666666\n6aaa666aaaaafffffffffffaaaa666888888888aaa6666aaaaaaaafffff888888888888888888888888888888f88888888886666666666666668888888fffffaaaaaaaaaa66666666666666666666666\naa88888ffffff8888888888888aaaaaa8aaaffff88888888888888ffffffffffffffff8888866666666666668888888888888888888888ffffffffffff6666fffff66666666fffffffffffff66666666\n886666666666666666666668ffffffffffff666f66666666666666666ffffffff666aaaaaaa666666fffffffffff666666ffffffffff6666666666666666666666666666666666666666666666666666\n66666666fffffffffffff888666666666666666666666666aaaaa8aaa8666aaaaffafffffffffffff8866666666666ffff66666886666666666666666666666666666666666666666666666666666666\n6666666ff666666688886666666666666666ffffffffffffffffff6666666666666666688888866666666666666fff666666668666666666666666666666666666666666666666666666666666666666\n6666666666688888666666666666666666666688888886666666666666888888888888866666666666666666666666666666686666666666666666666666666666666666666666666666666666666666\n`;\n            case \"c^#HB{wS5hM[\":\n            case \"enemy\":return img`\n..............fc..............\n...............f..............\n...............f..............\n...............f..............\n............fffff.............\n............f5555ff...........\n.........fff555554f...........\n.........f5555555fffff........\n........f45555555544bffff..bb.\n.bb....f4545cc555c555c554f..b.\n...b..f4545c91c5c9c5c9c544ffbf\n.bb.bbf4445c99c55c555c5544ffbf\n...b..f44445cc55555555444f..b.\n.bb...f4444455555544444ffc..bb\n.......ff4444444444ffff.......\n.........fffffffcfff..........\n`;\n            case \"image1\":\n            case \"snail\":return img`\n. . . . . . . . . . . c c . . . \n. . . . . . . c c c c 6 3 c . . \n. . . . . . c 6 3 3 3 3 6 c . . \n. . c c . c 6 c c 3 3 3 3 3 c . \n. b 5 5 c 6 c 5 5 c 3 3 3 3 3 c \n. f f 5 c 6 c 5 f f 3 3 3 3 3 c \n. f f 5 c 6 c 5 f f 6 3 3 3 c c \n. b 5 5 3 c 3 5 5 c 6 6 6 6 c c \n. . b 5 5 3 5 5 c 3 3 3 3 3 3 c \n. c c 5 5 5 5 5 b c c 3 3 3 3 c \nc 5 5 4 5 5 5 4 b 5 5 c 3 3 c . \nb 5 4 b 4 4 4 4 b b 5 c b b . . \nc 4 5 5 b 4 b 5 5 5 4 c 4 5 b . \nc 5 5 5 c 4 c 5 5 5 c 4 c 5 c . \nc 5 5 5 5 c 5 5 5 5 c 4 c 5 c . \n. c c c c c c c c c . . c c c . \n`;\n            case \"image2\":\n            case \"fin\":return img`\n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . f f f f . . . . . . . \n. . . . f f f c c f f . . . . . \n. . . . f b b d d c f f . . . . \n. . . . . f b b d d c f . . . . \n. . . . . f c b b c c f f . . . \n. . . . f f c c c c c c f . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n. . . . . . . . . . . . . . . . \n`;\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"animation\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"animated enemy\":\n            case \"anim3\":return [img`\n..............fc..............\n...............f..............\n...............f..............\n...9...........f..............\n............fffff.............\n............f5555ff...........\n.........fff555554f..........9\n.........f5555555fffff........\n........f45555555544bffff..bb.\n.bb....f4545cc555c555c554f..b.\n...b..f4545c91c5c9c5c9c544ffbf\n.bb.bbf4445c99c55c555c5544ffbf\n...b..f44445cc55555555444f..b.\n.bb....f444455555544444ffc..bb\n........ff444444444ffff.......\n.........fffffffcfff..........\n`, img`\n..9...........fc..............\n...............f..............\n...............f..............\n...............f..............\n............fffff...........9.\n............f5555ff...........\n.........fff555554f...........\n.........f5555555fffff........\n.b......f45555555544bffff.....\n..b....f4545cc555c555c554f.bb.\n...b..f4545c91c5c9c5c9c544ffbf\n.bb.bbf4445c99c55c555c5544ffbf\n...b..f44445cc55555555444f..bb\n..b....f444455555544444ffc....\n.b......ff444444444ffff.......\n.........fffffffcfff..........\n`, img`\n..............fc..............\n...............f..............\n...............f.............9\n...............f..............\n............fffff.............\n............f5555ff...........\n.........fff555554f...........\n.9.......f5555555fffff........\n........f45555555544bffff.....\n.bb....f4545cc555c555c554f....\n...b..f4545c91c5c9c5c9c544ffbf\n.bb.bbf4445c99c55c555c5544ffbb\n...b..f44445cc55555555444f....\n.bb....f444455555544444ffc....\n........ff444444444ffff.......\n.........fffffffcfff..........\n`, img`\n..............fc...........9..\n...............f..............\n...............f..............\n...............f..............\n............fffff.............\n..9.........f5555ff...........\n.........fff555554f...........\n.........f5555555fffff........\n.b......f45555555544bffff.....\n..b....f4545cc555c555c554f....\n...b..f4545c91c5c9c5c9c544ffbb\n.bb.bbf4445c99c55c555c5544ffbf\n...b..f44445cc55555555444f....\n..b....f444455555544444ffc....\n.b......ff444444444ffff.......\n.........fffffffcfff..........\n`, img`\n..............fc..............\n...............f..............\n...............f..............\n.9.............f..............\n............fffff.............\n............f5555ff...........\n.........fff555554f...........\n.........f5555555fffff........\n.b......f45555555544bffff.....\n..b....f4545cc555c555c554f..bb\n...b..f4545c91c5c9c5c9c544ffbf\n.bb.bbf4445c99c55c555c5544ffbf\n...b..f44445cc55555555444f.bb.\n..b....f444455555544444ffc....\n.b......ff444444444ffff.......\n.........fffffffcfff..........\n`];\n            case \"animated food\":\n            case \"anim4\":return [img`\n. . . . . . . . . . . . . . . . \n. . . . . . . . c c c c . . . . \n. . . . . . c c d d d d c . . . \n. . . . . c c c c c c d c . . . \n. . . . c c 4 4 4 4 d c c . . . \n. . . c 4 d 4 4 4 4 4 1 c . c c \n. . c 4 4 4 1 4 4 4 4 d 1 c 4 c \n. c 4 4 4 4 1 4 4 4 4 4 1 c 4 c \nf 4 4 4 4 4 1 4 4 4 4 4 1 4 4 f \nf 4 4 4 f 4 1 c c 4 4 4 1 f 4 f \nf 4 4 4 4 4 1 4 4 f 4 4 d f 4 f \n. f 4 4 4 4 1 c 4 f 4 d f f f f \n. . f f 4 d 4 4 f f 4 c f c . . \n. . . . f f 4 4 4 4 c d b c . . \n. . . . . . f f f f d d d c . . \n. . . . . . . . . . c c c . . . \n`, img`\n. . . . . . . . . . . . . . . . \n. . . . . . . c c c c c . . . . \n. . . . . . c d d d d d c . . . \n. . . . . . c c c c c d c . . . \n. . . . . c 4 4 4 4 d c c . . . \n. . . . c d 4 4 4 4 4 1 c . . . \n. . . c 4 4 1 4 4 4 4 4 1 c . . \n. . c 4 4 4 4 1 4 4 4 4 1 c c c \n. c 4 4 4 4 4 1 c c 4 4 1 4 4 c \n. c 4 4 4 4 4 1 4 4 f 4 1 f 4 f \nf 4 4 4 4 f 4 1 c 4 f 4 d f 4 f \nf 4 4 4 4 4 4 1 4 f f 4 f f 4 f \n. f 4 4 4 4 1 4 4 4 4 c b c f f \n. . f f f d 4 4 4 4 c d d c . . \n. . . . . f f f f f c c c . . . \n. . . . . . . . . . . . . . . . \n`, img`\n. . . . . . . . c c c c . . . . \n. . . . . . c c d d d d c . . . \n. . . . . c c c c c c d c . . . \n. . . . c c 4 4 4 4 d c c . c c \n. . . c 4 d 4 4 4 4 4 1 c c 4 c \n. . c 4 4 4 1 4 4 4 4 d 1 c 4 f \n. c 4 4 4 4 1 4 4 4 4 4 1 4 4 f \nf 4 4 4 4 4 1 1 c f 4 4 1 f 4 f \nf 4 4 4 f 4 1 c 4 f 4 4 1 f 4 f \nf 4 4 4 4 4 1 4 4 f 4 4 d f f f \n. f 4 4 4 4 1 c c 4 4 d f f . . \n. . f f 4 d 4 4 4 4 4 c f . . . \n. . . . f f 4 4 4 4 c d b c . . \n. . . . . . f f f f d d d c . . \n. . . . . . . . . . c c c . . . \n. . . . . . . . . . . . . . . . \n`, img`\n. . . . . . . . . . . . . . . . \n. . . . . . . . . c c c c . . . \n. . . . . . . c c d d d d c . . \n. . . . . c c c c c c d d c . . \n. . . c c c 4 4 4 4 d c c c c c \n. . c 4 4 1 4 4 4 4 4 1 c c 4 f \n. c 4 4 4 4 1 4 4 4 4 d 1 f 4 f \nf 4 4 4 4 4 1 4 4 4 4 4 1 f 4 f \nf 4 4 f 4 4 1 4 c f 4 4 1 4 4 f \nf 4 4 4 4 4 1 c 4 f 4 4 1 f f f \n. f 4 4 4 4 1 4 4 f 4 4 d f . . \n. . f 4 4 1 4 c c 4 4 d f . . . \n. . . f d 4 4 4 4 4 4 c f . . . \n. . . . f f 4 4 4 4 c d b c . . \n. . . . . . f f f f d d d c . . \n. . . . . . . . . . c c c . . . \n`];\n            case \"swim left\":\n            case \"anim2\":return [img`\n.............ccfff..............\n...........ccddbcf..............\n..........ccddbbf...............\n..........fccbbcf...............\n.....fffffccccccff.........ccc..\n...ffbbbbbbbcbbbbcfff....ccbbc..\n..fbbbbbbbbcbcbbbbcccff.cdbbc...\nffbbbbbbffbbcbcbbbcccccfcdbbf...\nfbcbbb11ff1bcbbbbbcccccffbbf....\nfbbb11111111bbbbbcccccccbbcf....\n.fb11133cc11bbbbcccccccccccf....\n..fccc31c111bbbcccccbdbffbbcf...\n...fc13c111cbbbfcddddcc..fbbf...\n....fccc111fbdbbccdcc.....fbbf..\n........ccccfcdbbcc........fff..\n.............fffff..............\n`, img`\n.............ccfff..............\n............cddbbf..............\n...........cddbbf...............\n..........fccbbcf............ccc\n....ffffffccccccff.........ccbbc\n..ffbbbbbbbbbbbbbcfff.....cdbbc.\nffbbbbbbbbbcbcbbbbcccff..cddbbf.\nfbcbbbbbffbbcbcbbbcccccfffdbbf..\nfbbb1111ff1bcbcbbbcccccccbbbcf..\n.fb11111111bbbbbbcccccccccbccf..\n..fccc33cc11bbbbccccccccfffbbcf.\n...fc131c111bbbcccccbdbc...fbbf.\n....f33c111cbbbfdddddcc.....fbbf\n.....ff1111fbdbbfddcc........fff\n.......cccccfbdbbfc.............\n.............fffff..............\n`, img`\n..............cfff..............\n............ccddbf..............\n...........cbddbff.........ccc..\n..........fccbbcf.........cbbc..\n...fffffffccccccff.......cdbc...\n.ffcbbbbbbbbbbbbbcfff....cdbf...\nfcbbbbbbbbbcbbbbbbcccff.cdbf....\nfbcbbbbffbbbcbcbbbcccccffdcf....\nfbb1111ffbbbcbcbbbccccccbbcf....\n.fb11111111bbcbbbccccccccbbcf...\n..fccc33cb11bbbbcccccccfffbbf...\n...fc131c111bbbcccccbdbc..fbbf..\n....f33c111cbbccdddddbc....fff..\n.....ff1111fdbbccddbcc..........\n.......cccccfdbbbfcc............\n.............fffff..............\n`, img`\n.............ccfff..............\n............cddbbf..............\n...........cddbbf...............\n..........fccbbcf............ccc\n....ffffffccccccff.........ccbbc\n..ffbbbbbbbbbbbbbcfff.....cdbbc.\nffbbbbbbbbbcbcbbbbcccff..cddbbf.\nfbcbbbbbffbbcbcbbbcccccfffdbbf..\nfbbb1111ff1bcbcbbbcccccccbbbcf..\n.fb11111111bbbbbbcccccccccbccf..\n..fccc33cc11bbbbccccccccfffbbcf.\n...fc131c111bbbcccccbdbc...fbbf.\n....f33c111cbbbfdddddcc.....fbbf\n.....ff1111fbdbbfddcc........fff\n.......cccccfbdbbfc.............\n.............fffff..............\n`];\n            case \"swim right\":\n            case \"anim1\":return [img`\n..............fffcc.............\n..............fcbddcc...........\n...............fbbddcc..........\n...............fcbbccf..........\n..ccc.........ffccccccfffff.....\n..cbbcc....fffcbbbbcbbbbbbbff...\n...cbbdc.ffcccbbbbcbcbbbbbbbbf..\n...fbbdcfcccccbbbcbcbbffbbbbbbff\n....fbbffcccccbbbbbcb1ff11bbbcbf\n....fcbbcccccccbbbbb11111111bbbf\n....fcccccccccccbbbb11cc33111bf.\n...fcbbffbdbcccccbbb111c13cccf..\n...fbbf..ccddddcfbbbc111c31cf...\n..fbbf.....ccdccbbdbf111cccf....\n..fff........ccbbdcfcccc........\n..............fffff.............\n`, img`\n..............fffcc.............\n..............fbbddc............\n...............fbbddc...........\nccc............fcbbccf..........\ncbbcc.........ffccccccffffff....\n.cbbdc.....fffcbbbbbbbbbbbbbff..\n.fbbddc..ffcccbbbbcbcbbbbbbbbbff\n..fbbdfffcccccbbbcbcbbffbbbbbcbf\n..fcbbbcccccccbbbcbcb1ff1111bbbf\n..fccbcccccccccbbbbbb11111111bf.\n.fcbbfffccccccccbbbb11cc33cccf..\n.fbbf...cbdbcccccbbb111c131cf...\nfbbf.....ccdddddfbbbc111c33f....\nfff........ccddfbbdbf1111ff.....\n.............cfbbdbfccccc.......\n..............fffff.............\n`, img`\n..............fffc..............\n..............fbddcc............\n..ccc.........ffbddbc...........\n..cbbc.........fcbbccf..........\n...cbdc.......ffccccccfffffff...\n...fbdc....fffcbbbbbbbbbbbbbcff.\n....fbdc.ffcccbbbbbbcbbbbbbbbbcf\n....fcdffcccccbbbcbcbbbffbbbbcbf\n....fcbbccccccbbbcbcbbbff1111bbf\n...fcbbccccccccbbbcbb11111111bf.\n...fbbfffcccccccbbbb11bc33cccf..\n..fbbf..cbdbcccccbbb111c131cf...\n..fff....cbdddddccbbc111c33f....\n..........ccbddccbbdf1111ff.....\n............ccfbbbdfccccc.......\n..............fffff.............\n`, img`\n..............fffcc.............\n..............fbbddc............\n...............fbbddc...........\nccc............fcbbccf..........\ncbbcc.........ffccccccffffff....\n.cbbdc.....fffcbbbbbbbbbbbbbff..\n.fbbddc..ffcccbbbbcbcbbbbbbbbbff\n..fbbdfffcccccbbbcbcbbffbbbbbcbf\n..fcbbbcccccccbbbcbcb1ff1111bbbf\n..fccbcccccccccbbbbbb11111111bf.\n.fcbbfffccccccccbbbb11cc33cccf..\n.fbbf...cbdbcccccbbb111c131cf...\nfbbf.....ccdddddfbbbc111c33f....\nfff........ccddfbbdbf1111ff.....\n.............cfbbdbfccccc.......\n..............fffff.............\n`];\n            case \"shooting shark\":\n            case \"WRHzQ06n]_D#g\":return [img`\n..............fffcc.................\n..............fbbddc................\n...............fbbddc...............\nccc............fcbbccf..............\ncbbcc.........ffccccccffffff........\n.cbbdc.....fffcbbbbbbbbbbbbbff......\n.fbbddc..ffcccbbbbcbcbbbbbbbbbff....\n..fbbdfffcccccbbbcbcbbffbbbbbcbf....\n..fcbbbcccccccbbbcbcb1ff1111bbbf....\n..fccbcccccccccbbbbbb11111111bf.....\n.fcbbfffccccccccbbbb11cc33cccf......\n.fbbf...cbdbcccccbbb111c131cf.......\nfbbf.....ccdddddfbbbc111c33f........\nfff........ccddfbbdbf1111ff.........\n.............cfbbdbfccccc...........\n..............fffff.................\n`, img`\n..............fffcc.................\n..............fbbddc................\n...............fbbddc...............\n...............fcbbccffffff.........\n..............ffcccbbbbbbbbfff......\nccccc......fffcbbbbbbbbbbbbbbbf.....\ncbbbdc...ffcccbbbbcbcbffbbbbbcb.....\n.cbbddcffcccccbbbcbcbbff1111bbb.....\n..fbbdbcccccccbbbcbcb11111111bf.....\n..fcbbcccccccccbbbbbb11c33cccf......\n..fccbffccccccccbbbb11cc131cf.......\n.fcbbf..cbdbcccccbbb1111c33f........\n.fbbf....ccdddddfbbbc1111ff.........\nfbbf.......ccddfbbdbf1ccc...........\nfff..........cfbbdbfcc..............\n..............fffff.................\n`, img`\n.............fffcc..................\n.............fbbddc.................\n..............fbbddfffffffff........\n..............fcbcfbbbbbbbbbf.......\n...........ffffccbbffb111cbbf.......\nccccc....ffcccbbbbbff111111bf.......\ncbbbdc..fccccbbcbcbb1133cc1f........\n.cbbddcfcccccbcbcbbb1c131ccf........\n..fbbdbccccccbcbcbbb111111f.........\n..fcbbccccccccbbbbb1111111f.........\n..fccbffcccccccbbbb111111f..........\n.fcbbf.cbdbcccccbbbc1111c...........\n.fbbf...cddddddfbbbc11cc............\nfbbf.....ccdddfbbdbffc..............\nfff........ccfbbdbf.................\n.............fffff..................\n`, img`\n...........fffcc....................\n...........fbbbbcfffffffff..........\n............fbfffbbbbbbbbbf.........\n............ffbbbbffb111bbf.........\n..........ffcbbbbbff11111bf.........\n.........fcccbcbcbb11cccc1f.........\nccccc...fcccbcbcbbb1c1c1cf..........\ncbbddccfccccbcbcbbb1333c............\n.ccbddbcccccbbbbbbb1c333c...........\n..ccbbcccccccbbbbb11c133c...........\n..fccbffccccccbbbb111c31cc..........\n..fccf.cbbcccccbbbc111111c..........\n.fcbbf..cdddddfbbbc1111cc...........\n.fbbf....cdddfbbdbffccc.............\nfbbf......ccfbbdbf..................\nfff.........fffff...................\n`, img`\n..........fffcc...fffffff...........\n..........fbbbbcffbbbbbbbf..........\n...........fbffbbbbb111bbf..........\n...........ffbbbbff11111bf..........\n.........ffcbbbbbff1cccc1f..........\n........fcccbcbcbb1c1c1cff..........\nccccc..fcccbcbcbbb1333ccf...........\ncbbddcfccccbcbcbbb1c333c............\n.ccbddcccccbbbbbbb1c333c............\n..ccbbccccccbbbbb11c333c............\n..fccbfccccccbbbb11c133cc...........\n..fccfcbbcccccbbbc11c31cc...........\n.fcbbf.cdddddfbbbc111111c...........\n.fbbf...cdddfbbdbf1111cc............\nfbbf.....ccfbbdbfffccc..............\nfff........fffff....................\n`, img`\n....................................\n....................................\n....................................\n...............ffffcc...............\n...............fbbbddc..............\n................fbbbddcffffff.......\nccccc.......fffcbbbbbbbbbbbbbff.....\ncbbbdc....ffcccbbbbbcbcbbbbbbbbff...\n.cbbddcfffcccccbbbbcbbcbbbbbbbbbbf..\n..fbbdbccccccccbbbbcbcbbbbbbbbbbcbf.\n..fcbbccccccccccbbbbbcbbfffbbbbbbbf.\n..fccbffcbcccccccbbbbcbbfff1111bbff.\n.fcbbf..ccbbbccccccbbbb111111111ff..\nfbbff.....cccbddfbbbdb111ccccccc....\nfff..........ccfbbbdbfcccccc........\n...............ffffff...............\n`];\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n",
  "main.blocks": "<xml xmlns=\"https://developers.google.com/blockly/xml\"><variables><variable id=\";=7lAS%p|sLtN}r,6+zx\">projectile</variable><variable id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</variable><variable id=\"%smx33(Ul|1?/_tHKAwx\">myEnemy</variable><variable id=\"r,MaLOY#@!]M:|q]?VeI\">myFood</variable><variable id=\"cOo587Nod!wNUHk.UBeA\">myDecor</variable><variable id=\"eLJczBY$O$@9m9GhR;=o\">myPowerup</variable><variable type=\"KIND_SpriteKind\" id=\"E!FSfzFxF@uA}:~#?An(\">Decoration</variable><variable type=\"KIND_SpriteKind\" id=\"y%d7U{n}{dXb(wFnYQ1T\">Player</variable><variable type=\"KIND_SpriteKind\" id=\"2V|4j9rUB*nC@2+x%I2.\">Projectile</variable><variable type=\"KIND_SpriteKind\" id=\"pA;-[yxx-Sv9j;/+S5r}\">Food</variable><variable type=\"KIND_SpriteKind\" id=\"f7A_S}Ksa)/Q!#^xj/8f\">Enemy</variable><variable type=\"KIND_SpriteKind\" id=\"Xp8OLW;~:[`uL,ZN?m^*\">PowerUp</variable></variables><block type=\"pxt-on-start\" x=\"0\" y=\"0\"><statement name=\"HANDLER\"><block type=\"gamesetbackgroundcolor\"><value name=\"color\"><shadow type=\"colorindexpicker\"><field name=\"index\">8</field></shadow></value><next><block type=\"gamesetbackgroundimage\"><value name=\"img\"><shadow type=\"background_image_picker\"><field name=\"img\">assets.image`ocean1`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.Ik6joQcYX!hh)DS[|_?1\"}}</data></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`shark`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.~I/xlSOb!:ehNE!zTIaq\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value></block></value><next><block type=\"game_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><next><block type=\"spritesetsetstayinscreen\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"gamecountdown\"><value name=\"duration\"><shadow type=\"math_number\"><field name=\"NUM\">15</field></shadow></value><next><block type=\"controls_repeat_ext\"><value name=\"TIMES\"><shadow type=\"math_whole_number\"><field name=\"NUM\">10</field></shadow></value><statement name=\"DO\"><block type=\"variables_set\"><field name=\"VAR\" id=\"cOo587Nod!wNUHk.UBeA\">myDecor</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`decoration`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.?]c;BAWx@CPp7,Xc!||y\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Decoration</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"cOo587Nod!wNUHk.UBeA\">myDecor</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">160</field></shadow></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"><field name=\"index\">96</field></shadow></value></block></next></block></statement><next><block type=\"run_image_animation\"><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><value name=\"frames\"><shadow type=\"animation_editor\"><field name=\"frames\">assets.animation`swim right`</field><data>{\"commentRefs\":[],\"fieldData\":{\"frames\":\"myAnimations..anim1\"}}</data></shadow></value><value name=\"frameInterval\"><shadow type=\"timePicker\"><field name=\"ms\">200</field></shadow></value><value name=\"loop\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></statement></block><block type=\"gamecountdownevent\" x=\"847\" y=\"0\"><statement name=\"HANDLER\"><block type=\"gameOver\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"win\"><shadow type=\"toggleWinLose\"><field name=\"win\">true</field></shadow></value></block></statement></block><block type=\"gameinterval\" x=\"1214\" y=\"0\"><value name=\"period\"><shadow type=\"timePicker\"><field name=\"ms\">2100</field></shadow></value><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"r,MaLOY#@!]M:|q]?VeI\">myFood</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`food`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.]uSp,Yb2U]iY\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Food</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"r,MaLOY#@!]M:|q]?VeI\">myFood</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"scenescreenwidth\"></block></value><value name=\"y\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">5</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">115</field></shadow></value></block></value><next><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.vx@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"r,MaLOY#@!]M:|q]?VeI\">myFood</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">-75</field></shadow></value></block></next></block></next></block></statement></block><block type=\"gameinterval\" x=\"2065\" y=\"0\"><value name=\"period\"><shadow type=\"timePicker\"><field name=\"ms\">2500</field></shadow></value><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"%smx33(Ul|1?/_tHKAwx\">myEnemy</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`enemy`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.c^#HB{wS5hM[\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Enemy</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"%smx33(Ul|1?/_tHKAwx\">myEnemy</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"></shadow><block type=\"scenescreenwidth\"></block></value><value name=\"y\"><shadow type=\"positionPicker\"></shadow><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">120</field></shadow></value></block></value><next><block type=\"spriteFollowOtherSprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"1\" _input_init=\"true\"></mutation><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"%smx33(Ul|1?/_tHKAwx\">myEnemy</field></block></value><value name=\"target\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><value name=\"speed\"><shadow type=\"math_number\"><field name=\"NUM\">30</field></shadow></value></block></next></block></next></block></statement></block><block type=\"function_definition\" x=\"1290\" y=\"330\"><mutation name=\"Powerup\" functionid=\"Pjg({[Qkxm4$x-BYB,,$\"><arg name=\"mySprite\" id=\"|6EK:bG1/yHHs=bG;mJH\" type=\"Sprite\"></arg></mutation><field name=\"function_name\">Powerup</field><value name=\"|6EK:bG1/yHHs=bG;mJH\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">mySprite</field></shadow></value><statement name=\"STACK\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.bubbles</field><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">mySprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow></value><next><block type=\"controls_if\"><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"percentchance\"><value name=\"percentage\"><shadow type=\"math_number_minmax\"><mutation min=\"0\" max=\"Infinity\" label=\"Percentage\" precision=\"0\"></mutation><field name=\"SLIDER\">25</field></shadow></value></block></value><statement name=\"DO0\"><block type=\"variables_set\"><field name=\"VAR\" id=\"eLJczBY$O$@9m9GhR;=o\">myPowerup</field><value name=\"VALUE\"><shadow xmlns=\"http://www.w3.org/1999/xhtml\" type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`fin`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image2\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">PowerUp</field></shadow></value></block></value><next><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.x@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"eLJczBY$O$@9m9GhR;=o\">myPowerup</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">mySprite</field></block></value></block></value><next><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.y@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"eLJczBY$O$@9m9GhR;=o\">myPowerup</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.y</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">mySprite</field></block></value></block></value><next><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.vy@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"eLJczBY$O$@9m9GhR;=o\">myPowerup</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">-25</field></shadow></value></block></next></block></next></block></next></block></statement></block></next></block></statement></block><block type=\"spritesoverlap\" x=\"2070\" y=\"490\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">PowerUp</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.bubbles</field><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow></value><next><block type=\"hudChangeLifeBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">5</field></shadow></value></block></next></block></next></block></statement></block><block type=\"variables_get\" disabled=\"true\" x=\"2009\" y=\"559\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block><block type=\"variables_get\" disabled=\"true\" x=\"1814\" y=\"674\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block><block type=\"keyonevent\" x=\"250\" y=\"790\"><field name=\"button\">controller.A</field><field name=\"event\">ControllerButtonEvent.Pressed</field><statement name=\"HANDLER\"><block type=\"run_image_animation\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block></value><value name=\"frames\"><block type=\"animation_editor\"><field name=\"frames\">assets.animation`shooting shark`</field><data>{\"commentRefs\":[],\"fieldData\":{\"frames\":\"[XxxVj..WRHzQ06n]_D#g\"}}</data></block></value><value name=\"frameInterval\"><shadow type=\"timePicker\"><field name=\"ms\">50</field></shadow></value><value name=\"loop\"><shadow type=\"toggleOnOff\"><field name=\"on\">false</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\";=7lAS%p|sLtN}r,6+zx\">projectile</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreateprojectilefromsprite\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`laser`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.=NL1D;jj+wTeW(}r0(uZ\"}}</data></shadow></value><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">200</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value></block></value></block></next></block></statement></block><block type=\"variables_get\" disabled=\"true\" x=\"1808\" y=\"723\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block><block type=\"keyonevent\" x=\"933\" y=\"829\"><field name=\"button\">controller.right</field><field name=\"event\">ControllerButtonEvent.Pressed</field><statement name=\"HANDLER\"><block type=\"run_image_animation\"><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><value name=\"frames\"><shadow type=\"animation_editor\"><field name=\"frames\">assets.animation`swim right`</field><data>{\"commentRefs\":[],\"fieldData\":{\"frames\":\"myAnimations..anim1\"}}</data></shadow></value><value name=\"frameInterval\"><shadow type=\"timePicker\"><field name=\"ms\">200</field></shadow></value><value name=\"loop\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value></block></statement></block><block type=\"keyonevent\" x=\"1290\" y=\"829\"><field name=\"button\">controller.left</field><field name=\"event\">ControllerButtonEvent.Pressed</field><statement name=\"HANDLER\"><block type=\"run_image_animation\"><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow></value><value name=\"frames\"><shadow type=\"animation_editor\"><field name=\"frames\">assets.animation`swim left`</field><data>{\"commentRefs\":[],\"fieldData\":{\"frames\":\"myAnimations..anim2\"}}</data></shadow></value><value name=\"frameInterval\"><shadow type=\"timePicker\"><field name=\"ms\">200</field></shadow></value><value name=\"loop\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value></block></statement></block><block type=\"spritesoverlap\" x=\"1637\" y=\"829\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Projectile</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Enemy</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></block></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value><next><block type=\"function_call\"><mutation name=\"Powerup\" functionid=\"Pjg({[Qkxm4$x-BYB,,$\"><arg name=\"mySprite\" id=\"|6EK:bG1/yHHs=bG;mJH\" type=\"Sprite\"></arg></mutation><value name=\"|6EK:bG1/yHHs=bG;mJH\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></shadow><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value></block></next></block></next></block></statement></block><block type=\"variables_get\" disabled=\"true\" x=\"2259\" y=\"807\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block><block type=\"spritesoverlap\" x=\"-10\" y=\"1150\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Enemy</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"0\" _input_init=\"false\"></mutation><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><next><block type=\"hudChangeLifeBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">-1</field></shadow></value><next><block type=\"camerashake\"><value name=\"amplitude\"><shadow type=\"math_number_minmax\"><mutation min=\"1\" max=\"8\" label=\"Number\" precision=\"0\"></mutation><field name=\"SLIDER\">4</field></shadow></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">500</field></shadow></value></block></next></block></next></block></statement></block><block type=\"spritedestroy\" disabled=\"true\" x=\"1810\" y=\"1070\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.bubbles</field><value name=\"sprite\"><block type=\"argument_reporter_custom\" disabled=\"true\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\" disabled=\"true\"><field name=\"ms\">100</field></shadow></value></block><block type=\"spritesoverlap\" x=\"773\" y=\"1140\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Food</field></shadow></value><statement name=\"HANDLER\"><block type=\"spritedestroy\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"effect\">effects.disintegrate</field><value name=\"sprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"></mutation><field name=\"VALUE\">otherSprite</field></block></value><value name=\"duration\"><shadow type=\"timePicker\"><field name=\"ms\">100</field></shadow></value><next><block type=\"hudChangeScoreBy\"><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value></block></next></block></statement></block><block type=\"variables_get\" disabled=\"true\" x=\"1574\" y=\"1140\"><field name=\"VAR\" id=\"%9xF?sJl}OB/^rn$zDO8\">mySprite</field></block></xml>",
  "main.ts": "namespace SpriteKind {\n    export const Decoration = SpriteKind.create()\n    export const PowerUp = SpriteKind.create()\n}\ncontroller.A.onEvent(ControllerButtonEvent.Pressed, function () {\n    animation.runImageAnimation(\n    mySprite,\n    assets.animation`shooting shark`,\n    50,\n    false\n    )\n    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)\n})\ncontroller.left.onEvent(ControllerButtonEvent.Pressed, function () {\n    animation.runImageAnimation(\n    mySprite,\n    assets.animation`swim left`,\n    200,\n    true\n    )\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function (sprite, otherSprite) {\n    otherSprite.destroy(effects.bubbles, 100)\n    info.changeLifeBy(1)\n    info.changeScoreBy(5)\n})\ninfo.onCountdownEnd(function () {\n    game.over(true)\n})\ncontroller.right.onEvent(ControllerButtonEvent.Pressed, function () {\n    animation.runImageAnimation(\n    mySprite,\n    assets.animation`swim right`,\n    200,\n    true\n    )\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function (sprite, otherSprite) {\n    otherSprite.destroy(effects.disintegrate, 100)\n    info.changeScoreBy(1)\n})\nsprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function (sprite, otherSprite) {\n    sprite.destroy()\n    info.changeScoreBy(2)\n    Powerup(otherSprite)\n})\nfunction Powerup (mySprite: Sprite) {\n    mySprite.destroy(effects.bubbles, 100)\n    if (Math.percentChance(25)) {\n        myPowerup = sprites.create(assets.image`fin`, SpriteKind.PowerUp)\n        myPowerup.x = mySprite.x\n        myPowerup.y = mySprite.y\n        myPowerup.vy = -25\n    }\n}\nsprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite) {\n    otherSprite.destroy()\n    info.changeLifeBy(-1)\n    scene.cameraShake(4, 500)\n})\nlet myFood: Sprite = null\nlet myEnemy: Sprite = null\nlet myPowerup: Sprite = null\nlet projectile: Sprite = null\nlet myDecor: Sprite = null\nlet mySprite: Sprite = null\nscene.setBackgroundColor(8)\nscene.setBackgroundImage(assets.image`ocean1`)\nmySprite = sprites.create(assets.image`shark`, SpriteKind.Player)\ncontroller.moveSprite(mySprite)\nmySprite.setStayInScreen(true)\ninfo.startCountdown(15)\nfor (let index = 0; index < 10; index++) {\n    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)\n    myDecor.setPosition(randint(0, 160), 96)\n}\nanimation.runImageAnimation(\nmySprite,\nassets.animation`swim right`,\n200,\ntrue\n)\ngame.onUpdateInterval(2500, function () {\n    myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)\n    myEnemy.setPosition(scene.screenWidth(), randint(0, 120))\n    myEnemy.follow(mySprite, 30)\n})\ngame.onUpdateInterval(2100, function () {\n    myFood = sprites.create(assets.image`food`, SpriteKind.Food)\n    myFood.setPosition(scene.screenWidth(), randint(5, 115))\n    myFood.vx = -75\n})\n",
  "pxt.json": "{\n    \"name\": \"Mr. Wender's Final Feeding Frenzy\",\n    \"description\": \"\",\n    \"dependencies\": {\n        \"device\": \"*\",\n        \"Timers\": \"github:microsoft/arcade-timers#v1.1.0\"\n    },\n    \"files\": [\n        \"main.blocks\",\n        \"main.ts\",\n        \"README.md\",\n        \"assets.json\",\n        \"tilemap.g.jres\",\n        \"tilemap.g.ts\",\n        \"images.g.jres\",\n        \"images.g.ts\"\n    ],\n    \"targetVersions\": {\n        \"branch\": \"v1.8.5\",\n        \"tag\": \"v1.8.5\",\n        \"commits\": \"https://github.com/microsoft/pxt-arcade/commits/dcf9a020191b5d43e6a52beba4b97bad0beabb85\",\n        \"target\": \"1.8.5\",\n        \"pxt\": \"7.4.12\"\n    },\n    \"preferredEditor\": \"blocksprj\"\n}\n",
  "tilemap.g.jres": "{\n    \"transparency16\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myTiles\"\n    }\n}",
  "tilemap.g.ts": "// Auto-generated code. Do not edit.\nnamespace myTiles {\n    //% fixedInstance jres blockIdentity=images._tile\n    export const transparency16 = image.ofBuffer(hex``);\n\n    helpers._registerFactory(\"tile\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"transparency16\":return transparency16;\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n"
}

```


