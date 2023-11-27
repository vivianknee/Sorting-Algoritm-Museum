<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Art Gallery</title>
    <link rel="stylesheet" href="styles.css">
    <script src="gallery.js" defer></script>
</head>
<body>
    <header>
        <h1>Welcome to the Art Gallery</h1>
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