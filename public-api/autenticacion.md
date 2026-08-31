---
description: Cómo autenticar las llamadas a Public-API con el token de su conector.
---

# Autenticación

Public-API usa un **token JWT** que identifica a su conector y al cliente al que pertenece. El token se lo entrega el equipo de E-MW; no se genera desde la API.

## Cómo se envía

En el encabezado `Authorization`, con el prefijo `Bearer`:

```http
POST /v3/product/base HTTP/1.1
Host: su-host.e-middleware.ar
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json
```

Con `curl`:

```bash
curl -X GET "https://su-host.e-middleware.ar/v3/order/search?limit=10" \
  -H "Authorization: Bearer $EMW_TOKEN"
```

## Qué identifica el token

El token lleva adentro el cliente y el conector, así que **no hace falta enviarlos en cada llamada**: la API resuelve sola el alcance de los datos. Una consulta de órdenes devuelve únicamente las de su cliente.

```json
{
  "client_uid": "SU_CLIENTE",
  "connector_uid": "SU_CONECTOR",
  "token_type": "app_connector"
}
```

## Qué mirar

{% hint style="warning" %}
**El token es una credencial de producción y no vence.** Trátelo como una contraseña:

* Guárdelo en un gestor de secretos o en una variable de entorno, nunca en el código ni en un repositorio.
* No lo comparta por correo ni por chat. Si necesita enviarlo, use un servicio de secretos de un solo uso.
* Si sospecha que se filtró, avise **de inmediato** al equipo de E-MW: la baja de un token no es automática.
{% endhint %}

## Endpoints sin autenticación

Algunos endpoints son públicos por diseño y no requieren token, porque los consume el comprador final o una página pública:

| Endpoint | Para qué |
| --- | --- |
| `GET /v3/tracking/{order_uid}` | Seguimiento de una orden por su código |
| `GET /v3/tracking/{order_uid}/tracking` | Historial de estados del envío |
| `GET /v3/tracking/{order_uid}/documents` | Documentos asociados a la orden |
| `GET /v3/multimedia/{client_uid}/image/{uid}/{position}` | Imagen de producto |
| `GET /v3/integration/search` | Catálogo de integraciones disponibles |
| `GET /odata` · `GET /odata/$metadata` | Documento de servicio y metadatos OData |

## Errores de autenticación

| HTTP | Significado | Qué hacer |
| --- | --- | --- |
| `401` | Falta el encabezado, el token es inválido o está mal formado | Verifique que envía `Authorization: Bearer <token>` completo |
| `403` | El token es válido pero no tiene permiso para esa operación | El conector no tiene habilitado ese permiso; consulte con E-MW |
