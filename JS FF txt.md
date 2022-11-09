FF 


https://makecode.com/_hfHT2aA700km  //Fully Built Reference
https://makecode.com/_1gY8PWd3F3sH  //Empty With Assets

//Part 1: Swimming with Sharks
/* Setting up the shark in the ocean and establishing movement.*/

//Step #1: Establishing our Sprites
/*Add the following code to the beginning of our project. We will use this section and 
this code to continue establishing our variables as we work through the project.*/

let mySprite: Sprite = null


//Step #2: Background

scene.setBackgroundColor(8)

//Step #3: Adding our Shark

mySprite = sprites.create(assets.inmage`shark`, SpriteKind.Player)

//Step #4: Make it Move
contorller.moveSprite(mySprite)

//Step #5: Where'd it Go?
/*Use the setStayInScreen function to keep our shark on screen.*/
mySprite.setStayInScreen(true)


//Part 1: Final Code
let mySprite: Sprite = null

scene.setBackgroundColor(8)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)


//Part 2: Food, Not Friends
/* Setting up the fish food to appear*/

//Step #6: Establishing our Food Sprite
/*Add the following code to the code block where we established our mySprite image*/
let myFood: Sprites = null

//Step #7: Let's Go Fishing
/*Create an onUpdateInterval function to place the following code into*/
game.onUpdateInterval(2100, function(){
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
})

//Step #6: Never too Far Away
/*Add the following code to your onUpdateInterval function to create a random position 
for the food to spawn*/
myFood.setPosition(scene.screenWidth(), randint(5,115))

//Step #7: Fast Food
/*Add the following code to the function you previously created*/
myFood.vx = -75






//Part 2: Final Code

let myFood: Sprites = null
let mySprite: Sprite = null

scene.setBackgroundColor(8)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)

game.onUpdateInterval(2100, function(){
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5,115))
    myFood.vx = -75
})

//Part 3: Eat Up!
/* Setting up the scoring system, food overlap, and timer. */
//Step #8:Time to Eat!
/*We will use an onOverlap function for the majority of this code*/
sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function(sprite, otherSprite){

})

//Step #9: Down the Hatch
/*Add this code to the function you just created*/
otherSprite.destroy(effects.disintegrate, 100)

//Step #10: Score!
/*Add this code to the function you just used*/
info.changeScoreBy(1)

//Step #11: Setting Up the Timer
/*Add this code to the inital code block we created in Part 1*/
info.startCountdown(15)

//Step #12: Winning
/*Use the onCountdownEnd function to determine a way for the game to end*/
info.onCountdownEnd(function(){
    game.over(true)
})
 
//Part 3: Final Code

let myFood: Sprites = null
let mySprite: Sprite = null

scene.setBackgroundColor(8)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(15)

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function(sprite, otherSprite){
    otherSprite.destroy(effects.disintegrate, 100)
    info.changeScoreBy(1)
})

info.onCountdownEnd(function(){
    game.over(true)
})



//Part 4: Beware the Enemy
/* Setting up the enemy submarine to spawn and interact.*/

//Step #13: Establishing Our Enemy Sprite
/*Add the following code to the sprite establishment code block we have been building*/
let myEnemy: Sprite = null

//Step #14: Timing is Everything
/*We will be creating a new function block using the onUpdateInterval function*/
game.onUpdateInterval(2500, function(){

})

//Step #15: Make some Enemies
/*Add the following code to the function you just created*/
myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)


//Step #16: Location, Location, Location!
/*Add the following code to the function you just used*/
myEnemy.setPosition(scene.screenWidth(), randint(0,120))

//Step #17: Enemeies on the Move
/*Add the following code to the function you just used*/
myEnemy.follow(mySprite, 30)

//Step #18:Enemies Attack
/*Create a new onOverlap function*/
sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function (sprite, otherSprite){

})

//Step #19: Destroy My Enemy
/*Add this code to the function you just created*/
otherSprite.destroy()

//Step #120: Impacting My Player
/*Add the following code to the function you just used*/
info.changeLifeBy(-1)
scene.cameraShake(4,500)


Part 4: Final Code
let myEnemy: Sprite = null
let myFood: Sprites = null
let mySprite: Sprite = null

game.onUpdateInterval(2500,function(){
    myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    myEnemy.setPosition(scene.screenWidth(), randint(0,120))
    myEnemy.follow(mySprite,30)
    
})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function(sprite, otherSprite){
    otherSprite.destroy()
    info.changeLifeBy(-1)
    scene.cameraShake(4,500)
})




//Part 5: Laser Focus
/* Setting up the projectile to fire from the shark and having it interact with 
the enemeies as well as impact the score. */

//Step #21: Establishing our Projectile Sprite
/*Add the following code to the establishing sprite code block*/
let projectile: Sprite = null

//Step #22: Readying the Laser
/* Use the following function to set it so we fire our laz3er when using the A button */
controller.A.onEvent(ControllerButtonEvent.Pressed, function (){

})

//Step #23: Firing the Laser
/*Add the following code to the function you just established*/
projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200,0)

//Step #24: Laser Impact
/*Create a new overlap function for when an enemy overlaps with a laser*/
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function(sprite, otherSprite){

})

//Step #25: Destroying our Sprite on Impact
/*Add the following code to the function you just created*/
sprite.destoy()
otherSprite.destroy(effects.bubbles, 100)

//Step #26: Updating the Score
/*Add the following code to the function you just used*/
info.changeScoreBy(3)


//Part 5: Final Code
let projectile: Sprite = null
let myEnemy: Sprite = null
let myFood: Sprites = null
let mySprite: Sprite = null


controller.A.onEvent(ControllerButtonEvent.Pressed, function (){
    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
    
})

sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function(sprite, otherSprite){
    sprites.destroy()
    otherSprite.destroy(effects.bubbles, 100)
    info.changeScoreBy(3)
})

//Part 6: Extra Life
/* Setting up a powerup to drop to give the shark an extra life and extra time*/ 
//Step #27: Setting up our SpriteKind
/*Add this code to the top of our project*/
namespace SpriteKind{
    export const PowerUp = SpriteKind.create()
}

//Step #28:Establishing our Sprite
/*Add the following code to sprite establishment code block we have been building.*/
let myPowerup: Sprite = null

//Step #29: Creating our function
/*We will create our own function and use that to place a powerup*/
function PowerupDrop (mySprite:Sprite){

}

//Step #30: Destroying the Enemy
/* Add the following code to the function we just created.*/
mySprite.destroy(effects.bubbles, 100)

//Step #31: Dropping the Powerup
/* We will create an if loop to determine if the powerup should drop. 
Add this code under the destroy code you just added to the function.*/
if (Math.percentChance(25)){

}

//Step #32: Setting the Powerup Sprite
/*Add the following code to the inside of the if loop you just created
myPowerup = sprites.create(assets.image`fin`, SpriteKind.PowerUp)


//Step #33: Setting up our Powerup's Parameters
/*Add the following code to the if loop you created.*/
myPowerup.x = mySprite.x
myPowerup.y = mySprite.y
myPowerup.vy = -25


//Step #34: Picking Up the Powerup
/* We will create another onOverlap function to determine what happens when 
we pick up the Powerup.*/
sprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function(sprite, otherSprite){

})
//Step #35: Remove the Powerup
/*Add the following code to the overlap function you just created*/
otherSprite.destroy(effects.bubbles 100)

//Step #36: Additional Variables for the Powerup
/*Add the following code to our establishing variables codeblock*/
let Timer = 15

//Step #37: Modify the Timer
/*Edit the start countdown code in our initial code block to make use of the variable we
just established*/
info.startCountdown(Timer)

//Step #38: Extra Life and Extra Points
/*Add the following code to the overlap function you just used*/
info.changeLifeBy(1)
info.changeScoreBy(5)
Timer += 5

//Step #39: Adjust the Enemy Death
/*We need to modify the overlap code that determines what happens when a 
projectile hits an enemy sub in order for it to drop our newly created powerup.*/
sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function(sprite, otherSprite){
    sprite.destroy()
    PowerupDrop(otherSprite)
    info.changeScoreBy(3)
})

//Part 6: Final Code
namespace SpriteKind{
    export const PowerUp = SpriteKind.create()
    
}


let myPowerup: Sprite = null
let projectile: Sprite = null
let myEnemy: Sprite = null
let myFood: Sprites = null
let mySprite: Sprite = null
let Timer = 15

scene.setBackgroundColor(8)
scene.setBackgroundImage(assests.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(Timer)

function PowerupDrop (mySprite:Sprite){
    mySprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)){
        myPowerup = sprites.create(assets.image`fin`, SpriteKind.PowerUp)
        myPowerup.x =mySprite.x
        myPowerup.y = mySprite.y
        myPowerup.vy = -25
        }
   }

sprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function(sprite, otherSprite){
    otherSprite.destroy(effects.bubbles, 100)
    info.changeLifeBy(1)
    info.changeScoreBy(5)
    Timer +=5
})

sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function(sprite, otherSprite){
    sprite.destroy()
    PowerupDrop(otherSprite)
    info.changeScoreBy(3)
})

//Part 7: Under the Sea
/*Setting up the background and overall enviornment.*/

//Step #40: Setting up a background image
/*Add the following code to our inital code block under the background color code*/
scene.setBackgroundImage(assets.image`ocean1`)

//Step #41: Establishing our Decoration SpriteKind
/*Add the following code to the namespace code block*/
export const Decoration = SpriteKind.create()

//Step #42: Establishing our Decoration Sprite
/*Add the following code to the establishing sprite code block we have been building.*/
let myDecor: Sprite = null


//Step #43: Repeating our Decorations
/* We will create a for loop at the end of our initial background code to 
add some decorations to our game*/
for (let index = 0; index < 10; index++){

}

//Step #44: Asigning our Decorations Sprite
/*Add the following code to the for loop you just created*/
myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)

//Step #45: Placing our Decorations
/*Add the following code to the for loop you created*/
myDecor.setPosition(randint(0,160), 96) 



//Part 7: Final Code
namespace SpriteKind{
    export const PowerUp = SpriteKind.create()
    export const Decoration = SpriteKind.create()
}

let myDecor: Sprite = null 
let myPowerup: Sprite = null
let projectile: Sprite = null
let myEnemy: Sprite = null
let myFood: Sprites = null
let mySprite: Sprite = null
let Timer = 15

scene.setBackgroundColor(8)
scene.setBackgroundImage(assests.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(Timer)
for (let index = 0; index <10; index++){
    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)
    myDecor.setPosition(randint(0,160), 96)
    
}

//Part 8: Let's Get Animated
/*Setting up the animation for the shark's movement, laser firing, food movement,
 and enemy movement. 

In this last section we will be adding the animation code to our sprites as well as 
adding anaimation code to the controls. */

//Step #46
/*Add the following animation code to the end of the inital code block, 
after our for loop*/

animation.runImageAnimation(
mySprite,
assets.animation`swim right`,
200,
true
)

//Step #47: About Face Setup
/*We will use a controller function to make our shark turn around.*/
controller.left.onEvent(ControllerButtonEvent.Pressed, function (){

})

//Step #48: About Face Animation
/*Add the following code to the function you just wrote*/
animation.runImageAnimation(
mySprite,
assets.animation`swim left`,
200,
true
)

//Step #49: To the Right
/*Create another fucntion that will determine what happens when the 
character moves to the right.*/
controller.right.onEvent(ControllerButtonEvent.Pressed, function(){

})

//Step #50: Animating the Right
/* Add the following code to the controller function you just wrote.*/
animation.runImageAnimation(
mySprite,
assets.anmation`swim right`,
200,
true
)

//Step #51: Animating the Laser
/* We are going to add the following code to the controller fuction 
that you already established to fire the laser. */
animation.runImageAnimation(
mySprite,
assets.animation`shooting shark`
50,
true
)
})


//Step #52: Animating the Food
/* Add the following code to the onUpdateInterval function where 
we establish our food sprite. */
animation.runImageAnimation(
myFood,
assets.animation`animated food`,
200,
true
)
})


//Step #53: Animating the Enemy
/* Add the folllowing code to the onUpdateInterval function 
where we establish our enemy sprite.*/
anmiation.runImageAnimation(
myEnemy,
assets.animation`animated enemy`,
50,
true
)
})

//Part 8: Final Code

scene.setBackgroundColor(8)
scene.setBackgroundImage(assests.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(Timer)
for (let index = 0; index <10; index++){
    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)
    myDecor.setPosition(randint(0,160), 96)
    
}
animation.runImageAnimation(
mySprite,
assets.animation`swim right`,
200,
true
)


controller.left.onEvent(ControllerButtonEvent.Pressed, function(){
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim left`,
    200,
    true
    )
})

controller.right.onEvent(ControllerButtonEvent.Pressed, function(){
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim right`,
    200,
    true
    )
})

controller.A.onEvent(ControllerButtonEvent.Pressed, function (){
    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
  animation.runImageAnimation(
  mySprite,
  assets.animation`shooting shark`,
  50,
  true
  )
})

game.onUpdateInterval(2100, function(){
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5,115))
    myFood.vx = -75
    animation.runImageAnimation(
    myFood
    assets.animation`animated food`,
    200,
    true
    )
})

game.onUpdateInterval(2500,function(){
    myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    myEnemy.setPosition(scene.screenWidth(), randint(0,120))
    myEnemy.follow(mySprite,30)
    animation.runImageAnimation(
    myEnemy,
    assets.animation`animated enemy`,
    50,
    true
    )

})



//Final Code:
namespace SpriteKind{
    export const PowerUp = SpriteKind.create()
    export const Decoration = SpriteKind.create()
}

let myDecor: Sprite = null 
let myPowerup: Sprite = null
let projectile: Sprite = null
let myEnemy: Sprite = null
let myFood: Sprite = null
let mySprite: Sprite = null
let Timer = 15

scene.setBackgroundColor(8)
scene.setBackgroundImage(assets.image`ocean1`)
mySprite = sprites.create(assets.image`shark`, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
info.startCountdown(Timer)
for (let index = 0; index <10; index++){
    myDecor = sprites.create(assets.image`decoration`, SpriteKind.Decoration)
    myDecor.setPosition(randint(0,160), 96)
}    
animation.runImageAnimation(
mySprite,
assets.animation`swim right`,
200,
true
)

game.onUpdateInterval(2100, function(){
    myFood = sprites.create(assets.image`food`, SpriteKind.Food)
    myFood.setPosition(scene.screenWidth(), randint(5,115))
    myFood.vx = -75
    animation.runImageAnimation(
    myFood,
    assets.animation`animated food`,
    200,
    true
    )
})

sprites.onOverlap(SpriteKind.Player, SpriteKind.Food, function(sprite, otherSprite){
    otherSprite.destroy(effects.disintegrate, 100)
    info.changeScoreBy(1)
})

info.onCountdownEnd(function(){
    game.over(true)
})

game.onUpdateInterval(2500,function(){
    myEnemy = sprites.create(assets.image`enemy`, SpriteKind.Enemy)
    myEnemy.setPosition(scene.screenWidth(), randint(0,120))
    myEnemy.follow(mySprite,30)
    animation.runImageAnimation(
    myEnemy,
    assets.animation`animated enemy`,
    50,
    true
    )

})


sprites.onOverlap(SpriteKind.Player, SpriteKind.Enemy, function(sprite, otherSprite){
    otherSprite.destroy()
    info.changeLifeBy(-1)
    scene.cameraShake(4,500)
})

controller.A.onEvent(ControllerButtonEvent.Pressed, function (){
    projectile = sprites.createProjectileFromSprite(assets.image`laser`, mySprite, 200, 0)
  animation.runImageAnimation(
  mySprite,
  assets.animation`shooting shark`,
  50,
  true
  )
})

sprites.onOverlap(SpriteKind.Projectile, SpriteKind.Enemy, function(sprite, otherSprite){
    sprite.destroy()
    PowerupDrop(otherSprite)
    info.changeScoreBy(3)
})

function PowerupDrop (mySprite:Sprite){
    mySprite.destroy(effects.bubbles, 100)
    if (Math.percentChance(25)){
        myPowerup = sprites.create(assets.image`fin`, SpriteKind.PowerUp)
        myPowerup.x =mySprite.x
        myPowerup.y = mySprite.y
        myPowerup.vy = -25
        }
   }

sprites.onOverlap(SpriteKind.Player, SpriteKind.PowerUp, function(sprite, otherSprite){
    otherSprite.destroy(effects.bubbles, 100)
    info.changeLifeBy(1)
    info.changeScoreBy(5)
    Timer += 5
})

controller.left.onEvent(ControllerButtonEvent.Pressed, function(){
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim left`,
    200,
    true
    )
})

controller.right.onEvent(ControllerButtonEvent.Pressed, function(){
    animation.runImageAnimation(
    mySprite,
    assets.animation`swim right`,
    200,
    true
    )
})