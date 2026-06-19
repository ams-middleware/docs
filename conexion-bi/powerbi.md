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
        "https://api.e-middleware.ar/odata/Orders",
        [Authorization = "Bearer " & "TU_TOKEN"],
        [Implementation = "2.0"]
    )
in
    Origen
```

* Haga clic en **Listo**.

{% hint style="warning" %}
El formato del token suele ser `Bearer <su-token>`. Si la conexión es rechazada, confirme el formato exacto con [soporte](README.md#necesita-ayuda).
{% endhint %}

***

### 3. Configurar privacidad (si lo solicita)

Si Power BI pregunta por el **nivel de privacidad** de la fuente, seleccione **Organizational** (u **Organizativo**) y continúe.

***

### 4. Cargar los datos

* Verá una vista previa de sus órdenes en columnas.
* _(Opcional)_ Quite o transforme columnas que no necesite desde el editor.
* Haga clic en **Cerrar y aplicar**.

Sus órdenes ya están en Power BI, listas para construir tableros.

***

### 5. Refrescar y mantener actualizado

* Para traer los datos más recientes: pestaña **Inicio → Actualizar**.
* Para **automatizar** el refresco, publique el informe en **Power BI Service** y configure una **actualización programada** (allí se guardan sus credenciales de forma segura).

{% hint style="success" %}
**Refresco incremental (datasets grandes):** puede configurar Power BI para que filtre por fecha (`created_at`) y traiga solo lo nuevo o modificado en cada actualización, en lugar de todo el histórico. Esto hace los refrescos mucho más rápidos.
{% endhint %}

***

### Problemas frecuentes

| Síntoma | Posible causa / solución |
|---------|--------------------------|
| **Error 401 / no autorizado** | Token vencido, mal copiado o con formato incorrecto. Verifique el token y el prefijo `Bearer`. |
| **No trae datos / tabla vacía** | Su cuenta no tiene órdenes en el período, o el filtro aplicado es muy restrictivo. |
| **La actualización tarda mucho** | Active el **refresco incremental** por fecha (ver paso 5). |
