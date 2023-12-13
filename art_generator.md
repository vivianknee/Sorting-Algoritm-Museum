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
        <h6 id="number"></h6>
        <h6 id="fibMethod"></h6>
        <div><input type="number" id="fibNumber" placeholder="Enter a number" /></div>
        <div class="button-space">
            <button onclick="generateFibonacci('binet')">Generate Art (Binet)</button>
            <button onclick="generateFibonacci('golden')">Generate Art (Golden Ratio)</button>
            <button onclick="clearCanvas()">Clear</button>
            <button onclick="saveCanvasAsImage()">Save Image</button>
        </div>
    </header>
    <main>
        <canvas id="fibCanvas" width="600" height="400"></canvas>
    </main>
</body>
<script>
        const canvas = document.getElementById('fibCanvas');
    const ctx = canvas.getContext('2d');
    async function generateFibonacci(method) {
            const numberInput = document.getElementById('fibNumber').value;
            console.log(numberInput);
            const deployURL = "http://localhost:8013"; // Replace this with your deployment URL
            const fibMethod = document.getElementById('fibMethod');
            const minId = numberInput; // Minimum ID value
            const maxId = numberInput; // Maximum ID value (replace with your maximum ID value)
            const randomId = Math.floor(Math.random() * (maxId - minId + 1)) + minId;
            try {
                const startTime = performance.now(); // Capture start time
                const response = await fetch(`${deployURL}/api/fibo/${method}/${randomId}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({ id: randomId })
                });
                if (response.ok) {
                    const data = await response.json();
                    const endTime = performance.now(); // Capture end time
                    const timeTaken = endTime - startTime; // Calculate time taken
                    handleFibonacciData(data, method, timeTaken); // Pass time to the handler
                } else {
                    throw new Error('Failed to fetch data');
                }
            } catch (error) {
                console.error('Error:', error);
            }
        }
function handleFibonacciData(data, method, timeTaken) {
    const generationTime = document.getElementById('generationTime');
    generationTime.innerText = `Time taken for ${method} method: ${timeTaken} milliseconds`;
    const fibMethod = document.getElementById('fibMethod');
    fibMethod.innerText = `Fibonacci Method Used: ${method}`;
    const numberInput = document.getElementById('fibNumber').value;
   const numberThing = document.getElementById('number');
    numberThing.innerText = `Number: ${numberInput}`;  
    const canvas = document.getElementById('fibCanvas');
    const context = canvas.getContext('2d');
    context.clearRect(0, 0, canvas.width, canvas.height); // Clear canvas
    const centerX = canvas.width / 2;
    const centerY = canvas.height / 2;
    let angle = 0;
    data.forEach(num => {
        const radius = num * 5; // Scale the radius for better visualization
        const x = centerX + radius * Math.cos(angle);
        const y = centerY + radius * Math.sin(angle);       
        // Generate random colors
        const randomColor = `rgb(${Math.random() * 255},${Math.random() * 255},${Math.random() * 255})`;
        context.beginPath();
        context.arc(x, y, radius, 0, Math.PI * 2);
        context.strokeStyle = randomColor; // Set stroke color
        context.stroke();    
        angle += Math.PI / 8; // Increment the angle for the next iteration
    });
}
//Save Image
    function saveCanvasAsImage() {
        const link = document.createElement('a');
        link.download = 'fibonacci_art.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
    }
    // Clear Canvas function
    function clearCanvas() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    }
</script>
</html>

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