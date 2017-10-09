---
title: aaaGet a trabajar con Windows Universal aplicaciones de Azure Mobile Engagement
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción y de análisis para aplicaciones universales de Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="51c50-103">Introducción a Azure Mobile Engagement para aplicaciones universales de Windows</span><span class="sxs-lookup"><span data-stu-id="51c50-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="51c50-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción a los usuarios toosegmented de notificaciones de una aplicación Universal de Windows.</span><span class="sxs-lookup"><span data-stu-id="51c50-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="51c50-105">Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="51c50-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="51c50-106">Creará una aplicación Windows Universal vacía que recopila datos básicos de uso de aplicaciones y recibe notificaciones push mediante el Servicio de notificaciones de Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="51c50-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="51c50-107">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="51c50-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="51c50-108">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="51c50-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51c50-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="51c50-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="51c50-110">Configuración de Mobile Engagement para su aplicación universal de Windows</span><span class="sxs-lookup"><span data-stu-id="51c50-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="51c50-111"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="51c50-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="51c50-112">Este tutorial presenta una "integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="51c50-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="51c50-113">Encontrará documentación de integración completa de Hola Hola [integración con el SDK de Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="51c50-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="51c50-114">Crear una aplicación básica con la integración de Visual Studio toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="51c50-115">Creación de un proyecto de aplicación universal de Windows</span><span class="sxs-lookup"><span data-stu-id="51c50-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="51c50-116">Hello siguientes pasos supone Hola uso de Visual Studio 2015 aunque Hola pasos son similares en versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51c50-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="51c50-117">Inicie Visual Studio y en hello **inicio** pantalla, seleccione **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="51c50-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="51c50-118">En el menú emergente de hello, seleccione **Windows** -> **Universal** -> **aplicación vacía (Windows Universal)**.</span><span class="sxs-lookup"><span data-stu-id="51c50-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="51c50-119">Rellene la aplicación hello **nombre** y **nombre de la solución**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="51c50-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="51c50-120">Ahora ha creado un proyecto de aplicación Universal de Windows en la que a continuación se integran hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="51c50-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="51c50-121">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="51c50-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="51c50-122">Instalar hello [MicrosoftAzure.MobileEngagement] paquete de Nuget en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="51c50-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="51c50-123">Si tiene como destino plataformas Windows y Windows Phone, deberá toodo esto para ambos proyectos.</span><span class="sxs-lookup"><span data-stu-id="51c50-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="51c50-124">Para Windows 8.x y Windows Phone 8.1, Hola mismos Nuget paquete lugares Hola correcto específico de la plataforma binarios en cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="51c50-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="51c50-125">Abra **Package.appxmanifest** y asegúrese de que ese Hola después capacidad agregada no existe:</span><span class="sxs-lookup"><span data-stu-id="51c50-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="51c50-126">Ahora, copie la cadena de conexión de Hola que copió anteriormente para la aplicación de interacción móvil y péguelo en hello `Resources\EngagementConfiguration.xml` archivo entre hello `<connectionString>` y `</connectionString>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="51c50-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="51c50-127">Si su aplicación va a tener como destino las plataformas Windows y Windows Phone, aun así se deben crear dos aplicaciones Mobile Engagement, una para cada plataforma compatible.</span><span class="sxs-lookup"><span data-stu-id="51c50-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="51c50-128">Existencia de dos aplicaciones garantiza que se puede crear segmentación correcta de audiencia de Hola y puede enviar notificaciones de destino de forma adecuada para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="51c50-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="51c50-129">NuGet no copia automáticamente los recursos SDK de hello en la aplicación de UWP de Windows 10.</span><span class="sxs-lookup"><span data-stu-id="51c50-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="51c50-130">Tenerla toodo manualmente siguiendo los pasos de Hola que mostrarán (readme.txt) cuando se instala el paquete de Nuget Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="51c50-131">Hola `App.xaml.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="51c50-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="51c50-132">a.</span><span class="sxs-lookup"><span data-stu-id="51c50-132">a.</span></span> <span data-ttu-id="51c50-133">Agregar hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="51c50-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="51c50-134">b.</span><span class="sxs-lookup"><span data-stu-id="51c50-134">b.</span></span> <span data-ttu-id="51c50-135">Agregue un método que inicialice Hola interacción:</span><span class="sxs-lookup"><span data-stu-id="51c50-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="51c50-136">c.</span><span class="sxs-lookup"><span data-stu-id="51c50-136">c.</span></span> <span data-ttu-id="51c50-137">Inicializar Hola SDK en hello **OnLaunched** método:</span><span class="sxs-lookup"><span data-stu-id="51c50-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="51c50-138">c.</span><span class="sxs-lookup"><span data-stu-id="51c50-138">c.</span></span> <span data-ttu-id="51c50-139">Inserte el siguiente de Hola Hola **OnActivated** método y agregue el método hello si todavía no está presente:</span><span class="sxs-lookup"><span data-stu-id="51c50-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="51c50-140"><a id="monitor"></a>Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="51c50-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="51c50-141">toostart enviando los datos y garantizar que los usuarios de hello están activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).</span><span class="sxs-lookup"><span data-stu-id="51c50-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="51c50-142">Hola **MainPage.xaml.cs**, agregue los siguientes hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="51c50-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="51c50-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="51c50-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="51c50-144">Cambiar la clase base hello de **MainPage** de **página** demasiado**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="51c50-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="51c50-145">Hola `MainPage.xaml` archivo:</span><span class="sxs-lookup"><span data-stu-id="51c50-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="51c50-146">a.</span><span class="sxs-lookup"><span data-stu-id="51c50-146">a.</span></span> <span data-ttu-id="51c50-147">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="51c50-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="51c50-148">b.</span><span class="sxs-lookup"><span data-stu-id="51c50-148">b.</span></span> <span data-ttu-id="51c50-149">Reemplace hello **página** en nombre de etiqueta XML de hello con **interacción: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="51c50-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51c50-150">Si la página invalida hello `OnNavigatedTo` método, ser seguro toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="51c50-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="51c50-151">En caso contrario, no se notifica la actividad hello `EngagementPage` llamadas `StartActivity` dentro de su `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="51c50-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="51c50-152">Esto es especialmente importante en un proyecto de Windows Phone que no tiene plantilla predeterminada de hello un `OnNavigatedTo` método.</span><span class="sxs-lookup"><span data-stu-id="51c50-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="51c50-153">Para **aplicaciones universales de Windows 10**, utilice método hello recomendada Hola "método recomendado: sobrecargar las clases de página" sección de [avanzada Reporting con SDK de interacción de aplicaciones Universal de Windows hello](mobile-engagement-windows-store-advanced-reporting.md) , en lugar de hello uno mencionadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="51c50-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="51c50-154"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="51c50-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="51c50-155"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="51c50-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="51c50-156">Mobile Engagement le permite toointeract y llegar a los usuarios con las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="51c50-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="51c50-157">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="51c50-158">Hello las secciones siguientes configure su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="51c50-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="51c50-159">Habilitar la tooreceive de la aplicación notificaciones de inserción de WNS</span><span class="sxs-lookup"><span data-stu-id="51c50-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="51c50-160">Hola `Package.appxmanifest` archivo Hola **aplicación** ficha **notificaciones**, establezca **capacidad de aviso:** demasiado**sí**</span><span class="sxs-lookup"><span data-stu-id="51c50-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="51c50-161">Inicializar Hola REACH SDK</span><span class="sxs-lookup"><span data-stu-id="51c50-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="51c50-162">En `App.xaml.cs`, llame a **EngagementReach.Instance.Init(e);** en hello **InitEngagement** función justo después de la inicialización del agente de hello:</span><span class="sxs-lookup"><span data-stu-id="51c50-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="51c50-163">Ya está listo toosend una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="51c50-163">You're ready toosend a toast.</span></span> <span data-ttu-id="51c50-164">Ahora comprobaremos que ha llevado a cabo correctamente esta integración básica.</span><span class="sxs-lookup"><span data-stu-id="51c50-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="51c50-165">Conceder acceso tooMobile interacción toosend notificaciones</span><span class="sxs-lookup"><span data-stu-id="51c50-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="51c50-166">Abra el [Centro de desarrollo de Tienda Windows] en el explorador web, inicie sesión y cree una cuenta, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="51c50-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="51c50-167">Haga clic en **panel** en hello parte superior derecha de las esquinas y, a continuación, haga clic en **crear una nueva aplicación** en el menú del panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="51c50-168">Cree la aplicación mediante la reserva de su nombre.</span><span class="sxs-lookup"><span data-stu-id="51c50-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="51c50-169">Una vez creada la aplicación hello, navegue demasiado**servicios -> notificaciones de inserción** desde el menú de la izquierda Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="51c50-170">Hola sección notificaciones de inserción, haga clic en hello **sitio de los servicios de Live** vínculo.</span><span class="sxs-lookup"><span data-stu-id="51c50-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="51c50-171">Navegue toohello sección de credenciales de inserción.</span><span class="sxs-lookup"><span data-stu-id="51c50-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="51c50-172">Asegúrese de que se encuentre en hello **configuración de la aplicación** sección y, a continuación, copie su **SID del paquete** y **secreto de cliente**</span><span class="sxs-lookup"><span data-stu-id="51c50-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="51c50-173">Navegue toohello **configuración** de portal de interacción móvil y haga clic en hello **inserción nativa** sección Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="51c50-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="51c50-174">A continuación, haga clic en hello **editar** tooenter botón su **identificador de seguridad (SID) de paquete** y su **clave secreta** tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="51c50-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="51c50-175">Por último, asegúrese de que la aplicación de Visual Studio se ha asociado con esta aplicación creada en la tienda de aplicaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="51c50-176">Haga clic en **Asociar aplicación con la Tienda** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="51c50-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="51c50-177"><a id="send"></a>Enviar una aplicación de tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="51c50-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="51c50-178">Si está ejecutando la aplicación hello, verá una notificación en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="51c50-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="51c50-179">en caso contrario, si se cierra la aplicación hello, verá una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="51c50-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="51c50-180">Si aparece una notificación en la aplicación pero no una notificación del sistema y está ejecutando la aplicación hello en modo de depuración en Visual Studio, vuelva a intentar **eventos de ciclo de vida -> Suspender** en tooensure de barra de herramientas de Hola se suspende esa aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="51c50-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="51c50-181">Si hace clic en botón de inicio de hello mientras se depura la aplicación hello en Visual Studio, a continuación, no siempre suspendido y mientras ve notificación hello como en la aplicación, no se muestre como una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="51c50-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centro de desarrollo de Tienda Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
