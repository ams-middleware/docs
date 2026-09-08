---
description: Crear y actualizar productos, de a uno o por lote, y sincronizar stock y precio.
---

# Productos

Public-API distingue dos tipos de producto:

| Tipo | Qué es |
| --- | --- |
| **base** | El producto padre, el que agrupa variaciones (por ejemplo, una remera con sus talles) |
| **simple** | Un producto sin variaciones, o una variación concreta de un base |

Un producto simple se asocia a su base con el campo `parents`.

## De a uno

### Crear

```http
POST /v3/product/base
POST /v3/product/simple
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/base" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/simple" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```json
{
  "sku": "REM-NEG-XL",
  "name": "Remera negra talle XL",
  "ref_code": "REM-001",
  "ean": "7791234567890",
  "upc": "012345678905",
  "category": "remeras",
  "multimedia_uid": "ABC000123456",
  "attributes": {
    "color": { "value": "Negro" },
    "talles": { "value": ["S", "M", "L"] }
  },
  "parents": ["REM-BASE-001"]
}
```

El único campo obligatorio es **`sku`**. El resto depende de lo que su catálogo necesite.

Tres detalles del formato que conviene mirar bien:

* **`attributes` es un objeto**, indexado por el identificador del atributo — no una lista. Esa clave
  es la que identifica al atributo: no hace falta repetirla adentro.
* **`attributes[].value` va con su tipo natural**: texto para `text`/`html`/`date`, número para
  `number`, booleano para `boolean`, lista para `list`, objeto para `json`. Si el atributo admite
  varios valores a la vez, se manda un objeto `{ "<tipo>": valor }`.
* **`parents` es una lista de SKU** de los productos base a los que pertenece la variación.

`ean` y `upc` son los códigos de barra del producto. `category` y `multimedia_uid` van como el
identificador suelto. La **marca** no tiene campo propio: va dentro de `attributes`, como cualquier
otro atributo del catálogo.

### Actualizar

```http
PUT /v3/product/base/{uid}
PUT /v3/product/simple/{uid}
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/base/{uid}" method="put" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/simple/{uid}" method="put" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

Mismo cuerpo que la creación, con dos diferencias:

* **El `uid` del producto va en la ruta**, no en el cuerpo.
* **El cuerpo es parcial**: un campo que no mande queda como estaba. Para vaciar un valor hay que
  mandarlo explícitamente en blanco.

El `sku` no se puede cambiar: identifica al producto dentro de su cliente y se ignora si viene.

### Stock y precio de un producto

```http
PUT /v3/product/inventory
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/inventory" method="put" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```json
{ "sku": "REM-NEG-XL", "stock": 42, "price": 15990.00 }
```

## Por lote

Para cargas masivas, los endpoints de **bulk** reciben un arreglo de productos en una sola llamada.

### Crear productos

```http
POST /v3/product/bulk/base
POST /v3/product/bulk/simple
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/bulk/base" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/bulk/simple" method="post" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```json
{
  "products": [
    { "sku": "REM-NEG-S",  "name": "Remera negra talle S",  "category": "REMERAS" },
    { "sku": "REM-NEG-M",  "name": "Remera negra talle M",  "category": "REMERAS" },
    { "sku": "REM-NEG-XL", "name": "Remera negra talle XL", "category": "REMERAS" }
  ]
}
```

{% hint style="warning" %}
**Estos endpoints solo CREAN.** No actualizan productos existentes: un SKU que ya existe se reporta como error en el detalle de la respuesta y el resto del lote sigue procesándose. Para modificar un producto use `PUT /v3/product/{tipo}/{uid}`.
{% endhint %}

### Actualizar stock y precio

```http
PUT /v3/product/bulk/inventory
```

{% openapi src="https://api.beta.e-middleware.com/docs.json" path="/v3/product/bulk/inventory" method="put" %}
https://api.beta.e-middleware.com/docs.json
{% endopenapi %}

```json
{
  "products": [
    { "sku": "REM-NEG-S",  "stock": 12, "price": 15990.00 },
    { "sku": "REM-NEG-M",  "stock": 8,  "price": 15990.00 }
  ]
}
```

### Respuesta de un lote

Los endpoints de lote informan cuántos entraron, cuántos fallaron y por qué:

```json
{
  "success": 2,
  "failed": 1,
  "details": [
    { "sku": "REM-NEG-XL", "code": "ERR409", "message": "product already exists" }
  ]
}
```

Un lote con errores parciales devuelve `200`: los que se pudieron crear se crearon. **Revise siempre `failed` y `details`**, no alcanza con mirar el código HTTP.

## Qué mirar

* **Máximo 200 productos por lote.** Un arreglo más grande se rechaza con `400`.
* **El `sku` es la clave.** Es lo que usa el middleware para identificar el producto dentro de su cliente.
* **`category` y los `attributes` deben existir** en la configuración de su cliente. Si manda un atributo que no está declarado, se ignora.
* Para asociar imágenes, cargue primero el set multimedia y pase su identificador en `multimedia_uid`. Ver [Multimedia](multimedia.md).
