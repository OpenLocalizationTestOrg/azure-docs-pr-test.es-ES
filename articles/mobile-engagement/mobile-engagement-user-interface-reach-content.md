---
title: aaaAzure interfaz de usuario de Mobile Engagement - alcanzar contenido
description: "Obtenga información acerca de cómo campañas contenido exclusivo de hello toomanage de diferentes tipos de notificación de inserción de hello en Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>¿Cómo toomanage Hola contenido exclusivo de tipos diferentes de hello de campañas de notificación de inserción
Puede usar la sección de contenido de Hola de alcance de la campaña toomodify Hola contenido nuevo de los anuncios, sondeos, inserta datos e iconos (solo Windows Phone). configuración de contenido de Hola de las campañas de inserción es toohello específicos de tipo de campaña. 

### <a name="content-types"></a>Tipos de contenido:
* Anuncios
* Sondeos
* Inserciones de datos
* Mosaicos (solo en Windows Phone)

## <a name="content-of-announcements"></a>Contenido de anuncios
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>Elija el tipo de saludo del anuncio:
* Solo notificación: es una notificación estándar simple. Lo que significa que, si un usuario hace clic en él, no aparecerá vista adicional, pero solo Hola acción asociada, se producirá tooit.
* Anuncio de texto: es una notificación que involucre a Hola usuario toohave un vistazo a una vista de texto.
* Anuncio de Web: es una notificación que involucre a Hola usuario toohave un vistazo a una vista web.

### <a name="see-also"></a>Otras referencias
* [Cobertura - Guía práctica - Anuncios][Link 3] 

### <a name="about-web-view-announcements"></a>Acerca de los anuncios de visualización web:
Apariciones del patrón de Hola "{deviceid}" en el código de hello HTML o código JavaScript que proporciona aquí se reemplazará automáticamente por identificador de hello de dispositivo de Hola que muestra el anuncio de Hola. Se trata de un identificadores de dispositivos de Azure Mobile Engagement de manera sencilla tooretrieve en externo hospedado en el área de operaciones de servicio web.
Si desea que toocreate una completa Pantalla vista web (sin Hola botones predeterminados acción y salir proporcionamos) puede usar Hola siguientes funciones de código JavaScript de anuncio de vista web: 

* realizar acción de anuncio Hola: ReachContent.actionContent()
* salir del anuncio de Hola: ReachContent.exitContent()

### <a name="choose-your-action"></a>Elija la acción:
### <a name="about-action-urls"></a>Acerca de las direcciones URL de la acción:
Cualquier dirección URL que puede ser interpretada por el sistema operativo de destino de un dispositivo puede utilizarse como una dirección URL de la acción.
Cualquier dirección URL dedicada que su aplicación podría compatibilidad (por ejemplo, los usuarios de toomake saltar tooa de pantalla determinada) también se puede utilizar como una dirección URL de acción.
Cada repetición del patrón de Hola {deviceid} se sustituye automáticamente por identificador de hello de dispositivo de hello realizar acción Hola. Esto puede resultar tooeasily usa identificadores de dispositivo de Azure Mobile Engagement de recuperar a través de un servicio web externo hospedado en el área de operaciones.

* **Acciones de Android + iOS**
  * Abrir una página web
  * http://\[dominio-sitio-web\] 
  * Ejemplo: http://www.azure.com
  * Enviar un correo electrónico
  * mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!
  * Enviar un SMS
  * sms:\[número-teléfono\] 
  * Ejemplo:sms:2125551212
  * Marcar un número de teléfono
  * tel:\[número-teléfono\] 
  * Ejemplo:tel:2125551212
* **Acciones solo para Android**
  * Descargar una aplicación de hello Play Store
  * market://details?id=\[paquete de la aplicación\] 
  * Ejemplo:market://details?id=com.microsoft.office.word
  * Iniciar una búsqueda localizada geográficamente
  * geo:0,0?q=\[consulta de búsqueda\] 
  * Ejemplo:geo:0,0?q=starbucks,paris
* **Acciones solo para iOS**
  * Descargar una aplicación de hello tienda de aplicaciones
  * http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8 
  * Ejemplo: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Acciones de Windows
  * Abrir una página web
  * http://\[dominio-sitio-web\] 
  * Ejemplo: http://www.azure.com
  * Enviar un correo electrónico
  * mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!
  * Enviar un SMS (requiere la aplicación Skype)
  * sms:\[número-teléfono\] 
  * Ejemplo:sms:2125551212
  * Marcar un número de teléfono (requiere la aplicación Skype)
  * tel:\[número-teléfono\] 
  * Ejemplo:tel:2125551212
  * Descargar una aplicación de hello Play Store
  * ms-windows-store:PDP?PFN=\[id. del paquete de la aplicación\] 
  * Ejemplo:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * Iniciar una búsqueda en Mapas de Bing
  * bingmaps:?q=\[consulta de búsqueda\] 
  * Ejemplo:bingmaps:?q=starbucks,paris
  * Utilice un esquema personalizado
  * \[esquema personalizado\]://\[parámetros del esquema personalizado\] 
  * Ejemplo:myCustomProtocol://myCustomParams
  * Utilizar datos de paquete (se necesita una aplicación de la tienda para leer la extensión)
  * \[carpeta\]\[datos\].\[extensión\] 
  * Ejemplo:myfolderdata.txt

### <a name="build-a-tracking-url"></a>Crear una dirección URL de seguimiento:
* Vea Hola sección "Configuración" de hello <UI Documentation> para obtener instrucciones sobre la creación de una dirección URL de seguimiento que le permitirá toodownload a los usuarios una de las otras aplicaciones.

### <a name="define-hello-texts-of-your-announcement"></a>Definir Hola textos del anuncio
Rellene Hola título, contenido y textos de botón del anuncio. Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña. La audiencia de destino puede basarse en los comentarios de Hola de si solo se ha insertado esta campaña, respondidos, accionado o cerrado.

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]

## <a name="content-of-polls"></a>Contenido de sondeos
![Reach-Content2][31] 

Rellene Hola título, descripción y textos de botón del anuncio. A continuación, agregue preguntas y opciones para hello respuestas tooyour preguntas.
Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña. La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña. La audiencia de destino también puede basarse en los comentarios de respuesta de sondeo, donde elección de pregunta y respuesta de Hola se utilizan como criterios.

### <a name="see-also"></a>Otras referencias
* [Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]

## <a name="content-of-data-pushes"></a>Contenido de las inserciones de datos
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a>Elija el tipo de saludo de los datos:
* Texto
* Datos binarios
* Datos de Base64

### <a name="define-hello-content-of-your-data"></a>Definir el contenido de Hola de los datos
* Si seleccionó toopush datos de texto, copie y pegue el texto hello en cuadro "contenido" Hola.
* Si seleccionó toopush datos binarios o base64, utilice tooupload de botón de "cargar el archivo" hello el archivo.
* Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña. La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña.

### <a name="see-also"></a>Consulte también
* [Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Contenido de los mosaicos (solo en Windows Phone)
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a>Definir el contenido de hello del título
carga de mosaico de Hello es hello toobe de texto mostrado en el icono de saludo de la aplicación en dispositivos Windows Phone.
Una inserción de mosaico es la versión de servicio de notificaciones de inserción de Microsoft (MPNS) de Hola de una inserción nativa para Windows Phone. tipo de inserción de mosaico de Hello es el único tipo de inserción de Hola que no tiene una respuesta y por lo que no se puede compilar audiencia Hola de campañas futuras en resultados de Hola de una campaña de inserción de mosaico. 

### <a name="see-also"></a>Otras referencias
* [Documentación de la API - API de cobertura - Inserción nativa][Link 4]

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

