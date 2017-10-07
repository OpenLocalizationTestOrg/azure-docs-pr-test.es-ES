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
# <a name="how-toouse-targeting-criteria-toosend-push-campaigns-tooa-select-subset-of-your-users"></a><span data-ttu-id="34499-103">¿Cómo toouse destinatarios criterios toosend inserción campañas tooa Seleccionar subconjunto de usuarios</span><span class="sxs-lookup"><span data-stu-id="34499-103">How toouse targeting criteria toosend push campaigns tooa select subset of your users</span></span>
<span data-ttu-id="34499-104">La audiencia de destino según unos criterios específicos con el botón de "Nuevo criterio" hello es uno de los conceptos de hello más eficaces en Azure Mobile Engagement que le ayuda a que enviar relevante inserción notificaciones de que los clientes de hello responderá tooinstead de spam todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="34499-104">Targeting your audience by specific criteria with hello "New Criteria" button is one of hello most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that hello customers will respond tooinstead of Spamming everyone.</span></span> <span data-ttu-id="34499-105">Puede limitar la audiencia basándose en criterios estándares y simular inserciones toodetermine cuántas personas recibirán la notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="34499-105">You can limit your audience based on standard criteria and simulate pushes toodetermine how many people will receive hello notification.</span></span>

<span data-ttu-id="34499-106">**Consulte también:**</span><span class="sxs-lookup"><span data-stu-id="34499-106">**See also:**</span></span>

* <span data-ttu-id="34499-107">[Documentación de la interfaz de usuario - Alcance - Nueva campaña de inserción][Link 27]</span><span class="sxs-lookup"><span data-stu-id="34499-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="34499-108">Dentro de los criterios de audiencia se pueden incluir:</span><span class="sxs-lookup"><span data-stu-id="34499-108">Audience criteria can include:</span></span>
* <span data-ttu-id="34499-109">** Technicals: ** puede tener como destino en función de hello misma información técnica puede ver en hello análisis y secciones de Monitor.</span><span class="sxs-lookup"><span data-stu-id="34499-109">**Technicals: ** You can target based on hello same technical information you can see in hello Analytics and Monitor sections.</span></span> <span data-ttu-id="34499-110">**Consulte también**: [Documentación de la interfaz de usuario - Análisis][Link 15], [Documentación de la interfaz de usuario - Supervisión][Link 16]</span><span class="sxs-lookup"><span data-stu-id="34499-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="34499-111">**Ubicación:** las aplicaciones que usan "informes de ubicación en tiempo Real" con barrera geográfica pueden usar ubicación geográfica como una tootarget criterios una audiencia de hello ubicación GPS.</span><span class="sxs-lookup"><span data-stu-id="34499-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria tootarget an audience from hello GPS location.</span></span> <span data-ttu-id="34499-112">Llamada "Informes de ubicación de área diferida" también ser utilizado tootarget una audiencia de ubicación de teléfono móvil de hello ("informes de ubicación en tiempo Real" y "Diferida área informes de ubicación" deben activarse desde Hola SDK).</span><span class="sxs-lookup"><span data-stu-id="34499-112">"Lazy Area Location Reporting" call also be used tootarget an audience from hello cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from hello SDK).</span></span> <span data-ttu-id="34499-113">**Consulte también:**[Documentación del SDK - iOS -][Link 5], [Documentación del SDK - Android - Integración][Link 5]</span><span class="sxs-lookup"><span data-stu-id="34499-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="34499-114">**Comentarios sobre la cobertura:** puede tener como destino su audiencia según sus comentarios de notificaciones de cobertura anteriores a través de comentarios sobre la cobertura de Anuncios, Sondeos e Inserciones de datos.</span><span class="sxs-lookup"><span data-stu-id="34499-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="34499-115">Esto le permite destino toobetter la audiencia después de dos o tres alcancen las campañas que se podría Hola la primera vez.</span><span class="sxs-lookup"><span data-stu-id="34499-115">This enables you toobetter target your audience after two or three reach campaigns than you could hello first time.</span></span> <span data-ttu-id="34499-116">Se puede utilizar también toofilter los usuarios que ya ha recibido una notificación con contenido similar, estableciendo una campaña tooNOT enviará toousers que han recibido una determinada campaña anterior.</span><span class="sxs-lookup"><span data-stu-id="34499-116">It can also be used toofilter out users who already received a notification with similar content, by setting a campaign tooNOT be sent toousers who already received a specific previous campaign.</span></span> <span data-ttu-id="34499-117">Incluso puede excluir a los usuarios incluidos en una campaña específica que está todavía activa para recibir inserciones nuevas.</span><span class="sxs-lookup"><span data-stu-id="34499-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="34499-118">**Vea también:**[Documentación de la interfaz de usuario - Cobertura - Insertar contenido][Link 29]</span><span class="sxs-lookup"><span data-stu-id="34499-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="34499-119">**Seguimiento de la instalación:** puede realizar un seguimiento de información basada en dónde instalaron los usuarios su aplicación.</span><span class="sxs-lookup"><span data-stu-id="34499-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="34499-120">**Consulte también:**[Documentación de interfaz de usuario - Configuración][Link 20]</span><span class="sxs-lookup"><span data-stu-id="34499-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="34499-121">**Perfil de usuario:** puede destino basándose en información de usuario estándar y usted puede destino basándose en información de la aplicación personalizada de Hola que haya creado.</span><span class="sxs-lookup"><span data-stu-id="34499-121">**User Profile:** You can target based on standard user information and you can target based on hello custom app info that you have created.</span></span> <span data-ttu-id="34499-122">Esto incluye los usuarios que han iniciado sesión en y los usuarios que responder a preguntas específicas que se ha solicitado tooset en hello propia aplicación en lugar de simplemente cómo han respondido tooprevious campañas.</span><span class="sxs-lookup"><span data-stu-id="34499-122">This includes users who are currently logged in and users that have answered specific questions you have asked them tooset in hello app itself instead of just how they have responded tooprevious campaigns.</span></span> <span data-ttu-id="34499-123">Toda la información de la aplicación definida para la aplicación aparece en esta lista.</span><span class="sxs-lookup"><span data-stu-id="34499-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="34499-124">Segmentos: también puede orientarse en función de segmentos que ha creado según el comportamiento específico del usuario que contiene varios criterios.</span><span class="sxs-lookup"><span data-stu-id="34499-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="34499-125">Todos los segmentos definidos para la aplicación aparecen en esta lista.</span><span class="sxs-lookup"><span data-stu-id="34499-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="34499-126">**Consulte también:**[Documentación de interfaz de usuario - Segmentos][Link 18]</span><span class="sxs-lookup"><span data-stu-id="34499-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="34499-127">**Información de la aplicación:** etiquetas de información de aplicación personalizadas se pueden crear de comportamiento del usuario tootrack "Configuración".</span><span class="sxs-lookup"><span data-stu-id="34499-127">**App Info:** Custom App Info Tags can be created from “Settings” tootrack user behavior.</span></span> <span data-ttu-id="34499-128">**Consulte también:**[Documentación de interfaz de usuario - Configuración][Link 20]</span><span class="sxs-lookup"><span data-stu-id="34499-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="34499-129">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="34499-129">Example:</span></span>
<span data-ttu-id="34499-130">Si desea que toopush un anuncio solo toohello subjuego de los usuarios que ha llevado a cabo una aplicación de compra acción.</span><span class="sxs-lookup"><span data-stu-id="34499-130">If you want toopush an announcement only toohello sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="34499-131">Ir a página de configuración de aplicación tooyour, seleccione el menú de "Información de la aplicación" hello y seleccione "Nueva información de aplicación"</span><span class="sxs-lookup"><span data-stu-id="34499-131">Go tooyour application settings page, select hello "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="34499-132">Registre una nueva información de aplicación de booleano denominada "inAppPurchase"</span><span class="sxs-lookup"><span data-stu-id="34499-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="34499-133">Hacer que su aplicación establecer esta información de aplicación demasiado "true" cuando el usuario de hello correctamente realiza una compra en la aplicación (mediante el uso de hello sendAppInfo ("inAppPurchase",...) función)</span><span class="sxs-lookup"><span data-stu-id="34499-133">Make your application set this app info too"true" when hello user successfully performs an in-app purchase (by using hello sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="34499-134">Si no desea toodo esto desde la aplicación, puede hacerlo desde el back-end a través de API de dispositivo de hello)</span><span class="sxs-lookup"><span data-stu-id="34499-134">If you don't want toodo this from your application, you can do it from your backend by using hello device API)</span></span>
5. <span data-ttu-id="34499-135">A continuación, simplemente deberá toocreate anuncio, con un criterio limitar su toousers de audiencia tener "inAppPurchase" establecido demasiado "true")</span><span class="sxs-lookup"><span data-stu-id="34499-135">Then, you just need toocreate your announcement, with a criterion limiting your audience toousers having "inAppPurchase" set too"true")</span></span>

> [!NOTE]
> <span data-ttu-id="34499-136">Según los criterios que no sea de etiquetas de información de aplicación de destino, requiere información de toogather de Azure Mobile Engagement de dispositivos de los usuarios antes de inserción de Hola se envía y puede producir un retraso.</span><span class="sxs-lookup"><span data-stu-id="34499-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement toogather information from your users' devices before hello push is sent and so can cause a delay.</span></span> <span data-ttu-id="34499-137">Las opciones de configuración de inserción complejas (como la actualización de insignias) también pueden retrasar las inserciones.</span><span class="sxs-lookup"><span data-stu-id="34499-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="34499-138">Usando una campaña "Monoestable" de hello API de inserción es absoluta método de inserción hello más rápido de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="34499-138">Using a "one shot" campaign from hello Push API is hello absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="34499-139">Usar sólo las etiquetas de información de aplicación como criterios de inserción para una campaña de cobertura (ya sea de hello API de cobertura o hello interfaz de usuario) es Hola next más rápido (método) puesto que las etiquetas de información de aplicación se almacenan en el lado del servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="34499-139">Using only app info tags as push criteria for a Reach campaign (either from hello Reach API or hello UI) is hello next fastest method since app info tags are stored on hello server side.</span></span> <span data-ttu-id="34499-140">Usando otros criterios de destino para una campaña de inserción es Hola método de inserción más flexible pero más lento debido a que Azure Mobile Engagement tiene dispositivos de hello tooquery de campaña de orden toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="34499-140">Using other targeting criteria for a push campaign is hello most flexible but slowest push method since Azure Mobile Engagement has tooquery hello devices in order toosend hello campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="34499-142">Las opciones de criterios se aplican a:</span><span class="sxs-lookup"><span data-stu-id="34499-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="34499-143">**Notas técnicas**</span><span class="sxs-lookup"><span data-stu-id="34499-143">**Technicals**</span></span>     
* <span data-ttu-id="34499-144">Nombre del firmware: el nombre del firmware.</span><span class="sxs-lookup"><span data-stu-id="34499-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="34499-145">Versión del firmware: la versión del firmware.</span><span class="sxs-lookup"><span data-stu-id="34499-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="34499-146">Modelo de dispositivo: el modelo del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34499-146">Device model:    Device model</span></span>
* <span data-ttu-id="34499-147">Fabricante del dispositivo: el fabricante del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="34499-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="34499-148">Versión de la aplicación: la versión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="34499-148">Application version:    Application version</span></span>
* <span data-ttu-id="34499-149">Nombre del operador: el nombre del operador.</span><span class="sxs-lookup"><span data-stu-id="34499-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="34499-150">País del operador: el país del operador, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="34499-151">Tipo de red: el tipo de red.</span><span class="sxs-lookup"><span data-stu-id="34499-151">Network type:    Network type</span></span>
* <span data-ttu-id="34499-152">Configuración regional: la configuración regional.</span><span class="sxs-lookup"><span data-stu-id="34499-152">Locale:    Locale</span></span>
* <span data-ttu-id="34499-153">Tamaño de pantalla: el tamaño de pantalla.</span><span class="sxs-lookup"><span data-stu-id="34499-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="34499-154">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="34499-154">**Location**</span></span>      
* <span data-ttu-id="34499-155">Última área conocida: país, región, localidad.</span><span class="sxs-lookup"><span data-stu-id="34499-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="34499-156">Geovallado en tiempo real: lista de puntos de interés (nombre, acciones), punto de interés circular (nombre, latitud, longitud, radio en metros)</span><span class="sxs-lookup"><span data-stu-id="34499-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="34499-157">**Comentarios sobre la cobertura**</span><span class="sxs-lookup"><span data-stu-id="34499-157">**Reach feedback**</span></span>     
* <span data-ttu-id="34499-158">Comentarios de anuncio: anuncio, comentarios.</span><span class="sxs-lookup"><span data-stu-id="34499-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="34499-159">Comentarios de sondeo: sondeo, comentarios.</span><span class="sxs-lookup"><span data-stu-id="34499-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="34499-160">Comentarios de respuesta de sondeo: comentarios de respuesta de sondeo, pregunta, opción.</span><span class="sxs-lookup"><span data-stu-id="34499-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="34499-161">Comentarios de inserción de datos: inserción de datos, comentarios.</span><span class="sxs-lookup"><span data-stu-id="34499-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="34499-162">**Seguimiento de la instalación**</span><span class="sxs-lookup"><span data-stu-id="34499-162">**Install Tracking**</span></span>     
* <span data-ttu-id="34499-163">Tienda: tienda, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="34499-164">Origen: origen, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="34499-165">**Perfil de usuario**</span><span class="sxs-lookup"><span data-stu-id="34499-165">**User profile**</span></span>     
* <span data-ttu-id="34499-166">Género: hombre o mujer, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="34499-167">Fecha de nacimiento: operador, fecha, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="34499-168">Participar: verdadero o falso, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="34499-169">**Información de la aplicación**</span><span class="sxs-lookup"><span data-stu-id="34499-169">**App Info**</span></span>      
* <span data-ttu-id="34499-170">Cadena: cadena, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-170">String:    String, undefined</span></span>
* <span data-ttu-id="34499-171">Fecha: operador, fecha, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="34499-172">Entero: operador, número, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="34499-173">Booleano: verdadero o falso, sin definir.</span><span class="sxs-lookup"><span data-stu-id="34499-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="34499-174">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="34499-174">**Segment**</span></span>    
* <span data-ttu-id="34499-175">Nombre de segmentos (de la lista desplegable), exclusión (usuarios de destino que no forman parte de este segmento).</span><span class="sxs-lookup"><span data-stu-id="34499-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

