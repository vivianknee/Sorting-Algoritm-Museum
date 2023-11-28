---
layout: none
title: Art Generator
permalink: /ArtGenerator/
---

{%- include avk_head.html -%}

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fibonacci Art Generator</title>
    <style>
        /* Add your styling here */
        canvas {
            border: 1px solid #000;
            display: block;
            margin: 20px auto;
        }
    </style>
    <script src="fibonacci-art.js" defer></script>
</head>

<body>
    <header>
        <h1>Fibonacci Art Generator</h1>
        <div>
            <button onclick="generateArt()">Generate Art</button>
            <button onclick="clearCanvas()">Clear</button>
        </div>
    </header>
    <main>
        <canvas id="fibCanvas" width="600" height="400"></canvas>
    </main>
    <footer>
        <p>&copy; 2023 Fibonacci Art Gallery</p>
    </footer>
</body>

</html>
<script>
// fibonacci-art.js
const canvas = document.getElementById('fibCanvas');
const ctx = canvas.getContext('2d');
function fibonacciBinet(n) {
    const phi = (1 + Math.sqrt(5)) / 2; // Golden ratio
    const sqrt5 = Math.sqrt(5);
    const fibN = Math.round((Math.pow(phi, n) - Math.pow(1 - phi, n)) / sqrt5);
    return fibN;
}
function generateArt() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    const method = Math.random() < 0.5 ? 'recursive' : 'goldenRatio';
    if (method === 'recursive') {
        generateRecursiveArt();
    } else {
        generateRecursiveArtWithBinet(12);
    }
}
function generateRecursiveArt() {
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    recursiveDraw(centerX, centerY, 1, 1, 0, 20);
}
function recursiveDraw(x, y, a, b, count, maxIterations) {
    if (count < maxIterations) {
        ctx.beginPath();
        ctx.arc(x, y, a * 5, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${(count * 20) % 360}, 70%, 50%)`; // Adjust color based on iteration
        ctx.fill();
        const nextX = x + b * 5 * Math.cos(count);
        const nextY = y + b * 5 * Math.sin(count);
        recursiveDraw(nextX, nextY, b, a + b, count + 1, maxIterations);
    }
}
function generateRecursiveArtWithBinet(maxIterations) {
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    recursiveDrawWithBinet(centerX, centerY - 350, 1, maxIterations, 0);
}
function recursiveDrawWithBinet(x, y, size, remainingIterations, angle) {
    if (remainingIterations > 0) {
        ctx.beginPath();
        ctx.arc(x, y, size * 3.2, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${(size * 20 + remainingIterations * 10) % 360}, 70%, 50%)`; // Adjust color based on size and iteration
        ctx.fill();
        const newSize = fibonacciBinet(remainingIterations); // Use Binet formula for size
        const nextX = x + size * 5 * Math.cos(angle); // Adjust x-position based on angle
        const nextY = y + size * 5 * Math.sin(angle); // Adjust y-position based on angle
        const newAngle = angle + Math.PI / 3; // Increment angle for each iteration
        recursiveDrawWithBinet(nextX, nextY, newSize / 2, remainingIterations - 1, newAngle);
    }
}
function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
}
</script>