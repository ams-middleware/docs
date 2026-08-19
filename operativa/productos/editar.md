---
description: Alta y modificación de un producto.
---

# Crear y editar un producto

1. **Nuevo producto** en el toolbar.
2. **Información general** — nombre, descripción, marca y **SKU**.
3. **Categoría** — define qué atributos le va a pedir el formulario.
4. **Atributos** — complete los que correspondan a esa categoría.
5. **Multimedia** — sume las imágenes. Ver [Multimedia](../multimedia.md).
6. Guarde.

{% hint style="info" %}
📸 **Captura pendiente — `prod-editar-01`** · GIF (12 s)

Alta completa de un producto simple: datos generales, elegir categoría (mostrando cómo cambian los
atributos disponibles), completar atributos y guardar.
{% endhint %}

{% hint style="danger" %}
🛑 El **SKU** es la llave del producto en todos los canales. Una vez publicado, cambiarlo rompe la
relación con las publicaciones existentes y puede duplicar el producto en el canal. Elíjalo bien de
entrada.
{% endhint %}

## La categoría manda

Los atributos que ve en el formulario **dependen de la categoría** elegida. Si le falta un campo,
casi siempre es porque el producto está en la categoría equivocada.

{% hint style="warning" %}
⚠️ Cambiar la categoría de un producto ya cargado puede dejar atributos huérfanos: los valores que ya
no participan en la categoría nueva dejan de enviarse a los canales.
{% endhint %}

## Duplicar

Para cargar productos parecidos, use **Duplicar** en las
[acciones de la fila](../../comunes/acciones-fila.md): copia todo salvo el SKU, que debe ser único.

{% hint style="info" %}
💡 ¿Está cargando más de diez productos parecidos? Conviene
[importar por archivo](../../comunes/importar-exportar.md).
{% endhint %}
