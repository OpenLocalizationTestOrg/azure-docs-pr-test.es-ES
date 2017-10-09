---
title: "aaaAzure centros de notificaciones - directrices de diagnóstico"
description: "Directrices sobre cómo emite toodiagnose comunes con centros de notificaciones de Azure."
services: notification-hubs
documentationcenter: Mobile
author: ysxu
manager: erikre
editor: 
ms.assetid: b5c89a2a-63b8-46d2-bbed-924f5a4cce61
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: NA
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: e374278f2bfdfad36ba091e8846059cd184c17ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs---diagnosis-guidelines"></a>Centros de notificaciones de Azure: pautas de diagnóstico
## <a name="overview"></a>Información general
Una de las preguntas más frecuentes de hello recibimos una respuesta de los clientes de centros de notificaciones de Azure es cómo aparecen los toofigure out ¿por qué no verán una notificación enviada desde su aplicación de back-end en dispositivo de cliente de hello - dónde y porqué se han quitado las notificaciones y cómo toofix esto. En este artículo veremos Hola diversas razones por las notificaciones pueden quitar o no terminan en dispositivos de Hola. También se tratará a través de maneras en que puede analizar y averiguar la causa raíz de Hola. 

En primer lugar, resulta crítico toounderstand modo en que los centros de notificaciones de Azure inserta los dispositivos de toohello de notificaciones.
![][0]

En un flujo de notificación de envío típica, el mensaje Hola se envía desde hello **aplicación back-end** demasiado**concentrador de notificación de Azure (NH)** que a su vez hace algún procesamiento en todos los registros de hello teniendo en Hola cuenta había configurado etiquetas & toodetermine de expresiones de etiqueta "destino", es decir, todos los registros de Hola que necesitan la notificación de inserción de tooreceive Hola. Estos registros se pueden distribuir en cualquiera de nuestras plataformas compatibles o en todas ellas: iOS, Google, Windows, Windows Phone, Kindle y Baidu para Android de China. Una vez que se han establecido los destinos de hello, NH, a continuación, extrae las notificaciones, se dividen en varios lotes de los registros, específicas de la plataforma de dispositivo de toohello **servicio de notificación de inserción (PNS)** -p. ej., APNS de Apple, GCM para etcetera de Google. NH se autentica con hello que PNS respectivos basándose en credenciales de hello establecido en hello Portal clásico de Azure en la página Configurar centro de notificaciones de Hola. Hola PNS, a continuación, reenvía Hola notificaciones toohello respectivo **dispositivos cliente**. Se trata de plataforma de hello recomendada notificaciones de inserción de manera toodeliver y tenga en cuenta que la bifurcación final de Hola de entrega de notificaciones de tiene lugar entre Hola plataforma PNS y el dispositivo de Hola. Por lo tanto, hay cuatro componentes principales: *cliente*, *back-end de la aplicación*, *Azure Notification Hubs (NH)* y *servicios de notificación de inserción (PNS)*, y cualquiera de ellos puede provocar que se eliminen las notificaciones. Se puede encontrar más información sobre esta arquitectura en [Información general de Notification Hubs].

Toodeliver error notificaciones pueden ocurrir durante el saludo inicial fase que puede indicar un problema de configuración o de prueba/staging puede ocurrir en producción donde todos o algunos de Hola notificaciones puede ser quitaran que indica alguna aplicación más profunda o bien, el problema de patrón de mensajería. En la sección de hello, a continuación, veremos diversos escenarios de colocarlo notificaciones desde common tipo poco frecuentes de toohello, que algunos de los cuales es posible obvios y otros no tanta. 

## <a name="azure-notifications-hub-mis-configuration"></a>Error de configuración del Centro de notificaciones de Azure
Centros de notificaciones de Azure necesita tooauthenticate propio en el contexto de Hola de toohello del toosuccessfully capaz de enviar notificaciones del desarrollador de hello aplicación toobe PNS respectivos. Esto se logra al desarrollador de hello creando una cuenta de desarrollador con la plataforma correspondiente de hello (Google, Apple, etcetera de Windows) y, a continuación, registrar su aplicación donde obtener credenciales que necesitan toobe configurado en el portal de hello en notificación Sección de configuración de concentradores. Si ninguna notificación se realiza a través el primer paso se debe tooensure que se configuran las credenciales correctas de hello en hello centro de notificaciones que coincide con la aplicación hello crear en su cuenta de desarrollador específico de plataforma. Encontrará nuestro [tutoriales de introducción] toogo útil sobre este proceso de una manera de paso a paso. A continuación se indican algunos errores de configuración comunes:

1. **General**
   
    a) asegúrese de seguro de que el nombre del concentrador de notificación (sin errores ortográficos) es Hola mismo:
   
   * Donde va a registrar desde el cliente de hello, 
   * Donde va a enviar las notificaciones de back-end de hello,  
   * Donde se han configurado las credenciales PNS de Hola y 
   * Cuyas credenciales SAS configuradas en Hola back-end de hello y cliente. 
     
     b) asegúrese de seguro de que está usando las cadenas de configuración correcta de SAS de hello en el cliente de Hola y el back-end de aplicación de Hola. Como regla general, debe contar con hello **DefaultListenSharedAccessSignature** en el cliente de Hola y **DefaultFullSharedAccessSignature** en hello back-end de aplicación (que proporciona permiso toobe toosend capaz de notificación toohello NH)
2. **Configuración del Servicio de notificaciones push de Apple (APNS)**
   
    Debe mantener dos centros diferentes: uno para producción y otro para fines de prueba. Esto significa cargar certificado Hola que va toouse concentrador independiente de tooa de entorno de espacio aislado y certificado de hello que va toouse hub de producción tooa independiente. No intente distintos tipos de certificados toohello de tooupload mismo concentrador tal como puede dar lugar a errores de notificación línea hello hacia abajo. Si se encuentra en una posición donde se han cargado inadvertidamente diferentes tipos de certificado toohello mismo concentrador, se recomienda toodelete Hola hub- and inicio nueva. Si por algún motivo, no es capaz de toodelete concentrador de hello, a continuación, en hello muy menos, debe eliminar todos los registros existentes de Hola de concentrador de Hola. 
3. **Configuración del Servicio de mensajería en la nube de Google (GCM)** 
   
    a) Asegúrese de que ha habilitado "Google Cloud Messaging for Android" (Servicio de mensajería en la nube de Google para Android) en su proyecto de nube. 
   
    ![][2]
   
    b) asegúrese de, cree una clave de"servidor" mientras se obtienen las credenciales de hello qué NH utilizará tooauthenticate con GCM. 
   
    ![][3]
   
    c) asegúrese de Asegúrese de que ha configurado "Identificador de proyecto" en cliente de Hola que es una entidad totalmente numérica que puede obtener desde el panel de hello:
   
    ![][1]

## <a name="application-issues"></a>Problemas de la aplicación
1) **Etiquetas/expresiones de etiqueta**

Si está utilizando toosegment de expresiones de etiqueta o etiquetas de la audiencia, siempre es posible que cuando se envían notificaciones de hello, no hay ningún destino en la que se encontró basándose en expresiones de etiquetas o etiquetas de Hola que se especifica en la llamada de envío. Es mejor tooreview su tooensure de registros que no hay etiquetas que coinciden al enviar la notificación y, a continuación, compruebe la confirmación de notificación de hello solo desde clientes de hello con esos registros. Por ejemplo, Si todos los registros con NH se completaron con dice etiqueta "Política" y que está enviando una notificación con la etiqueta "Sports", no se envía tooany dispositivo. Un caso complejo podría incluir expresiones de etiqueta donde solo se registró con "Etiqueta A" O "Etiqueta B" pero cuando envía notificaciones, los destinatarios son "Etiqueta A && Etiqueta B". Hola diagnosticar automáticamente el siguiente de la sección de sugerencias, hay formas en el que puede revisar los registros junto con etiquetas de hello tienen. 

2) **Problemas de plantillas**

Si se utilizan plantillas, asegúrese de que está siguiendo las directrices de hello descritas en [instrucciones de la plantilla]. 

3) **Registros no válidos**

Suponiendo que se usaron Hola que centro de notificaciones se configuró correctamente y las expresiones de etiquetas/etiqueta correctamente resultante en Buscar Hola de destinos válidos notificaciones de hello toowhich necesitan toobe enviado, NH desencadena varios lotes de procesamiento en paralelo - cada lote enviar mensajes tooa conjunto de registros. 

> [!NOTE]
> Puesto que se hello de procesamiento en paralelo, no garantizamos orden hello en qué Hola se entregarán las notificaciones. 
> 
> 

Ahora el Centro de notificaciones de Azure está optimizado para un modelo de entrega de mensajes "una vez como máximo". Esto significa que se intente una desduplicación para que no hay notificaciones se entregan tooa dispositivo más de una vez. tooensure se examine los registros de Hola y asegúrese de que solo un mensaje se envía por identificador de dispositivo antes de toohello realmente envío de mensaje de Hola PNS. Como cada lote se envía toohello PNS, que a su vez está aceptando y validar los registros de hello, es posible que hello PNS detecta un error con uno o varios de los registros de hello en un lote, devuelve un tooAzure NH de error y detiene el procesamiento, por tanto, quitar procesar por lotes por completo. Esto ocurre así con APNS, que usa un protocolo de transmisión TCP. Aunque nos estamos optimizados una vez en la mayoría de entrega, en este caso quitamos Hola con errores registro de la base de datos y, a continuación, entrega de notificaciones de reintento de rest de Hola de dispositivos de hello en ese lote.

Puede obtener información de error de intento de error de la entrega de hello en un registro con hello API de REST de centros de notificaciones de Azure: [por mensaje de telemetría: obtener telemetría de mensaje de notificación](https://msdn.microsoft.com/library/azure/mt608135.aspx) y [PNS comentarios](https://msdn.microsoft.com/library/azure/mt705560.aspx). Vea hello [SendRESTExample](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/SendRestExample) por ejemplo de código.

## <a name="pns-issues"></a>Problemas del PNS
Una vez que ha recibido el mensaje de notificación de Hola Hola PNS respectivos es su dispositivo de toohello de notificación de responsabilidad toodeliver Hola. Centros de notificaciones de Azure está fuera de la imagen de hello aquí y cuando o si notificación Hola va toobe entregado toohello dispositivo no tiene ningún control. Puesto que Servicios de notificación de plataforma de hello son bastante sólidos, notificaciones suelen tooreach dispositivos de hello en unos pocos segundos de hello PNS. Si hello PNS sin embargo está limitando los centros de notificaciones de Azure aplique una estrategia de retroceso exponencial y si hello PNS permanece accesible durante 30 minutos, a continuación, tenemos una directiva en colocar tooexpire y eliminar permanentemente los mensajes. 

Si un PNS intenta toodeliver una notificación pero Hola dispositivo está desconectado, notificación de hello es almacenando hello PNS durante un período limitado de tiempo y entregan toohello dispositivo cuando esté disponible. Solo se almacena una notificación reciente de una aplicación en particular. Si varias notificaciones se envían mientras el dispositivo de hello está sin conexión, cada nueva notificación hace notificación previa de hello toobe descarta. Este comportamiento se debe mantener solo notificación más reciente de Hola de es que se hace referencia tooas fusión notificaciones en APN y contraer en GCM (que utiliza una clave contraída). Si el dispositivo de Hola permanece sin conexión durante mucho tiempo, se descartan las notificaciones que se va a almacenar para él. Origen: [Instrucciones para APNS] & [Instrucciones para GCM]

Con centros de notificaciones de Azure - puede pasar una clave de fusión a través de un encabezado HTTP con hello genérico `SendNotification` API (por ejemplo, para el SDK. NET: `SendNotificationAsync`) que también toma los encabezados HTTP que se pasan como es toohello PNS respectivos. 

## <a name="self-diagnose-tips"></a>Sugerencias de autodiagnóstico
Aquí examinaremos Hola distintos accesos toodiagnose y raíz causar ningún problema de centro de notificaciones:

### <a name="verify-credentials"></a>Comprobar las credenciales
1. **Portal para desarrolladores de PNS**
   
    Comprobarlos en hello respectivos PNS developer portal (APNS, GCM, WNS etcetera) mediante nuestro [tutoriales de introducción].
2. **Portal de Azure clásico**
   
    Vaya toohello configurar pestaña tooreview y coincidir con las credenciales de hello con los que se obtienen del portal para desarrolladores de hello PNS. 
   
    ![][4]

### <a name="verify-registrations"></a>Verificar los registros
1. **Visual Studio**
   
    Si usa Visual Studio para el desarrollo puede conectarse tooMicrosoft Azure y ver y administrar un grupo de servicios de Azure incluido el centro de notificaciones "Del explorador de servidores". Esto es especialmente útil para su entorno de desarrollo y prueba. 
   
    ![][9]
   
    Puede ver y administrar todos los registros de hello en el centro que se clasifican correctamente para la plataforma, nativo o plantilla de registro, las etiquetas, identificador PNS, fecha de expiración de hello y el Id. de registro. También puede editar un registro en marcha hello - lo que resulta útil diga si desea tooedit las etiquetas. 
   
    ![][8]
   
   > [!NOTE]
   > Registros de tooedit de funcionalidad de Visual Studio solo deben usarse durante el desarrollo y pruebas con un número limitado de registros. Si se produce una necesidad toofix los registros de forma masiva, tenga en cuenta con funcionalidad de registro de exportación/importación Hola descrita aquí - [registros de importación/exportación](https://msdn.microsoft.com/library/dn790624.aspx)
   > 
   > 
2. **Explorador de Bus de servicio**
   
    Muchos clientes usan el explorador de Bus de servicio que se describe en [Explorador de Bus de servicio] para ver y administrar sus centros de notificaciones. Se trata de un proyecto de código abierto disponible en code.microsoft.com, [Código del explorador de Bus de servicio]

### <a name="verify-message-notifications"></a>Comprobar las notificaciones de mensajes
1. **Portal de Azure clásico**
   
    Puede ir a toohello "Debug" pestaña toosend prueba notificaciones tooyour los clientes sin necesidad de cualquier servicio back-end de y en ejecución. 
   
    ![][7]
2. **Visual Studio**
   
    También puede enviar notificaciones de prueba desde comodidades Hola de Visual Studio:
   
    ![][10]
   
    Puede leer más en hello Azure de concentrador de notificación de Visual Studio funcionalidades del explorador de aquí: 
   
   * [Introducción al Explorador de servidores de VS]
   * [Entrada del blog del Explorador de servidores de VS - 1]
   * [Entrada del blog del Explorador de servidores de VS - 2]

### <a name="debug-failed-notifications-review-notification-outcome"></a>Depurar las notificaciones incorrectas y revisar el resultado de la notificación
**Propiedad EnableTestSend**

Cuando se envía una notificación a través de los centros de notificaciones, inicialmente solo obtiene en la cola para toodo NH toofigure out todos sus destinos de procesamiento y, a continuación, eventualmente NH lo envía toohello PNS. Esto significa que cuando se usa la API de REST o cualquiera de los SDK de cliente de hello, hello la devolución es correcta de su envío llamada único medio que Hola mensaje ha están correctamente en la cola con el centro de notificaciones. No da una idea en ¿qué ocurrió cuando NH finalmente obtuvo toosend Hola mensaje tooPNS. Si la notificación es no llegan al dispositivo de cliente de hello, hay una posibilidad de que, cuando NH prueba toodeliver Hola mensaje tooPNS, hubo un error, por ejemplo, el tamaño de carga Hola supera el máximo de hello permitido por hello PNS o credenciales de hello configuradas en NH son tooget etc. válida una información sobre errores PNS de hello, hemos introducido una propiedad denominada [EnableTestSend característica]. Esta propiedad se habilita automáticamente cuando se envía a prueba los mensajes del portal de Hola o el cliente de Visual Studio y, por tanto, le permite toosee detallada información de depuración. Puede utilizar esto a través de las API tomando el ejemplo hello de hello .NET SDK que está disponible ahora y será agregado tooall SDK de cliente al final. toouse con la llamada de REST de hello, basta con anexar un parámetro de cadena de consulta denominado por ejemplo, "test" al final de saludo de la llamada de envío 

    https://mynamespace.servicebus.windows.net/mynotificationhub/messages?api-version=2013-10&test

*Ejemplo (SDK para .NET)*

Imagine que está usando el SDK de .NET toosend una notificación del sistema nativo:

    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName);
    var result = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(result.State);

`result.State`le basta con estado `Enqueued` final Hola de ejecución de hello sin ninguna información sobre lo que ha ocurrido tooyour inserción. Ahora puede usar hello `EnableTestSend` propiedad booleana al inicializar hello `NotificationHubClient` y puede obtener el estado detallado de hello PNS han detectado errores al enviar notificación de Hola. aquí la llamada de envío de Hola tardará más tiempo tooreturn porque se devuelve sólo una vez NH ha entregado el resultado de hello notificación tooPNS toodetermine Hola. 

    bool enableTestSend = true;
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(connString, hubName, enableTestSend);

    var outcome = await hub.SendWindowsNativeNotificationAsync(toast);
    Console.WriteLine(outcome.State);

    foreach (RegistrationResult result in outcome.Results)
    {
        Console.WriteLine(result.ApplicationPlatform + "\n" + result.RegistrationId + "\n" + result.Outcome);
    }

*Salida de ejemplo*

    DetailedStateAvailable
    windows
    7619785862101227384-7840974832647865618-3
    hello Token obtained from hello Token Provider is wrong

Este mensaje indica las credenciales no válidas se configuran en el centro de notificaciones de Hola o un problema con los registros de hello en el concentrador de Hola y Hola recomienda curso se toodelete este registro y permiten cliente hello volver a crearla antes de enviar Hola Mensaje. 

> [!NOTE]
> Tenga en cuenta que uso Hola de esta propiedad muy limitado y por lo que sólo debe usar esto en el entorno de desarrollo y pruebas con un conjunto limitado de registros. Enviamos solo las notificaciones de depuración too10 dispositivos. También tenemos un límite de procesamiento de depuración envía toobe 10 por minuto. 
> 
> 

### <a name="review-telemetry"></a>Revisar la telemetría
1. **Uso del Portal de Azure clásico**
   
    Hola portal permite tooget una introducción rápida de todas las actividades de hello en el centro de notificaciones. 
   
    a) desde la pestaña de "panel" hello puede ver una vista agregada de los registros de hello, notificaciones, así como errores por plataforma. 
   
    ![][5]
   
    b) también puede agregar muchas otras métricas específicas de plataforma de Hola "Monitor" pestaña tootake minuciosos especialmente en los errores específicos de PNS devolvió cuando trate de NH toosend Hola notificación toohello PNS. 
   
    ![][6]
   
    c) que debe empezar revisando hello **los mensajes entrantes**, **las operaciones de registro**, **notificaciones correctas** y, a continuación, vaya Hola de tooper plataforma pestaña tooreview Errores específicos de PNS. 
   
    d) si tiene notificación Hola concentrador mal configurado con la configuración de autenticación de hello, a continuación, se mostrará el Error de autenticación de PNS. Se trata de un buen indicativo toocheck hello PNS de credenciales. 

2) **Acceso mediante programación**

Más detalles aquí: 

* [Acceso de telemetría mediante programación]
* [Ejemplo de acceso de telemetría mediante API] 

> [!NOTE]
> Varias características relacionadas con la telemetría, como **exportación e importación de registros**, **acceso a telemetría a través de API**, etc., están solamente disponibles en el nivel Estándar. Si intentas toouse estas características si se encuentra en nivel gratis o básico, a continuación, se obtendrá el efecto de toothis de mensaje de excepción al usar Hola SDK y un HTTP 403 (prohibido) cuando se usen directamente desde las API de REST de Hola. Asegúrese de que se ha movido tooStandard verticalmente a través del Portal de Azure clásico.  
> 
> 

<!-- IMAGES -->
[0]: ./media/notification-hubs-diagnosing/Architecture.png
[1]: ./media/notification-hubs-diagnosing/GCMConfigure.png
[2]: ./media/notification-hubs-diagnosing/GCMEnable.png
[3]: ./media/notification-hubs-diagnosing/GCMServerKey.png
[4]: ./media/notification-hubs-diagnosing/PortalConfigure.png
[5]: ./media/notification-hubs-diagnosing/PortalDashboard.png
[6]: ./media/notification-hubs-diagnosing/PortalMonitoring.png
[7]: ./media/notification-hubs-diagnosing/PortalTestNotification.png
[8]: ./media/notification-hubs-diagnosing/VSRegistrations.png
[9]: ./media/notification-hubs-diagnosing/VSServerExplorer.png
[10]: ./media/notification-hubs-diagnosing/VSTestNotification.png

<!-- LINKS -->
[Información general de Notification Hubs]: notification-hubs-push-notification-overview.md
[tutoriales de introducción]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[instrucciones de la plantilla]: https://msdn.microsoft.com/library/dn530748.aspx 
[Instrucciones para APNS]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW4
[Instrucciones para GCM]: http://developer.android.com/google/gcm/adv.html
[Export/Import Registrations]: http://msdn.microsoft.com/library/dn790624.aspx
[Explorador de Bus de servicio]: http://msdn.microsoft.com/library/dn530751.aspx
[Código del explorador de Bus de servicio]: https://code.msdn.microsoft.com/windowsazure/Service-Bus-Explorer-f2abca5a
[Introducción al Explorador de servidores de VS]: http://msdn.microsoft.com/library/windows/apps/xaml/dn792122.aspx 
[Entrada del blog del Explorador de servidores de VS - 1]: http://azure.microsoft.com/blog/2014/04/09/deep-dive-visual-studio-2013-update-2-rc-and-azure-sdk-2-3/#NotificationHubs 
[Entrada del blog del Explorador de servidores de VS - 2]: http://azure.microsoft.com/blog/2014/08/04/announcing-release-of-visual-studio-2013-update-3-and-azure-sdk-2-4/ 
[EnableTestSend característica]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.notificationhubclient.enabletestsend.aspx
[Acceso de telemetría mediante programación]: http://msdn.microsoft.com/library/azure/dn458823.aspx
[Ejemplo de acceso de telemetría mediante API]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel

