---
layout: home
title: Art Generator
---
<!DOCTYPE html>
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
