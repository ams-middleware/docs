---
description: Mandar un producto a una tienda o marketplace y entender qué pasó.
---

# Publicar en un canal

Publicar es enviar el producto a un canal para que se ponga a la venta. Un producto puede estar en
varios canales a la vez, cada uno con sus reglas.

## Antes de publicar

La mayoría de los rechazos se evita con este checklist:

1. ✅ El producto tiene **categoría** y sus atributos obligatorios completos.
2. ✅ La categoría tiene su [mapeo](../mapeo-de-categorias.md) al canal.
3. ✅ Los valores de atributo tienen su [traducción](../atributos.md) para ese canal.
4. ✅ Tiene al menos una imagen. Ver [Multimedia](../multimedia.md).
5. ✅ Tiene stock y precio.

## Publicar

1. Abra el producto → pestaña de **conectores**, o selecciónelo en el listado.
2. Elija el canal.
3. **Sincronizar** / **Publicar**.

{% hint style="info" %}
📸 **Captura pendiente — `prod-publicar-01`** · GIF (10 s)

Desde el detalle de un producto: abrir la pestaña de conectores, elegir un canal y lanzar la
publicación. Mostrar el aviso de proceso iniciado.
{% endhint %}

La publicación **no es inmediata**: genera un proceso. El resultado —publicado, o rechazado y por
qué— se ve en [Procesos en segundo plano](../../comunes/procesos.md).

## Diferencias por canal

Un mismo producto puede necesitar otro título o otra foto en un marketplace. Eso se resuelve con
**valores específicos por conector**: lo que cargue ahí pisa al valor general, solo para ese canal.

{% hint style="info" %}
💡 Empiece siempre por el valor general. Use el específico por canal solo cuando el canal lo exija:
mantener diez variantes de la misma descripción se vuelve incontrolable.
{% endhint %}

## Rechazos frecuentes

| Mensaje del canal | Causa habitual |
|---|---|
| Categoría inexistente o inválida | Falta el [mapeo de categoría](../mapeo-de-categorias.md). |
| Atributo obligatorio faltante | El canal pide un atributo que su categoría no completa. |
| Valor no permitido | El valor no tiene [traducción](../atributos.md) para ese canal. |
| SKU duplicado | Ya existe una publicación con ese SKU en el canal. |

{% hint style="warning" %}
⚠️ **Despublicar no borra la publicación en el canal** en todas las plataformas. En algunos
marketplaces solo la pausa. Verifique en el canal si necesita que desaparezca.
{% endhint %}
