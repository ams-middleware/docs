---
description: Toda la información de una orden y las acciones que puede ejecutar.
---

# Detalle de la orden

Un clic sobre la fila abre el detalle.

{% hint style="info" %}
📸 **Captura pendiente — `ord-detalle-01`** · PNG

Detalle de una orden con las pestañas visibles y el toolbar de acciones arriba. Tapar los datos
personales del comprador.
{% endhint %}

## Las pestañas

| Pestaña | Qué trae |
|---|---|
| **Detalles** | Resumen general de la orden. |
| **Cliente** | Datos del comprador. |
| **Pago** | Método, estado de la transacción y montos. |
| **Envío** | Dirección, método y seguimiento. |
| **Productos** | Ítems, cantidades y precios. |
| **Workflow** | Por qué etapa va y qué pasó en cada una. |
| **Conector** | De qué canal vino y qué se intercambió con él. |

{% hint style="info" %}
💡 La pestaña **Workflow** es la primera que hay que mirar cuando una orden "no avanza": muestra en
qué etapa quedó trabada y con qué error.
{% endhint %}

## Acciones

| Acción | Para qué |
|---|---|
| **Editar** | Corregir datos de la orden. |
| **Procesar** | Empujar la orden a la siguiente etapa. |
| **Cambiar estado** | Forzar el estado a mano. Ver [Estados](estados.md). |
| **Cambio** / **Devolución** | Abrir un caso de postventa. Ver [Postventa](postventa.md). |
| **Versionar** | Generar una versión nueva de una orden ya completada. |
| **Liberar stock** | Soltar la reserva de inventario. |
| **Normalizar** | Reordenar los datos al formato estándar cuando el canal los mandó raros. |
| **Traer del canal** | Volver a pedir la orden al canal de origen. |

{% hint style="warning" %}
⚠️ **Liberar stock** devuelve las unidades al disponible y eso se propaga a los canales. Úselo solo
si está seguro de que la venta no se concreta.
{% endhint %}

## Versionar

Genera una orden nueva a partir de una **completada**, sin volver a cargarla. Sirve típicamente
cuando hay que rehacer una venta.

1. Abra la orden completada y elija **Versionar**.
2. Decida si la orden anterior se **cancela** o queda como está.
3. Confirme.

{% hint style="warning" %}
⚠️ Solo se versionan órdenes en estado **Completada**, y aplica a los tres tipos: estándar, cambio y
devolución.
{% endhint %}
