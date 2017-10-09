---
title: "aaaHow tooUse Hola API de interacción en iOS"
description: "IOS más reciente SDK - cómo tooUse Hola API de interacción en iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="3a9f1-103">¿Cómo tooUse Hola API de interacción en iOS</span><span class="sxs-lookup"><span data-stu-id="3a9f1-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="3a9f1-104">Este documento es un complemento toohello cómo tooIntegrate interacción en iOS: proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="3a9f1-105">Tenga en cuenta que si sólo desea interacción tooreport sesiones, actividades, bloqueos y obtener información técnica, de la aplicación hello más sencillo cierto es toomake todos personalizado `UIViewController` objetos heredan de hello correspondiente `EngagementViewController` (clase) .</span><span class="sxs-lookup"><span data-stu-id="3a9f1-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="3a9f1-106">Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementViewController` clases, deberá toouse Hola API de contratación.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="3a9f1-107">Hello interacción API proporcionada por hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="3a9f1-108">Se puede recuperar una instancia de esta clase que realiza la llamada hello `[EngagementAgent shared]` método estático (tenga en cuenta que hello `EngagementAgent` objeto devuelto es un singleton).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="3a9f1-109">Antes de que las llamadas de API, hello `EngagementAgent` objeto debe inicializarse mediante una llamada a método hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="3a9f1-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3a9f1-110">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="3a9f1-110">Engagement concepts</span></span>
<span data-ttu-id="3a9f1-111">Hello partes siguientes refinar Hola comunes [Mobile Engagement conceptos](mobile-engagement-concepts.md) para la plataforma de iOS de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3a9f1-112">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="3a9f1-112">`Session` and `Activity`</span></span>
<span data-ttu-id="3a9f1-113">Un *actividad* suele estar asociado a una pantalla de la aplicación hello, que es hello toosay *actividad* se inicia cuando la pantalla de bienvenida se muestra y se detiene cuando se cierra la pantalla de bienvenida: se trata de hello caso en el que Hello Engagement SDK integrado utilizando hello `EngagementViewController` clases.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="3a9f1-114">Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="3a9f1-115">Esto permite toosplit una pantalla determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta pantalla (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta pantalla).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3a9f1-116">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="3a9f1-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3a9f1-117">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="3a9f1-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="3a9f1-118">Necesita toocall `startActivity()` cambia cada actividad de usuario de hello de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="3a9f1-119">Hola primera llamada toothis función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3a9f1-120">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="3a9f1-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="3a9f1-121">Debería **nunca** llame a esta función por sí mismo, excepto si desea toosplit un uso de la aplicación en varias sesiones: una llamada de función toothis finalizaría Hola actual sesión inmediatamente, por lo tanto, una llamada subsiguiente demasiado`startActivity()`podría iniciar una sesión de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="3a9f1-122">Esta función se invoca automáticamente por hello SDK cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="3a9f1-123">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="3a9f1-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="3a9f1-124">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="3a9f1-124">Session events</span></span>
<span data-ttu-id="3a9f1-125">Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="3a9f1-126">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="3a9f1-127">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="3a9f1-128">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="3a9f1-128">Standalone events</span></span>
<span data-ttu-id="3a9f1-129">Eventos toosession contrarias, independiente pueden utilizarse fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="3a9f1-130">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="3a9f1-131">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="3a9f1-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="3a9f1-132">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="3a9f1-132">Session errors</span></span>
<span data-ttu-id="3a9f1-133">Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="3a9f1-134">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="3a9f1-135">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="3a9f1-135">Standalone errors</span></span>
<span data-ttu-id="3a9f1-136">Toosession contrarias errores, errores de independientes se pueden utilizar fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="3a9f1-137">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="3a9f1-138">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="3a9f1-138">Reporting Jobs</span></span>
<span data-ttu-id="3a9f1-139">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-139">**Example:**</span></span>

<span data-ttu-id="3a9f1-140">Suponga que desea tooreport Hola que dure el proceso de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-140">Suppose you want tooreport hello duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="3a9f1-141">Informe de errores durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3a9f1-141">Report Errors during a Job</span></span>
<span data-ttu-id="3a9f1-142">Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="3a9f1-143">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-143">**Example:**</span></span>

<span data-ttu-id="3a9f1-144">Suponga que desea tooreport un error durante el proceso de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="3a9f1-145">Eventos durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3a9f1-145">Events during a job</span></span>
<span data-ttu-id="3a9f1-146">Pueden tooa relacionado ejecutando el trabajo en lugar de eventos relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="3a9f1-147">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-147">**Example:**</span></span>

<span data-ttu-id="3a9f1-148">Supongamos que tenemos una red social, y utilizamos un trabajo tooreport Hola tiempo total durante qué Hola usuario está conectado toohello server.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="3a9f1-149">usuario de Hello puede recibir mensajes de sus amigos, se trata de un evento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-149">hello user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="3a9f1-150">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="3a9f1-150">Extra parameters</span></span>
<span data-ttu-id="3a9f1-151">Pueden ser datos arbitrarios tooevents adjunto, errores, las actividades y trabajos.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="3a9f1-152">Estos datos pueden estructurarse, utilizan la clase de NSDictionary de iOS.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="3a9f1-153">Tenga en cuenta que los extras pueden contener `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` u otras `NSDictionary` instancias.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="3a9f1-154">Hello adicional parámetro se serializa en JSON.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="3a9f1-155">Si desea toopass distintos objetos que hello las descritas anteriormente, debe implementar Hola siguiendo el método en la clase:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="3a9f1-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="3a9f1-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="3a9f1-157">método Hello debe devolver la representación JSON del objeto.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="3a9f1-158">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3a9f1-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="3a9f1-159">Límites</span><span class="sxs-lookup"><span data-stu-id="3a9f1-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3a9f1-160">simétricas</span><span class="sxs-lookup"><span data-stu-id="3a9f1-160">Keys</span></span>
<span data-ttu-id="3a9f1-161">Cada clave de hello `NSDictionary` debe coincidir con la siguiente expresión regular de Hola:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3a9f1-162">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3a9f1-163">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3a9f1-163">Size</span></span>
<span data-ttu-id="3a9f1-164">Extras se limitan demasiado**1024** caracteres por llamada (una vez codificados en JSON por agente de interacción de hello).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="3a9f1-165">Hola ejemplo anterior, Hola JSON enviado toohello server es 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="3a9f1-166">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="3a9f1-166">Reporting Application Information</span></span>
<span data-ttu-id="3a9f1-167">Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de aplicación) con hello `sendAppInfo:` función.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="3a9f1-168">Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="3a9f1-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="3a9f1-169">Como extras de eventos, hello `NSDictionary` clase es tooabstract usa información de la aplicación, tenga en cuenta que las matrices o diccionarios secundarios se tratará como cadenas sin formato (con la serialización de JSON).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="3a9f1-170">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3a9f1-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="3a9f1-171">Límites</span><span class="sxs-lookup"><span data-stu-id="3a9f1-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3a9f1-172">simétricas</span><span class="sxs-lookup"><span data-stu-id="3a9f1-172">Keys</span></span>
<span data-ttu-id="3a9f1-173">Cada clave de hello `NSDictionary` debe coincidir con la siguiente expresión regular de Hola:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3a9f1-174">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3a9f1-175">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3a9f1-175">Size</span></span>
<span data-ttu-id="3a9f1-176">Información de la aplicación se limitan demasiado**1024** caracteres por llamada (una vez codificados en JSON por agente de interacción de hello).</span><span class="sxs-lookup"><span data-stu-id="3a9f1-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="3a9f1-177">Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="3a9f1-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
