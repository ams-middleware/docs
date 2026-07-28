# 🤖 Asistente IA por API

El sistema permite conectar **su propio canal de atención** —el chat de su tienda, su aplicación móvil, su bot de WhatsApp o el panel de su call center— a nuestro **asistente con inteligencia artificial**.

El asistente responde las consultas de sus compradores sobre **productos** y sobre **sus pedidos**, con datos reales y actualizados de su catálogo y sus órdenes.

{% hint style="success" %}
**Una sola llamada.** Su sistema envía el mensaje del comprador y recibe la respuesta lista para mostrar. Toda la complejidad —entender la pregunta, buscar en el catálogo, consultar el pedido, redactar la respuesta— ocurre de nuestro lado.
{% endhint %}

***

### ¿Qué puede responder el asistente?

| Tipo de consulta | Ejemplos | ¿Requiere identificar al comprador? |
|---|---|---|
| **Catálogo** | "¿Tienen la camisa en talle 42?", "¿Cuánto sale?", "¿Qué colores hay?" | **No.** Responde a cualquiera |
| **Pedidos** | "¿Dónde está mi pedido?", "¿Cuándo llega?", "¿A qué dirección va?" | **Sí.** Ver [Identificar al comprador](identificacion.md) |

Sobre disponibilidad, el asistente informa **si hay o no hay** stock, nunca la cantidad exacta.

***

### Requisitos previos

| Requisito | Detalle |
|---|---|
| **Token de acceso** | El **mismo token** que usa para el resto de nuestra API pública. Si ya integró productos u órdenes, no necesita credenciales nuevas. Si no lo tiene, solicítelo a soporte |
| **Servicio contratado** | El asistente IA es un servicio que se contrata aparte. Si no está activo para su cuenta, la API responde con un aviso claro |
| **Un servidor propio** | Las llamadas se hacen **desde su servidor**, nunca desde el navegador del comprador. Ver la advertencia de abajo |

{% hint style="danger" %}
**Nunca ponga su token en el navegador ni en una aplicación móvil.** El token identifica a su empresa y da acceso a sus datos. Si lo incluye en el código de una página web o de una app, cualquier persona puede leerlo y usarlo.

Su página o app debe hablar con **su propio servidor**, y su servidor con nuestra API.
{% endhint %}

***

### Cómo funciona: la conversación

El asistente **recuerda** lo que se habló. Para eso, cada conversación tiene un identificador llamado `chat_uid`.

1. **Primer mensaje:** usted lo envía **sin** `chat_uid`. Nosotros creamos la conversación y le devolvemos su `chat_uid`.
2. **Mensajes siguientes:** usted **reenvía ese mismo `chat_uid`** en cada llamada. Así el asistente entiende el hilo.

{% hint style="warning" %}
**Guardar el `chat_uid` es responsabilidad de su sistema.** Asócielo a la sesión del comprador (o a su usuario, si está logueado). Si lo pierde y envía un mensaje sin él, se abre una conversación nueva y el asistente no recordará lo anterior.
{% endhint %}

***

### Cuando interviene una persona

Si el comprador pide hablar con un humano, o su consulta necesita una gestión que el asistente no puede resolver (cancelar, modificar, un reclamo), la conversación pasa a un **operador de su equipo**, que la atiende desde el panel del sistema.

Usted se entera porque la respuesta viene con `mode: "handoff"` en lugar de `mode: "ai"`. A partir de ahí conviene avisarle al comprador que un asesor va a continuar la conversación.

***

### Guías

* [Guía de integración paso a paso](integracion.md)
* [Identificar al comprador](identificacion.md)
* [Referencia de la API](referencia.md)

***

### ¿Necesita ayuda?

Si no tiene su token, no sabe si el servicio está activo en su cuenta o tiene problemas para integrar, escriba a nuestro equipo de soporte: [support@mw-flow.com](mailto:support@mw-flow.com).
