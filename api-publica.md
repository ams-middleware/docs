---
description: >-
  Conectar su propio sistema al middleware: órdenes, productos, seguimiento e
  imágenes por API.
---

# 🔗 Conectar su sistema por API

Todo lo que hace desde el panel se puede hacer también **desde su propio sistema**, por API: consultar órdenes, dar de alta productos, actualizar stock y precios, seguir un envío o extraer datos para reporting.

Esa es la **API pública** del middleware, y su documentación técnica vive en un sitio aparte, pensado para el equipo de desarrollo que hace la integración.

{% hint style="info" %}
**📘 Documentación técnica: [docs.e-middleware.dev](https://docs.e-middleware.dev/)**

Ahí están los endpoints, los parámetros, los ejemplos y la especificación OpenAPI lista para importar en Postman.
{% endhint %}

***

### Qué puede integrar

| Necesidad | Dónde leerlo |
| --- | --- |
| Consultar y buscar órdenes | [Órdenes](https://docs.e-middleware.dev/public-api/ordenes) |
| Crear productos y actualizar stock y precios | [Productos](https://docs.e-middleware.dev/public-api/productos) |
| Mostrar el seguimiento de un pedido en su web | [Seguimiento](https://docs.e-middleware.dev/public-api/seguimiento) |
| Servir las imágenes del catálogo con el tamaño que necesita | [Multimedia](https://docs.e-middleware.dev/public-api/multimedia) |
| Conectar Power BI o Excel a los datos de órdenes | [Reporting](https://docs.e-middleware.dev/public-api/reporting) |

### Cómo se empieza

1. Pida al equipo de E-MW el **token de su conector** y la **URL de su cuenta**.
2. Siga la [guía de autenticación](https://docs.e-middleware.dev/public-api/autenticacion).
3. Pruebe contra el entorno de pruebas antes de apuntar a producción.

{% hint style="warning" %}
**El token es una credencial de producción y no vence.** Guárdelo como una contraseña, nunca en el código ni en un correo. Si sospecha que se filtró, avise de inmediato al equipo de E-MW.
{% endhint %}

***

### Otras integraciones

* **[🤖 Asistente IA por API](api-asistente/README.md)** — conectar su chat, su app o su call center al asistente.
* **[Conectar con Power BI](conexion-bi/powerbi.md)** y **[con Excel](conexion-bi/excel.md)** — sin escribir código.
