---
title: aaaTemplates
description: En este tema se explican las plantillas para los Centros de notificaciones de Azure.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="fafab-103">Plantillas</span><span class="sxs-lookup"><span data-stu-id="fafab-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="fafab-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fafab-104">Overview</span></span>
<span data-ttu-id="fafab-105">Las plantillas permiten un cliente toospecify Hola exacta formato de aplicación de notificaciones de Hola que desee tooreceive.</span><span class="sxs-lookup"><span data-stu-id="fafab-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="fafab-106">Mediante plantillas, una aplicación puede obtener distintas ventajas, incluidos Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fafab-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="fafab-107">Un back-end independiente de la plataforma</span><span class="sxs-lookup"><span data-stu-id="fafab-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="fafab-108">Notificaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="fafab-108">Personalized notifications</span></span>
* <span data-ttu-id="fafab-109">Independencia de la versión del cliente</span><span class="sxs-lookup"><span data-stu-id="fafab-109">Client-version independence</span></span>
* <span data-ttu-id="fafab-110">Localización sencilla</span><span class="sxs-lookup"><span data-stu-id="fafab-110">Easy localization</span></span>

<span data-ttu-id="fafab-111">Esta sección proporciona dos ejemplos detallados de cómo toouse plantillas toosend independiente de la plataforma las notificaciones de todos los dispositivos de destino a través de plataformas y toopersonalize difusión dispositivo tooeach de notificación.</span><span class="sxs-lookup"><span data-stu-id="fafab-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="fafab-112">Uso de plantillas multiplataforma</span><span class="sxs-lookup"><span data-stu-id="fafab-112">Using templates cross-platform</span></span>
<span data-ttu-id="fafab-113">notificaciones de inserción de toosend de manera estándar de Hello es toosend, para cada notificación que es toobe envía, un servicios de notificación de tooplatform carga concreto (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="fafab-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="fafab-114">Por ejemplo, una alerta tooAPNS, toosend carga Hola es un objeto Json de hello siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="fafab-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="fafab-115">toosend un mensaje de notificación del sistema similar en una aplicación Windows Store, carga XML de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="fafab-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="fafab-116">Puede crear cargas similares para plataformas MPNS (Windows Phone) y GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="fafab-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="fafab-117">Este requisito fuerza Hola aplicación back-end tooproduce diferentes cargas para cada plataforma y eficazmente hace responsable de la parte de la capa de presentación de Hola de aplicación hello Hola back-end.</span><span class="sxs-lookup"><span data-stu-id="fafab-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="fafab-118">Algunos problemas incluye diseños gráficos y de localización (especialmente para las aplicaciones de la Tienda Windows que incluyen notificaciones para varios tipos de iconos).</span><span class="sxs-lookup"><span data-stu-id="fafab-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="fafab-119">característica de plantilla de centros de notificaciones de Hello permite que una aplicación toocreate especial registros de cliente, llama a los registros de plantilla, que incluyen, además de toohello conjunto de etiquetas, una plantilla.</span><span class="sxs-lookup"><span data-stu-id="fafab-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="fafab-120">característica de plantilla de centros de notificaciones de Hello permite dispositivos cliente aplicación tooassociate con plantillas si está trabajando con las instalaciones (opción preferidas) o registros.</span><span class="sxs-lookup"><span data-stu-id="fafab-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="fafab-121">Dados Hola anteriores ejemplos de carga, hello únicamente información de independiente de la plataforma es Hola real mensaje de alerta (Hola).</span><span class="sxs-lookup"><span data-stu-id="fafab-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="fafab-122">Una plantilla es un conjunto de instrucciones para el centro de notificaciones de hello en cómo tooformat un independiente de la plataforma mensaje para el registro de hello de esa aplicación de cliente específico.</span><span class="sxs-lookup"><span data-stu-id="fafab-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="fafab-123">En el anterior ejemplo de Hola, mensaje de bienvenida de plataforma independiente es una propiedad única: **mensaje = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="fafab-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="fafab-124">Hola siguiente imagen muestra hello por encima de proceso:</span><span class="sxs-lookup"><span data-stu-id="fafab-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="fafab-125">plantilla de Hello para el registro de aplicación de cliente de iOS de hello es como sigue:</span><span class="sxs-lookup"><span data-stu-id="fafab-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="fafab-126">Hola plantilla correspondiente para la aplicación de cliente de la tienda Windows hello es:</span><span class="sxs-lookup"><span data-stu-id="fafab-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="fafab-127">Tenga en cuenta que Hola real del mensaje se sustituye por la expresión de hello $(mensaje).</span><span class="sxs-lookup"><span data-stu-id="fafab-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="fafab-128">Esta expresión indica Hola centro de notificaciones, cada vez que envía un mensaje toothis registro determinado, un mensaje que sigue a él y los conmutadores de valor común de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="fafab-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="fafab-129">Si está trabajando con el modelo de instalación, clave de la instalación "plantillas" hello contiene JSON de varias plantillas.</span><span class="sxs-lookup"><span data-stu-id="fafab-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="fafab-130">Si está trabajando con el modelo de registro, aplicación de cliente de hello puede crear de la varios registros en orden toouse varias plantillas; Por ejemplo, una plantilla para mensajes de alerta y una plantilla para las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="fafab-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="fafab-131">Las aplicaciones cliente también pueden combinar los registros nativos (registros sin plantilla) y los registros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="fafab-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="fafab-132">Hola centro de notificaciones envía una notificación para cada plantilla sin tener en cuenta si pertenecen toohello misma aplicación de cliente.</span><span class="sxs-lookup"><span data-stu-id="fafab-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="fafab-133">Este comportamiento puede ser notificaciones de independiente de la plataforma tootranslate usados en notificaciones más.</span><span class="sxs-lookup"><span data-stu-id="fafab-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="fafab-134">Por ejemplo, hello toohello de mensaje independiente de plataforma mismo que centro de notificaciones se pueden traducir sin problemas en una alerta de notificación del sistema y una actualización del icono, sin necesidad de Hola toobe de back-end consciente de ello.</span><span class="sxs-lookup"><span data-stu-id="fafab-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="fafab-135">Tenga en cuenta que algunas plataformas (por ejemplo, iOS) pueden contraer varias toohello notificaciones mismo dispositivo si se envían en un breve período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="fafab-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="fafab-136">Uso de plantillas para personalización</span><span class="sxs-lookup"><span data-stu-id="fafab-136">Using templates for personalization</span></span>
<span data-ttu-id="fafab-137">Plantillas de toousing de otra ventaja es Hola capacidad toouse personalización de los centros de notificaciones tooperform por registro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="fafab-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="fafab-138">Por ejemplo, considere la posibilidad de una aplicación del tiempo que muestra un icono con las condiciones meteorológicas de hello en una ubicación específica.</span><span class="sxs-lookup"><span data-stu-id="fafab-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="fafab-139">Un usuario puede elegir entre grados Celsius o Fahrenheit, además de un pronóstico de un día o de cinco días.</span><span class="sxs-lookup"><span data-stu-id="fafab-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="fafab-140">Mediante plantillas, cada instalación de la aplicación cliente puede registrar para formato Hola requerido (1 día Celsius, 1 día Fahrenheit, 5 días grados centígrados, 5 días Fahrenheit), y que Hola back-end envíe un mensaje único que contiene toda la información de hello necesario toofill los plantillas (por ejemplo, una cinco días previsión con grados Celsius y Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="fafab-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="fafab-141">plantilla de Hola Hola un día de previsión con grados centígrados temperaturas es como sigue:</span><span class="sxs-lookup"><span data-stu-id="fafab-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="fafab-142">Hola mensaje enviado toohello centro de notificaciones contiene Hola todas las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="fafab-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="fafab-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="fafab-143">day1_image</span></span></td><td><span data-ttu-id="fafab-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="fafab-144">day2_image</span></span></td><td><span data-ttu-id="fafab-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="fafab-145">day3_image</span></span></td><td><span data-ttu-id="fafab-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="fafab-146">day4_image</span></span></td><td><span data-ttu-id="fafab-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="fafab-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="fafab-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="fafab-148">day1_tempC</span></span></td><td><span data-ttu-id="fafab-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="fafab-149">day2_tempC</span></span></td><td><span data-ttu-id="fafab-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="fafab-150">day3_tempC</span></span></td><td><span data-ttu-id="fafab-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="fafab-151">day4_tempC</span></span></td><td><span data-ttu-id="fafab-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="fafab-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="fafab-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="fafab-153">day1_tempF</span></span></td><td><span data-ttu-id="fafab-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="fafab-154">day2_tempF</span></span></td><td><span data-ttu-id="fafab-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="fafab-155">day3_tempF</span></span></td><td><span data-ttu-id="fafab-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="fafab-156">day4_tempF</span></span></td><td><span data-ttu-id="fafab-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="fafab-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="fafab-158">Mediante el uso de este patrón, Hola back-end sólo envía un mensaje único sin necesidad de opciones de personalización específicas de toostore para los usuarios de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="fafab-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="fafab-159">Hola siguiente muestra este escenario:</span><span class="sxs-lookup"><span data-stu-id="fafab-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="fafab-160">¿Cómo tooregister plantillas</span><span class="sxs-lookup"><span data-stu-id="fafab-160">How tooregister templates</span></span>
<span data-ttu-id="fafab-161">tooregister con plantillas mediante el modelo de instalación de hello (opción preferida) o hello modelo de registro, consulte [administración de registros](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="fafab-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="fafab-162">Lenguaje de expresión de plantilla</span><span class="sxs-lookup"><span data-stu-id="fafab-162">Template expression language</span></span>
<span data-ttu-id="fafab-163">Las plantillas son tooXML limitado o formatos de documento JSON.</span><span class="sxs-lookup"><span data-stu-id="fafab-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="fafab-164">Además, solo puede ubicar expresiones en lugares específicos; por ejemplo, valores o atributos de nodo para XML, valores de propiedad de cadena para JSON.</span><span class="sxs-lookup"><span data-stu-id="fafab-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="fafab-165">Hello siguiente tabla muestra lenguaje Hola permitida en las plantillas:</span><span class="sxs-lookup"><span data-stu-id="fafab-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="fafab-166">Expression</span><span class="sxs-lookup"><span data-stu-id="fafab-166">Expression</span></span> | <span data-ttu-id="fafab-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="fafab-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fafab-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="fafab-168">$(prop)</span></span> |<span data-ttu-id="fafab-169">Propiedad de evento de tooan de referencia con el nombre especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="fafab-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="fafab-170">Los nombres de propiedad no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="fafab-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="fafab-171">Esta expresión se resuelve en valor de texto de la propiedad de Hola o en una cadena vacía si no hay propiedad Hola.</span><span class="sxs-lookup"><span data-stu-id="fafab-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="fafab-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="fafab-172">$(prop, n)</span></span> |<span data-ttu-id="fafab-173">Como anteriormente, pero hello se explícitamente texto se recorta en n caracteres, por ejemplo $(título, 20) recorta contenido Hola de propiedad de título de hello en 20 caracteres.</span><span class="sxs-lookup"><span data-stu-id="fafab-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="fafab-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="fafab-174">.(prop, n)</span></span> |<span data-ttu-id="fafab-175">Como anteriormente, pero hello texto se utiliza como sufijo con tres puntos tal y como se recorta.</span><span class="sxs-lookup"><span data-stu-id="fafab-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="fafab-176">tamaño total de Hola de hello recorta la cadena y sufijo hello no supere los n caracteres.</span><span class="sxs-lookup"><span data-stu-id="fafab-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="fafab-177">. (cargo, 20) con una propiedad de entrada de "This is línea del título de Hola" da como resultado **este es el título de Hola...**</span><span class="sxs-lookup"><span data-stu-id="fafab-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="fafab-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="fafab-178">%(prop)</span></span> |<span data-ttu-id="fafab-179">Too$(name) similar, salvo que los resultados del Hola está codificada por el URI.</span><span class="sxs-lookup"><span data-stu-id="fafab-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="fafab-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="fafab-180">#(prop)</span></span> |<span data-ttu-id="fafab-181">Se usa en las plantillas JSON (por ejemplo, para plantillas de iOS y Android).</span><span class="sxs-lookup"><span data-stu-id="fafab-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="fafab-182">Esta función funciona exactamente igual Hola como $(prop) especificado anteriormente, excepto cuando se utilizan en las plantillas de JSON (por ejemplo, plantillas de Apple).</span><span class="sxs-lookup"><span data-stu-id="fafab-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="fafab-183">En este caso, si esta función no está rodeada por "{','}" (por ejemplo, 'myJsonProperty': "#(name)"), y se evalúa como el número de tooa en formato de Javascript, por ejemplo, regexp: (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. ¿&#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, a continuación, Hola de salida JSON es un número.</span><span class="sxs-lookup"><span data-stu-id="fafab-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="fafab-184">Por ejemplo, ‘badge : ‘#(name)’ se convierte en ‘badge’ : 40 (y no ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="fafab-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="fafab-185">‘texto’ o “texto”</span><span class="sxs-lookup"><span data-stu-id="fafab-185">‘text’ or “text”</span></span> |<span data-ttu-id="fafab-186">Un literal.</span><span class="sxs-lookup"><span data-stu-id="fafab-186">A literal.</span></span> <span data-ttu-id="fafab-187">Los literales contienen texto arbitrario encerrado entre comillas simples o dobles.</span><span class="sxs-lookup"><span data-stu-id="fafab-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="fafab-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="fafab-188">expr1 + expr2</span></span> |<span data-ttu-id="fafab-189">operador de concatenación de Hello combinar dos expresiones en una sola cadena.</span><span class="sxs-lookup"><span data-stu-id="fafab-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="fafab-190">expresiones de Hello pueden ser cualquiera de hello anterior formularios.</span><span class="sxs-lookup"><span data-stu-id="fafab-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="fafab-191">Cuando se utiliza la concatenación, la expresión completa de Hola debe incluirse entre con {}.</span><span class="sxs-lookup"><span data-stu-id="fafab-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="fafab-192">Por ejemplo, {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="fafab-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="fafab-193">Por ejemplo, el siguiente hello no es una plantilla XML válida:</span><span class="sxs-lookup"><span data-stu-id="fafab-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="fafab-194">Como se explicó anteriormente, cuando se usa la concatenación, las expresiones deben ir entre llaves.</span><span class="sxs-lookup"><span data-stu-id="fafab-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="fafab-195">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fafab-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

