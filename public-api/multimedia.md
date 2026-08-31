---
description: Servir imágenes de producto con transformaciones al vuelo.
---

# Multimedia

Public-API sirve las imágenes de producto y aplica las transformaciones **en el momento de la petición**. No hay que generar ni almacenar versiones previas: se pide la imagen con los parámetros que se necesitan y el servicio la devuelve.

```http
GET /v3/multimedia/{client_uid}/image/{uid}/{position}
```

| Parte de la ruta | Qué es |
| --- | --- |
| `client_uid` | Identificador de su cliente |
| `uid` | Identificador del set multimedia |
| `position` | Posición de la imagen dentro del set, empezando en `1` |

No requiere token: son imágenes públicas, pensadas para usarse directamente en un `<img src="...">`.

## Transformaciones

Se piden como parámetros de query y se combinan entre sí:

| Parámetro | Valores | Para qué |
| --- | --- | --- |
| `w` | entero | Ancho en píxeles |
| `h` | entero | Alto en píxeles |
| `format` | `webp` · `jpeg` · `png` · `avif` | Formato de salida |
| `quality` | 1-100 | Calidad de compresión |
| `bg` | hexadecimal, sin `#` | Color de fondo |
| `fit` | `fit` · `fill` · `force` · `auto` · `crop` | Cómo encajar la imagen en el tamaño pedido |

```
https://su-host.e-middleware.ar/v3/multimedia/SU_CLIENTE/image/ABC000123/1?w=800&format=webp&quality=90&fit=fit
```

## Qué mirar

* **`bg` solo tiene efecto sobre imágenes con transparencia** (PNG). En una imagen sin canal alfa el parámetro se ignora.
* Sin parámetros se devuelve el **archivo original**, que suele ser más pesado. Para catálogo y listados conviene pedir siempre `w` y `format=webp`.
* La posición empieza en `1`, no en `0`.
* Si el set o la posición no existen, responde `404`.
