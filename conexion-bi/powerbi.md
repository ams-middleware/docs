# Conectar con Power BI

Esta guía explica cómo conectar **Power BI Desktop** a sus órdenes a través de la API pública.

{% hint style="info" %}
Antes de empezar, revise los [requisitos previos](README.md#requisitos-previos): necesita su **token de acceso** y la **URL del feed**.
{% endhint %}

***

### 1. Abrir el conector de datos

* Abra **Power BI Desktop**.
* En la pestaña **Inicio**, haga clic en **Obtener datos → Consulta en blanco**.

> Usamos una *consulta en blanco* porque nos permite enviar su token de forma segura en el encabezado de autorización.

***

### 2. Pegar la consulta con su token

* Se abre el **Editor de Power Query**. Haga clic en **Editor avanzado**.
* Borre el contenido y pegue lo siguiente, **reemplazando `TU_TOKEN`** por su token:

```text
let
    Origen = OData.Feed(
        "https://api.e-middleware.ar/odata",
        [Authorization = "Bearer " & "TU_TOKEN"],
        [Implementation = "2.0"]
    ),
    orders = Origen{[Name = "orders", Signature = "table"]}[Data]
in
    orders
```

* Haga clic en **Listo**.

{% hint style="warning" %}
**Apunte a la raíz `/odata`, no a `/odata/orders`.** Power BI necesita la raíz del servicio para descubrir los feeds; si apunta directo a un feed da el error *"la dirección URL especificada no señala a un servicio OData"*. La línea `orders = Origen{[Name="orders",…]}` selecciona el feed de órdenes una vez descubierto el servicio.
{% endhint %}

{% hint style="warning" %}
El formato del token suele ser `Bearer <su-token>`. Si la conexión es rechazada, confirme el formato exacto con [soporte](README.md#necesita-ayuda).
{% endhint %}

***

### 3. Elegir credencial: **Anónimo**

La primera vez que se conecta, Power BI muestra **"Se requieren credenciales para conectarse al origen OData"**. Esto es esperado: Power BI gestiona un permiso propio por origen, **aparte** del token.

* Haga clic en **Editar credenciales**.
* Elija la pestaña **Anónimo** (*Anonymous*).
* Deje el nivel en la URL del origen (`https://api.e-middleware.ar/odata`) y haga clic en **Conectar**.

{% hint style="info" %}
Se elige **Anónimo a propósito**: su autenticación real viaja en el header `Authorization` que ya está en la consulta. Power BI solo necesita que confirme el nivel; no agrega ninguna credencial adicional. Lo configura **una sola vez** por origen.
{% endhint %}

***

### 4. Configurar privacidad (si lo solicita)

Si Power BI pregunta por el **nivel de privacidad** de la fuente, seleccione **Organizational** (u **Organizativo**) y continúe.

***

### 5. Cargar los datos

* Verá una vista previa de sus órdenes en columnas. Las columnas **anidadas** (envío, facturación, ítems, pagos…) aparecen como **`Record`** (un objeto) o **`List`** (una lista).
* _(Opcional)_ Quite o transforme columnas que no necesite desde el editor.
* Haga clic en **Cerrar y aplicar**.

Sus órdenes ya están en Power BI, listas para construir tableros.

{% hint style="info" %}
**Si ve el mensaje "El valor de vista previa actual es demasiado complejo para mostrarse" (*too complex to display*):** no es un error. Es solo que el panel de vista previa no puede dibujar la estructura anidada de las órdenes. Los datos **se cargan igual**: haga clic en **Cerrar y aplicar** y continúe.
{% endhint %}

***

### 6. Ver y expandir la información

Una vez cargados los datos, arme un informe para verlos:

1. En el panel **Datos** (derecha) verá la tabla **`orders`** con todos sus campos.
2. En **Visualizaciones**, elija el ícono de **Tabla**. Tilde los campos que quiera ver (`ref_code`, `status`, `type`, `grand_total`, `created_at`, `store_uid`…) y aparecerán como columnas. Así ve sus órdenes fila por fila.

**Para ver los datos anidados** (envío, facturación, ítems…), que llegan como `Record`/`List`:

* Vaya a **Inicio → Transformar datos** (Editor de Power Query).
* En la columna anidada, haga clic en el botón **⇲** (expandir) del encabezado y elija los subcampos. Por ejemplo: `shipping` → ciudad, provincia; `items` → se despliega en una fila por ítem con su precio y cantidad.
* **Cerrar y aplicar.** Esos subcampos quedan como columnas planas, listas para usar.

***

### 7. Refrescar y mantener actualizado

* Para traer los datos más recientes: pestaña **Inicio → Actualizar**.
* Para **automatizar** el refresco, publique el informe en **Power BI Service** y configure una **actualización programada** (allí se guardan sus credenciales de forma segura). En *Configuración del modelo semántico → Credenciales del origen de datos*, fije el origen también en **Anónimo** (igual que en el paso 3), o el refresco fallará.

{% hint style="success" %}
**Refresco incremental (datasets grandes):** puede configurar Power BI para que filtre por fecha (`created_at`) y traiga solo lo nuevo o modificado en cada actualización, en lugar de todo el histórico. Esto hace los refrescos mucho más rápidos.
{% endhint %}

{% hint style="warning" %}
**La primera carga puede tardar varios minutos.** Si tiene muchas órdenes (decenas de miles), Power BI las trae todas, página por página, con su estructura completa. Es normal que demore en la **primera** importación; una vez cargado, el informe responde al instante. Para acotarlo, filtre por fecha o use el refresco incremental. Mientras carga, Power BI muestra *"Creando…"* / *"Esperando para abrir el editor"*: está armando el modelo, no está colgado.
{% endhint %}

***

### Problemas frecuentes

| Síntoma | Posible causa / solución |
|---------|--------------------------|
| **"Se requieren credenciales para conectarse al origen OData"** | Es el pedido normal de credencial de Power BI (aparte del token). **Editar credenciales → Anónimo → Conectar** (ver paso 3). El token ya va en el header del script. |
| **"La URL no señala a un servicio OData"** | Está apuntando a un feed (`/odata/orders`) en vez de a la **raíz** (`/odata`). Use la raíz; la selección del feed la hace la línea `orders = Origen{…}` del script. |
| **Error 401 / no autorizado** | Token vencido, mal copiado o con formato incorrecto. Verifique el token y el prefijo `Bearer`. |
| **"Demasiado complejo para mostrarse"** | No es un error: es solo la vista previa con datos anidados. Haga **Cerrar y aplicar**; los datos se cargan igual. |
| **No trae datos / tabla vacía** | Su cuenta no tiene órdenes en el período, o el filtro aplicado es muy restrictivo. |
| **La actualización tarda mucho** | Active el **refresco incremental** por fecha (ver paso 7) o filtre el rango de fechas. |
