---
description: Automatizar acciones cuando se cumple una condición.
---

# Reglas

Una regla es un **si pasa esto, hacé aquello**: si la orden supera cierto monto, marcarla para
revisión; si viene de tal canal, asignarle un depósito.

## Armar una regla

1. Entre a **Sistema → Reglas** → **Nueva regla**.
2. **Condición** — qué tiene que cumplirse.
3. **Acción** — qué hacer cuando se cumple.
4. Guarde y **actívela**.

{% hint style="info" %}
📸 **Captura pendiente — `conf-reglas-01`** · GIF (10 s)

Crear una regla simple: elegir condición, elegir acción, guardar y mostrarla activa en el listado.
{% endhint %}

{% hint style="info" %}
💡 Deje la regla **inactiva** mientras la arma y actívela recién cuando esté completa. Una regla a
medias puede empezar a actuar sobre órdenes reales.
{% endhint %}

{% hint style="warning" %}
⚠️ Si tiene varias reglas que aplican al mismo caso, se ejecutan **todas**. Revise que no se pisen
entre sí antes de sumar una nueva.
{% endhint %}

{% hint style="danger" %}
🛑 Una regla mal armada actúa sobre **todas** las órdenes que cumplan la condición, en silencio y sin
confirmación. Después de activarla, mire las órdenes de la hora siguiente para confirmar que hace lo
que esperaba.
{% endhint %}
