---
title: "aaaWindows Universal integración con el SDK de aplicaciones de interacción"
description: "¿Cómo tooIntegrate Azure Mobile Engagement con aplicaciones universales de Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="4ce7b-103">Integración del SDK de Windows Universal Apps Engagement</span><span class="sxs-lookup"><span data-stu-id="4ce7b-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ce7b-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="4ce7b-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="4ce7b-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="4ce7b-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="4ce7b-106">iOS</span><span class="sxs-lookup"><span data-stu-id="4ce7b-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="4ce7b-107">Android</span><span class="sxs-lookup"><span data-stu-id="4ce7b-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="4ce7b-108">Este procedimiento describe las funciones de la aplicación Universal de Windows de supervisión y análisis hello más sencilla forma tooactivate Engagement.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="4ce7b-109">Hola pasos es que toocompute necesita un suficiente informe de hello tooactivate de los registros de todas las estadísticas relacionadas con los usuarios, sesiones, actividades, se bloquea y Technicals.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="4ce7b-110">Hola de registros necesita un informe toocompute otras estadísticas como trabajos, errores y eventos deben realizarse manualmente mediante la API de interacción de Hola (vea [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md) desde Estas estadísticas son dependientes de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="4ce7b-111">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="4ce7b-111">Supported versions</span></span>
<span data-ttu-id="4ce7b-112">Hola Mobile Engagement SDK para aplicaciones universales de Windows solo se puede integrar en tiempo de ejecución de Windows y aplicaciones de plataforma Universal de Windows de destino:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="4ce7b-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="4ce7b-113">Windows 8</span></span>
* <span data-ttu-id="4ce7b-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="4ce7b-114">Windows 8.1</span></span>
* <span data-ttu-id="4ce7b-115">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="4ce7b-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="4ce7b-116">Windows 10 (familias de escritorio y portátiles)</span><span class="sxs-lookup"><span data-stu-id="4ce7b-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="4ce7b-117">Si se dirige a Windows Phone Silverlight, consulte toohello [procedimiento de integración de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="4ce7b-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="4ce7b-118">Instalar SDK de aplicaciones universales de Mobile Engagement Hola</span><span class="sxs-lookup"><span data-stu-id="4ce7b-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="4ce7b-119">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="4ce7b-119">All platforms</span></span>
<span data-ttu-id="4ce7b-120">Hola Mobile Engagement SDK para Windows aplicación Universal está disponible como un paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="4ce7b-121">Puede instalarlo desde Hola Administrador de paquetes de Nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="4ce7b-122">Windows 8.x y Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="4ce7b-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="4ce7b-123">NuGet implementa automáticamente los recursos SDK de Hola Hola `Resources` carpeta Hola raíz de su proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="4ce7b-124">Aplicaciones de la Plataforma universal de Windows de Windows 10</span><span class="sxs-lookup"><span data-stu-id="4ce7b-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="4ce7b-125">NuGet no implementar automáticamente los recursos SDK de hello en la aplicación de UWP todavía.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="4ce7b-126">Deberá toodo manualmente hasta que la implementación de recursos vuelve a producirse en NuGet:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="4ce7b-127">Abra el Explorador de archivos.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="4ce7b-128">Navegue toohello ubicación siguiente (**x.x.x** es la versión de hello de interacción que se va a instalar): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="4ce7b-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="4ce7b-129">Hola de arrastrar y colocar **recursos** carpeta desde la raíz del toohello explorer Hola del archivo del proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="4ce7b-130">En Visual Studio, seleccione el proyecto y activar hello **mostrar todos los archivos** icono encima de hello **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="4ce7b-131">Algunos archivos no se incluyen en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-131">Some files are not included in hello project.</span></span> <span data-ttu-id="4ce7b-132">tooimport ellos a la vez haga clic en hello **recursos** carpeta, **excluir del proyecto** otro derecho haga clic en hello **recursos** carpeta, **Include en el proyecto** toore-incluir toda la carpeta Hola.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="4ce7b-133">Todos los archivos de hello **recursos** carpeta ahora se incluyen en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="4ce7b-134">Agregar capacidades de Hola</span><span class="sxs-lookup"><span data-stu-id="4ce7b-134">Add hello capabilities</span></span>
<span data-ttu-id="4ce7b-135">Hola Engagement SDK tiene algunas capacidades de hello SDK de Windows en orden toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="4ce7b-136">Abra su `Package.appxmanifest` de archivos y asegúrese de que se declaran ese Hola siguiendo las capacidades:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="4ce7b-137">Inicializar Hola Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="4ce7b-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="4ce7b-138">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="4ce7b-138">Engagement configuration</span></span>
<span data-ttu-id="4ce7b-139">configuración de la interacción de Hello está centralizada en hello `Resources\EngagementConfiguration.xml` archivo del proyecto.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="4ce7b-140">Editar este archivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="4ce7b-141">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="4ce7b-142">Si desea que toospecify en tiempo de ejecución en su lugar, se puede llamar a siguiente Hola método antes de la inicialización de agente de interacción de hello:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="4ce7b-143">cadena de conexión de Hello para la aplicación se muestra en hello Portal clásico de Azure.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="4ce7b-144">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="4ce7b-144">Engagement initialization</span></span>
<span data-ttu-id="4ce7b-145">Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="4ce7b-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="4ce7b-146">Esta clase hereda de `Application` y contiene muchos métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="4ce7b-147">También será usado tooinitialize Hola Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="4ce7b-148">Modificar Hola `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="4ce7b-149">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="4ce7b-150">Definir una método tooshare Hola interacción la inicialización una vez para todas las llamadas:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="4ce7b-151">Llame a `InitEngagement` en hello `OnLaunched` método:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="4ce7b-152">Cuando la aplicación se inicia utilizando un esquema personalizado, a continuación, Hola otra línea de comandos de aplicación o hello `OnActivated` se llama al método.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="4ce7b-153">También debe tooinitiate Hola Engagement SDK cuando se activa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="4ce7b-154">por lo tanto, invalidar toodo `OnActivated` método:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="4ce7b-155">Se desaconseja encarecidamente tooadd Hola interacción inicialización en otro lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="4ce7b-156">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="4ce7b-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="4ce7b-157">Método recomendado: sobrecargar las clases `Page`</span><span class="sxs-lookup"><span data-stu-id="4ce7b-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="4ce7b-158">Informe de hello order tooactivate de todos los registros de hello requiere interacción toocompute usuarios, sesiones, actividades, bloqueos y las estadísticas técnicas, basta con hacer que todos los su `Page` subclases heredan de hello `EngagementPage` clases.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="4ce7b-159">Este es un ejemplo de cómo toodo esto en una página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="4ce7b-160">Puede hacer lo mismo para todas las páginas de la aplicación de Hola.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="4ce7b-161">Archivo de código fuente C#</span><span class="sxs-lookup"><span data-stu-id="4ce7b-161">C# Source file</span></span>
<span data-ttu-id="4ce7b-162">Modifique el archivo `.xaml.cs` de página:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="4ce7b-163">Agregar tooyour `using` instrucciones:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="4ce7b-164">Reemplace `Page` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="4ce7b-165">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="4ce7b-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="4ce7b-166">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="4ce7b-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="4ce7b-167">Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="4ce7b-168">En caso contrario, no se incluirán actividad hello (hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="4ce7b-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="4ce7b-169">Archivo XAML</span><span class="sxs-lookup"><span data-stu-id="4ce7b-169">XAML file</span></span>
<span data-ttu-id="4ce7b-170">Modifique el archivo `.xaml` de página:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="4ce7b-171">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="4ce7b-172">Reemplace `Page` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="4ce7b-173">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="4ce7b-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="4ce7b-174">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="4ce7b-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="4ce7b-175">Invalidar el comportamiento predeterminado de Hola</span><span class="sxs-lookup"><span data-stu-id="4ce7b-175">Override hello default behaviour</span></span>
<span data-ttu-id="4ce7b-176">De forma predeterminada, nombre de la clase de página de Hola Hola se notifica como nombre de la actividad de hello, con ningún extra.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="4ce7b-177">Si la clase hello usa el sufijo "Página" Hola, interacción, también se quitará.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="4ce7b-178">Si desea comportamiento predeterminado de toooverride Hola para nombre de hello, basta con agregar este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="4ce7b-179">Si desea tooreport algunos datos adicionales con la actividad, puede agregar este código tooyour:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="4ce7b-180">Estos métodos se invocan desde dentro de hello `OnNavigatedTo` método de la página.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="4ce7b-181">Método alternativo: llamar a `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="4ce7b-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="4ce7b-182">Si no puede o no desea que toooverload su `Page` clases, en su lugar, puede iniciar las actividades mediante una llamada a `EngagementAgent` métodos directamente.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="4ce7b-183">Se recomienda toocall `StartActivity` dentro de su `OnNavigatedTo` al método de la página.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="4ce7b-184">Asegúrese de finalizar la sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="4ce7b-185">Hola SDK Universal de Windows llama automáticamente a hello `EndActivity` método cuando se cierra la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="4ce7b-186">Por lo tanto, es **alta** recomienda hello toocall `StartActivity` método cada vez que cambia la actividad de hello del usuario de hello y demasiado**nunca** llamada hello `EndActivity` método, este método envía tooEngagement servidor que usuario actual tiene deje Hola aplicación, esta acción afecta a todos los registros de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="4ce7b-187">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="4ce7b-187">Advanced reporting</span></span>
<span data-ttu-id="4ce7b-188">Si lo desea, puede que desee eventos específicos de aplicación tooreport, errores y los trabajos y toodo por lo tanto, use otros métodos que se encuentran en Hola Hola `EngagementAgent` clase.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="4ce7b-189">Hola interacción API permite toouse todas las capacidades avanzadas de contratación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="4ce7b-190">Para obtener más información, consulte [cómo toouse Hola avanzada Mobile Engagement etiquetado API en su aplicación Universal de Windows](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="4ce7b-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="4ce7b-191">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="4ce7b-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="4ce7b-192">Deshabilitar los informes automáticos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="4ce7b-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="4ce7b-193">Puede deshabilitar Hola automática de informes de errores característica de contratación.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="4ce7b-194">A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="4ce7b-195">Si tiene previsto toodisable esta característica, tenga en cuenta que cuando se producirá un bloqueo no controlado en la aplicación, interacción no enviará bloqueo hello **AND** no se cerrará la sesión de Hola y trabajos.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="4ce7b-196">bloqueo automático toodisable reporting, simplemente personalizar la configuración según la forma de Hola se declaró:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="4ce7b-197">Desde el archivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="4ce7b-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="4ce7b-198">Establecer un informe de bloqueo demasiado`false` entre `<reportCrash>` y `</reportCrash>` etiquetas.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="4ce7b-199">Desde el objeto `EngagementConfiguration` en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="4ce7b-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="4ce7b-200">Establecer toofalse de bloqueo de informe mediante el objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="4ce7b-201">Modo de ráfaga</span><span class="sxs-lookup"><span data-stu-id="4ce7b-201">Burst mode</span></span>
<span data-ttu-id="4ce7b-202">De forma predeterminada, los registros de informes del servicio de contratación de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="4ce7b-203">Si la aplicación informa de los registros con mucha frecuencia, es mejor toobuffer Hola registros y tooreport usarlas todos a la vez en una base de tiempo regular (Esto se denomina hello "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="4ce7b-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="4ce7b-204">toodo por lo tanto, llame al método hello:</span><span class="sxs-lookup"><span data-stu-id="4ce7b-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="4ce7b-205">Hola argumento es un valor en **milisegundos**.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="4ce7b-206">En cualquier momento, si desea que el registro en tiempo real de tooreactivate hello, simplemente llamar a Hola método sin parámetros o con el valor de hello 0.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="4ce7b-207">Hello el modo de ráfaga incremente ligeramente batería Hola vida pero tiene un impacto en hello Monitor de contratación: duración de las sesiones y los trabajos de todos los será redondeado toohello ráfaga umbral (por lo tanto, las sesiones y trabajos más cortos que el umbral de ráfaga de hello puede no estar visible).</span><span class="sxs-lookup"><span data-stu-id="4ce7b-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="4ce7b-208">Es recomendable toouse ya no es un umbral de ráfaga de 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="4ce7b-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="4ce7b-209">Tendrá que toobe tenga en cuenta que los registros guardados son elementos too300 limitado.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="4ce7b-210">Si el envío es demasiado largo, puede perder algunos registros.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="4ce7b-211">umbral de ráfaga de Hello no se puede configurar tooa período anterior a 1s.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="4ce7b-212">Si intentas toodo por lo tanto, Hola SDK se muestran un seguimiento con error de Hola y configurará automáticamente y restablece valor predeterminado de toohello, es decir, 0.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="4ce7b-213">Esto desencadenará Hola SDK tooreport Hola registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="4ce7b-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

