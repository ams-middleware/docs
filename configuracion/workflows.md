---
description: El circuito que recorre una orden desde que entra hasta que se completa.
---

# Workflow de órdenes

El workflow define las etapas de una orden y qué pasa en cada una: reservar stock, cobrar, facturar,
despachar, informar al canal. La orden avanza sola de etapa en etapa.

{% hint style="info" %}
📸 **Captura pendiente — `conf-workflow-01`** · PNG

Pantalla de Workflow mostrando el circuito con sus etapas. Si hay vista de diagrama, usar esa.
{% endhint %}

## Dónde se ve el recorrido de una orden

En la pestaña **Workflow** del [detalle de la orden](../operativa/ordenes/detalle.md): muestra por
qué etapa va, cuáles pasó y dónde se trabó, con el error.

{% hint style="info" %}
💡 "La orden no avanza" casi siempre se responde en esa pestaña. Antes de forzar el estado a mano,
lea el error de la etapa trabada.
{% endhint %}

## Cuando una etapa falla

Una etapa que falla no siempre queda trabada. Si el problema puede ser pasajero —el canal caído, una
demora del courier— la plataforma la reintenta sola, esperando cada vez más entre un intento y el
siguiente:

| Intento | Espera |
|---|---|
| 1º | 1 minuto |
| 2º | 16 minutos |
| 3º | 1 hora y 20 |
| 4º | 4 horas y cuarto |
| 5º | 12 horas |
| 6º | 24 horas |

Los dos últimos son largos a propósito: si un canal se cae un viernes a la tarde, la orden sigue
intentando durante el fin de semana en lugar de darse por vencida en una hora.

{% hint style="info" %}
💡 Mientras una etapa espera, la pestaña **Workflow** muestra cuándo vuelve a intentar. No hace falta
hacer nada: si el canal se recupera, la orden sigue sola.
{% endhint %}

### Etapas que no reintentan

Algunas se detienen en el primer fallo, a propósito:

- **Las que revisan los datos de la orden.** Si falta información o los importes no cierran, el
  resultado va a ser el mismo las seis veces. Reintentar solo retrasaría el aviso.
- **Las que ya hicieron algo fuera de la plataforma.** Si el courier ya generó el retiro, repetir la
  etapa generaría una segunda etiqueta.

En esos casos corrija lo que falla y vuelva a lanzar la etapa desde la pestaña **Workflow**.

{% hint style="warning" %}
⚠️ Forzar el estado desde [Estados](../operativa/ordenes/estados.md) **saltea las etapas
pendientes**: si el workflow todavía no facturó o no descontó stock, esas acciones no van a ocurrir.
{% endhint %}

{% hint style="danger" %}
🛑 Modificar el workflow cambia el comportamiento de **todas las órdenes que entren desde ese
momento**, en todos los canales. Pruébelo con una orden de prueba antes de dejarlo activo.
{% endhint %}
