---
title: "Integración del SDK de Windows Phone Silverlight Engagement"
description: "Cómo integrar Azure Mobile Engagement con aplicaciones Windows Phone Silverlight"
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
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="1f2ef-103">Integración del SDK de Windows Phone Silverlight Engagement</span><span class="sxs-lookup"><span data-stu-id="1f2ef-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f2ef-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="1f2ef-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="1f2ef-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1f2ef-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="1f2ef-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1f2ef-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="1f2ef-107">Android</span><span class="sxs-lookup"><span data-stu-id="1f2ef-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="1f2ef-108">En este procedimiento se describe la manera más sencilla de activar las funciones de análisis y supervisión de Azure Mobile Engagement en su aplicación de Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="1f2ef-109">Los siguientes pasos son suficientes para activar el informe de los registros necesarios para calcular todas las estadísticas en relación con los usuarios, las sesiones, las actividades, los bloqueos y los aspectos técnicos.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="1f2ef-110">El informe de los registros necesarios para calcular otras estadísticas, como eventos, errores y trabajos debe realizarse manualmente mediante la API de Engagement (vea [Cómo usar la API de Engagement en Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) a continuación) debido a que estas estadísticas dependen de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="1f2ef-111">Versiones compatibles</span><span class="sxs-lookup"><span data-stu-id="1f2ef-111">Supported versions</span></span>
<span data-ttu-id="1f2ef-112">El SDK de Mobile Engagement para Windows Silverlight solo se puede integrar en las aplicaciones destinadas a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="1f2ef-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="1f2ef-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="1f2ef-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="1f2ef-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="1f2ef-115">Si va a desarrollar para Windows Phone 8.1 (no Silverlight), consulte entonces el [procedimiento de integración de Windows Universal](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="1f2ef-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="1f2ef-116">Instale el SDK de Mobile Engagement Silverlight</span><span class="sxs-lookup"><span data-stu-id="1f2ef-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="1f2ef-117">El SDK de Mobile Engagement para Windows Silverlight está disponible como un paquete de Nuget llamado *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="1f2ef-118">Puede instalarlo desde el Administrador de paquetes nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="1f2ef-119">Agregar las capacidades</span><span class="sxs-lookup"><span data-stu-id="1f2ef-119">Add the capabilities</span></span>
<span data-ttu-id="1f2ef-120">El SDK de Engagement necesita algunas capacidades del SDK de Windows Phone Silverlight para que funcione correctamente.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="1f2ef-121">Abra el archivo `WMAppManifest.xml` y asegúrese de que en el panel `Capabilities` se han declarado las siguientes capacidades:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="1f2ef-122">Inicializar el SDK de Engagement</span><span class="sxs-lookup"><span data-stu-id="1f2ef-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="1f2ef-123">Configuración de Engagement</span><span class="sxs-lookup"><span data-stu-id="1f2ef-123">Engagement configuration</span></span>
<span data-ttu-id="1f2ef-124">La configuración de Engagement se centraliza en el archivo `Resources\EngagementConfiguration.xml` del proyecto.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="1f2ef-125">Edite este archivo para especificar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-125">Edit this file to specify :</span></span>

* <span data-ttu-id="1f2ef-126">La cadena de conexión de la aplicación entre las etiquetas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="1f2ef-127">Si desea especificarla en tiempo de ejecución, puede llamar al método siguiente antes de la inicialización del agente de Engagement:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="1f2ef-128">La cadena de conexión de la aplicación se muestra en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="1f2ef-129">Inicialización de Engagement</span><span class="sxs-lookup"><span data-stu-id="1f2ef-129">Engagement initialization</span></span>
<span data-ttu-id="1f2ef-130">Al crear un nuevo proyecto, se genera un archivo `App.xaml.cs` .</span><span class="sxs-lookup"><span data-stu-id="1f2ef-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="1f2ef-131">Esta clase hereda de `Application` y contiene muchos métodos importantes.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="1f2ef-132">También se usará para inicializar el SDK de Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="1f2ef-133">Modifique `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="1f2ef-134">Agregue las instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="1f2ef-135">Inserte `EngagementAgent.Instance.Init` en el método `Application_Launching`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="1f2ef-136">Inserte `EngagementAgent.Instance.OnActivated` en el método `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="1f2ef-137">Se desaconseja encarecidamente agregar la inicialización de Engagement en otro lugar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="1f2ef-138">Sin embargo, tenga en cuenta que el método `EngagementAgent.Instance.Init` se ejecuta en un subproceso dedicado y no en el subproceso de la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="1f2ef-139">Informes básicos</span><span class="sxs-lookup"><span data-stu-id="1f2ef-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="1f2ef-140">Método recomendado: sobrecargar las clases `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="1f2ef-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="1f2ef-141">Para activar el informe de todos los registros que Engagement necesita para calcular las estadísticas de usuarios, sesiones, actividades, bloqueos y aspectos técnicos, puede hacer que todas las subclases `PhoneApplicationPage` hereden de las clases `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="1f2ef-142">Este es un ejemplo de cómo hacer esto para una página de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="1f2ef-143">Puede hacer lo mismo para todas las páginas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="1f2ef-144">Archivo de código fuente C#</span><span class="sxs-lookup"><span data-stu-id="1f2ef-144">C# Source file</span></span>
<span data-ttu-id="1f2ef-145">Modifique el archivo `.xaml.cs` de página:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="1f2ef-146">Agregue las instrucciones `using`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="1f2ef-147">Reemplace `PhoneApplicationPage` por `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="1f2ef-148">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1f2ef-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="1f2ef-149">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1f2ef-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="1f2ef-150">Si la página hereda del método `OnNavigatedTo`, asegúrese de permitir la llamada `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="1f2ef-151">De lo contrario, no se informará la actividad.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="1f2ef-152">De hecho, `EngagementPage` llama a `StartActivity` dentro del método `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="1f2ef-153">Archivo XAML</span><span class="sxs-lookup"><span data-stu-id="1f2ef-153">XAML file</span></span>
<span data-ttu-id="1f2ef-154">Modifique el archivo `.xaml` de página:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="1f2ef-155">Agregue a las declaraciones de espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="1f2ef-156">Reemplace `phone:PhoneApplicationPage` por `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="1f2ef-157">**Sin Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1f2ef-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="1f2ef-158">**Con Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1f2ef-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="1f2ef-159">Invalidar el comportamiento predeterminado</span><span class="sxs-lookup"><span data-stu-id="1f2ef-159">Override the default behavior</span></span>
<span data-ttu-id="1f2ef-160">De forma predeterminada, el nombre de clase de la página se informa como el nombre de actividad, sin más.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="1f2ef-161">Si la clase usa el sufijo "Página", Engagement también la quitará.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="1f2ef-162">Si desea invalidar el comportamiento predeterminado para el nombre, simplemente agregue lo siguiente a su código:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="1f2ef-163">Si desea informar algunos datos adicionales con su actividad, puede agregar lo siguiente a su código:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="1f2ef-164">Estos métodos se invocan desde el método `OnNavigatedTo` de la página.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="1f2ef-165">Método alternativo: llamar a `StartActivity()` manualmente</span><span class="sxs-lookup"><span data-stu-id="1f2ef-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="1f2ef-166">Si no puede o no quiere sobrecargar las clases `PhoneApplicationPage`, en su lugar, puede iniciar las actividades mediante una llamada directa a los métodos `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="1f2ef-167">Recomendamos que llame a `StartActivity` dentro del método `OnNavigatedTo` de su PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="1f2ef-168">Asegúrese de finalizar la sesión correctamente.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="1f2ef-169">El SDK de iOS llama automáticamente al método `EndActivity` cuando se cierra la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="1f2ef-170">Por lo tanto, es **MUY** recomendable llamar al método `StartActivity` cada vez que cambie la actividad del usuario y no llamar **NUNCA** al método `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="1f2ef-171">Este método envía un mensaje al servidor de Engagement indicando que el usuario actual ha salido de la aplicación, lo que afecta a todos los registros de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="1f2ef-172">Informes avanzados</span><span class="sxs-lookup"><span data-stu-id="1f2ef-172">Advanced reporting</span></span>
<span data-ttu-id="1f2ef-173">Opcionalmente, es aconsejable informar eventos, errores y trabajos de aplicación específicos. Para ello, use los otros métodos que se encuentran en la clase `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="1f2ef-174">La API de Engagement permite usar todas las capacidades avanzadas de Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="1f2ef-175">Para obtener más información, consulte [Cómo usar la API de etiquetado avanzado de Mobile Engagement en la aplicación de Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="1f2ef-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="1f2ef-176">Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="1f2ef-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="1f2ef-177">Deshabilitar los informes automáticos de bloqueo</span><span class="sxs-lookup"><span data-stu-id="1f2ef-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="1f2ef-178">Puede deshabilitar la característica de informes automáticos de bloqueo de Engagement.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="1f2ef-179">A continuación, cuando se produce una excepción no controlada, Engagement no hará nada.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="1f2ef-180">Si tiene previsto deshabilitar esta característica, tenga en cuenta que cuando se produzca un error no controlado en la aplicación, Engagement no enviará la información del bloqueo **NI** tampoco cerrará la sesión ni los trabajos.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="1f2ef-181">Para deshabilitar los informes automáticos de bloqueo, personalice la configuración según la manera en que la declaró:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="1f2ef-182">Desde el archivo `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="1f2ef-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="1f2ef-183">Establezca el informe de bloqueo en `false` entre las etiquetas `<reportCrash>` y `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="1f2ef-184">Desde el objeto `EngagementConfiguration` en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="1f2ef-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="1f2ef-185">Establezca el informe de bloqueo mediante el objeto EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="1f2ef-186">Modo de ráfaga</span><span class="sxs-lookup"><span data-stu-id="1f2ef-186">Burst mode</span></span>
<span data-ttu-id="1f2ef-187">De forma predeterminada, el servicio de Engagement informa los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="1f2ef-188">Si la aplicación informa los registros con mucha frecuencia, es mejor almacenar los registros en el búfer e informarlos todos a la vez de forma periódica (esto se denomina "modo de ráfaga").</span><span class="sxs-lookup"><span data-stu-id="1f2ef-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="1f2ef-189">Para ello, llame al método siguiente:</span><span class="sxs-lookup"><span data-stu-id="1f2ef-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="1f2ef-190">El argumento es un valor en **milisegundos**.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="1f2ef-191">En cualquier momento, si desea volver a activar el registro en tiempo real, simplemente llame al método sin ningún parámetro o con el valor 0.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="1f2ef-192">El modo de ráfaga aumenta ligeramente la duración de la batería, pero afecta al monitor de Engagement: la duración de todas las sesiones y trabajos se redondeará al umbral de ráfaga (por lo tanto, es posible que las sesiones y los trabajos más cortos que el umbral de ráfaga no sean visibles).</span><span class="sxs-lookup"><span data-stu-id="1f2ef-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="1f2ef-193">Se recomienda usar un umbral de ráfaga inferior a 30.000 (30 segundos).</span><span class="sxs-lookup"><span data-stu-id="1f2ef-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="1f2ef-194">Tenga en cuenta que los registros guardados se limitan a 300 elementos.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="1f2ef-195">Si el envío es demasiado largo, puede perder algunos registros.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="1f2ef-196">El umbral de ráfaga no se puede configurar en un período inferior a un segundo.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="1f2ef-197">Si intenta hacerlo, el SDK mostrará un seguimiento con el error y se restablecerá automáticamente en el valor predeterminado; es decir, cero segundos.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="1f2ef-198">Esto hará que el SDK informe los registros en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="1f2ef-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

