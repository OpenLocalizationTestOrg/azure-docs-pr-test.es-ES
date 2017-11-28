---
title: "Cómo usar la API de Engagement en Windows Phone Silverlight"
description: "Cómo usar la API de Engagement en Windows Phone Silverlight"
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="49e59-103">Cómo usar la API de Engagement en Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="49e59-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="49e59-104">Este documento es un complemento al documento [Cómo integrar Mobile Engagement en su aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="49e59-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="49e59-105">En él se proporciona información detallada acerca de cómo usar la API de Engagement para informar de las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e59-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="49e59-106">Si solo desea que Engagement informe sobre las sesiones, las actividades, los bloqueos y la información técnica de la aplicación, la manera más sencilla consiste en hacer que las subclases `PhoneApplicationPage` hereden de la clase `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="49e59-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="49e59-107">Si desea hacer más, por ejemplo, si necesita informar de eventos, errores y trabajos específicos de la aplicación, o si debe informar de las actividades de la aplicación de manera diferente de la que se implementa en las clases `EngagementPage`, deberá usar la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="49e59-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="49e59-108">La API de Engagement la proporciona la clase `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="49e59-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="49e59-109">Puede acceder a esos métodos a través de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="49e59-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="49e59-110">Incluso si no se ha inicializado el módulo de agente, las llamadas a la API se aplazan y se ejecutará de nuevo cuando el agente está disponible.</span><span class="sxs-lookup"><span data-stu-id="49e59-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="49e59-111">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="49e59-111">Engagement concepts</span></span>
<span data-ttu-id="49e59-112">En las siguientes secciones se detallan los conceptos de Mobile Engagement para la plataforma Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="49e59-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="49e59-113">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="49e59-113">`Session` and `Activity`</span></span>
<span data-ttu-id="49e59-114">Una *actividad* suele estar asociada con una página de la aplicación. Es decir, la *actividad* se inicia cuando la página se muestra y se detiene cuando se cierra la página. Este es el caso cuando la integración del SDK de Engagement se realiza mediante la clase `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="49e59-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="49e59-115">Sin embargo, las *actividades* también se pueden controlar manualmente mediante la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="49e59-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="49e59-116">Esto permite dividir una página determinada en varias subpartes para obtener más detalles sobre el uso de esta página (por ejemplo, la frecuencia y la duración con las que se usan los cuadros de diálogo en esta página).</span><span class="sxs-lookup"><span data-stu-id="49e59-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="49e59-117">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="49e59-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="49e59-118">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="49e59-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-119">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-120">Debe llamar a `StartActivity()` cada vez que cambie la actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="49e59-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="49e59-121">La primera llamada a esta función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="49e59-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49e59-122">El SDK llaman automáticamente al método EndActivity cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e59-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="49e59-123">Por lo tanto, es MUY recomendable llamar al método StartActivity cada vez que cambie la actividad del usuario y NUNCA llamar al método EndActivity, ya que esto obliga la finalización de la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="49e59-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="49e59-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="49e59-125">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="49e59-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-126">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="49e59-127">Cuando el usuario finaliza su última actividad, se debe llamar a `EndActivity()` al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="49e59-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="49e59-128">De esta manera se informa al SDK de Engagement de que el usuario está inactivo y que la sesión del usuario se debe cerrar cuando expire el tiempo de espera de la misma (si se llama a `StartActivity()` antes de que expire dicho tiempo de espera, la sesión simplemente continúa).</span><span class="sxs-lookup"><span data-stu-id="49e59-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-129">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="49e59-130">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="49e59-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="49e59-131">Iniciar un trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-132">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-133">Puede usar el trabajo para hace un seguimiento de tareas determinadas durante un período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="49e59-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-134">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="49e59-135">Finalizar un trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-136">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="49e59-137">Cuando haya finalizado una tarea de la que un trabajo realiza el seguimiento, se debe llamar al método EndJob para este trabajo al proporcionar su nombre.</span><span class="sxs-lookup"><span data-stu-id="49e59-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="49e59-139">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="49e59-139">Reporting Events</span></span>
<span data-ttu-id="49e59-140">Hay tres tipos de eventos:</span><span class="sxs-lookup"><span data-stu-id="49e59-140">There is three types of events :</span></span>

* <span data-ttu-id="49e59-141">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="49e59-141">Standalone events</span></span>
* <span data-ttu-id="49e59-142">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="49e59-142">Session events</span></span>
* <span data-ttu-id="49e59-143">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="49e59-144">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="49e59-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-145">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-146">Los eventos independientes se pueden producir fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="49e59-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-147">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="49e59-148">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="49e59-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-149">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-150">Los eventos de sesión se suelen usar para notificar las acciones que realiza el usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="49e59-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-151">Example</span></span>
<span data-ttu-id="49e59-152">**Sin datos:**</span><span class="sxs-lookup"><span data-stu-id="49e59-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="49e59-153">**Con datos:**</span><span class="sxs-lookup"><span data-stu-id="49e59-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="49e59-154">Eventos de trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-155">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-156">Los eventos de trabajo se suelen usar para notificar las acciones que realiza un usuario durante un trabajo.</span><span class="sxs-lookup"><span data-stu-id="49e59-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-157">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="49e59-158">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="49e59-158">Reporting Errors</span></span>
<span data-ttu-id="49e59-159">Hay tres tipos de errores:</span><span class="sxs-lookup"><span data-stu-id="49e59-159">There is three types of errors :</span></span>

* <span data-ttu-id="49e59-160">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="49e59-160">Standalone errors</span></span>
* <span data-ttu-id="49e59-161">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="49e59-161">Session errors</span></span>
* <span data-ttu-id="49e59-162">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="49e59-163">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="49e59-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-164">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-165">Al contrario de los errores de sesión, los errores independientes se pueden producir fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="49e59-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-166">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="49e59-167">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="49e59-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-168">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-169">Los errores de sesión suelen usarse para notificar los errores que afectan al usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="49e59-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-170">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="49e59-171">Errores de trabajo</span><span class="sxs-lookup"><span data-stu-id="49e59-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-172">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="49e59-173">Los errores pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="49e59-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="49e59-175">Informes de bloqueos</span><span class="sxs-lookup"><span data-stu-id="49e59-175">Reporting Crashes</span></span>
<span data-ttu-id="49e59-176">El agente proporciona dos métodos para tratar los bloqueos.</span><span class="sxs-lookup"><span data-stu-id="49e59-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="49e59-177">Enviar una excepción</span><span class="sxs-lookup"><span data-stu-id="49e59-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-178">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="49e59-179">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-179">Example</span></span>
<span data-ttu-id="49e59-180">Puede enviar una excepción en cualquier momento al llamar a:</span><span class="sxs-lookup"><span data-stu-id="49e59-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="49e59-181">También puede usar un parámetro opcional para finalizar la sesión de Engagement al mismo tiempo que se envía el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="49e59-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="49e59-182">Para ello, llame a:</span><span class="sxs-lookup"><span data-stu-id="49e59-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="49e59-183">Si lo hace, la sesión y los trabajos se cerrarán después de enviar el bloqueo.</span><span class="sxs-lookup"><span data-stu-id="49e59-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="49e59-184">Enviar una excepción no controlada</span><span class="sxs-lookup"><span data-stu-id="49e59-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="49e59-185">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="49e59-186">Engagement también proporciona un método para enviar excepciones no controladas.</span><span class="sxs-lookup"><span data-stu-id="49e59-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="49e59-187">Esto es especialmente útil cuando se usa dentro del controlador de eventos UnhandledException de Silverlight.</span><span class="sxs-lookup"><span data-stu-id="49e59-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="49e59-188">Este método **SIEMPRE** finalizará la sesión y los trabajos de Engagement después de su invocación.</span><span class="sxs-lookup"><span data-stu-id="49e59-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="49e59-189">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-189">Example</span></span>
<span data-ttu-id="49e59-190">Puede usarlo para implementar su propio controlador UnhandledException (especialmente si deshabilitó la característica de informes de errores automáticos de Engagement).</span><span class="sxs-lookup"><span data-stu-id="49e59-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="49e59-191">Por ejemplo, en el método `Application_UnhandledException` del archivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="49e59-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="49e59-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="49e59-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="49e59-193">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="49e59-194">Cuando el usuario se desplaza hacia delante, alejándose de una aplicación, después de que se genere el evento Desactivado, el sistema operativo intentará poner la aplicación en un estado inactivo.</span><span class="sxs-lookup"><span data-stu-id="49e59-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="49e59-195">A continuación, la aplicación se encuentra en un estado conocido como "extinción".</span><span class="sxs-lookup"><span data-stu-id="49e59-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="49e59-196">En este proceso, la aplicación se finaliza, pero se conservan algunos datos sobre su estado, así como las páginas individuales dentro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="49e59-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="49e59-197">Tiene que insertar `EngagementAgent.Instance.OnActivated(e)` en el método `Application_Activated` desde el archivo App.xaml.cs para restablecer el agente de Engagement cuando la aplicación se haya puesto en estado de extinción.</span><span class="sxs-lookup"><span data-stu-id="49e59-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="49e59-198">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="49e59-199">Identificador de dispositivo</span><span class="sxs-lookup"><span data-stu-id="49e59-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="49e59-200">Puede obtener el identificador del dispositivo de Engagement mediante una llamada a este método.</span><span class="sxs-lookup"><span data-stu-id="49e59-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="49e59-201">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="49e59-201">Extras parameters</span></span>
<span data-ttu-id="49e59-202">Es posible adjuntar datos arbitrarios a un evento, un error, una actividad o un trabajo.</span><span class="sxs-lookup"><span data-stu-id="49e59-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="49e59-203">Estos datos se pueden estructurar mediante un diccionario.</span><span class="sxs-lookup"><span data-stu-id="49e59-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="49e59-204">Las claves y los valores pueden ser de cualquier tipo.</span><span class="sxs-lookup"><span data-stu-id="49e59-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="49e59-205">Los datos adicionales se serializan, de modo que si desea insertar su propio tipo de datos adicionales, tendrá que agregar un contrato de datos para este tipo.</span><span class="sxs-lookup"><span data-stu-id="49e59-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="49e59-206">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-206">Example</span></span>
<span data-ttu-id="49e59-207">Creamos una nueva clase "Person".</span><span class="sxs-lookup"><span data-stu-id="49e59-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="49e59-208">A continuación, agregaremos una instancia de `Person` a un dato adicional.</span><span class="sxs-lookup"><span data-stu-id="49e59-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="49e59-209">Si coloca otros tipos de objetos, asegúrese de que el método ToString() se implementa para devolver una cadena legible.</span><span class="sxs-lookup"><span data-stu-id="49e59-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="49e59-210">Límites</span><span class="sxs-lookup"><span data-stu-id="49e59-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="49e59-211">simétricas</span><span class="sxs-lookup"><span data-stu-id="49e59-211">Keys</span></span>
<span data-ttu-id="49e59-212">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="49e59-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="49e59-213">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="49e59-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="49e59-214">Tamaño</span><span class="sxs-lookup"><span data-stu-id="49e59-214">Size</span></span>
<span data-ttu-id="49e59-215">Los datos adicionales están limitados a **1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="49e59-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="49e59-216">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="49e59-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="49e59-217">Referencia</span><span class="sxs-lookup"><span data-stu-id="49e59-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="49e59-218">Puede notificar manualmente la información de seguimiento (o cualquier otro tipo de información específica de la aplicación) mediante la función SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="49e59-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="49e59-219">Tenga en cuenta que esta información se puede enviar de forma incremental: para un dispositivo dado solo se conservará el último valor de una clave determinada.</span><span class="sxs-lookup"><span data-stu-id="49e59-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="49e59-220">Al igual que los datos adicionales de evento, use un elemento de Dictionary \<object, object\> para adjuntar información.</span><span class="sxs-lookup"><span data-stu-id="49e59-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="49e59-221">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="49e59-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="49e59-222">Límites</span><span class="sxs-lookup"><span data-stu-id="49e59-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="49e59-223">simétricas</span><span class="sxs-lookup"><span data-stu-id="49e59-223">Keys</span></span>
<span data-ttu-id="49e59-224">Cada clave del objeto debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="49e59-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="49e59-225">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="49e59-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="49e59-226">Tamaño</span><span class="sxs-lookup"><span data-stu-id="49e59-226">Size</span></span>
<span data-ttu-id="49e59-227">La información de la aplicación está limitada a **1024** caracteres por llamada.</span><span class="sxs-lookup"><span data-stu-id="49e59-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="49e59-228">En el ejemplo anterior, el JSON que se envía al servidor tiene una longitud de 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="49e59-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="49e59-229">Registro</span><span class="sxs-lookup"><span data-stu-id="49e59-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="49e59-230">Habilitación del registro</span><span class="sxs-lookup"><span data-stu-id="49e59-230">Enable Logging</span></span>
<span data-ttu-id="49e59-231">El SDK puede configurarse para generar registros de prueba en la consola del IDE.</span><span class="sxs-lookup"><span data-stu-id="49e59-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="49e59-232">Estos registros no están activados de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="49e59-232">These logs are not activated by default.</span></span> <span data-ttu-id="49e59-233">Para personalizar esto, actualice la propiedad `EngagementAgent.Instance.TestLogEnabled` a uno de los valores disponibles en la enumeración `EngagementTestLogLevel`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="49e59-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
