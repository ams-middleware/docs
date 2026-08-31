---
description: >-
  Documentación técnica de los servicios públicos del ecosistema E-MW: cómo
  conectarse, autenticarse y operar desde su propio sistema.
---

# Bienvenido

Esta es la documentación técnica de **E-MW**, pensada para los equipos de desarrollo que integran un sistema externo con el middleware.

Acá encontrará únicamente los **servicios públicos**: los que exponen una interfaz para que su plataforma —tienda, ERP, marketplace o desarrollo propio— consuma o alimente datos. Los servicios internos del ecosistema no se documentan porque no son accesibles desde afuera.

{% hint style="info" %}
¿Busca cómo se usa el panel? Eso está en el [manual de usuario](https://docs.e-middleware.com/).
{% endhint %}

***

## Servicios públicos

### 🔹 Public-API

El servicio de integración principal. Permite consultar órdenes, crear productos, actualizar stock y precios, seguir un envío, servir imágenes de catálogo y extraer datos para reporting.

{% content-ref url="public-api/intro.md" %}
[intro.md](public-api/intro.md)
{% endcontent-ref %}

### 🔹 Webhook-API

Recibe las notificaciones que las plataformas externas envían al middleware —cambios de estado, nuevas órdenes, eventos de mensajería— y las traduce a acciones internas. Es el sentido inverso de Public-API: en lugar de que usted consulte, la plataforma avisa.

| Endpoint | Para qué |
| --- | --- |
| `POST /v3/callback/{connector_uid}` | Callback genérico de un conector |
| `POST /v3/callback/mercadolibre` | Notificaciones de MercadoLibre |
| `GET`/`POST` `/v1/meta/whatsapp` | Verificación y recepción de mensajes de WhatsApp |

> Documentación detallada en preparación.

### 🔹 Control-API

La API de administración del middleware: configuración de tiendas, conectores, atributos y catálogos. La consume el panel de administración.

> Documentación detallada en preparación.

***

## Antes de empezar

1. Pida al equipo de E-MW el **token de su conector** y la **URL de su cuenta**.
2. Lea la [guía de autenticación](public-api/autenticacion.md).
3. Pruebe contra el entorno de pruebas antes de apuntar a producción.

Todas las referencias de endpoints de esta documentación se generan desde la **especificación OpenAPI** publicada por cada servicio, así que reflejan siempre el contrato vigente.
