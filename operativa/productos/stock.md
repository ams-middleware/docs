---
description: Cómo se llevan las existencias y los precios, y cómo llegan a los canales.
---

# Stock y precios

El stock se lleva en los **productos simples**. Cada movimiento queda registrado con su motivo: una
venta reserva, un despacho descuenta, una devolución repone.

{% hint style="info" %}
📸 **Captura pendiente — `prod-stock-01`** · PNG

Pestaña de stock de un producto simple con el historial de movimientos visible (RESERVED, OUT).
{% endhint %}

## Disponible vs. real

| | |
|---|---|
| **Real** | Lo que hay físicamente. |
| **Disponible** | Lo real menos lo reservado por órdenes en curso. Es lo que se publica. |

{% hint style="warning" %}
⚠️ Si en el canal ve menos unidades que en su depósito, no es un error: hay unidades **reservadas**
por ventas que todavía no se despacharon.
{% endhint %}

## Precios

Los precios se cargan por producto y, si su operación lo usa, pueden diferir por canal. El valor
específico de un canal **pisa** al general.

{% hint style="danger" %}
🛑 Un cambio de precio o de stock se propaga a **todos los canales publicados**, y en marketplaces
impacta en publicaciones activas con ventas en curso. Revise dos veces antes de una
[actualización masiva](../../comunes/acciones-masivas.md).
{% endhint %}

## Cuándo se sincroniza

La sincronización de stock corre sola, de forma periódica, según lo configurado en cada
[conector](../conectores.md). También puede forzarla desde el producto o desde el listado.

{% hint style="info" %}
💡 ¿Forzó la sincronización y el canal no cambió? Mire el resultado en
[Procesos en segundo plano](../../comunes/procesos.md): el envío pudo rechazarse.
{% endhint %}
