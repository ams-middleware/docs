---
description: Conectar su propio canal de atención al asistente con IA del middleware.
---

# Chat con IA

Public-API expone el **asistente con inteligencia artificial** para que su sistema —un chat web, una app, un bot de WhatsApp o el panel de un call center— lo consulte con una sola llamada. El asistente responde sobre el **catálogo** y sobre los **pedidos** del comprador, con datos reales de su cuenta.

```http
POST /v3/chat/message
Content-Type: application/json
Authorization: Bearer <token>
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/chat/message" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```json
{
  "message": "¿Dónde está mi pedido?",
  "chat_uid": "a1b2c3d4",
  "channel": "whatsapp",
  "email": "comprador@ejemplo.com",
  "order_ref": "ORD-2026-0001"
}
```

| Campo | Obligatorio | Para qué |
| --- | --- | --- |
| `message` | **sí** | El texto del comprador, tal cual lo escribió |
| `chat_uid` | no | Identificador de la conversación. **Sin él se abre una nueva**; la respuesta lo devuelve para que lo reenvíe en los mensajes siguientes |
| `channel` | no | Canal de origen (`web`, `whatsapp`, …), para trazabilidad |
| `email` · `document_id` · `order_ref` | no | Datos del comprador que su sistema ya validó. Ver más abajo |

## Conversación

El asistente mantiene el contexto por conversación. **Es responsabilidad de su sistema guardar el `chat_uid`** que devuelve la primera respuesta y enviarlo en cada mensaje posterior; sin él, cada mensaje arranca de cero.

## Consultar pedidos

Para responder sobre un pedido hay que saber de quién es. El asistente lo resuelve **dentro de la conversación**: si no tiene los datos, se los pide al comprador.

Si su sistema **ya identificó** al usuario, puede adelantarlos y ahorrarle esos pasos:

* `email` o `document_id`, **más** `order_ref`, o
* `email` **más** `document_id`.

{% hint style="info" %}
**Los datos no se creen: se validan contra el pedido real.** Enviarlos no le concede acceso a su sistema — si no coinciden con una orden, el asistente los vuelve a pedir por chat. Su sistema es un transporte de mensajes, no la autoridad de identidad.
{% endhint %}

## Qué mirar

* Sobre disponibilidad, el asistente informa **si hay o no hay** stock, nunca la cantidad exacta.
* Las consultas de catálogo no requieren identificar a nadie; las de pedidos sí.
* Este endpoint requiere el token de su conector, igual que el resto de la API.
