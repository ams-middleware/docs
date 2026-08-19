---
description: Cambios, devoluciones y cancelaciones sobre una orden ya vendida.
---

# Cambios, devoluciones y cancelaciones

Los tres se abren desde el detalle de la orden original y quedan **vinculados** a ella, así que la
trazabilidad se mantiene.

| | Cuándo | Qué genera |
|---|---|---|
| 🔁 **Cambio** | El comprador se lleva otro producto. | Una orden de cambio asociada. |
| ↩️ **Devolución** | El comprador devuelve y se le reintegra. | Una orden de devolución asociada. |
| 🚫 **Cancelación** | La venta no se concreta. | Anula la orden y libera el stock. |

## Cómo se hace

1. Abra la orden original.
2. Elija **Cambio** o **Devolución** en el toolbar.
3. Marque **qué ítems** entran en el caso y las cantidades.
4. Complete el motivo y confirme.

{% hint style="info" %}
📸 **Captura pendiente — `ord-postventa-01`** · GIF (10 s)

Desde el detalle de una orden completada: abrir **Devolución**, seleccionar un ítem, poner motivo y
confirmar. Mostrar la orden nueva que queda vinculada.
{% endhint %}

{% hint style="warning" %}
⚠️ Un cambio o una devolución **mueven stock**: lo devuelto vuelve al disponible y lo entregado se
descuenta. Confirme los ítems antes de guardar.
{% endhint %}

## Cancelar

Se cancela desde **Cambiar estado** → **Cancelada**. Ver [Estados](estados.md).

{% hint style="danger" %}
🛑 Solo se puede cancelar **antes** de que la orden llegue a Completada. Después, el camino es una
devolución.
{% endhint %}

## Qué ve el canal

Según el conector, el cambio de estado puede informarse de vuelta a la plataforma de origen. Si el
canal no lo refleja, revise el [conector](../conectores.md): puede no tener habilitado el envío de
estados.
