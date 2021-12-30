1. Set up your background to white for your snow
	scene.setBackgroundColor(1)
2. Set your skier sprite
	scene.setBackgroundColor(1)
	let mySprite = sprites.create(assets.image`Skier`,SpriteKind.Player)

3. Make your character move
	scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)

4. Set your skier to stay on screen
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)

5. Set the position of the skier
scene.setBackgroundColor(1)
let mySprite = sprites.create(assets.image`Skier`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
mySprite.setPosition(80, 11)

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
	-Add the 




	Establish obstacles
		Rocks
		Trees
	Establish obstacles overlap
	Game Over on Crash? 
On Zero Life
	
	Adjust Speed Value
	Set scoring system 
	
7. Create Gates 

8.        Create Key Variables
	RockSpeed should be a managable integer.
	RockSpawnTime should be a value in miliseconds. 
