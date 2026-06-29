# 📊 Conexión con BI (PowerBI / Excel)

El sistema permite conectar herramientas de análisis externas como **Microsoft Power BI** y **Microsoft Excel** directamente a sus datos, para que pueda construir sus propios tableros, reportes y análisis **sin** descargar archivos manualmente.

La conexión se realiza a través de nuestra **API pública** usando el estándar **OData**, un protocolo que estas herramientas entienden de forma nativa.

{% hint style="success" %}
**Sus datos, siempre actualizados.** Una vez configurada la conexión, Power BI o Excel pueden **refrescar** la información cuando usted quiera (manual o programado), trayendo siempre los datos más recientes.
{% endhint %}

***

### ¿Qué es OData y por qué lo usamos?

OData es un estándar abierto para consultar datos por internet. Lo elegimos porque:

* **Es seguro:** usted nunca accede directamente a nuestra base de datos. Solo recibe **sus** datos, a través de una conexión protegida con un token personal.
* **Es automático:** Power BI y Excel se encargan solos de traer toda la información, página por página. Usted no programa nada.
* **Permite filtrar:** puede pedir solo lo que necesita (por ejemplo, las órdenes de un rango de fechas).

***

### Requisitos previos

Antes de conectar, asegúrese de tener:

| Requisito | Detalle |
|-----------|---------|
| **Token de acceso** | Su clave personal para la API pública. Si no la tiene, solicítela a nuestro equipo de soporte (ver más abajo). **Es personal e intransferible.** |
| **URL del servicio** | La **raíz** del servicio OData: `https://api.e-middleware.ar/odata`. Power BI / Excel descubren solos los feeds disponibles (hoy: `orders`). **Importante:** apunte a `/odata`, **no** a `/odata/orders` — si apunta directo a un feed, la herramienta no reconoce el servicio. |
| **La herramienta instalada** | **Power BI Desktop** (gratuito) o **Microsoft Excel** (versión 2016 o superior, con *Power Query / Obtener datos*). |
| **Conexión a internet** | Necesaria para traer y refrescar los datos. |

{% hint style="warning" %}
**Cuide su token.** Cualquiera que tenga su token puede consultar sus datos. No lo comparta ni lo deje en archivos públicos. Si cree que se filtró, contacte a soporte para **revocarlo** y generar uno nuevo.
{% endhint %}

***

### Datos disponibles

Se conecta a la **raíz** `https://api.e-middleware.ar/odata` y la herramienta le muestra los feeds disponibles para elegir:

| Feed (tabla) | Contenido |
|------|-----------|
| **`orders`** | Sus pedidos con todos sus datos: fechas, estados, totales, datos del comprador, envío, facturación e ítems. |

> Próximamente se sumarán más conjuntos de datos (ventas por día, stock). Esta sección se actualizará a medida que estén disponibles.

{% hint style="info" %}
**Sus datos llegan con la misma estructura que en el sistema.** Cada orden conserva su forma original, incluyendo la información **anidada** (envío, facturación, ítems, pagos…) como sub-tablas. No se aplana ni se recorta nada: usted decide qué expandir y mostrar desde Power BI o Excel.
{% endhint %}

***

### Lo que puede hacer desde la herramienta

La API entiende las siguientes opciones de OData, que Power BI y Excel usan automáticamente o que usted puede aplicar:

| Opción | Para qué sirve |
|--------|----------------|
| **Filtrar por fecha** | Traer solo las órdenes de un período (clave para el *refresco incremental*, que trae únicamente lo nuevo). |
| **Elegir columnas** | Traer solo los campos que necesita. |
| **Ordenar** | Ordenar los resultados (por fecha, por estado, etc.). |
| **Paginado automático** | La herramienta recorre todas las páginas sola hasta traer el dataset completo. |

***

### Guías paso a paso

* [Conectar con Power BI](powerbi.md)
* [Conectar con Excel](excel.md)

***

### ¿Necesita ayuda?

Si no tiene su token, no conoce su URL o tiene problemas para conectar, escriba a nuestro equipo de soporte: [support@mw-flow.com](mailto:support@mw-flow.com).
