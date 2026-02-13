<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Be My Valentine</title>

<style>
body {
  margin: 0;
  font-family: 'Poppins', Arial, sans-serif;
  background: linear-gradient(-45deg, #ff5fa2, #ff8dc7, #ffb3d9, #ff4da6);
  background-size: 400% 400%;
  animation: gradient 8s ease infinite;
  height: 100vh;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

@keyframes gradient {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

/* Floating hearts */
.heart {
  position: fixed;
  bottom: -30px;
  font-size: 24px;
  animation: floatUp linear infinite, spin 4s linear infinite;
  opacity: 0.9;
}

@keyframes floatUp {
  from { transform: translateY(0); }
  to { transform: translateY(-120vh); }
}

@keyframes spin {
  from { rotate: 0deg; }
  to { rotate: 360deg; }
}

/* Main center */
.center {
  text-align: center;
  color: white;
  z-index: 5;
}

h1 {
  font-size: 32px;
  margin-bottom: 20px;
  text-shadow: 0 0 15px rgba(255,255,255,0.8);
}

.buttons {
  position: relative;
}

button {
  font-size: 20px;
  padding: 14px 32px;
  margin: 12px;
  border: none;
  border-radius: 30px;
  cursor: pointer;
  transition: 0.2s;
}

#yesBtn {
  background: linear-gradient(135deg, #ff2f92, #ff6fb1);
  color: white;
  box-shadow: 0 0 20px rgba(255,0,150,0.8);
}

#noBtn {
  background: linear-gradient(135deg, #777, #444);
  color: white;
  position: absolute;
}

button:hover {
  transform: scale(1.1);
}

/* Explosion */
.boom {
  position: fixed;
  font-size: 30px;
  animation: explode 1s forwards;
  pointer-events: none;
}

@keyframes explode {
  from { transform: scale(1); opacity: 1; }
  to { transform: scale(2) translate(var(--x), var(--y)); opacity: 0; }
}
</style>
</head>

<body>

<audio id="bgMusic" loop>
  <source src="https://www.dropbox.com/scl/fi/0knhtf1x5opqzgj6v6b6b/cupid.mp3?raw=1" type="audio/mpeg">
</audio>

<div class="center">
  <h1 id="text">Will you be my Valentine? 💖</h1>

  <div class="buttons" id="buttons">
    <button id="yesBtn" onclick="yesClick()">Yes 💘</button>
    <button id="noBtn" onmouseover="moveNo()">No 💔</button>
  </div>
</div>

<script>
const music = document.getElementById("bgMusic");

function yesClick() {
  music.play(); // iPhone allows music after user tap
  document.getElementById("text").innerHTML =
    "You just unlocked unlimited love 💖✨";
  document.getElementById("buttons").innerHTML = "";
  heartExplosion();
}

function moveNo() {
  music.play(); // start music on interaction
  const btn = document.getElementById("noBtn");
  const x = Math.random() * 260 - 130;
  const y = Math.random() * 180 - 90;
  btn.style.transform = `translate(${x}px, ${y}px)`;
}

/* Floating hearts */
function createHeart() {
  const hearts = ["💖","💕","💗","💘","💝","💞","💓","❤️","🩷"];
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.innerHTML = hearts[Math.floor(Math.random()*hearts.length)];
  heart.style.left = Math.random()*100 + "vw";
  heart.style.animationDuration = (3 + Math.random()*4) + "s";
  document.body.appendChild(heart);
  setTimeout(() => heart.remove(), 7000);
}
setInterval(createHeart, 200);

/* Heart explosion */
function heartExplosion() {
  const hearts = ["💖","💕","💗","💘","💝","💞","💓","❤️","🩷"];
  for (let i = 0; i < 60; i++) {
    const boom = document.createElement("div");
    boom.className = "boom";
    boom.innerHTML = hearts[Math.floor(Math.random()*hearts.length)];
    boom.style.left = "50%";
    boom.style.top = "50%";
    boom.style.setProperty("--x", (Math.random()*700 - 350) + "px");
    boom.style.setProperty("--y", (Math.random()*700 - 350) + "px");
    document.body.appendChild(boom);
    setTimeout(() => boom.remove(), 1000);
  }
}
</script>

</body>
</html>
