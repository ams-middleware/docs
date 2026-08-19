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

{% hint style="warning" %}
⚠️ Forzar el estado desde [Estados](../operativa/ordenes/estados.md) **saltea las etapas
pendientes**: si el workflow todavía no facturó o no descontó stock, esas acciones no van a ocurrir.
{% endhint %}

{% hint style="danger" %}
🛑 Modificar el workflow cambia el comportamiento de **todas las órdenes que entren desde ese
momento**, en todos los canales. Pruébelo con una orden de prueba antes de dejarlo activo.
{% endhint %}
