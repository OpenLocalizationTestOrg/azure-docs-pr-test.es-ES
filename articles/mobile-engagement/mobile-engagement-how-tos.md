---
title: "aaaAzure interfaz de usuario de Mobile Engagement - alcanzar cómo de a"
description: "Introducción de la interfaz de usuario de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 30af87e6-c816-4cce-8609-6cbd3e83de14
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4b6dafd09d894214d4c386f5c6f157a77671606f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-using-and-managing-pushes-tooreach-out-tooyour-end-users"></a>Cómo tooget a usar y administrar inserta tooreach a los usuarios finales de tooyour
Una vez hello SDK está totalmente integrado en la aplicación, puede empezar a usar sección de alcance de Hola Hola Hola UI tooPush notificaciones toohello usuarios de la aplicación.  

## <a name="do-your-first-push-notification-campaign"></a>Creación de la primera campaña de notificación de inserción
* Confirme que su alcance se integra en la aplicación con hello SDK. 
* Seleccione la aplicación.

![First1][1]

* Vaya toohello sección "Alcance" y haga clic en "nuevo anuncio"

![First2][2]

* Cree una campaña nueva y asígnele un nombre.
  
![First3][3]

* Seleccione cómo se deben entregar notificaciones de hello, como en la aplicación solo

![First4][4]

* Crear mensajes de bienvenida que desee toopush

![First5][5]

* Puede escribir un título en la notificación de hello (opcional).
* Escriba el contenido del mensaje de inserción.
* Puede cargar una imagen. Tenga en cuenta que el tamaño de Hola de archivo hello no puede superar 32.768 bytes.
* También tienen Hola capacidad tooselect más opciones, pero para se centran Hola de este tutorial, veremos más adelante.
* Seleccionar tipo de contenido de hello como notificación solo

![First6][6]

* Cree la campaña de inserción, que aparecerá en la lista de campañas.

![First7][7]

## <a name="test-your-push-notification-campaign"></a>Prueba de la campaña de notificación de inserción
![Test1][8]

* Registre el dispositivo.
* Haga clic en la casilla de verificación de hello de dispositivo de hello desea toopush.
* Haga clic en hello "Test" botón toosend Hola inserción toohello dispositivo.

![Test2][9]

* Activar la campaña Hola

![Test3][10]

* Ahora que ha creado la campaña debe tooactivate para toobe de notificación de hello inserta tooyour a los usuarios.

## <a name="send-personalized-pushes"></a>Envío de inserciones personalizadas
* Este ejemplo crea una inserción donde se escribe un código de descuento personalizado en la notificación de inserción de Hola.

![Personalize1][11]

Personalización funciona reemplazando un marcador de la forma de una etiqueta de información de la aplicación por lo tanto, tendrá que usuario Hola tenga Hola apropiado app-info primero define toomake. En este Hola ejemplo los usuarios de destino tendrá una etiqueta de información de aplicación denominada rebate_code definido.
Como se ve anteriormente contenido de notificación de inserción de Hola incluye hello marcador ${rebate_code} que indicará que está toobe reemplazado por el contenido real de Hola de etiqueta de información de aplicación Hola.

> [!WARNING]
> Si no se define la etiqueta de información de aplicación hello para el usuario de hello, usuario de hello no recibirá la inserción de Hola.

* Resultado

![Personalize2][12]

### <a name="you-can-further-personalize-hello-text-your-notification"></a>Se puede personalizar aún más texto hello la notificación
![Personalize3][13]

* Incluido el título de Hola de notificación de hello,
* Y el contenido de Hola de mensaje de bienvenida.
* Elegir tipo de Hola de anuncio (vista de texto o Web)

![Personalize4][14]

### <a name="hello-body-of-an-announcement-may-also-be-personalized-with"></a>cuerpo de Hola de un anuncio también puede personalizarse con:
* dirección URL de acción de Hello, si quiere que hello toocustomize página de aterrizaje
* título de Hello,
* cuerpo de Hello del mensaje de bienvenida.

## <a name="differentiate-your-push-notification-in-or-out-of-app"></a>Diferenciación de la notificación de inserción (en la aplicación o fuera de ella)
* Elija el tipo de saludo de notificación se push, seleccione la aplicación, vaya toohello "Alcance" sección, seleccione o cree una campaña de inserción y vaya toohello "sección"notificación.
* Haga clic en "modo de entrega" hello que desee.
* Haga clic en hello "Restringir actividades" casilla de verificación si desea que la notificación de Hola se produce en actividades específicas (pantallas).

![Differentiate1][15]

### <a name="out-of-app-only-delivery-mode"></a>Modo de entrega "Solo fuera de la aplicación"
![Differentiate2][16]

"Fuera de la aplicación solo" modo de entrega proporciona una notificación de inserción cuando se cierra la aplicación hello. Se trata de una notificación de inserción estándar de Hola.
Cuando se selecciona "fuera de la aplicación solo", deben haber proporcionado certificados Hola de plataforma de Hola que se está ejecutando la aplicación en (APN o GCM).

### <a name="see-also"></a>Otras referencias
* [Apple Push Notification Service: certificados](http://developer.apple.com/library/mac/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9), [Google Cloud Messaging: certificado](http://developer.android.com/google/gcm/index.html) 

### <a name="in-app-only-delivery-mode"></a>Modo de entrega "Solo en la aplicación"
![Differentiate3][17]

El modo de entrega "En la aplicación solo" proporciona una notificación de inserción cuando se ejecuta la aplicación hello.
Para esta notificación, no es necesario toogo a través de hello APN y sistema GCM.
Puede usar tooreach de sistema de entrega de la aplicación hello en los usuarios finales.
Totalmente puede personalizar la notificación de Hola y decidir en qué actividad (pantalla) aparecerá la notificación de Hola.

### <a name="anytime-delivery-mode"></a>Modo de entrega "En cualquier momento"
Puede elegir un modo de entrega "En cualquier momento", asegura tooreach Hola a los usuarios finales si está ejecutando la aplicación o no.
Cuando se selecciona "En cualquier momento", deben haber proporcionado certificados Hola de plataforma de Hola que se está ejecutando la aplicación (APN o GCM). 

## <a name="schedule-a-push-campaign"></a>Programación una campaña de inserción
### <a name="plan-toostart-a-campaign"></a>Planear una campaña tooStart
![Shedule1][18]

Es Hola 21 de marzo y tiene un toomake de anuncio y cepillada 22 de marzo de Hola a medianoche. No tiene toostay delante Hola interfaz toodo una inserción. Puede planear de antemano Hola exacta minuto se enviarán las notificaciones.

* Desactive Hola "None" casilla de verificación y seleccione una hora de inicio 
* Elija Hola fecha y hora en hello que desea campaña de inserción de toostart Hola.

### <a name="plan-tooend-a-campaign"></a>Planear una campaña tooend
![Shedule2][19]

Desea el toostop campaña en hello a 3:00 p.m. el 25 de marzo pero sabe no estando ahí toodo lo.
¡No tienes toostay delante Hola interfaz toopush! Puede planear de antemano Hola exacta minuto que la campaña se detendrá.

* Haga clic en hello "None" casilla o seleccione una hora de finalización
* Elija Hola fecha y hora en hello que desea campaña de inserción de toofinish Hola.

### <a name="end-a-campaign-manually"></a>Finalización de una campaña manualmente
![Shedule3][20]

De forma predeterminada, Hola "None" casillas de verificación están activadas.
Esto significa que campaña Hola se iniciará en cuanto activarlo en hello llegar a la sección y alcanzará final al que detendrá en hello sección.

> [!NOTE]
> Las campañas que se creó sin una fecha de finalización almacenan localmente inserción hello en dispositivo de Hola y mostrarlo Hola próxima vez que se abre la aplicación hello aunque manualmente se finalizó la campaña Hola.

## <a name="enhance-a-push-notification-with-a-text-view"></a>Mejora de una notificación de inserción con una vista de texto
### <a name="what-is-a-text-view"></a>¿Qué es una vista de texto?
![TextView1][21]

Una vista de texto es un elemento emergente con contenido de texto. Este elemento emergente aparece después de que haya hecho clic en para el usuario final de hello en la notificación de inserción de Hola.
Una vista de texto permite toopresent más contenido por el usuario final tooyour. También es Hola oportunidad toopresent un tooaction de llamada como saltar página tooa de la aplicación, redirigiendo tooa almacén, abrir una página web, enviar un correo electrónico, a partir de una búsqueda geolocalizados, etcetera...

### <a name="example-text-view"></a>Ejemplo: vista de texto
* Crear la campaña de notificación de inserción en la sección "Alcance" de Hola y asigne un nombre a la campaña

![TextView2][22]

* Escribir el mensaje de Hola que va a aparecer en la notificación de Hola.
* Seleccione el tipo de contenido de anuncio de "texto" Hola

![TextView3][23]

> [!NOTE]
> Cuando inserta una vista de texto, siempre va acompañada de una notificación en primer lugar. 

* Definir el texto hello (tras haber seleccionado el contenido de la presentación de texto hello, aparecerá la subsección de hello, permitiéndole texto de hello toodefine que desea toobe muestra.)

![TextView4][24]

* Escribir el título de Hola que aparecerá en la parte superior de Hola de mensaje de bienvenida.
* Escribir contenido principal de Hola de vista de texto hello.
* Escribir contenido de Hola que va a aparecer en el botón de acción de hello (un botón de acción permite Hola aplicación toomake una acción específica como la apertura de una página de aplicación hello, redirigiendo tooan App store o cualquier tipo de orígenes que pueden proporcionar).
* Contenido de Hola de escritura que va a aparecer en el botón Salir de hello (haciendo clic en botón Salir de hello, vista de texto hello desaparecerá.)
* Crear la campaña de notificación de inserción y aparecerá en la lista de la campaña de Hola.

![TextView5][25]

* Activar la inserción notificación campaña toosend Hola texto vista tooyour a los usuarios.

![TextView6][26]

* Resultado

![TextView7][27]

* Hola usuario recibe la notificación de Hola y haga clic en él.
* vista de texto Hello aparece como un toointeract de usuario Hola permitiendo emergente con él.

## <a name="enhance-a-push-notification-with-a-web-view"></a>Mejora de una notificación de inserción con una vista web
### <a name="what-is-a-web-view"></a>¿Qué es una vista web?
![WebView1][28]

Una vista web es un elemento emergente con contenido web. Este elemento emergente aparece cuando se hace clic en para el usuario final de hello en la notificación de inserción de Hola.
Una vista web le permite toohave más interacción con el usuario final de Hola.
También es Hola oportunidad toopresent un tooaction de llamada como almacén de tooApp de redirección, abrir una página web, enviar un correo electrónico, a partir de una búsqueda geolocalizados, etcetera...

### <a name="example-web-view"></a>Ejemplo: vista web
* Crear la campaña de inserción en la sección "Alcance" de Hola y asigne un nombre a la campaña.

![WebView2][29]

* Escribir el mensaje de Hola que va a aparecer en la notificación de Hola.
* Seleccione el tipo de contenido del anuncio de Hola como "web"

![WebView3][30]

### <a name="about-announcement-types"></a>Acerca de los tipos de anuncio:
* Solo notificación: es una notificación estándar simple. Lo que significa que, si un usuario hace clic en él, no aparecerá vista adicional, pero solo Hola acción asociada, se producirá tooit.
* Anuncio de texto: es una notificación que involucre a Hola usuario toohave un vistazo a una vista de texto.
* Anuncio de Web: es una notificación que involucre a Hola usuario toohave un vistazo a una vista web.
  Seleccione Hola contenido "Anuncio de Web".

> [!NOTE]
> cuando inserta una vista de web, siempre va acompañada de una notificación en primer lugar.

* Definir el contenido de web de hello (tras haber seleccionado el contenido de la presentación de web hello, aparecerá la subsección de hello, permitiéndole toodefine hello web ver el contenido que desee toobe muestra.)

![WebView4][31]

* Escribir el título de Hola que aparecerá en la parte superior de Hola de mensajes de bienvenida (opcional).
* Escriba el código HTML aquí.
* Haga clic en la edición de tooswitch de botón de modo de edición de origen de Hola y vea cómo funciona.
* Escribir contenido de Hola que va a aparecer en el botón de acción de hello (un botón de acción permite Hola aplicación toomake una acción específica como la apertura de una página de aplicación hello, redirigiendo tooa almacén o en cualquier tipo de orígenes que pueden proporcionar).
* Contenido de Hola de escritura que va a aparecer en el botón Salir de hello (haciendo clic en botón Salir de hello, vista de hello web desaparecerá).
* Resultado

![WebView5][32]

* usuario de Hola recibir una notificación de Hola y haga clic en él.
* vista de texto Hello aparece como un toointeract de usuario Hola permitiendo emergente con él.

<!--Image references-->
[1]: ./media/mobile-engagement-how-tos/First1.png
[2]: ./media/mobile-engagement-how-tos/First2.png
[3]: ./media/mobile-engagement-how-tos/First3.png
[4]: ./media/mobile-engagement-how-tos/First4.png
[5]: ./media/mobile-engagement-how-tos/First5.png
[6]: ./media/mobile-engagement-how-tos/First6.png
[7]: ./media/mobile-engagement-how-tos/First7.png
[8]: ./media/mobile-engagement-how-tos/Test1.png
[9]: ./media/mobile-engagement-how-tos/Test2.png
[10]: ./media/mobile-engagement-how-tos/Test3.png
[11]: ./media/mobile-engagement-how-tos/Personalize1.png
[12]: ./media/mobile-engagement-how-tos/Personalize2.png
[13]: ./media/mobile-engagement-how-tos/Personalize3.png
[14]: ./media/mobile-engagement-how-tos/Personalize4.png
[15]: ./media/mobile-engagement-how-tos/Differentiate1.png
[16]: ./media/mobile-engagement-how-tos/Differentiate2.png
[17]: ./media/mobile-engagement-how-tos/Differentiate3.png
[18]: ./media/mobile-engagement-how-tos/Schedule1.png
[19]: ./media/mobile-engagement-how-tos/Schedule2.png
[20]: ./media/mobile-engagement-how-tos/Schedule3.png
[21]: ./media/mobile-engagement-how-tos/TextView1.png
[22]: ./media/mobile-engagement-how-tos/TextView2.png
[23]: ./media/mobile-engagement-how-tos/TextView3.png
[24]: ./media/mobile-engagement-how-tos/TextView4.png
[25]: ./media/mobile-engagement-how-tos/TextView5.png
[26]: ./media/mobile-engagement-how-tos/TextView6.png
[27]: ./media/mobile-engagement-how-tos/TextView7.png
[28]: ./media/mobile-engagement-how-tos/WebView1.png
[29]: ./media/mobile-engagement-how-tos/WebView2.png
[30]: ./media/mobile-engagement-how-tos/WebView3.png
[31]: ./media/mobile-engagement-how-tos/WebView4.png
[32]: ./media/mobile-engagement-how-tos/WebView5.png

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

