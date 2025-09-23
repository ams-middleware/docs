# ℹ️ Preguntas Frecuentes Middleware

**Problema: Las variantes no se asocian al producto configurable en Magento**

**Solución recomendada:**\
Cuando un producto configurable en Magento no asocia correctamente sus variantes, se debe realizar una sincronización manual desde un producto simple para identificar posibles errores. Generalmente, este problema ocurre debido a la falta de configuración de atributos necesarios. Una vez verificados y corregidos los atributos faltantes en Magento, se debe proceder con la sincronización del producto base desde el middleware (MW) de la siguiente manera:

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

#### Error: Estructura del XML inválida: There is an unclosed literal string

<figure><img src="../.gitbook/assets/image (3)(1)(1) (1).png" alt=""><figcaption></figcaption></figure>

Este error normalmente aparece cuando en la información de envío existen caracteres especiales o espacios adicionales que afectan la estructura del XML. Aunque suele presentarse en el campo de referencia, también puede ocurrir en otros campos como nombre, apellido o dirección.

<figure><img src="../.gitbook/assets/image (4)(1)(1).png" alt=""><figcaption></figcaption></figure>

