---
description: Consultar órdenes del cliente — listado simple, búsqueda avanzada y detalle.
---

# Órdenes

Public-API permite **consultar** las órdenes de su cliente. El alcance lo define el token: solo ve las órdenes que le corresponden.

## Listado simple

```http
GET /v3/order/search?value=ABC123&page=1&limit=10
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/order/search" method="get" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```bash
curl -X GET "https://su-host.e-middleware.ar/v3/order/search?limit=10" \
  -H "Authorization: Bearer $EMW_TOKEN"
```

## Búsqueda avanzada

Cuando necesita filtrar por campos concretos, combinarlos u ordenar, use la versión `POST`:

```http
POST /v3/order/search
Content-Type: application/json
```

```json
{
  "fields": ["uid", "ref_code", "status", "created_at"],
  "filters": {
    "query_filter": [
      { "field": "status", "operator": "eq", "value": "completed" },
      { "field": "created_at", "operator": "gte", "value": "2026-01-01" }
    ]
  },
  "sort": { "field": "created_at", "order_by": "desc" },
  "page": 1,
  "limit": 50
}
```

| Campo | Para qué |
| --- | --- |
| `fields` | Qué campos devolver. Si se omite, vienen todos. Pedir solo lo necesario acelera la respuesta |
| `filters.query_filter` | Lista de condiciones. Se combinan con **Y** lógico |
| `sort` | `field` más `order_by` (`asc` o `desc`) |
| `page` · `limit` | Paginado. `limit` máximo **300** |

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/order/search" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

### Operadores disponibles

| Operador | Significado | Ejemplo de `value` |
| --- | --- | --- |
| `eq` | Igual a | `"completed"` |
| `ne` | Distinto de | `"canceled"` |
| `gt` · `gte` | Mayor / mayor o igual | `"2026-01-01"` |
| `lt` · `lte` | Menor / menor o igual | `"2026-12-31"` |
| `in` | Está en la lista | `"pending,processing"` |
| `nin` | No está en la lista | `"canceled,deleted"` |
| `regex` | Coincide con la expresión | `"^ORD-2026"` |

## Detalle de una orden

```http
GET /v3/order/{uid}
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/order/{uid}" method="get" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```bash
curl -X GET "https://su-host.e-middleware.ar/v3/order/ORD000123456" \
  -H "Authorization: Bearer $EMW_TOKEN"
```

Devuelve la orden completa: items, importes, dirección de envío, estado del workflow y datos del comprador.

## Qué mirar

* **`limit` tiene tope 300.** Un valor mayor se rechaza con `400`. Para volúmenes grandes, recorra las páginas con `page`.
* **Los filtros se combinan con Y**, no con O. Para un "o" use el operador `in` sobre el mismo campo.
* **Las fechas van en texto** con formato `AAAA-MM-DD`.
* Si necesita seguir un envío desde una página pública, sin token, use [Seguimiento](seguimiento.md).
