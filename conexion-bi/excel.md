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
**Apunte a la raíz `/odata`, no a `/odata/orders`.** Excel necesita la raíz del servicio para reconocerlo y descubrir los feeds; la línea `orders = Origen{[Name="orders",…]}` selecciona el de órdenes.
{% endhint %}

{% hint style="warning" %}
El formato del token suele ser `Bearer <su-token>`. Si la conexión es rechazada, confirme el formato exacto con [soporte](README.md#necesita-ayuda).
{% endhint %}

***

### 3. Elegir credencial: **Anónimo**

La primera vez, Excel muestra **"Se requieren credenciales para conectarse al origen OData"**. Es esperado: Excel gestiona un permiso propio por origen, aparte del token.

* Haga clic en **Editar credenciales** → pestaña **Anónimo** (*Anonymous*) → **Conectar**.

{% hint style="info" %}
Se elige **Anónimo a propósito**: su autenticación real viaja en el header `Authorization` que ya está en la consulta. Excel no agrega ninguna credencial; solo necesita que confirme el nivel. Se configura **una sola vez** por origen.
{% endhint %}

***

### 4. Cargar los datos a la hoja

* Verá una vista previa de sus órdenes. Las columnas **anidadas** (envío, facturación, ítems…) aparecen como `Record`/`List`: expándalas con el botón **⇲** del encabezado para volcar sus subcampos como columnas.
* _(Opcional)_ Quite o transforme columnas desde el editor.
* Haga clic en **Cerrar y cargar** para volcar los datos en una hoja de cálculo (o en el **Modelo de datos** si prefiere usar tablas dinámicas).

{% hint style="info" %}
Si aparece *"demasiado complejo para mostrarse"* en la vista previa, no es un error: es por los datos anidados. Los datos se cargan igual con **Cerrar y cargar**.
{% endhint %}

***

### 5. Actualizar los datos

* Para traer la información más reciente: pestaña **Datos → Actualizar todo**.
* _(Opcional)_ En **Datos → Consultas y conexiones**, puede configurar la actualización **automática** al abrir el archivo o cada cierto intervalo.

***

### Problemas frecuentes

| Síntoma | Posible causa / solución |
|---------|--------------------------|
| **"Se requieren credenciales para conectarse al origen OData"** | Pedido normal de credencial (aparte del token). **Editar credenciales → Anónimo → Conectar** (ver paso 3). |
| **"La URL no señala a un servicio OData"** | Está apuntando a un feed (`/odata/orders`) en vez de a la **raíz** (`/odata`). Use la raíz; el feed lo selecciona la línea `orders = Origen{…}`. |
| **Error 401 / no autorizado** | Token vencido, mal copiado o con formato incorrecto. Verifique el token y el prefijo `Bearer`. |
| **No aparece "Obtener datos"** | Su versión de Excel es anterior a 2016 o no tiene Power Query. Actualice Excel. |
| **"Demasiado complejo para mostrarse"** | No es un error: es la vista previa con datos anidados. Haga **Cerrar y cargar**; los datos entran igual. |
| **Tabla vacía** | Su cuenta no tiene órdenes en el período consultado. |
