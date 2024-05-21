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

### control structures in game control

- **conditional statements**: used for checking conditions like player health, collision detection, etc.
- **loop statements**: primarily used to update and draw gameobjects in the game loop.

### unique gamesetup collection of javascript objects

```javascript
const player = new GameObject('Player', 50, 50, 30, 30);
const enemy = new GameObject('Enemy', 100, 100, 30, 30);

const level1 = new GameLevel(1);
level1.addGameObject(player);
level1.addGameObject(enemy);

const levels = [level1];
```

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

**Drawing Time!**  

<div style="text-align: center; margin-top: 20px; margin-bottom: 20px;">
  <img src="{{site.baseurl}}/images/anito/flowchart.drawio.png" alt="Diagram showing Goomba Collisions" />
</div>  

This diagram illustrates what occurs when a Goomba, a Game Object, interacts with other Game Objects within the Game Level.