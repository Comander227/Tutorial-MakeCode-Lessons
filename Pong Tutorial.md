https://arcade.makecode.com/#tutorial:42774-97417-65865-25080 
 
 
# Pong
## Part 1: Setting Up Key Variables
### We will use the ``||Variables:Variable||`` category to create our players and our background image.
## Setting Up the Players Variables
- :bars: Create a ``||variables: players||`` variable from the variables section by clicking on the ``||Variables: Make a Variable ||`` button.
- :bars: Name the variable ``||variables: players||``.
- :bars: Drag a ``||variables:set players to 0||`` block from the ``||variables:Variables||`` category to the ``||loops:on start||`` container.
- :mouse pointer: Set the value of ``||variables: players||`` to **1**.

```blocks
//@highlight
let players = 1
```

## Setting Up the Background Variable
### We need to create an image to use as our background.
- :bars: Use the ``||Variables: Make a Variable ||`` button to create a variable.
- :bars: name the variable **Background** for our background image. 
- :bars: Add a ``||variables:set Background||`` block from the ``||variables:Variables||`` category to the ``||loops:on start||`` loop

```blocks
let players = 1
//@highlight
let Background = (0)
```

## Setting Up the Background Image
- :chevron down: Open the **Advanced** section of the toolbox.
- :image: Click on the ``||images:Images||`` category.
- :image: Grab a ``||images: create image width () height()||`` circle from the ``||images: Images||`` category and place it in the value space for the ``||variables: set Background||`` block.

```blocks
let players = 1
//@highlight
let Background =image.create(0, 0)
```

## Set the Size of the Image
- :tree: Open the ``||scene:Scene||`` category.
- :tree: Add a ``||scene:screenWidth||`` circle to the image's width and a ``||scene:screenHeight||`` circle to the image height.

```blocks
let players = 1
//@highlight
let Background = image.create(scene.screenWidth(), scene.screenHeight(),)
```
 
## Part 2: Setting Up the Net
### Here is where we will edit our background picture to include a net.
### We will use a ``||loops:for loop||`` to create a uniform net.

## Using a For Loop
- :redo: Add a ``||loops:for loop||`` from the ``||loops:Loops||`` category to the ``||loops: on start||`` container.
- :tree: Add the ``||scene: screenHeight||`` circle from the ``||scene:Scene||`` category to the max index value.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(),)
//@highlight
for (let index = 0; index <= scene.screenHeight(); index++) {
}
```

## Using an If Statement to Set Up the Net
- :random: Grab an ``||logic:if then loop||`` from the ``||logic:Logic||`` category and add it to the ``||loops:for||`` loop.
- :random: Add a ``||logic: 0 < 0 ||`` diamond (also known as a ``||logic:comparison diamond||``) from the ``||logic:Logic||`` category to the ``||logic:if then loop||``.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(),)
for (let index = 0; index <= scene.screenHeight(); index++) {
//@highlight
if (0 < 0) {
}}
```

## Adding the Math
- :calculator: Add a ``||math: remainder of 0 ÷ 1||`` to the first value space in the ``||logic: comparison||`` diamond.  
- :mouse pointer: Then the drag the local ``||variables:index||`` to the ``||math: ÷||`` circle.
Set the values so it reads ``||logic:if||`` the ``||math:remainder of the||`` ``||variables:index||`` ``||math:÷ by 6||`` ``||logic:<||`` 4.
![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")


```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(),)
for (let index = 0; index <= scene.screenHeight(); index++) {
//@highlight
if (index % 6 < 4) {
 }}
```

## Creating Our Net
- :image: Add a ``||images:set picture at x () y () color||`` block from the ``||image:Image||`` category to the ``||logic:if then loop||``.
- :bars: Add a ``||variables: Background||`` circle from the ``||variables:Variable||`` category to the ``||images:set picture at x () y () color||`` block.
- :calculator: Add a ``||math: division||`` circle (``||math: 0 ÷ 0||``) from the ``||math:Math||`` category to the **x** coordinate space.
- :tree: Add the ``||scene: screenHeight||`` circle from the ``||scene:Scene||`` category to the first value in the ``||math: division||`` circle. 
- :mouse pointer: Set the divisor to **2**.
- :paint brush: **Remember to select a color for your net by clicking on the circle at the end of the block.**

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(),)
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     //@highlight
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
```

## Setting the Background
- :tree: Add a ``||scene: set background image||`` block from the ``||scene:Scene||`` category to the ``||loops: on start||`` container.
- :bars: Grab the ``||variables: Background||`` circle from the ``||variables:Variables||`` category and place that in the image value space.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(), )
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
//@highlight
scene.setBackgroundImage(Background)
```

## Part 3: Setting Up Our Player Paddles
### In this section we will set up our player paddles.

## Creating our Player Sprite
- :paper plane: Add a ``||sprites:set mySprite to sprite [] of kind Player ||`` from the ``||sprites:Sprites||`` category under the ``||scene: set background image||`` block in the ``||loops: on start||`` container.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight(), )
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
//@highlight
let mySprite = sprites.create(img``,SpriteKind.Player)
```

## Setting the Player1 Paddle
- :mouse pointer: Click on the triangle next to ``||variables:mySprite||``. 
- :bars: Choose the ``||variables:Rename Variable...||`` option.
- :mouse pointer: Rename ``||variables:mySprite||`` to ``||variables:Player1||``.
- :paint brush: Click the **grey box** to open the sprite editor.
- :paint brush: Click the **My Assets** tab.
- :paint brush: Select the Player 1 asset. It looks like a white Paddle. 
- :paint brush: Feel free to change the color using the sprite editor. 

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
//@highlight
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
```

## Moving Player1
- :gamepad: Add a ``||controller:move||`` ``||variables:mySprite||`` ``||controller:with buttons||`` block from the ``||controller:Controller||`` category.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||``.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
//@highlight
controller.moveSprite(Player1)
```

## Moving in One Direction
- :mouse pointer: Click on the (**+**) button on the ``||controller:move Player1 with buttons||`` block.
- :mouse pointer: Change the **vx** value from **100** to **0**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
//@highlight
controller.moveSprite(Player1, 0, 100)
```

## Setting the Player1 Paddle's Position
- :paper plane: Add a ``||sprites: Set mySprite x() y()||`` block from the ``||sprites:Sprites||`` category.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||``.
- :mouse pointer: Set the **x** value to **8** and the **y** value to **60**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
//@highlight
Player1.setPosition(8,60)
```

## Setting Up the Player1 Paddle to Stay on Screen
- :paper plane: Add a ``||sprites: set mySprite stay on screen||`` block from the ``||sprites:Sprites||`` category.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||``.
- :mouse pointer: Set the value to **on**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
//@highlight
Player1.setStayInScreen(true)
```

## Setting Up the Player2 Paddle
### We will use the same blocks that we used for Player1's Paddle but changing the sprite to Player2.
- :paper plane: Start with adding the ``||sprites: set mySprite [] of kind Player||`` from the ``||sprites:Sprites||`` category to the ``||loops:on start||`` container.
- :mouse pointer: Rename ``||variables:mySprite||`` to ``||variables:Player2||``.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
//@highlight
let Player2 = sprites.create(img``,SpriteKind.Player)
```

## Setting the Player2 Paddle Image.
- :mouse pointer: Click the grey box in the ``||sprites:set Player2 [] of kind Player||`` to open the sprite editor. 
- :mouse pointer: Click on the **My Assets** tab. 
- :mouse pointer: Click on the paddle image labeled **Player 2**
- :paint brush: Feel free to change the color if you want to. 

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
//@highlight
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
```

## Setting Up Player2's Position
- :paper plane: Add the ``||sprites:set mySprite x() y()||`` block from the ``||sprites:Sprites||`` category under the ``||sprites:set Player2 [] of kind Player||`` block.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player2||``.
- :mouse pointer: Set the **x** value to **152** and the **y** value to **60**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
//@highlight
Player2.setPosition(152,60)
```

## Setting the Player2 Paddle to Stay on Screen.
- :paper plane: Add a ``||sprites:set mySprite Stay on Screen||`` block from the ``||sprites:Sprites||`` category to the ``||loops:on start||`` container.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player2||``.
- :mouse pointer: Set the value to **on**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
//@highlight
Player2.setStayInScreen(true)
```

## Part 4: Setting Up the Ball
### Now we are going to set up our game ball.

## Setting up a Projectile
- :paper plane: Add a ``||sprites: set Projectile [] From mySprite with vx 50 vy 50 ||`` block from the ``||sprites:Sprites||`` category to the ``||loops:on start||``.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||`` as we want the ball to spawn from Player1.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
//@highlight
let projectile = sprites.createProjectileFromSprite(img``,Player1,0,0)
```

## Assign the Projectile to the Ball Asset.
- :mouse pointer: Click on the ``||variables:projectile||``'s **gray box** to open the sprite editor.
- :mouse pointer : Open the **My Asset** tab.
- :mouse pointer: Choose the asset labeled **Ball**.
- :paint brush: Feel free to change the Ball's color. 

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
//@highlight
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,0,0)
```

## Step 3: Assigning Random vx and vy Values.
- :calculator: Add a ``||math:pick random (min) to (max)||`` circle from the ``||math:Math||`` category to the **vx** and **vy** value of the ``||sprites:set Projectile from mySprite with vx 50 vy 50||`` block.
- :mouse pointer: Set the vx values to a minimum of **50** and maximum of **75**.
- :mouse pointer: Set the vy values to a minimum of **25** and maximum of **50**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
//@highlight
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,randint(50,75),randint(25,50))
```

## Moving the Ball
- :paper plane: Add a ``||sprites:change mySprite x by ()||`` block from the ``||sprites:Sprites||`` category to the ``||loops:on start||`` container.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.
- :mouse pointer: Change the value from **0** to **3**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,randint(50,75),randint(25,50))
//@highlight
projectile.x +=3
```

## Setting the Ball to Bounce
- :paper plane: Add a ``||sprites:set mySprite Bounce on Walls||`` block from the ``||sprites:Sprites||`` category.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.
- :mouse pointer: Set the value to **on**.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,randint(50,75),randint(25,50))
projectile.x +=3
//@highlight
projectile.setBounceOnWall(true)
```

## Part 5: Setting up the Scoring System
### Now that we have set up our paddles and ball we can move on to set up our scoring system.

## Adding an On Game Update Container
- :circle: Add a ``||game:on game update||`` container from the ``||game:Game||`` category.

```blocks
//@highlight
game.onUpdate(function(){})
```

## Setting Up our If Then Containers
- :random: Add an ``||logic:if then loop||`` from the ``||logic:Logic||`` category.
- :random: Add a ``||logic: comparison||`` diamond <``||logic: 0 < 0||``> from the ``||logic:Logic||`` category to the **true** value of your ``||logic:if then loop||``.

```blocks
game.onUpdate(function(){
//@highlight
if (0 < 0) {
}})
```

## Add the Needed Sprite Values
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to each comparison value.

```blocks
game.onUpdate(function(){
let mySprite: Sprite = null
  //@highlight
  if (mySprite.x > mySprite.x) {
  
  }
})
```

## Adjusting Our Sprites and Values
- :mouse pointer: Change the comparison diamond so it reads ``||variables:projectile||`` ``||sprites:x||`` is greater than ``||logic:(>)||`` ``||variables:Player2||`` ``||sprites:right||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
game.onUpdate(function(){
  //@highlight
  if (projectile.x > Player2.right) {
  
  }
})
```

## Scoring Points
- :id card: Add the ``||info: Change Player 2 Score By 1||`` block from the ``||info:Info||`` category to your ``||logic: if then||`` container.
- :mouse pointer: Change ``||info:Player 2||`` to ``||info:Player 1||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  //@highlight
  info.player1.changeScoreBy(1) 
  }
})
```

## Adding Sound Effects
- :headphones: Add a  ``||music:play sound||`` block from the ``||music:Music||`` category under your ``||info: Change Player 1 Score By 1||`` block.
- :mouse pointer: Change ``||music:ba ding||`` to ``||music:jumpUp||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  //@highlight
  music.jumpUp.play()
  }
})
```

## Resetting the Ball's Position
- :paper plane: Add a ``||sprites: set mySprite position to x() y()||`` block from the ``||sprites:Sprites||`` category under the ``||music:play sound jump up||`` block.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(0,0)
  }
})
```

## Resetting the Ball's Horizontal Position to Player1
- :calculator: Add a ``||math:addition||`` circle (``||math: 0 + 0||``) from the ``||math:Math||`` to the **x** value for your ``||sprites: set||`` ``||variables:projectile||`` ``||sprites:position||``.
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to your ``||math:addition circle||``.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||``.
- :mouse pointer: Use the ``||math:addition||``to add ``||math: 3||`` to the ``||variables:projectile||`` ``||sprites:x value||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(Player1.x +3, 0)
  }
})
```

## Resetting the Ball's Vertical Position to Player1
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to the ``||sprites: set||`` ``||variables:projectile||`` ``||sprites:position||`` **y** value. 
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player1||``.
- :mouse pointer: Change ``||sprites:x||`` to ``||sprites:y||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(Player1.x +3, Player1.y)
  }
})
```


## Resetting the Ball's Velocity
- :paper plane: Add a ``||sprites:set mySprite velocity to vx() vy()||`` block from the ``||sprites:Sprites||`` category under your ``||sprites:set projectile position||`` block.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  //@highlight
  projectile.setVelocity(0,0)
  }
})
```
 
## Setting the Ball's Velocity Values
- :calculator: Add a ``||math:pick random 0 to 10||`` circle from the ``||math:Math||`` category to the ``||sprites:vx||`` and the``||sprites:vy||`` values.
- :mouse pointer: Set the ``||sprites:vx value||`` to ``||math: 50 min and 75 max||``.
- :mouse pointer: Set the ``||sprites:vy value||`` to ``||math: 25 min and 50 max||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  //@highlight
  projectile.setVelocity(randint(50,75),randint(25,50))
  }
})
```

## Setting up Player2's Scoring System
- :random: Click the (**+**) button on the ``||logic:if then||`` container twice. This will create an ``||logic:else if||`` loop and an ``||logic:else||`` loop.
- :random: Click the (**-**) button to remove the ``||logic:else||`` loop.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } 
  //@highlight
  else if (false){
  }
})
```

## Setting up the Scoring Condition
- :mouse pointer: Duplicate the ``||logic:comparison||`` diamond from the top of the ``||logic:if then loop||`` by **right clicking** on the diamond and then selecting **Duplicate**.
- :random: Drag it to the new ``||logic:else if loop||``.
- :mouse pointer: Change the values so it reads ``||variables:projectile||`` ``||sprites:x||`` ``||logic:<||`` ``||variables:Player1||`` ``||sprites:left||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } 
  //@highlight
  else if (projectile.x < Player1.left){
  }
})
```
 
## Updating Player2's Score
- :id card: Add a ``||info:change player 2 score by 1||`` block from the ``||info:Info||`` category to your ``||logic:else if loop||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  //@highlight
  info.player2.changeScoreBy(1)
 
  }
})
```

## Adding a Sound Effect
- :headphones: Add a ``||music:play sound||`` block from the ``||music:Music||`` category under the ``||info:change player 2 score by 1||`` block.
- :mouse pointer: Change ``||music:ba ding||`` to ``||music:jump up||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  //@highlight
  music.jumpUp.play()
  }
})
```
 
## Resetting the Ball's Position
- :paper plane: Add a ``||sprites: set mySprite position to x() y()||`` block from the ``||sprites:Sprites||`` category under the ``||music:play sound jump up||`` block.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(0,0)
  }
})
```

## Resetting the Ball's Horizontal Position to Player2
- :calculator: Add a ``||math:subtraction||`` circle (``||math: 0 - 0||``) from the ``||math:Math||`` category to the x value ``||sprites: set||`` ``||variables:projectile||`` ``||sprites:position||``.
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to the first value of your ``||math:subtraction circle||``.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player2||``.
- :mouse pointer: Use the ``||math:subtraction||``to subtract ``||math: 3||`` to the ``||variables:projectile||`` ``||sprites:x value||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(Player2.x -3,0)
  }
})
```

## Resetting the Ball's Vertical Position to Player2
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to the ``||sprites: set||`` ``||variables:projectile||`` ``||sprites:position||`` y value. 
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:Player2||``.
- :mouse pointer: Change ``||sprites:x||`` to ``||sprites:y||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  music.jumpUp.play()
  //@highlight
  projectile.setPosition(Player2.x -3,Player2.y)
  }
})
```

## Resetting the Ball's Velocity.
- :paper plane: Add a ``||sprites:set mySprite velocity to vx() vy()||`` block from the ``||sprites:Sprites||`` category under your ``||sprites:set projectile position||`` block.
- :mouse pointer: Change ``||variables:mySprite||`` to ``||variables:projectile||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  music.jumpUp.play()
  projectile.setPosition(Player2.x -3,Player2.y)
  //@highlight
  projectile.setVelocity(0,0)
  }
})
```

## Setting the Ball's Velocity Values.
- :calculator: Add a ``||math:pick random||`` circle from ``||math:Math||`` category to the ``||sprites:vx||`` and the``||sprites:vy||`` values.
- :mouse pointer: Set the ``||sprites:vx value||`` to ``||math: -75 min and -50 max||``.
- :mouse pointer: Set the ``||sprites:vy value||`` to ``||math: -50 min and -25 max||``.

```blocks
let projectile: Sprite = null
let Player2: Sprite = null
let Player1: Sprite = null
game.onUpdate(function(){
  if (projectile.x > Player2.right) {
  info.player1.changeScoreBy(1) 
  music.jumpUp.play()
  projectile.setPosition(Player1.x +3,Player1.y)
  projectile.setVelocity(randint(50,75),randint(25,50))
  } else if (projectile.x < Player1.left){
  info.player2.changeScoreBy(1)
  music.jumpUp.play()
  projectile.setPosition(Player2.x -3,Player2.y)
  //@highlight
  projectile.setVelocity(randint(-75,-50),randint(-50,-25))
  }
})
```
 
## Setting up Player1's Starting Score.
- :id card: Add one ``||info:set player 2 score to 0||`` from the ``||info:Info||`` category to your ``||loops: on start||`` container.
- :mouse pointer: Change ``||info:set player 2 score to 0||`` to ``||info:set player 1 score to 0||``.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,randint(50,75),randint(25,50))
projectile.x +=3
projectile.setBounceOnWall(true)
//@highlight
info.player1.setScore(0)
```

## Setting up Player2's Starting Score.
- :id card: Add another ``||info:set player 2 score to 0||`` to your ``||loops: on start||`` container.

```blocks
let players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
if (index % 6 < 4) {
     Background.setPixel(scene.screenWidth() / 2, index, 1)
 }}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`,SpriteKind.Player)
controller.moveSprite(Player1, 0, 100)
Player1.setPosition(8,60)
Player1.setStayInScreen(true)
let Player2 = sprites.create(assets.image`Player 2`,SpriteKind.Player)
Player2.setPosition(152,60)
Player2.setStayInScreen(true)
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`,Player1,randint(50,75),randint(25,50))
projectile.x +=3
projectile.setBounceOnWall(true)
info.player1.setScore(0)
//@highlight
info.player2.setScore(0)
```
 
## Part 6: Making an Impact.
### Now we will use an ``||sprites:On Overlap||`` container to make our ball bounce off the paddles.
 
## Adding the New Container.
- :paper plane: Add a new ``||sprites: on sprite of kind Player overlaps otherSprite of kind Player||`` container from the ``||sprites:Sprites||`` category to the workspace.
- :mouse pointer: Change the ``||variables:otherSprite||`` ``||sprites:kind||`` from ``||sprites:Player||`` to ``||sprites:Projectile||``.

```blocks
//@highlight
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
 
})
```

## Updating the Ball's Velocity
- :paper plane: Add a ``||sprites:set mySprite x to ()||`` from the ``||sprites:Sprites||`` category to the ``||sprites:on Overlap||`` container.
- :calculator: Add ``||math:multiplication||`` circle (``||math: 0 * 0||``) from the ``||math:Math||`` category to the value. 

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
 let mySprite: Sprite = null
   //@highlight
   mySprite.x = 0 * 0

})
```


## Altering the Value
- :paper plane: Add a``||sprites: mySprite x||`` circle from the ``||sprites:Sprites||`` category to your second ``||math:multiplication||`` value.
- :mouse pointer: Drag the local ``||variables:otherSprite||`` over the all of the ``||variables:mySprite||`` variables.

![Grabbing variable from block](/static/skillmap/space/give-var.gif "So that's how you do that!")

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
   //@highlight
   otherSprite.x = 0 * otherSprite.x

})
```
## Duplicating the Block.
- :mouse pointer: Duplicate the ``||sprites:set otherSprite x to||`` ``||math:(0 * otherSprite.x)||`` by **right clicking** on the whole block and selecting duplicate. 
- :mouse pointer: Set the new block below the previous one.

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
   otherSprite.x = 0 * otherSprite.x
   //@highlight
   otherSprite.x = 0 * otherSprite.x
})
``` 
 
 
## Setting the vx Values
- :mouse pointer: Change the first ``||sprites:set otherSprite x||`` to ``||sprites:set otherSprite vx||``.
- :mouse pointer: Set the ``||math:multiplication||`` circle to read ``||math: -1.1 *||`` ``||variables:otherSprite||`` ``||sprites:vx||``.

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
   //@highlight
   otherSprite.vx = -1.1 * otherSprite.vx
   otherSprite.x = 0 * otherSprite.x
})
```
 
## Setting the vy Values
- :mouse pointer: Change the second ``||sprites:set otherSprite x||`` to ``||sprites:set otherSprite vy||``.
- :mouse pointer: Set the ``||math:multiplication||`` circle to read ``||math: 1.1 *||`` ``||variables:otherSprite||`` ``||sprites:vy||``.

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
 
   otherSprite.vx = -1.1 * otherSprite.vx
   //@highlight
   otherSprite.vy = 1.1 * otherSprite.vy
})
```
 
## Adding A Sound Effect.
- :headphones: Add ``||music:play tone at Middle C for 1/2 beat||`` from the ``||music:Music||`` category to the ``||sprites:on overlap||`` container.
- :mouse pointer: Change ``||music: Middle C||`` to ``||music:Middle B||``. If you can't find Middle B, enter the value **494**.

```blocks
sprites.onOverlap(SpriteKind.Player,SpriteKind.Projectile, function(sprite,otherSprite){
 
   otherSprite.vx = -1.1 * otherSprite.vx
   otherSprite.vy = 1.1 * otherSprite.vy
   //@highlight
   music.playTone(494,music.beat(BeatFraction.Half))
})
```

## Part 7 Setting Up Solo Mode
### Now we are going to set up our Player2 paddle to function as a computer so we can play on our own. 

## Adding a New Container
 - :circle: Grab a new ``||game:on game update||`` container from the ``||game:Game||`` category.

```blocks
//@highlight
game.onUpdate(function(){
 
})
```

## Adding Logic
- :random: Add an ``||logic:if then loop||`` from the ``||logic:Logic||`` category to your ``||game: on game update||`` container.
- :random: Add an ``||logic: and||`` diamond from the ``||logic:Logic||`` category to the ``||logic:if then loop||``.

```blocks
game.onUpdate(function(){
 //@highlight
 if (true && true){
 }
})
```

## Setting Up the Core If Then Loop.
- :random: Add a ``||logic:0 > 0||`` comparison diamond from the ``||logic:Logic||`` category to the ``||logic: and||`` diamond.
- :calculator: Add a ``||math:division||`` circle (``||math: 0 ÷ 0||``) from the ``||math:Math||`` category to the``||logic:comparison||`` diamond.
- :paper plane: Add a ``||sprites:mySprite x||`` circle from the ``||sprites:Sprites||`` category to the ``||logic: 0 > 0||`` comparison diamond.
- :tree: Add a ``||scene:screenWidth||`` circle from the ``||scene:Scene||`` category to the other side of the ``||logic: 0 > 0||`` comparison diamond.
- :mouse pointer: Set the diamond so it reads ``||variables:projectile||`` ``||sprites:y||`` ``||logic:>||`` ``||scene:screenWidth||`` ``||math: ÷ 2||``

```blocks
let projectile: Sprite = null
game.onUpdate(function(){
 //@highlight
 if (projectile.y > scene.screenWidth() /2 && true){
 }
})
```
 
## How Many Players Do We Have?
### We need to check how many players we have. 
- :random: Add an ``||logic: 0 = 0||`` comparison diamond from the ``||logic:Logic||`` category to the second half of the ``||logic:and||`` diamond.
- :bars: Add the ``||variables:players||`` from the ``||variables:Variables||`` category to the ``|||logic: 0 = 0||``comparison diamond.
- :mouse pointer: Set the second value to **1**.
- :check: It should read ``||variables:players||`` ``||logic:=||`` **1**.

```blocks
let projectile: Sprite = null
game.onUpdate(function(){
 //@highlight
 if (projectile.y > scene.screenWidth() /2 && players == 1){
 }
})
```
 
## Adding More Logic to Our Computer Opponent.
- :random: Add an ``||logic: if then else loop||`` from the ``||logic:Logic||`` category to the ``||logic: if then loop||`` you already have.

```blocks
let projectile: Sprite = null
game.onUpdate(function(){
 if (projectile.y > scene.screenWidth() /2 && players == 1){
   //@highlight
   if (true){
   }else {
   }
 }
})
```

## Comparing the Computer's Position to the Ball's Position.
- :random: Add a ``||logic:comparison||`` diamond <``||logic: 0 > 0||``> from the ``||logic:Logic||`` category to the ``||logic:if then loop||`` you just added.
- :paper plane: Add a ``||sprites:mySprite x||`` circle to both parts of the ``||logic: 0 > 0||`` comparison diamond.
- :mouse pointer: Set the ``||variables:variables||`` so the ``||logic:comparison||`` diamond reads ``||variables:projectile||`` ``||sprites:y||`` ``||logic: >||`` ``||variables:Player2||`` ``||sprites:y||``.

```blocks
let Player2: Sprite = null
let projectile: Sprite = null
game.onUpdate(function(){
 if (projectile.y > scene.screenWidth() /2 && players == 1){
   //@highlight
   if (projectile.y > Player2.y){
   }else {
   }
 }
})
```

## Moving the Computer's Paddle.
- :paper plane: Add a ``||sprites:change mySprite x by ()||`` block from the ``||sprites:Sprites||`` category to the ``||logic:if the loop||``.
- :mouse pointer: Set the block to read ``||sprites: change||`` ``||variables:Player2||`` ``||sprites:y by 2||``.

```blocks
let Player2: Sprite = null
let projectile: Sprite = null
game.onUpdate(function(){
 if (projectile.y > scene.screenWidth() /2 && players == 1){
   if (projectile.y > Player2.y){
   //@highlight
   Player2.y += 2
   }else {
   }
 }
})
```

## Moving the Computer's Paddle.
- :mouse pointer: Duplicate the ``||sprites:change mySprite x by ()||`` block in the ``||logic:if the loop||`` by **right clicking** the block and selecting **Duplicate** and add it to the ``||logic:else loop||``.
- :mouse pointer: Set the block to read  ``||sprites: change||`` ``||variables:Player2||`` ``||sprites:y by -2||``.


```blocks
let Player2: Sprite = null
let projectile: Sprite = null
game.onUpdate(function(){
 if (projectile.y > scene.screenWidth() /2 && players == 1){
   //@highlight
   if (projectile.y > Player2.y){
   Player2.y += 2
   }else {
   //@highlight
   Player2.y += -2
   }
 }
})
```
 
## Part 8: Controlling Player 2
### Now we are going to establish the controls for Player 2.
 
## Adding a New Controller Container
- :gamepad: Drag a ``||controller: on player 2 A button pressed||`` from the ``||controller:Controller||`` category to the workspace.
- :mouse pointer: Change ``||controller: A||`` to ``||controller: up||``.

```blocks
//@highlight
controller.player2.onButtonEvent(ControllerButton.Up,ControllerButtonEvent.Pressed, function(){
})
```
 
## Altering the Number of Players
- :bars: Add a ``||variables:set players to 0||`` block from the ``||variables:Variables||`` category to the ``||controller: on player 2 up button pressed||`` container.
- :mouse pointer: Change the value from ``||variables:0||`` to ``||variables:2||``.

```blocks
controller.player2.onButtonEvent(ControllerButton.Up,ControllerButtonEvent.Pressed, function(){
//@highlight
let players = 2
})
```
 
 
## Adding Controller Blocks
- :gamepad: Add a ``||controller: player 2 move mySprite with buttons||`` from the ``||controller: Controller||`` category to the ``||controller: on player 2 up button pressed||`` container.
- :bars: Change ``||variables:mySprite||`` to ``||variables:Player2||``.
- :mouse pointer: Click on the ``||controller: +||`` button.
- :mouse pointer: Change the ``||controller: vx||`` value to **0**.

```blocks
controller.player2.onButtonEvent(ControllerButton.Up,ControllerButtonEvent.Pressed, function(){
let players = 2
//@highlight
controller.player2.moveSprite(Player2,0,100)
})
```
 
## Duplicating the Controller Container
- :mouse pointer: **Right click** on the ``||controller: on player 2 up button pressed||`` container.
- :mouse pointer: Click on **Duplicate**.
- :mouse pointer: Change ``||controller: up||`` to ``||controller:down||``.

```blocks
controller.player2.onButtonEvent(ControllerButton.Up,ControllerButtonEvent.Pressed, function(){
let players = 2
controller.player2.moveSprite(Player2,0,100)
})
 
//@highlight
controller.player2.onButtonEvent(ControllerButton.Down,ControllerButtonEvent.Pressed, function(){
let players = 2
controller.player2.moveSprite(Player2,0,100)
})
```
 
 
 
## Finish
### Congrats on completing your own version of Pong. Feel free to play a few rounds and challenge your friends.

```blocks
controller.player2.onButtonEvent(ControllerButton.Down, ControllerButtonEvent.Pressed, function () {
  players = 2
  controller.player2.moveSprite(Player2, 0, 100)
})
controller.player2.onButtonEvent(ControllerButton.Up, ControllerButtonEvent.Pressed, function () {
  players = 2
  controller.player2.moveSprite(Player2, 0, 100)
})
sprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {
  otherSprite.vx = -1.1 * otherSprite.vx
  otherSprite.vy = 1.1 * otherSprite.vy
  music.playTone(494, music.beat(BeatFraction.Half))
})
let Player2: Sprite = null
let players = 0
players = 1
let Background = image.create(scene.screenWidth(), scene.screenHeight())
for (let index = 0; index <= scene.screenHeight(); index++) {
  if (index % 6 < 4) {
      Background.setPixel(scene.screenWidth() / 2, index, 1)
  }
}
scene.setBackgroundImage(Background)
let Player1 = sprites.create(assets.image`Player 1`, SpriteKind.Player)
Player1.setPosition(8, 60)
controller.moveSprite(Player1, 0, 100)
Player1.setStayInScreen(true)
Player2 = sprites.create(assets.image`Player 2`, SpriteKind.Player)
Player2.setPosition(152, 60)
Player2.setStayInScreen(true)
let projectile = sprites.createProjectileFromSprite(assets.image`Ball`, Player1, randint(50, 75), randint(25, 50))
projectile.x += 3
projectile.setBounceOnWall(true)
projectile.setFlag(SpriteFlag.ShowPhysics, false)
info.player1.setScore(0)
info.player2.setScore(0)
game.onUpdate(function () {
  if (projectile.x > scene.screenWidth() / 2 && players == 1) {
      if (projectile.y > Player2.y) {
          Player2.y += 2
      } else {
          Player2.y += -2
      }
  }
})
game.onUpdate(function () {
  if (projectile.x > Player2.right) {
      info.player1.changeScoreBy(1)
      music.jumpUp.play()
      projectile.setPosition(Player1.x + 3, Player1.y)
      projectile.setVelocity(randint(50, 75), randint(25, 50))
  } else if (projectile.x < Player1.left) {
      info.player2.changeScoreBy(1)
      music.jumpUp.play()
      projectile.setPosition(Player2.x - 3, Player2.y)
      projectile.setVelocity(randint(-75, -50), randint(25, 50))
  }
})
```
```assetjson
{
"README.md": " ",
"assets.json": "",
"images.g.jres": "{\n    \"image1\": {\n        \"data\": \"hwQEABAAAAAREREREREREREREREREREREREREREREREREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Player 1\"\n    },\n    \"image2\": {\n        \"data\": \"hwQEABAAAAAREREREREREREREREREREREREREREREREREREREREREQ==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Player 2\"\n    },\n    \"image3\": {\n        \"data\": \"hwQEAAQAAAAREQAAEREAABERAAAREQAA\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"displayName\": \"Ball\"\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myImages\"\n    }\n}",
"images.g.ts": "// Auto-generated code. Do not edit.\nnamespace myImages {\n\n    helpers._registerFactory(\"image\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"image1\":\n            case \"Player 1\":return img`\n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n`;\n            case \"image2\":\n            case \"Player 2\":return img`\n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n`;\n            case \"image3\":\n            case \"Ball\":return img`\n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n1 1 1 1 \n`;\n        }\n        return null;\n    })\n\n    helpers._registerFactory(\"animation\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n",
"main.blocks": "<xml xmlns=\"https://developers.google.com/blockly/xml\"><variables><variable id=\"rz2=;8%bkqrt,ku)g}8M\">players</variable><variable id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</variable><variable id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</variable><variable id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</variable><variable id=\"|~*o`cGlL}Vg`sOzA~iz\">Picture</variable><variable id=\"d99wZJ-_8I(|Y|=w)gg;\">index</variable><variable type=\"KIND_SpriteKind\" id=\"qqVNHMhe/y7?3;Yc.M-g\">Player</variable><variable type=\"KIND_SpriteKind\" id=\"3M=CxbLYdCu}8gS@hg|C\">Projectile</variable><variable type=\"KIND_SpriteKind\" id=\"mZ@-)oD$D,$SWFG3:a32\">Food</variable><variable type=\"KIND_SpriteKind\" id=\"v|$._^oCK:dm*)Q]uVW=\">Enemy</variable></variables><block type=\"pxt-on-start\" x=\"20\" y=\"20\"><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"rz2=;8%bkqrt,ku)g}8M\">players</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"|~*o`cGlL}Vg`sOzA~iz\">Picture</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"image_create\"><value name=\"width\"><block type=\"scenescreenwidth\"/></value><value name=\"height\"><block type=\"scenescreenheight\"/></value></block></value><next><block type=\"pxt_controls_for\"><value name=\"VAR\"><shadow type=\"variables_get_reporter\"><field name=\"VAR\" id=\"d99wZJ-_8I(|Y|=w)gg;\">index</field></shadow></value><value name=\"TO\"><shadow type=\"math_whole_number\"><field name=\"NUM\">0</field></shadow><block type=\"scenescreenheight\"/></value><statement name=\"DO\"><block type=\"controls_if\"><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">LT</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"math_modulo\"><value name=\"DIVIDEND\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"d99wZJ-_8I(|Y|=w)gg;\">index</field></block></value><value name=\"DIVISOR\"><shadow type=\"math_number\"><field name=\"NUM\">6</field></shadow></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">4</field></shadow></value></block></value><statement name=\"DO0\"><block type=\"Image_setPixel\"><value name=\"picture\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"|~*o`cGlL}Vg`sOzA~iz\">Picture</field></shadow></value><value name=\"x\"><block type=\"math_arithmetic\"><field name=\"OP\">DIVIDE</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"scenescreenwidth\"/></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value></block></value><value name=\"y\"><block type=\"variables_get\"><field name=\"VAR\" id=\"d99wZJ-_8I(|Y|=w)gg;\">index</field></block></value><value name=\"c\"><shadow type=\"colorindexpicker\"><field name=\"index\">1</field></shadow></value></block></statement></block></statement><next><block type=\"gamesetbackgroundimage\"><value name=\"img\"><shadow type=\"background_image_picker\"/><block type=\"variables_get\"><field name=\"VAR\" id=\"|~*o`cGlL}Vg`sOzA~iz\">Picture</field></block></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Player 1`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image1\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"><field name=\"index\">8</field></shadow></value><value name=\"y\"><shadow type=\"positionPicker\"><field name=\"index\">60</field></shadow></value><next><block type=\"game_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></shadow></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">100</field></shadow></value><next><block type=\"spritesetsetstayinscreen\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreate\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Player 2`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image2\"}}</data></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value></block></value><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"><field name=\"index\">152</field></shadow></value><value name=\"y\"><shadow type=\"positionPicker\"><field name=\"index\">60</field></shadow></value><next><block type=\"spritesetsetstayinscreen\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"variables_set\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"spritescreateprojectilefromsprite\"><value name=\"img\"><shadow type=\"screen_image_picker\"><field name=\"img\">assets.image`Ball`</field><data>{\"commentRefs\":[],\"fieldData\":{\"img\":\"myImages.image3\"}}</data></shadow></value><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></shadow></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">50</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">75</field></shadow></value></block></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">25</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">50</field></shadow></value></block></value></block></value><next><block type=\"Sprite_blockCombine_change\"><field name=\"property\">Sprite.x@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">3</field></shadow></value><next><block type=\"spritesetsetbounceonwall\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">true</field></shadow></value><next><block type=\"spritesetsetflag\"><field name=\"flag\">SpriteFlag.ShowPhysics</field><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"on\"><shadow type=\"toggleOnOff\"><field name=\"on\">false</field></shadow></value><next><block type=\"pisetscore\"><field name=\"player\">info.player1</field><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value><next><block type=\"pisetscore\"><field name=\"player\">info.player2</field><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow></value></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></next></block></statement></block><block type=\"ctrlonbuttonevent\" x=\"1369\" y=\"20\"><field name=\"controller\">controller.player2</field><field name=\"button\">ControllerButton.Down</field><field name=\"event\">ControllerButtonEvent.Pressed</field><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"rz2=;8%bkqrt,ku)g}8M\">players</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value><next><block type=\"ctrlgame_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"controller\">controller.player2</field><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></shadow></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">100</field></shadow></value></block></next></block></statement></block><block type=\"ctrlonbuttonevent\" x=\"2116\" y=\"20\"><field name=\"controller\">controller.player2</field><field name=\"button\">ControllerButton.Up</field><field name=\"event\">ControllerButtonEvent.Pressed</field><statement name=\"HANDLER\"><block type=\"variables_set\"><field name=\"VAR\" id=\"rz2=;8%bkqrt,ku)g}8M\">players</field><value name=\"VALUE\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value><next><block type=\"ctrlgame_control_sprite\"><mutation xmlns=\"http://www.w3.org/1999/xhtml\" _expanded=\"2\" _input_init=\"true\"></mutation><field name=\"controller\">controller.player2</field><value name=\"sprite\"><shadow type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></shadow></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">0</field></shadow></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"><field name=\"speed\">100</field></shadow></value></block></next></block></statement></block><block type=\"gameupdate\" x=\"2863\" y=\"20\"><statement name=\"HANDLER\"><block type=\"controls_if\"><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_operation\"><field name=\"OP\">AND</field><value name=\"A\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">GT</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"math_arithmetic\"><field name=\"OP\">DIVIDE</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"scenescreenwidth\"/></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value></block></value></block></value><value name=\"B\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">EQ</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"variables_get\"><field name=\"VAR\" id=\"rz2=;8%bkqrt,ku)g}8M\">players</field></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value></block></value></block></value><statement name=\"DO0\"><block type=\"controls_if\"><mutation else=\"1\"/><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">GT</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.y</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.y</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value></block></value></block></value><statement name=\"DO0\"><block type=\"Sprite_blockCombine_change\"><field name=\"property\">Sprite.y@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">2</field></shadow></value></block></statement><statement name=\"ELSE\"><block type=\"Sprite_blockCombine_change\"><field name=\"property\">Sprite.y@set</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">-2</field></shadow></value></block></statement></block></statement></block></statement></block><block type=\"gameupdate\" x=\"20\" y=\"1207\"><statement name=\"HANDLER\"><block type=\"controls_if\"><mutation elseif=\"1\"/><value name=\"IF0\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">GT</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.right</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value></block></value></block></value><statement name=\"DO0\"><block type=\"pichangescore\"><field name=\"player\">info.player1</field><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value><next><block type=\"mixer_play_sound\"><field name=\"sound\">music.jumpUp</field><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"/><block type=\"math_arithmetic\"><field name=\"OP\">ADD</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">3</field></shadow></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"/><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.y</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></block></value></block></value><next><block type=\"spritesetvel\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">50</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">75</field></shadow></value></block></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">25</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">50</field></shadow></value></block></value></block></next></block></next></block></next></block></statement><value name=\"IF1\"><shadow type=\"logic_boolean\"><field name=\"BOOL\">TRUE</field></shadow><block type=\"logic_compare\"><field name=\"OP\">LT</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.left</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"k7D8@~,f^PwaT*^)7?Z/\">Player_1</field></block></value></block></value></block></value><statement name=\"DO1\"><block type=\"pichangescore\"><field name=\"player\">info.player2</field><value name=\"value\"><shadow type=\"math_number\"><field name=\"NUM\">1</field></shadow></value><next><block type=\"mixer_play_sound\"><field name=\"sound\">music.jumpUp</field><next><block type=\"spritesetpos\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"x\"><shadow type=\"positionPicker\"/><block type=\"math_arithmetic\"><field name=\"OP\">MINUS</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.x</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value></block></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">3</field></shadow></value></block></value><value name=\"y\"><shadow type=\"positionPicker\"/><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.y</field><value name=\"mySprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"#f.b?SPX2EsqPu1X23dc\">Player_2</field></block></value></block></value><next><block type=\"spritesetvel\"><value name=\"sprite\"><block type=\"variables_get\"><field name=\"VAR\" id=\"Ec|Im!!IX8Pe~*~zo^Yz\">projectile</field></block></value><value name=\"vx\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">-75</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">-50</field></shadow></value></block></value><value name=\"vy\"><shadow type=\"spriteSpeedPicker\"/><block type=\"device_random\"><value name=\"min\"><shadow type=\"math_number\"><field name=\"NUM\">25</field></shadow></value><value name=\"limit\"><shadow type=\"math_number\"><field name=\"NUM\">50</field></shadow></value></block></value></block></next></block></next></block></next></block></statement></block></statement></block><block type=\"spritesoverlap\" x=\"1121\" y=\"1207\"><value name=\"HANDLER_DRAG_PARAM_sprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">sprite</field></shadow></value><value name=\"kind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Player</field></shadow></value><value name=\"HANDLER_DRAG_PARAM_otherSprite\"><shadow type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">otherSprite</field></shadow></value><value name=\"otherKind\"><shadow type=\"spritekind\"><field name=\"MEMBER\">Projectile</field></shadow></value><statement name=\"HANDLER\"><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.vx@set</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">otherSprite</field></block></value><value name=\"value\"><block type=\"math_arithmetic\"><field name=\"OP\">MULTIPLY</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">-1.1</field></shadow></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.vx</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">otherSprite</field></block></value></block></value></block></value><next><block type=\"Sprite_blockCombine_set\"><field name=\"property\">Sprite.vy@set</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">otherSprite</field></block></value><value name=\"value\"><block type=\"math_arithmetic\"><field name=\"OP\">MULTIPLY</field><value name=\"A\"><shadow type=\"math_number\"><field name=\"NUM\">1.1</field></shadow></value><value name=\"B\"><shadow type=\"math_number\"><field name=\"NUM\">0</field></shadow><block type=\"Sprite_blockCombine_get\"><field name=\"property\">Sprite.vy</field><value name=\"mySprite\"><block type=\"argument_reporter_custom\"><mutation typename=\"Sprite\"/><field name=\"VALUE\">otherSprite</field></block></value></block></value></block></value><next><block type=\"mixer_play_note\"><value name=\"note\"><shadow type=\"device_note\"><field name=\"note\">494</field></shadow></value><value name=\"duration\"><shadow type=\"device_beat\"><field name=\"fraction\">BeatFraction.Half</field></shadow></value></block></next></block></next></block></statement></block></xml>",
"main.ts": "controller.player2.onButtonEvent(ControllerButton.Down, ControllerButtonEvent.Pressed, function () {\n    players = 2\n    controller.player2.moveSprite(Player_2, 0, 100)\n})\ncontroller.player2.onButtonEvent(ControllerButton.Up, ControllerButtonEvent.Pressed, function () {\n    players = 2\n    controller.player2.moveSprite(Player_2, 0, 100)\n})\nsprites.onOverlap(SpriteKind.Player, SpriteKind.Projectile, function (sprite, otherSprite) {\n    otherSprite.vx = -1.1 * otherSprite.vx\n    otherSprite.vy = 1.1 * otherSprite.vy\n    music.playTone(494, music.beat(BeatFraction.Half))\n})\nlet Player_2: Sprite = null\nlet players = 0\nplayers = 1\nlet Picture = image.create(scene.screenWidth(), scene.screenHeight())\nfor (let index = 0; index <= scene.screenHeight(); index++) {\n    if (index % 6 < 4) {\n        Picture.setPixel(scene.screenWidth() / 2, index, 1)\n    }\n}\nscene.setBackgroundImage(Picture)\nlet Player_1 = sprites.create(assets.image`Player 1`, SpriteKind.Player)\nPlayer_1.setPosition(8, 60)\ncontroller.moveSprite(Player_1, 0, 100)\nPlayer_1.setStayInScreen(true)\nPlayer_2 = sprites.create(assets.image`Player 2`, SpriteKind.Player)\nPlayer_2.setPosition(152, 60)\nPlayer_2.setStayInScreen(true)\nlet projectile = sprites.createProjectileFromSprite(assets.image`Ball`, Player_1, randint(50, 75), randint(25, 50))\nprojectile.x += 3\nprojectile.setBounceOnWall(true)\nprojectile.setFlag(SpriteFlag.ShowPhysics, false)\ninfo.player1.setScore(0)\ninfo.player2.setScore(0)\ngame.onUpdate(function () {\n    if (projectile.x > scene.screenWidth() / 2 && players == 1) {\n        if (projectile.y > Player_2.y) {\n            Player_2.y += 2\n        } else {\n            Player_2.y += -2\n        }\n    }\n})\ngame.onUpdate(function () {\n    if (projectile.x > Player_2.right) {\n        info.player1.changeScoreBy(1)\n        music.jumpUp.play()\n        projectile.setPosition(Player_1.x + 3, Player_1.y)\n        projectile.setVelocity(randint(50, 75), randint(25, 50))\n    } else if (projectile.x < Player_1.left) {\n        info.player2.changeScoreBy(1)\n        music.jumpUp.play()\n        projectile.setPosition(Player_2.x - 3, Player_2.y)\n        projectile.setVelocity(randint(-75, -50), randint(25, 50))\n    }\n})\n",
"pxt.json": "{\n    \"name\": \"JS Pong Personally Built Empty Test\",\n    \"description\": \"\",\n    \"dependencies\": {\n        \"device\": \"*\"\n    },\n    \"files\": [\n        \"main.blocks\",\n        \"main.ts\",\n        \"README.md\",\n        \"assets.json\",\n        \"tilemap.g.jres\",\n        \"tilemap.g.ts\",\n        \"images.g.jres\",\n        \"images.g.ts\"\n    ],\n    \"targetVersions\": {\n        \"branch\": \"v1.7.22\",\n        \"tag\": \"v1.7.22\",\n        \"commits\": \"https://github.com/microsoft/pxt-arcade/commits/fa9cc16632907b4dd59f733b62e573beded922dc\",\n        \"target\": \"1.7.22\",\n        \"pxt\": \"7.3.23\"\n    },\n    \"preferredEditor\": \"tsprj\"\n}\n",
"tilemap.g.jres": "{\n    \"transparency16\": {\n        \"data\": \"hwQQABAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA==\",\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"tilemapTile\": true\n    },\n    \"*\": {\n        \"mimeType\": \"image/x-mkcd-f4\",\n        \"dataEncoding\": \"base64\",\n        \"namespace\": \"myTiles\"\n    }\n}",
"tilemap.g.ts": "// Auto-generated code. Do not edit.\nnamespace myTiles {\n    //% fixedInstance jres blockIdentity=images._tile\n    export const transparency16 = image.ofBuffer(hex``);\n\n    helpers._registerFactory(\"tile\", function(name: string) {\n        switch(helpers.stringTrim(name)) {\n            case \"transparency16\":return transparency16;\n        }\n        return null;\n    })\n\n}\n// Auto-generated code. Do not edit.\n"
}
```
 




