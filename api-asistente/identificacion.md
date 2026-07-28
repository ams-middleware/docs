# Identificar al comprador

Para responder consultas sobre **productos**, el asistente no necesita saber quién pregunta.

Para hablar de un **pedido** —su estado, su dirección de entrega, sus pagos— sí: son datos personales, y hay que confirmar que quien pregunta es el titular.

{% hint style="warning" %}
**Un número de pedido, por sí solo, no identifica a nadie.** Los números de pedido son fáciles de adivinar o de encontrar en un correo reenviado. Por eso hacen falta **dos datos**.
{% endhint %}

***

### Los dos caminos

#### A. Su sistema ya conoce al comprador

Es el caso de una tienda con usuarios registrados: cuando el comprador escribe, usted ya sabe su email y su documento.

**Envíe esos datos junto al mensaje** y el asistente responde sin preguntar nada.

```json
{
  "message": "¿cuándo llega mi pedido?",
  "email": "comprador@ejemplo.com",
  "order_ref": "A-10045"
}
```

#### B. El comprador es anónimo

Es el caso de un chat abierto en la web, sin login. **No envíe datos de identidad.** El asistente le va a pedir al comprador los datos que necesita, dentro de la propia conversación, y usted solo transporta esos mensajes.

No tiene que programar nada especial para esto: es una conversación como cualquier otra.

***

### Qué combinaciones sirven

Hacen falta **dos** de estos tres datos. Con uno solo, el asistente pedirá el que falta.

| Combinación | Qué habilita |
|---|---|
| **Email + número de pedido** | Ese pedido |
| **Documento + número de pedido** | Ese pedido |
| **Email + documento** | Todos los pedidos de esa persona |

{% hint style="info" %}
**El número de pedido puede ser el suyo.** Aceptamos tanto nuestro número interno como el número de la plataforma donde se generó la venta. No necesita traducir nada.
{% endhint %}

***

### Campos

| Campo | Descripción |
|---|---|
| `email` | Email con el que se hizo la compra |
| `document_id` | Documento (DNI) del comprador |
| `order_ref` | Número del pedido sobre el que consulta |

***

### Qué pasa si los datos no coinciden

Nada se rompe. Si los datos que envía no corresponden a ningún pedido —porque están desactualizados, porque el comprador compró con otro email, o por un error de su sistema—, el asistente simplemente **le pedirá los datos al comprador** dentro de la conversación.

Su integración no necesita detectar ni manejar ese caso.

***

### Cómo saber si el comprador quedó identificado

La respuesta incluye el campo `identified`:

```json
{
  "chat_uid": "6a68f40cc27db2b9a0f4e226",
  "reply": "Tu pedido A-10045 está en camino, llega el jueves.",
  "mode": "ai",
  "identified": true
}
```

| Valor | Significado |
|---|---|
| `true` | Ya se confirmó la identidad: el asistente puede hablar de sus pedidos |
| `false` | Todavía no. Puede responder consultas de catálogo, pero pedirá datos si preguntan por un pedido |

Es informativo: no hace falta que su sistema haga nada distinto según ese valor.

***

### Por qué lo hacemos así

{% hint style="success" %}
**Los datos que usted envía no se dan por buenos: se verifican.** No alcanza con que su sistema afirme quién es el comprador — nosotros comprobamos que esos datos correspondan a un pedido real.

Esto protege a las dos partes. Si su sistema tiene un error, o si alguien lograra usar sus credenciales, **no puede obtener datos de compradores ajenos**: sin los datos correctos de un pedido real, no hay acceso.
{% endhint %}

Por seguridad, si se acumulan varios intentos fallidos de identificación en una misma conversación, esta se deriva automáticamente a un operador de su equipo.

***

### Volver

* [Guía de integración](integracion.md)
* [Referencia de la API](referencia.md)
