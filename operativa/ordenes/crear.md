---
description: Cargar a mano una venta que no vino de un canal.
---

# Crear una orden

Sirve para ventas por teléfono, mostrador o WhatsApp. Las ventas de los canales conectados **no** se
cargan a mano: entran solas.

## Pasos

1. **Nueva orden** en el toolbar del listado.
2. **Comprador** — búsquelo por documento o correo. Si no existe, créelo desde el mismo formulario.
3. **Productos** — busque por SKU o nombre y ajuste cantidades.
4. **Envío** — dirección y método. El costo puede calcularse solo según las reglas de su operación.
5. **Pago** — método y estado.
6. **Guardar**.

{% hint style="info" %}
📸 **Captura pendiente — `ord-crear-01`** · GIF (12 s)

Recorrer el alta completa: buscar comprador, agregar dos productos, elegir envío y guardar. Usar
datos ficticios.
{% endhint %}

{% hint style="warning" %}
⚠️ Los productos se agregan por **SKU**. Si el SKU no aparece en la búsqueda, el producto no existe o
está inactivo en la tienda con la que está trabajando: revíselo en
[Productos](../productos.md) antes de seguir.
{% endhint %}

{% hint style="info" %}
💡 Antes de guardar, confirme la **tienda activa** en la barra superior. La orden queda asociada a
ella y eso no se cambia después.
{% endhint %}

## Qué pasa al guardar

La orden arranca su circuito: reserva el stock y entra al
[workflow](../../configuracion/workflows.md) configurado. A partir de ahí se sigue como cualquier
otra desde [el detalle](detalle.md).
