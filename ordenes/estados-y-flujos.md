---
description: >-
  En Middleware, cada orden pasa por diferentes estados que indican su progreso
  en el proceso de ejecución. A continuación, se describen los estados
  disponibles:
---

# 🔄 Estados y Flujos

**Estados Disponibles**

1. **Pending (Pendiente)**
   * La orden ha sido registrada y está en espera de iniciar su procesamiento.
2. **Complete (Completada)**
   * La orden ha sido procesada exitosamente y finalizó todas sus etapas.
   * **Nota:** Una orden en este estado no puede volver a **Pending** ni ser cancelada.
3. **Cancel (Cancelada)**
   * Permite anular una orden en cualquier momento antes de que alcance el estado **Complete**.
   * **Nota**: Una orden **cancelada** no puede volver a **Complete.**&#x20;

#### **Procedimiento para Cambiar el Estado**

1. **Cambiar Estado**
   * Dentro de la pantalla de detalle de la orden, ubique la opción **“Cambiar status”** en la parte superior.
   * Presione este botón para abrir el menú de estados.
2. **Seleccionar Nuevo Estado**
   * En la ventana emergente, elija el estado deseado:
     * **Pending (Pendiente)**
     * **Complete (Completado)**
     * **Cancel (Cancelar)**
   * Confirme la selección para actualizar el estado de la orden.

<figure><img src="../.gitbook/assets/07-01-2026_16-27-53 (1).gif" alt=""><figcaption></figcaption></figure>
