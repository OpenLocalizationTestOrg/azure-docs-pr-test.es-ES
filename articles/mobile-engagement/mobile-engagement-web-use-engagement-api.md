---
title: API del SDK de Mobile Engagement Web aaaAzure | Documentos de Microsoft
description: "Hola actualizaciones más recientes y procedimientos para hello Web SDK de Azure Mobile Engagement"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="61fd1-103">Usar hello Azure Mobile Engagement API en una aplicación web</span><span class="sxs-lookup"><span data-stu-id="61fd1-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="61fd1-104">Este documento es un documento de toohello de suma que le indica cómo demasiado[integrar Mobile Engagement en una aplicación web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="61fd1-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="61fd1-105">Proporciona información detallada acerca de cómo toouse Hola API de Azure Mobile Engagement tooreport las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="61fd1-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="61fd1-106">Hello API de Mobile Engagement proporciona hello `engagement.agent` objeto.</span><span class="sxs-lookup"><span data-stu-id="61fd1-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="61fd1-107">Hola predeterminado SDK de Azure Mobile Engagement Web alias es `engagement`.</span><span class="sxs-lookup"><span data-stu-id="61fd1-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="61fd1-108">Puede volver a definir este alias de configuración de SDK de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="61fd1-109">Conceptos de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="61fd1-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="61fd1-110">Hello partes siguientes refinar comunes [conceptos de Mobile Engagement](mobile-engagement-concepts.md) de plataforma web de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="61fd1-111">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="61fd1-111">`Session` and `Activity`</span></span>
<span data-ttu-id="61fd1-112">Si el usuario de Hola permanece inactiva durante más de unos pocos segundos entre dos actividades, hello secuencia del usuario de actividades se divide en dos sesiones diferentes.</span><span class="sxs-lookup"><span data-stu-id="61fd1-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="61fd1-113">Estos pocos segundos se denominan Hola tiempo de espera de sesión.</span><span class="sxs-lookup"><span data-stu-id="61fd1-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="61fd1-114">Si la aplicación web no declara final Hola de actividades de usuario por sí mismo (por Hola que realiza la llamada `engagement.agent.endActivity` función), servidor de Mobile Engagement Hola expira automáticamente Hola sesión de usuario en los tres minutos después de cerrar la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="61fd1-115">Esto se denomina tiempo de espera de sesión de servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="61fd1-116">No se crean informes automatizados de excepciones de JavaScript no detectadas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="61fd1-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="61fd1-117">Sin embargo, puede crear informes de bloqueos manualmente mediante el uso de hello `sendCrash` función (consulte la sección de hello en reporting bloqueos).</span><span class="sxs-lookup"><span data-stu-id="61fd1-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="61fd1-118">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="61fd1-118">Reporting activities</span></span>
<span data-ttu-id="61fd1-119">Creación de informes sobre la actividad de usuario incluye cuando un usuario inicia una nueva actividad, y al usuario de hello finaliza la actividad actual de hello.</span><span class="sxs-lookup"><span data-stu-id="61fd1-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="61fd1-120">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="61fd1-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="61fd1-121">Necesita toocall `startActivity()` cambia cada actividad de usuario de tiempo.</span><span class="sxs-lookup"><span data-stu-id="61fd1-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="61fd1-122">Hola primera llamada toothis función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="61fd1-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="61fd1-123">Usuario finaliza la actividad actual de hello</span><span class="sxs-lookup"><span data-stu-id="61fd1-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="61fd1-124">Necesita toocall `endActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad.</span><span class="sxs-lookup"><span data-stu-id="61fd1-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="61fd1-125">Este modo, se informa hello Web SDK de Mobile Engagement que usuario Hola está inactivo y que la sesión de usuario de hello necesita toobe cerrado después de que expire el tiempo de espera de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="61fd1-126">Si se llama a `startActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente se reanuda la sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="61fd1-127">Porque no hay ninguna llamada confiable para cuando se cierra la ventana del navegador de hello, suele ser final de hello toocatch difíciles o imposibles de actividades de usuario dentro de un entorno web.</span><span class="sxs-lookup"><span data-stu-id="61fd1-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="61fd1-128">¿Por qué que se Hola Mobile Engagement server expira automáticamente sesión de usuario de hello en los tres minutos después de cerrar la página de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="61fd1-129">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="61fd1-129">Reporting events</span></span>
<span data-ttu-id="61fd1-130">La creación de informes sobre eventos incluye los eventos de sesión y los eventos independientes.</span><span class="sxs-lookup"><span data-stu-id="61fd1-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="61fd1-131">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="61fd1-131">Session events</span></span>
<span data-ttu-id="61fd1-132">Eventos de sesión suelen ser las acciones de hello tooreport usado realizadas por un usuario durante la sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="61fd1-133">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="61fd1-134">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="61fd1-135">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="61fd1-135">Standalone events</span></span>
<span data-ttu-id="61fd1-136">A diferencia de los eventos de sesión, pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="61fd1-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="61fd1-137">Por ello, utilice ``engagement.agent.sendEvent`` en lugar de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="61fd1-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="61fd1-138">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="61fd1-138">Reporting errors</span></span>
<span data-ttu-id="61fd1-139">La creación de informes sobre errores incluye los errores de sesión y los errores independientes.</span><span class="sxs-lookup"><span data-stu-id="61fd1-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="61fd1-140">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="61fd1-140">Session errors</span></span>
<span data-ttu-id="61fd1-141">Errores de sesión suelen ser errores de hello tooreport usado que tenga un impacto en el usuario de Hola durante la sesión de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="61fd1-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="61fd1-142">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="61fd1-143">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="61fd1-144">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="61fd1-144">Standalone errors</span></span>
<span data-ttu-id="61fd1-145">A diferencia de los errores de la sesión, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="61fd1-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="61fd1-146">Por ello, utilice `engagement.agent.sendError` en lugar de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="61fd1-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="61fd1-147">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="61fd1-147">Reporting jobs</span></span>
<span data-ttu-id="61fd1-148">La creación de informes sobre trabajos incluye la notificación de errores y eventos que se producen durante un trabajo y la notificación de bloqueos.</span><span class="sxs-lookup"><span data-stu-id="61fd1-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="61fd1-149">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-149">**Example:**</span></span>

<span data-ttu-id="61fd1-150">Si desea toomonitor una solicitud AJAX, utilizaría Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="61fd1-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="61fd1-151">Informes de errores durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="61fd1-151">Reporting errors during a job</span></span>
<span data-ttu-id="61fd1-152">Errores pueden ser tooa relacionado ejecutando el trabajo en lugar de toohello sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="61fd1-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="61fd1-153">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-153">**Example:**</span></span>

<span data-ttu-id="61fd1-154">Si desea que un error si una solicitud AJAX tooreport produce un error:</span><span class="sxs-lookup"><span data-stu-id="61fd1-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="61fd1-155">Informes de eventos durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="61fd1-155">Reporting events during a job</span></span>
<span data-ttu-id="61fd1-156">Los eventos pueden ser tooa relacionado ejecutando trabajo en lugar de la sesión del usuario actual toohello, gracias toohello `engagement.agent.sendJobEvent` función.</span><span class="sxs-lookup"><span data-stu-id="61fd1-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="61fd1-157">Esta función se comporta exactamente como `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="61fd1-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="61fd1-158">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="61fd1-158">Reporting crashes</span></span>
<span data-ttu-id="61fd1-159">Hola de uso `sendCrash` tooreport de función se bloquea de forma manual.</span><span class="sxs-lookup"><span data-stu-id="61fd1-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="61fd1-160">Hola `crashid` argumento es una cadena que identifica el tipo de saludo de bloqueo.</span><span class="sxs-lookup"><span data-stu-id="61fd1-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="61fd1-161">Hola `crash` argumento es normalmente el seguimiento de la pila de Hola de fallo de hello como una cadena.</span><span class="sxs-lookup"><span data-stu-id="61fd1-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="61fd1-162">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="61fd1-162">Extra parameters</span></span>
<span data-ttu-id="61fd1-163">Puede asociar el evento tooan de datos arbitrarios, error, actividad o el trabajo.</span><span class="sxs-lookup"><span data-stu-id="61fd1-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="61fd1-164">Hola datos pueden ser cualquier objeto JSON (pero no una matriz o tipo primitivo).</span><span class="sxs-lookup"><span data-stu-id="61fd1-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="61fd1-165">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="61fd1-166">límites</span><span class="sxs-lookup"><span data-stu-id="61fd1-166">Limits</span></span>
<span data-ttu-id="61fd1-167">Límites que se apliquen tooextra parámetros están en áreas de Hola de expresiones regulares para las claves, tipos de valor y tamaño.</span><span class="sxs-lookup"><span data-stu-id="61fd1-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="61fd1-168">simétricas</span><span class="sxs-lookup"><span data-stu-id="61fd1-168">Keys</span></span>
<span data-ttu-id="61fd1-169">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="61fd1-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="61fd1-170">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="61fd1-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="61fd1-171">Valores</span><span class="sxs-lookup"><span data-stu-id="61fd1-171">Values</span></span>
<span data-ttu-id="61fd1-172">Los valores son toostring limitado, el número y los tipos booleanos.</span><span class="sxs-lookup"><span data-stu-id="61fd1-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="61fd1-173">Tamaño</span><span class="sxs-lookup"><span data-stu-id="61fd1-173">Size</span></span>
<span data-ttu-id="61fd1-174">Extras son too1 limitado, 024 caracteres por llamada (después de hello Web SDK de Mobile Engagement lo codifica en JSON).</span><span class="sxs-lookup"><span data-stu-id="61fd1-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="61fd1-175">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="61fd1-175">Reporting application information</span></span>
<span data-ttu-id="61fd1-176">Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de la aplicación) mediante el uso de hello `sendAppInfo()` función.</span><span class="sxs-lookup"><span data-stu-id="61fd1-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="61fd1-177">Tenga en cuenta que esta información se puede enviar de forma incremental.</span><span class="sxs-lookup"><span data-stu-id="61fd1-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="61fd1-178">Solo Hola valor más reciente de una clave específica se mantendrán para un dispositivo específico.</span><span class="sxs-lookup"><span data-stu-id="61fd1-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="61fd1-179">Como eventos adicionales, puede usar cualquier información de aplicación de tooabstract de objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="61fd1-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="61fd1-180">Tenga en cuenta que las matrices o subobjetos se tratarán como cadenas sin formato (con la serialización de JSON).</span><span class="sxs-lookup"><span data-stu-id="61fd1-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="61fd1-181">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="61fd1-181">**Example:**</span></span>

<span data-ttu-id="61fd1-182">Este es un ejemplo de código para el género del usuario que envía hello y fecha de nacimiento:</span><span class="sxs-lookup"><span data-stu-id="61fd1-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="61fd1-183">límites</span><span class="sxs-lookup"><span data-stu-id="61fd1-183">Limits</span></span>
<span data-ttu-id="61fd1-184">Son límites que se apliquen tooapplication información en las áreas de Hola de expresiones regulares para las claves y el tamaño.</span><span class="sxs-lookup"><span data-stu-id="61fd1-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="61fd1-185">simétricas</span><span class="sxs-lookup"><span data-stu-id="61fd1-185">Keys</span></span>
<span data-ttu-id="61fd1-186">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="61fd1-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="61fd1-187">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="61fd1-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="61fd1-188">Tamaño</span><span class="sxs-lookup"><span data-stu-id="61fd1-188">Size</span></span>
<span data-ttu-id="61fd1-189">Información de la aplicación es too1 limitado, 024 caracteres por llamada (después de hello Web SDK de Mobile Engagement lo codifica en JSON).</span><span class="sxs-lookup"><span data-stu-id="61fd1-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="61fd1-190">En el anterior ejemplo de Hola, hello JSON enviadas toohello server es 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="61fd1-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
