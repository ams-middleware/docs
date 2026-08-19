---
description: Qué son los procesos, cómo se siguen y qué hacer si uno falla.
---

# Procesos en segundo plano

Las tareas pesadas —sincronizar, importar, exportar, acciones masivas— no se ejecutan en el momento:
la plataforma crea un **proceso** y sigue trabajando. Usted puede seguir operando mientras corre.

## Estados

| Estado | Significa |
|---|---|
| ⏳ **Pendiente** | En cola, todavía no arrancó. |
| 🔄 **En proceso** | Ejecutándose. |
| ✅ **Completado** | Terminó y todos los registros salieron bien. |
| ⚠️ **Completado con errores** | Terminó, pero algunos registros fallaron. Hay detalle. |
| ❌ **Error** | No pudo ejecutarse. |

{% hint style="warning" %}
⚠️ **Completado con errores** es el estado que más se pasa por alto. El proceso figura terminado,
pero parte de sus registros no se aplicó. Ábralo y revise el detalle.
{% endhint %}

## Dónde se siguen

En [Gestión masiva](../operativa/cargas-masivas.md) están todos los procesos, con su origen, quién
los lanzó y el resultado. Cada uno abre el detalle registro por registro.

{% hint style="info" %}
📸 **Captura pendiente — `comunes-procesos-01`** · PNG

Listado de Gestión masiva con procesos en distintos estados (al menos uno completado con errores).
Resaltar la columna de estado.
{% endhint %}

## Si algo falla

1. Abra el proceso y lea el detalle: dice **qué registro** y **por qué**.
2. Los errores más comunes son de datos: un SKU que no existe, un valor de atributo que el canal no
   acepta, un campo obligatorio vacío.
3. Corrija el origen y vuelva a lanzarlo. Reintentar sin corregir da el mismo resultado.

{% hint style="info" %}
💡 Si fallan **todos** los registros con el mismo mensaje, no es un problema de datos: mire el
conector. Ver [Conectores](../operativa/conectores.md).
{% endhint %}
