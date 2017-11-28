---
title: aaaAdvanced reporting opciones para Android SDK de Azure Mobile Engagement
description: "Describe cómo toodo informes toocapture análisis avanzados para Android SDK de Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="a53f2-103">Informes avanzados con Engagement en Android</span><span class="sxs-lookup"><span data-stu-id="a53f2-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a53f2-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="a53f2-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="a53f2-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a53f2-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="a53f2-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a53f2-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="a53f2-107">Android</span><span class="sxs-lookup"><span data-stu-id="a53f2-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="a53f2-108">Este tema describe los escenarios de informes adicionales en la aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="a53f2-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="a53f2-109">Puede aplicar estas aplicaciones de toohello opciones creado en hello [Introducción](mobile-engagement-android-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a53f2-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a53f2-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a53f2-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="a53f2-111">tutorial de Hola completó era deliberadamente sencillo y directo, pero existe son las opciones avanzadas que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="a53f2-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="a53f2-112">Modificación de sus clases `Activity`</span><span class="sxs-lookup"><span data-stu-id="a53f2-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="a53f2-113">Hola [tutorial de introducción](mobile-engagement-android-get-started.md), todo lo que tenía toodo fue toomake su `*Activity` subclases heredan de hello correspondiente `Engagement*Activity` clases.</span><span class="sxs-lookup"><span data-stu-id="a53f2-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="a53f2-114">Por ejemplo, si su actividad heredada amplía `ListActivity`, se ampliaría `EngagementListActivity` también.</span><span class="sxs-lookup"><span data-stu-id="a53f2-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a53f2-115">Cuando se usa `EngagementListActivity` o `EngagementExpandableListActivity`, asegúrese de que todas las llamadas demasiado`requestWindowFeature(...);` se realiza antes de la llamada de hello demasiado`super.onCreate(...);`, de lo contrario se produce un bloqueo.</span><span class="sxs-lookup"><span data-stu-id="a53f2-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="a53f2-116">Puede encontrar estas clases en hello `src` carpeta y puede copiarlos en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="a53f2-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="a53f2-117">clases de Hello también están en hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="a53f2-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="a53f2-118">Método alternativo: llamar a `startActivity()` y `endActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="a53f2-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="a53f2-119">Si no puede o no desea que toooverload su `Activity` clases, puede en su lugar, inicio y finalización de las actividades mediante una llamada a hello `EngagementAgent`de métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="a53f2-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a53f2-120">Hola SDK de Android nunca llama hello `endActivity()` método, incluso cuando se cierra la aplicación hello (en Android, las aplicaciones nunca se cierran).</span><span class="sxs-lookup"><span data-stu-id="a53f2-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="a53f2-121">Por lo tanto, es *alta* recomienda hello toocall `startActivity()` método Hola `onResume` devolución de llamada de *todos los* sus actividades y hello `endActivity()` método Hola `onPause()` devolución de llamada de *todos los* sus actividades.</span><span class="sxs-lookup"><span data-stu-id="a53f2-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="a53f2-122">Se trata de toobe de manera única de hello seguro de que no se pierden las sesiones.</span><span class="sxs-lookup"><span data-stu-id="a53f2-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="a53f2-123">Si una sesión se ha filtrado, Hola servicio interacción nunca se desconecta de backend de interacción de hello (ya que servicio Hola permanece conectado mientras está pendiente una sesión).</span><span class="sxs-lookup"><span data-stu-id="a53f2-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="a53f2-124">Aquí tiene un ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a53f2-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="a53f2-125">En este ejemplo es similar toohello `EngagementActivity` clase y sus variantes, cuyo código fuente se proporciona en hello `src` carpeta.</span><span class="sxs-lookup"><span data-stu-id="a53f2-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="a53f2-126">Uso de Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="a53f2-126">Using Application.onCreate()</span></span>
<span data-ttu-id="a53f2-127">Cualquier código que se coloque en `Application.onCreate()` y en otra aplicación, las devoluciones de llamada se ejecuta para los procesos de todas las de su aplicación, incluido el servicio de contratación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a53f2-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="a53f2-128">Puede tener efectos secundarios no deseados, como las asignaciones de memoria innecesario y subprocesos en el proceso de contratación de hello, o duplicado difusión receptores o servicios.</span><span class="sxs-lookup"><span data-stu-id="a53f2-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="a53f2-129">Si invalida `Application.onCreate()`, se recomienda agregar Hola siguiente fragmento de código al principio de Hola de su `Application.onCreate()` función:</span><span class="sxs-lookup"><span data-stu-id="a53f2-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="a53f2-130">Puede hacer lo mismo para Hola `Application.onTerminate()`, `Application.onLowMemory()`, y `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="a53f2-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="a53f2-131">También puede extender `EngagementApplication` en lugar de extender `Application`: Hola de devolución de llamada `Application.onCreate()` Hola comprobación del proceso y llamadas `Application.onApplicationProcessCreate()` solo si proceso actual de hello es no Hola uno Hola interacción servicio de hospedaje, hello mismas reglas se aplican para Hola otras devoluciones de llamada.</span><span class="sxs-lookup"><span data-stu-id="a53f2-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="a53f2-132">Etiquetas en el archivo AndroidManifest.xml Hola</span><span class="sxs-lookup"><span data-stu-id="a53f2-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="a53f2-133">En la etiqueta de servicio de hello en el archivo AndroidManifest.xml hello, Hola `android:label` atributo permite toochoose Hola nombre de servicio de contratación de hello tal y como aparece tooend a los usuarios en la pantalla de bienvenida "Ejecutar servicios" de su teléfono.</span><span class="sxs-lookup"><span data-stu-id="a53f2-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="a53f2-134">Se recomienda establecer este atributo demasiado`"<Your application name>Service"` (por ejemplo, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="a53f2-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="a53f2-135">Hola especificando `android:process` atributo garantiza que Hola se ejecuta en su propio proceso (ejecutando interacción en el mismo proceso cuando la aplicación realiza el subproceso de interfaz de usuario/main potencialmente menos capacidad de respuesta de Hola) en el servicio de contratación.</span><span class="sxs-lookup"><span data-stu-id="a53f2-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="a53f2-136">Compilación con ProGuard</span><span class="sxs-lookup"><span data-stu-id="a53f2-136">Building with ProGuard</span></span>
<span data-ttu-id="a53f2-137">Si compila el paquete de aplicación con ProGuard, deberá tookeep algunas clases.</span><span class="sxs-lookup"><span data-stu-id="a53f2-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="a53f2-138">Puede usar Hola siguiente fragmento de código de configuración:</span><span class="sxs-lookup"><span data-stu-id="a53f2-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
