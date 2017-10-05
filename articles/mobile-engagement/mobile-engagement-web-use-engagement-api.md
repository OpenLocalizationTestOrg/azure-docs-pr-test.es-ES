---
title: API de SDK web de Azure Mobile Engagement | Microsoft Docs
description: "Actualizaciones y procedimientos más recientes para el SDK web para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="3acac-103">Uso de la API de Azure Mobile Engagement en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="3acac-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="3acac-104">Este documento es un complemento al documento que muestra [cómo integrar Mobile Engagement en una aplicación web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="3acac-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="3acac-105">En él se proporciona información detallada acerca de cómo usar la API de Azure Mobile Engagement para notificar las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3acac-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="3acac-106">El objeto `engagement.agent` proporciona la API de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3acac-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="3acac-107">El SDK web de Azure Mobile Engagement predeterminado es `engagement`.</span><span class="sxs-lookup"><span data-stu-id="3acac-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="3acac-108">Puede volver a definir este alias desde la configuración del SDK.</span><span class="sxs-lookup"><span data-stu-id="3acac-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="3acac-109">Conceptos de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3acac-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="3acac-110">En las siguientes secciones se detallan los [conceptos de Mobile Engagement](mobile-engagement-concepts.md) habituales para la plataforma web.</span><span class="sxs-lookup"><span data-stu-id="3acac-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3acac-111">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="3acac-111">`Session` and `Activity`</span></span>
<span data-ttu-id="3acac-112">Si el usuario permanece inactivo entre dos actividades durante más de unos segundos, la secuencia de actividades del usuario se divide en dos sesiones distintas.</span><span class="sxs-lookup"><span data-stu-id="3acac-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="3acac-113">Estos segundos se denominan tiempo de espera de la sesión.</span><span class="sxs-lookup"><span data-stu-id="3acac-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="3acac-114">Si la aplicación web no declara el final de las actividades de usuario por sí misma (mediante una llamada a la función `engagement.agent.endActivity` ), el servidor de Mobile Engagement hará que la sesión del usuario expire automáticamente en los tres minutos posteriores al cierre de la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3acac-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="3acac-115">Esto se denomina tiempo de espera del servidor.</span><span class="sxs-lookup"><span data-stu-id="3acac-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="3acac-116">No se crean informes automatizados de excepciones de JavaScript no detectadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="3acac-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="3acac-117">No obstante, puede notificar bloqueos manualmente mediante la función `sendCrash` (consulte la sección sobre informes de bloqueos).</span><span class="sxs-lookup"><span data-stu-id="3acac-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3acac-118">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="3acac-118">Reporting activities</span></span>
<span data-ttu-id="3acac-119">La creación de informes sobre la actividad del usuario incluye cuando un usuario inicia una nueva actividad y cuando el usuario finaliza la actividad actual.</span><span class="sxs-lookup"><span data-stu-id="3acac-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3acac-120">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="3acac-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="3acac-121">Debe llamar a `startActivity()` cada vez que cambie la actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="3acac-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="3acac-122">La primera llamada a esta función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3acac-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="3acac-123">El usuario finaliza la actividad actual</span><span class="sxs-lookup"><span data-stu-id="3acac-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="3acac-124">Cuando el usuario finaliza su última actividad, debe llamar a `endActivity()` al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="3acac-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="3acac-125">Esto informa al SDK web de Mobile Engagement que el usuario está inactivo y que la sesión de usuario debe cerrarse después de que expire el tiempo de espera de la sesión.</span><span class="sxs-lookup"><span data-stu-id="3acac-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="3acac-126">Si llama a `startActivity()` antes de que expire el tiempo de espera de la sesión, simplemente se reanudará la sesión.</span><span class="sxs-lookup"><span data-stu-id="3acac-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="3acac-127">Como no hay ninguna llamada confiable cuando se cierra la ventana del navegador, a menudo resulta difícil o imposible detectar el final de las actividades de usuario dentro de un entorno web.</span><span class="sxs-lookup"><span data-stu-id="3acac-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="3acac-128">Por esta razón, el servidor de Mobile Engagement hace que la sesión de usuario expire automáticamente en los tres minutos posteriores al cierre de la página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3acac-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="3acac-129">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="3acac-129">Reporting events</span></span>
<span data-ttu-id="3acac-130">La creación de informes sobre eventos incluye los eventos de sesión y los eventos independientes.</span><span class="sxs-lookup"><span data-stu-id="3acac-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="3acac-131">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="3acac-131">Session events</span></span>
<span data-ttu-id="3acac-132">Los eventos de sesión se suelen usar para notificar las acciones que realiza el usuario durante la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3acac-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="3acac-133">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3acac-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="3acac-134">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3acac-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="3acac-135">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="3acac-135">Standalone events</span></span>
<span data-ttu-id="3acac-136">A diferencia de los eventos de sesión, los eventos independientes pueden producirse fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3acac-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="3acac-137">Por ello, utilice ``engagement.agent.sendEvent`` en lugar de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="3acac-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="3acac-138">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="3acac-138">Reporting errors</span></span>
<span data-ttu-id="3acac-139">La creación de informes sobre errores incluye los errores de sesión y los errores independientes.</span><span class="sxs-lookup"><span data-stu-id="3acac-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="3acac-140">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="3acac-140">Session errors</span></span>
<span data-ttu-id="3acac-141">Los errores de sesión se usan normalmente para notificar los errores que tienen un impacto en el usuario durante la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3acac-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="3acac-142">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3acac-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="3acac-143">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3acac-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="3acac-144">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="3acac-144">Standalone errors</span></span>
<span data-ttu-id="3acac-145">A diferencia de los errores de sesión, los errores independientes pueden producirse fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3acac-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="3acac-146">Por ello, utilice `engagement.agent.sendError` en lugar de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="3acac-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="3acac-147">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="3acac-147">Reporting jobs</span></span>
<span data-ttu-id="3acac-148">La creación de informes sobre trabajos incluye la notificación de errores y eventos que se producen durante un trabajo y la notificación de bloqueos.</span><span class="sxs-lookup"><span data-stu-id="3acac-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="3acac-149">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3acac-149">**Example:**</span></span>

<span data-ttu-id="3acac-150">Si desea supervisar una solicitud AJAX, utilizaría lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="3acac-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="3acac-151">Informes de errores durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3acac-151">Reporting errors during a job</span></span>
<span data-ttu-id="3acac-152">Los errores pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="3acac-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="3acac-153">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3acac-153">**Example:**</span></span>

<span data-ttu-id="3acac-154">Si desea notificar que se ha producido un error en una solicitud de AJAX:</span><span class="sxs-lookup"><span data-stu-id="3acac-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="3acac-155">Informes de eventos durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3acac-155">Reporting events during a job</span></span>
<span data-ttu-id="3acac-156">Los eventos pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual gracias a la función `engagement.agent.sendJobEvent` .</span><span class="sxs-lookup"><span data-stu-id="3acac-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="3acac-157">Esta función se comporta exactamente como `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="3acac-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="3acac-158">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="3acac-158">Reporting crashes</span></span>
<span data-ttu-id="3acac-159">Utilice la función `sendCrash` para notificar bloqueos manualmente.</span><span class="sxs-lookup"><span data-stu-id="3acac-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="3acac-160">El argumento `crashid` es una cadena que identifica el tipo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="3acac-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="3acac-161">El argumento `crash` es normalmente el seguimiento de la pila del bloqueo en forma de cadena.</span><span class="sxs-lookup"><span data-stu-id="3acac-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="3acac-162">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="3acac-162">Extra parameters</span></span>
<span data-ttu-id="3acac-163">Puede adjuntar datos arbitrarios a un evento, error, actividad o trabajo.</span><span class="sxs-lookup"><span data-stu-id="3acac-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="3acac-164">Estos datos pueden ser cualquier objeto JSON (pero no de tipo primitivo ni de matriz).</span><span class="sxs-lookup"><span data-stu-id="3acac-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="3acac-165">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3acac-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="3acac-166">Límites</span><span class="sxs-lookup"><span data-stu-id="3acac-166">Limits</span></span>
<span data-ttu-id="3acac-167">Los límites que se aplican a los parámetros adicionales están en las áreas de expresiones regulares para claves, tipos de valor y tamaño.</span><span class="sxs-lookup"><span data-stu-id="3acac-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="3acac-168">simétricas</span><span class="sxs-lookup"><span data-stu-id="3acac-168">Keys</span></span>
<span data-ttu-id="3acac-169">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="3acac-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="3acac-170">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3acac-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="3acac-171">Valores</span><span class="sxs-lookup"><span data-stu-id="3acac-171">Values</span></span>
<span data-ttu-id="3acac-172">Los valores solo pueden ser de tipo booleano, de número y de cadena.</span><span class="sxs-lookup"><span data-stu-id="3acac-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="3acac-173">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3acac-173">Size</span></span>
<span data-ttu-id="3acac-174">Los extras están limitados a 1024 caracteres por llamada (después de que el SDK web de Mobile Engagement lo codifique en JSON).</span><span class="sxs-lookup"><span data-stu-id="3acac-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="3acac-175">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="3acac-175">Reporting application information</span></span>
<span data-ttu-id="3acac-176">Puede notificar manualmente la información de seguimiento (o cualquier otro tipo de información específica de la aplicación) mediante la función `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="3acac-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="3acac-177">Tenga en cuenta que esta información se puede enviar de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="3acac-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="3acac-178">Solo se conservará el último valor de una clave específica para un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="3acac-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="3acac-179">Al igual que los extras de evento, puede utilizar cualquier objeto JSON para resumir la información de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3acac-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="3acac-180">Tenga en cuenta que las matrices o subobjetos se tratarán como cadenas sin formato (con la serialización de JSON).</span><span class="sxs-lookup"><span data-stu-id="3acac-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="3acac-181">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3acac-181">**Example:**</span></span>

<span data-ttu-id="3acac-182">Este es un ejemplo de código para enviar el sexo del usuario y la fecha de nacimiento:</span><span class="sxs-lookup"><span data-stu-id="3acac-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="3acac-183">Límites</span><span class="sxs-lookup"><span data-stu-id="3acac-183">Limits</span></span>
<span data-ttu-id="3acac-184">Los límites que se aplican a la información de la aplicación están en las áreas de expresiones regulares para claves y tamaño.</span><span class="sxs-lookup"><span data-stu-id="3acac-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="3acac-185">simétricas</span><span class="sxs-lookup"><span data-stu-id="3acac-185">Keys</span></span>
<span data-ttu-id="3acac-186">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="3acac-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="3acac-187">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3acac-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3acac-188">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3acac-188">Size</span></span>
<span data-ttu-id="3acac-189">La información de la aplicación está limitada a 1024 caracteres por llamada (después de que el SDK web de Mobile Engagement lo codifique en JSON).</span><span class="sxs-lookup"><span data-stu-id="3acac-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="3acac-190">En el ejemplo anterior, el JSON que se envía al servidor tiene una longitud de 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="3acac-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
