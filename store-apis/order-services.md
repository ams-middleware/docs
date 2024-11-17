# Order Services

Este servicio ofrece una amplia gama de APIs especializadas en la creación y gestión eficiente de órdenes generadas para una tienda específica. La plataforma implementa un robusto sistema de seguridad basado en tokens JWT (JSON Web Tokens), garantizando la autenticación y autorización segura de cada transacción. Para acceder y utilizar estas APIs, es necesario haber contratado previamente los servicios de MW, lo cual asegura una integración completa y personalizada con nuestra plataforma.

{% hint style="info" %}
Requiere de Access token
{% endhint %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/search" method="post" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/search" method="get" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/standard" method="post" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/standard/{uid}" method="put" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/{connector_uid}/webhook" method="post" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/{uid}" method="get" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}

{% swagger src="https://store-api.e-middleware.ar/docs.json" path="/v3/order/{uid}/reserve" method="get" %}
[https://store-api.e-middleware.ar/docs.json](https://store-api.e-middleware.ar/docs.json)
{% endswagger %}
