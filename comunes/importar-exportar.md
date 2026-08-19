---
description: Sacar datos a un archivo y cargarlos desde uno.
---

# Importar y exportar

## Exportar

1. Deje el listado con el filtro que quiere llevarse.
2. **Exportar**, en el toolbar.
3. Se genera un proceso; cuando termina, el archivo queda disponible para descargar.

{% hint style="info" %}
💡 Se exporta **todo lo filtrado**, no solo la página que está viendo. Si necesita el catálogo
completo, exporte sin filtros.
{% endhint %}

{% hint style="info" %}
📸 **Captura pendiente — `comunes-exportar-01`** · GIF (8 s)

Desde un listado de Productos: abrir Exportar, elegir columnas si la pantalla lo ofrece, confirmar y
mostrar el aviso de que el proceso arrancó.
{% endhint %}

## Importar

1. **Descargue primero la plantilla** desde la misma pantalla de importación.
2. Complete el archivo respetando los encabezados. No agregue, borre ni renombre columnas.
3. Súbalo y confirme.
4. Revise el resultado del proceso: la plataforma informa fila por fila qué se cargó y qué se rechazó.

{% hint style="warning" %}
⚠️ La columna que identifica al registro —normalmente el **SKU**— es la que decide si se **crea** uno
nuevo o se **actualiza** el existente. Un SKU mal escrito no da error: crea un producto duplicado.
{% endhint %}

{% hint style="danger" %}
🛑 Una importación puede modificar miles de registros de una vez y **no tiene deshacer**. Pruebe
siempre con un archivo de 3 o 4 filas antes de subir el archivo completo.
{% endhint %}

## Formato

| | |
|---|---|
| Formatos | Excel (`.xlsx`) y CSV |
| Codificación | UTF-8. Si ve caracteres raros en los acentos, el archivo se guardó en otra codificación. |
| Decimales | Punto como separador decimal. Sin separador de miles. |
| Fechas | `AAAA-MM-DD` |

El detalle de cada tipo de carga y el seguimiento de los archivos está en
[Gestión masiva](../operativa/cargas-masivas.md).
