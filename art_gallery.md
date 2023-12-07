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
        <h1>Art Gallery</h1>
    </header>
    <div class="select">
        <form class="sort_typesbg">
            <label class="sort_types" for="sorts">Sort Types</label>
            <select name="sorts" id="sorts">  
                <option value="blank"></option>
                <option value="merge">Merge</option>
                <option value="selection">Selection</option>
                <option value="insertion">Insertion</option>
                <option value="bubble">Bubble</option>
            </select>
        </form>
        <button class="sort_button" id="sort_button">Sort</button>
    </div>
    <div>
        <p class="sort_time" id="sort_time">Sort Time: </p>
    </div>
    <main class = "grid" id="art_root">
    </main>
</body>

</html>
<script>
    //get request to display art
    function getArtWorks() {
        fetch('https://avk.stu.nighthawkcodingsociety.com/api/art/')
            .then(response => response.json())
            .then(data => {
                formatArt(data);  
            })
            .catch(err => {
                console.log(err);
            });
    }
    //format display and population of data
    function formatArt(arts) {
        // find the root div
        //outer most div
         const root_div = document.getElementById("art_root");
         //clear each time
         root_div.innerHTML = "";
         arts.forEach(art =>{
            //individual artwork div
            const art_section = document.createElement("section");
            art_section.className = "art_piece";
            //art_section.id = art.id;
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
            const like_button = document.createElement('button');
            like_button.className = "like_button"
            like_button.innerHTML = "Like";
            const span = document.createElement('span');
            span.id = art.id;
            span.innerHTML = art.like;
            span.className = "likes_count"
            //update likes function
            like_button.addEventListener("click", function(){
                fetch(`https://avk.stu.nighthawkcodingsociety.com/api/art/like/${art.id}`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                })
                .then((response) => response.json())
                .then((newArt) => { 
                    const update_span = document.getElementById(art.id);
                    update_span.innerHTML = newArt.like;
                    //console.log(newArt);
                });
            });
            //append
            like_div.appendChild(like_button);
            like_div.appendChild(span);
            art_section.appendChild(art_label);
            art_section.appendChild(img_div);
            art_section.appendChild(like_div);
            root_div.appendChild(art_section);
    });
    }
    //perform sort
    function setupSort() {
        var sort_button = document.getElementById("sort_button");
        console.log(sort_button);
        sort_button.addEventListener("click", function(){
                    var sortingMethod = document.getElementById('sorts').value
                    fetch(`https://avk.stu.nighthawkcodingsociety.com/api/art/sorted/${sortingMethod}`, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json',
                        },
                    })
                    .then((response) => response.json())
                    .then((sortResult) => { 
                        console.log(sortResult);
                        formatArt(sortResult.sortedArts); 
                        const sort_time = document.getElementById("sort_time");
                        sort_time.innerHTML = "Sort Time: " + sortResult.sortTime + " ns";
                    });
                });
    }
    setupSort();
    getArtWorks();
</script>

<style>
    body {
        font-family: 'Arial', sans-serif;
        margin: 0;
        padding: 0;
        background-color: #F6F6F2;
        color: #333;
        place-items: center;
    }
    header {
        background-color: #F6F6F2;
        color: #F6F6F2;
        padding: 10px;
        text-align: center;
    }
    .grid{ 
        background-color: #F6F6F2;
        padding: 20px;
        position: absolute;
        top: 25%;
        left: 12%;
        width: 87%;
        display: grid;
        overflow: hidden;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        grid-gap: 15px;
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
    .like_button, .sort_button {
        background-color: #60e085;
        color: #fff;
        padding: 5px 10px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        margin-top: 10px;
    }
    .likes_count {
        margin-left: 5px;
        color: #333;
        background-color: #ffffff;
        padding: 5px 10px;
        border-radius: 5px;
        font-size: 20px;
    }
    .sort_types{
        color: #2f5154;
        background-color: #F6F6F2;
        font-family: Optima, sans-serif;
        margin-bottom: 10px;
    }
    .sort_time{
        color: #2f5154;
        background-color: #F6F6F2;
        font-family: Optima, sans-serif;
        margin-left: 20px;
    }
    .select {
        justify-content: center;
        align-items: left;
        margin-bottom: 20px;
        margin-left: 20px;
        background-color: #F6F6F2;
    }
    .sort_typesbg {
        background-color: #F6F6F2;
    }
</style>
