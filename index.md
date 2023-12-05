---
layout: none
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
    <div class="numbers" id="numbers">
    <span>8</span>
    <span>3</span>
    <span>4</span>
    <span>5</span>
    <span>2</span>
    <span>1</span>
    <span>7</span>
    <span>9</span>
    <span>3</span>
    <span>6</span>
    <span>0</span>
  </div>
     <script>
    // Sorting animation function using bubble sort
    async function bubbleSort() {
      const numbersDiv = document.getElementById('numbers');
      const numbers = numbersDiv.children;
      for (let i = 0; i < numbers.length - 1; i++) {
        for (let j = 0; j < numbers.length - i - 1; j++) {
          // Highlight elements being compared
          numbers[j].style.backgroundColor = 'red';
          numbers[j + 1].style.backgroundColor = 'red';
          await sleep(1000); // Delay for visualization
          // Convert span elements to numbers for comparison
          const num1 = parseInt(numbers[j].innerText);
          const num2 = parseInt(numbers[j + 1].innerText);
          if (num1 > num2) {
            // Swap elements if needed
            const temp = numbers[j].innerText;
            numbers[j].innerText = numbers[j + 1].innerText;
            numbers[j + 1].innerText = temp;
          }
          // Remove background color after comparison
          numbers[j].style.backgroundColor = '';
          numbers[j + 1].style.backgroundColor = '';
        }
      }
    }
    // Function to create delay
    function sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    }
    // Run the sorting animation when the page loads
    window.onload = () => {
      bubbleSort();
    };
  </script>
</body>

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
    .numbers {
      display: flex;
      justify-content: center;
      margin-top: 50px;
       font-family: "Times New Roman", sans-serif;
        color: #388087; 
        font-size: 50px;
        background-color: #F6F6F2;
        margin-top: 10px;
        animation-duration: 1s;
      animation-fill-mode: forwards;
    }
    @keyframes moveUp {
      from { transform: translateY(0); }
      to { transform: translateY(-100px); }
    }
    @keyframes moveDown {
      from { transform: translateY(0); }
      to { transform: translateY(100px); }
    }
</style>
