---
layout: none
---

{%- include avk_head.html -%}

<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fibonacci Art Gallery</title>
    <link rel="stylesheet" href="styles.css">
    <script src="sort.js" defer></script>
</head>

<body>
    <header>
        <h1>Welcome to the AVK Art Gallery</h1>
        <nav>
            <ul>
                <li><a href="#randomize">Randomize</a></li>
                <li><a href="#sorted-by-likes">Sorted by Likes</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <section id="original">
            <h2>Randomized Fibonacci Art</h2>
            <div class="art-gallery">
                <!-- Art pieces generated through Java backend -->
                <!-- Display original art here -->
            </div>
        </section>
        <section id="sorted-by-likes">
            <h2>Sorted by Likes</h2>
            <div class="art-gallery" id="likesGallery">
                <!-- Art pieces sorted by likes -->
                <!-- Display sorted art here -->
            </div>
        </section>
    </main>
    <footer>
        <p>&copy; 2023 Fibonacci Art Gallery</p>
    </footer>
</body>

</html>