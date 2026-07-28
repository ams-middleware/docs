# Referencia de la API

***

## Enviar un mensaje

```
POST https://api.e-middleware.ar/v3/chat/message
```

Crea una conversación o continúa una existente, según incluya o no `chat_uid`.

### Encabezados

| Encabezado | Valor |
|---|---|
| `Authorization` | `Bearer SU_TOKEN` |
| `Content-Type` | `application/json` |

### Cuerpo del pedido

| Campo | Tipo | Obligatorio | Descripción |
|---|---|---|---|
| `message` | texto | **Sí** | Mensaje del comprador |
| `chat_uid` | texto | No | Identificador de la conversación. **Omitir en el primer mensaje**; incluirlo en todos los siguientes |
| `channel` | texto | No | Canal por el que escribe: `web`, `whatsapp` o `email`. Por defecto `web` |
| `email` | texto | No | Email de compra del comprador. Ver [Identificar al comprador](identificacion.md) |
| `document_id` | texto | No | Documento (DNI) del comprador |
| `order_ref` | texto | No | Número del pedido sobre el que consulta. Acepta el número nuestro o el de su plataforma |

### Respuesta

| Campo | Tipo | Descripción |
|---|---|---|
| `chat_uid` | texto | Identificador de la conversación. **Guárdelo y reenvíelo** en el próximo mensaje |
| `reply` | texto | Respuesta del asistente, lista para mostrar al comprador |
| `mode` | texto | `ai` = responde el asistente · `handoff` = la conversación pasó a un operador de su equipo |
| `identified` | booleano | Si la identidad del comprador ya está confirmada en esta conversación |

### Ejemplo

```bash
curl -X POST https://api.e-middleware.ar/v3/chat/message \
  -H "Authorization: Bearer SU_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "¿cuándo llega mi pedido?",
    "chat_uid": "6a68f40cc27db2b9a0f4e226",
    "email": "comprador@ejemplo.com",
    "order_ref": "A-10045"
  }'
```

```json
{
  "chat_uid": "6a68f40cc27db2b9a0f4e226",
  "reply": "Tu pedido A-10045 salió de nuestro depósito y llega el jueves a Av. Corrientes 1234.",
  "mode": "ai",
  "identified": true
}
```

***

## Errores

Todos los errores devuelven un cuerpo con esta forma:

```json
{
  "code": "ERR401",
  "name": "unauthorized",
  "message": "token inválido o expirado",
  "details": ""
}
```

| Código HTTP | Significado | Qué hacer |
|---|---|---|
| **400** | Falta `message` o el cuerpo no es JSON válido | Corregir el pedido |
| **401** | Token ausente, inválido o vencido | Revisar el encabezado `Authorization`. Si persiste, contactar a soporte |
| **409** | El asistente IA no está contratado para su cuenta | Contactar a soporte para activarlo |
| **429** | El servicio de IA está temporalmente sin capacidad | **Reintentar en unos minutos.** No es un error de su integración |
| **500** | Error de nuestro lado | Reintentar más tarde; si persiste, contactar a soporte |

{% hint style="warning" %}
**El 429 es temporal, el 500 no necesariamente.** Ante un 429 conviene reintentar con una espera creciente. Ante un 500 repetido, escriba a soporte en vez de seguir reintentando.
{% endhint %}

***

## Límites

| Límite | Detalle |
|---|---|
| **Tiempo de respuesta** | Hasta 2 minutos. El asistente consulta datos reales antes de responder; lo habitual son unos pocos segundos |
| **Consumo** | Cada mensaje consume su servicio contratado. Evite reintentos automáticos en bucle |

***

### Volver

* [Asistente IA por API](README.md)
* [Guía de integración](integracion.md)
