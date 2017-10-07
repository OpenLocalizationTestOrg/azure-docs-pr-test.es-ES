---
title: Interfaz de usuario de Mobile Engagement - alcance aaaAzure
description: "Obtenga información acerca de cómo tooreach toohello usuarios de la aplicación con las notificaciones de inserción con Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a>Cómo tooreach toohello usuarios de la aplicación con las notificaciones de inserción
Este artículo describe hello **ALCANZAR** ficha de hello **Mobile Engagement** portal. Usar hello **Mobile Engagement** toomonitor portal y administrar aplicaciones móviles. Tenga en cuenta que toostart mediante portal Hola primero debe toocreate una **Azure Mobile Engagement** cuenta. Para obtener más información, consulte [Crear una cuenta de Azure Mobile Engagement](mobile-engagement-create.md).

Hola llegar a sección de hello es la interfaz de usuario de herramienta de administración de campaña Hola inserción siempre que sea posible crear/editar/activar/finalizar/monitor y obtener estadísticas sobre las campañas de notificación de inserción y otras características que también son accesibles a través de API de cobertura de hello (y algunos elementos del programa Hola baja nivel de API de inserción). Recuerde que si utiliza las API de Hola o hello interfaz de usuario, necesitará toointegrate Azure Mobile Engagement y alcance en la aplicación para cada plataforma con hello SDK para poder utilizar alcanzan las campañas.

> [!NOTE]
> Muchas de las secciones de hello **Mobile Engagement** portal de interfaz de usuario contienen hello **ayuda para mostrar** botón. Presione este botón tooget más información contextual sobre una sección.
> 
> 

## <a name="four-types-of-push-notifications"></a>Cuatro tipos de notificaciones de inserción
1. Anuncios - permitir toosend publicidad mensajes toousers que redirigirá tooanother ubicación dentro de su aplicación o toosend su página Web tooa o almacenar fuera de la aplicación. 
2. Sondeos - permitir toogather información a los usuarios finales cuando les pregunta preguntas.
3. Inserciones de datos - permitir toosend un archivo de datos binarios o de base64. información de Hello contenida en una inserción de datos es enviado tooyour aplicación toomodify experiencia actual de los usuarios de la aplicación. La aplicación necesita datos de hello toobe tooprocess pueda en una inserción de datos.

## <a name="campaign-details"></a>Detalles de la campaña
Puede editar, clonar, eliminar o activar las campañas que todavía no ha activado todavía desplazando el puntero sobre sus nombres o puede hacer clic en tooopen ellos. Puede clonar las campañas que ya se han activado desplazando el puntero sobre sus nombres o puede hacer clic en tooopen ellos. Sin embargo, no puede cambiar una campaña una vez activada.

![Reach1][18]

## <a name="reach-feedback"></a>Comentarios sobre la cobertura
Haga clic en **estadísticas** detalles de hello toosee de una campaña de cobertura. Hola **Simple** vista proporciona una representación visual en forma de Hola de un gráfico de barras de columna sobre lo que sucedieron después de que se activó una campaña. Hola **avanzadas** vista proporciona detalles más granulares acerca de la campaña de inserción de Hola. Estos detalles no estará disponibles si va a enviar una campaña de prueba, es decir, un dispositivo de prueba de tooa enviado de inserción. A continuación le mostramos cómo interpretar estos detalles:

1. **Insertar** -especifica Hola número de mensajes insertados toohello dispositivos. Este número dependerá de la audiencia de destino de hello que especifica al crear una campaña de inserción de Hola. Si no especifica ninguna audiencia de destino, se enviará este inserción out tooall Hola registrado dispositivos. Al igual que todos los demás servicios de inserción, se no hello las notificaciones de inserción directamente toohello dispositivos pero en su lugar insertarlas toohello respectivos plataforma servicios específicos de notificaciones de inserción (PNS - APN/GCM/WNS) para que pueden entregar notificaciones de hello toohello dispositivos. 
2. **Entregar** -especifica Hola número de mensajes entregados por dispositivo de toohello PNS de Hola y confirmado correctamente como recibido por el SDK de Mobile Engagement. 
   
   *Razones de que el número de entregados sea inferior al número de insertados:*
   
   1. Si usuario de hello ha desinstalado la aplicación hello de dispositivo de hello pero no sabe hello PNS sobre él en tiempo de hello que enviamos Hola inserción toohello PNS se eliminarán los mensajes de bienvenida.
   2. Si dispositivo hello tiene aplicación hello pero propios dispositivos Hola estaban sin conexión durante largos períodos de tiempo, a continuación, hello PNS producirá dispositivo toohello de toodeliver Hola mensajes. 
   3. Si mensaje Hola se entrega toohello dispositivo pero Hola SDK de Mobile Engagement en la aplicación hello no reconoce el contenido de hello del mensaje de bienvenida, coloca ese mensaje. Esto podría suceder si personalización Hola de notificación de hello en la aplicación hello genera una excepción que se captura en mensaje de saludo SDK y drop Hola. Esto también puede ocurrir si la aplicación hello en dispositivo Hola está usando una versión de SDK de Mobile Engagement que no es capaz de toounderstand Hola versión posterior de mensaje de inserción de Hola Hola enviados desde la plataforma de Hola pero se trata solo cuando la aplicación hello se actualizó después de la notificación de Hola se distribuyó de plataforma del servicio Hola. Hola **avanzadas** ficha indicará cuántos mensajes se han quitado. 
   4. En dispositivos iOS, mensajes a veces no se entrega si cualquiera de estos dispositivos Hola de batería baja o si aplicación hello consume gran cantidad de energía al procesar notificaciones remotas. Se trata de una limitación de los dispositivos de iOS de Hola.   
3. **Muestra** -especifica Hola número de mensajes que se correctamente muestran toohello usuario de aplicación en dispositivos de hello en forma de Hola de una notificación de inserción/out-de-app del sistema en el centro de notificaciones de Hola o una notificación en la aplicación dentro de hello móviles aplicación.  Hola **avanzadas** ficha le indicará cuántos estaban notificaciones del sistema y cuántas notificaciones en la aplicación. 
   
   *Razones para mostradas recuento es menor que el recuento de entregado (toobe de espera muestra)*
   
   1. Si campaña de notificación de hello tenía una fecha de finalización en el es posible que se entregó notificación Hola pero al tiempo de hello suministrada tooopen y mostrar toohello usuario de aplicación, ya había expirado para que nunca se visualizó.   
   2. Si la notificación de hello es una notificación en la aplicación, a continuación, notificación de hello solo se muestra al usuario de aplicación Hola abre la aplicación hello. En casos donde usuario de aplicación hello no ha abierto la aplicación hello, Hola SDK notificará que notificación Hola se entrega pero aún no aparece hasta que se abra la aplicación hello. 
   3. Si la notificación de hello es una notificación en la aplicación y configura toobe que se muestra en una pantalla/actividad específica, a continuación, también se notificará notificación Hola tal como se entrega pero todavía no se han entregado hasta que el usuario de hello abre la aplicación hello en una pantalla específica. 
4. **Las interacciones del usuario** -especifica Hola número de mensajes que usuario de la aplicación hello ha interactuado con e incluirá los mensajes de Hola que son accionado o cerrado. 
   
   * *usuario de aplicación Hola puede accionar una notificación en la vista de hello siguientes maneras:*
     
     1. Si hello notificación es una notificación de sistema/out-de-app o envía una notificación de aplicación como de solo notificación, a continuación, haga clic en usuario de aplicación hello en la notificación de Hola.
     2. Si la notificación de hello es una notificación en la aplicación con un texto o una vista web o sondeos Hola, a continuación, el usuario de la aplicación hace clic en hello botón de acción de notificación de Hola.
     3. Si la notificación de hello es una notificación en la aplicación, a continuación, con una vista web Hola aplicación clics del usuario en una dirección URL en hello web solo en la vista [Android]
   * *usuario de aplicación Hola puede cerrar una notificación en la vista de hello siguientes maneras:*
     
     1. Haga clic en botón de cierre de hello en la notificación de hello directamente. 
     2. Eliminar notificación Hola o Deslizar rápidamente inmediatamente. 
     3. Las notificaciones de aplicación con sondeos y contenido web y de texto son normalmente muestran toohello usuario de aplicación en un proceso de dos pasos. Verán una notificación en primer lugar y cuando haga clic en él, podrán ver contenido de texto/web/sondeo subsiguiente de Hola. usuario de aplicación Hola puede salir de una notificación en cualquiera de estos pasos y captura los detalles de hello en vista avanzada de hello esto. 
5. **Accionado** -especifica Hola número de mensajes que hayan sido accionados explícitamente por el usuario de aplicación Hola. Éste es el número de más interesante de hello como esto indica cuántos usuarios de aplicación se está interesados mensaje Hola que sobresale en la notificación de Hola. 

> [!NOTE]
> En iOS y plataformas de Windows, si usuario hello tiene aplicación Hola abierta y campaña Hola era una campaña "En cualquier momento" es posible que ambos fuera de la aplicación y en la aplicación de notificaciones se muestran en hello mismo tiempo. Esto puede provocar un recuento de mostradas superior Hola entregado. Si Hola usuario interactúa o notificación de Hola de acciones, hello, a continuación, incluso el recuento de las interacciones de usuario/Actioned podría ser mayor que entregado. 
> 
> 

![Reach2][19]

## <a name="see-also"></a>Otras referencias
* [Conceptos][Link 6]
* [Guía de solución de problemas de servicios][Link 24]

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

