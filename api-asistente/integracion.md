# Guía de integración paso a paso

Esta guía muestra cómo conectar su canal al asistente. Los ejemplos usan `curl`, pero el mismo pedido se hace igual desde cualquier lenguaje.

***

### Antes de empezar

| Dato | Valor |
|---|---|
| **Dirección** | `https://api.e-middleware.ar` |
| **Endpoint** | `POST /v3/chat/message` |
| **Autenticación** | Encabezado `Authorization: Bearer SU_TOKEN` |
| **Formato** | JSON (`Content-Type: application/json`) |

***

### Paso 1 — El primer mensaje

Envíe el mensaje del comprador **sin** `chat_uid`. Así nos indica que es una conversación nueva.

```bash
curl -X POST https://api.e-middleware.ar/v3/chat/message \
  -H "Authorization: Bearer SU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "hola, ¿tienen la camisa oversize en talle M?"
  }'
```

Respuesta:

```json
{
  "chat_uid": "6a68f40cc27db2b9a0f4e226",
  "reply": "¡Hola! Sí, la CAMISA OVERSIZE está disponible en talle M, a $58.000.",
  "mode": "ai",
  "identified": false
}
```

**Muestre `reply` al comprador y guarde `chat_uid`.**

***

### Paso 2 — Continuar la conversación

En cada mensaje siguiente, incluya el `chat_uid` que recibió.

```bash
curl -X POST https://api.e-middleware.ar/v3/chat/message \
  -H "Authorization: Bearer SU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "chat_uid": "6a68f40cc27db2b9a0f4e226",
    "message": "¿y en negro?"
  }'
```

Como el asistente tiene el hilo, entiende que "¿y en negro?" se refiere a la camisa de la que venían hablando.

{% hint style="info" %}
**No hay que "cerrar" ni "abrir" nada.** El mismo endpoint crea la conversación o la continúa, según incluya o no el `chat_uid`.
{% endhint %}

***

### Paso 3 — Consultas sobre pedidos

Si el comprador pregunta por un pedido, el asistente **necesita confirmar su identidad** antes de dar información. Tiene dos caminos:

**A. Su sistema ya sabe quién es** (el comprador está logueado en su tienda). Envíe sus datos y el asistente responde directo, sin preguntar nada:

```bash
curl -X POST https://api.e-middleware.ar/v3/chat/message \
  -H "Authorization: Bearer SU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "¿cuándo llega mi pedido?",
    "email": "comprador@ejemplo.com",
    "order_ref": "A-10045"
  }'
```

**B. No sabe quién es** (un chat anónimo en la web). No envíe nada: el asistente le va a pedir los datos al comprador dentro de la conversación, y usted solo transporta esos mensajes como cualquier otro.

Los detalles de qué datos enviar están en [Identificar al comprador](identificacion.md).

***

### Paso 4 — Detectar que interviene una persona

Revise el campo `mode` de cada respuesta:

| `mode` | Significado | Qué hacer |
|---|---|---|
| `ai` | Responde el asistente | Mostrar `reply` normalmente |
| `handoff` | La conversación pasó a un operador de su equipo | Mostrar `reply` y avisar que un asesor va a continuar |

{% hint style="info" %}
Después de un `handoff`, su sistema puede seguir enviando los mensajes del comprador con el mismo `chat_uid`: quedan registrados y el operador los ve en su panel.
{% endhint %}

***

### Ejemplo completo

Así se ve una integración mínima en su servidor:

```javascript
// EN SU SERVIDOR — nunca en el navegador del comprador
async function preguntarAlAsistente(mensaje, chatUid, comprador) {
  const res = await fetch("https://api.e-middleware.ar/v3/chat/message", {
    method: "POST",
    headers: {
      "Authorization": `Bearer ${process.env.EMW_TOKEN}`,
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      message: mensaje,
      chat_uid: chatUid || undefined,          // ausente en el primer mensaje
      email: comprador?.email,                  // si lo conoce
      document_id: comprador?.documento,        // si lo conoce
    }),
  });

  if (res.status === 429) {
    return { reply: "Estamos con mucha demanda, probá de nuevo en un momento." };
  }
  if (!res.ok) {
    return { reply: "No pudimos procesar tu consulta. Intentá más tarde." };
  }

  const data = await res.json();
  // Guardar data.chat_uid en la sesión del comprador para el próximo mensaje
  return data;
}
```

***

### Buenas prácticas

| Recomendación | Por qué |
|---|---|
| **El token vive solo en su servidor** | En el navegador o en una app, cualquiera puede leerlo |
| **Un `chat_uid` por comprador** | Si mezcla conversaciones, el asistente cruza contextos de personas distintas |
| **Envíe los datos del comprador si los tiene** | Le ahorra al comprador tener que identificarse |
| **Muestre un indicador de "escribiendo…"** | La respuesta puede demorar unos segundos: el asistente consulta datos reales antes de contestar |
| **Contemple el error 429** | Significa "reintentá en un momento", no "algo se rompió" |
| **No reintente automáticamente en bucle** | Cada mensaje consume su servicio contratado |

***

### Próximos pasos

* [Identificar al comprador](identificacion.md) — cómo evitar que el asistente pida datos
* [Referencia de la API](referencia.md) — todos los campos y errores
