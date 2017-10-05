---
title: "Cómo usar la API de Engagement en Windows Universal"
description: "Cómo usar la API de Engagement en Windows Universal"
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="14eff-103">Cómo usar la API de Engagement en Windows Universal</span><span class="sxs-lookup"><span data-stu-id="14eff-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="14eff-104">Este documento es un complemento al documento [Cómo integrar Engagement en Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): en él se proporciona información detallada acerca de cómo usar la API de Engagement para informar de las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14eff-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="14eff-105">Tenga en cuenta que si solo desea que Engagement informe sobre las sesiones, las actividades, los bloqueos y la información técnica de la aplicación, la manera más sencilla consiste en hacer que las subclases `Page` hereden de la clase `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="14eff-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="14eff-106">Si desea hacer más, por ejemplo, si necesita informar de eventos, errores y trabajos específicos de la aplicación, o si debe informar de las actividades de la aplicación de manera diferente de la que se implementa en las clases `EngagementPage`, deberá usar la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="14eff-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="14eff-107">La API de Engagement la proporciona la clase `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="14eff-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="14eff-108">Puede acceder a esos métodos a través de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="14eff-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="14eff-109">Incluso si no se ha inicializado el módulo de agente, las llamadas a la API se aplazan y se ejecutará de nuevo cuando el agente está disponible.</span><span class="sxs-lookup"><span data-stu-id="14eff-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="14eff-110">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="14eff-110">Engagement concepts</span></span>
<span data-ttu-id="14eff-111">En las siguientes secciones se detallan los [conceptos de Mobile Engagement](mobile-engagement-concepts.md) para la plataforma Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="14eff-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="14eff-112">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="14eff-112">`Session` and `Activity`</span></span>
<span data-ttu-id="14eff-113">Una *actividad* suele estar asociada con una página de la aplicación. Es decir, la *actividad* se inicia cuando la página se muestra y se detiene cuando se cierra la página. Este es el caso cuando la integración del SDK de Engagement se realiza mediante la clase `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="14eff-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="14eff-114">Sin embargo, las *actividades* también se pueden controlar manualmente mediante la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="14eff-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="14eff-115">Esto permite dividir una página determinada en varias subpartes para obtener más detalles sobre el uso de esta página (por ejemplo, la frecuencia y la duración con las que se usan los cuadros de diálogo en esta página).</span><span class="sxs-lookup"><span data-stu-id="14eff-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="14eff-116">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="14eff-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="14eff-117">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="14eff-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-118">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-119">Debe llamar a `StartActivity()` cada vez que cambie la actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="14eff-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="14eff-120">La primera llamada a esta función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="14eff-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14eff-121">El SDK llama automáticamente al método EndActivity cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="14eff-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="14eff-122">Por lo tanto, es MUY recomendable llamar al método StartActivity cada vez que cambie la actividad del usuario y NUNCA llamar al método EndActivity, ya que esto obliga la finalización de la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="14eff-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="14eff-123">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="14eff-124">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="14eff-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-125">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="14eff-126">Esto finaliza la actividad y la sesión.</span><span class="sxs-lookup"><span data-stu-id="14eff-126">This ends the activity and the session.</span></span> <span data-ttu-id="14eff-127">No debe llamar a este método, a menos que realmente sepa lo que está haciendo.</span><span class="sxs-lookup"><span data-stu-id="14eff-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-128">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="14eff-129">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="14eff-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="14eff-130">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-131">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-132">Puede usar el trabajo para hace un seguimiento de tareas determinadas durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="14eff-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-133">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="14eff-134">Finalizar un trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-135">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="14eff-136">Cuando haya finalizado una tarea de la que un trabajo realiza el seguimiento, se debe llamar al método EndJob para este trabajo al proporcionar su nombre.</span><span class="sxs-lookup"><span data-stu-id="14eff-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-137">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="14eff-138">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="14eff-138">Reporting Events</span></span>
<span data-ttu-id="14eff-139">Hay tres tipos de eventos:</span><span class="sxs-lookup"><span data-stu-id="14eff-139">There is three types of events :</span></span>

* <span data-ttu-id="14eff-140">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="14eff-140">Standalone events</span></span>
* <span data-ttu-id="14eff-141">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="14eff-141">Session events</span></span>
* <span data-ttu-id="14eff-142">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="14eff-143">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="14eff-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-144">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-145">Los eventos independientes se pueden producir fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="14eff-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-146">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="14eff-147">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="14eff-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-148">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-149">Los eventos de sesión se suelen usar para notificar las acciones que realiza el usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="14eff-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-150">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-150">Example</span></span>
<span data-ttu-id="14eff-151">**Sin datos:**</span><span class="sxs-lookup"><span data-stu-id="14eff-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="14eff-152">**Con datos:**</span><span class="sxs-lookup"><span data-stu-id="14eff-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="14eff-153">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-154">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-155">Los eventos de trabajo se suelen usar para notificar las acciones que realiza un usuario durante un trabajo.</span><span class="sxs-lookup"><span data-stu-id="14eff-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-156">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="14eff-157">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="14eff-157">Reporting Errors</span></span>
<span data-ttu-id="14eff-158">Existen tres tipos de errores:</span><span class="sxs-lookup"><span data-stu-id="14eff-158">There are three types of errors :</span></span>

* <span data-ttu-id="14eff-159">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="14eff-159">Standalone errors</span></span>
* <span data-ttu-id="14eff-160">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="14eff-160">Session errors</span></span>
* <span data-ttu-id="14eff-161">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="14eff-162">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="14eff-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-163">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-164">Al contrario de los errores de sesión, los errores independientes se pueden producir fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="14eff-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-165">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="14eff-166">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="14eff-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-167">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-168">Los errores de sesión suelen usarse para notificar los errores que afectan al usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="14eff-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-169">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="14eff-170">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="14eff-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-171">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="14eff-172">Los errores pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="14eff-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-173">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="14eff-174">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="14eff-174">Reporting Crashes</span></span>
<span data-ttu-id="14eff-175">El agente proporciona dos métodos para tratar los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="14eff-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="14eff-176">Enviar una excepción</span><span class="sxs-lookup"><span data-stu-id="14eff-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-177">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="14eff-178">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-178">Example</span></span>
<span data-ttu-id="14eff-179">Puede enviar una excepción en cualquier momento al llamar a:</span><span class="sxs-lookup"><span data-stu-id="14eff-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="14eff-180">También puede usar un parámetro opcional para finalizar la sesión de Engagement al mismo tiempo que se envía el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="14eff-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="14eff-181">Para ello, llame a:</span><span class="sxs-lookup"><span data-stu-id="14eff-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="14eff-182">Si lo hace, la sesión y los trabajos se cerrarán después de enviar el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="14eff-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="14eff-183">Enviar una excepción no controlada</span><span class="sxs-lookup"><span data-stu-id="14eff-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="14eff-184">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="14eff-185">Engagement también proporciona un método para enviar excepciones no controladas si ha **DESHABILITADO** los informes de **bloqueo** automáticos de Engagement.</span><span class="sxs-lookup"><span data-stu-id="14eff-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="14eff-186">Esto es especialmente útil cuando se usa dentro del controlador de eventos UnhandledException.</span><span class="sxs-lookup"><span data-stu-id="14eff-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="14eff-187">Este método **SIEMPRE** finalizará la sesión y los trabajos de Engagement después de su invocación.</span><span class="sxs-lookup"><span data-stu-id="14eff-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="14eff-188">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-188">Example</span></span>
<span data-ttu-id="14eff-189">Puede usarlo para implementar su propio controlador UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="14eff-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="14eff-190">Por ejemplo, agregue el método `Current_UnhandledException` del archivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="14eff-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="14eff-191">En App.xaml.cs, en "Public App(){}", agregue lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="14eff-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="14eff-192">Identificador de dispositivo</span><span class="sxs-lookup"><span data-stu-id="14eff-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="14eff-193">Puede obtener el identificador del dispositivo de Engagement mediante una llamada a este método.</span><span class="sxs-lookup"><span data-stu-id="14eff-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="14eff-194">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="14eff-194">Extras parameters</span></span>
<span data-ttu-id="14eff-195">Es posible adjuntar datos arbitrarios a un evento, un error, una actividad o un trabajo.</span><span class="sxs-lookup"><span data-stu-id="14eff-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="14eff-196">Estos datos se pueden estructurar mediante un diccionario.</span><span class="sxs-lookup"><span data-stu-id="14eff-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="14eff-197">Las claves y los valores pueden ser de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="14eff-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="14eff-198">Los datos adicionales se serializan, de modo que si desea insertar su propio tipo de datos adicionales, tendrá que agregar un contrato de datos para este tipo.</span><span class="sxs-lookup"><span data-stu-id="14eff-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="14eff-199">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-199">Example</span></span>
<span data-ttu-id="14eff-200">Creamos una nueva clase "Person".</span><span class="sxs-lookup"><span data-stu-id="14eff-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="14eff-201">A continuación, agregaremos una instancia de `Person` a un dato adicional.</span><span class="sxs-lookup"><span data-stu-id="14eff-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="14eff-202">Si coloca otros tipos de objetos, asegúrese de que el método ToString() se implementa para devolver una cadena legible.</span><span class="sxs-lookup"><span data-stu-id="14eff-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="14eff-203">Límites</span><span class="sxs-lookup"><span data-stu-id="14eff-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="14eff-204">simétricas</span><span class="sxs-lookup"><span data-stu-id="14eff-204">Keys</span></span>
<span data-ttu-id="14eff-205">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="14eff-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="14eff-206">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="14eff-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="14eff-207">Tamaño</span><span class="sxs-lookup"><span data-stu-id="14eff-207">Size</span></span>
<span data-ttu-id="14eff-208">Los datos adicionales están limitados a **1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="14eff-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="14eff-209">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="14eff-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="14eff-210">Referencia</span><span class="sxs-lookup"><span data-stu-id="14eff-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="14eff-211">Puede notificar manualmente la información de seguimiento (o cualquier otro tipo de información específica de la aplicación) mediante la función SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="14eff-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="14eff-212">Tenga en cuenta que estos datos se pueden enviar de forma incremental: para un dispositivo concreto solo se conservará el último valor de una clave determinada.</span><span class="sxs-lookup"><span data-stu-id="14eff-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="14eff-213">Al igual que los datos adicionales de evento, use un elemento Dictionary \<object, object\> para adjuntar datos.</span><span class="sxs-lookup"><span data-stu-id="14eff-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="14eff-214">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="14eff-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="14eff-215">Límites</span><span class="sxs-lookup"><span data-stu-id="14eff-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="14eff-216">simétricas</span><span class="sxs-lookup"><span data-stu-id="14eff-216">Keys</span></span>
<span data-ttu-id="14eff-217">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="14eff-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="14eff-218">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="14eff-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="14eff-219">Tamaño</span><span class="sxs-lookup"><span data-stu-id="14eff-219">Size</span></span>
<span data-ttu-id="14eff-220">La información de la aplicación está limitada a **1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="14eff-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="14eff-221">En el ejemplo anterior, el JSON que se envía al servidor tiene una longitud de 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="14eff-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="14eff-222">Registro</span><span class="sxs-lookup"><span data-stu-id="14eff-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="14eff-223">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="14eff-223">Enable Logging</span></span>
<span data-ttu-id="14eff-224">El SDK puede configurarse para generar registros de prueba en la consola del IDE.</span><span class="sxs-lookup"><span data-stu-id="14eff-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="14eff-225">Estos registros no están activados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="14eff-225">These logs are not activated by default.</span></span> <span data-ttu-id="14eff-226">Para personalizar esto, actualice la propiedad `EngagementAgent.Instance.TestLogEnabled` a uno de los valores disponibles en la enumeración `EngagementTestLogLevel`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="14eff-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

