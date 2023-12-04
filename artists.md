---
layout: none
permalink: /Artists/
title: Artists
---

{%- include avk_head.html -%}
<body>
    <header>
        <h1>Welcome to AVK Mini Project</h1>
    </header>
    <section>
        <h2>Aliya Tang, Kevin Du, Vivian Ni</h2>
        <section>
            <button onclick="window.location.href='{{ site.baseurl }}/ArtGallery'">Art Gallery</button>
            <button onclick="window.location.href='{{ site.baseurl }}/ArtGenerator'">Fibonacci Art Generator</button>
        </section>
    </section>
</body>
<footer>
        <p>&copy; 2023 Home Art Gallery</p>
</footer>

<style>
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
    section {
        text-align: center;
        margin-top: 40px;
        background-color: #F6F6F2;
    }
    h1 {
        font-family: Optima, sans-serif;
        color: #388087; 
        font-size: 75px;
        background-color: #F6F6F2;
        margin-top: 150px;
    }
    h2 {
        font-family: Optima, sans-serif;
        color: #2f5154; 
        font-size: 35px;
        background-color: #F6F6F2;
        text-align: center;
    }
    button {
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
