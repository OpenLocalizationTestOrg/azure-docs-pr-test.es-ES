---
title: "aaaHow tooUse Hola API de interacción de Windows Phone Silverlight"
description: "¿Cómo tooUse Hola API de interacción de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="8a455-103">¿Cómo tooUse Hola API de interacción de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="8a455-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="8a455-104">Este documento es un complemento toohello [cómo toointegrate Mobile Engagement en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="8a455-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="8a455-105">Proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8a455-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="8a455-106">Si sólo desea interacción tooreport sesiones, actividades, bloqueos e información técnica de la aplicación, hello más sencillo cierto es toomake todos los su `PhoneApplicationPage` subclases heredan de hello `EngagementPage` clase.</span><span class="sxs-lookup"><span data-stu-id="8a455-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="8a455-107">Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementPage` clases, deberá toouse Hola API de contratación.</span><span class="sxs-lookup"><span data-stu-id="8a455-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="8a455-108">Hello interacción API proporcionada por hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="8a455-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="8a455-109">Puede tener acceso a los métodos de toothose a través de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="8a455-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="8a455-110">Incluso si no se ha inicializado el módulo de agente de hello, cada API toohello de llamada se pospone y se ejecutará de nuevo cuando el agente Hola está disponible.</span><span class="sxs-lookup"><span data-stu-id="8a455-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="8a455-111">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="8a455-111">Engagement concepts</span></span>
<span data-ttu-id="8a455-112">Hola siguientes piezas refinar Hola Mobile Engagement conceptos para la plataforma de Windows Phone Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="8a455-113">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="8a455-113">`Session` and `Activity`</span></span>
<span data-ttu-id="8a455-114">Un *actividad* suele estar asociado a una página de aplicación hello, que es hello toosay *actividad* se inicia cuando la página de Hola se muestra y se detiene cuando se cierra la página de Hola: se trata de los casos de hello cuando hello Engagement SDK se integra mediante hello `EngagementPage` clase.</span><span class="sxs-lookup"><span data-stu-id="8a455-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="8a455-115">Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="8a455-116">Esto permite toosplit una página determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta página (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta página).</span><span class="sxs-lookup"><span data-stu-id="8a455-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="8a455-117">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="8a455-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="8a455-118">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="8a455-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-119">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-120">Necesita toocall `StartActivity()` cambia cada actividad de usuario de hello de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8a455-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="8a455-121">Hola primera llamada toothis función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="8a455-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8a455-122">Hola SDK automáticamente llame al método EndActivity de hello cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8a455-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="8a455-123">Por lo tanto, se recomienda encarecidamente método de toocall hello StartActivity cada vez que ha finalizado la actividad de hello del cambio de usuario de Hola y llamada tooNEVER Hola método EndActivity, desde una llamada a este método obliga a toobe de la sesión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="8a455-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="8a455-125">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="8a455-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-126">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="8a455-127">Necesita toocall `EndActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad.</span><span class="sxs-lookup"><span data-stu-id="8a455-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="8a455-128">Este modo, informa Hola expirará Engagement SDK que usuario Hola está inactivo y que la sesión de usuario de hello necesario toobe una vez cerrado Hola tiempo de espera de sesión (si se llama a `StartActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente continúa sesión hello).</span><span class="sxs-lookup"><span data-stu-id="8a455-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="8a455-130">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="8a455-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="8a455-131">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-132">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-133">Puede utilizar tareas de hello trabajo tootrack ciertos durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8a455-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-134">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="8a455-135">Finalizar un trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-136">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="8a455-137">Tan pronto como se ha terminado una tarea que realiza el seguimiento de un trabajo, se debería llamar a hello EndJob método para este trabajo, proporcionando el nombre del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="8a455-139">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="8a455-139">Reporting Events</span></span>
<span data-ttu-id="8a455-140">Hay tres tipos de eventos:</span><span class="sxs-lookup"><span data-stu-id="8a455-140">There is three types of events :</span></span>

* <span data-ttu-id="8a455-141">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="8a455-141">Standalone events</span></span>
* <span data-ttu-id="8a455-142">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="8a455-142">Session events</span></span>
* <span data-ttu-id="8a455-143">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="8a455-144">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="8a455-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-145">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-146">Pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="8a455-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-147">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="8a455-148">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="8a455-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-149">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-150">Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="8a455-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-151">Example</span></span>
<span data-ttu-id="8a455-152">**Sin datos:**</span><span class="sxs-lookup"><span data-stu-id="8a455-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="8a455-153">**Con datos:**</span><span class="sxs-lookup"><span data-stu-id="8a455-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="8a455-154">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-155">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-156">Eventos de trabajo son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante un trabajo.</span><span class="sxs-lookup"><span data-stu-id="8a455-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-157">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="8a455-158">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="8a455-158">Reporting Errors</span></span>
<span data-ttu-id="8a455-159">Hay tres tipos de errores:</span><span class="sxs-lookup"><span data-stu-id="8a455-159">There is three types of errors :</span></span>

* <span data-ttu-id="8a455-160">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="8a455-160">Standalone errors</span></span>
* <span data-ttu-id="8a455-161">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="8a455-161">Session errors</span></span>
* <span data-ttu-id="8a455-162">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="8a455-163">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="8a455-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-164">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-165">Errores de toosession contrarias, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="8a455-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-166">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="8a455-167">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="8a455-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-168">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-169">Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="8a455-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="8a455-171">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="8a455-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-172">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="8a455-173">Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="8a455-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="8a455-175">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="8a455-175">Reporting Crashes</span></span>
<span data-ttu-id="8a455-176">agente de Hello proporciona dos toodeal métodos con los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="8a455-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="8a455-177">Enviar una excepción</span><span class="sxs-lookup"><span data-stu-id="8a455-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-178">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="8a455-179">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-179">Example</span></span>
<span data-ttu-id="8a455-180">Puede enviar una excepción en cualquier momento al llamar a:</span><span class="sxs-lookup"><span data-stu-id="8a455-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="8a455-181">También puede utilizar una sesión de interacción de parámetro opcional tooterminate hello en hello mismo tiempo que el envío de bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="8a455-182">por lo tanto, llame la toodo:</span><span class="sxs-lookup"><span data-stu-id="8a455-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="8a455-183">Si lo hace, trabajos y sesión Hola se cerrará inmediatamente después de enviar el bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a455-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="8a455-184">Enviar una excepción no controlada</span><span class="sxs-lookup"><span data-stu-id="8a455-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="8a455-185">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="8a455-186">Interacción también proporciona un excepciones de toosend no controlada por el método.</span><span class="sxs-lookup"><span data-stu-id="8a455-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="8a455-187">Esto es especialmente útil cuando se usa dentro del controlador de eventos de hello silverlight UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="8a455-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="8a455-188">Este método le **siempre** finalizar sesión de interacción de Hola y trabajos tras la llamada.</span><span class="sxs-lookup"><span data-stu-id="8a455-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="8a455-189">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-189">Example</span></span>
<span data-ttu-id="8a455-190">Puede usar tooimplement su propio controlador UnhandledException (especialmente si ha deshabilitado la característica de interacción de informes de bloqueo automática hello).</span><span class="sxs-lookup"><span data-stu-id="8a455-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="8a455-191">Por ejemplo, en hello `Application_UnhandledException` método de hello `App.xaml.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="8a455-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="8a455-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="8a455-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="8a455-193">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="8a455-194">Al usuario Hola se desplaza hacia delante, fuera de una aplicación, después de que se genera el evento de hello desactivado, sistema operativo de hello tratará de aplicación de hello tooput en estado inactivo.</span><span class="sxs-lookup"><span data-stu-id="8a455-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="8a455-195">A continuación, la aplicación hello es extinción.</span><span class="sxs-lookup"><span data-stu-id="8a455-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="8a455-196">En este proceso se termina una aplicación, pero se conservan algunos datos sobre el estado de Hola de hello páginas de aplicación y Hola individuales dentro de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8a455-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="8a455-197">Tiene tooinsert `EngagementAgent.Instance.OnActivated(e)` en hello `Application_Activated` método de Hola de tooreset de archivo hello App.xaml.cs interacción agente cuando aplicación hello se ha desechado.</span><span class="sxs-lookup"><span data-stu-id="8a455-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="8a455-198">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="8a455-199">Identificador de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8a455-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="8a455-200">Puede obtener Id. de dispositivo de interacción de hello mediante una llamada a este método.</span><span class="sxs-lookup"><span data-stu-id="8a455-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="8a455-201">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="8a455-201">Extras parameters</span></span>
<span data-ttu-id="8a455-202">Evento tooan adjunto, un error, una actividad o un trabajo, pueden ser datos arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="8a455-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="8a455-203">Estos datos se pueden estructurar mediante un diccionario.</span><span class="sxs-lookup"><span data-stu-id="8a455-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="8a455-204">Las claves y los valores pueden ser de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="8a455-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="8a455-205">Por lo que si desea tooinsert su propio tipo de extras tener tooadd un contrato de datos para este tipo, se serializan datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="8a455-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="8a455-206">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-206">Example</span></span>
<span data-ttu-id="8a455-207">Creamos una nueva clase "Person".</span><span class="sxs-lookup"><span data-stu-id="8a455-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="8a455-208">A continuación, agregaremos un `Person` tooan de instancia adicional.</span><span class="sxs-lookup"><span data-stu-id="8a455-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="8a455-209">Si coloca otros tipos de objetos, asegúrese de que su método ToString() es tooreturn implementada una cadena legible.</span><span class="sxs-lookup"><span data-stu-id="8a455-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="8a455-210">límites</span><span class="sxs-lookup"><span data-stu-id="8a455-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8a455-211">simétricas</span><span class="sxs-lookup"><span data-stu-id="8a455-211">Keys</span></span>
<span data-ttu-id="8a455-212">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="8a455-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8a455-213">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="8a455-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8a455-214">Tamaño</span><span class="sxs-lookup"><span data-stu-id="8a455-214">Size</span></span>
<span data-ttu-id="8a455-215">Extras se limitan demasiado**1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="8a455-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="8a455-216">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="8a455-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="8a455-217">Referencia</span><span class="sxs-lookup"><span data-stu-id="8a455-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="8a455-218">Puede crear informes manualmente información (o cualquier otra información específica de aplicación) con hello SendAppInfo() función de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="8a455-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="8a455-219">Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="8a455-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="8a455-220">Como eventos adicionales, utilice un diccionario\<(objeto), objeto\> tooattach informaciones.</span><span class="sxs-lookup"><span data-stu-id="8a455-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="8a455-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8a455-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="8a455-222">Límites</span><span class="sxs-lookup"><span data-stu-id="8a455-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="8a455-223">simétricas</span><span class="sxs-lookup"><span data-stu-id="8a455-223">Keys</span></span>
<span data-ttu-id="8a455-224">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="8a455-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="8a455-225">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="8a455-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="8a455-226">Tamaño</span><span class="sxs-lookup"><span data-stu-id="8a455-226">Size</span></span>
<span data-ttu-id="8a455-227">Información de la aplicación se limitan demasiado**1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="8a455-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="8a455-228">Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="8a455-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="8a455-229">Registro</span><span class="sxs-lookup"><span data-stu-id="8a455-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="8a455-230">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="8a455-230">Enable Logging</span></span>
<span data-ttu-id="8a455-231">Hola SDK puede ser tooproduce configurado los registros de pruebas en la consola de hello IDE.</span><span class="sxs-lookup"><span data-stu-id="8a455-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="8a455-232">Estos registros no están activados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8a455-232">These logs are not activated by default.</span></span> <span data-ttu-id="8a455-233">toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8a455-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
