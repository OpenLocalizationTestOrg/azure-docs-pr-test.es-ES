---
title: "Integración del SDK de Windows Universal Apps Engagement"
description: "Cómo integrar Azure Mobile Engagement con aplicaciones Windows Universal"
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
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="03ec0-103">Integración del SDK de Windows Universal Apps Engagement</span><span class="sxs-lookup"><span data-stu-id="03ec0-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="03ec0-104">Windows universal</span><span class="sxs-lookup"><span data-stu-id="03ec0-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="03ec0-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="03ec0-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="03ec0-106">iOS</span><span class="sxs-lookup"><span data-stu-id="03ec0-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="03ec0-107">Android</span><span class="sxs-lookup"><span data-stu-id="03ec0-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="03ec0-108">En este procedimiento se describe la manera más sencilla de activar las funciones de análisis y supervisión de Engagement en su aplicación de Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="03ec0-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="03ec0-109">Los siguientes pasos son suficientes para activar el informe de los registros necesarios para calcular todas las estadísticas en relación con los usuarios, las sesiones, las actividades, los bloqueos y los aspectos técnicos.</span><span class="sxs-lookup"><span data-stu-id="03ec0-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="03ec0-110">El informe de los registros necesarios para calcular otras estadísticas, como eventos, errores y trabajos debe realizarse manualmente mediante la API de Engagement (vea [Cómo usar la API de etiquetado avanzado de Mobile Engagement en la aplicación de Windows Universal](mobile-engagement-windows-store-use-engagement-api.md) ) debido a que estas estadísticas dependen de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="03ec0-111">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="03ec0-111">Supported versions</span></span>
<span data-ttu-id="03ec0-112">El SDK de Mobile Engagement para aplicaciones Windows Universal solo se puede integrar en las aplicaciones Windows en tiempo de ejecución y aplicaciones de Plataforma universal de Windows destinadas a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="03ec0-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="03ec0-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="03ec0-113">Windows 8</span></span>
* <span data-ttu-id="03ec0-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="03ec0-114">Windows 8.1</span></span>
* <span data-ttu-id="03ec0-115">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="03ec0-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="03ec0-116">Windows 10 (familias de escritorio y portátiles)</span><span class="sxs-lookup"><span data-stu-id="03ec0-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="03ec0-117">Si va a desarrollar para Windows Phone Silverlight, vea entonces el [procedimiento de integración de Windows Universal Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="03ec0-117">If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="03ec0-118">Instale el SDK de aplicaciones Mobile Engagement Universal</span><span class="sxs-lookup"><span data-stu-id="03ec0-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="03ec0-119">Todas las plataformas</span><span class="sxs-lookup"><span data-stu-id="03ec0-119">All platforms</span></span>
<span data-ttu-id="03ec0-120">El SDK de Mobile Engagement para la aplicación Windows Universal está disponible como paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="03ec0-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="03ec0-121">Puede instalarlo desde el Administrador de paquetes nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03ec0-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="03ec0-122">Windows 8.x y Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="03ec0-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="03ec0-123">NuGet implementa automáticamente los recursos SDK en la carpeta `Resources` en la raíz de su proyecto de aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="03ec0-124">Aplicaciones de la Plataforma universal de Windows de Windows 10</span><span class="sxs-lookup"><span data-stu-id="03ec0-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="03ec0-125">NuGet no implementa automáticamente los recursos SDK en su aplicación UWP todavía.</span><span class="sxs-lookup"><span data-stu-id="03ec0-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="03ec0-126">Tiene que hacerlo manualmente hasta que la implementación de recursos se vuelva a insertar en NuGet:</span><span class="sxs-lookup"><span data-stu-id="03ec0-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="03ec0-127">Abra el Explorador de archivos.</span><span class="sxs-lookup"><span data-stu-id="03ec0-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="03ec0-128">Vaya a la siguiente ubicación (**x.x.x** es la versión de Engagement que está instalando): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="03ec0-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="03ec0-129">Arrastre y coloque la carpeta **Recursos** del explorador de archivos en la raíz del proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="03ec0-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="03ec0-130">En Visual Studio, seleccione el proyecto y active el icono **Mostrar todos los archivos** en la parte superior del **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="03ec0-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="03ec0-131">Algunos archivos no se incluyen en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="03ec0-131">Some files are not included in the project.</span></span> <span data-ttu-id="03ec0-132">Para importarlos a la vez, haga clic con el botón derecho en la carpeta **Recursos**, **Excluir del proyecto** y, a continuación, haga clic de nuevo con el botón derecho en la carpeta **Recursos**, **Incluir en el proyecto** para volver a incluir toda la carpeta.</span><span class="sxs-lookup"><span data-stu-id="03ec0-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="03ec0-133">Todos los archivos de la carpeta **Recursos** estarán ahora incluidos en su proyecto.</span><span class="sxs-lookup"><span data-stu-id="03ec0-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="03ec0-134">Agregar las capacidades</span><span class="sxs-lookup"><span data-stu-id="03ec0-134">Add the capabilities</span></span>
<span data-ttu-id="03ec0-135">El SDK de Engagement necesita algunas capacidades del SDK de Windows para que funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="03ec0-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="03ec0-136">Abra el archivo `Package.appxmanifest` y asegúrese de que en el panel se han declarado las siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="03ec0-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="03ec0-137">Inicializar el SDK de Engagement</span><span class="sxs-lookup"><span data-stu-id="03ec0-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="03ec0-138">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="03ec0-138">Engagement configuration</span></span>
<span data-ttu-id="03ec0-139">La configuración de Engagement se centraliza en el archivo `Resources\EngagementConfiguration.xml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="03ec0-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="03ec0-140">Edite este archivo para especificar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="03ec0-140">Edit this file to specify:</span></span>

* <span data-ttu-id="03ec0-141">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="03ec0-142">Si desea especificarla en tiempo de ejecución, puede llamar al método siguiente antes de la inicialización del agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="03ec0-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="03ec0-143">La cadena de conexión de la aplicación se muestra en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="03ec0-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="03ec0-144">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="03ec0-144">Engagement initialization</span></span>
<span data-ttu-id="03ec0-145">Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="03ec0-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="03ec0-146">Esta clase hereda de `Application` y contiene muchos métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="03ec0-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="03ec0-147">También se usará para inicializar el SDK de Engagement.</span><span class="sxs-lookup"><span data-stu-id="03ec0-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="03ec0-148">Modifique `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="03ec0-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="03ec0-149">Agregue las instrucciones `using` :</span><span class="sxs-lookup"><span data-stu-id="03ec0-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="03ec0-150">Defina un método para compartir la inicialización de Engagement una vez para todas las llamadas:</span><span class="sxs-lookup"><span data-stu-id="03ec0-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="03ec0-151">Llame a `InitEngagement` en el método `OnLaunched`:</span><span class="sxs-lookup"><span data-stu-id="03ec0-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="03ec0-152">Cuando la aplicación se inicia mediante un esquema personalizado, otra aplicación o la línea de comandos, se llama al método `OnActivated`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="03ec0-153">También debe iniciar el SDK de Engagement cuando se activa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="03ec0-154">Para ello, invalide el método `OnActivated` :</span><span class="sxs-lookup"><span data-stu-id="03ec0-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="03ec0-155">Se desaconseja encarecidamente agregar la inicialización de Engagement en otro lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-155">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="03ec0-156">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="03ec0-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="03ec0-157">Método recomendado: sobrecargar las clases `Page`</span><span class="sxs-lookup"><span data-stu-id="03ec0-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="03ec0-158">Para activar el informe de todos los registros que Engagement necesita para calcular las estadísticas de usuarios, sesiones, actividades, bloqueos y aspectos técnicos, puede hacer que todas las subclases `Page` hereden de las clases `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="03ec0-159">Este es un ejemplo de cómo hacer esto para una página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="03ec0-160">Puede hacer lo mismo para todas las páginas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="03ec0-161">Archivo de código fuente C#</span><span class="sxs-lookup"><span data-stu-id="03ec0-161">C# Source file</span></span>
<span data-ttu-id="03ec0-162">Modifique el archivo `.xaml.cs` de página:</span><span class="sxs-lookup"><span data-stu-id="03ec0-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="03ec0-163">Agregue las instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="03ec0-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="03ec0-164">Reemplace `Page` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="03ec0-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="03ec0-165">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="03ec0-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="03ec0-166">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="03ec0-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="03ec0-167">Si la página invalida el método `OnNavigatedTo`, no olvide llamar a `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-167">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="03ec0-168">De lo contrario, no se informará de la actividad (`EngagementPage` llama a `StartActivity` en su método `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="03ec0-168">Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="03ec0-169">Archivo XAML</span><span class="sxs-lookup"><span data-stu-id="03ec0-169">XAML file</span></span>
<span data-ttu-id="03ec0-170">Modifique el archivo `.xaml` de página:</span><span class="sxs-lookup"><span data-stu-id="03ec0-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="03ec0-171">Agregue a las declaraciones de espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="03ec0-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="03ec0-172">Reemplace `Page` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="03ec0-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="03ec0-173">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="03ec0-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="03ec0-174">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="03ec0-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="03ec0-175">Invalidar el comportamiento predeterminado</span><span class="sxs-lookup"><span data-stu-id="03ec0-175">Override the default behaviour</span></span>
<span data-ttu-id="03ec0-176">De forma predeterminada, el nombre de clase de la página se informa como el nombre de actividad, sin más.</span><span class="sxs-lookup"><span data-stu-id="03ec0-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="03ec0-177">Si la clase usa el sufijo "Página", Engagement también la quitará.</span><span class="sxs-lookup"><span data-stu-id="03ec0-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="03ec0-178">Si desea invalidar el comportamiento predeterminado para el nombre, simplemente agregue lo siguiente a su código:</span><span class="sxs-lookup"><span data-stu-id="03ec0-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="03ec0-179">Si desea informar algunos datos adicionales con su actividad, puede agregar lo siguiente a su código:</span><span class="sxs-lookup"><span data-stu-id="03ec0-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="03ec0-180">Estos métodos se invocan desde el método `OnNavigatedTo` de la página.</span><span class="sxs-lookup"><span data-stu-id="03ec0-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="03ec0-181">Método alternativo: llamar a `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="03ec0-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="03ec0-182">Si no puede o no quiere sobrecargar las clases `Page`, en su lugar, puede iniciar las actividades mediante una llamada directa a los métodos `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="03ec0-183">Recomendamos que llame a `StartActivity` dentro del método `OnNavigatedTo` de su página.</span><span class="sxs-lookup"><span data-stu-id="03ec0-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="03ec0-184">Asegúrese de finalizar la sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="03ec0-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="03ec0-185">El SDK de Windows Universal llama automáticamente al método `EndActivity` cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-185">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="03ec0-186">Por lo tanto, es **MUY** recomendable llamar al método `StartActivity` cada vez que cambie la actividad del usuario y no llamar **NUNCA** al método `EndActivity`. Este método envía un mensaje al servidor de Engagement indicando que el usuario actual ha salido de la aplicación, lo que afecta a todos los registros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="03ec0-186">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="03ec0-187">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="03ec0-187">Advanced reporting</span></span>
<span data-ttu-id="03ec0-188">Opcionalmente, es aconsejable informar eventos, errores y trabajos de aplicación específicos. Para ello, use los otros métodos que se encuentran en la clase `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="03ec0-189">La API de Engagement permite usar todas las capacidades avanzadas de Engagement.</span><span class="sxs-lookup"><span data-stu-id="03ec0-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="03ec0-190">Para obtener más información, consulte [Cómo usar la API de etiquetado avanzado de Mobile Engagement en la aplicación Windows Universal](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="03ec0-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="03ec0-191">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="03ec0-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="03ec0-192">Deshabilitar los informes automáticos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="03ec0-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="03ec0-193">Puede deshabilitar la característica de informes automáticos de bloqueo de Engagement.</span><span class="sxs-lookup"><span data-stu-id="03ec0-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="03ec0-194">A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.</span><span class="sxs-lookup"><span data-stu-id="03ec0-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="03ec0-195">Si tiene previsto deshabilitar esta característica, tenga en cuenta que cuando se produzca un error no controlado en la aplicación, Engagement no enviará la información del bloqueo **NI** tampoco cerrará la sesión ni los trabajos.</span><span class="sxs-lookup"><span data-stu-id="03ec0-195">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="03ec0-196">Para deshabilitar los informes automáticos de bloqueo, personalice la configuración según la manera en que la declaró:</span><span class="sxs-lookup"><span data-stu-id="03ec0-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="03ec0-197">Desde el archivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="03ec0-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="03ec0-198">Establezca el informe de bloqueo en `false` entre las etiquetas `<reportCrash>` y `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="03ec0-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="03ec0-199">Desde el objeto `EngagementConfiguration` en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="03ec0-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="03ec0-200">Establezca el informe de bloqueo mediante el objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="03ec0-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="03ec0-201">Modo de ráfaga</span><span class="sxs-lookup"><span data-stu-id="03ec0-201">Burst mode</span></span>
<span data-ttu-id="03ec0-202">De forma predeterminada, el servicio de Engagement informa los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="03ec0-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="03ec0-203">Si la aplicación informa los registros con mucha frecuencia, es mejor almacenar los registros en el búfer e informarlos todos a la vez de forma periódica (esto se denomina "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="03ec0-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="03ec0-204">Para ello, llame al método siguiente:</span><span class="sxs-lookup"><span data-stu-id="03ec0-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="03ec0-205">El argumento es un valor en **milisegundos**.</span><span class="sxs-lookup"><span data-stu-id="03ec0-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="03ec0-206">En cualquier momento, si desea volver a activar el registro en tiempo real, simplemente llame al método sin ningún parámetro o con el valor 0.</span><span class="sxs-lookup"><span data-stu-id="03ec0-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="03ec0-207">El modo de ráfaga aumenta ligeramente la duración de la batería, pero afecta al monitor de Engagement: la duración de todas las sesiones y trabajos se redondeará al umbral de ráfaga (por lo tanto, es posible que las sesiones y los trabajos más cortos que el umbral de ráfaga no sean visibles).</span><span class="sxs-lookup"><span data-stu-id="03ec0-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="03ec0-208">Se recomienda usar un umbral de ráfaga inferior a 30.000 (30 segundos).</span><span class="sxs-lookup"><span data-stu-id="03ec0-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="03ec0-209">Tenga en cuenta que los registros guardados se limitan a 300 elementos.</span><span class="sxs-lookup"><span data-stu-id="03ec0-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="03ec0-210">Si el envío es demasiado largo, puede perder algunos registros.</span><span class="sxs-lookup"><span data-stu-id="03ec0-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="03ec0-211">El umbral de ráfaga no se puede configurar en un período inferior a un segundo.</span><span class="sxs-lookup"><span data-stu-id="03ec0-211">The burst threshold cannot be configured to a period lesser than 1s.</span></span> <span data-ttu-id="03ec0-212">Si intenta hacerlo, el SDK mostrará un seguimiento con el error y se restablecerá automáticamente en el valor predeterminado; es decir, cero segundos.</span><span class="sxs-lookup"><span data-stu-id="03ec0-212">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s.</span></span> <span data-ttu-id="03ec0-213">Esto hará que el SDK informe los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="03ec0-213">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

