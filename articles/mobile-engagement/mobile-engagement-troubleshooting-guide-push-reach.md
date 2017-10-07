---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - inserción/alcance"
description: "Solución de problemas de interacción de usuario y notificación en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Guía de solución de problemas de inserción y cobertura
los siguientes Hola son posibles problemas que pueden producirse con la forma en que Azure Mobile Engagement envía información de los usuarios tooyour.

## <a name="push-failures"></a>Errores de inserción
### <a name="issue"></a>Problema
* Las inserciones no funcionan (en la aplicación, fuera de la aplicación, o en ambos ámbitos).

### <a name="causes"></a>Causas
* Muchas veces un error de inserción es una indicación de que Azure Mobile Engagement, alcance u otra característica avanzada de Azure Mobile Engagement no está correctamente integrado o que es una actualización necesaria en hello SDK toofix un problema conocido con una nueva plataforma de sistema operativo o el dispositivo.
* Probar simplemente una inserción en la aplicación y solo un toodetermine de inserción fuera de la aplicación si algo es un problema en la aplicación o fuera de la aplicación.
* Pruebas de interfaz de usuario de Hola y Hola API como una solución de problemas toosee paso está disponible la información de error adicional ambos lugares.
* Fuera de la aplicación inserciones no funcionarán a menos que se integran Azure Mobile Engagement y alcance Hola SDK.
* Las inserciones no funcionarán si los certificados no son válidos o usan PROD frente a DEV correctamente (únicamente iOS). (**Nota:** "fuera de la aplicación" notificaciones de inserción pueden no entregarse tooiOS, si tiene ambos desarrollo hello (desarrollo) y versiones de producción (PROD) de la aplicación instaladas en hello mismo dispositivo desde el token de seguridad de hello asociado puede invalidar con el certificado de Apple. tooresolve este problema, desinstale Hola DEV y PROD versiones de la aplicación y volver a instalar solo Hola una versión en el dispositivo.)
* Fuera de la aplicación los recuentos de inserción se tratan de forma diferente en distintas plataformas (iOS muestra menos información que Android si se deshabilitan inserciones nativo en un dispositivo, Hola API puede proporcionar más información que la interfaz de usuario de hello en estadísticas de inserción).
* Las inserciones fuera de la aplicación pueden ser bloqueadas por los clientes a nivel de sistema operativo (iOS y Android).
* Fuera de la aplicación inserciones se mostrará como deshabilitado en la interfaz de usuario de Azure Mobile Engagement Hola si no se integra correctamente, pero puede producir un error en modo silencioso desde Hola API.
* En la aplicación inserciones no funcionarán a menos que se integran Azure Mobile Engagement y alcance Hola SDK.
* Inserciones GCM y ADM no funcionarán a menos que Azure Mobile Engagement y servidor específico de hello están integradas en hello SDK (solo Android).
* De aplicación y fuera de la aplicación deben ser inserciones probado por separado toodetermine si es un problema de inserción o de alcance.
* En inserciones de aplicación requieren que la aplicación hello puede abrir toobe recibido.
* En la aplicación inserciones son a menudo toobe el programa de instalación filtrado por una etiqueta de información de aplicación opcional o no.
* Si usas una categoría personalizada en las notificaciones de alcance toodisplay en la aplicación, necesita toofollow Hola correcta ciclo de vida de la notificación de hello, o bien notificación hello no se puede borrar al usuario Hola descartarla.
* Si inicia una campaña con sin fecha de finalización y un dispositivo recibe hello en la notificación de la aplicación, pero no mostrar aún, usuario Hola seguirá recibiendo Hola Hola de notificación próxima vez que inicien sesión en la aplicación hello, incluso si manualmente finaliza la campaña Hola.
* Para problemas con la API de inserción de hello, confirme que realmente desea toouse Hola API de inserción en lugar de hello API de cobertura (desde que se utiliza con más frecuencia Hola API de Reach) y que no está confuso Hola "carga" y los parámetros de "notificador".
* Pruebe las campañas de inserción con ambos un dispositivo conectado a través de Wi-Fi y 3G tooeliminate Hola conexión de red como un posible origen de problemas.

## <a name="push-testing"></a>Pruebas de inserción
### <a name="issue"></a>Problema
* Se puede enviar notificaciones Push tooa dispositivo específico en función de un identificador de dispositivo.

### <a name="causes"></a>Causas
* Dispositivos de prueba son el programa de instalación diferente para cada plataforma, pero genera un evento en la aplicación en un dispositivo de prueba y busca el identificador de dispositivo en el portal de hello deben funcionar toofind su Id. de dispositivo para todas las plataformas.
* Los dispositivos de prueba funcionan de manera diferente con IDFA frente a IDFV (únicamente en iOS).

## <a name="push-customization"></a>Personalización de inserción
### <a name="issue"></a>Problema
* El elemento de contenido de inserción avanzada no funciona (distintivo, anillo, vibración, imagen, etc.).
* No funcionan los vínculos de inserciones (fuera de la aplicación, en la aplicación, el sitio Web de tooa, la ubicación de tooa en aplicación).
* Mostrar estadísticas de inserción que una inserción no envía tooas muchas personas según lo previsto (demasiados o no hay suficiente).
* Inserción duplicada y recibida dos veces.
* No se puede registrar el dispositivo de prueba para inserciones de Azure Mobile Engagement (con su propia aplicación de producción o desarrollo).

### <a name="causes"></a>Causas
* toolink tooa una ubicación concreta de la aplicación requiere "categorías" (solo Android).
* Profundidad de vinculación de esquemas de ubicación alternativa tooan de tooredirect usuarios tras hacer clic en una notificación de inserción necesario toobe creada en y administrada por el dispositivo de hello y aplicación de sistema operativo no por Mobile Engagement directamente. (**Nota:** fuera de la aplicación las notificaciones no pueden vincular directamente tooin ubicaciones de aplicación con iOS se puede hacer con Android.)
* Servidores de imágenes externo necesitan toobe capaz de toouse HTTP "GET" y "Principal" para panorama inserta toowork (solo Android).
* En el código, puede deshabilitar agente de Azure Mobile Engagement hello cuando se abre el teclado de Hola y hacer que el código volver a activar el agente de Azure Mobile Engagement Hola una vez cerrada teclado Hola para que hello teclado no afectan a Hola apariencia de su notificación (solo iOS).
* Algunos elementos no funcionan en las simulaciones de prueba, sino solo las campañas reales (distintivo, anillo, vibración, imagen, etc.).
* Ningún servidor datos se registran cuando se usa el botón de hello demasiado "test" inserta. Los datos solo se registran para campañas de inserción real.
* toohelp aislar el problema, solucionar problemas con: de prueba, simular y una campaña real, ya que cada uno de ellos funciona de manera ligeramente diferente.
* Hello período de tiempo que el "aplicación" y campañas "en cualquier momento" están programado toorun puede afectar a números de entrega desde una campaña solo se entregarán toousers que están "en la aplicación" mientras se ejecuta la campaña de hello (y los usuarios que tienen su configuración de dispositivo establece tooreceive notificaciones de "fuera de la aplicación").
* diferencias de Hello entre lo iOS y Android identificador fuera de las notificaciones de la aplicación que resulta difícil toodirectly comparan las estadísticas de inserción entre la versión de iOS y Android de saludo de la aplicación. Android proporciona más información de notificación a nivel de sistema operativo que iOS. Android notifica si una notificación nativa es recibida, hace clic en o eliminada en el centro de notificaciones de hello, pero iOS no proporcionan esta información a menos que se hace clic en la notificación de Hola. 
* Hola principal motivo por el que sean diferentes de los diferentes de números de "entrega" para llegar a las campañas es que "en la aplicación" y "fuera de la aplicación" las notificaciones se cuentan de manera distinta números "push". "En la aplicación" notificaciones se administran por Mobile Engagement, pero "fuera de la aplicación" notificaciones se administran mediante el centro de notificaciones de Hola Hola SO del dispositivo.

## <a name="push-targeting"></a>Orientación de la inserción
### <a name="issue"></a>Problema
* El destino integrado no funciona según lo esperado.
* La orientación de la etiqueta de información de la aplicación no funciona como se esperaba.
* La orientación de geolocalización no funcionan según lo esperado.
* Las opciones de idioma no funcionan según lo esperado.

### <a name="causes"></a>Causas
* Asegúrese de que ha cargado etiquetas de información de aplicación a través de interfaz de usuario de Azure Mobile Engagement Hola o API.
* Limitación Hola velocidad o inserción cuota de inserción en el nivel de aplicación de Hola o restricción audiencia de hello en el nivel de la campaña de hello puede impedir que una persona que se reciba una inserción específica incluso si cumplen los criterios de destinatarios. 
* Establecer un "idioma" es diferente de orientar en función del país o la configuración regional, que también es diferente a orientar según la geolocalización basada en una ubicación de teléfono o de GPS.
* mensaje de Hola Hola "idioma predeterminado" se envía a tooany cliente que no disponga de su dispositivo establezca tooone de idiomas alternativos de Hola que especifique.

## <a name="push-scheduling"></a>Programación de la inserción
### <a name="issue"></a>Problema
* La programación de la inserción no funciona como se esperaba (envío demasiado tiempo o retrasado).

### <a name="causes"></a>Causas
* Zonas horarias puede problemas con la programación, especialmente cuando se usa la zona horaria de los usuarios de finales de Hola.
* Las funciones avanzadas de inserción pueden retrasar las inserciones.
* Destino basado en teléfono puede retrasar la configuración (en lugar de la aplicación información de etiquetas) inserta ya que Azure Mobile Engagement podría tener datos toorequest de teléfono hello en tiempo real antes de enviar una inserción.
* Las campañas que se creó sin una fecha de finalización almacenan localmente inserción hello en dispositivo de Hola y mostrarlo Hola próxima vez que se abre la aplicación hello aunque manualmente se finalizó la campaña Hola.
* A partir de más de una campaña en hello mismo tiempo puede tardar un tooscan de tiempo más largo su base de usuarios (intente tooonly inicio una campaña simultáneamente con un máximo de cuatro, también tienen como destino sólo los usuarios activos tooyour para que los usuarios antiguos no tengan toobe analizado).
* Si utiliza opción de "Omitir audiencia, dejarán de enviarse toousers a través de la API de Hola" hello en hello "Campaña" sección de una campaña de cobertura, campaña de hello no enviará automáticamente, deberá toosend esta manualmente a través de la API de cobertura de Hola.
* Si usas una categoría personalizada en las notificaciones de alcance toodisplay en la aplicación, necesita toofollow Hola correcta ciclo de vida de una notificación, o bien notificación hello no se puede borrar al usuario Hola descartarla.

