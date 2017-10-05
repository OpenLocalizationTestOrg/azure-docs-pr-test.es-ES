---
title: Plantillas
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="209aa-103">Plantillas</span><span class="sxs-lookup"><span data-stu-id="209aa-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="209aa-104">Información general</span><span class="sxs-lookup"><span data-stu-id="209aa-104">Overview</span></span>
<span data-ttu-id="209aa-105">Las plantillas permiten que una aplicación cliente especifique el formato exacto de la notificación que desea recibir.</span><span class="sxs-lookup"><span data-stu-id="209aa-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="209aa-106">Con las plantillas, una aplicación puede obtener muchos beneficios distintos, incluidos los siguientes:</span><span class="sxs-lookup"><span data-stu-id="209aa-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="209aa-107">Un back-end independiente de la plataforma</span><span class="sxs-lookup"><span data-stu-id="209aa-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="209aa-108">Notificaciones personalizadas</span><span class="sxs-lookup"><span data-stu-id="209aa-108">Personalized notifications</span></span>
* <span data-ttu-id="209aa-109">Independencia de la versión del cliente</span><span class="sxs-lookup"><span data-stu-id="209aa-109">Client-version independence</span></span>
* <span data-ttu-id="209aa-110">Localización sencilla</span><span class="sxs-lookup"><span data-stu-id="209aa-110">Easy localization</span></span>

<span data-ttu-id="209aa-111">Esta sección proporciona ejemplos detallados sobre cómo usar las plantillas para enviar notificaciones independientes de la plataforma orientadas a todos los dispositivos en todas las plataformas y para personalizar la notificación de difusión a cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="209aa-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="209aa-112">Uso de plantillas multiplataforma</span><span class="sxs-lookup"><span data-stu-id="209aa-112">Using templates cross-platform</span></span>
<span data-ttu-id="209aa-113">La forma estándar de enviar notificaciones push es enviar una carga específica a los servicios de notificación de plataforma (WNS, APNS) para cada notificación que se debe enviar.</span><span class="sxs-lookup"><span data-stu-id="209aa-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="209aa-114">Por ejemplo, para enviar una alerta a APNS, la carga es un objeto JSON con el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="209aa-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="209aa-115">Para enviar un mensaje de notificación del sistema similar en una aplicación de la Tienda Windows, la carga XML es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="209aa-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="209aa-116">Puede crear cargas similares para plataformas MPNS (Windows Phone) y GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="209aa-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="209aa-117">Este requisito obliga al back-end de la aplicación a generar cargas distintas para cada plataforma y, de manera efectiva, hace que el back-end sea responsable de parte del nivel de presentación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="209aa-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="209aa-118">Algunos problemas incluye diseños gráficos y de localización (especialmente para las aplicaciones de la Tienda Windows que incluyen notificaciones para varios tipos de iconos).</span><span class="sxs-lookup"><span data-stu-id="209aa-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="209aa-119">La característica de plantilla de Centros de notificaciones permite que una aplicación cliente cree registros especiales, llamados registros de plantilla, que, además del conjunto de etiquetas, incluye una plantilla.</span><span class="sxs-lookup"><span data-stu-id="209aa-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="209aa-120">La característica de plantilla de Centros de notificaciones permite que una aplicación cliente asocie los dispositivos con plantillas, ya sea que trabaje con Instalaciones (la opción de preferencia) o con Registros.</span><span class="sxs-lookup"><span data-stu-id="209aa-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="209aa-121">Dados los ejemplos de carga anteriores, la única información independiente de la plataforma es el mensaje de alerta mismo (Hello!).</span><span class="sxs-lookup"><span data-stu-id="209aa-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="209aa-122">Una plantilla es un conjunto de instrucciones para el Centro de notificaciones sobre cómo dar formato a un mensaje independiente de la plataforma para el registro de esa aplicación cliente específica.</span><span class="sxs-lookup"><span data-stu-id="209aa-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="209aa-123">En el ejemplo anterior, el mensaje independiente de la plataforma es una propiedad única: **message = Hello!**.</span><span class="sxs-lookup"><span data-stu-id="209aa-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="209aa-124">La siguiente ilustración muestra el proceso anterior:</span><span class="sxs-lookup"><span data-stu-id="209aa-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="209aa-125">La plantilla para el registro de una aplicación cliente de iOS es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="209aa-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="209aa-126">La plantilla correspondiente a una aplicación cliente de la Tienda Windows es:</span><span class="sxs-lookup"><span data-stu-id="209aa-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="209aa-127">Observe que la expresión $(message) sustituye al mensaje mismo.</span><span class="sxs-lookup"><span data-stu-id="209aa-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="209aa-128">Esta expresión indica al Centro de notificaciones, cada vez que envía un mensaje a este registro en especial, que cree un mensaje que lo siga y cambia el valor común.</span><span class="sxs-lookup"><span data-stu-id="209aa-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="209aa-129">Si trabaja con el modelo de Instalación, la clave "plantillas" de la instalación contiene el código JSON de varias plantillas.</span><span class="sxs-lookup"><span data-stu-id="209aa-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="209aa-130">Si trabaja con el modelo de Registro, la aplicación cliente puede crear varios registros para usar varias plantillas; por ejemplo, una plantilla para los mensajes de alerta y una plantilla para las actualizaciones de icono.</span><span class="sxs-lookup"><span data-stu-id="209aa-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="209aa-131">Las aplicaciones cliente también pueden combinar los registros nativos (registros sin plantilla) y los registros de plantilla.</span><span class="sxs-lookup"><span data-stu-id="209aa-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="209aa-132">El Centro de notificaciones envía una notificación para cada plantilla sin considerar si pertenecen a la misma aplicación cliente.</span><span class="sxs-lookup"><span data-stu-id="209aa-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="209aa-133">Este comportamiento se puede usar para traducir las notificaciones independientes de la plataforma en más notificaciones.</span><span class="sxs-lookup"><span data-stu-id="209aa-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="209aa-134">Por ejemplo, el mismo mensaje independiente de la plataforma al Centro de notificaciones se puede traducir sin problemas en una alerta de notificación del sistema y una actualización de icono, sin requerir que el back-end lo sepa.</span><span class="sxs-lookup"><span data-stu-id="209aa-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="209aa-135">Tenga en cuenta que algunas plataformas (por ejemplo, iOS) puede contraer las diversas notificaciones en el mismo dispositivo si se envían en un período breve.</span><span class="sxs-lookup"><span data-stu-id="209aa-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="209aa-136">Uso de plantillas para personalización</span><span class="sxs-lookup"><span data-stu-id="209aa-136">Using templates for personalization</span></span>
<span data-ttu-id="209aa-137">Otra ventaja de usar plantillas es la capacidad de usar Centros de notificaciones para ejecutar la personalización por registro de las notificaciones.</span><span class="sxs-lookup"><span data-stu-id="209aa-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="209aa-138">Por ejemplo, considere una aplicación para el clima que muestra un icono con las condiciones climáticas de una ubicación específica.</span><span class="sxs-lookup"><span data-stu-id="209aa-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="209aa-139">Un usuario puede elegir entre grados Celsius o Fahrenheit, además de un pronóstico de un día o de cinco días.</span><span class="sxs-lookup"><span data-stu-id="209aa-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="209aa-140">Con las plantillas, cada instalación de aplicación cliente puede registrar el formato requerido (pronóstico de 1 día en grados Celsius, pronóstico de 1 día en grados Fahrenheit, pronóstico de 5 días en grados Celsius, pronóstico de 5 días en grados Fahrenheit) y hacer que el back-end envíe un mensaje único con toda la información necesaria para rellenar esas plantillas (por ejemplo, un pronóstico de 5 días con grados Celsius y Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="209aa-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="209aa-141">La plantilla para un pronóstico de 1 día con temperaturas expresadas en Celsius es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="209aa-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="209aa-142">El mensaje enviado al Centro de notificaciones contiene todas las propiedades siguientes:</span><span class="sxs-lookup"><span data-stu-id="209aa-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="209aa-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="209aa-143">day1_image</span></span></td><td><span data-ttu-id="209aa-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="209aa-144">day2_image</span></span></td><td><span data-ttu-id="209aa-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="209aa-145">day3_image</span></span></td><td><span data-ttu-id="209aa-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="209aa-146">day4_image</span></span></td><td><span data-ttu-id="209aa-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="209aa-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="209aa-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="209aa-148">day1_tempC</span></span></td><td><span data-ttu-id="209aa-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="209aa-149">day2_tempC</span></span></td><td><span data-ttu-id="209aa-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="209aa-150">day3_tempC</span></span></td><td><span data-ttu-id="209aa-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="209aa-151">day4_tempC</span></span></td><td><span data-ttu-id="209aa-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="209aa-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="209aa-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="209aa-153">day1_tempF</span></span></td><td><span data-ttu-id="209aa-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="209aa-154">day2_tempF</span></span></td><td><span data-ttu-id="209aa-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="209aa-155">day3_tempF</span></span></td><td><span data-ttu-id="209aa-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="209aa-156">day4_tempF</span></span></td><td><span data-ttu-id="209aa-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="209aa-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="209aa-158">Con este patrón, el back-end solo envía un mensaje único sin tener que almacenar opciones de personalización específicas para los usuarios de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="209aa-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="209aa-159">La siguiente ilustración muestra este escenario:</span><span class="sxs-lookup"><span data-stu-id="209aa-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="209aa-160">Registro de las plantillas</span><span class="sxs-lookup"><span data-stu-id="209aa-160">How to register templates</span></span>
<span data-ttu-id="209aa-161">Para registrar las plantillas con el modelo de Instalación (la opción de preferencia) o el modelo de Registro, consulte [Administración de registros](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="209aa-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="209aa-162">Lenguaje de expresión de plantilla</span><span class="sxs-lookup"><span data-stu-id="209aa-162">Template expression language</span></span>
<span data-ttu-id="209aa-163">Las plantillas se limitan a los formatos de documento XML o JSON.</span><span class="sxs-lookup"><span data-stu-id="209aa-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="209aa-164">Además, solo puede ubicar expresiones en lugares específicos; por ejemplo, valores o atributos de nodo para XML, valores de propiedad de cadena para JSON.</span><span class="sxs-lookup"><span data-stu-id="209aa-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="209aa-165">La tabla siguiente muestra el lenguaje que se permite en las plantillas:</span><span class="sxs-lookup"><span data-stu-id="209aa-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="209aa-166">Expresión</span><span class="sxs-lookup"><span data-stu-id="209aa-166">Expression</span></span> | <span data-ttu-id="209aa-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="209aa-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="209aa-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="209aa-168">$(prop)</span></span> |<span data-ttu-id="209aa-169">Referencia a una propiedad de evento con el nombre especificado.</span><span class="sxs-lookup"><span data-stu-id="209aa-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="209aa-170">Los nombres de propiedad no distinguen mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="209aa-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="209aa-171">Esta expresión se resuelve en el valor de texto de la propiedad o en una cadena vacía, si la propiedad no está presente.</span><span class="sxs-lookup"><span data-stu-id="209aa-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="209aa-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="209aa-172">$(prop, n)</span></span> |<span data-ttu-id="209aa-173">Igual que el caso anterior, pero el texto se recorta explícitamente en n caracteres, por ejemplo, $(title, 20) recorta el contenido de la propiedad title en 20 caracteres.</span><span class="sxs-lookup"><span data-stu-id="209aa-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="209aa-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="209aa-174">.(prop, n)</span></span> |<span data-ttu-id="209aa-175">Igual que el caso anterior, pero se agregan tres puntos como sufijo al texto debido a que se recorta.</span><span class="sxs-lookup"><span data-stu-id="209aa-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="209aa-176">El tamaño total de la cadena recortada y el sufijo no exceden los n caracteres.</span><span class="sxs-lookup"><span data-stu-id="209aa-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="209aa-177">.(title, 20) con una propiedad de entrada de "Esta es la línea del título", con lo que queda como **Esta es la línea ...**</span><span class="sxs-lookup"><span data-stu-id="209aa-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="209aa-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="209aa-178">%(prop)</span></span> |<span data-ttu-id="209aa-179">Similar a $(name), salvo en que la salida está codificada en URI.</span><span class="sxs-lookup"><span data-stu-id="209aa-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="209aa-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="209aa-180">#(prop)</span></span> |<span data-ttu-id="209aa-181">Se usa en las plantillas JSON (por ejemplo, para plantillas de iOS y Android).</span><span class="sxs-lookup"><span data-stu-id="209aa-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="209aa-182">Esta función se comporta igual que $(prop) especificada anteriormente, salvo cuando se usa en plantillas de JSON (por ejemplo, plantillas de Apple).</span><span class="sxs-lookup"><span data-stu-id="209aa-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="209aa-183">En este caso, si esta función no está entre “{‘,’}” (por ejemplo, ‘myJsonProperty’ : ‘#(name)’) y se evalúa en un número en formato JavaScript, por ejemplo, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, el JSON de salida es un número.</span><span class="sxs-lookup"><span data-stu-id="209aa-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="209aa-184">Por ejemplo, ‘badge : ‘#(name)’ se convierte en ‘badge’ : 40 (y no ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="209aa-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="209aa-185">‘texto’ o “texto”</span><span class="sxs-lookup"><span data-stu-id="209aa-185">‘text’ or “text”</span></span> |<span data-ttu-id="209aa-186">Un literal.</span><span class="sxs-lookup"><span data-stu-id="209aa-186">A literal.</span></span> <span data-ttu-id="209aa-187">Los literales contienen texto arbitrario encerrado entre comillas simples o dobles.</span><span class="sxs-lookup"><span data-stu-id="209aa-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="209aa-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="209aa-188">expr1 + expr2</span></span> |<span data-ttu-id="209aa-189">El operador de concatenación que une dos expresiones en una sola cadena.</span><span class="sxs-lookup"><span data-stu-id="209aa-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="209aa-190">Las expresiones pueden estar en cualquiera de los formatos anteriores.</span><span class="sxs-lookup"><span data-stu-id="209aa-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="209aa-191">Cuando se usa la concatenación, toda la expresión debe estar entre {}.</span><span class="sxs-lookup"><span data-stu-id="209aa-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="209aa-192">Por ejemplo, {$(prop) + ‘ - ’ + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="209aa-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="209aa-193">El siguiente ejemplo no es una plantilla XML válida:</span><span class="sxs-lookup"><span data-stu-id="209aa-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="209aa-194">Como se explicó anteriormente, cuando se usa la concatenación, las expresiones deben ir entre llaves.</span><span class="sxs-lookup"><span data-stu-id="209aa-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="209aa-195">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="209aa-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

