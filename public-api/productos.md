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
    { "sku": "REM-NEG-M",  "stock": 0 },
    { "sku": "REM-NEG-XL", "price": 16990.00 }
  ]
}
```

| Campo | Tipo | Obligatorio | Detalle |
| --- | --- | --- | --- |
| `sku` | string | sí | SKU del producto en el middleware. Tiene que existir: este endpoint no crea productos. |
| `stock` | entero ≥ 0 | uno de los dos | Stock **disponible absoluto**: el valor enviado pasa a ser el stock, no se suma ni se resta. Máximo 32.767. |
| `price` | número ≥ 0 | uno de los dos | Precio de venta. |

* **Hasta 300 productos por llamada.** Un arreglo más grande se rechaza entero con `400`.
* **El stock va en el SKU de cada variación** (talle, color…). En el SKU de un producto base se ignora.
* **El precio en un producto base se aplica a todas sus variaciones.** Si cada variación tiene su precio, mándelo por SKU de variación.
* **Puede mandar solo stock, solo precio o los dos.** No se aceptan negativos.
* **Mandar el mismo stock que ya tiene no genera movimiento** ni se reenvía a los canales: reenviar es seguro.
* **Mande siempre el disponible de su depósito.** El middleware descuenta lo reservado por órdenes en curso y publica el resultado.

La respuesta trae el total del lote y, en `details`, **solo los productos que fallaron** (SKU inexistente, negativos, ni stock ni precio):

```json
{
  "total": 3,
  "success": 2,
  "failed": 1,
  "details": [
    { "sku": "REM-NEG-XL", "code": "ERR000", "message": "product not found" }
  ]
}
```

| HTTP | Cuándo |
| --- | --- |
| `200` | el lote se procesó (revise `failed` y `details`) |
| `400` | lista vacía o más de 300 productos |
| `401` | token inválido |
| `403` | el conector no tiene el permiso de inventario por API |
| `5xx` / timeout | error temporal: reintente el mismo lote |

{% hint style="info" %}
**El `200` confirma que el middleware guardó el dato, no que ya esté en cada tienda.** El envío a los canales donde el producto está publicado (VTEX, Salesforce, Tiendanube…) se encola y se hace enseguida, de forma asincrónica.
{% endhint %}

#### Cómo integrarlo bien

1. **Agrupe en lotes de hasta 300 SKU** en vez de una llamada por producto.
2. **Mande solo lo que cambió** desde la última sincronización y, una vez al día, una carga completa.
3. **Procese los lotes de a uno**, o como mucho 2 o 3 en paralelo.
4. **Ante `5xx` o timeout, reintente el mismo lote** con espera creciente (5 s, 30 s, 2 min): como el stock es absoluto, repetir no duplica.
5. **No repita un SKU dentro del mismo lote.**

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

* **Máximo 200 productos por lote al crear y 300 al actualizar stock y precio.** Un arreglo más grande se rechaza con `400`.
* **El `sku` es la clave.** Es lo que usa el middleware para identificar el producto dentro de su cliente.
* **`category` y los `attributes` deben existir** en la configuración de su cliente. Si manda un atributo que no está declarado, se ignora.
* Para asociar imágenes, cargue primero el set multimedia y pase su identificador en `multimedia_uid`. Ver [Multimedia](multimedia.md).
