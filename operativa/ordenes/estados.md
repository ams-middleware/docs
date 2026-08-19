---
description: Los estados de una orden y cómo cambiarlos a mano.
---

# Estados de una orden

| Estado | Significa |
|---|---|
| ⏳ **Pendiente** | Registrada, esperando avanzar. |
| ✅ **Completada** | Terminó todas sus etapas. |
| 🚫 **Cancelada** | Se anuló antes de completarse. |

## Cambiarlo a mano

1. En el detalle de la orden, **Cambiar estado**.
2. Elija el estado nuevo y confirme.

<figure><img src="../../.gitbook/assets/07-01-2026_16-27-53 (1).gif" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
🛑 Los cambios de estado **no tienen vuelta atrás**:
una orden **Completada** no vuelve a Pendiente ni se cancela; una **Cancelada** no puede completarse.
Si se equivocó, la salida es [versionar](detalle.md#versionar), no revertir.
{% endhint %}

{% hint style="info" %}
💡 Lo normal es que el estado avance solo con el [workflow](../../configuracion/workflows.md).
Cambiarlo a mano es para destrabar casos puntuales, no la operación de todos los días.
{% endhint %}
