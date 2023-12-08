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
    <script src="fibonacci-art.js" defer></script>
</head>

<body>
    <header>
        <h1>Fibonacci Art Generator</h1>
        <h6 id="generationTime"></h6>
        <h6 id="fibMethod"></h6> <!-- Added this line for displaying the Fibonacci method -->
        <div class="button-space">
            <button onclick="generateArt()">Generate Art</button>
            <button onclick="clearCanvas()">Clear</button>
            <button onclick="saveCanvasAsImage()">Save Image</button>
        </div>
    </header>
    <main>
        <canvas id="fibCanvas" width="600" height="400"></canvas>
    </main>
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
    const startTime = performance.now();
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    const method = Math.random(); // Randomly choose a method
    let generationTime;
    if (method < 0.25) {
        displayFibMethod('recursive');
        generateRecursiveArt();
    } else if (method < 0.5) {
        displayFibMethod('Binet formula');
        generateRecursiveArtWithBinet(20);
    } else if (method < 0.75) {
        displayFibMethod('iterative');
        generateIterativeArt();
        generationTime = performance.now() - startTime;
    } else {
        displayFibMethod('matrix');
        generateMatrixArt();
        generationTime = performance.now() - startTime;
    }
    if (!generationTime) {
        generationTime = performance.now() - startTime;
    }
    displayGenerationTime(generationTime);
}
function drawCircle(x, y, radius) {
    ctx.beginPath();
    ctx.arc(x, y, radius * 5, 0, Math.PI * 2);
    ctx.fillStyle = `hsl(${Math.random() * 360}, 70%, 50%)`;
    ctx.fill();
}
function displayFibMethod(method) {
    const fibMethodElement = document.getElementById('fibMethod');
    fibMethodElement.textContent = `Fibonacci Method Used: ${method}`;
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
        ctx.fillStyle = `hsl(${Math.random() * 360}, 70%, 50%)`; // Adjust color based on iteration
        ctx.fill();
        const nextX = x + b * 5 * Math.cos(count);
        const nextY = y + b * 5 * Math.sin(count);
        recursiveDraw(nextX, nextY, b, a + b, count + 1, maxIterations);
    }
}
function displayGenerationTime(time) {
    const generationTimeElement = document.getElementById('generationTime');
    generationTimeElement.textContent = `Generation Time: ${time.toFixed(2)} milliseconds`;
}
function generateRecursiveArtWithBinet(maxIterations) {
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 1;
    recursiveDrawWithBinet(centerX, centerY - 350, 0.5, maxIterations, 0);
}
function fibonacciBinet(n) {
    return Math.round(
        (1 / Math.sqrt(5)) *
        (Math.pow((1 + Math.sqrt(5)) / 2, n) - Math.pow((1 - Math.sqrt(5)) / 2, n))
    );
}
function recursiveDrawWithBinet(x, y, size, remainingIterations, angle) {
    if (remainingIterations > 0) {
        ctx.beginPath();
        ctx.arc(x, y, size * 3.2, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${(size * 20 + remainingIterations * 10) % 360}, 70%, 50%)`; // Adjust color based on size and iteration
        ctx.fill();
        const newSize = fibonacciBinet(remainingIterations); // Use Binet formula for size
        const nextX = x + size * 0.05 * Math.cos(angle); // Adjust x-position based on angle
        const nextY = y + size * 0.05 * Math.sin(angle); // Adjust y-position based on angle
        const newAngle = angle + Math.PI / 3; // Increment angle for each iteration
        recursiveDrawWithBinet(nextX, nextY, newSize * 0.3, remainingIterations - 1, newAngle);
    }
}
// Iterative
function fibonacciIterative(n) {
    let a = 0, b = 1;
    for (let i = 2; i <= n; i++) {
        let temp = a + b;
        a = b;
        b = temp;
    }
    return b;
}
function generateIterativeArt() {
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    const maxIterations = 20;
    let x = centerX;
    let y = centerY;
    let a = 1;
    let b = 1;
    let count = 0;
    while (count < maxIterations) {
        ctx.beginPath();
        ctx.arc(x, y, a * 5, 0, Math.PI * 2);
        ctx.fillStyle = `hsl(${Math.random() * 360}, 70%, 50%)`; // Adjust color based on iteration
        ctx.fill();
        const nextX = x + b * 5 * Math.cos(count);
        const nextY = y + b * 5 * Math.sin(count);
        x = nextX;
        y = nextY;
        const temp = a;
        a = b;
        b = temp + b;
        count++;
    }
}
// Matrix
function power(matrix, n) {
    let result = [[1, 0], [0, 1]];
    while (n > 0) {
        if (n % 2 === 1) {
            result = multiplyMatrices(result, matrix);
        }
        matrix = multiplyMatrices(matrix, matrix);
        n = Math.floor(n / 2);
    }
    return result;
}
function multiplyMatrices(matrix1, matrix2) {
    let result = [];
    for (let i = 0; i < matrix1.length; i++) {
        result[i] = [];
        for (let j = 0; j < matrix2[0].length; j++) {
            let sum = 0;
            for (let k = 0; k < matrix1[0].length; k++) {
                sum += matrix1[i][k] * matrix2[k][j];
            }
            result[i][j] = sum;
        }
    }
    return result;
}
function fibonacciMatrix(n) {
    const baseMatrix = [[1, 1], [1, 0]];
    if (n === 0) return 0;
    const result = power(baseMatrix, n - 1);
    return result[0][0];
}
function generateMatrixArt() {
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    let a = 0, b = 1;
    let angle = 0;
    const scale = 12; // Adjust scaling factor
    for (let i = 0; i < 20; i++) { // Adjust iterations as needed
        const fibNumber = fibonacciMatrix(i); // Generate Fibonacci number using matrix method
        const radius = fibNumber * scale;
        // Calculate position based on polar coordinates
        const x = centerX + radius *0.5* Math.cos(angle);
        const y = centerY + radius *0.5* Math.sin(angle);
        drawCircle(x, y, fibNumber);
        // Update angle for the next circle placement
        angle += Math.PI / 2; // You can experiment with different angles
    }
}
//Save Image
function saveCanvasAsImage() {
    const link = document.createElement('a');
    link.download = 'fibonacci_art.png';
    link.href = canvas.toDataURL('image/png');
    link.click();
}
function clearCanvas() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
}
</script>

<style>
    canvas {
        border: 1px solid #6FB3B8;
        display: block;
        margin: 5px auto;
    }
    .button-space {
        background-color: #F6F6F2;
        text-align: center;
    }
    body {
        font-family: 'Arial', sans-serif;
        margin: 0;
        padding: 0;
        background-color: #F6F6F2;
        color: #333;
    }
    header {
        background-color: #F6F6F2;
        color: #F6F6F2;
        padding: 10px;
        text-align: center;
    }
    main {
        padding: 20px;
        background-color: #F6F6F2;
    }
    h1 {
        font-family: Optima, sans-serif;
        color: #388087; 
        font-size: 50px;
        background-color: #F6F6F2;
    }
    h6 {
        font-family: Optima, sans-serif;
        color: red; 
        font-size: 25px;
        background-color: #F6F6F2;
    }
    button {
        margin-top: 20px;
        background-color: #60e085;
        color: #fff;
        padding: 5px 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    footer {
        background-color: #F6F6F2;
        font-family: "Times New Roman", sans-serif;
        color: #388087;
        text-align: center;
        padding: 10px;
        position: fixed;
        bottom: 0;
        width: 100%;
    }
</style>