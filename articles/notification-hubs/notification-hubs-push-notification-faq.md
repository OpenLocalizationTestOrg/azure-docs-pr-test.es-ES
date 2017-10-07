---
title: "Azure Notification Hubs: preguntas más frecuentes (P+F) | Microsoft Docs"
description: "Preguntas más frecuentes sobre el diseño y la implementación de soluciones en los Centros de notificaciones"
services: notification-hubs
documentationcenter: mobile
author: ysxu
manager: erikre
keywords: "notificación push, notificaciones push, notificaciones push de iOS, notificaciones push de android, inserción de ios, inserción de android"
editor: 
ms.assetid: 7b385713-ef3b-4f01-8b1f-ffe3690bbd40
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 01/19/2017
ms.author: yuaxu
ms.openlocfilehash: a70efa7fc5954966847d5a173e9b10accf4b737e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="push-notifications-with-azure-notification-hubs-frequently-asked-questions"></a>Notificaciones push en Azure Notification Hubs: preguntas más frecuentes
## <a name="general"></a>General
### <a name="what-is-hello-resource-structure-of-notification-hubs"></a>¿Cuál es la estructura de los recursos Hola de centros de notificaciones?

Azure Notification Hubs tiene dos niveles de recursos, concentradores y espacios de nombres. Un concentrador es un recurso de inserción que puede contener información de inserción de multiplataforma Hola de una aplicación. Un espacio de nombres es una colección de concentradores en una región.

La asignación recomendada hace coincidir un espacio de nombres con una aplicación. Dentro de un espacio de nombres, puede tener un concentrador de producción que funcione con la aplicación de producción, un concentrador de prueba que funcione con la aplicación de prueba, etc.

### <a name="what-is-hello-price-model-for-notification-hubs"></a>¿Qué es el modelo de precios de hello centrales de notificaciones?
Hello detalles de precios más reciente se encuentra en hello [los precios de notificación] página. Los centros de notificaciones se factura a nivel de espacio de nombres de Hola. (Para la definición de Hola de un espacio de nombres, vea "¿Cuál es la estructura de los recursos de centros de notificaciones Hola?") Los centros de notificaciones ofrece tres niveles:

* **Gratis**: Este nivel es un buen punto de partida para explorar las funcionalidades de inserción. No se recomienda para las aplicaciones de producción. Se incluyen 500 dispositivos y 1 millón de inserciones por espacio de nombres por mes, sin garantía de Acuerdo de Nivel de Servicio (SLA).
* **Básico**: este nivel (o el nivel estándar de Hola) se recomienda para las aplicaciones de producción más pequeñas. Se incluyen 200 000 dispositivos y 10 millones de inserciones por espacio de nombres por mes como línea base. Se incluyen opciones de aumento con cuota.
* **Estándar**: se recomienda este nivel para aplicaciones de producción de toolarge intermedio. Se incluyen 10 millones de dispositivos y 10 millones de inserciones por espacio de nombres por mes como línea base. Se incluyen opciones de aumento con cuota y funcionalidades de telemetría enriquecida.

Características del nivel Estándar:
* **Telemetría completa**: puede usar los centros de notificaciones por mensaje telemetría tootrack cualquiera insertar las solicitudes y comentarios de sistema de notificación de plataforma para la depuración.
* **Multiinquilinato**: Puede trabajar con credenciales del Sistema de notificación de plataforma a nivel de un espacio de nombres. Esta opción permite tooeasily divide los inquilinos en centros de hello mismo espacio de nombres.
* **Programado inserción**: puede programar toobe de notificaciones que se envíen en cualquier momento.

### <a name="what-is-hello-notification-hubs-sla"></a>¿Qué es hello SLA de los centros de notificaciones?
Para los niveles básico y estándar de los centros de notificaciones, aplicaciones configuradas correctamente pueden enviar notificaciones de inserción o realizar operaciones de administración de registro al menos un 99,9% de tiempo de Hola. más información acerca de los SLA de hello, vaya toohello toolearn [SLA de los centros de notificaciones](https://azure.microsoft.com/support/legal/sla/notification-hubs/) página.

> [!NOTE]
> Dado que las notificaciones de inserción dependen de los sistemas de notificación de plataforma de aplicaciones de terceros (por ejemplo, APNS de Apple y Google FCM), no hay ninguna garantía de SLA para la entrega de Hola de estos mensajes. Después de los centros de notificaciones envía lotes Hola sistemas de notificación de tooPlatform (SLA garantizada), es responsabilidad de Hola de Hola Hola de toodeliver de sistemas de notificación de plataforma inserta (no se garantiza que ningún SLA).

### <a name="which-customers-are-using-notification-hubs"></a>¿Qué clientes utilizan los Centros de notificaciones?
Muchos clientes usan Notification Hubs. Los siguientes son algunos clientes destacados:

* Sochi 2014: cientos de grupos de interés, más de 3 millones de dispositivos y más de 150 millones de notificaciones enviadas en dos semanas. [Caso práctico: Sochi]
* Skanska. [Caso práctico: Skanska]
* Seattle Times. [Caso práctico: Seattle Times]
* Mural.ly. [Caso práctico: Mural.ly]
* 7Digital. [Caso práctico: 7Digital]
* Aplicaciones de Bing: decenas de millones de dispositivos envían 3 millones de notificaciones al día.

### <a name="how-do-i-upgrade-or-downgrade-my-hub-or-namespace-tooa-different-tier"></a>¿Cómo se puede actualizar o degradar el concentrador o espacio de nombres tooa otro nivel?
Vaya toohello  **[portal de Azure]** > **espacios de nombres de los centros de notificaciones** o **centros de notificaciones**. Seleccione el recurso de Hola que desee tooupdate y vaya demasiado**tarifa**. Tenga en cuenta Hola según los requisitos:

* Hello tarifa actualizada se aplica demasiado*todos los* centros de espacio de nombres de hello trabaja con.
* Si el número de dispositivos supera el límite de Hola de capa de hello a que va degradar, debe toodelete dispositivos antes de cambiar.


## <a name="design-and-development"></a>Diseño y desarrollo
### <a name="which-server-side-platforms-do-you-support"></a>¿Qué plataformas de servicio se admiten?
Hay SDK de servidor para .NET, Java, Node.js, PHP y Python. Las API de Notification Hubs se basan en interfaces REST, por lo que puede trabajar directamente con las API de REST si usa distintas plataformas o no desea una dependencia adicional. Para obtener más información, visite toohello [API de REST de centros de notificaciones] página.

### <a name="which-client-platforms-do-you-support"></a>¿Qué plataformas de cliente se admiten?
Las notificaciones push son compatibles con [iOS](notification-hubs-ios-apple-push-notification-apns-get-started.md), [Android](notification-hubs-android-push-notification-google-gcm-get-started.md), [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), [Windows Phone](notification-hubs-windows-mobile-push-notifications-mpns.md), [Kindle](notification-hubs-kindle-amazon-adm-push-notification.md), [Android China (con Baidu)](notification-hubs-baidu-china-android-notifications-get-started.md), Xamarin ([iOS](xamarin-notification-hubs-ios-push-notification-apns-get-started.md) y [Android](xamarin-notification-hubs-push-notifications-android-gcm.md)), [Chrome Apps](notification-hubs-chrome-push-notifications-get-started.md) y [Safari](https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSafari). Para obtener más información, visite toohello [notificación Introducción a concentradores tutoriales] página.

### <a name="do-you-support-text-message-email-or-web-notifications"></a>¿Se admiten notificaciones por mensaje de texto, correo electrónico o web?
Los centros de notificaciones es principalmente diseñada toosend notificaciones toomobile aplicaciones. No ofrece funcionalidades de correo electrónico ni mensaje de texto. Sin embargo, plataformas de terceros que proporcionan estas funciones se pueden integrar con las notificaciones de inserción nativa de los centros de notificaciones toosend mediante [aplicaciones móviles].

También centros de notificaciones no proporciona un servicio de entrega de notificación de inserción en el explorador desde el principio de Hola. Los clientes pueden implementar esta característica con SignalR sobre Hola admitida plataformas de servidor. Si desea toosend notificaciones toobrowser aplicaciones en espacio aislado de Chrome hello, vea hello [tutorial Chrome aplicaciones].

### <a name="how-are-mobile-apps-and-azure-notification-hubs-related-and-when-do-i-use-them"></a>¿Cómo se relacionan Mobile Apps y Azure Notification Hubs y cuándo las uso?
Si dispone de una móviles Finalizar aplicación nuevo y desea que las notificaciones de inserción del toosend capacidad de la hello tooadd solo, puede usar los centros de notificaciones de Azure. Si desea tooset el back-end de aplicación móvil desde el principio, considere el uso de la característica de aplicaciones móviles de Hola de servicio de aplicaciones de Azure. Una aplicación móvil proporciona automáticamente un centro de notificaciones para que pueda enviar fácilmente notificaciones de inserción de back-end de aplicación móvil de Hola. Precios de aplicaciones móviles incluyen los cargos de base de Hola de un centro de notificaciones. Se paga solo cuando supera Hola incluida inserta. Para obtener más detalles sobre los costos, visite toohello [precios del servicio de aplicación] página.

### <a name="how-many-devices-can-i-support-if-i-send-push-notifications-via-notification-hubs"></a>¿Cuántos dispositivos puedo admitir si envío notificaciones push a través de los Centros de notificaciones?
Consulte toohello [los precios de notificación] para obtener detalles sobre el número de Hola de dispositivos compatibles.

Si necesita compatibilidad con más de 10 millones de dispositivos registrados, [póngase en contacto con nosotros](https://azure.microsoft.com/overview/contact-us/) directamente y le ayudaremos a escalar su solución.

### <a name="how-many-push-notifications-can-i-send-out"></a>¿Cuántas notificaciones de inserción puedo enviar?
Según el nivel seleccionado de hello, centros de notificaciones de Azure automáticamente se amplía en función de número de Hola de notificaciones que fluyen a través del sistema de Hola.

> [!NOTE]
> Hello costo de uso general puede aumentar según Hola número de notificaciones de inserción servirlo. Asegúrese de que es consciente de los límites de la capa de hello descritos en hello [los precios de notificación] página.
> 
> 

Nuestros clientes utilizan los centros de notificaciones toosend millones de notificaciones de inserción diariamente. No es necesario toodo nada especial tooscale Hola alcanzar de las notificaciones de inserción mientras utilizas centros de notificaciones de Azure.

### <a name="how-long-does-it-take-for-sent-push-notifications-tooreach-my-device"></a>¿Cuánto toman para enviar tooreach de notificaciones de inserción mi dispositivo?
En un escenario de uso normal, que carga entrante hello es coherente e incluso, centros de notificaciones de Azure pueden procesar al menos *notificación de inserción de 1 millón envía un minuto*. Esta velocidad puede variar según el número de Hola de etiquetas, la naturaleza de Hola de Hola entrantes envía y otros factores externos.

Durante el tiempo de entrega de hello estimado, servicio de hello calcula destinos Hola por cada plataforma y los enruta toohello mensajes servicio de notificación de inserción (PNS) en función de las expresiones de etiqueta o etiquetas de hello registrado. Es responsabilidad de hello de dispositivo de hello PNS toosend notificaciones toohello.

Hola PNS no garantiza que los SLA para entregar las notificaciones. Sin embargo, la mayoría de las notificaciones de inserción se entregan tootarget dispositivos dentro de unos minutos (normalmente tarda 10 minutos) de tiempo Hola enviarlos tooNotification concentradores. Algunas notificaciones podrían tardar más.

> [!NOTE]
> Centros de notificaciones de Azure tiene una directiva en lugar toodrop las notificaciones de inserción que no se entregan toohello PNS dentro de 30 minutos. Este retraso puede deberse a una serie de motivos, pero la mayoría habitualmente porque hello PNS está limitando la aplicación.
> 
> 

### <a name="is-there-any-latency-guarantee"></a>¿Hay alguna garantía de latencia?
Debido a la naturaleza de Hola de notificaciones de inserción (que se entregan por un PNS externa, específica de la plataforma), no hay ninguna garantía de latencia. Por lo general, la mayoría de Hola de notificaciones de inserción se entregan dentro de unos minutos.

### <a name="what-do-i-need-tooconsider-when-designing-a-solution-with-namespaces-and-notification-hubs"></a>¿Qué necesito tooconsider al diseñar una solución con los centros de espacios de nombres y notificación?
#### <a name="mobile-appenvironment"></a>Entorno/aplicación móvil
* Use un centro de notificaciones por aplicación móvil por entorno.
* En un escenario multiinquilino, cada inquilino debe tener un centro independiente.
* Nunca el recurso compartido de Hola mismo centro de notificaciones para entornos de producción y pruebas. Si lo hace, podría tener problemas al enviar notificaciones. (Apple ofrece puntos de conexión de inserción de producción y espacio aislado, cada uno con credenciales independientes).
* De forma predeterminada, puede enviar prueba notificaciones tooyour registrado dispositivos a través del portal de Azure de Hola o hello Azure componente integrado en Visual Studio. umbral de Hola se establece too10 dispositivos que se seleccionan aleatoriamente de grupo de registro de hello.

> [!NOTE]
> Si el concentrador se configuró originalmente con un certificado de espacio aislado de Apple y, a continuación, era toouse ha vuelto a configurar un certificado de producción de Apple, tokens de dispositivo de hello original no son válidos. Tokens no válidos hacer inserciones toofail. Separe los entornos de producción y prueba y use centros distintos para entornos diferentes.
> 
> 

#### <a name="pns-credentials"></a>Credenciales PNS:
Cuando una aplicación móvil se registra con un portal para desarrolladores de una plataforma (por ejemplo, Apple o Google), se envían tokens de seguridad y un identificador de aplicación. Hola aplicación back-end proporciona estos PNS tokens toohello plataforma para que se pueden enviar notificaciones de inserción toodevices. Tokens de seguridad pueden ser en forma de Hola de certificados (por ejemplo, Apple iOS o Windows Phone) o las claves de seguridad (por ejemplo, Google Android o Windows). Se deben configurar en los centros de notificaciones. Configuración normalmente se realiza en el nivel del centro de notificaciones de hello, pero también puede realizarse en el nivel de espacio de nombres de hello en un escenario de varios inquilinos.

#### <a name="namespaces"></a>Espacios de nombres
Los espacios de nombres pueden usarse para la agrupación de implementación. También pueden ser utilizado toorepresent todos los centros de notificaciones para todos los inquilinos de Hola la misma aplicación en un escenario de varios inquilinos.

#### <a name="geo-distribution"></a>Distribución geográfica
La distribución geográfica no siempre es fundamental en el caso de las notificaciones push. No se distribuyen por varios PNSes (por ejemplo, APNS o GCM) que ofrecen toodevices de notificaciones de inserción.

Si tiene una aplicación que se usa de forma global, puede crear concentradores en diferentes espacios de nombres mediante el servicio de centros de notificaciones de hello en diferentes regiones de Azure alrededor de Hola a todos.

> [!NOTE]
> No se recomienda esta disposición porque aumenta el costo de administración, en especial para los registros. Solo se debe hacer si es explícitamente necesario.
> 
> 

### <a name="should-i-do-registrations-from-hello-app-back-end-or-directly-through-client-devices"></a>¿Hago registros de back-end de aplicación de Hola o directamente a través del cliente de dispositivos?
Registros de hello aplicación back-end son útiles cuando hay clientes tooauthenticate antes de crear el registro de hello. También resultan útiles si tiene etiquetas que se deben crear o modificar Hola aplicación back-end basado en lógica de aplicación. Para obtener más información, visite toohello [instrucciones de registro de back-end] y [instrucciones de registro de back-end 2] páginas.

### <a name="what-is-hello-push-notification-delivery-security-model"></a>¿Qué es el modelo de seguridad de entrega de notificación de inserción de hello?
Azure Notification Hubs usa un modelo de seguridad basado en [firma de acceso compartido](../storage/common/storage-dotnet-shared-access-signature-part-1.md). Puede usar tokens de firma de acceso compartido de hello en el nivel de espacio de nombres de raíz de Hola o en el nivel de concentrador de notificación específico de Hola. Tokens de firma de acceso compartido pueden ser toofollow en el conjunto de reglas de autorización diferentes, por ejemplo, los permisos de los mensajes toosend o toolisten para permisos de notificaciones. Para obtener más información, vea hello [modelo de seguridad de los centros de notificaciones] documento.

### <a name="how-should-i-handle-sensitive-payload-in-push-notifications"></a>¿Cómo debo controlar la carga confidencial de las notificaciones push?
Todas las notificaciones se entregan tootarget dispositivos por PNS la plataforma de hello. Cuando se envía una notificación tooAzure centros de notificaciones, se procesa y pasa toohello PNS respectivos.

Todas las conexiones, de hello remitente toohello centros de notificaciones de Azure toohello PNS, utilicen HTTPS.

> [!NOTE]
> Centros de notificaciones de Azure no registra carga Hola de mensajes de ninguna manera.
> 
> 

toosend cargas confidenciales, se recomienda utilizar un patrón de seguros de inserción. remitente de Hello entrega una notificación de ping con un dispositivo de toohello de identificador de mensaje sin carga confidencial Hola. Cuando la aplicación hello en dispositivo Hola recibe carga hello, aplicación hello llama a una API segura directamente toofetch Hola detalles del mensaje. Para obtener una guía sobre cómo tooimplement este patrón, vaya toohello [notificación concentradores seguros Push tutorial] página.

## <a name="operations"></a>Operaciones
### <a name="what-support-is-provided-for-disaster-recovery"></a>¿Qué compatibilidad se proporciona para la recuperación ante desastres?
Cobertura de recuperación ante desastres de metadatos se proporciona por nuestra parte (nombre de los centros de notificaciones de hello, cadena de conexión de Hola y otra información crítica). Cuando se desencadena un escenario de recuperación ante desastres, datos de registro están hello *sólo segmento* de la infraestructura de los centros de notificaciones de Hola que se pierde. Necesitará tooimplement un toorepopulate solución estos datos en la recuperación de posterior a la base de datos central nueva:

1. Cree un centro de notificaciones secundario en otro centro de datos. Se recomienda crear uno de hello principio tooshield desde un evento de recuperación ante desastres que podría afectar a sus capacidades de administración. También puede crear uno en tiempo de Hola de Hola de recuperación ante desastres.

2. Rellenar el centro de notificaciones secundaria de hello con registros de Hola desde el centro de notificaciones principal. No recomienda intentar toomaintain registros en ambos centros y mantenerlos sincronizados como registros vienen en. Esta práctica no funciona correctamente debido a la tendencia inherente Hola de registros tooexpire en hello lado PNS. Notification Hubs los limpia cuando recibe informaciones del PNS con respecto a los registros expirados o no válidos.  

Hay dos recomendaciones para los back-ends de aplicación:

* Use un back-end de aplicación que mantiene un conjunto determinado de registros en su extremo. A continuación, puede realizar una inserción masiva en el centro de notificaciones secundaria de Hola.

* Usar un back-end aplicación que obtiene un volcado normal de los registros del centro de notificaciones principal de hello como una copia de seguridad. A continuación, puede realizar una inserción masiva en el centro de notificaciones secundaria de Hola.

> [!NOTE]
> Se describe la funcionalidad de exportación/importación de registros disponible en el nivel estándar de Hola en hello [registros de exportación/importación] documento.
> 
> 

Si no tienes un back-end, cuando se inicia aplicación hello en dispositivos de destino, realizan un nuevo registro en el centro de notificaciones secundaria de Hola. Finalmente hello centro de notificaciones secundaria tendrá todos los dispositivos activos que Hola registrados.

Habrá un período en el que los dispositivos que no tengan aplicaciones abiertas no recibirán notificaciones.

### <a name="is-there-audit-log-capability"></a>¿Hay alguna funcionalidad de registro de auditoría?
Todas las operaciones de administración de centros de notificaciones vaya toooperation registros, que se exponen en hello [portal de Azure clásico].

## <a name="monitoring-and-troubleshooting"></a>Supervisión y solución de problemas
### <a name="what-troubleshooting-capabilities-are-available"></a>¿Qué funcionalidades de solución de problemas hay disponibles?
Centros de notificaciones de Azure proporciona varias características para solucionar problemas, especialmente para el escenario más común de Hola de notificaciones colocarlo. Para obtener más información, vea hello [solución de problemas de los centros de notificaciones] notas del producto.

### <a name="what-telemetry-features-are-available"></a>¿Qué características de telemetría hay disponibles?
Azure de centros de notificaciones de permite ver los datos de telemetría en hello [portal de Azure clásico]. Están los detalles de las métricas de hello en hello [las métricas de los centros de notificaciones] página.

> [!NOTE]
> Notificaciones correctas simplemente significan que las notificaciones de inserción se han entregado toohello externo PNS (por ejemplo, APNS de Apple) o GCM de Google. Es responsabilidad de Hola de dispositivos de tootarget de notificaciones de hello PNS toodeliver Hola. Por lo general, hello PNS no expone las partes toothird de las métricas de entrega.  
> 
> 

También se proporcionan los datos de telemetría de hello capacidad tooexport hello mediante programación (en el nivel de estándar de hello). Para obtener más información, vea hello [muestra las métricas de bases de datos centrales de notificación].

[portal de Azure clásico]: https://manage.windowsazure.com
[los precios de notificación]: http://azure.microsoft.com/pricing/details/notification-hubs/
[Notification Hubs SLA]: http://azure.microsoft.com/support/legal/sla/
[Caso práctico: Sochi]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=7942
[Caso práctico: Skanska]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5847
[Caso práctico: Seattle Times]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=8354
[Caso práctico: Mural.ly]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=11592
[Caso práctico: 7Digital]: https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=3684
[API de REST de centros de notificaciones]: https://msdn.microsoft.com/library/azure/dn530746.aspx
[notificación Introducción a concentradores tutoriales]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[tutorial Chrome aplicaciones]: http://azure.microsoft.com/documentation/articles/notification-hubs-chrome-get-started/
[Mobile Services Pricing]: http://azure.microsoft.com/pricing/details/mobile-services/
[instrucciones de registro de back-end]: https://msdn.microsoft.com/library/azure/dn743807.aspx
[instrucciones de registro de back-end 2]: https://msdn.microsoft.com/library/azure/dn530747.aspx
[modelo de seguridad de los centros de notificaciones]: https://msdn.microsoft.com/library/azure/dn495373.aspx
[notificación concentradores seguros Push tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-aspnet-backend-ios-secure-push/
[solución de problemas de los centros de notificaciones]: http://azure.microsoft.com/documentation/articles/notification-hubs-diagnosing/
[las métricas de los centros de notificaciones]: https://msdn.microsoft.com/library/dn458822.aspx
[muestra las métricas de bases de datos centrales de notificación]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/FetchNHTelemetryInExcel
[registros de exportación/importación]: https://msdn.microsoft.com/library/dn790624.aspx
[portal de Azure]: https://portal.azure.com
[complete samples]: https://github.com/Azure/azure-notificationhubs-samples
[aplicaciones móviles]: https://azure.microsoft.com/services/app-service/mobile/
[precios del servicio de aplicación]: https://azure.microsoft.com/pricing/details/app-service/
