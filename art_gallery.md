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
</head>
<body>
    <header>
        <h1>Welcome to the Art Gallery</h1>
    </header>
    <main id="art_root">
    </main>
</body>

</html>
<script>
    //get request to display art
    function getArtWorks() {
        fetch('http://localhost:8013/api/art/')
            .then(response => response.json())
            .then(data => {
                formatArt(data);  
            })
            .catch(err => {
                console.log(err);
            });
    }
    getArtWorks();
    //format display and population of data
    function formatArt(arts) {
        // find the root div
         arts.forEach(art =>{
            //outer most div
            const root_div = document.getElementById("art_root");
            //individual artwork div
            const art_section = document.createElement("section");
            art_section.className = "art_piece";
            // label artwork
            const art_label = document.createElement("h2")
            art_label.innerHTML += art.artName;
            //img inside art div
            const img_div = document.createElement('div');
            img_div.className = "img_div"
            const img = document.createElement('img');
            img.src = "{{ site.baseurl }}/images/" + art.id + ".jpg";
            img.width = "350";
            img.height = "300";
            console.log(img.src);
            img_div.appendChild(img);
            //format likes inside like div
            const like_div = document.createElement('div');
            like_div.className = "like_div";
            const button = document.createElement('button');
            button.className = "like_button"
            button.innerHTML = "Like";
            const span = document.createElement('span');
            span.className = "likes_count"
            span.innerHTML += art.like;
            //append
            like_div.appendChild(button);
            like_div.appendChild(span);
            art_section.appendChild(art_label);
            art_section.appendChild(img_div);
            art_section.appendChild(like_div);
            root_div.appendChild(art_section);
        });
    }
    formatArt(arts);
    //post request to update likes
    //
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
    .art_piece {
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
    .img_div {
        background-color: #BADFE7;
        margin-top: 10px;
    }
    .like_div {
        margin-top: 10px;
        display: flex;
        align-items: center;
        background-color: #BADFE7;
    }
    .like_button {
        background-color: #60e085;
        color: #fff;
        padding: 5px 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    .likes_count {
        margin-left: 5px;
        color: #333;
        background-color: #ffffff;
        padding: 5px 10px;
        border-radius: 5px;
        font-size: 20px;
    }
</style>
