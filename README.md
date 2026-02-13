<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Valentine Fun 💖</title>

<style>
* { box-sizing: border-box; }
body {
    margin: 0;
    font-family: 'Segoe UI', sans-serif;
    background: linear-gradient(135deg, #ffdde1, #fad0c4, #fcb7c2, #ff9a9e);
    background-size: 400% 400%;
    animation: bg 12s ease infinite;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    flex-direction: column;
}

@keyframes bg {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

h1 {
    color: white;
    font-size: clamp(22px, 5vw, 38px);
    margin-bottom: 10px;
    text-shadow: 0 0 10px #ff85a2;
}

#board {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(110px, 1fr));
    gap: 15px;
    width: 90%;
    max-width: 480px;
    margin-top: 20px;
}

.card {
    background: white;
    color: #ff3366;
    border-radius: 20px;
    aspect-ratio: 1/1;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: clamp(14px, 3.5vw, 18px);
    font-weight: bold;
    cursor: pointer;
    padding: 12px;
    text-align: center;
    transition: 0.4s ease;
    box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    position: relative;
    overflow: hidden;
}

.card::after {
    content: '';
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0; left: 0;
    border-radius: 20px;
    background: radial-gradient(circle, rgba(255,255,255,0.4) 0%, transparent 70%);
    transform: scale(0);
    transition: transform 0.5s;
}

.card:hover::after { transform: scale(1); }

.card.revealed {
    background: #ffe6f0;
    transform: scale(1.08);
}

#navButtons {
    margin-top: 20px;
}

button {
    background: #ff85a2;
    border: none;
    padding: 10px 18px;
    margin: 5px;
    font-size: 16px;
    color: white;
    border-radius: 12px;
    cursor: pointer;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
    transition: 0.3s;
}

button:hover {
    transform: scale(1.05);
    background: #ff4d6d;
}

/* Page 2 Styles */
#page2 {
    display: none;
    position: relative;
    width: 100%;
    height: 80vh;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}

#heart {
    position: relative;
    width: 250px;
    height: 250px;
}

#heart::before,
#heart::after {
    content: "";
    position: absolute;
    width: 250px;
    height: 250px;
    background: red;
    border-radius: 50%;
}

#heart::before { top: -125px; left: 0; }
#heart::after { left: 125px; top: 0; }

#heartText {
    position: absolute;
    color: white;
    font-size: clamp(24px,5vw,32px);
    font-weight: bold;
    text-align: center;
    width: 100%;
    top: 50%;
    transform: translateY(-50%);
}

/* Floating hearts */
.floatingHeart {
    position: absolute;
    font-size: 20px;
    animation: floatUp linear infinite;
    opacity: 0.8;
}

@keyframes floatUp {
    0% { transform: translateY(100vh) scale(0.5); opacity: 0; }
    50% { opacity: 1; }
    100% { transform: translateY(-10vh) scale(1.2); opacity: 0; }
}
</style>
</head>

<body>

<!-- Page 1 -->
<div id="page1">
    <h1 id="pageTitle">💖 Love Missions 💕</h1>
    <div id="board"></div>
</div>

<!-- Page 2 -->
<div id="page2">
    <div id="heart"></div>
    <div id="heartText">I LOVE YOU 💖</div>
</div>

<!-- Navigation -->
<div id="navButtons">
    <button onclick="goToPage(1)">Page 1</button>
    <button onclick="goToPage(2)">Page 2</button>
</div>

<script>
// Disable right-click
document.addEventListener("contextmenu", e => e.preventDefault());

// Page 1 Missions
const loveMissions = [
    "💋 Give a sweet kiss",
    "🤗 Big warm hug",
    "🌹 Surprise with a rose",
    "💌 Say 'I love you'",
    "💃 Slow dance together",
    "🍫 Share chocolate",
    "🌙 Stargaze together",
    "🎵 Sing a love song",
    "💍 Promise forever"
];

const board = document.getElementById("board");
const page1 = document.getElementById("page1");
const page2 = document.getElementById("page2");
const heartContainer = document.getElementById("heart");

// Page management
function loadPage1() {
    page1.style.display = "block";
    page2.style.display = "none";
    board.innerHTML = "";
    const shuffled = loveMissions.sort(() => Math.random() - 0.5);
    shuffled.forEach(text => {
        const card = document.createElement("div");
        card.classList.add("card");
        card.innerHTML = "💖";
        card.addEventListener("click", () => {
            if(!card.classList.contains("revealed")){
                card.innerHTML = text;
                card.classList.add("revealed");
            }
        });
        board.appendChild(card);
    });
}

function createFloatingHearts() {
    for(let i=0;i<15;i++){
        const h = document.createElement("div");
        h.classList.add("floatingHeart");
        h.innerHTML = "💖";
        h.style.left = Math.random()*100 + "vw";
        h.style.animationDuration = (3+Math.random()*5)+"s";
        h.style.fontSize = (15+Math.random()*15)+"px";
        document.body.appendChild(h);
        setTimeout(()=> h.remove(), 8000);
    }
}

function goToPage(num){
    if(num===1){
        loadPage1();
    } else {
        page1.style.display = "none";
        page2.style.display = "flex";
        createFloatingHearts();
    }
}

// Load initial page
loadPage1();
</script>

</body>
</html>
