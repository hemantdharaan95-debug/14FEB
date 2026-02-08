# 14FEB
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>For Minika 💖</title>

<!-- Italian Romantic Font -->
<link href="https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap" rel="stylesheet">

<style>
body {
  margin: 0;
  height: 100vh;
  background: linear-gradient(135deg, #ff758c, #ff7eb3);
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: Arial, sans-serif;
  color: white;
  text-align: center;
}

/* ================= CARD ================= */
.card {
  background: rgba(255,255,255,0.15);
  padding: 40px;
  border-radius: 20px;
  width: 340px;
}

/* ================= INPUT & BUTTON ================= */
input {
  padding: 10px;
  border-radius: 20px;
  border: none;
  width: 80%;
  margin-top: 15px;
  text-align: center;
}

button {
  margin-top: 15px;
  padding: 12px 25px;
  border-radius: 25px;
  border: none;
  font-size: 18px;
  cursor: pointer;
  transition: all 0.3s ease;
}

#yes {
  background: #ff4d6d;
  color: white;
}

#no {
  background: white;
  color: #ff4d6d;
}

#message {
  margin-top: 10px;
  font-size: 14px;
}

/* ================= ENVELOPE ================= */
.envelope {
  position: relative;
  width: 340px;
  height: 220px;
  background: #f5f5f5;
  border-radius: 12px;
  box-shadow: 0 15px 35px rgba(0,0,0,0.35);
  overflow: hidden;
}

/* Envelope flap */
.flap {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #ff4d6d;
  clip-path: polygon(0 0, 50% 65%, 100% 0, 100% 100%, 0 100%);
  transform-origin: top;
  transition: transform 1s ease;
  z-index: 3;
}

/* Open state */
.envelope.open .flap {
  transform: rotateX(180deg);
}

/* ================= LETTER ================= */
.letter {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 100%;
  background: white;
  padding: 30px;
  box-sizing: border-box;
  transform: translateY(100%);
  transition: transform 1.2s ease;
  font-family: 'Great Vibes', cursive;
  color: #ff4d6d;
  font-size: 26px;
  line-height: 1.4;
  z-index: 1;
}

.envelope.open .letter {
  transform: translateY(0);
}

/* ================= WAX SEAL ================= */
.wax-seal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 70px;
  height: 70px;
  background: radial-gradient(circle at 30% 30%, #ff8fa3, #c9184a);
  border-radius: 50%;
  box-shadow: inset -5px -5px 10px rgba(0,0,0,0.25),
              inset 5px 5px 10px rgba(255,255,255,0.3);
  cursor: pointer;
  z-index: 5;
  transition: transform 0.4s ease, opacity 0.4s ease;
}

.wax-seal::after {
  content: "❤";
  color: #fff;
  font-size: 26px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

/* Break animation */
.wax-seal.break {
  transform: translate(-50%, -50%) scale(1.6);
  opacity: 0;
}
</style>
</head>

<body>

<div class="card" id="game">
  <h2 id="title">Riddle 1 💌</h2>
  <p id="riddle">
    I’m not a place, yet we’ve been there,<br>
    I live in photos and late-night stares.<br>
    Where do our memories sleep?
  </p>

  <input type="text" id="answer" placeholder="Type your answer..." />
  <br>
  <button onclick="checkAnswer()">Submit</button>
  <p id="message"></p>
</div>

<script>
let step = 1;
let yesSize = 1;
let noSize = 1;

const noMessages = [
  "Nice try Minika 😜",
  "Are you sure? 😏",
  "Destiny says NO to NO 💖",
  "Come on Minika 😍",
  "Only one right answer ❤️"
];

function checkAnswer() {
  const ans = document.getElementById("answer").value.toLowerCase().trim();
  const msg = document.getElementById("message");

  if (step === 1 && (ans === "gallery" || ans === "photos")) {
    step = 2;
    nextRiddle("Riddle 2 💖",
      "I beat without a sound,<br>I race when you’re around.<br>What am I?"
    );
  } 
  else if (step === 2 && ans === "heart") {
    showValentine();
  } 
  else {
    msg.innerText = "Hmm… think again Minika 😉";
  }
}

function nextRiddle(title, text) {
  document.getElementById("title").innerHTML = title;
  document.getElementById("riddle").innerHTML = text;
  document.getElementById("answer").value = "";
  document.getElementById("message").innerText = "";
}

function showValentine() {
  document.getElementById("game").innerHTML = `
    <h1>Minika Manhas ❤️</h1>
    <h2>Will you be my Valentine?</h2>
    <button id="yes" onclick="yesClicked()">YES 💖</button>
    <button id="no" onclick="noClicked()">NO 😜</button>
    <p id="message"></p>
  `;
}

function noClicked() {
  const yes = document.getElementById("yes");
  const no = document.getElementById("no");
  const msg = document.getElementById("message");

  yesSize += 0.35;
  noSize -= 0.25;

  yes.style.transform = `scale(${yesSize})`;
  no.style.transform = `scale(${noSize})`;
  no.style.opacity = noSize;

  msg.innerText = noMessages[Math.floor(Math.random() * noMessages.length)];

  if (noSize <= 0.3) {
    no.style.display = "none";
    yes.innerHTML = "ONLY YES 💖";
    msg.innerText = "Okay okay… destiny has spoken 😌❤️";
  }
}

function yesClicked() {
  document.body.innerHTML = `
    <div class="envelope" id="envelope">
      <div class="flap"></div>
      <div class="wax-seal" onclick="openEnvelope(this)"></div>
      <div class="letter">
        Cara Minika ❤️<br><br>
        Sei il mio sorriso,<br>
        il mio battito,<br>
        il mio per sempre 💕<br><br>
        Vuoi essere<br>
        la mia Valentine? 🌹<br><br>
        — Con amore 💌
      </div>
    </div>
  `;
}

function openEnvelope(seal) {
  const envelope = document.getElementById("envelope");
  seal.classList.add("break");
  setTimeout(() => {
    seal.remove();
    envelope.classList.add("open");
  }, 400);
}
</script>

</body>
</html>
