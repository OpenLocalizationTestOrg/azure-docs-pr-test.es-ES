---
title: "aaaWindows Universal avanzada Reporting con interacción de MobileApps"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="76ee5-103">Informes avanzados con hello SDK de interacción de aplicaciones Universal de Windows</span><span class="sxs-lookup"><span data-stu-id="76ee5-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76ee5-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="76ee5-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="76ee5-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="76ee5-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="76ee5-106">iOS</span><span class="sxs-lookup"><span data-stu-id="76ee5-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="76ee5-107">Android</span><span class="sxs-lookup"><span data-stu-id="76ee5-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="76ee5-108">Este tema describe los escenarios de informes adicionales en la aplicación universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="76ee5-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="76ee5-109">Estos escenarios incluyen opciones que puede elegir tooapply toohello aplicación creado en hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="76ee5-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76ee5-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="76ee5-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="76ee5-111">Antes de iniciar este tutorial, debe completar primero hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, que es deliberadamente sencilla y directa.</span><span class="sxs-lookup"><span data-stu-id="76ee5-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="76ee5-112">Este tutorial explica las opciones adicionales que puede elegir.</span><span class="sxs-lookup"><span data-stu-id="76ee5-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="76ee5-113">Especificación de la configuración de Engagement en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="76ee5-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="76ee5-114">configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto, que es donde se especifica en hello [Introducción](mobile-engagement-windows-store-dotnet-get-started.md) tema.</span><span class="sxs-lookup"><span data-stu-id="76ee5-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="76ee5-115">Pero también puede especificar en tiempo de ejecución: se puede llamar a Hola siguiente método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="76ee5-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="76ee5-116">Método recomendado: sobrecargar las clases `Page`</span><span class="sxs-lookup"><span data-stu-id="76ee5-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="76ee5-117">tooactivate Hola reporting de todos los registros de hello requeridos interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, poner todos los su `Page` subclases heredan de hello `EngagementPage` clases.</span><span class="sxs-lookup"><span data-stu-id="76ee5-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="76ee5-118">Este es un ejemplo para una página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="76ee5-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="76ee5-119">Puede hacer lo mismo para todas las páginas de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="76ee5-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="76ee5-120">Archivo de código fuente C#</span><span class="sxs-lookup"><span data-stu-id="76ee5-120">C# Source file</span></span>
<span data-ttu-id="76ee5-121">Modifique el archivo `.xaml.cs` de página:</span><span class="sxs-lookup"><span data-stu-id="76ee5-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="76ee5-122">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="76ee5-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="76ee5-123">Reemplace `Page` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="76ee5-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="76ee5-124">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76ee5-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="76ee5-125">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76ee5-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="76ee5-126">Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="76ee5-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="76ee5-127">De lo contrario, actividad hello no se notificará (hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="76ee5-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="76ee5-128">Archivo XAML</span><span class="sxs-lookup"><span data-stu-id="76ee5-128">XAML file</span></span>
<span data-ttu-id="76ee5-129">Modifique el archivo `.xaml` de página:</span><span class="sxs-lookup"><span data-stu-id="76ee5-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="76ee5-130">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="76ee5-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="76ee5-131">Reemplace `Page` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="76ee5-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="76ee5-132">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76ee5-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="76ee5-133">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="76ee5-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="76ee5-134">Invalidar el comportamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="76ee5-134">Override hello default behaviour</span></span>
<span data-ttu-id="76ee5-135">De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra.</span><span class="sxs-lookup"><span data-stu-id="76ee5-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="76ee5-136">Si la clase hello usa el sufijo "Página" Hola, interacción quita.</span><span class="sxs-lookup"><span data-stu-id="76ee5-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="76ee5-137">comportamiento de toooverride Hola predeterminado para el nombre de hello, agregue este código:</span><span class="sxs-lookup"><span data-stu-id="76ee5-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="76ee5-138">tooreport información adicional con la actividad, agregue este código:</span><span class="sxs-lookup"><span data-stu-id="76ee5-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="76ee5-139">Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.</span><span class="sxs-lookup"><span data-stu-id="76ee5-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="76ee5-140">Método alternativo: llamar a `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="76ee5-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="76ee5-141">Si no puede o no desea que toooverload su `Page` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="76ee5-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="76ee5-142">Se recomienda llamar a `StartActivity` dentro del método `OnNavigatedTo` de su página.</span><span class="sxs-lookup"><span data-stu-id="76ee5-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="76ee5-143">Asegúrese de finalizar la sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="76ee5-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="76ee5-144">Hola SDK Universal de Windows llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="76ee5-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="76ee5-145">Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método.</span><span class="sxs-lookup"><span data-stu-id="76ee5-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="76ee5-146">Este método notifica a servidor de interacción de Hola que el usuario actual Hola ha dejado la aplicación hello, lo que afectará a todos los registros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="76ee5-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="76ee5-147">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="76ee5-147">Advanced reporting</span></span>
<span data-ttu-id="76ee5-148">Si lo desea, puede que desee eventos específicos de la aplicación de tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="76ee5-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="76ee5-149">Hola interacción API permite el uso de las capacidades avanzadas de todas las interacciones.</span><span class="sxs-lookup"><span data-stu-id="76ee5-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="76ee5-150">Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="76ee5-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

