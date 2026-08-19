---
icon: layer-group
description: El historial de todo lo que corre en segundo plano y el estado de cada carga.
---

# 🗂️ Gestión masiva

Acá aterrizan las importaciones, las exportaciones, las acciones masivas y las sincronizaciones. Cada
una es un **proceso** con su resultado.

{% hint style="info" %}
📸 **Captura pendiente — `bulk-listado-01`** · PNG

Listado de Gestión masiva con procesos de distinto origen (importación, exportación, sincronización)
y distintos estados.
{% endhint %}

## Qué muestra cada línea

| | |
|---|---|
| **Origen** | Qué lo generó: una importación, una exportación, una acción masiva. |
| **Estado** | Ver [Procesos en segundo plano](../comunes/procesos.md). |
| **Registros** | Cuántos se procesaron, cuántos fallaron. |
| **Usuario y fecha** | Quién lo lanzó y cuándo. |

## Ver el detalle

Al abrir un proceso ve **fila por fila** qué pasó. Las que fallaron traen el motivo.

{% hint style="info" %}
💡 Filtre por estado **Completado con errores** para encontrar rápido lo que quedó a medias. Ver
[Filtrado avanzado](../comunes/filtrado-avanzado.md).
{% endhint %}

## Lanzar una carga

Las importaciones y exportaciones se disparan desde el módulo correspondiente —Productos, Órdenes— y
aparecen acá. El paso a paso y el formato del archivo están en
[Importar y exportar](../comunes/importar-exportar.md).

{% hint style="warning" %}
⚠️ Un archivo grande puede tardar. No lo vuelva a subir porque "no pasó nada": revise primero el
estado del proceso. Subirlo dos veces duplica el trabajo y puede duplicar registros.
{% endhint %}
