---
title: "aaaHow tooUse Hola API de interacción en universales de Windows"
description: "¿Cómo tooUse Hola API de interacción en universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="bb84e-103">¿Cómo tooUse Hola API de interacción en universales de Windows</span><span class="sxs-lookup"><span data-stu-id="bb84e-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="bb84e-104">Este documento es un complemento toohello [cómo tooIntegrate interacción en universales de Windows](mobile-engagement-windows-store-integrate-engagement.md): proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bb84e-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="bb84e-105">Tenga en cuenta que si sólo desea tooreport de interacción de su aplicación sesiones, actividades, se bloquea y obtener información técnica, a continuación, hello manera más sencilla de toomake todos los `Page` subclases heredan de hello `EngagementPage` clase.</span><span class="sxs-lookup"><span data-stu-id="bb84e-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="bb84e-106">Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementPage` clases, deberá toouse Hola API de contratación.</span><span class="sxs-lookup"><span data-stu-id="bb84e-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="bb84e-107">Hello interacción API proporcionada por hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="bb84e-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="bb84e-108">Puede tener acceso a los métodos de toothose a través de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="bb84e-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="bb84e-109">Incluso si no se ha inicializado el módulo de agente de hello, cada API toohello de llamada se pospone y se ejecutará de nuevo cuando el agente Hola está disponible.</span><span class="sxs-lookup"><span data-stu-id="bb84e-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="bb84e-110">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="bb84e-110">Engagement concepts</span></span>
<span data-ttu-id="bb84e-111">Hello partes siguientes refinar Hola comunes [Mobile Engagement conceptos](mobile-engagement-concepts.md) para la plataforma Universal de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="bb84e-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="bb84e-112">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="bb84e-112">`Session` and `Activity`</span></span>
<span data-ttu-id="bb84e-113">Un *actividad* suele estar asociado a una página de aplicación hello, que es hello toosay *actividad* se inicia cuando la página de Hola se muestra y se detiene cuando se cierra la página de Hola: se trata de los casos de hello cuando hello Engagement SDK se integra mediante hello `EngagementPage` clase.</span><span class="sxs-lookup"><span data-stu-id="bb84e-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="bb84e-114">Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb84e-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="bb84e-115">Esto le permite toosplit sub de una página determinada en varios elementos tooget más detalles acerca del uso de Hola de esta página (por ejemplo tooknow con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta página).</span><span class="sxs-lookup"><span data-stu-id="bb84e-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="bb84e-116">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="bb84e-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="bb84e-117">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="bb84e-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-118">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-119">Necesita toocall `StartActivity()` cambia cada actividad de usuario de hello de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bb84e-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="bb84e-120">Hola primera llamada toothis función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="bb84e-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bb84e-121">Hola SDK llama automáticamente a método de hello EndActivity cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="bb84e-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="bb84e-122">Por lo tanto, se recomienda encarecidamente método de toocall hello StartActivity cada vez que Hola actividad de usuario de hello los cambios, y el final de la llamada tooNEVER Hola método EndActivity, desde una llamada a este método obliga a toobe de la sesión actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb84e-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="bb84e-123">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="bb84e-124">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="bb84e-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-125">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="bb84e-126">Esto finaliza la sesión de Hola y actividad hello.</span><span class="sxs-lookup"><span data-stu-id="bb84e-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="bb84e-127">No debe llamar a este método, a menos que realmente sepa lo que está haciendo.</span><span class="sxs-lookup"><span data-stu-id="bb84e-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-128">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="bb84e-129">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="bb84e-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="bb84e-130">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-131">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-132">Puede utilizar tareas de hello trabajo tootrack ciertos durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bb84e-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-133">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="bb84e-134">Finalizar un trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-135">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="bb84e-136">Tan pronto como se ha terminado una tarea que realiza el seguimiento de un trabajo, se debería llamar a hello EndJob método para este trabajo, proporcionando el nombre del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb84e-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-137">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="bb84e-138">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="bb84e-138">Reporting Events</span></span>
<span data-ttu-id="bb84e-139">Hay tres tipos de eventos:</span><span class="sxs-lookup"><span data-stu-id="bb84e-139">There is three types of events :</span></span>

* <span data-ttu-id="bb84e-140">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="bb84e-140">Standalone events</span></span>
* <span data-ttu-id="bb84e-141">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="bb84e-141">Session events</span></span>
* <span data-ttu-id="bb84e-142">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="bb84e-143">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="bb84e-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-144">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-145">Pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="bb84e-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-146">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="bb84e-147">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="bb84e-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-148">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-149">Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="bb84e-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-150">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-150">Example</span></span>
<span data-ttu-id="bb84e-151">**Sin datos:**</span><span class="sxs-lookup"><span data-stu-id="bb84e-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="bb84e-152">**Con datos:**</span><span class="sxs-lookup"><span data-stu-id="bb84e-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="bb84e-153">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-154">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-155">Eventos de trabajo son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante un trabajo.</span><span class="sxs-lookup"><span data-stu-id="bb84e-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-156">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="bb84e-157">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="bb84e-157">Reporting Errors</span></span>
<span data-ttu-id="bb84e-158">Existen tres tipos de errores:</span><span class="sxs-lookup"><span data-stu-id="bb84e-158">There are three types of errors :</span></span>

* <span data-ttu-id="bb84e-159">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="bb84e-159">Standalone errors</span></span>
* <span data-ttu-id="bb84e-160">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="bb84e-160">Session errors</span></span>
* <span data-ttu-id="bb84e-161">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="bb84e-162">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="bb84e-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-163">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-164">Errores de toosession contrarias, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="bb84e-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-165">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="bb84e-166">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="bb84e-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-167">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-168">Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="bb84e-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-169">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="bb84e-170">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="bb84e-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-171">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="bb84e-172">Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="bb84e-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-173">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="bb84e-174">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="bb84e-174">Reporting Crashes</span></span>
<span data-ttu-id="bb84e-175">agente de Hello proporciona dos toodeal métodos con los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="bb84e-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="bb84e-176">Enviar una excepción</span><span class="sxs-lookup"><span data-stu-id="bb84e-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-177">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="bb84e-178">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-178">Example</span></span>
<span data-ttu-id="bb84e-179">Puede enviar una excepción en cualquier momento al llamar a:</span><span class="sxs-lookup"><span data-stu-id="bb84e-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="bb84e-180">También puede utilizar una sesión de interacción de parámetro opcional tooterminate hello en hello mismo tiempo que el envío de bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb84e-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="bb84e-181">por lo tanto, llame la toodo:</span><span class="sxs-lookup"><span data-stu-id="bb84e-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="bb84e-182">Si lo hace, trabajos y sesión Hola se cerrará inmediatamente después de enviar el bloqueo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb84e-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="bb84e-183">Enviar una excepción no controlada</span><span class="sxs-lookup"><span data-stu-id="bb84e-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="bb84e-184">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="bb84e-185">Interacción también proporciona un excepciones de toosend no controlada por el método si tiene **deshabilitado** automático de contratación **bloqueo** reporting.</span><span class="sxs-lookup"><span data-stu-id="bb84e-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="bb84e-186">Esto es especialmente útil cuando se usa dentro del controlador de eventos de hello aplicación UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="bb84e-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="bb84e-187">Este método le **siempre** finalizar sesión de interacción de Hola y trabajos tras la llamada.</span><span class="sxs-lookup"><span data-stu-id="bb84e-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="bb84e-188">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-188">Example</span></span>
<span data-ttu-id="bb84e-189">Puede usar tooimplement su propio controlador UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="bb84e-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="bb84e-190">Por ejemplo, agregar hello `Current_UnhandledException` método de hello `App.xaml.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="bb84e-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="bb84e-191">En App.xaml.cs, en "Public App(){}", agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb84e-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="bb84e-192">Identificador de dispositivo</span><span class="sxs-lookup"><span data-stu-id="bb84e-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="bb84e-193">Puede obtener Id. de dispositivo de interacción de hello mediante una llamada a este método.</span><span class="sxs-lookup"><span data-stu-id="bb84e-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="bb84e-194">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="bb84e-194">Extras parameters</span></span>
<span data-ttu-id="bb84e-195">Evento tooan adjunto, un error, una actividad o un trabajo, pueden ser datos arbitrarios.</span><span class="sxs-lookup"><span data-stu-id="bb84e-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="bb84e-196">Estos datos se pueden estructurar mediante un diccionario.</span><span class="sxs-lookup"><span data-stu-id="bb84e-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="bb84e-197">Las claves y los valores pueden ser de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="bb84e-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="bb84e-198">Por lo que si desea tooinsert su propio tipo de extras tener tooadd un contrato de datos para este tipo, se serializan datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="bb84e-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="bb84e-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-199">Example</span></span>
<span data-ttu-id="bb84e-200">Creamos una nueva clase "Person".</span><span class="sxs-lookup"><span data-stu-id="bb84e-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="bb84e-201">A continuación, agregaremos un `Person` tooan de instancia adicional.</span><span class="sxs-lookup"><span data-stu-id="bb84e-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="bb84e-202">Si coloca otros tipos de objetos, asegúrese de que su método ToString() es tooreturn implementada una cadena legible.</span><span class="sxs-lookup"><span data-stu-id="bb84e-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="bb84e-203">límites</span><span class="sxs-lookup"><span data-stu-id="bb84e-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="bb84e-204">simétricas</span><span class="sxs-lookup"><span data-stu-id="bb84e-204">Keys</span></span>
<span data-ttu-id="bb84e-205">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="bb84e-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="bb84e-206">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="bb84e-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="bb84e-207">Tamaño</span><span class="sxs-lookup"><span data-stu-id="bb84e-207">Size</span></span>
<span data-ttu-id="bb84e-208">Extras se limitan demasiado**1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="bb84e-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="bb84e-209">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="bb84e-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="bb84e-210">Referencia</span><span class="sxs-lookup"><span data-stu-id="bb84e-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="bb84e-211">Puede crear informes manualmente información (o cualquier otra información específica de aplicación) con hello SendAppInfo() función de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="bb84e-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="bb84e-212">Tenga en cuenta que estos datos pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="bb84e-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="bb84e-213">Como eventos adicionales, utilice un diccionario\<(objeto), objeto\> tooattach datos.</span><span class="sxs-lookup"><span data-stu-id="bb84e-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="bb84e-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb84e-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="bb84e-215">Límites</span><span class="sxs-lookup"><span data-stu-id="bb84e-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="bb84e-216">simétricas</span><span class="sxs-lookup"><span data-stu-id="bb84e-216">Keys</span></span>
<span data-ttu-id="bb84e-217">Cada clave Hola objeto debe coincidir Hola siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="bb84e-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="bb84e-218">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="bb84e-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="bb84e-219">Tamaño</span><span class="sxs-lookup"><span data-stu-id="bb84e-219">Size</span></span>
<span data-ttu-id="bb84e-220">Información de la aplicación se limita demasiado**1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="bb84e-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="bb84e-221">Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="bb84e-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="bb84e-222">Registro</span><span class="sxs-lookup"><span data-stu-id="bb84e-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="bb84e-223">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="bb84e-223">Enable Logging</span></span>
<span data-ttu-id="bb84e-224">Hola SDK puede ser tooproduce configurado los registros de pruebas en la consola de hello IDE.</span><span class="sxs-lookup"><span data-stu-id="bb84e-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="bb84e-225">Estos registros no están activados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bb84e-225">These logs are not activated by default.</span></span> <span data-ttu-id="bb84e-226">toocustomize, propiedad de hello actualización `EngagementAgent.Instance.TestLogEnabled` tooone del valor de hello disponible de hello `EngagementTestLogLevel` enumeración, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb84e-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

