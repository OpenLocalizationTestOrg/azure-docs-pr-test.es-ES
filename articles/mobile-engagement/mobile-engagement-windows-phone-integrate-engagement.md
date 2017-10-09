---
title: "aaaWindows integración con el SDK interacción Phone Silverlight"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones de Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="11703-103">Integración del SDK de Windows Phone Silverlight Engagement</span><span class="sxs-lookup"><span data-stu-id="11703-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="11703-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="11703-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="11703-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="11703-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="11703-106">iOS</span><span class="sxs-lookup"><span data-stu-id="11703-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="11703-107">Android</span><span class="sxs-lookup"><span data-stu-id="11703-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="11703-108">Este procedimiento describe las funciones en la aplicación de Windows Phone Silverlight de supervisión y análisis hello más sencilla forma tooactivate Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="11703-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="11703-109">Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals.</span><span class="sxs-lookup"><span data-stu-id="11703-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="11703-110">Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) a continuación) debido a que estas estadísticas son dependientes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11703-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="11703-111">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="11703-111">Supported versions</span></span>
<span data-ttu-id="11703-112">Hola Mobile Engagement SDK para Silverlight para Windows sólo se puede integrar en las aplicaciones con destino:</span><span class="sxs-lookup"><span data-stu-id="11703-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="11703-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="11703-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="11703-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="11703-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="11703-115">Si se dirige a Windows Phone 8.1 (no de Silverlight), consulte toohello [procedimiento de integración de Windows Universal](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="11703-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="11703-116">Instalar el SDK de Silverlight de Mobile Engagement Hola</span><span class="sxs-lookup"><span data-stu-id="11703-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="11703-117">Hola Mobile Engagement SDK para Silverlight para Windows está disponible como un paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="11703-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="11703-118">Puede instalarlo desde Hola Administrador de paquetes de Nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="11703-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="11703-119">Agregar capacidades de Hola</span><span class="sxs-lookup"><span data-stu-id="11703-119">Add hello capabilities</span></span>
<span data-ttu-id="11703-120">Hola Engagement SDK tiene algunas capacidades de hello SDK de Windows Phone Silverlight en orden toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="11703-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="11703-121">Abra su `WMAppManifest.xml` de archivos y asegúrese de que Hola siguiendo las capacidades se declaran en hello `Capabilities` panel:</span><span class="sxs-lookup"><span data-stu-id="11703-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="11703-122">Inicializar Hola Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="11703-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="11703-123">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="11703-123">Engagement configuration</span></span>
<span data-ttu-id="11703-124">configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="11703-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="11703-125">Editar este archivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="11703-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="11703-126">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="11703-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="11703-127">Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="11703-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="11703-128">cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="11703-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="11703-129">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="11703-129">Engagement initialization</span></span>
<span data-ttu-id="11703-130">Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="11703-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="11703-131">Esta clase hereda de `Application` y contiene muchos métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="11703-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="11703-132">También será usado tooinitialize Hola Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="11703-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="11703-133">Modificar Hola `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="11703-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="11703-134">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="11703-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="11703-135">Insertar `EngagementAgent.Instance.Init` en hello `Application_Launching` método:</span><span class="sxs-lookup"><span data-stu-id="11703-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="11703-136">Insertar `EngagementAgent.Instance.OnActivated` en hello `Application_Activated` método:</span><span class="sxs-lookup"><span data-stu-id="11703-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="11703-137">Se desaconseja encarecidamente tooadd Hola interacción inicialización en otro lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11703-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="11703-138">Sin embargo, tenga en cuenta que hello `EngagementAgent.Instance.Init` método se ejecuta en un subproceso dedicado y no en el subproceso de interfaz de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="11703-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="11703-139">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="11703-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="11703-140">Método recomendado: sobrecargar las clases `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="11703-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="11703-141">Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `PhoneApplicationPage` subclases heredan de hello `EngagementPage` clases.</span><span class="sxs-lookup"><span data-stu-id="11703-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="11703-142">Este es un ejemplo de cómo toodo esto en una página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="11703-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="11703-143">Puede hacer lo mismo para todas las páginas de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="11703-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="11703-144">Archivo de código fuente C#</span><span class="sxs-lookup"><span data-stu-id="11703-144">C# Source file</span></span>
<span data-ttu-id="11703-145">Modifique el archivo `.xaml.cs` de página:</span><span class="sxs-lookup"><span data-stu-id="11703-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="11703-146">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="11703-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="11703-147">Reemplace `PhoneApplicationPage` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="11703-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="11703-148">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="11703-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="11703-149">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="11703-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="11703-150">Si la página hereda de hello `OnNavigatedTo` método, puede toolet cuidado Hola `base.OnNavigatedTo(e)` llamar.</span><span class="sxs-lookup"><span data-stu-id="11703-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="11703-151">En caso contrario, no se notificarán actividad hello.</span><span class="sxs-lookup"><span data-stu-id="11703-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="11703-152">De hecho, Hola `EngagementPage` llama a `StartActivity` dentro de hello `OnNavigatedTo` método.</span><span class="sxs-lookup"><span data-stu-id="11703-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="11703-153">Archivo XAML</span><span class="sxs-lookup"><span data-stu-id="11703-153">XAML file</span></span>
<span data-ttu-id="11703-154">Modifique el archivo `.xaml` de página:</span><span class="sxs-lookup"><span data-stu-id="11703-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="11703-155">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="11703-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="11703-156">Reemplace `phone:PhoneApplicationPage` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="11703-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="11703-157">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="11703-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="11703-158">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="11703-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="11703-159">Invalidar el comportamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="11703-159">Override hello default behavior</span></span>
<span data-ttu-id="11703-160">De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra.</span><span class="sxs-lookup"><span data-stu-id="11703-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="11703-161">Si la clase hello usa el sufijo "Página" Hola, interacción, también se quitará.</span><span class="sxs-lookup"><span data-stu-id="11703-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="11703-162">Si desea comportamiento predeterminado de toooverride Hola para nombre de hello, basta con agregar este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="11703-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="11703-163">Si desea tooreport cierta información adicional con la actividad, puede agregar este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="11703-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="11703-164">Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.</span><span class="sxs-lookup"><span data-stu-id="11703-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="11703-165">Método alternativo: llamar a `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="11703-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="11703-166">Si no puede o no desea que toooverload su `PhoneApplicationPage` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="11703-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="11703-167">Recomendamos que llame a `StartActivity` dentro del método `OnNavigatedTo` de su PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="11703-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="11703-168">Asegúrese de finalizar la sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="11703-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="11703-169">Hola SDK llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="11703-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="11703-170">Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método.</span><span class="sxs-lookup"><span data-stu-id="11703-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="11703-171">Este método envía un servidor de interacción de toohello mensajes que usuario actual de hello ha abandonado la aplicación hello y esto afecta a todos los registros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="11703-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="11703-172">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="11703-172">Advanced reporting</span></span>
<span data-ttu-id="11703-173">Si lo desea, puede que desee eventos específicos de aplicación tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="11703-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="11703-174">Hola interacción API permite toouse todas las capacidades avanzadas de contratación.</span><span class="sxs-lookup"><span data-stu-id="11703-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="11703-175">Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="11703-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="11703-176">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="11703-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="11703-177">Deshabilitar los informes automáticos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="11703-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="11703-178">Puede deshabilitar Hola automática de informes de errores característica de contratación.</span><span class="sxs-lookup"><span data-stu-id="11703-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="11703-179">A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.</span><span class="sxs-lookup"><span data-stu-id="11703-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="11703-180">Si tiene previsto toodisable esta característica, tenga en cuenta que cuando se producirá un bloqueo no controlado en la aplicación, interacción no enviará bloqueo hello **AND** no cerrará sesión hello y trabajos.</span><span class="sxs-lookup"><span data-stu-id="11703-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="11703-181">bloqueo automático toodisable reporting, simplemente personalizar la configuración según la forma de Hola se declaró:</span><span class="sxs-lookup"><span data-stu-id="11703-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="11703-182">Desde el archivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="11703-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="11703-183">Establecer un informe de bloqueo demasiado`false` entre `<reportCrash>` y `</reportCrash>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="11703-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="11703-184">Desde el objeto `EngagementConfiguration` en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="11703-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="11703-185">Establecer toofalse de bloqueo de informe mediante el objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="11703-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="11703-186">Modo de ráfaga</span><span class="sxs-lookup"><span data-stu-id="11703-186">Burst mode</span></span>
<span data-ttu-id="11703-187">De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="11703-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="11703-188">Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="11703-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="11703-189">toodo por lo tanto, llame al método hello:</span><span class="sxs-lookup"><span data-stu-id="11703-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="11703-190">Hola argumento es un valor en **milisegundos**.</span><span class="sxs-lookup"><span data-stu-id="11703-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="11703-191">En cualquier momento, si desea que el registro en tiempo real de tooreactivate hello, simplemente llamar a Hola método sin parámetros o con el valor de hello 0.</span><span class="sxs-lookup"><span data-stu-id="11703-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="11703-192">Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible).</span><span class="sxs-lookup"><span data-stu-id="11703-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="11703-193">Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="11703-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="11703-194">Tendrá que toobe tenga en cuenta que los registros guardados son elementos too300 limitado.</span><span class="sxs-lookup"><span data-stu-id="11703-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="11703-195">Si el envío es demasiado largo, puede perder algunos registros.</span><span class="sxs-lookup"><span data-stu-id="11703-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="11703-196">Hello umbral de ráfaga no se puede configurar tooa período menor que un segundo.</span><span class="sxs-lookup"><span data-stu-id="11703-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="11703-197">Si intentas toodo por lo tanto, Hola SDK se muestran un seguimiento con error de Hola y configurará automáticamente y restablece toohello valor de manera predeterminada, es decir, cero segundos.</span><span class="sxs-lookup"><span data-stu-id="11703-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="11703-198">Esto desencadenará Hola SDK tooreport Hola registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="11703-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

