---
title: aaaAzure interfaz de usuario de Mobile Engagement - alcanzar criterio
description: "Obtenga información acerca de cómo toouse destinatarios criterios toosend inserción campañas tooa Seleccionar subconjunto de los usuarios mediante Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d956add1b7edc1d49451596019c5a4dec098d724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a>¿Cómo toouse destinatarios criterios toosend inserción campañas tooa Seleccionar subconjunto de usuarios
La audiencia de destino según unos criterios específicos con el botón de "Nuevo criterio" hello es uno de los conceptos de hello más eficaces en Azure Mobile Engagement que le ayuda a que enviar relevante inserción notificaciones de que los clientes de hello responderá tooinstead de spam todos los usuarios. Puede limitar la audiencia basándose en criterios estándares y simular inserciones toodetermine cuántas personas recibirán la notificación de Hola.

**Consulte también:**

* [Documentación de la interfaz de usuario - Alcance - Nueva campaña de inserción][Link 27]

## <a name="audience-criteria-can-include"></a>Dentro de los criterios de audiencia se pueden incluir:
* ** Technicals: ** puede tener como destino en función de hello misma información técnica puede ver en hello análisis y secciones de Monitor. **Consulte también**: [Documentación de la interfaz de usuario - Análisis][Link 15], [Documentación de la interfaz de usuario - Supervisión][Link 16]
* **Ubicación:** las aplicaciones que usan "informes de ubicación en tiempo Real" con barrera geográfica pueden usar ubicación geográfica como una tootarget criterios una audiencia de hello ubicación GPS. Llamada "Informes de ubicación de área diferida" también ser utilizado tootarget una audiencia de ubicación de teléfono móvil de hello ("informes de ubicación en tiempo Real" y "Diferida área informes de ubicación" deben activarse desde Hola SDK). **Consulte también:**[Documentación del SDK - iOS -][Link 5], [Documentación del SDK - Android - Integración][Link 5]
* **Comentarios sobre la cobertura:** puede tener como destino su audiencia según sus comentarios de notificaciones de cobertura anteriores a través de comentarios sobre la cobertura de Anuncios, Sondeos e Inserciones de datos. Esto le permite destino toobetter la audiencia después de dos o tres alcancen las campañas que se podría Hola la primera vez. Se puede utilizar también toofilter los usuarios que ya ha recibido una notificación con contenido similar, estableciendo una campaña tooNOT enviará toousers que han recibido una determinada campaña anterior. Incluso puede excluir a los usuarios incluidos en una campaña específica que está todavía activa para recibir inserciones nuevas. **Vea también:**[Documentación de la interfaz de usuario - Cobertura - Insertar contenido][Link 29]
* **Seguimiento de la instalación:** puede realizar un seguimiento de información basada en dónde instalaron los usuarios su aplicación. **Consulte también:**[Documentación de interfaz de usuario - Configuración][Link 20]
* **Perfil de usuario:** puede destino basándose en información de usuario estándar y usted puede destino basándose en información de la aplicación personalizada de Hola que haya creado. Esto incluye los usuarios que han iniciado sesión en y los usuarios que responder a preguntas específicas que se ha solicitado tooset en hello propia aplicación en lugar de simplemente cómo han respondido tooprevious campañas. Toda la información de la aplicación definida para la aplicación aparece en esta lista.
* Segmentos: también puede orientarse en función de segmentos que ha creado según el comportamiento específico del usuario que contiene varios criterios. Todos los segmentos definidos para la aplicación aparecen en esta lista. **Consulte también:**[Documentación de interfaz de usuario - Segmentos][Link 18]
* **Información de la aplicación:** etiquetas de información de aplicación personalizadas se pueden crear de comportamiento del usuario tootrack "Configuración". **Consulte también:**[Documentación de interfaz de usuario - Configuración][Link 20]

## <a name="example"></a>Ejemplo:
Si desea que toopush un anuncio solo toohello subjuego de los usuarios que ha llevado a cabo una aplicación de compra acción.

1. Ir a página de configuración de aplicación tooyour, seleccione el menú de "Información de la aplicación" hello y seleccione "Nueva información de aplicación"
2. Registre una nueva información de aplicación de booleano denominada "inAppPurchase"
3. Hacer que su aplicación establecer esta información de aplicación demasiado "true" cuando el usuario de hello correctamente realiza una compra en la aplicación (mediante el uso de hello sendAppInfo ("inAppPurchase",...) función)
4. Si no desea toodo esto desde la aplicación, puede hacerlo desde el back-end a través de API de dispositivo de hello)
5. A continuación, simplemente deberá toocreate anuncio, con un criterio limitar su toousers de audiencia tener "inAppPurchase" establecido demasiado "true")

> [!NOTE]
> Según los criterios que no sea de etiquetas de información de aplicación de destino, requiere información de toogather de Azure Mobile Engagement de dispositivos de los usuarios antes de inserción de Hola se envía y puede producir un retraso. Las opciones de configuración de inserción complejas (como la actualización de insignias) también pueden retrasar las inserciones. Usando una campaña "Monoestable" de hello API de inserción es absoluta método de inserción hello más rápido de Azure Mobile Engagement. Usar sólo las etiquetas de información de aplicación como criterios de inserción para una campaña de cobertura (ya sea de hello API de cobertura o hello interfaz de usuario) es Hola next más rápido (método) puesto que las etiquetas de información de aplicación se almacenan en el lado del servidor de Hola. Usando otros criterios de destino para una campaña de inserción es Hola método de inserción más flexible pero más lento debido a que Azure Mobile Engagement tiene dispositivos de hello tooquery de campaña de orden toosend Hola.

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a>Las opciones de criterios se aplican a:
* **Notas técnicas**     
* Nombre del firmware: el nombre del firmware.
* Versión del firmware: la versión del firmware.
* Modelo de dispositivo: el modelo del dispositivo.
* Fabricante del dispositivo: el fabricante del dispositivo.
* Versión de la aplicación: la versión de la aplicación.
* Nombre del operador: el nombre del operador.
* País del operador: el país del operador, sin definir.
* Tipo de red: el tipo de red.
* Configuración regional: la configuración regional.
* Tamaño de pantalla: el tamaño de pantalla.
* **Ubicación**      
* Última área conocida: país, región, localidad.
* Geovallado en tiempo real: lista de puntos de interés (nombre, acciones), punto de interés circular (nombre, latitud, longitud, radio en metros)
* **Comentarios sobre la cobertura**     
* Comentarios de anuncio: anuncio, comentarios.
* Comentarios de sondeo: sondeo, comentarios.
* Comentarios de respuesta de sondeo: comentarios de respuesta de sondeo, pregunta, opción.
* Comentarios de inserción de datos: inserción de datos, comentarios.
* **Seguimiento de la instalación**     
* Tienda: tienda, sin definir.
* Origen: origen, sin definir.
* **Perfil de usuario**     
* Género: hombre o mujer, sin definir.
* Fecha de nacimiento: operador, fecha, sin definir.
* Participar: verdadero o falso, sin definir.
* **Información de la aplicación**      
* Cadena: cadena, sin definir.
* Fecha: operador, fecha, sin definir.
* Entero: operador, número, sin definir.
* Booleano: verdadero o falso, sin definir.
* **Segmento**    
* Nombre de segmentos (de la lista desplegable), exclusión (usuarios de destino que no forman parte de este segmento).

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

