---
toc: true
comments: true
layout: post
title:  Articulation Blog
subtitle: Katelyn Gelle
cover-img: /images/swordplaylink.gif
description: wauaauw
type: plans
courses: { csse: {week: 11} }
categories: [C1.4]
---

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
  <img src="{{site.baseurl}}/images/anito/canyouhearmelink.gif" alt="Link, The Legend of Zelda: Skyward Sword" />
</div>  

**Articulation Blog**  

### gameobjects to gamelevel

1. **gameobjects** are individual entities in the game like players, enemies, or obstacles. we'll define them using javascript objects.

```javascript
class GameObject {
    constructor(name, x, y, width, height) {
        this.name = name;
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    draw(context) {
        context.fillStyle = 'blue';
        context.fillRect(this.x, this.y, this.width, this.height);
    }

    update() {
        // update logic for game object
    }
}
```

- **Definition**: a gameobject represents any interactive element in the game. it has properties such as position (x, y), dimensions (width, height), and a name. the `draw` method renders the object on the screen using the given context, while the `update` method handles the object's behavior over time.

2. **gamelevel** is a collection of gameobjects. we can define a gamelevel as an array of gameobjects.

```javascript
class GameLevel {
    constructor(levelNumber) {
        this.levelNumber = levelNumber;
        this.gameObjects = [];
    }

    addGameObject(gameObject) {
        this.gameObjects.push(gameObject);
    }

    draw(context) {
        this.gameObjects.forEach(obj => obj.draw(context));
    }

    update() {
        this.gameObjects.forEach(obj => obj.update());
    }
}
```

- **Definition**: a gamelevel consists of multiple gameobjects, representing a specific stage or environment in the game. the `addGameObject` method allows adding new objects to the level. the `draw` and `update` methods ensure that all gameobjects within the level are rendered and updated correctly.

### gamelevel to an array of gamelevels

we can create multiple levels and store them in an array.

```javascript
const levels = [];

for (let i = 0; i < 5; i++) {
    const level = new GameLevel(i + 1);
    level.addGameObject(new GameObject('Player', 50, 50, 30, 30));
    level.addGameObject(new GameObject('Enemy', 100, 100, 30, 30));
    levels.push(level);
}
```

- **Definition**: this code snippet demonstrates the creation of multiple game levels, each containing a player and an enemy. the levels are stored in an array for easy access and management. each level is assigned a unique number, ensuring they can be differentiated.

### control structures in game control

- **conditional statements**: used for checking conditions like player health, collision detection, etc.
- **loop statements**: primarily used to update and draw gameobjects in the game loop.

- **Definition**: control structures are fundamental to game logic. conditional statements (`if`, `else`) allow the game to make decisions based on certain conditions, such as detecting collisions or checking if a player's health is zero. loop statements (`for`, `while`) enable repetitive actions, like continuously updating and drawing game objects in the game loop, ensuring the game runs smoothly and responsively.

### unique gamesetup collection of javascript objects

```javascript
const player = new GameObject('Player', 50, 50, 30, 30);
const enemy = new GameObject('Enemy', 100, 100, 30, 30);

const level1 = new GameLevel(1);
level1.addGameObject(player);
level1.addGameObject(enemy);

const levels = [level1];
```

- **Definition**: this example shows a specific setup where a player and an enemy gameobject are created and added to level 1. the levels array then holds this single level. this setup can be expanded to include more objects and levels, forming the structure of the game.

### using gamelevel in gamecontrol

```javascript
class GameControl {
    constructor(levels) {
        this.levels = levels;
        this.currentLevelIndex = 0;
    }

    startLevel() {
        const currentLevel = this.levels[this.currentLevelIndex];
        // start level logic
    }

    endLevel() {
        this.currentLevelIndex++;
        if (this.currentLevelIndex < this.levels.length) {
            this.startLevel();
        } else {
            console.log('game over!');
        }
    }
}
```

- **Definition**: the GameControl class manages the progression through different levels. it starts with the first level and can transition to the next level upon completion. if all levels are completed, it signals the end of the game. this class ensures that levels are started and ended correctly, maintaining the game's flow.

### using gameloop to call gameenv methods

```javascript
class GameEnv {
    constructor(context) {
        this.context = context;
    }

    updateAndDraw(gameLevel) {
        gameLevel.update();
        this.context.clearRect(0, 0, canvas.width, canvas.height);
        gameLevel.draw(this.context);
    }
}

function gameLoop(gameEnv, gameLevel) {
    function loop() {
        gameEnv.updateAndDraw(gameLevel);
        requestAnimationFrame(loop);
    }
    loop();
}

const canvas = document.getElementById('gameCanvas');
const context = canvas.getContext('2d');
const gameEnv = new GameEnv(context);

gameLoop(gameEnv, levels[0]);
```

- **Definition**: the GameEnv class is responsible for managing the rendering context. it provides a method to update and draw the game level. the `gameLoop` function continuously calls this method, ensuring the game state is updated and rendered frame by frame. this loop runs indefinitely, creating the real-time interaction in the game.

### inspect/elements to examine gameobjects

open your browser's developer tools (usually f12 or right-click -> inspect), then go to the 'elements' tab. you can see your canvas element there. to see changes in properties, add console logs in your update methods.

```javascript
class GameObject {
    constructor(name, x, y, width, height) {
        this.name = name;
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }

    draw(context) {
        context.fillStyle = 'blue';
        context.fillRect(this.x, this.y, this.width, this.height);
    }

    update() {
        console.log(`${this.name} position: (${this.x}, ${this.y})`);
    }
}
```

- **Definition**: using browser developer tools, you can inspect the canvas element and track changes to gameobjects' properties in real-time. by adding console logs in the `update` method, you can output information about the gameobject's state, such as its position, to the console. this is useful for debugging and understanding how your game logic affects game objects.

### determining end of level and transitioning

```javascript
class GameControl {
    constructor(levels) {
        this.levels = levels;
        this.currentLevelIndex = 0;
    }

    startLevel() {
        const currentLevel = this.levels[this.currentLevelIndex];
        console.log(`starting level ${currentLevel.levelNumber}`);
    }

    endLevel() {
        this.currentLevelIndex++;
        if (this.currentLevelIndex < this.levels.length) {
            this.startLevel();
        } else {
            console.log('game over!');
        }
    }

    checkLevelEndCondition() {
        const currentLevel = this.levels[this.currentLevelIndex];
        if (currentLevel.gameObjects.length === 0) {
            this.endLevel();
        }
    }
}
```

- **Definition**: the GameControl class also handles the end-of-level conditions and transitioning between levels. the `checkLevelEndCondition` method determines if the current level should end, based on criteria such as whether all gameobjects are eliminated. if the level ends, it transitions to the next level or concludes the game if all levels are completed.

in your game loop, you can check the level end condition like this:

```javascript
function gameLoop(gameEnv, gameControl) {
    function loop() {
        const currentLevel = gameControl.levels[gameControl.currentLevelIndex];
        gameEnv.updateAndDraw(currentLevel);
        gameControl.checkLevelEndCondition();
        requestAnimationFrame(loop);
    }
    loop();
}

const gameControl = new GameControl(levels);
gameControl.startLevel();
gameLoop(gameEnv, gameControl);
```

- **Definition**: integrating the game control into the game loop, this snippet ensures that the game state is continuously updated, drawn, and checked for level completion. if a level ends, it transitions to the next level seamlessly, maintaining the game's flow.

### drawing time!

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
  <img src="{{site.baseurl}}/images/anito/flowchart.drawio.png" alt="Diagram showing Goomba Collisions" />
</div>

this diagram illustrates what occurs when a goomba, a game object, interacts with other game objects within the game level.

1. **goomba detection**: the goomba's position is checked against other game objects to detect a collision.

- **Definition**: goomba detection involves comparing the goomba's position and size with other game objects to see if they overlap. this is usually done using collision detection algorithms that check if the bounding boxes of the objects intersect.

2. **collision response**: if a collision is detected, appropriate actions are taken, such as changing the goomba's direction or reducing player health.

- **Definition**: collision response defines what happens after a collision is detected. for a goomba, this might mean bouncing back, changing direction, or triggering a hit effect on a player. the response depends on the game.