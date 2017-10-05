---
title: Centros de notificaciones de Azure
description: "Aprenda a agregar funcionalidades de notificación push con Azure Notification Hubs."
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
ms.openlocfilehash: a1be0b13cd1feb582a23965df142e44d90ac6851
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs"></a><span data-ttu-id="d15ed-103">Centros de notificaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="d15ed-103">Azure Notification Hubs</span></span>
## <a name="overview"></a><span data-ttu-id="d15ed-104">Información general</span><span class="sxs-lookup"><span data-stu-id="d15ed-104">Overview</span></span>
<span data-ttu-id="d15ed-105">Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="d15ed-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="d15ed-106">Con una única llamada de API multiplataforma puede enviar fácilmente notificaciones push específicas y personalizadas a cualquier plataforma móvil desde cualquier back-end local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="d15ed-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

<span data-ttu-id="d15ed-107">Notification Hubs funciona muy bien tanto para escenarios empresariales como de consumidores.</span><span class="sxs-lookup"><span data-stu-id="d15ed-107">Notification Hubs works great for both enterprise and consumer scenarios.</span></span> <span data-ttu-id="d15ed-108">Estos son algunos ejemplos de para qué utilizan los clientes Notification Hubs:</span><span class="sxs-lookup"><span data-stu-id="d15ed-108">Here are a few examples customers use Notification Hubs for:</span></span>

* <span data-ttu-id="d15ed-109">Enviar notificaciones de noticias de última hora a millones de usuarios con baja latencia.</span><span class="sxs-lookup"><span data-stu-id="d15ed-109">Send breaking news notifications to millions with low latency.</span></span>
* <span data-ttu-id="d15ed-110">Enviar cupones basados en la ubicación a segmentos de usuarios interesados.</span><span class="sxs-lookup"><span data-stu-id="d15ed-110">Send location-based coupons to interested user segments.</span></span>
* <span data-ttu-id="d15ed-111">Enviar notificaciones relacionadas con eventos a usuarios o grupos para aplicaciones de medios, deportivas, de finanzas o de juegos.</span><span class="sxs-lookup"><span data-stu-id="d15ed-111">Send event-related notifications to users or groups for media/sports/finance/gaming applications.</span></span>
* <span data-ttu-id="d15ed-112">Insertar contenido promocional en aplicaciones para ponerse en contacto y comercializar con clientes.</span><span class="sxs-lookup"><span data-stu-id="d15ed-112">Push promotional contents to apps to engage and market to customers.</span></span>
* <span data-ttu-id="d15ed-113">Informar a los usuarios sobre eventos empresariales como, por ejemplo, nuevos mensajes o elementos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="d15ed-113">Notify users of enterprise events like new messages and work items.</span></span>
* <span data-ttu-id="d15ed-114">Enviar códigos para Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="d15ed-114">Send codes for multi-factor authentication.</span></span>

## <a name="what-are-push-notifications"></a><span data-ttu-id="d15ed-115">¿Qué son las notificaciones de inserción?</span><span class="sxs-lookup"><span data-stu-id="d15ed-115">What are Push Notifications?</span></span>
<span data-ttu-id="d15ed-116">Las notificaciones push son una forma de comunicación de aplicación a usuario en la que los usuarios de aplicaciones móviles reciben una notificación con determinada información que desean, por lo general, en un cuadro de diálogo o una ventana emergente.</span><span class="sxs-lookup"><span data-stu-id="d15ed-116">Push notifications is a form of app-to-user communication where users of mobile apps are notified of certain desired information, usually in a pop-up or dialog box.</span></span> <span data-ttu-id="d15ed-117">Normalmente, los usuarios pueden elegir ver o descartar el mensaje y, si eligen lo primero, se abrirá la aplicación móvil que les ha comunicado la notificación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-117">Users can generally choose to view or dismiss the message, and choosing the former will open the mobile app that had communicated the notification.</span></span>

<span data-ttu-id="d15ed-118">Las notificaciones push son vitales para las aplicaciones de consumidor, ya que aumentan el uso y la interacción de las aplicaciones, así como para las aplicaciones empresariales porque comunican información empresarial actualizada.</span><span class="sxs-lookup"><span data-stu-id="d15ed-118">Push notifications is vital for consumer apps in increasing app engagement and usage, and for enterprise apps in communicating up-to-date business information.</span></span> <span data-ttu-id="d15ed-119">Es la mejor forma de comunicación de aplicación a usuario porque ahorra energía para los dispositivos móviles, es flexible para los remitentes de notificaciones y está disponible cuando las aplicaciones correspondientes no están activas.</span><span class="sxs-lookup"><span data-stu-id="d15ed-119">It is the best app-to-user communication because it is energy-efficient for  mobile devices, flexible for the notifications senders, and available while corresponding apps are not active.</span></span>

<span data-ttu-id="d15ed-120">Más información acerca de las notificaciones push de algunas plataformas populares:</span><span class="sxs-lookup"><span data-stu-id="d15ed-120">For more information on push notifications for a few popular platforms:</span></span>
* [<span data-ttu-id="d15ed-121">iOS</span><span class="sxs-lookup"><span data-stu-id="d15ed-121">iOS</span></span>](https://developer.apple.com/notifications/)
* [<span data-ttu-id="d15ed-122">Android</span><span class="sxs-lookup"><span data-stu-id="d15ed-122">Android</span></span>](https://developer.android.com/guide/topics/ui/notifiers/notifications.html)
* [<span data-ttu-id="d15ed-123">Windows</span><span class="sxs-lookup"><span data-stu-id="d15ed-123">Windows</span></span>](http://msdn.microsoft.com/library/windows/apps/hh779725.aspx)

## <a name="how-push-notifications-work"></a><span data-ttu-id="d15ed-124">Funcionamiento de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="d15ed-124">How Push Notifications Work</span></span>
<span data-ttu-id="d15ed-125">Las notificaciones push se entregan a través de unas infraestructuras específicas para la plataforma llamadas *Sistemas de notificación de plataforma* (PNS).</span><span class="sxs-lookup"><span data-stu-id="d15ed-125">Push notifications are delivered through platform-specific infrastructures called *Platform Notification Systems* (PNSes).</span></span> <span data-ttu-id="d15ed-126">Ofrecen funcionalidades de inserción esenciales para la entrega de un mensaje a un dispositivo con un identificador proporcionado y no tienen ninguna interfaz común.</span><span class="sxs-lookup"><span data-stu-id="d15ed-126">They offer barebone push functionalities to delivery message to a device with a provided handle, and have no common interface.</span></span> <span data-ttu-id="d15ed-127">Para enviar una notificación a todos los clientes mediante las versiones de iOS, Android y Windows de una aplicación, el desarrollador debe trabajar con APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), WNS (Servicio de notificaciones de Windows) al procesar por lotes los envíos.</span><span class="sxs-lookup"><span data-stu-id="d15ed-127">To send a notification to all customers across the iOS, Android, and Windows versions of an app, the developer must work with APNS (Apple Push Notification Service), FCM (Firebase Cloud Messaging), and WNS (Windows Notification Service), while batching the sends.</span></span>

<span data-ttu-id="d15ed-128">A continuación se muestra cómo funciona la inserción, a nivel general:</span><span class="sxs-lookup"><span data-stu-id="d15ed-128">At a high level, here is how push works:</span></span>

1. <span data-ttu-id="d15ed-129">La aplicación cliente decide si desea recibir inserciones, por lo que se pone en contacto con el PNS correspondiente para recuperar su identificador de inserción único y temporal.</span><span class="sxs-lookup"><span data-stu-id="d15ed-129">The client app decides it wants to receive pushes hence contacts the corresponding PNS to retrieve its unique and temporary push handle.</span></span> <span data-ttu-id="d15ed-130">El tipo de identificador depende del sistema (por ejemplo, WNS tiene URI mientras APNS tiene tokens).</span><span class="sxs-lookup"><span data-stu-id="d15ed-130">The handle type depends on the system (e.g. WNS has URIs while APNS has tokens).</span></span>
2. <span data-ttu-id="d15ed-131">La aplicación cliente almacena este identificador en el back-end o el proveedor de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-131">The client app stores this handle in the app back-end or provider.</span></span>
3. <span data-ttu-id="d15ed-132">Para enviar una notificación push, el back-end de la aplicación se pone en contacto con el PNS a través del identificador para dirigirse a una aplicación cliente específica.</span><span class="sxs-lookup"><span data-stu-id="d15ed-132">To send a push notification, the app back-end contacts the PNS using the handle to target a specific client app.</span></span>
4. <span data-ttu-id="d15ed-133">El PNS reenvía la notificación al dispositivo que especifica el identificador.</span><span class="sxs-lookup"><span data-stu-id="d15ed-133">The PNS forwards the notification to the device specified by the handle.</span></span>

![][0]

## <a name="the-challenges-of-push-notifications"></a><span data-ttu-id="d15ed-134">Los desafíos de las notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="d15ed-134">The Challenges of Push Notifications</span></span>
<span data-ttu-id="d15ed-135">A pesar de que los PNS son muy potentes, de todos modos dejan mucho trabajo al desarrollador de aplicaciones para poder implementar incluso escenarios comunes de notificaciones push, como la difusión o el envío de notificaciones push a usuarios segmentados.</span><span class="sxs-lookup"><span data-stu-id="d15ed-135">While PNSes are powerful, they leave much work to the app developer in order to implement even common push notification scenarios, such as broadcasting or sending push notifications to segmented users.</span></span>

<span data-ttu-id="d15ed-136">La inserción es una de las características más solicitadas en servicios de dispositivos móviles en la nube, ya que su funcionamiento requiere infraestructuras complejas que no están relacionadas con la lógica de negocios principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-136">Push is one of the most requested features in mobile cloud services, because its working requires complex infrastructures that are unrelated to the app's main business logic.</span></span> <span data-ttu-id="d15ed-137">Algunos de los desafíos que presenta la infraestructura son:</span><span class="sxs-lookup"><span data-stu-id="d15ed-137">Some of the infrastructural challenges are:</span></span>

* <span data-ttu-id="d15ed-138">**Dependencia de la plataforma**:</span><span class="sxs-lookup"><span data-stu-id="d15ed-138">**Platform dependency**:</span></span> 

  * <span data-ttu-id="d15ed-139">El back-end debe tener una lógica, dependiente de la plataforma, compleja y difícil de mantener para enviar notificaciones a dispositivos de distintas plataformas, ya que los PNS no están unificados.</span><span class="sxs-lookup"><span data-stu-id="d15ed-139">The backend needs to have complex and hard-to-maintain platform-dependent logic to send notifications to devices on various platforms as PNSes are not unified.</span></span>
* <span data-ttu-id="d15ed-140">**Escala**:</span><span class="sxs-lookup"><span data-stu-id="d15ed-140">**Scale**:</span></span>

  * <span data-ttu-id="d15ed-141">Según las directrices de PNS, se deben actualizar los tokens de dispositivo cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-141">Per PNS guidelines, device tokens must be refreshed upon every app launch.</span></span> <span data-ttu-id="d15ed-142">Esto significa que el back-end debe tratar con una gran cantidad de tráfico y acceso de bases de datos solo para mantener actualizados los tokens.</span><span class="sxs-lookup"><span data-stu-id="d15ed-142">This means the backend is dealing with a large amount of traffic and database access just to keep the tokens up-to-date.</span></span> <span data-ttu-id="d15ed-143">Cuando el número de dispositivos aumenta a centenares y miles de millones, la creación y el mantenimiento de esta infraestructura supone un costo enorme.</span><span class="sxs-lookup"><span data-stu-id="d15ed-143">When the number of devices grows to hundreds and thousands of millions, the cost of creating and maintaining this infrastructure is massive.</span></span>
  * <span data-ttu-id="d15ed-144">La mayoría de los PNS no son compatibles con la difusión a varios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d15ed-144">Most PNSes do not support broadcast to multiple devices.</span></span> <span data-ttu-id="d15ed-145">Esto significa que una simple difusión a un millón de dispositivos genera un millón de llamadas a los PNS.</span><span class="sxs-lookup"><span data-stu-id="d15ed-145">This means a simple broadcast to a million devices results in a million calls to the PNSes.</span></span> <span data-ttu-id="d15ed-146">El escalado de esta cantidad de tráfico con una latencia mínima no es algo trivial.</span><span class="sxs-lookup"><span data-stu-id="d15ed-146">Scaling this amount of traffic with minimal latency is nontrivial.</span></span>
* <span data-ttu-id="d15ed-147">**Enrutamiento**:</span><span class="sxs-lookup"><span data-stu-id="d15ed-147">**Routing**:</span></span>
  
  * <span data-ttu-id="d15ed-148">Aunque los PNS proporcionan una manera de enviar mensajes a dispositivos, la mayoría de las notificaciones de aplicaciones se dirigen a usuarios o grupos de interés.</span><span class="sxs-lookup"><span data-stu-id="d15ed-148">Though PNSes provide a way to send messages to devices, most apps notifications are targeted at users or interest groups.</span></span> <span data-ttu-id="d15ed-149">Esto significa que el back-end debe mantener un registro para asociar dispositivos a grupos de interés, usuarios, propiedades, etc. Esta sobrecarga se agrega al tiempo de comercialización total y a los costos de mantenimiento de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-149">This means the backend must maintain a registry to associate devices with interest groups, users, properties, etc. This overhead adds to the time to market and maintenance costs of an app.</span></span>

## <a name="why-use-notification-hubs"></a><span data-ttu-id="d15ed-150">¿Por qué usar los Centros de notificaciones?</span><span class="sxs-lookup"><span data-stu-id="d15ed-150">Why Use Notification Hubs?</span></span>
<span data-ttu-id="d15ed-151">Notification Hubs elimina todas las complejidades asociadas con la habilitación de una inserción propia.</span><span class="sxs-lookup"><span data-stu-id="d15ed-151">Notification Hubs eliminates all complexities associated with enabling push on your own.</span></span> <span data-ttu-id="d15ed-152">Su infraestructura de notificaciones push multiplataforma y escalada horizontalmente reduce los códigos relativos a la inserción y simplifica el back-end.</span><span class="sxs-lookup"><span data-stu-id="d15ed-152">Its multi-platform, scaled-out push notification infrastructure reduces push-related codes and simplifies your backend.</span></span> <span data-ttu-id="d15ed-153">Con Notification Hubs, los dispositivos solo son responsables de registrar identificadores de PNS con un centro, mientras que el back-end envía mensajes a usuarios o grupos de interés, tal como se muestra en la ilustración siguiente:</span><span class="sxs-lookup"><span data-stu-id="d15ed-153">With Notification Hubs, devices are merely responsible for registering their PNS handles with a hub, while the backend sends messages to users or interest groups, as shown in the following figure:</span></span>

![][1]

<span data-ttu-id="d15ed-154">Notification Hubs es un motor de inserción listo para usar que presenta las siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="d15ed-154">Notification hubs is your ready-to-use push engine with the following advantages:</span></span>

* <span data-ttu-id="d15ed-155">**Multiplataforma**</span><span class="sxs-lookup"><span data-stu-id="d15ed-155">**Cross platforms**</span></span>

  * <span data-ttu-id="d15ed-156">Compatibilidad para las principales plataformas push incluidos iOS, Android, Windows, Kindle y Baidu.</span><span class="sxs-lookup"><span data-stu-id="d15ed-156">Support for all major push platforms including iOS, Android, Windows, and Kindle and Baidu.</span></span>
  * <span data-ttu-id="d15ed-157">Una interfaz común para insertar en todas las plataformas en formatos específicos de la plataforma o independientes de esta sin ningún tipo de trabajo específico de la plataforma.</span><span class="sxs-lookup"><span data-stu-id="d15ed-157">A common interface to push to all platforms in platform-specific or platform-independent formats with no platform-specific work.</span></span>
  * <span data-ttu-id="d15ed-158">Administración de controladores de dispositivos en un único lugar.</span><span class="sxs-lookup"><span data-stu-id="d15ed-158">Device handle management in one place.</span></span>
* <span data-ttu-id="d15ed-159">**Back-ends cruzados**</span><span class="sxs-lookup"><span data-stu-id="d15ed-159">**Cross backends**</span></span>
  
  * <span data-ttu-id="d15ed-160">En la nube o local</span><span class="sxs-lookup"><span data-stu-id="d15ed-160">Cloud or on-premises</span></span>
  * <span data-ttu-id="d15ed-161">.NET, Node.js, Java, etc.</span><span class="sxs-lookup"><span data-stu-id="d15ed-161">.NET, Node.js, Java, etc.</span></span>
* <span data-ttu-id="d15ed-162">**Conjunto completo de patrones de entrega**:</span><span class="sxs-lookup"><span data-stu-id="d15ed-162">**Rich set of delivery patterns**:</span></span>

  * <span data-ttu-id="d15ed-163">*Difusión para una o varias plataformas*: puede difundir al instante a millones de dispositivos entre plataformas con una sola llamada API.</span><span class="sxs-lookup"><span data-stu-id="d15ed-163">*Broadcast to one or multiple platforms*: You can instantly broadcast to millions of devices across platforms with a single API call.</span></span>
  * <span data-ttu-id="d15ed-164">*Inserción en dispositivo*: puede destinar las notificaciones a dispositivos individuales.</span><span class="sxs-lookup"><span data-stu-id="d15ed-164">*Push to device*: You can target notifications to individual devices.</span></span>
  * <span data-ttu-id="d15ed-165">*Inserción en usuario*: las características de etiquetas y plantillas le ayudan a llegar a todos los dispositivos multiplataforma de un usuario.</span><span class="sxs-lookup"><span data-stu-id="d15ed-165">*Push to user*: Tags and templates features help you reach all cross-platform devices of a user.</span></span>
  * <span data-ttu-id="d15ed-166">*Inserción en segmento con etiquetas dinámicas*: las característica de etiquetas le ayudan a segmentar dispositivos e insertar en ellos en función de sus necesidades, tanto si va a enviar a un segmento como si lo envía a una expresión de segmentos (p. ej. AND activo reside en Seattle NO es un usuario nuevo).</span><span class="sxs-lookup"><span data-stu-id="d15ed-166">*Push to segment with dynamic tags*: Tags feature helps you segment devices and push to them according to your needs, whether you are sending to one segment or an expression of segments (e.g. active AND lives in Seattle NOT new user).</span></span> <span data-ttu-id="d15ed-167">En lugar de limitarse a la publicación-suscripción, puede actualizar las etiquetas de dispositivo en cualquier lugar y en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d15ed-167">Instead of being restricted to pub-sub, you can update device tags anywhere and anytime.</span></span>
  * <span data-ttu-id="d15ed-168">*Inserción localizada*: la característica de plantillas le ayuda a obtener la localización sin alterar el código de back-end.</span><span class="sxs-lookup"><span data-stu-id="d15ed-168">*Localized push*: Templates feature helps achieve localization without affecting backend code.</span></span>
  * <span data-ttu-id="d15ed-169">*Inserción silenciosa*: puede habilitar el modelo de inserción a extracción enviando notificaciones silenciosas a dispositivos y desencadenándolos para que realicen ciertas extracciones o acciones.</span><span class="sxs-lookup"><span data-stu-id="d15ed-169">*Silent push*: You can enables the push-to-pull pattern by sending silent notifications to devices and triggering them to complete certain pulls or actions.</span></span>
  * <span data-ttu-id="d15ed-170">*Inserción programada*: puede programar el envío de notificaciones en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="d15ed-170">*Scheduled push*: You can schedule to send out notifications anytime.</span></span>
  * <span data-ttu-id="d15ed-171">*Inserción directa*: puede omitir el registro de dispositivos con nuestro servicio y procesar por lotes directamente las inserciones a una lista de identificadores de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d15ed-171">*Direct push*: You can skip registering devices with our service and directly batch push to a list of device handles.</span></span>
  * <span data-ttu-id="d15ed-172">*Inserción personalizada*: las variables de inserción de dispositivo le ayudan a enviar notificaciones push personalizadas específicas de dispositivo con pares de clave-valor personalizados.</span><span class="sxs-lookup"><span data-stu-id="d15ed-172">*Personalized push*: Device push variables helps you send device-specific personalized push notifications with customized key-value pairs.</span></span>
* <span data-ttu-id="d15ed-173">**Telemetría enriquecida**</span><span class="sxs-lookup"><span data-stu-id="d15ed-173">**Rich telemetry**</span></span>
  
  * <span data-ttu-id="d15ed-174">La telemetría de inserción general, dispositivo, error y operación está disponible en Azure Portal y mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d15ed-174">General push, device, error, and operation telemetry is available in the Azure portal and programmatically.</span></span>
  * <span data-ttu-id="d15ed-175">La telemetría por mensaje realiza el seguimiento de cada inserción desde la llamada de la solicitud inicial a nuestro servicio, procesando por lotes correctamente el envío de las inserciones.</span><span class="sxs-lookup"><span data-stu-id="d15ed-175">Per Message Telemetry tracks each push from your initial request call to our service successfully batching the pushes out.</span></span>
  * <span data-ttu-id="d15ed-176">Platform Notification System Feedback (Comentarios del Sistema de notificación de plataforma) comunica todos los comentarios de los Sistemas de notificación de plataforma para ayudar en la depuración.</span><span class="sxs-lookup"><span data-stu-id="d15ed-176">Platform Notification System Feedback communicates all feedback from Platfom Notification Systems to assist in debugging.</span></span>
* <span data-ttu-id="d15ed-177">**Escalabilidad**</span><span class="sxs-lookup"><span data-stu-id="d15ed-177">**Scalability**</span></span> 
  
  * <span data-ttu-id="d15ed-178">Enviar mensajes rápidos a millones de dispositivos sin tener que volver a diseñar la arquitectura o realizar el particionamiento del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d15ed-178">Send fast messages to millions of devices without re-architecting or device sharding.</span></span>
* <span data-ttu-id="d15ed-179">**Seguridad**</span><span class="sxs-lookup"><span data-stu-id="d15ed-179">**Security**</span></span>

  * <span data-ttu-id="d15ed-180">Firma de acceso compartido (SAS) o autenticación federada.</span><span class="sxs-lookup"><span data-stu-id="d15ed-180">Shared Access Secret (SAS) or federated authentication.</span></span>

## <a name="integration-with-app-service-mobile-apps"></a><span data-ttu-id="d15ed-181">Integración con las Aplicaciones móviles del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="d15ed-181">Integration with App Service Mobile Apps</span></span>
<span data-ttu-id="d15ed-182">Para facilitar una experiencia perfecta y unificadora entre servicios de Azure, [Aplicaciones móviles del Servicio de aplicaciones] tiene compatibilidad integrada con notificaciones push mediante centros de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="d15ed-182">To facilitate a seamless and unifying experience across Azure services, [App Service Mobile Apps] has built-in support for push notifications using Notification Hubs.</span></span> <span data-ttu-id="d15ed-183">[Aplicaciones móviles del Servicio de aplicaciones] ofrecen una plataforma de desarrollo de aplicaciones móviles altamente escalable y disponible globalmente para desarrolladores empresariales e integradores de sistemas que proporciona un amplio conjunto de funcionalidades a desarrolladores móviles.</span><span class="sxs-lookup"><span data-stu-id="d15ed-183">[App Service Mobile Apps] offers a highly scalable, globally available mobile application development platform for Enterprise Developers and System Integrators that brings a rich set of capabilities to mobile developers.</span></span>

<span data-ttu-id="d15ed-184">Los desarrolladores de aplicaciones móviles pueden usar centros de notificaciones con el siguiente flujo de trabajo:</span><span class="sxs-lookup"><span data-stu-id="d15ed-184">Mobile Apps developers can utilize Notification Hubs with the following workflow:</span></span>

1. <span data-ttu-id="d15ed-185">Recuperar controlador PNS de dispositivo</span><span class="sxs-lookup"><span data-stu-id="d15ed-185">Retrieve device PNS handle</span></span>
2. <span data-ttu-id="d15ed-186">Registrar el dispositivo con Notification Hubs a través de la API adecuada del registro del SDK de cliente de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="d15ed-186">Register device with Notification Hubs through convenient Mobile Apps Client SDK register API</span></span>
   * <span data-ttu-id="d15ed-187">Tenga en cuenta que las aplicaciones móviles eliminan todas las etiquetas en los registros por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="d15ed-187">Note that Mobile Apps strips away all tags on registrations for security purposes.</span></span> <span data-ttu-id="d15ed-188">Trabaje con centros de notificaciones desde su back-end directamente para asociar etiquetas a dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d15ed-188">Work with Notification Hubs from your backend directly to associate tags with devices.</span></span>
3. <span data-ttu-id="d15ed-189">Enviar notificaciones desde su back-end de aplicación con los centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="d15ed-189">Send notifications from your app backend with Notification Hubs</span></span>

<span data-ttu-id="d15ed-190">Estas son algunas ventajas para los desarrolladores de esta integración:</span><span class="sxs-lookup"><span data-stu-id="d15ed-190">Here are some conveniences brought to developers with this integration:</span></span>

* <span data-ttu-id="d15ed-191">**SKD de cliente de Mobile Apps**: estos SDK multiplataforma ofrecen API simples para el registro y se comunican con el centro de notificaciones vinculado con la aplicación móvil automáticamente.</span><span class="sxs-lookup"><span data-stu-id="d15ed-191">**Mobile Apps Client SDKs**: These multi-platform SDKs provide simple APIs for registration and talk to the notification hub linked up with the mobile app automatically.</span></span> <span data-ttu-id="d15ed-192">Los desarrolladores no tienen que indagar en las credenciales de los Centros de notificaciones y trabajar con un servicio adicional.</span><span class="sxs-lookup"><span data-stu-id="d15ed-192">Developers do not need to dig through Notification Hubs credentials and work with an additional service.</span></span>

  * <span data-ttu-id="d15ed-193">*Inserción en usuario*: los SDK etiquetan automáticamente el dispositivo específico con un identificador de usuario autenticado de Mobile Apps para habilitar la inserción en un escenario de usuario.</span><span class="sxs-lookup"><span data-stu-id="d15ed-193">*Push to user*: The SDKs automatically tag the given device with Mobile Apps authenticated User ID to enable push to user scenario.</span></span>
  * <span data-ttu-id="d15ed-194">*Inserción en dispositivo*: los SDK utilizan automáticamente el identificador de instalación de Mobile Apps como GUID para registrarse con Notification Hubs, lo que permite que los desarrolladores no tengan que mantener varios GUID de servicio.</span><span class="sxs-lookup"><span data-stu-id="d15ed-194">*Push to device*: The SDKs automatically use the Mobile Apps Installation ID as GUID to register with Notification Hubs, saving developers the trouble of maintaining multiple service GUIDs.</span></span>
* <span data-ttu-id="d15ed-195">**Modelo de instalación**: Mobile Apps funciona con el modelo de inserción más reciente de Notification Hubs para representar todas las propiedades de inserción asociadas a un dispositivo en una instalación de JSON que se alinea con Servicios de notificaciones de inserción y es sencillo de usar.</span><span class="sxs-lookup"><span data-stu-id="d15ed-195">**Installation model**: Mobile Apps works with Notification Hubs' latest push model to represent all push properties associated with a device in a JSON Installation that aligns with Push Notification Services and is easy to use.</span></span>
* <span data-ttu-id="d15ed-196">**Flexibilidad**: los desarrolladores siempre pueden elegir trabajar con Notification Hubs directamente, incluso con la integración implementada.</span><span class="sxs-lookup"><span data-stu-id="d15ed-196">**Flexibility**: Developers can always choose to work with Notification Hubs directly even with the integration in place.</span></span>
* <span data-ttu-id="d15ed-197">**Experiencia integrada en [Azure Portal]**: la inserción como funcionalidad se representa visualmente en Mobile Apps y los desarrolladores pueden trabajar fácilmente con el centro de notificaciones asociado a través de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="d15ed-197">**Integrated experience in [Azure portal]**: Push as a capability is represented visually in Mobile Apps and developers can easily work with the associated notification hub through Mobile Apps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d15ed-198">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d15ed-198">Next Steps</span></span>
<span data-ttu-id="d15ed-199">Más información acerca de los Centros de notificaciones en estos temas:</span><span class="sxs-lookup"><span data-stu-id="d15ed-199">You can find out more about Notification Hubs in these topics:</span></span>

* <span data-ttu-id="d15ed-200">**[Cómo utilizan los clientes los Notification Hubs]**</span><span class="sxs-lookup"><span data-stu-id="d15ed-200">**[How customers are using Notification Hubs]**</span></span>
* <span data-ttu-id="d15ed-201">**[Tutoriales y guías sobre los Notification Hubs]**</span><span class="sxs-lookup"><span data-stu-id="d15ed-201">**[Notification Hubs tutorials and guides]**</span></span>
* <span data-ttu-id="d15ed-202">**Tutoriales de introducción sobre los Notification Hubs**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS] y [Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="d15ed-202">**Notification Hubs Getting Started tutorials**: [iOS], [Android], [Windows Universal], [Windows Phone], [Kindle], [Xamarin.iOS], [Xamarin.Android]</span></span>

[0]: ./media/notification-hubs-overview/registration-diagram.png
[1]: ./media/notification-hubs-overview/notification-hub-diagram.png
<span data-ttu-id="d15ed-203">[Cómo utilizan los clientes los Notification Hubs]: http://azure.microsoft.com/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="d15ed-203">[How customers are using Notification Hubs]: http://azure.microsoft.com/services/notification-hubs</span></span>
<span data-ttu-id="d15ed-204">[Tutoriales y guías sobre los Notification Hubs]: http://azure.microsoft.com/documentation/services/notification-hubs</span><span class="sxs-lookup"><span data-stu-id="d15ed-204">[Notification Hubs tutorials and guides]: http://azure.microsoft.com/documentation/services/notification-hubs</span></span>
<span data-ttu-id="d15ed-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-205">[iOS]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started</span></span>
<span data-ttu-id="d15ed-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-206">[Android]: http://azure.microsoft.com/documentation/articles/notification-hubs-android-get-started</span></span>
<span data-ttu-id="d15ed-207">[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-207">[Windows Universal]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started</span></span>
<span data-ttu-id="d15ed-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-208">[Windows Phone]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-phone-get-started</span></span>
<span data-ttu-id="d15ed-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-209">[Kindle]: http://azure.microsoft.com/documentation/articles/notification-hubs-kindle-get-started</span></span>
<span data-ttu-id="d15ed-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-210">[Xamarin.iOS]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-ios-get-started</span></span>
<span data-ttu-id="d15ed-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span><span class="sxs-lookup"><span data-stu-id="d15ed-211">[Xamarin.Android]: http://azure.microsoft.com/documentation/articles/partner-xamarin-notification-hubs-android-get-started</span></span>
[Microsoft.WindowsAzure.Messaging.NotificationHub]: http://msdn.microsoft.com/library/microsoft.windowsazure.messaging.notificationhub.aspx
[Microsoft.ServiceBus.Notifications]: http://msdn.microsoft.com/library/microsoft.servicebus.notifications.aspx
<span data-ttu-id="d15ed-212">[Aplicaciones móviles del Servicio de aplicaciones]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span><span class="sxs-lookup"><span data-stu-id="d15ed-212">[App Service Mobile Apps]: https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-value-prop/</span></span>
[templates]: notification-hubs-templates-cross-platform-push-messages.md
<span data-ttu-id="d15ed-213">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="d15ed-213">[Azure portal]: https://portal.azure.com</span></span>
[tags]: (http://msdn.microsoft.com/library/azure/dn530749.aspx)