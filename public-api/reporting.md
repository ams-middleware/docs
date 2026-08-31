---
description: Extraer órdenes por OData para Power BI, Excel u otra herramienta de análisis.
---

# Reporting (OData)

Public-API expone un endpoint **OData v4** de solo lectura para conectar herramientas de análisis —Power BI, Excel, Tableau— directamente contra los datos de órdenes, sin exportar archivos a mano.

## Endpoints

| Endpoint | Autenticación | Para qué |
| --- | --- | --- |
| `GET /odata` | pública | Documento de servicio: qué colecciones hay |
| `GET /odata/$metadata` | pública | Esquema de los datos (lo que consume el cliente OData) |
| `GET /odata/orders` | **token** | Los datos de órdenes |

## Conectar Power BI

1. **Obtener datos** → **Fuente OData**.
2. URL: `https://su-host.e-middleware.ar/odata`
3. Autenticación: **Básica** o **Web API**, según su versión, usando el token del conector.

## Parámetros de consulta

`/odata/orders` acepta los operadores estándar de OData:

| Parámetro | Ejemplo | Para qué |
| --- | --- | --- |
| `$top` | `$top=100` | Traer las primeras N filas |
| `$skip` | `$skip=100` | Saltear N filas (paginado) |
| `$skiptoken` | `$skiptoken=...` | Continuar un listado grande |
| `$select` | `$select=uid,status,total` | Elegir columnas |
| `$orderby` | `$orderby=created_at desc` | Ordenar |
| `$filter` | `$filter=status eq 'completed'` | Filtrar |

```
https://su-host.e-middleware.ar/odata/orders?$filter=status eq 'completed'&$select=uid,total,created_at&$top=500
```

## Qué mirar

* Es **solo lectura**: OData no crea ni modifica nada.
* Las órdenes devueltas son siempre las de su cliente; el alcance lo fija el token.
* Para volúmenes grandes use `$top` junto con `$skip` o `$skiptoken` en vez de traer todo de una.
* La estructura anidada de la orden se conserva tal como está en el modelo; el `$metadata` es la referencia de qué campos hay.
