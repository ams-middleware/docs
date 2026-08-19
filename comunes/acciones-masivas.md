---
description: Aplicar la misma acción sobre muchos registros a la vez.
---

# Selección múltiple y acciones masivas

Marque los registros con la casilla de la izquierda. La casilla del encabezado selecciona **toda la
página**. Al haber algo seleccionado, el toolbar cambia y muestra las acciones disponibles.

{% hint style="info" %}
📸 **Captura pendiente — `comunes-masivas-01`** · GIF (8 s)

Listado de Productos: marcar 3 filas, mostrar cómo cambia el toolbar superior con el contador de
seleccionados y abrir el menú de acciones masivas.
{% endhint %}

## Cómo se usa

1. Filtre el listado hasta dejar solo lo que quiere tocar. Ver
   [Filtrado avanzado](filtrado-avanzado.md).
2. Seleccione los registros.
3. Elija la acción en el toolbar.
4. Confirme. La acción se ejecuta **en segundo plano**: el listado no se queda esperando.

{% hint style="warning" %}
⚠️ La casilla del encabezado marca **la página actual**, no el resultado completo del filtro. Si
quiere alcanzar más registros, suba la cantidad por página o use
[Gestión masiva](../operativa/cargas-masivas.md).
{% endhint %}

## Dónde ver el resultado

Las acciones masivas generan un **proceso**. Ahí se ve cuántos registros salieron bien, cuántos
fallaron y por qué. Ver [Procesos en segundo plano](procesos.md).

{% hint style="danger" %}
🛑 Una acción masiva sobre productos publicados **impacta en los canales de venta**: cambios de
precio, de stock o bajas se propagan. Verifique la selección antes de confirmar.
{% endhint %}
