---
description: Las diez palabras que se usan todo el tiempo en la plataforma.
---

# Glosario

| Término | Qué es |
|---|---|
| **Orden** | Una compra. Trae los productos, el pago y los datos de envío del comprador. |
| **Tienda** | Su unidad de negocio dentro de la plataforma. Todo lo que ve pertenece a la tienda activa. |
| **Integración** | El tipo de plataforma con la que se conecta: VTEX, Magento, Mercado Libre, Tienda Nube… |
| **Conector** | La conexión concreta con **una** tienda de esa plataforma, con sus credenciales y sus reglas. Puede tener varios conectores de la misma integración. |
| **Canal** | Coloquialmente, el destino donde se publica o desde donde entra una venta. En la práctica, un conector. |
| **SKU** | El código que identifica a un producto de forma única. Es la llave con la que se cruzan los canales. |
| **Producto base** | El producto "padre", con la información común. Agrupa variantes. |
| **Producto simple** | La unidad que se vende y se le sigue el stock: un talle y color concretos. |
| **Atributo** | Una característica del producto (color, talle, material). Cada canal la puede llamar distinto. |
| **Mapeo** | La traducción entre lo que usted carga y lo que el canal espera. Ver [Mapeos de categoría](../operativa/mapeo-de-categorias.md). |
| **Workflow** | El circuito por el que pasa una orden desde que entra hasta que se completa. |
| **Proceso** | Una tarea que corre en segundo plano: una sincronización, una carga masiva, una exportación. |

{% hint style="info" %}
💡 **Integración vs. conector**, que es la confusión más común: la integración es *"Mercado Libre"*;
el conector es *"mi cuenta de Mercado Libre Argentina"*. Si vende en dos cuentas de Mercado Libre,
tiene una integración y dos conectores.
{% endhint %}
