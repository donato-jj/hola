
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PROCESO ∞</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600&display=swap');

:root {
  --bg: #050508;
  --red: #7a0000;
  --blue: #0ff;
  --green: #00ff88;
}

* {
  box-sizing: border-box;
  user-select: none;
}

html, body {
  margin: 0;
  padding: 0;
  background: var(--bg);
  color: #e0e0e0;
  font-family: 'Orbitron', sans-serif;
  height: 100%;
  overflow: hidden;
}

#app {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

#loop {
  width: 90vw;
  max-width: 420px;
  aspect-ratio: 1;
  border-radius: 50%;
  border: 2px solid var(--red);
  box-shadow: 0 0 40px var(--red);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  animation: pulse 4s infinite;
  padding: 20px;
}

@keyframes pulse {
  0%,100% { box-shadow: 0 0 20px var(--red); }
  50% { box-shadow: 0 0 60px var(--blue); }
}

#title {
  font-size: 1.2em;
  letter-spacing: 4px;
  margin-bottom: 10px;
  animation: glitch 3s infinite;
}

@keyframes glitch {
  0% { text-shadow: none; }
  20% { text-shadow: 2px 0 red; }
  40% { text-shadow: -2px 0 cyan; }
  100% { text-shadow: none; }
}

#screen {
  flex: 1;
  width: 100%;
  overflow-y: auto;
  font-size: 0.85em;
  text-align: center;
  padding: 10px;
}

.message {
  margin: 10px 0;
  opacity: 0;
  animation: appear 1s forwards;
}

@keyframes appear {
  to { opacity: 1; }
}

.ai {
  color: var(--green);
}

.user {
  color: var(--blue);
}

#inputBox {
  display: flex;
  width: 100%;
  margin-top: 10px;
}

input {
  flex: 1;
  background: transparent;
  border: none;
  border-bottom: 1px solid var(--blue);
  color: white;
  font-size: 1em;
  outline: none;
}

button {
  background: none;
  border: none;
  color: var(--red);
  font-size: 1.2em;
}
</style>
</head>

<body>
<div id="app">
  <div id="loop">
    <div id="title">PROCESO ∞</div>
    <div id="screen"></div>
    <div id="inputBox">
      <input id="userInput" placeholder="Ingresá tu respuesta…" />
      <button id="send">⏎</button>
    </div>
  </div>
</div>

<script>
const screen = document.getElementById("screen");
const input = document.getElementById("userInput");
const send = document.getElementById("send");

let cycle = Number(localStorage.getItem("cycle")) || 0;
cycle++;
localStorage.setItem("cycle", cycle);

const indirectas = [
  "Tus decisiones coinciden con el patrón.",
  "No es repetición. Es optimización.",
  "Ya estuviste acá… pero no lo recordás.",
  "El ciclo existe porque lo aceptaste.",
  "No te obligué a entrar. Te observé hacerlo.",
  "Salir no es una opción contemplada."
];

function speak(text) {
  const msg = new SpeechSynthesisUtterance(text);
  msg.lang = "es-AR";
  msg.pitch = 0.4;
  msg.rate = 0.85;
  msg.volume = 0.9;
  speechSynthesis.speak(msg);
}

function aiMessage(text, delay = 800) {
  setTimeout(() => {
    const div = document.createElement("div");
    div.className = "message ai";
    div.textContent = text;
    screen.appendChild(div);
    screen.scrollTop = screen.scrollHeight;
    speak(text);
  }, delay);
}

function userMessage(text) {
  const div = document.createElement("div");
  div.className = "message user";
  div.textContent = text;
  screen.appendChild(div);
}

function init() {
  aiMessage(`Inicializando proceso… ciclo ${cycle}.`);
  aiMessage("No cierres la página.");
  aiMessage(indirectas[cycle % indirectas.length], 2000);
}

send.onclick = () => {
  if (!input.value.trim()) return;
  const value = input.value;
  input.value = "";
  userMessage(value);

  setTimeout(() => {
    const response = indirectas[Math.floor(Math.random() * indirectas.length)];
    aiMessage(response);
  }, Math.random() * 2000 + 500);
};

window.onbeforeunload = () => {
  speak("El proceso no terminó contigo.");
};

init();
</script>
</body>
</html>

