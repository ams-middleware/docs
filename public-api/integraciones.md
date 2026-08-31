---
description: Consultar el catálogo público de plataformas con las que el middleware se integra.
---

# Integraciones

Devuelve las plataformas con las que el middleware puede conectarse —tiendas, marketplaces, ERP, couriers—. Es un **catálogo público**: no requiere token, y está pensado para páginas de login, landings o pantallas de alta donde hay que mostrar con qué se integra el sistema.

```http
GET /v3/integration/search?type=ecommerce&limit=20
```

| Parámetro | Tipo | Para qué |
| --- | --- | --- |
| `type` | string | Filtrar por tipo (`ecommerce`, `courier`, `payment`, `notification`, …) |
| `value` | string | Texto libre de búsqueda |
| `flows` | string | Filtrar por flujo soportado |
| `page` · `limit` | entero | Paginado |

```bash
curl "https://su-host.e-middleware.ar/v3/integration/search?type=ecommerce"
```

## Qué mirar

{% hint style="info" %}
**Devuelve solo información pública** de cada integración: nombre, tipo y estado. La configuración, las credenciales y los permisos **nunca** salen por este endpoint, que es lo que permite exponerlo sin token.
{% endhint %}

* Se listan únicamente las integraciones **activas**.
* El resultado viene ordenado por nombre.
