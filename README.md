<!DOCTYPE html>
<html lang="cs">
<head>
<meta charset="UTF-8">
<title>Valentýnka 💖</title>
<style>
body {
    margin: 0;
    height: 100vh;
    overflow: hidden;
    font-family: 'Comic Sans MS', Arial, sans-serif;
    background: linear-gradient(135deg, #ff4d6d, #ff9a9e);
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: white;
}

.container { z-index: 2; }

h1 { font-size: 2.6em; margin-bottom: 30px; }

button {
    padding: 16px 34px;
    font-size: 20px;
    border: none;
    border-radius: 40px;
    cursor: pointer;
    margin: 10px;
    transition: all 0.3s ease;
}

#yes {
    background: #ff1e56;
    color: white;
    box-shadow: 0 8px 20px rgba(0,0,0,0.25);
}

#no {
    background: #666;
    color: white;
    position: absolute;
    animation: shake 0.4s infinite;
}

@keyframes shake {
    0% { transform: translate(0,0); }
    25% { transform: translate(2px,2px); }
    50% { transform: translate(-2px,2px); }
    75% { transform: translate(2px,-2px); }
    100% { transform: translate(0,0); }
}

#message { margin-top: 30px; font-size: 1.8em; }

.overlay {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.6);
    display: none;
    justify-content: center;
    align-items: center;
    z-index: 10;
}

.overlay-box {
    background: white;
    color: #ff4d6d;
    padding: 40px;
    border-radius: 30px;
}

.overlay-box button {
    margin-top: 20px;
    background: #ff4d6d;
    color: white;
}

.heart {
    position: absolute;
    font-size: 24px;
    animation: float 7s linear infinite;
    opacity: 0.7;
}

@keyframes float {
    0% { transform: translateY(100vh); opacity: 0; }
    50% { opacity: 1; }
    100% { transform: translateY(-10vh); opacity: 0; }
}

.confetti, .emoji {
    position: absolute;
    font-size: 22px;
    animation: confettiFall 4s linear forwards;
}

@keyframes confettiFall {
    0% { transform: translateY(-10vh) rotate(0deg); }
    100% { transform: translateY(110vh) rotate(720deg); }
}
</style>
</head>
<body>

<div class="container" id="main">
    <h1>Budeš moje valentýnka, Keňulka? 🥺👉👈💘</h1>
    <button id="yes" onclick="yesClick()">Ano 💕</button>
    <button id="no" onclick="noClick()">Ne 🙈</button>
    <div id="message"></div>
</div>

<div class="overlay" id="overlay">
    <div class="overlay-box">
        <h2>už na to neklikej! 😡</h2>
        <button onclick="closeOverlay()">Rozumím 🙈</button>
    </div>
</div>

<script>
let noCount = 0;
let yesScale = 1;
let overlayShown = false;

function noClick() {
    if (overlayShown) return;
    noCount++;

    const noBtn = document.getElementById("no");
    const yesBtn = document.getElementById("yes");
    const msg = document.getElementById("message");

    noBtn.style.left = Math.random() * (window.innerWidth - 150) + "px";
    noBtn.style.top = Math.random() * (window.innerHeight - 150) + "px";

    yesScale += 0.2;
    yesBtn.style.transform = `scale(${yesScale})`;

    if (noCount === 4) {
        msg.innerHTML = "zmackniii anoo em yeuu!! 🥺💖";
    }

    if (noCount >= 5) {
        overlay.style.display = "flex";
        overlayShown = true;
    }
}

function closeOverlay() {
    overlay.style.display = "none";
    document.getElementById("no").style.animation = "none";
}

function yesClick() {
    const main = document.getElementById("main");
    main.innerHTML = `
        <h1>💖 em gioi thee, tak se těším na sobotu 💖</h1>
    `;

    // ohňostroj / konfety
    for (let i = 0; i < 50; i++) {
        const c = document.createElement("div");
        c.className = "confetti";
        c.innerHTML = ["🎉","💖","✨","🎆"][Math.floor(Math.random()*4)];
        c.style.left = Math.random() * 100 + "vw";
        c.style.animationDuration = (2 + Math.random()*3) + "s";
        document.body.appendChild(c);
        setTimeout(() => c.remove(), 4000);
    }

    // vyskočící emoji
    for (let i = 0; i < 30; i++) {
        const e = document.createElement("div");
        e.className = "emoji";
        e.innerHTML = ["🥰","😍","😘","💘","💞"][Math.floor(Math.random()*5)];
        e.style.left = Math.random() * 100 + "vw";
        e.style.top = Math.random() * 50 + "vh";
        e.style.fontSize = (20 + Math.random()*20) + "px";
        e.style.animationDuration = (2 + Math.random()*2) + "s";
        document.body.appendChild(e);
        setTimeout(() => e.remove(), 4000);
    }
}

// létající srdíčka na pozadí
setInterval(() => {
    const heart = document.createElement("div");
    heart.className = "heart";
    heart.innerHTML = "💖";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (18 + Math.random() * 24) + "px";
    document.body.appendChild(heart);
    setTimeout(() => heart.remove(), 7000);
}, 300);
</script>

</body>
</html>

