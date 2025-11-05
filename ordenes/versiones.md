---
description: Proceso de Versionado de Órdenes
---

# 🧾 Versiones

**Requisitos Previos**

* El usuario solo podrá versionar una orden si esta se encuentra en estado "completada".
* Se pueden versionar los tres tipos de órdenes: Estándar, Cambio y Devolución.

### Pasos para Versionar una Orden

1. **Acceder a la Orden**
   * Desde el listado de órdenes, localiza la orden que deseas versionar.
   * Haz clic en el botón **"Visualizar"**.
2. **Interacción con el Modal**
   * Se abrirá un modal con las siguientes opciones:
     * **Opción para cancelar la orden anterior**.
     * **Opción para versionar la orden sin cancelar la anterior**.
     * Dos botones disponibles: **"Aplicar"** o **"Cerrar"**.

***

### Versionar Orden Estándar

{% hint style="info" %}
No se puede versionar una Orden Standar si tiene órdenes relacionadas (cambio o devolución).
{% endhint %}

* Al hacer clic en **"Aplicar"**:
  * La orden estándar se versionará automáticamente.
  * El UID cambiará de **S1 a S2**.
  * El estado cambiará de **Pendiente** a **Completado**.
  * Se ofrecerá la opción de editar el versionado de la orden.

#### Versionar Orden de Cambio

* Al hacer clic en **"Aplicar"**:
  * La orden de cambio se versionará automáticamente.
  * El UID cambiará de **C1 a C2**.
  * El estado cambiará de **Pendiente** a **Completado**.
  * Se ofrecerá la opción de editar el versionado de la orden.

***

#### Versionar Orden de Devolución

* Al hacer clic en **"Aplicar"**:
  * La orden de devolución se versionará automáticamente.
  * El UID cambiará de **R1 a R2**.
  * El estado cambiará de  completado a pendiente.
  * Se ofrecerá la opción de editar el versionado de la orden.

***

<figure><img src="../.gitbook/assets/Logo indumentaria mujer circular simple negro (11).png" alt=""><figcaption></figcaption></figure>

NOTA: VIDEO DEMOSTRATIVO DEL PASO A PASO PARA VERSIONAR UNA ORDEN
