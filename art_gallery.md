---
layout: none
title: Art Gallery
permalink: /ArtGallery/
---

{%- include avk_head.html -%}

<!-- sort by likes -->

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Art Gallery</title>
    <!-- 
    <link rel="stylesheet" href="{{ site.baseurl }}/assets/css/styles.css">
    -->
    <script src="gallery.js" defer></script>
</head>
<body>
    <header>
        <h1>Art Gallery</h1>
    </header>
    <main>
        <section class="art-piece" data-artid="1">
            <h2>Art Piece 1</h2>
            <div class="art-content">
                <!-- Display the art piece here -->
                <img src="art1.jpg" alt="Art Piece 1">
            </div>
            <div class="like-section">
                <button onclick="likeArt(1)">Like</button>
                <span class="likes-count">0</span>
            </div>
        </section>
        <section class="art-piece" data-artid="2">
            <h2>Art Piece 2</h2>
            <div class="art-content">
                <!-- Display the art piece here -->
                <img src="art2.jpg" alt="Art Piece 2">
            </div>
            <div class="like-section">
                <button onclick="likeArt(2)">Like</button>
                <span class="likes-count">0</span>
            </div>
        </section>
        <!-- Add more art pieces with similar structure -->
    </main>
    <footer>
        <p>&copy; 2023 Art Gallery</p>
    </footer>
</body>

</html>
<script>
    // gallery.js
// Simulating an array of art pieces with their IDs and initial likes
const artPieces = [
    { id: 1, likes: 0 },
    { id: 2, likes: 0 },
    // Add more art pieces with their IDs and initial likes
];
function likeArt(artId) {
    const artPiece = artPieces.find(piece => piece.id === artId);
    if (artPiece) {
        artPiece.likes++;
        updateLikesCount(artId, artPiece.likes);
    }
}
function updateLikesCount(artId, likes) {
    const likeSection = document.querySelector(`.art-piece[data-artid="${artId}"] .likes-count`);
    if (likeSection) {
        likeSection.textContent = likes;
    }
}
</script>

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
        margin-bottom: 30px;
        border: 1px solid #6FB3B8;
        padding: 10px;
        border-radius: 8px;
        background-color: #BADFE7; 
    }
    h1 {
        font-family: Optima, sans-serif;
        color: #388087; 
        font-size: 50px;
        background-color: #F6F6F2;
    }
    h2 {
        font-family: Optima, sans-serif;
        color: #2f5154; 
        font-size: 35px;
        background-color: #BADFE7;
    }
    img {
        max-width: 100%; 
        height: auto;
    }
    .art-content {
        background-color: #BADFE7;
        margin-top: 10px;
    }
    .like-section {
        margin-top: 10px;
        display: flex;
        align-items: center;
        background-color: #BADFE7;
    }
    button {
        background-color: #60e085;
        color: #fff;
        padding: 5px 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    .likes-count {
        margin-left: 5px;
        color: #333;
        background-color: #ffffff;
        padding: 5px 10px;
        border-radius: 5px;
        font-size: 20px;
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
