---
icon: plug
description: La conexión con cada tienda o marketplace.
---

# 🔌 Conectores

Un **conector** es la conexión con una tienda concreta: sus credenciales, qué se sincroniza y cada
cuánto. Si vende en dos cuentas del mismo marketplace, son dos conectores.

{% hint style="info" %}
📸 **Captura pendiente — `conect-listado-01`** · PNG

Listado de Conectores con varios canales y su estado (activo / con error). Tapar credenciales.
{% endhint %}

## Qué se ve de cada uno

| | |
|---|---|
| **Estado** | Si está activo y si la última conexión funcionó. |
| **Qué sincroniza** | Órdenes, stock, precios, catálogo: cada cosa se habilita por separado. |
| **Frecuencia** | Cada cuánto corre cada sincronización. |
| **Última ejecución** | Cuándo fue y con qué resultado. |

## Probar la conexión

Antes de dar por sentado que un canal anda, use la prueba de conexión del conector: valida las
credenciales sin mover datos.

{% hint style="info" %}
💡 Cuando **todas** las órdenes o publicaciones de un canal fallan al mismo tiempo, el problema es el
conector, no los datos. Empiece siempre por acá.
{% endhint %}

{% hint style="warning" %}
⚠️ Las credenciales de los marketplaces **caducan**. Un conector que funcionó meses puede empezar a
fallar sin que usted haya tocado nada: hay que reautorizarlo.
{% endhint %}

{% hint style="danger" %}
🛑 Desactivar un conector **corta la entrada de órdenes de ese canal**. Las ventas siguen ocurriendo
allá y no llegan acá. Desactive solo si sabe lo que está haciendo, y por poco tiempo.
{% endhint %}

## Sincronizaciones

Cada conector corre sus tareas según su frecuencia. También se pueden lanzar a mano desde el producto
o desde la orden. Todo queda registrado en
[Procesos en segundo plano](../comunes/procesos.md).
