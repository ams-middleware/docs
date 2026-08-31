---
description: >-
  Public-API es la puerta de entrada del ecosistema E-MW para integradores:
  órdenes, productos, seguimiento, multimedia y reporting.
---

# Intro

**Public-API** es el microservicio de integración pública del ecosistema E-MW. Expone las operaciones que un sistema externo necesita para trabajar contra el middleware: consultar y crear órdenes, dar de alta productos, actualizar inventario y precios, seguir un envío y extraer datos para reporting.

## URL base

Cada cliente tiene su propio host. El que corresponde a su cuenta se lo entrega el equipo de E-MW junto con el token.

| Entorno | URL base |
| --- | --- |
| Producción | `https://<su-host>.e-middleware.ar` |
| Pruebas (beta) | `https://api.beta.e-middleware.com` |

{% hint style="info" %}
Todas las rutas de esta documentación son relativas a esa URL base. Un `POST /v3/product/base` significa `POST https://<su-host>.e-middleware.ar/v3/product/base`.
{% endhint %}

## Especificación OpenAPI

La lista completa y siempre actualizada de endpoints, con sus esquemas, parámetros y respuestas, está publicada en formato **OpenAPI 3**:

{% embed url="https://api.beta.e-middleware.com/docs.json" %}
Especificación OpenAPI 3 de Public-API
{% endembed %}

Ese archivo se puede importar en Postman, Insomnia o Swagger UI, y sirve para generar clientes automáticamente en el lenguaje que use su equipo.

{% hint style="success" %}
**Las tablas de parámetros de esta documentación se generan desde esa especificación.** Cuando cambia la API, cambian solas: no hay una copia escrita a mano que pueda quedar desactualizada.
{% endhint %}

## Qué ofrece

{% content-ref url="autenticacion.md" %}
[autenticacion.md](autenticacion.md)
{% endcontent-ref %}

{% content-ref url="ordenes.md" %}
[ordenes.md](ordenes.md)
{% endcontent-ref %}

{% content-ref url="productos.md" %}
[productos.md](productos.md)
{% endcontent-ref %}

{% content-ref url="seguimiento.md" %}
[seguimiento.md](seguimiento.md)
{% endcontent-ref %}

{% content-ref url="multimedia.md" %}
[multimedia.md](multimedia.md)
{% endcontent-ref %}

{% content-ref url="reporting.md" %}
[reporting.md](reporting.md)
{% endcontent-ref %}

{% content-ref url="chat.md" %}
[chat.md](chat.md)
{% endcontent-ref %}

{% content-ref url="integraciones.md" %}
[integraciones.md](integraciones.md)
{% endcontent-ref %}

## Formato de las respuestas

Todas las respuestas son JSON. Los listados devuelven los resultados junto con la información de paginado:

```json
{
  "results": [ ... ],
  "info": {
    "total_rows": 128,
    "total_pages": 13,
    "current_page": 1,
    "per_page": 10
  }
}
```

Los errores devuelven siempre la misma forma, con el código HTTP correspondiente:

```json
{
  "name": "not_found",
  "message": "Resource not found",
  "code": "ERR404"
}
```

| HTTP | Cuándo |
| --- | --- |
| `400` | El cuerpo o los parámetros no son válidos |
| `401` | Falta el token, está vencido o es inválido |
| `403` | El token no tiene permiso para esa operación |
| `404` | El recurso no existe |
| `409` | El recurso ya existe o hay un conflicto de estado |
| `429` | Se alcanzó un límite de uso |
| `500` | Error interno |
