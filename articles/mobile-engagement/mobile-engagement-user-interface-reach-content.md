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
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="a0176-103">¿Cómo toomanage Hola contenido exclusivo de tipos diferentes de hello de campañas de notificación de inserción</span><span class="sxs-lookup"><span data-stu-id="a0176-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="a0176-104">Puede usar la sección de contenido de Hola de alcance de la campaña toomodify Hola contenido nuevo de los anuncios, sondeos, inserta datos e iconos (solo Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="a0176-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="a0176-105">configuración de contenido de Hola de las campañas de inserción es toohello específicos de tipo de campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="a0176-106">Tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="a0176-106">Content types:</span></span>
* <span data-ttu-id="a0176-107">Anuncios</span><span class="sxs-lookup"><span data-stu-id="a0176-107">Announcements</span></span>
* <span data-ttu-id="a0176-108">Sondeos</span><span class="sxs-lookup"><span data-stu-id="a0176-108">Polls</span></span>
* <span data-ttu-id="a0176-109">Inserciones de datos</span><span class="sxs-lookup"><span data-stu-id="a0176-109">Data pushes</span></span>
* <span data-ttu-id="a0176-110">Mosaicos (solo en Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a0176-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="a0176-111">Contenido de anuncios</span><span class="sxs-lookup"><span data-stu-id="a0176-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="a0176-113">Elija el tipo de saludo del anuncio:</span><span class="sxs-lookup"><span data-stu-id="a0176-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="a0176-114">Solo notificación: es una notificación estándar simple.</span><span class="sxs-lookup"><span data-stu-id="a0176-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="a0176-115">Lo que significa que, si un usuario hace clic en él, no aparecerá vista adicional, pero solo Hola acción asociada, se producirá tooit.</span><span class="sxs-lookup"><span data-stu-id="a0176-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="a0176-116">Anuncio de texto: es una notificación que involucre a Hola usuario toohave un vistazo a una vista de texto.</span><span class="sxs-lookup"><span data-stu-id="a0176-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="a0176-117">Anuncio de Web: es una notificación que involucre a Hola usuario toohave un vistazo a una vista web.</span><span class="sxs-lookup"><span data-stu-id="a0176-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="a0176-118">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a0176-118">See also</span></span>
* <span data-ttu-id="a0176-119">[Cobertura - Guía práctica - Anuncios][Link 3]</span><span class="sxs-lookup"><span data-stu-id="a0176-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="a0176-120">Acerca de los anuncios de visualización web:</span><span class="sxs-lookup"><span data-stu-id="a0176-120">About Web View Announcements:</span></span>
<span data-ttu-id="a0176-121">Apariciones del patrón de Hola "{deviceid}" en el código de hello HTML o código JavaScript que proporciona aquí se reemplazará automáticamente por identificador de hello de dispositivo de Hola que muestra el anuncio de Hola.</span><span class="sxs-lookup"><span data-stu-id="a0176-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="a0176-122">Se trata de un identificadores de dispositivos de Azure Mobile Engagement de manera sencilla tooretrieve en externo hospedado en el área de operaciones de servicio web.</span><span class="sxs-lookup"><span data-stu-id="a0176-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="a0176-123">Si desea que toocreate una completa Pantalla vista web (sin Hola botones predeterminados acción y salir proporcionamos) puede usar Hola siguientes funciones de código JavaScript de anuncio de vista web:</span><span class="sxs-lookup"><span data-stu-id="a0176-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="a0176-124">realizar acción de anuncio Hola: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="a0176-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="a0176-125">salir del anuncio de Hola: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="a0176-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="a0176-126">Elija la acción:</span><span class="sxs-lookup"><span data-stu-id="a0176-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="a0176-127">Acerca de las direcciones URL de la acción:</span><span class="sxs-lookup"><span data-stu-id="a0176-127">About Action URLs:</span></span>
<span data-ttu-id="a0176-128">Cualquier dirección URL que puede ser interpretada por el sistema operativo de destino de un dispositivo puede utilizarse como una dirección URL de la acción.</span><span class="sxs-lookup"><span data-stu-id="a0176-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="a0176-129">Cualquier dirección URL dedicada que su aplicación podría compatibilidad (por ejemplo, los usuarios de toomake saltar tooa de pantalla determinada) también se puede utilizar como una dirección URL de acción.</span><span class="sxs-lookup"><span data-stu-id="a0176-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="a0176-130">Cada repetición del patrón de Hola {deviceid} se sustituye automáticamente por identificador de hello de dispositivo de hello realizar acción Hola.</span><span class="sxs-lookup"><span data-stu-id="a0176-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="a0176-131">Esto puede resultar tooeasily usa identificadores de dispositivo de Azure Mobile Engagement de recuperar a través de un servicio web externo hospedado en el área de operaciones.</span><span class="sxs-lookup"><span data-stu-id="a0176-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="a0176-132">**Acciones de Android + iOS**</span><span class="sxs-lookup"><span data-stu-id="a0176-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="a0176-133">Abrir una página web</span><span class="sxs-lookup"><span data-stu-id="a0176-133">Open a web page</span></span>
  * <span data-ttu-id="a0176-134">http://\[dominio-sitio-web\]</span><span class="sxs-lookup"><span data-stu-id="a0176-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a0176-135">Ejemplo: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="a0176-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a0176-136">Enviar un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="a0176-136">Send an e-mail</span></span>
  * <span data-ttu-id="a0176-137">mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\]</span><span class="sxs-lookup"><span data-stu-id="a0176-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a0176-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="a0176-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a0176-139">Enviar un SMS</span><span class="sxs-lookup"><span data-stu-id="a0176-139">Send a SMS</span></span>
  * <span data-ttu-id="a0176-140">sms:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="a0176-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a0176-141">Ejemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a0176-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a0176-142">Marcar un número de teléfono</span><span class="sxs-lookup"><span data-stu-id="a0176-142">Dial a phone number</span></span>
  * <span data-ttu-id="a0176-143">tel:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="a0176-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a0176-144">Ejemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a0176-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="a0176-145">**Acciones solo para Android**</span><span class="sxs-lookup"><span data-stu-id="a0176-145">**Android only actions**</span></span>
  * <span data-ttu-id="a0176-146">Descargar una aplicación de hello Play Store</span><span class="sxs-lookup"><span data-stu-id="a0176-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="a0176-147">market://details?id=\[paquete de la aplicación\]</span><span class="sxs-lookup"><span data-stu-id="a0176-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="a0176-148">Ejemplo:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="a0176-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="a0176-149">Iniciar una búsqueda localizada geográficamente</span><span class="sxs-lookup"><span data-stu-id="a0176-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="a0176-150">geo:0,0?q=\[consulta de búsqueda\]</span><span class="sxs-lookup"><span data-stu-id="a0176-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="a0176-151">Ejemplo:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="a0176-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="a0176-152">**Acciones solo para iOS**</span><span class="sxs-lookup"><span data-stu-id="a0176-152">**iOS only actions**</span></span>
  * <span data-ttu-id="a0176-153">Descargar una aplicación de hello tienda de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="a0176-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="a0176-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="a0176-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="a0176-155">Ejemplo: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="a0176-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="a0176-156">Acciones de Windows</span><span class="sxs-lookup"><span data-stu-id="a0176-156">Windows Actions</span></span>
  * <span data-ttu-id="a0176-157">Abrir una página web</span><span class="sxs-lookup"><span data-stu-id="a0176-157">Open a web page</span></span>
  * <span data-ttu-id="a0176-158">http://\[dominio-sitio-web\]</span><span class="sxs-lookup"><span data-stu-id="a0176-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a0176-159">Ejemplo: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="a0176-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a0176-160">Enviar un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="a0176-160">Send an e-mail</span></span>
  * <span data-ttu-id="a0176-161">mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\]</span><span class="sxs-lookup"><span data-stu-id="a0176-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a0176-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="a0176-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a0176-163">Enviar un SMS (requiere la aplicación Skype)</span><span class="sxs-lookup"><span data-stu-id="a0176-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="a0176-164">sms:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="a0176-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a0176-165">Ejemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a0176-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a0176-166">Marcar un número de teléfono (requiere la aplicación Skype)</span><span class="sxs-lookup"><span data-stu-id="a0176-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="a0176-167">tel:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="a0176-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a0176-168">Ejemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a0176-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="a0176-169">Descargar una aplicación de hello Play Store</span><span class="sxs-lookup"><span data-stu-id="a0176-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="a0176-170">ms-windows-store:PDP?PFN=\[id. del paquete de la aplicación\]</span><span class="sxs-lookup"><span data-stu-id="a0176-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="a0176-171">Ejemplo:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="a0176-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="a0176-172">Iniciar una búsqueda en Mapas de Bing</span><span class="sxs-lookup"><span data-stu-id="a0176-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="a0176-173">bingmaps:?q=\[consulta de búsqueda\]</span><span class="sxs-lookup"><span data-stu-id="a0176-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="a0176-174">Ejemplo:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="a0176-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="a0176-175">Utilice un esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="a0176-175">Use a custom scheme</span></span>
  * <span data-ttu-id="a0176-176">\[esquema personalizado\]://\[parámetros del esquema personalizado\]</span><span class="sxs-lookup"><span data-stu-id="a0176-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="a0176-177">Ejemplo:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="a0176-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="a0176-178">Utilizar datos de paquete (se necesita una aplicación de la tienda para leer la extensión)</span><span class="sxs-lookup"><span data-stu-id="a0176-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="a0176-179">\[carpeta\]\[datos\].\[extensión\]</span><span class="sxs-lookup"><span data-stu-id="a0176-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="a0176-180">Ejemplo:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="a0176-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="a0176-181">Crear una dirección URL de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="a0176-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="a0176-182">Vea Hola sección "Configuración" de hello <UI Documentation> para obtener instrucciones sobre la creación de una dirección URL de seguimiento que le permitirá toodownload a los usuarios una de las otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a0176-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="a0176-183">Definir Hola textos del anuncio</span><span class="sxs-lookup"><span data-stu-id="a0176-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="a0176-184">Rellene Hola título, contenido y textos de botón del anuncio.</span><span class="sxs-lookup"><span data-stu-id="a0176-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="a0176-185">Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a0176-186">La audiencia de destino puede basarse en los comentarios de Hola de si solo se ha insertado esta campaña, respondidos, accionado o cerrado.</span><span class="sxs-lookup"><span data-stu-id="a0176-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a0176-187">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a0176-187">See also</span></span>
* <span data-ttu-id="a0176-188">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a0176-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="a0176-189">Contenido de sondeos</span><span class="sxs-lookup"><span data-stu-id="a0176-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="a0176-191">Rellene Hola título, descripción y textos de botón del anuncio.</span><span class="sxs-lookup"><span data-stu-id="a0176-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="a0176-192">A continuación, agregue preguntas y opciones para hello respuestas tooyour preguntas.</span><span class="sxs-lookup"><span data-stu-id="a0176-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="a0176-193">Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a0176-194">La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="a0176-195">La audiencia de destino también puede basarse en los comentarios de respuesta de sondeo, donde elección de pregunta y respuesta de Hola se utilizan como criterios.</span><span class="sxs-lookup"><span data-stu-id="a0176-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="a0176-196">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a0176-196">See also</span></span>
* <span data-ttu-id="a0176-197">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a0176-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="a0176-198">Contenido de las inserciones de datos</span><span class="sxs-lookup"><span data-stu-id="a0176-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="a0176-200">Elija el tipo de saludo de los datos:</span><span class="sxs-lookup"><span data-stu-id="a0176-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="a0176-201">Texto</span><span class="sxs-lookup"><span data-stu-id="a0176-201">Text</span></span>
* <span data-ttu-id="a0176-202">Datos binarios</span><span class="sxs-lookup"><span data-stu-id="a0176-202">Binary data</span></span>
* <span data-ttu-id="a0176-203">Datos de Base64</span><span class="sxs-lookup"><span data-stu-id="a0176-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="a0176-204">Definir el contenido de Hola de los datos</span><span class="sxs-lookup"><span data-stu-id="a0176-204">Define hello content of your data</span></span>
* <span data-ttu-id="a0176-205">Si seleccionó toopush datos de texto, copie y pegue el texto hello en cuadro "contenido" Hola.</span><span class="sxs-lookup"><span data-stu-id="a0176-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="a0176-206">Si seleccionó toopush datos binarios o base64, utilice tooupload de botón de "cargar el archivo" hello el archivo.</span><span class="sxs-lookup"><span data-stu-id="a0176-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="a0176-207">Puede tener como destino una audiencia de una campaña futura basada en los comentarios de Hola alcance de la forma en que los usuarios han respondido toothis campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="a0176-208">La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña.</span><span class="sxs-lookup"><span data-stu-id="a0176-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a0176-209">Consulte también</span><span class="sxs-lookup"><span data-stu-id="a0176-209">See also</span></span>
* <span data-ttu-id="a0176-210">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a0176-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="a0176-211">Contenido de los mosaicos (solo en Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a0176-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="a0176-213">Definir el contenido de hello del título</span><span class="sxs-lookup"><span data-stu-id="a0176-213">Define hello content of your tile</span></span>
<span data-ttu-id="a0176-214">carga de mosaico de Hello es hello toobe de texto mostrado en el icono de saludo de la aplicación en dispositivos Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a0176-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="a0176-215">Una inserción de mosaico es la versión de servicio de notificaciones de inserción de Microsoft (MPNS) de Hola de una inserción nativa para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a0176-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="a0176-216">tipo de inserción de mosaico de Hello es el único tipo de inserción de Hola que no tiene una respuesta y por lo que no se puede compilar audiencia Hola de campañas futuras en resultados de Hola de una campaña de inserción de mosaico.</span><span class="sxs-lookup"><span data-stu-id="a0176-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="a0176-217">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a0176-217">See also</span></span>
* <span data-ttu-id="a0176-218">[Documentación de la API - API de cobertura - Inserción nativa][Link 4]</span><span class="sxs-lookup"><span data-stu-id="a0176-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

