
---
title: Javascript Snake Game
subtitle: Built Javascript snake game
description: Javascript code to create a snake game using HTML, CSS and Javascript.
slug: javascript-snake-game
tags: [javascript, snippets]
featured_image: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Javascript%20Snake%20Game,co_rgb:fff/javascriptwithexample/bg1.png
thumbnail: https://res.cloudinary.com/harendra21/image/upload/l_text:Roboto_50_bold:Javascript%20Snake%20Game,co_rgb:fff/javascriptwithexample/bg1.png
comments: true
date: 2023-12-14
toc: false
draft: false
---


Creating a JavaScript Snake Game involves using HTML for the structure, CSS for styling, and JavaScript for the game logic. Here's a simple example of a Snake Game:

HTML (index.html):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Snake Game</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="game-board"></div>
    <script src="script.js"></script>
</body>
</html>
```

CSS (style.css):

```css
#game-board {
    display: grid;
    grid-template-columns: repeat(20, 20px);
    grid-template-rows: repeat(20, 20px);
}
.snake, .food {
    width: 20px;
    height: 20px;
}
.snake {
    background-color: green;
}
.food {
    background-color: red;
}
```

JavaScript (script.js):

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const board = document.getElementById('game-board');
    const gridSize = 20;
    let snake = [{ x: 10, y: 10 }];
    let food = getRandomPosition();

    function draw() {
        board.innerHTML = '';
        drawSnake();
        drawFood();
    }

    function drawSnake() {
        snake.forEach(segment => {
            const snakeElement = createGameElement('div', 'snake');
            snakeElement.style.gridRowStart = segment.y;
            snakeElement.style.gridColumnStart = segment.x;
            board.appendChild(snakeElement);
        });
    }

    function drawFood() {
        const foodElement = createGameElement('div', 'food');
        foodElement.style.gridRowStart = food.y;
        foodElement.style.gridColumnStart = food.x;
        board.appendChild(foodElement);
    }

    function createGameElement(tagName, className) {
        const element = document.createElement(tagName);
        element.className = className;
        return element;
    }

    function getRandomPosition() {
        return {
            x: Math.floor(Math.random() * gridSize) + 1,
            y: Math.floor(Math.random() * gridSize) + 1
        };
    }

    function move() {
        const head = { ...snake[0] };
        switch (direction) {
            case 'UP':
                head.y--;
                break;
            case 'DOWN':
                head.y++;
                break;
            case 'LEFT':
                head.x--;
                break;
            case 'RIGHT':
                head.x++;
                break;
        }

        if (head.x === food.x && head.y === food.y) {
            snake.push({});
            food = getRandomPosition();
        }

        snake.unshift(head);
        snake.pop();
    }

    function checkCollision() {
        const head = snake[0];
        return (
            head.x < 1 || head.x > gridSize ||
            head.y < 1 || head.y > gridSize ||
            snake.slice(1).some(segment => segment.x === head.x && segment.y === head.y)
        );
    }

    let direction = 'RIGHT';

    window.addEventListener('keydown', event => {
        switch (event.key) {
            case 'ArrowUp':
                direction = 'UP';
                break;
            case 'ArrowDown':
                direction = 'DOWN';
                break;
            case 'ArrowLeft':
                direction = 'LEFT';
                break;
            case 'ArrowRight':
                direction = 'RIGHT';
                break;
        }
    });

    function gameLoop() {
        move();
        if (checkCollision()) {
            alert('Game Over!');
            snake = [{ x: 10, y: 10 }];
            direction = 'RIGHT';
        }
        draw();
    }

    setInterval(gameLoop, 200);
});
```

This is a basic implementation, and you can enhance it further by adding features such as score tracking, increasing difficulty, or adding sound effects.