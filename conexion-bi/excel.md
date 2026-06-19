# Conectar con Excel

Esta guía explica cómo conectar **Microsoft Excel** a sus órdenes a través de la API pública. Requiere Excel **2016 o superior** (con *Obtener datos / Power Query*).

{% hint style="info" %}
Antes de empezar, revise los [requisitos previos](README.md#requisitos-previos): necesita su **token de acceso** y la **URL del feed**.
{% endhint %}

***

### 1. Abrir el conector de datos

* Vaya a la pestaña **Datos**.
* Haga clic en **Obtener datos → Desde otras fuentes → Consulta en blanco**.

> Usamos una *consulta en blanco* porque permite enviar su token de forma segura en el encabezado de autorización.

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

### 3. Cargar los datos a la hoja

* Verá una vista previa de sus órdenes.
* _(Opcional)_ Quite o transforme columnas desde el editor.
* Haga clic en **Cerrar y cargar** para volcar los datos en una hoja de cálculo (o en el **Modelo de datos** si prefiere usar tablas dinámicas).

***

### 4. Actualizar los datos

* Para traer la información más reciente: pestaña **Datos → Actualizar todo**.
* _(Opcional)_ En **Datos → Consultas y conexiones**, puede configurar la actualización **automática** al abrir el archivo o cada cierto intervalo.

***

### Problemas frecuentes

| Síntoma | Posible causa / solución |
|---------|--------------------------|
| **Error 401 / no autorizado** | Token vencido, mal copiado o con formato incorrecto. Verifique el token y el prefijo `Bearer`. |
| **No aparece "Obtener datos"** | Su versión de Excel es anterior a 2016 o no tiene Power Query. Actualice Excel. |
| **Tabla vacía** | Su cuenta no tiene órdenes en el período consultado. |
