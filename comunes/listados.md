---
description: Buscar, ordenar, paginar y refrescar. Igual en todos los módulos.
---

# Listados: buscar, ordenar y paginar

{% hint style="info" %}
📸 **Captura pendiente — `comunes-listado-01`** · PNG

Cualquier listado (preferentemente Órdenes) mostrando la zona superior completa. Resaltar por
separado: buscador, ícono de filtro avanzado, botón de refrescar y selector de cantidad por página.
{% endhint %}

## Buscar

El campo de búsqueda de la barra superior busca **dentro del listado que está viendo**. Escriba y el
listado se actualiza solo; no hace falta presionar Enter.

{% hint style="info" %}
💡 Busque por el dato más único que tenga: número de orden, SKU o correo del comprador. Buscar por
nombre suele traer demasiados resultados.
{% endhint %}

Para cruzar varios criterios —por ejemplo, órdenes de un canal *y* de un rango de fechas— use
[Filtrado avanzado](filtrado-avanzado.md).

## Ordenar

Haga clic en el encabezado de una columna para ordenar por ella. Un segundo clic invierte el orden.

## Cuántos registros ve

Abajo del listado elige cuántos registros trae por página y navega entre páginas.

{% hint style="warning" %}
⚠️ El orden y los filtros se aplican **sobre todo el conjunto**, no solo sobre la página que ve. Si
exporta, se exporta lo filtrado completo, no los registros visibles.
{% endhint %}

## Refrescar

El botón ↻ vuelve a pedir los datos al servidor. Después de usarlo queda **inactivo unos segundos**
antes de poder repetirlo: es a propósito, para no saturar la plataforma.

{% hint style="info" %}
💡 Si acaba de lanzar una sincronización, no refresque en loop. Mire el estado del proceso en
[Procesos en segundo plano](procesos.md).
{% endhint %}
