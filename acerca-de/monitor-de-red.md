# Monitor de conexión

El **monitor de conexión** es el punto de color que aparece en la barra inferior (footer), a la
derecha. Sirve para responder una sola pregunta cuando el sistema se siente lento:

> **¿El problema es del sistema, o no?**

En lugar de adivinar, el monitor lo mide y te lo dice.

## El semáforo

El color del punto resume el estado del servicio en ese momento:

| Color | Significa |
|-------|-----------|
| 🟢 Verde | Todo bien: el servidor responde con normalidad. |
| 🟡 Amarillo | El servidor está lento, pero seguís pudiendo trabajar. |
| 🔴 Rojo | El servidor no responde o tarda demasiado. |

Si además hay algún servicio caído, el footer lo avisa directamente con un texto
("N servicio(s) con problemas").

## El detalle

Al hacer clic se abre un panel con el diagnóstico. Arriba vas a ver una **frase-veredicto** que te
dice directamente a quién atribuir la lentitud, y debajo los indicadores que la componen:

| Indicador | Qué mide |
|-----------|----------|
| **Recorrido al servidor** | La distancia y la ruta entre vos y el servidor. |
| **Servidor** | El tiempo que tarda el servidor en procesar y responder. |
| **Servicios** | Si cada servicio del sistema está respondiendo, y en cuánto tiempo. |

{% hint style="info" %}
Un valor alto en **Recorrido al servidor** normalmente significa que el servidor está lejos
geográficamente —no que algo esté roto—, por eso se muestra en gris y nunca prende la alarma. Un
valor alto en **Servidor** sí indica que el problema es del lado del sistema.
{% endhint %}

## Reportar un problema

Si el sistema te resulta lento y querés que soporte lo revise:

1. Hacé clic en el monitor de conexión, en la barra inferior.
2. Presioná **Copiar**.
3. Pegá ese texto en tu mensaje a soporte (o adjuntá una captura del panel).

Ese diagnóstico le da a nuestro equipo la información exacta para saber dónde está el cuello de
botella sin tener que pedirte más datos.

{% hint style="success" %}
Con ese reporte podemos distinguir en segundos si el problema es nuestro —y ahorrarte idas y
vueltas—.
{% endhint %}
