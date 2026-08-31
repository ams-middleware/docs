---
description: Seguimiento público de una orden — estado, historial del envío y documentos.
---

# Seguimiento

Estos endpoints están pensados para que **el comprador final** consulte su pedido desde una página pública, sin credenciales del integrador. Reciben el código de la orden y un token de seguimiento.

{% hint style="info" %}
Son los únicos endpoints de órdenes que no exigen el token del conector. El `token` que reciben por query es el **token de seguimiento de esa orden**, no la credencial de su integración.
{% endhint %}

## Estado de la orden

```http
GET /v3/tracking/{order_uid}?token={token_de_seguimiento}
```

```bash
curl "https://su-host.e-middleware.ar/v3/tracking/ORD000123456?token=abc123"
```

Devuelve el estado actual del pedido y sus datos visibles para el comprador.

## Historial del envío

```http
GET /v3/tracking/{order_uid}/tracking?token={token_de_seguimiento}
```

Devuelve los eventos del envío en orden cronológico: despachado, en camino, entregado.

## Documentos

```http
GET /v3/tracking/{order_uid}/documents?token={token_de_seguimiento}
```

Devuelve los documentos asociados a la orden —etiqueta, remito, factura— cuando existen.

## Qué mirar

* El `order_uid` va en la ruta; el `token` de seguimiento en la query.
* Un `404` significa que la orden no existe **o** que el token no corresponde a esa orden. Es deliberado: no se distingue una cosa de la otra para no revelar si un código existe.
* Estos endpoints exponen solo la información que el comprador puede ver. Para el detalle completo de una orden use [Órdenes](ordenes.md) con el token de su conector.
