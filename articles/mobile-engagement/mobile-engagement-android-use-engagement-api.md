---
title: "aaaHow tooUse Hola API de interacción en Android"
description: "SDK de Android más reciente: cómo tooUse Hola API de interacción en Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="3d86e-103">¿Cómo tooUse Hola API de interacción en Android</span><span class="sxs-lookup"><span data-stu-id="3d86e-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="3d86e-104">Este documento es un complemento toohello [opciones avanzadas Reporting para Android SDK de Mobile Engagement](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="3d86e-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="3d86e-105">Proporciona detalles de profundidad acerca de cómo toouse Hola interacción API tooreport las estadísticas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3d86e-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="3d86e-106">Tenga en cuenta que si sólo desea tooreport de interacción de su aplicación sesiones, actividades, se bloquea y obtener información técnica, a continuación, hello manera más sencilla de toomake todas la `Activity` subclases heredan de hello correspondiente `EngagementActivity` clase.</span><span class="sxs-lookup"><span data-stu-id="3d86e-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="3d86e-107">Si desea que toodo más, por ejemplo, si necesita eventos específicos de aplicación tooreport, errores y tareas, o si tienes tooreport actividades de la aplicación de forma diferente de Hola uno implementado en hello `EngagementActivity` clases, deberá toouse Hola API de contratación.</span><span class="sxs-lookup"><span data-stu-id="3d86e-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="3d86e-108">Hello interacción API proporcionada por hello `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="3d86e-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="3d86e-109">Se puede recuperar una instancia de esta clase que realiza la llamada hello `EngagementAgent.getInstance(Context)` método estático (tenga en cuenta que hello `EngagementAgent` objeto devuelto es un singleton).</span><span class="sxs-lookup"><span data-stu-id="3d86e-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="3d86e-110">Conceptos de Engagement</span><span class="sxs-lookup"><span data-stu-id="3d86e-110">Engagement concepts</span></span>
<span data-ttu-id="3d86e-111">Hello partes siguientes refinar Hola comunes [Mobile Engagement conceptos](mobile-engagement-concepts.md), para la plataforma Android Hola.</span><span class="sxs-lookup"><span data-stu-id="3d86e-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="3d86e-112">`Session` y `Activity`</span><span class="sxs-lookup"><span data-stu-id="3d86e-112">`Session` and `Activity`</span></span>
<span data-ttu-id="3d86e-113">Si el usuario de hello permanece más de unos pocos segundos de inactividad entre dos *actividades*, a continuación, su secuencia de *actividades* se divide en dos distintos *sesiones*.</span><span class="sxs-lookup"><span data-stu-id="3d86e-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="3d86e-114">Estos pocos segundos se denominan Hola "session timeout".</span><span class="sxs-lookup"><span data-stu-id="3d86e-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="3d86e-115">Un *actividad* suele estar asociado a una pantalla de la aplicación hello, que es hello toosay *actividad* se inicia cuando la pantalla de bienvenida se muestra y se detiene cuando se cierra la pantalla de bienvenida: se trata de hello caso en el que Hello Engagement SDK integrado utilizando hello `EngagementActivity` clases.</span><span class="sxs-lookup"><span data-stu-id="3d86e-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="3d86e-116">Pero *actividades* también se puede controlar manualmente mediante el uso de API de interacción de Hola.</span><span class="sxs-lookup"><span data-stu-id="3d86e-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="3d86e-117">Esto permite toosplit una pantalla determinada en varios tooget de partes de sub Hola a más detalles sobre el uso de esta pantalla (por ejemplo tooknown con qué frecuencia y cuánto tiempo se utilizan los cuadros de diálogo dentro de esta pantalla).</span><span class="sxs-lookup"><span data-stu-id="3d86e-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="3d86e-118">Informes sobre actividades</span><span class="sxs-lookup"><span data-stu-id="3d86e-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3d86e-119">No es necesario tooreport actividades, como se describe en esta sección si usas hello `EngagementActivity` clase y sus variantes tal como se explica cómo Hola tooIntegrate interacción en documento Android.</span><span class="sxs-lookup"><span data-stu-id="3d86e-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="3d86e-120">El usuario inicia una nueva actividad</span><span class="sxs-lookup"><span data-stu-id="3d86e-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="3d86e-121">Necesita toocall `startActivity()` cambia cada actividad de usuario de hello de tiempo.</span><span class="sxs-lookup"><span data-stu-id="3d86e-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="3d86e-122">Hola primera llamada toothis función inicia una nueva sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="3d86e-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="3d86e-123">Hola mejor toocall lugar esta función es en cada actividad `onResume` devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="3d86e-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="3d86e-124">El usuario finaliza su actividad actual</span><span class="sxs-lookup"><span data-stu-id="3d86e-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="3d86e-125">Necesita toocall `endActivity()` al menos una vez cuando el usuario de hello finaliza su última actividad.</span><span class="sxs-lookup"><span data-stu-id="3d86e-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="3d86e-126">Este modo, informa Hola expirará Engagement SDK que usuario Hola está inactivo y que la sesión de usuario de hello necesario toobe una vez cerrado Hola tiempo de espera de sesión (si se llama a `startActivity()` antes de que expire el tiempo de espera de sesión de hello, simplemente se reanuda la sesión de hello).</span><span class="sxs-lookup"><span data-stu-id="3d86e-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="3d86e-127">Hola mejor toocall lugar esta función es en cada actividad `onPause` devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="3d86e-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="3d86e-128">Informes de eventos</span><span class="sxs-lookup"><span data-stu-id="3d86e-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="3d86e-129">Eventos de sesión</span><span class="sxs-lookup"><span data-stu-id="3d86e-129">Session events</span></span>
<span data-ttu-id="3d86e-130">Eventos de sesión son acciones de Hola de tooreport utilizadas normalmente realizadas por un usuario durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="3d86e-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="3d86e-131">**Ejemplo sin datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="3d86e-132">**Ejemplo con datos adicionales:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="3d86e-133">Eventos independientes</span><span class="sxs-lookup"><span data-stu-id="3d86e-133">Standalone Events</span></span>
<span data-ttu-id="3d86e-134">Eventos de toosession contrarias, pueden producirse eventos de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3d86e-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="3d86e-135">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-135">**Example:**</span></span>

<span data-ttu-id="3d86e-136">Suponga que desea que se producen cuando se desencadena un difusión receptor de eventos de tooreport:</span><span class="sxs-lookup"><span data-stu-id="3d86e-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="3d86e-137">Informes de errores</span><span class="sxs-lookup"><span data-stu-id="3d86e-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="3d86e-138">Errores de sesión</span><span class="sxs-lookup"><span data-stu-id="3d86e-138">Session errors</span></span>
<span data-ttu-id="3d86e-139">Sesión errores son normalmente utilizados tooreport Hola impactar al usuario de Hola durante su sesión.</span><span class="sxs-lookup"><span data-stu-id="3d86e-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="3d86e-140">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="3d86e-141">Errores independientes</span><span class="sxs-lookup"><span data-stu-id="3d86e-141">Standalone errors</span></span>
<span data-ttu-id="3d86e-142">Errores de toosession contrarias, pueden producirse errores de independiente fuera de contexto de Hola de una sesión.</span><span class="sxs-lookup"><span data-stu-id="3d86e-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="3d86e-143">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-143">**Example:**</span></span>

<span data-ttu-id="3d86e-144">Hello en el ejemplo siguiente se muestra cómo tooreport un error cada vez que la memoria de Hola se queda corto de teléfono de Hola durante el proceso de la aplicación se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="3d86e-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="3d86e-145">Informes de trabajos</span><span class="sxs-lookup"><span data-stu-id="3d86e-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="3d86e-146">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d86e-146">Example</span></span>
<span data-ttu-id="3d86e-147">Suponga que desea tooreport Hola que dure el proceso de inicio de sesión:</span><span class="sxs-lookup"><span data-stu-id="3d86e-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="3d86e-148">Informe de errores durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3d86e-148">Report Errors during a Job</span></span>
<span data-ttu-id="3d86e-149">Los errores pueden ser tooa relacionado ejecutando el trabajo en lugar de ser relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="3d86e-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="3d86e-150">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-150">**Example:**</span></span>

<span data-ttu-id="3d86e-151">Suponga que desea tooreport un error durante la iniciar sesión proceso:</span><span class="sxs-lookup"><span data-stu-id="3d86e-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="3d86e-152">[...] inicio de sesión vacío público(Contexto contexto, ...) {</span><span class="sxs-lookup"><span data-stu-id="3d86e-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="3d86e-153">Notificación de eventos durante un trabajo</span><span class="sxs-lookup"><span data-stu-id="3d86e-153">Reporting Events during a job</span></span>
<span data-ttu-id="3d86e-154">Pueden tooa relacionado ejecutando el trabajo en lugar de eventos relacionados con la sesión del usuario actual toohello.</span><span class="sxs-lookup"><span data-stu-id="3d86e-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="3d86e-155">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="3d86e-155">**Example:**</span></span>

<span data-ttu-id="3d86e-156">Supongamos que tenemos una red social, y utilizamos un trabajo tooreport Hola tiempo total durante qué Hola usuario está conectado toohello server.</span><span class="sxs-lookup"><span data-stu-id="3d86e-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="3d86e-157">usuario de Hello puede permanecer conectado en segundo plano incluso cuando está usando otra aplicación o al teléfono de hello está en espera, así que no hay ninguna sesión.</span><span class="sxs-lookup"><span data-stu-id="3d86e-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="3d86e-158">usuario de Hello puede recibir mensajes de sus amigos, se trata de un evento de trabajo.</span><span class="sxs-lookup"><span data-stu-id="3d86e-158">hello user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="3d86e-159">Parámetros adicionales</span><span class="sxs-lookup"><span data-stu-id="3d86e-159">Extra parameters</span></span>
<span data-ttu-id="3d86e-160">Pueden ser datos arbitrarios tooevents adjunto, errores, las actividades y trabajos.</span><span class="sxs-lookup"><span data-stu-id="3d86e-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="3d86e-161">Estos datos se pueden estructurar y usan la clase Bundle de Android (en realidad, funcionan como los parámetros adicionales en los elementos Intent de Android).</span><span class="sxs-lookup"><span data-stu-id="3d86e-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="3d86e-162">Tenga en cuenta que una clase Bundle puede contener matrices u otras instancias de Bundle.</span><span class="sxs-lookup"><span data-stu-id="3d86e-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d86e-163">Si se coloca en los parámetros parcelable o serializables, asegúrese de que sus `toString()` método es tooreturn implementada una cadena legible para el usuario.</span><span class="sxs-lookup"><span data-stu-id="3d86e-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="3d86e-164">Las clases serializables con campos no transitorios de tipo no serializable provocarán un bloqueo de Android cuando se llame a `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="3d86e-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="3d86e-165">No se admiten las matrices ralas en los parámetros adicionales, es decir, no se serializarán como matriz.</span><span class="sxs-lookup"><span data-stu-id="3d86e-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="3d86e-166">Deberán convertirse en matrices estándar antes de usarlas en dichos parámetros.</span><span class="sxs-lookup"><span data-stu-id="3d86e-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="3d86e-167">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d86e-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="3d86e-168">Límites</span><span class="sxs-lookup"><span data-stu-id="3d86e-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3d86e-169">simétricas</span><span class="sxs-lookup"><span data-stu-id="3d86e-169">Keys</span></span>
<span data-ttu-id="3d86e-170">Cada clave de hello `Bundle` debe coincidir con la siguiente expresión regular de Hola:</span><span class="sxs-lookup"><span data-stu-id="3d86e-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3d86e-171">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3d86e-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3d86e-172">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3d86e-172">Size</span></span>
<span data-ttu-id="3d86e-173">Extras se limitan demasiado**1024** caracteres por llamada (una vez codificada en JSON mediante servicio de contratación de hello).</span><span class="sxs-lookup"><span data-stu-id="3d86e-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="3d86e-174">Hola ejemplo anterior, Hola JSON enviado toohello server es 58 caracteres:</span><span class="sxs-lookup"><span data-stu-id="3d86e-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="3d86e-175">Información de la aplicación de informes</span><span class="sxs-lookup"><span data-stu-id="3d86e-175">Reporting Application Information</span></span>
<span data-ttu-id="3d86e-176">Puede crear manualmente informes seguimiento de información (o cualquier otra información específica de aplicación) con hello `sendAppInfo()` función.</span><span class="sxs-lookup"><span data-stu-id="3d86e-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="3d86e-177">Tenga en cuenta que esta información pueden enviarse de forma incremental: solo Hola valor más reciente de una clave determinada se mantendrán para un dispositivo determinado.</span><span class="sxs-lookup"><span data-stu-id="3d86e-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="3d86e-178">Al igual que eventos adicionales, hello clase agrupación es tooabstract usa información de la aplicación, tenga en cuenta que las matrices o Sub-empaqueta se tratará como cadenas sin formato (con la serialización de JSON).</span><span class="sxs-lookup"><span data-stu-id="3d86e-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="3d86e-179">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3d86e-179">Example</span></span>
<span data-ttu-id="3d86e-180">Este es un sexo del usuario de toosend de ejemplo de código y la fecha de nacimiento:</span><span class="sxs-lookup"><span data-stu-id="3d86e-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="3d86e-181">límites</span><span class="sxs-lookup"><span data-stu-id="3d86e-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="3d86e-182">simétricas</span><span class="sxs-lookup"><span data-stu-id="3d86e-182">Keys</span></span>
<span data-ttu-id="3d86e-183">Cada clave de hello `Bundle` debe coincidir con la siguiente expresión regular de Hola:</span><span class="sxs-lookup"><span data-stu-id="3d86e-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="3d86e-184">Esto significa que las claves deben empezar con al menos una letra, seguida de letras, dígitos o caracteres de subrayado (\_).</span><span class="sxs-lookup"><span data-stu-id="3d86e-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="3d86e-185">Tamaño</span><span class="sxs-lookup"><span data-stu-id="3d86e-185">Size</span></span>
<span data-ttu-id="3d86e-186">Información de la aplicación se limitan demasiado**1024** caracteres por llamada (una vez codificada en JSON mediante servicio de contratación de hello).</span><span class="sxs-lookup"><span data-stu-id="3d86e-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="3d86e-187">Hola ejemplo anterior, Hola JSON enviado toohello server es 44 caracteres:</span><span class="sxs-lookup"><span data-stu-id="3d86e-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
