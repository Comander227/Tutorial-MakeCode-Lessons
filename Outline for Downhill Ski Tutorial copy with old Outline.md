# Downhill Ski Game Jam 

## Setting your background
### Set up your background to white for your snow
- :tree: Add a set background block from the ``||scene:scene||`` section to your ``||loops:on start||`` container
	
	```blocks
	scene.setBackgroundColor(1)
	```


## Creating your Skier Sprite
### Setting the Player Sprite

- :paper plane: Next we are going to add our ``||sprites:set mySprite to sprite [] of kind Player||`` to our ``||loops:on start||`` contianer. 
	
	```blocks
		scene.setBackgroundColor(1); 
		let mySprite = sprites.create(img``,SpriteKind.Player)
	```

## Giving our Skier an image
### Adding the Skier asset 
- :paint brush: Click on the grey box in the ``||sprites:set mySprite to [] of kind Player||`` block. 
Next select the My Assets tab and click on the Skier Asset. 
Then click done. 

```blocks
	scene.setBackgroundColor(1)
	let mySprite = sprites.create(assets.image`Skier`,SpriteKind.Player)
```

## Moving our Skier
### Asignning controllers to our sprite 
- :game: Now we are going to add our ``||controller:move mySprite with buttons||`` block to our ``||loops:on start||`` container. 

```blocks
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
```
## Don't lose the Skier
### Keeping our Skier on screen 
- :paper plane: Add a ``||sprites:set mySprite stay in screen||`` block from the ``||sprites:sprites||`` category to our ``||loops:on start||`` container. 

```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
```

## Where should our skier start?
### Setting the Skier's position
- :paper plane: Add a ``||sprites: set mySprite position to x() y()||`` from the ``||sprites:sprites||`` category to our ``||loops:on start||`` container. 

```blocks
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
```



## Creating our Rock Obstacle
### Setting up the container
- :cirlce: Grab an ``||game:on game update every 500 ms||`` container from the ``||game:game||`` category. 

```blocks
game.onUpdateInterval(500, function () {
	
})
```

## Establishing our Rock
### Setting the Rock Sprite
- :paper plane: Add a ``||sprites:set mySprite to sprite [] of kind Player||`` block to the ``||game:update game every 500 ms||`` container. 
- :paint brush: Click on the grey box to open the sprite editor. Open the **My Assets** tab. Select the **rock** image. 
- :mouse pointer: Change the sprite kind from **Player** to a new kind called **Rock**

```blocks
let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
})
```





6.Create Obstcales
-Creating the Rock
	-Grab an on game update every 500 ms container
		game.onUpdateInterval(500, function () {
	
})
	-Add a set mySprite block. Rename the sprite to Rock. Create a new SpriteKind called Rocks. 
	let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
     Rocks = sprites.create(img``, SpriteKind.Rock)
})
	-assign the rock asset to the rock sprite we just created. 
	let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
})
	-Grab a set position block and place it in the container. 
	-Change mySprite to Rocks
	
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
let Rocks: Sprite = null
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(0, 0)
})

	-Grab a screen hight circle and place that in the y value. 
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(0, scene.screenHeight())
})

	-Grab a pick random circle from the math category and place it in the x value. 
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, 10), scene.screenHeight())
})

	-Place a screen width circle in the max value of the pick random circle. 
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
})

	-Grab a set mySprite vx and vy block and place it in the on game update every 500 ms seconds container. 
	-change mySprite to Rocks
	-set vx to 0
	-set vy to a negative value. -50 works well. 
	game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
})

	-Grab the set mySprite auto destory block and place it in the on game update every 500 ms container. 
	-Change mySpite to Rocks.
	-Set the value to true.
game.onUpdateInterval(500, function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    mySprite.setFlag(SpriteFlag.AutoDestroy, true)
})

	-Lets adjust the speed of this using a variable that we can manipulate.
	-Lets create a new variable to use as our speed. 
	-In the variable section click on the button that says "make a variable"
	-Name the new variable SkierSpeed.
	-Set the value to -20
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let SkierSpeed = -20

	-Create another variable and name it RockSpawnTimer
	-set the value to 2000
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let SkierSpeed = -20
let RockSpawnTime = 2000


	-To make this function work we need to change the way the spawn code for the rock works.
	-Replace the on game update every 500ms seconds with a forever loop from the loops section.
	forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    mySprite.setFlag(SpriteFlag.AutoDestroy, true)
})
	-Add a pause block from the loops section to the bottom of the forever loop. 
	forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    mySprite.setFlag(SpriteFlag.AutoDestroy, true)
    pause(100)
})

	-Set the pause value to the RockSpawnTimer variable circle.
	forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, -50)
    mySprite.setFlag(SpriteFlag.AutoDestroy, true)
    pause(RockSpawnTime)
})
	-Add the Skier Speed to the vy value of the Rocks sprite. 
	forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, SkierSpeed)
    mySprite.setFlag(SpriteFlag.AutoDestroy, true)
    pause(RockSpawnTime)
})

	-lets adjust the speed values so they change over time. 
	-Grab a new on game update every 500 ms container. 
	-Change the value to 3000
	game.onUpdateInterval(3000, function () {
	
})

	-Add a change SkierSpeed block from the variables group to the on game update every 3000ms contianer. 
	-Set the value to -5. 
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
})

	-We need to set a top speed for the skier.
	-Grab another set SkierSpeed block and place it under the change SkierSpeed Block.
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = 0
})

	-Add a grab max of 0 and 0 cirlce from the Math group.
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(0, 0)
})
	-Add a SkierSpeed varaible circle to the first max value space. 
	-Set the second value to be a desired skier speed max value. Rememeber it needs to be negative. -100 works. 
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
})

	-The same concept can be used to adjust the RockSpawnTime speed. 
	-Grab a change RockSpawnTime block and place it under the set SkierSpeed block. 
	-Set the value to -200
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
})
	-Grab another set RockSpawnTime block.
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    RockSpawnTime = 0
})

	- Grab another max of 0 and 0 cirlce and place it in the set RockSpawnTime vlaue space.
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    RockSpawnTime = Math.max(0, 0)
})
	-Grab a RockSpawnTime cirlce and place it in the first value space. 
	-change the second value to 500. 
	game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    RockSpawnTime = Math.max(RockSpawnTime, 500)
})


	-Now that we have set up the timers, lets set up the overlap code. 
	-Grab an on spirte of Player kind overlaps otherSprite of Player kind container and place it in the workspace. 
	-Change the otherSprite kind from Player to Rock.
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
	
})

	-If our skier crashes into a rock, we want them to lose a life and destory the rock. Let do that in steps. 
	-First lets destory the rock if it runs into our player. 
	-Add  destory block to the overlap code. 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    mySprite.destroy()
})
	-Next we need to use the local otherSprite variable from our overlap container to make sure that we destory the correct rock. 
	**insert GIF here**
	-Feel free to change the destory effect if you want. 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    otherSprite.destroy(effects.blizzard, 100)
})
	-Next lets take a life from our player. 
	-Add a change player life by -1 block from the info section into our overlap container. 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    otherSprite.destroy(effects.blizzard, 100)
    info.changeLifeBy(-1)
})
	
	-Since we make the player lose a life we need to tell the game what should happen when we run out of them. 
	-Add an on life zero container from the info category to the workspace.
	info.onLifeZero(function () {
})
	-Add a game over block from the game category to the on life zero container. 
	info.onLifeZero(function () {
    game.over(false)
})
	

	-Lets have our player score some points. 
	-Grab the on destory sprite of kind container from the sprites category. 
	-Change the kind from Player to Rocks.
	sprites.onDestroyed(SpriteKind.Rock, function (sprite) {
	
})
	-Add a change score by 1 block from the info category to the on destory sprite of Rock kind container. 
	sprites.onDestroyed(SpriteKind.Rock, function (sprite) {
    info.changeScoreBy(1)
})

	-Now we are going to set up an incentive for our player to pick up. 
	-Create a new variable by clicking the make a variable button in the variables section.
	-Name the variable PurpleGateTimer. 
	-Grab the set PurpleGateTimer block and add it to the on start container. 
	-Set the value to 5000
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000

	-Grab another forever loop from the loop category. 
	forever(function () {
	
})
	-Add the pause 100 ms block from the loop category to the top of the forever loop you just added. 
	forever(function () {
    pause(100)
})
	-Add the PurpleGateTimer variable circle from the varaiables category to the value in the pause block. 
	forever(function () {
    pause(PurpleGateTimer)
})
	-Add the set mySprite2 block from the sprites section under the pause block. 
	-Change mySprite2 to PurpleGate.
	-Change the kind to PGate. 
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
}
let PurpleGate: Sprite = null
	forever(function () {
    pause(PurpleGateTimer)
    PurpleGate = sprites.create(img``, SpriteKind.PGate)
})

	-Set the asset of the PurpleGate to the Purple Gate Sprite by clicking on the grey box, selecting my assets and choosing the purple gate image. 
	    forever (function (){
	    pause(PurpleGateTimer)
	    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
})

	-Duplicate the set Rocks position block from the Rocks forever loop. 
	-Change Rocks to PurpleGate.
	forever(function () {
    pause(PurpleGateTimer)
       PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
})

	-Duplicate the set Rocks vx 0 and vy SkierSpeed block from the Rocks forever loop and add it to your new forever loop.
	-change Rocks to PurpleGate. 
	forever(function () {
    pause(PurpleGateTimer)
    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    PurpleGate.setVelocity(0, SkierSpeed)
})


	-Lets make our purple gate do something. 
	-Add an on sprite of kind player overlaps otherSprite of kind player container onto the workspace.
	-Change the otherSprite kind from Player to PGate.
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
	
})

	-First we need to remove the gate.
	-Add a destroy mySprite block from the sprite category. 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    mySprite.destroy()
})
	-Next grab the local otherSprite variable from the overlap container and replace the mySprite circle.
	**Grab the Gif**
	-Feel free to add an effect on the destory code.
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
})

	-Now we want to add some additonal effects. 
	-How about making our Skier faster.
	-Add a change SkierSpeed block to the overlap code.
	-Change the value to -5. 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    SkierSpeed += -5
})
	-Next lets give our player additonal points for hitting the gates. 
	-Add a change score by 1 block to the overlap code.
	-Change the value from 1 to 3.
	sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    SkierSpeed += -5
    info.changeScoreBy(3)
})





# Adding Distance values
	### Set your varaible in the on start container
		Create new variable
		Call it distance
		Set it to 0 
	```blocks
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
let distance = 0
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000
```
	
	
	### Adjusting distance
	 Add another forever loop into the workspace
	 ```blocks
	 forever(function () {
	
})
```
	 Grab a pause block from the loop category
	 Leave the pause value as 100ms because we want to update the distance often.
	 ```blocks
	 forever(function () {
    pause(100)
})
```
	 Grab a change variabale block and place it under the pause block.
	 ```blocks
	 forever(function () {
    pause(100)
    distance += 1
})
```
	 Place a multiplication cirlce in the varaiable's value space. 
	 ```blocks
	 forever(function () {
    pause(100)
    distance += 0 * 0
})
```
	Grab the SkierSpeed variable circle and place it in one of the spaces for the multiplication circle.
	```blocks
	forever(function () {
    pause(100)
    distance += SkierSpeed * 0
})
```
	Set the other value to -0.05
	```blocks
	forever(function () {
    pause(100)
    distance += SkierSpeed * -0.05
})
```
## Showing the distance value

	Add a show long text block from the ``||game:game||`` category to your on life zero continer. Be sure to add it above the game over block. 
	Set the text to appear in the center of the screen.
	```blocks
	info.onLifeZero(function () {
    game.showLongText("", DialogLayout.Center)
    game.over(false)
})
```
	Add a join text circle from the ``||text:text||`` catagory under the advanced section. 
	Add a third value space by clicking the plus button on the variable circle. 
	```blocks
	info.onLifeZero(function () {
    game.showLongText("Hello" + "World" + "", DialogLayout.Center)
    game.over(false)
})
```
	Place a round circle from the ``||math:math||`` catagory into the middle value space.
	```blocks
	info.onLifeZero(function () {
    game.showLongText("Hello" + Math.round(0) + "", DialogLayout.Center)
    game.over(false)
})
```
	Add the distance variable cirlce to the value space in the round cirlce. 
	```blocks
	info.onLifeZero(function () {
    game.showLongText("Hello" + Math.round(distance) + "", DialogLayout.Center)
    game.over(false)
})
```
	Replace the text so it reads ``||text:"you went"||`` ``||math:round||`` ``||variables:distance||`` ``||text:"feet"||``.
	```blocks
	info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    game.over(false)
})
```

	Add a change score by block from the ``||info:info||`` catagory. 
	```blocks
	info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(1)
    game.over(false)
})
	```
	Duplicate the round distance circle and add it to the score block.
	```blocks
	info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(false)
})
```
# Creating a Win Condition
	### Add another forever loop to your workspace.
	```blocks
	forever(function () {
	
})
```
	### Add an if then loop to the forever loop you just placed.
	```blocks
	forever(function () {
    if (true) {
    	
    }
})
```
### Add a comparison diamond to the if then loop. Change the symbol from less than < to great than or equal >=.
```blocks
forever(function () {
    if (0 >= 0) {
    	
    }
})
```

	### Add a distance varaiable circle to the first value in the comparison. Set the second value to a high number such as 500. 
	```blocks
	forever(function () {
    if (distance >= 500) {
    	
    }
})
```
## Adding the the checkered gate. 
	### Add a set mySprite2 to sprite [] of kind Player.
	### Rename mySprite2 to CheckGate.
	### Change the kind from Player to a new kind called CGate. 
	```blocks
	namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
	
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(img` `, SpriteKind.CGate)
    }
})

```
	### Click on the grey box and select the checkered gate from the my Assets section.
	
	```blocks
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
    }
})
```
	### Create a new variable called CGateTimer in our on start loop.
	### Set the value to 7000
	```blocks
	let CheckGate: Sprite = null
let PurpleGate: Sprite = null
let Rocks: Sprite = null
let distance = 0
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
distance = 0
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000
let CGateTimer = 7000
```
	###Copy the set position block from the Purple gate forever loop and place it in the if then statement for the CheckGate loop.
	### Change PurpleGate to CheckGate. 
	```blocks
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    }
})
```
	### Copy the set PurpleGate vx and vy block from the Purple Gate forever loop and add it to the ChcekGate Loop.
	### Change PurpleGate to CheckGate. 
	```blocks
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
})
```
	### Add a pause block within the forever loop, but outside the if then statement.
	```blocks
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
    pause(100)
})
	```
	### Add a CheckGateTimer varaiable circle to the value space in the pause block. 
	```blocks
	forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
    pause(CGateTimer)
})
```
	### Add an overlap container and adjust the kinds so it reads when sprite of kind Player overlaps otherSprite kind of CGate. 
	```blocks
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
	
})
```
	### Copy the long text block from the on life zero container and add it to the overlap code we just added.
	```blocks 
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
})
``` 
	### Copy the change score by round distance block from the on life zero container and add it to the overlap container. 
	```blocks
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
})
```
	### Add a game over block from the ``||game:game||`` catagory to the overlap code.
	### Change the value from lose to win. 
	### Feel free to add an effect. 
	```blocks
	sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(true)
})
```

## Final Code

```blocks
namespace SpriteKind {
    export const Rock = SpriteKind.create()
    export const PGate = SpriteKind.create()
    export const CGate = SpriteKind.create()
}
sprites.onOverlap(SpriteKind.Player, SpriteKind.PGate, function (sprite, otherSprite) {
    otherSprite.destroy(effects.coolRadial, 200)
    SkierSpeed += -5
    info.changeScoreBy(3)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Rock, function (sprite, otherSprite) {
    otherSprite.destroy(effects.blizzard, 100)
    info.changeLifeBy(-1)
})
sprites.onDestroyed(SpriteKind.Rock, function (sprite) {
    info.changeScoreBy(1)
})
info.onLifeZero(function () {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(false)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.CGate, function (sprite, otherSprite) {
    game.showLongText("\"you went\"" + Math.round(distance) + "\"feet!\"", DialogLayout.Center)
    info.changeScoreBy(Math.round(distance))
    game.over(true)
})
let CheckGate: Sprite = null
let PurpleGate: Sprite = null
let Rocks: Sprite = null
let distance = 0
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)
distance = 0
let SkierSpeed = -20
let RockSpawnTime = 2000
let PurpleGateTimer = 5000
let CGateTimer = 7000
forever(function () {
    pause(100)
    distance += SkierSpeed * -0.05
})
forever(function () {
    Rocks = sprites.create(assets.image`mediumOceanRock`, SpriteKind.Rock)
    Rocks.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    Rocks.setVelocity(0, SkierSpeed)
    Rocks.setFlag(SpriteFlag.AutoDestroy, true)
    pause(RockSpawnTime)
})
forever(function () {
    PurpleGate = sprites.create(assets.image`Purple Gate`, SpriteKind.PGate)
    PurpleGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
    PurpleGate.setVelocity(0, SkierSpeed)
    pause(PurpleGateTimer)
})
forever(function () {
    if (distance >= 500) {
        CheckGate = sprites.create(assets.image`CheckGate`, SpriteKind.CGate)
        CheckGate.setPosition(randint(0, scene.screenWidth()), scene.screenHeight())
        CheckGate.setVelocity(0, SkierSpeed)
    }
    pause(CGateTimer)
})
game.onUpdateInterval(3000, function () {
    SkierSpeed += -5
    SkierSpeed = Math.max(SkierSpeed, -100)
    RockSpawnTime += -200
    RockSpawnTime = Math.max(RockSpawnTime, 500)
})
