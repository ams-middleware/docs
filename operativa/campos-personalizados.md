---
description: Agregar a las órdenes datos propios que la plataforma no trae de fábrica.
---

# Campos personalizados

Sirven para guardar información de su operación que no viene en la orden estándar: número de remito,
vendedor asignado, observaciones de depósito.

## Crear uno

1. Entre a **Órdenes → Campos personalizados**.
2. **Nuevo campo** y complete:
   - **Nombre** — cómo se ve en la orden.
   - **Tipo** — texto, número, fecha, lista de opciones.
   - **Obligatorio** — si hay que completarlo sí o sí.
3. Guarde.

El campo aparece desde ese momento en el formulario de la orden.

{% hint style="info" %}
📸 **Captura pendiente — `ord-campos-01`** · GIF (8 s)

Crear un campo de tipo lista con dos opciones y después mostrarlo ya disponible en el formulario de
una orden.
{% endhint %}

{% hint style="warning" %}
⚠️ Marcar un campo como **obligatorio** afecta a las órdenes que se carguen desde ese momento. Las
que ya existen no se modifican, pero al editarlas le va a pedir completarlo.
{% endhint %}

{% hint style="danger" %}
🛑 Eliminar un campo borra también **los valores cargados en todas las órdenes**. Si solo quiere
dejar de usarlo, desactívelo.
{% endhint %}

{% hint style="info" %}
💡 Los campos personalizados salen en las [exportaciones](../comunes/importar-exportar.md), así que
sirven para clasificar y después analizar en Excel o Power BI.
{% endhint %}
