---
description: >-
  Webhook-API recibe las notificaciones que las plataformas externas envían al
  middleware.
---

# Intro

**Webhook-API** es el punto de entrada de los eventos que llegan desde afuera. Mientras [Public-API](../public-api/intro.md) es el servicio que *usted consulta*, Webhook-API es el que *la plataforma externa llama* cuando algo cambia de su lado: una orden nueva, un pago acreditado, un cambio de estado, un mensaje entrante.

## URL base

| Entorno | URL base |
| --- | --- |
| Producción | `https://webhook.e-middleware.ar` |
| Pruebas (beta) | `https://webhook.beta.e-middleware.com` |

## Endpoints

| Método | Ruta | Para qué |
| --- | --- | --- |
| `POST` | `/v3/callback/{connector_uid}` | Callback genérico. El `connector_uid` identifica de qué conector viene el evento |
| `GET` | `/v3/callback/{connector_uid}` | Verificación del endpoint, cuando la plataforma la exige antes de enviar eventos |
| `POST` | `/v3/callback/mercadolibre` | Notificaciones de MercadoLibre, que usa un formato propio |
| `GET` · `POST` | `/v1/meta/whatsapp` | Verificación y recepción de mensajes de WhatsApp (Meta) |

## Cómo se configura

La URL del webhook se carga **en la plataforma externa**, apuntando al conector correspondiente:

```
https://webhook.e-middleware.ar/v3/callback/SU_CONECTOR
```

El equipo de E-MW le indica el `connector_uid` que corresponde a su integración.

## Qué mirar

* **El middleware responde rápido y procesa después.** Un `200` significa "recibí el evento", no "ya lo procesé". Si la plataforma espera confirmación de procesamiento, hay que consultarla aparte.
* **Los eventos pueden llegar repetidos.** Las plataformas reintentan ante cualquier duda; el middleware descarta los duplicados, pero conviene saberlo si audita del otro lado.
* Cada plataforma define su propio formato de cuerpo y su propio esquema de verificación. Consulte con el equipo de E-MW al dar de alta un conector nuevo.

> Referencia detallada de cada formato en preparación.
