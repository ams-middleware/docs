---
icon: xmark-large
---

# Orden de Cancelación

El botón de cancelación solo estará habilitado para las órdenes tipo Estándar que se encuentren en estado "Completado" y que cumplan con los siguientes requisitos adicionales:&#x20;

* **No debe estar vinculada** a ninguna otra orden de:
  * **Devolución**
  * **Cambio**
  * **Versionado**

#### **Procedimiento para Cancelar una Orden**

Siga estos pasos para realizar la cancelación de una orden que cumpla con los requisitos.

**Paso 1: Acceder a la Orden**

1. Diríjase al Listado de Órdenes.
2. Utilice los filtros o la búsqueda para localizar la orden standar que desea cancelar.
3. Seleccione la orden haciendo clic sobre ella para abrir su detalle.

**Paso 2: Iniciar el Cambio de Estado**

1. Dentro de la interfaz de detalle de la orden, ubique y presione el botón **"Cambiar Status"**.

**Paso 3: Ejecutar la Cancelación en el Modal**

1. Se desplegará una ventana emergente (modal).
2. En el campo **"Seleccionar status"**, elija la opción **"Cancelar"** de la lista desplegable.
3. Selecciona el check "Crear orden de cancelación" para generar la orden de cancelación; de lo contrario, la orden estándar pasará a cancelada.
4. En el campo **"Observación"**, ingrese una justificación o motivo para la cancelación.&#x20;
5. Para finalizar, haga clic en el botón **"Aplicar"**.

**Resultado de la Cancelación**

Una vez que se presione **"Aplicar"**, el sistema realizará automáticamente lo siguiente:

* Se creará una nueva orden tipo **"cancel"** identificada con el prefijo **X1**
* En la orden original, los siguientes botones se deshabilitarán:
  * Cambio de status
  * Editar
  * Reservar stock
  * Versionar
  * Cambio
  * Devolución

<figure><img src="../.gitbook/assets/Logo indumentaria mujer circular simple negro (7).png" alt=""><figcaption></figcaption></figure>

NOTA:VIDEO DEMOSTRATIVO DE PASOS A SEGUIR PARA CANCELAR UNA ORDEN
