---
title: "Cómo usar la API de Engagement en iOS"
description: "Último SDK de iOS: cómo usar la API de Engagement en iOS"
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
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="10ee2-103">Cómo usar la API de Engagement en iOS</span><span class="sxs-lookup"><span data-stu-id="10ee2-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="10ee2-104">Este documento es un complemento al documento Cómo integrar Engagement en iOS: en él se proporciona información detallada acerca de cómo usar la API de Engagement para informar de las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10ee2-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="10ee2-105">Tenga en cuenta que si solo desea que Engagement informe de las sesiones, las actividades, bloqueos e información técnica de la aplicación, a continuación, la manera más sencilla es hacer que todos los objetos `UIViewController` personalizados hereden de la clase `EngagementViewController` correspondiente.</span><span class="sxs-lookup"><span data-stu-id="10ee2-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="10ee2-106">Si desea hacer más, por ejemplo, si necesita informar de eventos, errores y trabajos específicos de la aplicación, o si debe informar de las actividades de la aplicación de manera diferente de la que se implementa en las clases `EngagementViewController`, deberá usar la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="10ee2-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="10ee2-107">La API de Engagement la proporciona la clase `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="10ee2-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="10ee2-108">Para recuperar una instancia de esta clase puede llamarse al método estático `[EngagementAgent shared]` (tenga en cuenta que el objeto `EngagementAgent` que se devuelve es un singleton).</span><span class="sxs-lookup"><span data-stu-id="10ee2-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="10ee2-109">Antes de las llamadas a una API, el objeto `EngagementAgent` debe inicializarse llamando al método `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="10ee2-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="10ee2-110">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="10ee2-110">Engagement concepts</span></span>
<span data-ttu-id="10ee2-111">En las siguientes secciones se detallan los [conceptos de Mobile Engagement](mobile-engagement-concepts.md) para la plataforma iOS.</span><span class="sxs-lookup"><span data-stu-id="10ee2-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="10ee2-112">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="10ee2-112">`Session` and `Activity`</span></span>
<span data-ttu-id="10ee2-113">Una *actividad* suele asociarse con una pantalla de la aplicación (es decir, la *actividad* se inicia cuando la pantalla se muestra y se detiene cuando se cierra la pantalla, como cuando se integra el SDK de Engagement con el uso de las clases `EngagementViewController`).</span><span class="sxs-lookup"><span data-stu-id="10ee2-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="10ee2-114">Sin embargo, las *actividades* también se pueden controlar manualmente mediante la API de Engagement.</span><span class="sxs-lookup"><span data-stu-id="10ee2-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="10ee2-115">Esto permite dividir una pantalla dada en varias subpartes para obtener más detalles sobre el uso de esta pantalla (por ejemplo, para saber con qué frecuencia y durante cuánto tiempo se utilizan los cuadros de diálogo dentro de esta pantalla).</span><span class="sxs-lookup"><span data-stu-id="10ee2-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="10ee2-116">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="10ee2-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="10ee2-117">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="10ee2-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="10ee2-118">Debe llamar a `startActivity()` cada vez que cambie la actividad de usuario.</span><span class="sxs-lookup"><span data-stu-id="10ee2-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="10ee2-119">La primera llamada a esta función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="10ee2-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="10ee2-120">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="10ee2-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="10ee2-121">**NUNCA** realice una llamada a esta función, excepto si quiere dividir un uso de la aplicación en varias sesiones: una llamada a esta función terminaría la sesión actual inmediatamente, pero puede realizar una llamada posterior a `startActivity()` para iniciar una nueva sesión.</span><span class="sxs-lookup"><span data-stu-id="10ee2-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="10ee2-122">Esta función es invocada automáticamente por el SDK cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="10ee2-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="10ee2-123">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="10ee2-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="10ee2-124">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="10ee2-124">Session events</span></span>
<span data-ttu-id="10ee2-125">Los eventos de sesión se suelen usar para notificar las acciones que realiza el usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="10ee2-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="10ee2-126">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="10ee2-127">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="10ee2-128">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="10ee2-128">Standalone events</span></span>
<span data-ttu-id="10ee2-129">Al contrario de los eventos de sesión, los eventos independientes pueden utilizarse fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="10ee2-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="10ee2-130">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="10ee2-131">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="10ee2-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="10ee2-132">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="10ee2-132">Session errors</span></span>
<span data-ttu-id="10ee2-133">Los errores de sesión suelen usarse para notificar los errores que afectan al usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="10ee2-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="10ee2-134">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="10ee2-135">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="10ee2-135">Standalone errors</span></span>
<span data-ttu-id="10ee2-136">Al contrario de los errores de la sesión, los errores independientes pueden utilizarse fuera del contexto de una sesión.</span><span class="sxs-lookup"><span data-stu-id="10ee2-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="10ee2-137">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="10ee2-138">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="10ee2-138">Reporting Jobs</span></span>
<span data-ttu-id="10ee2-139">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-139">**Example:**</span></span>

<span data-ttu-id="10ee2-140">Supongamos que desea notificar la duración del proceso de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="10ee2-140">Suppose you want to report the duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="10ee2-141">Informe de errores durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="10ee2-141">Report Errors during a Job</span></span>
<span data-ttu-id="10ee2-142">Los errores pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="10ee2-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="10ee2-143">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-143">**Example:**</span></span>

<span data-ttu-id="10ee2-144">Suponga que desea notificar un error durante el proceso de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="10ee2-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="10ee2-145">Eventos durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="10ee2-145">Events during a job</span></span>
<span data-ttu-id="10ee2-146">Los errores pueden estar relacionados con un trabajo en ejecución en lugar de la sesión del usuario actual.</span><span class="sxs-lookup"><span data-stu-id="10ee2-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="10ee2-147">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-147">**Example:**</span></span>

<span data-ttu-id="10ee2-148">Supongamos que tenemos una red social y utilizamos un trabajo de informe del tiempo total durante el cual el usuario está conectado al servidor.</span><span class="sxs-lookup"><span data-stu-id="10ee2-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="10ee2-149">El usuario puede recibir mensajes de sus amigos, este es un evento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="10ee2-149">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="10ee2-150">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="10ee2-150">Extra parameters</span></span>
<span data-ttu-id="10ee2-151">Se pueden adjuntar datos arbitrarios en eventos, errores, actividades y trabajos.</span><span class="sxs-lookup"><span data-stu-id="10ee2-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="10ee2-152">Estos datos pueden estructurarse, utilizan la clase de NSDictionary de iOS.</span><span class="sxs-lookup"><span data-stu-id="10ee2-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="10ee2-153">Tenga en cuenta que los extras pueden contener `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` u otras `NSDictionary` instancias.</span><span class="sxs-lookup"><span data-stu-id="10ee2-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="10ee2-154">El parámetro adicional se serializa en JSON.</span><span class="sxs-lookup"><span data-stu-id="10ee2-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="10ee2-155">Si desea pasar objetos distintos de los descritos anteriormente, debe implementar el método siguiente en la clase:</span><span class="sxs-lookup"><span data-stu-id="10ee2-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="10ee2-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="10ee2-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="10ee2-157">El método debe devolver una representación JSON del objeto.</span><span class="sxs-lookup"><span data-stu-id="10ee2-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="10ee2-158">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10ee2-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="10ee2-159">Límites</span><span class="sxs-lookup"><span data-stu-id="10ee2-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="10ee2-160">simétricas</span><span class="sxs-lookup"><span data-stu-id="10ee2-160">Keys</span></span>
<span data-ttu-id="10ee2-161">Cada clave de la `NSDictionary` debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="10ee2-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="10ee2-162">Esto significa que las claves tienen que empezar como mínimo con una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="10ee2-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="10ee2-163">Tamaño</span><span class="sxs-lookup"><span data-stu-id="10ee2-163">Size</span></span>
<span data-ttu-id="10ee2-164">Los extras están limitados a **1024** caracteres por llamada (una vez codificados en JSON por el agente de Engagement).</span><span class="sxs-lookup"><span data-stu-id="10ee2-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="10ee2-165">En el ejemplo anterior, el JSON que se envía al servidor tiene una longitud de 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="10ee2-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="10ee2-166">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="10ee2-166">Reporting Application Information</span></span>
<span data-ttu-id="10ee2-167">Puede notificar manualmente la información de seguimiento (o cualquier otro tipo de información específica de la aplicación) mediante la función `sendAppInfo:` .</span><span class="sxs-lookup"><span data-stu-id="10ee2-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="10ee2-168">Tenga en cuenta que esta información se puede enviar de forma incremental: para un dispositivo dado solo se conservará el último valor de una clave determinada.</span><span class="sxs-lookup"><span data-stu-id="10ee2-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="10ee2-169">Al igual que los extras de evento, la clase `NSDictionary` se usa para resumir la información de la aplicación. Tenga en cuenta que las matrices o diccionarios secundarios se tratarán como cadenas sin formato (con la serialización de JSON).</span><span class="sxs-lookup"><span data-stu-id="10ee2-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="10ee2-170">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="10ee2-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="10ee2-171">Límites</span><span class="sxs-lookup"><span data-stu-id="10ee2-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="10ee2-172">simétricas</span><span class="sxs-lookup"><span data-stu-id="10ee2-172">Keys</span></span>
<span data-ttu-id="10ee2-173">Cada clave de la `NSDictionary` debe coincidir con la siguiente expresión regular:</span><span class="sxs-lookup"><span data-stu-id="10ee2-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="10ee2-174">Esto significa que las claves tienen que empezar como mínimo con una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="10ee2-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="10ee2-175">Tamaño</span><span class="sxs-lookup"><span data-stu-id="10ee2-175">Size</span></span>
<span data-ttu-id="10ee2-176">La información de la aplicación está limitada a **1024** caracteres por llamada (una vez codificados en JSON por el agente de Engagement).</span><span class="sxs-lookup"><span data-stu-id="10ee2-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="10ee2-177">En el ejemplo anterior, el JSON que se envía al servidor tiene una longitud de 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="10ee2-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
