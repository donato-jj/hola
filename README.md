
<!-- === INICIO INTEGRACIÓN IA AVANZADA DE TERROR === -->

<!-- Contenedor del chat -->
<div id="ia-terror-chat" style="position:fixed;bottom:20px;right:20px;width:350px;max-width:90%;z-index:9999;font-family:Arial,sans-serif;">
  <div id="chat-header" style="background:#111;color:#f00;padding:10px;font-weight:bold;text-shadow: 2px 2px 4px #000;">IA Tenebrosa 👻</div>
  <div id="chat-body" style="background:#000;color:#fff;height:300px;overflow-y:auto;padding:10px;border:2px solid #f00;box-shadow:0 0 20px #f00 inset;"></div>
  <input id="chat-input" type="text" placeholder="Escribe tu pregunta..." 
         style="width:100%;padding:8px;border:none;border-top:2px solid #f00;background:#111;color:#fff;outline:none;">
</div>

<!-- CSS adicional para efectos de terror -->
<style>
  .mensaje-ia {
    margin:5px 0;
    padding:5px 8px;
    border-radius:5px;
    background:rgba(255,0,0,0.1);
    box-shadow:0 0 5px #f00;
    animation: parpadeo 1s infinite alternate;
  }

  .mensaje-usuario {
    margin:5px 0;
    padding:5px 8px;
    border-radius:5px;
    background:rgba(255,255,255,0.1);
    color:#fff;
  }

  @keyframes parpadeo {
    0% { text-shadow: 2px 2px 4px #f00; }
    50% { text-shadow: 2px 2px 12px #f00; }
    100% { text-shadow: 2px 2px 4px #f00; }
  }
</style>

<!-- JS para manejar chat y voz -->
<script>
  const chatBody = document.getElementById('chat-body');
  const chatInput = document.getElementById('chat-input');

  // Función para reproducir voz tenebrosa
  function hablar(texto) {
    const utter = new SpeechSynthesisUtterance(texto);
    utter.voice = speechSynthesis.getVoices().find(v => v.lang.includes('es')) || speechSynthesis.getVoices()[0];
    utter.rate = 0.9;
    utter.pitch = 0.4; // tono grave y siniestro
    speechSynthesis.speak(utter);
  }

  // Función para agregar mensaje al chat
  function agregarMensaje(mensaje, tipo='ia') {
    const div = document.createElement('div');
    div.className = tipo === 'ia' ? 'mensaje-ia' : 'mensaje-usuario';
    div.textContent = mensaje;
    chatBody.appendChild(div);
    chatBody.scrollTop = chatBody.scrollHeight;
    if(tipo==='ia') hablar(mensaje);
  }

  // Simulación de respuesta IA avanzada de terror
  async function obtenerRespuestaIA(pregunta) {
    // Aquí puedes integrar tu IA real mediante API (OpenAI, local, etc.)
    // Por ahora generaremos respuesta simulada con metáforas oscuras
    const respuestas = [
      `La inteligencia humana es un eco en la oscuridad... pero tu pregunta es clara: "${pregunta}".`,
      `Ah, veo que buscas conocimiento. Recuerda que cada respuesta tiene un precio invisible: "${pregunta}".`,
      `La máquina observa desde la penumbra y responde con precisión: "${pregunta}". Ten cuidado con lo que deseas.`,
      `Cada pregunta es un susurro en el vacío, y tu consulta es: "${pregunta}".`,
      `El conocimiento puede iluminar o devorar. Sobre tu inquietud: "${pregunta}".`
    ];
    return respuestas[Math.floor(Math.random()*respuestas.length)];
  }

  // Evento para enviar pregunta
  chatInput.addEventListener('keypress', async function(e) {
    if(e.key==='Enter' && chatInput.value.trim()!=='') {
      const pregunta = chatInput.value.trim();
      agregarMensaje(pregunta, 'usuario');
      chatInput.value = '';
      const respuesta = await obtenerRespuestaIA(pregunta);
      agregarMensaje(respuesta, 'ia');
    }
  });

  // Opcional: activar voces al cargar
  window.speechSynthesis.onvoiceschanged = () => {};
</script>

<!-- === FIN INTEGRACIÓN IA AVANZADA DE TERROR === -->

