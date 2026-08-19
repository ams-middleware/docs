---
description: Ver, editar, duplicar o eliminar un registro desde el listado.
---

# Acciones sobre una fila

Cada fila tiene sus acciones al final, a la derecha. Cuáles aparecen depende del módulo y de sus
permisos.

| Acción | Qué hace |
|---|---|
| 👁️ **Ver** | Abre el detalle sin permitir cambios. |
| ✏️ **Editar** | Abre el formulario del registro. |
| 📄 **Duplicar** | Crea una copia para no cargar todo de nuevo. Disponible en Productos. |
| 🗑️ **Eliminar** | Borra el registro. |

{% hint style="info" %}
💡 Un clic sobre la fila entra al detalle. No hace falta buscar el botón.
{% endhint %}

## Eliminar es de dos pasos

En los listados, eliminar **no abre una ventana de confirmación**. Funciona así:

1. Presione 🗑️. El botón cambia y pide confirmación **en la misma fila**.
2. Vuelva a presionar para confirmar. Si no confirma en unos segundos, se cancela solo.

{% hint style="info" %}
📸 **Captura pendiente — `comunes-eliminar-01`** · GIF (5 s)

Mostrar el borrado de dos pasos en una fila de un listado: primer clic en el ícono, el botón
cambiando a confirmación, y el segundo clic. Usar un registro de prueba.
{% endhint %}

{% hint style="danger" %}
🛑 Eliminar no se deshace. En Productos y Órdenes, además, el registro puede estar publicado en un
canal: si duda, use el estado **Inactivo** en lugar de borrar.
{% endhint %}

## No veo una acción

Si una acción no aparece, es por una de dos razones:

- **Su rol no tiene el permiso.** Pídaselo al administrador de su empresa.
- **El registro no lo admite en ese estado.** Una orden completada, por ejemplo, ya no se edita.
