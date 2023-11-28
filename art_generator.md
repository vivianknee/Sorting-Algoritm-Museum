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
function generateArt() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    const method = Math.random() < 0.5 ? 'recursive' : 'goldenRatio';
    if (method === 'recursive') {
        generateRecursiveArt();
    } else {
        generateGoldenRatioArt();
    }
}
function generateRecursiveArt() {
    // Recursive Relation Method to generate Fibonacci art
    // Implement your recursive relation logic here
    // Example:
    const maxIterations = 100;
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    recursiveDraw(centerX, centerY, 1, 1, 0, maxIterations);
}
function recursiveDraw(x, y, a, b, count, maxIterations) {
    if (count < maxIterations) {
        ctx.beginPath();
        ctx.arc(x, y, a * 5, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${count * 3}, 70%, 50%)`; // Color based on iteration
        ctx.fill();
        const nextX = x + b * 5 * Math.cos(count);
        const nextY = y + b * 5 * Math.sin(count);
        recursiveDraw(nextX, nextY, b, a + b, count + 1, maxIterations);
    }
}
function generateGoldenRatioArt() {
    // Golden Ratio Method to generate Fibonacci art
    // Implement your golden ratio logic here
    const goldenRatio = (1 + Math.sqrt(5)) / 2;
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    let prevA = 0;
    let prevB = 1;
    for (let i = 0; i < 150; i++) {
        const temp = prevA;
        prevA = prevB;
        prevB = temp + prevB;
        const radius = prevA * 5; // Adjust the multiplier for size
        const angle = i * (Math.PI / 180) * goldenRatio;
        const x = centerX + radius * Math.cos(angle);
        const y = centerY + radius * Math.sin(angle);
        ctx.beginPath();
        ctx.arc(x, y, 1, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${i * 3}, 70%, 50%)`; // Color based on iteration
        ctx.fill();
    }
}
function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
}
</script>