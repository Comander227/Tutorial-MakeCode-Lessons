# Chase The Pizza Enhanced

## {Introduction @unplugged}

In this tutorial you will create a basic chase game with a bit of a twist at the end. 

## Step 1 : Background
### The first part of this project is to create the base game. We will start with our background. 


- :tree: Grab the ``||scene: set background color to ()||`` block and place it in the ``||loops:on start||`` container. 
- :paint brush: **Click** on the **grey circle** and pick a color for your background. 

```blocks
//@highlight
scene.setBackgroundColor(12)
``` 

## Step 2: Characters
### Let's create the player character. 

- :paper plane: Open the ``||sprites: Sprites||`` category and grab a ``||variables: Set mySprite to||`` ``||sprites: sprite [ ] of kind Player||`` and place it in the ``||loops: on start||`` container. 

- :paint brush: **Click** on the **grey** box and open the sprite editor. Open the **Gallery** section and pick a character for your game. 

```blocks
scene.setBackgroundColor(12)
//@highlight
let mySprite = sprites.create(img`
    e e e . . . . e e e . . . . 
    c d d c . . c d d c . . . . 
    c b d d f f d d b c . . . . 
    c 3 b d d b d b 3 c . . . . 
    f b 3 d d d d 3 b f . . . . 
    e d d d d d d d d e . . . . 
    e d f d d d d f d e . b f b 
    f d d f d d f d d f . f d f 
    f b d d b b d d 2 f . f d f 
    . f 2 2 2 2 2 2 b b f f d f 
    . f b d d d d d d b b d b f 
    . f d d d d d b d d f f f . 
    . f d f f f d f f d f . . . 
    . f f . . f f . . f f . . . 
    `, SpriteKind.Player)
```
## Step 3: Controlling the Character
### Now that we have a character, let's setup the controls. 

- :game: Open the ``||controller: Controller||`` category and grab the ``||controller: move mySprite with buttons||`` block and add it under your ``||variables: Set mySprite to||`` ``||sprites: sprite [ ] of kind Player||`` block in the ``||loops: on start||`` container.


```blocks
scene.setBackgroundColor(12)
let mySprite = sprites.create(img`
    e e e . . . . e e e . . . . 
    c d d c . . c d d c . . . . 
    c b d d f f d d b c . . . . 
    c 3 b d d b d b 3 c . . . . 
    f b 3 d d d d 3 b f . . . . 
    e d d d d d d d d e . . . . 
    e d f d d d d f d e . b f b 
    f d d f d d f d d f . f d f 
    f b d d b b d d 2 f . f d f 
    . f 2 2 2 2 2 2 b b f f d f 
    . f b d d d d d d b b d b f 
    . f d d d d d b d d f f f . 
    . f d f f f d f f d f . . . 
    . f f . . f f . . f f . . . 
    `, SpriteKind.Player)
//@highlight
controller.moveSprite(mySprite)
```

## Step 4: Keeping the Character On Screen

### Right now, if we are not careful then our character will run right off the screen. We have to fix that.

- :paper plane: Grab a ``||sprites: set mySprite stay on screen||`` block from the ``||sprites: Sprites||`` category and place it under the ``||controller: move mySprite with buttons||`` block. 
- :mouse pointer: set the value to **On**


```blocks
scene.setBackgroundColor(10)
let mySprite = sprites.create(img`
    e e e . . . . e e e . . . . 
    c d d c . . c d d c . . . . 
    c b d d f f d d b c . . . . 
    c 3 b d d b d b 3 c . . . . 
    f b 3 d d d d 3 b f . . . . 
    e d d d d d d d d e . . . . 
    e d f d d d d f d e . b f b 
    f d d f d d f d d f . f d f 
    f b d d b b d d 2 f . f d f 
    . f 2 2 2 2 2 2 b b f f d f 
    . f b d d d d d d b b d b f 
    . f d d d d d b d d f f f . 
    . f d f f f d f f d f . . . 
    . f f . . f f . . f f . . . 
    `, SpriteKind.Player)
controller.moveSprite(mySprite)
//@highlight
mySprite.setStayInScreen(true)
```

## Step 5: Let's Make Something to Chase
### Now that we are finished with our character let's give them something to chase.

- :paper plane: Grab another ``||variables: Set mySprite2 to||`` ``||sprites: sprite [ ] of kind Player||`` and place it in the ``||loops: on start||`` container.
- :mouse pointer: change the kind of the sprite from ``||sprites: Player||`` to ``||sprites: Food||``
- :paint brush: **Click** on the **grey** block and open the gallery. Pick the object that you want your character to chase. 

```blocks
scene.setBackgroundColor(10)
let mySprite = sprites.create(img`
    e e e . . . . e e e . . . . 
    c d d c . . c d d c . . . . 
    c b d d f f d d b c . . . . 
    c 3 b d d b d b 3 c . . . . 
    f b 3 d d d d 3 b f . . . . 
    e d d d d d d d d e . . . . 
    e d f d d d d f d e . b f b 
    f d d f d d f d d f . f d f 
    f b d d b b d d 2 f . f d f 
    . f 2 2 2 2 2 2 b b f f d f 
    . f b d d d d d d b b d b f 
    . f d d d d d b d d f f f . 
    . f d f f f d f f d f . . . 
    . f f . . f f . . f f . . . 
    `, SpriteKind.Player)
controller.moveSprite(mySprite)
mySprite.setStayInScreen(true)
//@highlight
let mySprite2 = sprites.create(img`
    . . . . . . b b b b . . . . . . 
    . . . . . . b 4 4 4 b . . . . . 
    . . . . . . b b 4 4 4 b . . . . 
    . . . . . b 4 b b b 4 4 b . . . 
    . . . . b d 5 5 5 4 b 4 4 b . . 
    . . . . b 3 2 3 5 5 4 e 4 4 b . 
    . . . b d 2 2 2 5 7 5 4 e 4 4 e 
    . . . b 5 3 2 3 5 5 5 5 e e e e 
    . . b d 7 5 5 5 3 2 3 5 5 e e e 
    . . b 5 5 5 5 5 2 2 2 5 5 d e e 
    . b 3 2 3 5 7 5 3 2 3 5 d d e 4 
    . b 2 2 2 5 5 5 5 5 5 d d e 4 . 
    b d 3 2 d 5 5 5 d d d 4 4 . . . 
    b 5 5 5 5 d d 4 4 4 4 . . . . . 
    4 d d d 4 4 4 . . . . . . . . . 
    4 4 4 4 . . . . . . . . . . . . 
    `, SpriteKind.Food)
```
## Step 6: What a Catch!

### Now that we have an object to catch, we need to setup the collision code for our game to work.

- :paper plane: Grab the  

        