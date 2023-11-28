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
    // Your logic to generate Fibonacci art goes here
    // For example, drawing a simple Fibonacci pattern as a placeholder
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    let a = 1;
    let b = 1;
    ctx.beginPath();
    ctx.moveTo(canvas.width / 2, canvas.height / 2);
    for (let i = 0; i < 100; i++) {
        const temp = a;
        a = b;
        b = temp + b;
        ctx.lineTo(canvas.width / 2 + a, canvas.height / 2 + b);
    }
    ctx.strokeStyle = 'blue';
    ctx.stroke();
}
function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
}

</script>