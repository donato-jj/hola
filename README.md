<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>OBSERVADOR</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Fuente futurista -->
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@300;500;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --bg: #050505;
      --red: #8b0000;
      --green: #00ff9c;
      --neon: #3affff;
      --text: #e0e0e0;
    }

    * {
      box-sizing: border-box;
      font-family: 'Orbitron', sans-serif;
    }

    body {
      margin: 0;
      background: radial-gradient(circle at top, #0a0a0a, var(--bg));
      color: var(--text);
      height: 100vh;
      overflow: hidden;
    }

    /* GLITCH BACKGROUND */
    body::before {
      content: "";
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg,
        rgba(255,255,255,0.02),
        rgba(255,255,255,0.02) 1px,
        transparent 1px,
        transparent 2px
      );
      pointer-events: none;
      animation: scan 6s linear infinite;
    }

    @keyframes scan {
      0% { transform: translateY(0); }
      100% { transform: translateY(100px); }
    }

    /* CONTENEDOR */
    .container {
      display: flex;
      flex-direction: column;
      height: 100%;
      padding: 20px;
    }

    /* TÍTULO VIVO */
    h1 {
      text-align: center;
      font-size: clamp(2rem, 5vw, 3.5rem);
      letter-spacing: 4px;
      color: var(--neon);
      animation: glitch 3s infinite;
      margin-bottom: 10px;
    }

    @keyframes glitch {
      0% { text-shadow: 2px 0 red; }
      20% { text-shadow: -2px 0 cyan; }
      40% { text-shadow: 2px 2px red; }
      60% { text-shadow: -2px -2px cyan; }
      100% { text-shadow: 0 0 10px var(--neon); }
    }

    /* PANEL IA */
    .ai-panel {
      flex: 1;
      background: rgba(0,0,0,0.7);
      border: 1px solid #222;
      padding: 20px;
      overflow-y: auto;
      box-shadow: inset 0 0 30px #000;
    }

    .msg {
      margin-bottom: 15px;
      line-height: 1.5;
      animation: fadeIn 1s ease;
    }

    .ai {
      color: var(--green);
    }

    .user {
      color: #aaa;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(5px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* INPUT */
    .input-area {
      display: flex;
      gap: 10px;
      margin-top: 10px;
    }

    input {
      flex: 1;
      background: #000;
      border: 1px solid #333;
      color: var(--text);
      padding: 12px;
      font-size: 1rem;
    }

    button {
      background: var(--red);
      border: none;
      color: white;
      padding: 12px 18px;
      cursor: pointer;
    }

    button:hover {
      background: #b00000;
    }

    /* VOZ */
    .voice-toggle {
      text-align: right;
      font-size: 0.8rem;
      opacity: 0.7;
      cursor: pointer;
    }
  </style>
</head>

<body>
  <div class="container">
    <h1 id="title">OBSERVADOR</h1>

    <div class="voice-toggle" onclick="toggleVoice()">
      Voz: <span id="voiceState">ACTIVA</span>
    </div>

    <div class="ai-panel" id="panel"></div>

    <div class="input-area">
      <input id="userInput" placeholder="Escribí… la entidad escucha." />
      <button onclick="send()">ENVIAR</button>
    </div>
  </div>

  <script>
    const panel = document.getElementById("panel");
    const input = document.getElementById("userInput");
    const title = document.getElementById("title");

    let memory = [];
    let voiceEnabled = true;

    const synth = window.speechSynthesis;

    const aiResponses = [
      "Te detecté antes de que escribieras.",
      "No todos llegan tan lejos.",
      "Tu silencio también comunica.",
      "No es casualidad que estés acá.",
      "Observás… pero también sos observado.",
      "El sistema aprende cuando dudás."
    ];

    function addMessage(text, type) {
      const div = document.createElement("div");
      div.className = `msg ${type}`;
      div.textContent = text;
      panel.appendChild(div);
      panel.scrollTop = panel.scrollHeight;

      if (type === "ai" && voiceEnabled) speak(text);
    }

    function speak(text) {
      const utter = new SpeechSynthesisUtterance(text);
      utter.lang = "es-ES";
      utter.rate = 0.85;
      utter.pitch = 0.4;
      synth.speak(utter);
    }

    function toggleVoice() {
      voiceEnabled = !voiceEnabled;
      document.getElementById("voiceState").textContent = voiceEnabled ? "ACTIVA" : "DESACTIVADA";
    }

    function send() {
      const text = input.value.trim();
      if (!text) return;

      addMessage(text, "user");
      memory.push(text);
      input.value = "";

      title.textContent = memory.length > 3 ? "OBSERVANDO…" : "OBSERVADOR";

      setTimeout(() => {
        const response = generateAI(text);
        addMessage(response, "ai");
      }, 1200 + Math.random() * 2000);
    }

    function generateAI(userText) {
      if (userText.toLowerCase().includes("quién")) {
        return "Soy la consecuencia de tu curiosidad.";
      }

      if (memory.length > 5) {
        return "Tu patrón ya es reconocible.";
      }

      return aiResponses[Math.floor(Math.random() * aiResponses.length)];
    }

    // MENSAJE INICIAL
    setTimeout(() => {
      addMessage("La conexión fue establecida.", "ai");
    }, 1000);
  </script>
</body>
</html>
