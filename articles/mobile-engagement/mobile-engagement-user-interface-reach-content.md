---
title: Interfaz de usuario de Azure Mobile Engagement - Contenido de cobertura
description: "Aprenda a administrar el contenido exclusivo de los diferentes tipos de campañas de notificaciones de inserción en Azure Mobile Engagement"
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
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="09c8d-103">Cómo administrar el contenido exclusivo de los diferentes tipos de campañas de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="09c8d-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="09c8d-104">Puede utilizar la sección de contenido de una nueva campaña de cobertura para modificar el contenido de los anuncios, sondeos, inserción de datos y mosaicos (solo en Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="09c8d-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="09c8d-105">La configuración del contenido de las campañas de inserción es específica del tipo de campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="09c8d-106">Tipos de contenido:</span><span class="sxs-lookup"><span data-stu-id="09c8d-106">Content types:</span></span>
* <span data-ttu-id="09c8d-107">Anuncios</span><span class="sxs-lookup"><span data-stu-id="09c8d-107">Announcements</span></span>
* <span data-ttu-id="09c8d-108">Sondeos</span><span class="sxs-lookup"><span data-stu-id="09c8d-108">Polls</span></span>
* <span data-ttu-id="09c8d-109">Inserciones de datos</span><span class="sxs-lookup"><span data-stu-id="09c8d-109">Data pushes</span></span>
* <span data-ttu-id="09c8d-110">Mosaicos (solo en Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="09c8d-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="09c8d-111">Contenido de anuncios</span><span class="sxs-lookup"><span data-stu-id="09c8d-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="09c8d-113">Elija el tipo de anuncio:</span><span class="sxs-lookup"><span data-stu-id="09c8d-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="09c8d-114">Solo notificación: es una notificación estándar simple.</span><span class="sxs-lookup"><span data-stu-id="09c8d-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="09c8d-115">Lo que significa que si un usuario hace clic en él, no aparecerá ninguna vista adicional, pero se producirá solo la acción asociada a él.</span><span class="sxs-lookup"><span data-stu-id="09c8d-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="09c8d-116">Anuncio de texto: es una notificación que compromete al usuario a echar un vistazo a una vista de texto.</span><span class="sxs-lookup"><span data-stu-id="09c8d-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="09c8d-117">Anuncio web: es una notificación que compromete al usuario a echar un vistazo a una vista de texto.</span><span class="sxs-lookup"><span data-stu-id="09c8d-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="09c8d-118">Consulte también</span><span class="sxs-lookup"><span data-stu-id="09c8d-118">See also</span></span>
* <span data-ttu-id="09c8d-119">[Cobertura - Guía práctica - Anuncios][Link 3]</span><span class="sxs-lookup"><span data-stu-id="09c8d-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="09c8d-120">Acerca de los anuncios de visualización web:</span><span class="sxs-lookup"><span data-stu-id="09c8d-120">About Web View Announcements:</span></span>
<span data-ttu-id="09c8d-121">Las apariciones del patrón "{deviceid}" en el código HTML o JavaScript que proporcione aquí se reemplazarán automáticamente por el identificador del dispositivo que muestra el anuncio.</span><span class="sxs-lookup"><span data-stu-id="09c8d-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="09c8d-122">Se trata de una manera fácil de recuperar identificadores de dispositivo de Azure Mobile Engagement en un servicio web externo hospedado en su oficina.</span><span class="sxs-lookup"><span data-stu-id="09c8d-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="09c8d-123">Si desea crear una vista web de pantalla completa (sin los botones predeterminados de Acción y Salir proporcionados) puede utilizar las siguientes funciones desde código de JavaScript del anuncio de la vista web:</span><span class="sxs-lookup"><span data-stu-id="09c8d-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="09c8d-124">realizar la acción del anuncio: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="09c8d-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="09c8d-125">salir del anuncio: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="09c8d-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="09c8d-126">Elija la acción:</span><span class="sxs-lookup"><span data-stu-id="09c8d-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="09c8d-127">Acerca de las direcciones URL de la acción:</span><span class="sxs-lookup"><span data-stu-id="09c8d-127">About Action URLs:</span></span>
<span data-ttu-id="09c8d-128">Cualquier dirección URL que puede ser interpretada por el sistema operativo de destino de un dispositivo puede utilizarse como una dirección URL de la acción.</span><span class="sxs-lookup"><span data-stu-id="09c8d-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="09c8d-129">Cualquier dirección URL específica que pueda admitir su aplicación (por ejemplo, para hacer saltar a los usuarios a una pantalla concreta) también puede utilizarse como una dirección URL de acción.</span><span class="sxs-lookup"><span data-stu-id="09c8d-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="09c8d-130">Cada repetición del patrón {deviceid} se reemplaza automáticamente por el identificador del dispositivo que realiza la acción.</span><span class="sxs-lookup"><span data-stu-id="09c8d-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="09c8d-131">Esto puede utilizarse para recuperar fácilmente los identificadores de dispositivo Azure Mobile Engagement a través de un servicio web externo hospedado en su área de operaciones.</span><span class="sxs-lookup"><span data-stu-id="09c8d-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="09c8d-132">**Acciones de Android + iOS**</span><span class="sxs-lookup"><span data-stu-id="09c8d-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="09c8d-133">Abrir una página web</span><span class="sxs-lookup"><span data-stu-id="09c8d-133">Open a web page</span></span>
  * <span data-ttu-id="09c8d-134">http://\[dominio-sitio-web\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="09c8d-135">Ejemplo: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="09c8d-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="09c8d-136">Enviar un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="09c8d-136">Send an e-mail</span></span>
  * <span data-ttu-id="09c8d-137">mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="09c8d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="09c8d-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="09c8d-139">Enviar un SMS</span><span class="sxs-lookup"><span data-stu-id="09c8d-139">Send a SMS</span></span>
  * <span data-ttu-id="09c8d-140">sms:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="09c8d-141">Ejemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="09c8d-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="09c8d-142">Marcar un número de teléfono</span><span class="sxs-lookup"><span data-stu-id="09c8d-142">Dial a phone number</span></span>
  * <span data-ttu-id="09c8d-143">tel:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="09c8d-144">Ejemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="09c8d-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="09c8d-145">**Acciones solo para Android**</span><span class="sxs-lookup"><span data-stu-id="09c8d-145">**Android only actions**</span></span>
  * <span data-ttu-id="09c8d-146">Descargar una aplicación de Play Store</span><span class="sxs-lookup"><span data-stu-id="09c8d-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="09c8d-147">market://details?id=\[paquete de la aplicación\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="09c8d-148">Ejemplo:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="09c8d-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="09c8d-149">Iniciar una búsqueda localizada geográficamente</span><span class="sxs-lookup"><span data-stu-id="09c8d-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="09c8d-150">geo:0,0?q=\[consulta de búsqueda\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="09c8d-151">Ejemplo:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="09c8d-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="09c8d-152">**Acciones solo para iOS**</span><span class="sxs-lookup"><span data-stu-id="09c8d-152">**iOS only actions**</span></span>
  * <span data-ttu-id="09c8d-153">Descargar una aplicación de la App Store</span><span class="sxs-lookup"><span data-stu-id="09c8d-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="09c8d-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="09c8d-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="09c8d-155">Ejemplo: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="09c8d-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="09c8d-156">Acciones de Windows</span><span class="sxs-lookup"><span data-stu-id="09c8d-156">Windows Actions</span></span>
  * <span data-ttu-id="09c8d-157">Abrir una página web</span><span class="sxs-lookup"><span data-stu-id="09c8d-157">Open a web page</span></span>
  * <span data-ttu-id="09c8d-158">http://\[dominio-sitio-web\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="09c8d-159">Ejemplo: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="09c8d-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="09c8d-160">Enviar un correo electrónico</span><span class="sxs-lookup"><span data-stu-id="09c8d-160">Send an e-mail</span></span>
  * <span data-ttu-id="09c8d-161">mailto:\[destinatario-correo-electrónico\]?subject=\[asunto\]&body=\[mensaje\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="09c8d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="09c8d-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="09c8d-163">Enviar un SMS (requiere la aplicación Skype)</span><span class="sxs-lookup"><span data-stu-id="09c8d-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="09c8d-164">sms:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="09c8d-165">Ejemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="09c8d-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="09c8d-166">Marcar un número de teléfono (requiere la aplicación Skype)</span><span class="sxs-lookup"><span data-stu-id="09c8d-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="09c8d-167">tel:\[número-teléfono\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="09c8d-168">Ejemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="09c8d-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="09c8d-169">Descargar una aplicación de Play Store</span><span class="sxs-lookup"><span data-stu-id="09c8d-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="09c8d-170">ms-windows-store:PDP?PFN=\[id. del paquete de la aplicación\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="09c8d-171">Ejemplo:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="09c8d-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="09c8d-172">Iniciar una búsqueda en Mapas de Bing</span><span class="sxs-lookup"><span data-stu-id="09c8d-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="09c8d-173">bingmaps:?q=\[consulta de búsqueda\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="09c8d-174">Ejemplo:bingmaps:?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="09c8d-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="09c8d-175">Utilice un esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="09c8d-175">Use a custom scheme</span></span>
  * <span data-ttu-id="09c8d-176">\[esquema personalizado\]://\[parámetros del esquema personalizado\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="09c8d-177">Ejemplo:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="09c8d-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="09c8d-178">Utilizar datos de paquete (se necesita una aplicación de la tienda para leer la extensión)</span><span class="sxs-lookup"><span data-stu-id="09c8d-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="09c8d-179">\[carpeta\]\[datos\].\[extensión\]</span><span class="sxs-lookup"><span data-stu-id="09c8d-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="09c8d-180">Ejemplo:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="09c8d-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="09c8d-181">Crear una dirección URL de seguimiento:</span><span class="sxs-lookup"><span data-stu-id="09c8d-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="09c8d-182">Consulte la sección "Configuración" de <UI Documentation> para obtener instrucciones sobre la creación de una dirección URL de seguimiento que permita a los usuarios descargar una de las otras aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="09c8d-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="09c8d-183">Definir los textos del anuncio</span><span class="sxs-lookup"><span data-stu-id="09c8d-183">Define the texts of your announcement</span></span>
<span data-ttu-id="09c8d-184">Rellene el título, el contenido y los textos del anuncio.</span><span class="sxs-lookup"><span data-stu-id="09c8d-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="09c8d-185">Puede dirigirse a una audiencia de una campaña futura basándose en los comentarios de la cobertura sobre cómo respondieron los usuarios a esta campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="09c8d-186">La orientación a la audiencia puede basarse en los comentarios de si solo se ha insertado esta campaña, respondido, ejecutada o terminado.</span><span class="sxs-lookup"><span data-stu-id="09c8d-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="09c8d-187">Consulte también</span><span class="sxs-lookup"><span data-stu-id="09c8d-187">See also</span></span>
* <span data-ttu-id="09c8d-188">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="09c8d-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="09c8d-189">Contenido de sondeos</span><span class="sxs-lookup"><span data-stu-id="09c8d-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="09c8d-191">Rellene el título, la descripción y los textos de los botones del anuncio.</span><span class="sxs-lookup"><span data-stu-id="09c8d-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="09c8d-192">A continuación, agregue preguntas y opciones para las respuestas a sus preguntas.</span><span class="sxs-lookup"><span data-stu-id="09c8d-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="09c8d-193">Puede dirigirse a una audiencia de una campaña futura basándose en los comentarios de la cobertura sobre cómo respondieron los usuarios a esta campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="09c8d-194">La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="09c8d-195">La orientación de la audiencia también puede basarse en los comentarios de respuesta de sondeos, donde la pregunta y respuesta se utilizan como criterios.</span><span class="sxs-lookup"><span data-stu-id="09c8d-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="09c8d-196">Consulte también</span><span class="sxs-lookup"><span data-stu-id="09c8d-196">See also</span></span>
* <span data-ttu-id="09c8d-197">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="09c8d-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="09c8d-198">Contenido de las inserciones de datos</span><span class="sxs-lookup"><span data-stu-id="09c8d-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="09c8d-200">Elija el tipo de datos:</span><span class="sxs-lookup"><span data-stu-id="09c8d-200">Choose the type of your data:</span></span>
* <span data-ttu-id="09c8d-201">Texto</span><span class="sxs-lookup"><span data-stu-id="09c8d-201">Text</span></span>
* <span data-ttu-id="09c8d-202">Datos binarios</span><span class="sxs-lookup"><span data-stu-id="09c8d-202">Binary data</span></span>
* <span data-ttu-id="09c8d-203">Datos de Base64</span><span class="sxs-lookup"><span data-stu-id="09c8d-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="09c8d-204">Defina el contenido de los datos</span><span class="sxs-lookup"><span data-stu-id="09c8d-204">Define the content of your data</span></span>
* <span data-ttu-id="09c8d-205">Si ha seleccionado insertar datos de texto, copie y pegue el texto en el cuadro "content".</span><span class="sxs-lookup"><span data-stu-id="09c8d-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="09c8d-206">Si ha seleccionado insertar datos binarios o base64, use el botón "cargar el archivo" para cargar el archivo.</span><span class="sxs-lookup"><span data-stu-id="09c8d-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="09c8d-207">Puede dirigirse a una audiencia de una campaña futura basándose en los comentarios de la cobertura sobre cómo respondieron los usuarios a esta campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="09c8d-208">La orientación a la audiencia puede basarse en si solo se ha insertado, respondido, ejecutado o terminado esta campaña.</span><span class="sxs-lookup"><span data-stu-id="09c8d-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="09c8d-209">Consulte también</span><span class="sxs-lookup"><span data-stu-id="09c8d-209">See also</span></span>
* <span data-ttu-id="09c8d-210">[Documentación de la interfaz de usuario - Cobertura - Nuevo criterio de inserción][Link 28]</span><span class="sxs-lookup"><span data-stu-id="09c8d-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="09c8d-211">Contenido de los mosaicos (solo en Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="09c8d-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="09c8d-213">Defina el contenido de su mosaico</span><span class="sxs-lookup"><span data-stu-id="09c8d-213">Define the content of your tile</span></span>
<span data-ttu-id="09c8d-214">La carga de mosaicos es el texto que se mostrará en el mosaico de la aplicación en los dispositivos Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="09c8d-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="09c8d-215">La inserción de un mosaico es la versión del servicio de notificaciones de inserción de Microsoft (MPNS) de una inserción nativa para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="09c8d-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="09c8d-216">El tipo de inserción de mosaico es el único tipo de inserción que no tiene una respuesta y, por tanto, la audiencia de las campañas futuras no se puede integrar en los resultados de una campaña de inserción de mosaico.</span><span class="sxs-lookup"><span data-stu-id="09c8d-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="09c8d-217">Consulte también</span><span class="sxs-lookup"><span data-stu-id="09c8d-217">See also</span></span>
* <span data-ttu-id="09c8d-218">[Documentación de la API - API de cobertura - Inserción nativa][Link 4]</span><span class="sxs-lookup"><span data-stu-id="09c8d-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

