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
// Function to generate a random ID within a specified range
function generateRandomId(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
// Function to handle the POST request to the backend with a randomly generated ID
async function generateFibonacciArt() {
    var deployURL = "http://localhost:8013";
    const minId = 1; // Minimum ID value
    const maxId = 10; // Maximum ID value (replace with your maximum ID value)
    const randomId = generateRandomId(minId, maxId);
    try {
        const response = await fetch(deployURL+`/api/fibo/${randomId}`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ id: randomId }) // Sending the random ID to the backend
        });
        if (response.ok) {
            const data = await response.json();
            handleFibonacciData(data);
        } else {
            throw new Error('Failed to fetch data');
        }
    } catch (error) {
        console.error('Error:', error);
    }
}
// Function to handle the received Fibonacci data and generate art
function handleFibonacciData(data) {
    // Handle the received data and generate art based on the response
    // This might involve iterating through the data and creating the art based on the Fibonacci sequence
    // Example: Displaying Fibonacci method used and generating art
    const methods = Object.keys(data);
    methods.forEach(method => {
        const sequence = data[method];
        console.log(`Fibonacci Method Used: ${method}`);
        console.log(`Fibonacci Sequence: ${sequence.join(', ')}`);
        // Generate art based on the sequence received from the backend
        // Modify this part to generate your art based on the Fibonacci sequence
    });
}
// Event listener for the "Generate Art" button
const generateButton = document.getElementById('generateButton');
generateButton.addEventListener('click', generateFibonacciArt);
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