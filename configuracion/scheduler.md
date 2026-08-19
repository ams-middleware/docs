---
description: Las tareas que corren solas y cada cuánto.
---

# Tareas programadas

Acá se ve qué hace la plataforma sin que nadie la toque: traer órdenes, sincronizar stock, actualizar
precios. Cada tarea tiene su frecuencia y su historial.

{% hint style="info" %}
📸 **Captura pendiente — `conf-scheduler-01`** · PNG

Listado de tareas programadas con frecuencia, última ejecución y estado. Resaltar una que haya
fallado.
{% endhint %}

## Qué mirar

| | |
|---|---|
| **Última ejecución** | Cuándo corrió y con qué resultado. |
| **Frecuencia** | Cada cuánto se repite. |
| **Estado** | Si está activa. |

{% hint style="info" %}
💡 Es el primer lugar donde mirar cuando "hace rato que no entran órdenes": si la tarea del canal no
corre, no entra nada y no hay ningún error visible en Órdenes.
{% endhint %}

{% hint style="warning" %}
⚠️ Subir la frecuencia no siempre mejora nada: muchos marketplaces limitan cuántas consultas aceptan
por hora y, si se pasa, empiezan a rechazar.
{% endhint %}

{% hint style="danger" %}
🛑 Desactivar una tarea **detiene la sincronización que hace**, sin ningún aviso posterior. Es la
causa silenciosa más común de "faltan órdenes" o "el stock quedó viejo".
{% endhint %}
