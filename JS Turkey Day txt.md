JS Turkey Day txt

Turkey Rescue!
https://makecode.com/_6oPJv41hz2s4
https://arcade.makecode.com/--skillmap#turkey
//Part 1

//Step #1 Setting The Scene
scene.setBackgroundColor(9)
tiles.setTilemap(tilemap`level1`)

//Step #2 Establishing Your Player
let mySprite = sprites.create(assets.image`player`, SpriteKind.Player)

//Step #3 Controlling the Player
contorller.moveSprite(mySprite, 100, 0) 
//Step #4 Adding Gravity
mySprite.ay = 500
//Step #5 Follow with Camera
scene.cameraFollow Sprite(mySprite)
//Step #6 Starting at the Bottom
tiles.placeOnRandomTile(mySprite, assets.tile`start`)
//Step #7 Jumping
/*Place this code at the top of your codeblock to properly define the Sprite*/
let mySprite: Sprite = null

controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    mySprite.vy = -300
})

//Part 1 Final Code:
scene.setBackgroundColor(9)
tiles.setTilemap(tilemap`level1`)

let mySprite: Sprite = null
scene.setBackgroundColor(9)
tiles.setTilemap(tilemap`level1`)
mySprite = sprites.create(assets.image`player`, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile`start`)
mySprite.ay = 500
controller.moveSprite(mySprite, 100, 0)
scene.cameraFollowSprite(mySprite)

controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    mySprite.vy = -300
})
//Part 2
//Step #8 Rescuing the Others
scene.onOverlapTile(SpriteKind.Player, assets.tile`cage`, function(sprite, location){
    info.changeScoreBy(1)
    })    
//Step #9 Too Many Points
/*Add the following code to your onOverlapTile function*/
tiles.setTileAt(location, assets.tile`transparency16`)
//Step #10 Rescuing the Turkeys
namespace SpriteKind {
    export const Rescued = SpriteKind.create()
}
let turkey: Sprite = null

/*Add the following to the onOverlapTile function*/
turkey = sprites.create(assets.image`turkey`, SpriteKind.Rescued)

//Step #11 Appear Turkey! Appear!
/*Add the following code to your onOverlapTile function*/
tiles.placeOnTile(turkey, location)
//Step #12 Lead Them to Freedom
/*Add the following code to your onOverlapTile function*/
turkey.follow(mySprite)
//Part 2 Final Code
namespace SpriteKind {
    export const Rescued = SpriteKind.create()
}
let turkey: Sprite = null


scene.onOverlapTile(SpriteKind.Player, assets.tile`cage`, function (sprite, location) {
    info.changeScoreBy(1)
    tiles.setTileAt(location, assets.tile`transparency16`)
    let turkey = sprites.create(assets.image`turkey`, SpriteKind.Rescued)
    tiles.placeOnTile(turkey, location)
    turkey.follow(mySprite)
})
//Part 3
//Step #13: Setting Up a Win Condition
scene.onOverlapTile(SpriteKind.Player, sprite.swamp.swampTile16, function(sprite, location) {
game.over(true)
})

//Step #14: It's Time
/*Add the following code to your initial codeblock from Part 1*/
info.startCountdown(120)


//Step #15: Time's Up
info.onCountdownEnd(function() {
game.over(false)
})
//Part 3 Final Code
let turkey: Sprite = null
let mySprite: Sprite = null
scene.setBackgroundColor(9)
tiles.setTilemap(tilemap`level1`)
mySprite = sprites.create(assets.image`player`, SpriteKind.Player)
tiles.placeOnRandomTile(mySprite, assets.tile`start`)
mySprite.ay = 500
controller.moveSprite(mySprite, 100, 0)
scene.cameraFollowSprite(mySprite)
info.startCountdown(120)

controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
    mySprite.vy = -300
})

namespace SpriteKind {
    export const Rescued = SpriteKind.create()
}

scene.onOverlapTile(SpriteKind.Player, assets.tile`cage`, function (sprite, location) {
    tiles.setTileAt(location, assets.tile`transparency16`)
    turkey = sprites.create(assets.image`turkey`, SpriteKind.Rescued)
    tiles.placeOnTile(turkey, location)
    turkey.follow(mySprite)
    info.changeScoreBy(1)
})

scene.onOverlapTile(SpriteKind.Player, sprites.swamp.swampTile16, function (sprite, location) {
    game.over(true)
})

info.onCountdownEnd(function () {
    game.over(false)
})

