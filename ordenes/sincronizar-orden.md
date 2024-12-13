---
icon: arrows-rotate-reverse
---

# Sincronizar Orden

A través de la plataforma de e-Middleware, el usuario tiene la capacidad de sincronizar una orden desde la plataforma externa utilizando el código de referencia (ref code) que esta genera.

En el listado de órdenes tenemos la opción de sincronizar en la botonera que está situada a la derecha. Se mostrará un modal al hacerr clic en el botón de más opciones, donde deberá de seleccionar un conector y el ref code de la orden que desea sincronizar.

<figure><img src="../.gitbook/assets/Peek 2024-12-02 10-43.gif" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Esta opción solo se debe utilizar en casos especiales donde la orden deba de actualizarse o  ingresar a e-Middleware  por falta de pago.
{% endhint %}

### ¿Cómo obtener el ref code desde Magento?

Buscaremos la orden a sincronizar y visualizaremos su detalle. En la URL de la orden encontraremos el ref code que necesitaremos para sincronizar la orden.

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

### ¿Cómo obtener el ref code desde Salesforce?

En el listado de órdenes en Salesforce buscaremos la orden a sincronizar. Desde el detalle de la misma obtendremos el ref code.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>



