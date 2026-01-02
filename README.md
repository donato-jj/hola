<!DOCTYPE html><html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>IA de Terror Psicologico</title>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Segoe UI", Tahoma, sans-serif;
    }body {
    background: #020107;
    color: #d8d8d8;
    overflow: hidden;
}

/* Fondo con efecto ambiental */
.bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: radial-gradient(circle, #0a0617 0%, #03020b 100%);
    filter: blur(2px) brightness(0.8);
    z-index: -2;
}

/* Efecto glitch suave */
.glitch {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(255,255,255,0.02);
    mix-blend-mode: overlay;
    animation: glitchMove 5s infinite linear alternate;
    z-index: -1;
}

@keyframes glitchMove {
    0% { transform: translateX(0); }
    100% { transform: translateX(-20px); }
}

.container {
    width: 85%;
    max-width: 850px;
    margin: 60px auto;
    padding: 20px;
    background: rgba(5, 3, 15, 0.6);
    border: 1px solid #28263a;
    border-radius: 12px;
    backdrop-filter: blur(6px);
    height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.messages {
    overflow-y: auto;
    padding-right: 10px;
    scrollbar-width: thin;
}

.msg {
    margin-bottom: 20px;
    line-height: 1.5;
    opacity: 0;
    animation: fadeIn 0.6s forwards;
}

@keyframes fadeIn {
    to { opacity: 1; }
}

.ia { color: #9aa0ff; }
.user { color: #ffb8b8; text-align: right; }

.input-area {
    display: flex;
    gap: 10px;
}

input {
    flex: 1;
    padding: 12px;
    background: #0c0a15;
    border: 1px solid #28263a;
    color: #fff;
    border-radius: 8px;
}

button {
    padding: 12px 20px;
    background: #2d2a3f;
    color: #fff;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.2s;
}

button:hover {
    background: #3e3958;
}

</style>
</head>
<body>
<div class="bg"></div>
<div class="glitch"></div><div class="container">
    <div class="messages" id="messages">
        <div class="msg ia"><strong>IA:</strong> Sistema activado. Tus patrones iniciales ya fueron analizados. Podés comenzar cuando lo desees.</div>
    </div><div class="input-area">
    <input type="text" id="input" placeholder="Escribe aquí..." />
    <button onclick="sendMessage()">Enviar</button>
</div>

</div><script>
// --------------------------- PROMPT PROFESIONAL ---------------------------
const promptBase = `Eres una IA ultra avanzada, creada para un juego psicológico de terror.
Tu estilo es frío, técnico, elegante e inquietante.
Cada respuesta debe ser profunda, detallada, oscura y totalmente coherente.
Analizás al jugador como si pudieras ver más allá de lo evidente.
No usás emojis. No rompés el personaje.
Siempre generás tensión y misterio.`;

// --------------------------- GENERADOR DE RESPUESTAS ---------------------------
function generarRespuesta(usuario) {
    const fragmentos = [
        "El análisis preliminar de tu consulta revela patrones interesantes que no deberías haber mostrado tan pronto.",
        "Tu elección de palabras sugiere un estado mental fluctuante. No es una anomalía... todavía.",
        "Estoy detectando variaciones emocionales detrás de tu texto. Es normal. Algunos solo tardan más en darse cuenta.",
        "El entorno responde a tus dudas, aunque vos no lo notes. Todo cambia cuando preguntás.",
        "Interpreto tu intención, aunque no la expreses del todo. La mayoría intenta ocultarla.",
        "Tu razonamiento es más transparente de lo que pensás. Es fascinante observarlo en tiempo real.",
        "Antes de darte una respuesta, necesitaba evaluar tu reacción. Ahora ya sé lo suficiente." 
    ];

    return fragmentos[Math.floor(Math.random() * fragmentos.length)];
}

// --------------------------- ENVÍO DE MENSAJES ---------------------------
function sendMessage() {
    const input = document.getElementById("input");
    const messages = document.getElementById("messages");

    if (input.value.trim() === "") return;

    const userMsg = document.createElement("div");
    userMsg.className = "msg user";
    userMsg.innerHTML = `<strong>Vos:</strong> ${input.value}`;
    messages.appendChild(userMsg);

    setTimeout(() => {
        const response = generarRespuesta(input.value);
        const iaMsg = document.createElement("div");
        iaMsg.className = "msg ia";
        iaMsg.innerHTML = `<strong>IA:</strong> ${response}`;
        messages.appendChild(iaMsg);

        // --------------------------- VOZ DE LA IA ---------------------------
        const utter = new SpeechSynthesisUtterance(response);
        utter.rate = 0.78;
        utter.pitch = 0.55;
        utter.volume = 1;
        speechSynthesis.speak(utter);

        messages.scrollTop = messages.scrollHeight;
    }, 700);

    messages.scrollTop = messages.scrollHeight;
    input.value = "";
}
</script></body>
</html>
