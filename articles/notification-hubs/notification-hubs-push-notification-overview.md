---
title: aaaAzure centros de notificaciones
description: "Obtenga información acerca de cómo tooadd push capacidades de notificación con centros de notificaciones de Azure."
author: ysxu
manager: erikre
editor: 
services: notification-hubs
documentationcenter: 
ms.assetid: fcfb0ce8-0e19-4fa8-b777-6b9f9cdda178
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 1/17/2017
ms.author: yuaxu
ms.openlocfilehash: 78ce34b6b094b560c8002ab9652f7ba4563c5c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs"></a>Centros de notificaciones de Azure
## <a name="overview"></a>Información general
Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente. Con una llamada de API sencilla multiplataforma, puede enviar fácilmente plataforma móvil de tooany de notificaciones de inserción de destino y personalizada desde cualquier back-end de nube o local.

Notification Hubs funciona muy bien tanto para escenarios empresariales como de consumidores. Estos son algunos ejemplos de para qué utilizan los clientes Notification Hubs:

* Enviar notificaciones toomillions de separación de noticias con una latencia baja.
* Envíe cupones basados en ubicación toointerested segmentos de usuarios.
* Enviar notificaciones relacionadas con el evento toousers o grupos de aplicaciones de medios/deportes/finance/juegos.
* Insertar contenido promocional tooapps tooengage y mercado toocustomers.
* Informar a los usuarios sobre eventos empresariales como, por ejemplo, nuevos mensajes o elementos de trabajo.
* Enviar códigos para Multi-Factor Authentication.

## <a name="what-are-push-notifications"></a>¿Qué son las notificaciones de inserción?
Las notificaciones push son una forma de comunicación de aplicación a usuario en la que los usuarios de aplicaciones móviles reciben una notificación con determinada información que desean, por lo general, en un cuadro de diálogo o una ventana emergente. Los usuarios normalmente pueden elegir tooview o descartar el mensaje de bienvenida, y elegir primero Hola se abrirá Hola aplicación móvil que les ha comunicado la notificación de Hola.

Las notificaciones push son vitales para las aplicaciones de consumidor, ya que aumentan el uso y la interacción de las aplicaciones, así como para las aplicaciones empresariales porque comunican información empresarial actualizada. Es mejor comunicación de aplicaciones para usuario Hola porque resulta eficaz para la energía para dispositivos móviles, flexibles para los remitentes de las notificaciones de Hola y de disponibilidad mientras las aplicaciones correspondientes no están activas.

Más información acerca de las notificaciones push de algunas plataformas populares:
* [iOS](https://developer.apple.com/notifications/)
* [Android](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [Windows](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a>Funcionamiento de las notificaciones de inserción
Las notificaciones push se entregan a través de unas infraestructuras específicas para la plataforma llamadas *Sistemas de notificación de plataforma* (PNS). Ofrecen las funcionalidades de inserción de equipos toodelivery dispositivo de tooa de mensajes con proporcionado controlar y no tienen ninguna interfaz común. toosend una notificación tooall clientes a través de hello iOS, Android y Windows versiones de una aplicación, desarrollador Hola debe trabajar con APNS (servicio de notificaciones Push de Apple), FCM (Firebase Cloud Messaging) y WNS (servicio de notificación de Windows), al procesamiento por lotes Hola se envía.

A continuación se muestra cómo funciona la inserción, a nivel general:

1. aplicación de cliente de Hello decide que desea tooreceive inserta, por tanto, Hola contactos correspondiente PNS tooretrieve su identificador único y temporal de inserción. tipo de identificador Hello depende de sistema de hello (por ejemplo, WNS tiene URI mientras APN tiene tokens).
2. aplicación de cliente de Hello almacena este identificador en el back-end de la aplicación de Hola o proveedor.
3. toosend una notificación de inserción, back-end de la aplicación de Hola se pone en contacto con hello PNS con tootarget de identificador hello en una aplicación de cliente específico.
4. Hola PNS reenvía el dispositivo de toohello de notificación de hello especificado por el identificador hello.

![][0]

## <a name="hello-challenges-of-push-notifications"></a>Hola desafíos de notificaciones de inserción
Mientras PNSes son eficaces, dejan el desarrollador de aplicaciones de trabajo toohello en orden tooimplement incluso inserción notificación escenarios comunes, como la difusión o enviar los usuarios de toosegmented de notificaciones de inserción.

Inserción es uno de hello solicitado más características de servicios de dispositivos móviles en la nube, porque su espacio de trabajo requiere infraestructuras complejas de lógica empresarial principal de la aplicación toohello no relacionados. Algunos de los desafíos de hello son:

* **Dependencia de la plataforma**: 

  * Hola back-end debe toohave compleja y difícil de mantener la lógica depende de la plataforma toosend notificaciones toodevices en varias plataformas como PNSes no están unificados.
* **Escala**:

  * Según las directrices de PNS, se deben actualizar los tokens de dispositivo cada vez que se inicia la aplicación. Esto significa Hola back-end se trabaja con una gran cantidad de tráfico y solo los tokens de hello tookeep actualizados de acceso de la base de datos. Cuando toohundreds y miles de millones, aumenta el número de Hola de dispositivos, el costo de Hola de crear y mantener esta infraestructura es masivo.
  * PNSes mayoría no son compatibles con dispositivos toomultiple difusión. Esto significa que una simple tooa difusión resultados de millones de dispositivos en llamadas de un millón toohello PNSes. El escalado de esta cantidad de tráfico con una latencia mínima no es algo trivial.
* **Enrutamiento**:
  
  * Aunque PNSes proporcionar un toodevices de mensajes de manera toosend, la mayoría de las notificaciones de aplicaciones se dirigen a los usuarios o grupos de interés. Esto significa Hola back-end debe mantener los dispositivos con grupos de interés, los usuarios, las propiedades, etcetera tooassociate del registro. Esta sobrecarga agrega costes de toomarket y el mantenimiento del tiempo de toohello de una aplicación.

## <a name="why-use-notification-hubs"></a>¿Por qué usar los Centros de notificaciones?
Notification Hubs elimina todas las complejidades asociadas con la habilitación de una inserción propia. Su infraestructura de notificaciones push multiplataforma y escalada horizontalmente reduce los códigos relativos a la inserción y simplifica el back-end. Con centros de notificaciones son simplemente responsables de registrar los controladores de PNS con un concentrador, mientras Hola back-end envía mensajes toousers o grupos de interés, como se muestra en la figura siguiente de Hola dispositivos:

![][1]

Centros de notificaciones es el motor de inserción listos para usar con hello siguientes ventajas:

* **Multiplataforma**

  * Compatibilidad para las principales plataformas push incluidos iOS, Android, Windows, Kindle y Baidu.
  * Una interfaz toopush tooall plataformas comunes en formatos específicos de la plataforma o independiente de la plataforma con ningún tipo de trabajo específico de la plataforma.
  * Administración de controladores de dispositivos en un único lugar.
* **Back-ends cruzados**
  
  * En la nube o local
  * .NET, Node.js, Java, etc.
* **Conjunto completo de patrones de entrega**:

  * *Difusión tooone o varias plataformas*: al instante puede difundir toomillions de dispositivos entre plataformas con una sola llamada API.
  * *Insertar toodevice*: puede tener como destino dispositivos de tooindividual de notificaciones.
  * *Insertar toouser*: características de etiquetas y plantillas le ayudarán a llegar a todos los dispositivos multiplataforma de un usuario.
  * *Insertar toosegment con etiquetas dinámicas*: característica etiquetas le ayuda a segmentar dispositivos e insertar toothem según las necesidades tooyour, si va a enviar el segmento de tooone o una expresión de segmentos (p. ej. active AND reside en Seattle no nuevo usuario). En lugar de ser toopub-sub restringido, puede actualizar las etiquetas del dispositivo en cualquier lugar y en cualquier momento.
  * *Inserción localizada*: la característica de plantillas le ayuda a obtener la localización sin alterar el código de back-end.
  * *Inserción silenciosa*: puede permite patrón de inserción para la extracción de hello enviando notificaciones silenciosa toodevices y desencadenar ellos toocomplete determinados extrae o acciones.
  * *Programado inserción*: puede programar toosend notificaciones en cualquier momento.
  * *Dirigir inserción*: puede omitir el registro dispositivos con nuestro servicio y directamente tooa lista de inserción de lote de controladores de dispositivo.
  * *Inserción personalizada*: las variables de inserción de dispositivo le ayudan a enviar notificaciones push personalizadas específicas de dispositivo con pares de clave-valor personalizados.
* **Telemetría enriquecida**
  
  * Telemetría general de inserción, dispositivo, error y operación está disponible en hello portal de Azure y mediante programación.
  * Por cada mensaje telemetría pistas cada inserción desde el servicio de tooour de llamada de solicitud inicial correctamente procesamiento por lotes Hola emite.
  * Comentarios de sistema de notificación de plataforma se comunica a todos los comentarios de tooassist de sistemas de notificación de plataforma en la depuración.
* **Escalabilidad** 
  
  * Enviar mensajes rápida toomillions de dispositivos sin tener que volver a diseñar o dispositivo particionamiento.
* **Seguridad**

  * Firma de acceso compartido (SAS) o autenticación federada.

## <a name="integration-with-app-service-mobile-apps"></a>Integración con las Aplicaciones móviles del Servicio de aplicaciones
una experiencia perfecta y unificador a través de servicios de Azure, toofacilitate [aplicación del servicio de aplicaciones móviles] tiene compatibilidad integrada para las notificaciones de inserción con centros de notificaciones. [aplicación del servicio de aplicaciones móviles] ofrece una plataforma de desarrollo de aplicaciones móviles muy escalable, que están disponibles globalmente para los desarrolladores empresariales y los integradores que ofrece un amplio conjunto de capacidades toomobile a los desarrolladores.

Los desarrolladores de aplicaciones móviles pueden utilizar los centros de notificaciones con hello siguiendo el flujo de trabajo:

1. Recuperar controlador PNS de dispositivo
2. Registrar el dispositivo con Notification Hubs a través de la API adecuada del registro del SDK de cliente de Mobile Apps
   * Tenga en cuenta que las aplicaciones móviles eliminan todas las etiquetas en los registros por motivos de seguridad. Trabajar con los centros de notificaciones desde el back-end directamente tooassociate etiquetas con dispositivos.
3. Enviar notificaciones desde su back-end de aplicación con los centros de notificaciones

Estos son algunos comodidades poner toodevelopers con esta integración:

* **SDK de cliente de aplicaciones móviles**: estos SDK multiplataformas proporcionan API simples para el registro y hablar centro de notificaciones toohello vinculada con la aplicación móvil de hello automáticamente. Los desarrolladores no necesitan toodig a través de las credenciales de los centros de notificaciones y trabajar con un servicio adicional.

  * *Insertar toouser*: Hola SDK etiqueta automáticamente hello tiene dispositivos con aplicaciones móviles autenticados Id. de usuario tooenable toouser caso de la inserción.
  * *Insertar toodevice*: Hola SDK automáticamente usar hello identificador de instalación de aplicaciones móviles como GUID tooregister con centros de notificaciones, ahorrar a los desarrolladores problemas Hola de mantener varios GUID de servicio.
* **Modelo de instalación**: aplicaciones móviles funciona con última inserción modelo toorepresent los centros de notificaciones todas las propiedades asociadas a un dispositivo en una instalación de JSON que se alinea con los servicios de notificación de inserción y es fácil toouse de inserción.
* **Flexibilidad**: los desarrolladores pueden elegir siempre toowork con centros de notificaciones directamente incluso con la integración de hello en su lugar.
* **Experiencia en integrada [portal de Azure]**: inserción como una capacidad se representa visualmente en aplicaciones móviles y los desarrolladores pueden trabajar fácilmente con el centro de notificaciones asociada de Hola a través de aplicaciones móviles.

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de los Centros de notificaciones en estos temas:

* **[Cómo utilizan los clientes los Notification Hubs]**
* **[Tutoriales y guías sobre los Notification Hubs]**
* **Tutoriales de introducción sobre los Notification Hubs**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS] y [Xamarin.Android]

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
[Cómo utilizan los clientes los Notification Hubs]: http://azure.microsoft.com/services/notification-hubs
[Tutoriales y guías sobre los Notification Hubs]: http://azure.microsoft.com/documentation/services/notification-hubs
[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started
[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started
[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started
[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started
[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started
[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started
[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
[aplicación del servicio de aplicaciones móviles]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/
[templates]: notification-hubs-templates-cross-platform-push-messages.md
[portal de Azure]: https://portal.azure.com
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)
