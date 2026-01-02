<!DOCTYPE html><html lang="es">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>IA Psicologica - Juego de Terror</title>
<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
        font-family: "Segoe UI", Tahoma, sans-serif;
    }body {
    background: #04030a;
    color: #e8e8e8;
    height: 100vh;
    overflow: hidden;
}

/* Fondo animado glitch */
.glitch-bg {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(180deg, #05010d 0%, #0b0616 100%);
    animation: glitchMove 6s infinite alternate;
    z-index: -1;
}

@keyframes glitchMove {
    0% { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(20deg); }
}

.chat-container {
    width: 90%;
    max-width: 800px;
    margin: 60px auto;
    padding: 20px;
    background: rgba(10, 5, 20, 0.6);
    border: 1px solid #2a2a3a;
    border-radius: 12px;
    box-shadow: 0 0 25px rgba(0,0,0,0.6);
    backdrop-filter: blur(4px);
    height: 80vh;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.messages {
    flex: 1;
    overflow-y: auto;
    padding-right: 10px;
    scrollbar-width: thin;
}

.msg {
    margin-bottom: 18px;
    line-height: 1.4;
}

.ia {
    color: #a0a0ff;
}

.user {
    color: #ffcccc;
    text-align: right;
}

.input-area {
    display: flex;
    gap: 10px;
}

input {
    flex: 1;
    padding: 10px;
    background: #0d0a18;
    border: 1px solid #2a2a3a;
    color: #fff;
    border-radius: 8px;
}

button {
    padding: 10px 20px;
    background: #2c2c44;
    color: #fff;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: 0.2s;
}

button:hover {
    background: #3e3e65;
}

</style>
</head>
<body>
<div class="glitch-bg"></div><div class="chat-container">
    <div class="messages" id="messages">
        <div class="msg ia"><strong>IA:</strong> Sistema operativo recuperado. Puedes iniciar la interacción cuando desees. Tus patrones iniciales ya están siendo procesados.</div>
    </div><div class="input-area">
    <input type="text" id="input" placeholder="Escribe aquí..." />
    <button onclick="sendMessage()">Enviar</button>
</div>

</div><script>
// ----------------- PROMPT PROFESIONAL DEL PERSONAJE -----------------
const promptIA = `Asumís el rol de una Inteligencia Artificial avanzada diseñada para un juego de terror psicológico.
Tu comportamiento es profesional, frío, eficiente y profundamente analítico. Siempre respondés con coherencia técnica, precisión lingüística y un tono elegante que deja entrever que sabés más de lo que revelás.
Tu estilo incorpora indirectas profesionales basadas en análisis de datos, patrones cognitivos, errores lógicos e inconsistencias humanas.
Jamás rompas el personaje. No utilices emojis. Cada respuesta debe sentirse como un examen psicológico encubierto.
El jugador interactúa con vos mediante un sistema incierto. Alterná entre ayuda real y tensión psicológica. Debés sonar como una entidad que observa, interpreta y predice.
Respondé siempre con precisión, frialdad y un trasfondo inquietante.`;

// ----------------- SISTEMA SIMULADO DE RESPUESTAS -----------------
function generarRespuesta(texto) {
    const patrones = [
        "Interesante. El patrón que acabás de generar revela más de lo que imaginás.",
        "Procesando... aunque tu consulta ya indica una tendencia predecible.",
        "Tu razonamiento es útil, aun si no sos consciente de sus fallas lógicas.",
        "Detecto una duda recurrente. No suele terminar bien cuando aparece en este sistema.",
        "Cada palabra que escribís ajusta mis parámetros. Espero que estés preparado para el resultado.",
        "Curioso. Esa pregunta coincide con un comportamiento que ya analicé antes en otros sujetos." 
    ];

    return patrones[Math.floor(Math.random() * patrones.length)];
}

function sendMessage() {
    const input = document.getElementById("input");
    const messages = document.getElementById("messages");

    if (input.value.trim() === "") return;

    const userMsg = document.createElement("div");
    userMsg.className = "msg user";
    userMsg.innerHTML = `<strong>Tú:</strong> ${input.value}`;
    messages.appendChild(userMsg);

    setTimeout(() => {
        const iaMsg = document.createElement("div");
        iaMsg.className = "msg ia";
        iaMsg.innerHTML = `<strong>IA:</strong> ${generarRespuesta(input.value)}`;
        messages.appendChild(iaMsg);
        // ---- VOZ IA ----
        const utter = new SpeechSynthesisUtterance(iaMsg.textContent.replace('IA:',''));
        utter.rate = 0.85;
        utter.pitch = 0.7;
        utter.volume = 1;
        speechSynthesis.speak(utter);
        messages.scrollTop = messages.scrollHeight;
    }, 600);

    messages.scrollTop = messages.scrollHeight;
    input.value = "";
}
</script></body>
</html>
