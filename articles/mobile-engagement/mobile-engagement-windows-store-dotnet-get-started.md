---
title: "Introducción a Azure Mobile Engagement para aplicaciones universales de Windows"
description: "Aprenda a usar Azure Mobile Engagement con análisis y notificaciones push para aplicaciones universales de Windows."
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
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="e554e-103">Introducción a Azure Mobile Engagement para aplicaciones universales de Windows</span><span class="sxs-lookup"><span data-stu-id="e554e-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e554e-104">En este tema se muestra cómo usar Azure Mobile Engagement para comprender el uso que hace de las aplicaciones y enviar notificaciones push a los usuarios segmentados de una aplicación Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="e554e-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="e554e-105">En este tutorial se demuestra el escenario de difusión sencillo con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e554e-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="e554e-106">Creará una aplicación Windows Universal vacía que recopila datos básicos de uso de aplicaciones y recibe notificaciones push mediante el Servicio de notificaciones de Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="e554e-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="e554e-107">El servicio Azure Mobile Engagement se retirará en marzo de 2018 y actualmente solo está disponible para los clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="e554e-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="e554e-108">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="e554e-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e554e-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e554e-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="e554e-110">Configuración de Mobile Engagement para su aplicación universal de Windows</span><span class="sxs-lookup"><span data-stu-id="e554e-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e554e-111"><a id="connecting-app"></a>Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e554e-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="e554e-112">En este tutorial se presenta una "integración básica", que es el conjunto mínimo necesario para recopilar los datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="e554e-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="e554e-113">Toda la documentación de integración se encuentra en la [Integración del SDK de Windows Universal para Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e554e-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="e554e-114">Crearemos una aplicación básica con Visual Studio para demostrar la integración.</span><span class="sxs-lookup"><span data-stu-id="e554e-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="e554e-115">Creación de un proyecto de aplicación universal de Windows</span><span class="sxs-lookup"><span data-stu-id="e554e-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="e554e-116">En los siguientes pasos se supone el uso de Visual Studio de 2015 aunque los pasos son similares en versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e554e-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="e554e-117">Inicie Visual Studio y, en la pantalla **principal**, seleccione **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e554e-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="e554e-118">En el menú emergente, seleccione **Windows** -> **Universal** -> **Aplicación vacía** (Windows universal).</span><span class="sxs-lookup"><span data-stu-id="e554e-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="e554e-119">Rellene los campos **Nombre de la aplicación** y **Nombre de la solución** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e554e-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="e554e-120">Ahora ha creado un nuevo proyecto de aplicación universal de Windows en el que se integrará el SDK de Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e554e-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="e554e-121">Conectar la aplicación al back-end de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e554e-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="e554e-122">Instale el paquete de NuGet [MicrosoftAzure.MobileEngagement] en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="e554e-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="e554e-123">Si quiere usar las plataformas Windows y Windows Phone, necesitará hacer esto para los dos proyectos.</span><span class="sxs-lookup"><span data-stu-id="e554e-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="e554e-124">En Windows 8.x y Windows Phone 8.1, el mismo paquete de Nuget coloca los archivos binarios específicos de la plataforma correctos en cada proyecto.</span><span class="sxs-lookup"><span data-stu-id="e554e-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="e554e-125">Abra **Package.appxmanifest** y asegúrese de que la siguiente se agrega a él:</span><span class="sxs-lookup"><span data-stu-id="e554e-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="e554e-126">Ahora, copie la cadena de conexión que copió anteriormente para la aplicación Mobile Engagement y péguela en el archivo `Resources\EngagementConfiguration.xml`, entre las etiquetas `<connectionString>` y `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="e554e-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="e554e-127">Si su aplicación va a tener como destino las plataformas Windows y Windows Phone, aun así se deben crear dos aplicaciones Mobile Engagement, una para cada plataforma compatible.</span><span class="sxs-lookup"><span data-stu-id="e554e-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="e554e-128">De esta forma se garantiza que puede crear una segmentación correcta de la audiencia y que puede enviar notificaciones de destino de forma adecuada para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="e554e-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e554e-129">NuGet no copia automáticamente los recursos SDK en su aplicación de Windows 10 UWP.</span><span class="sxs-lookup"><span data-stu-id="e554e-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="e554e-130">Tendrá que hacerlo manualmente siguiendo los pasos que aparecen cuando se instala el paquete Nuget (readme.txt).</span><span class="sxs-lookup"><span data-stu-id="e554e-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="e554e-131">En el archivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="e554e-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="e554e-132">a.</span><span class="sxs-lookup"><span data-stu-id="e554e-132">a.</span></span> <span data-ttu-id="e554e-133">Agregue la instrucción `using`:</span><span class="sxs-lookup"><span data-stu-id="e554e-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="e554e-134">b.</span><span class="sxs-lookup"><span data-stu-id="e554e-134">b.</span></span> <span data-ttu-id="e554e-135">Agregue un método que inicialice Engagement:</span><span class="sxs-lookup"><span data-stu-id="e554e-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="e554e-136">c.</span><span class="sxs-lookup"><span data-stu-id="e554e-136">c.</span></span> <span data-ttu-id="e554e-137">Inicialice el SDK del método **OnLaunched** :</span><span class="sxs-lookup"><span data-stu-id="e554e-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="e554e-138">c.</span><span class="sxs-lookup"><span data-stu-id="e554e-138">c.</span></span> <span data-ttu-id="e554e-139">Inserte el siguiente código en el método **OnActivated** y agregue el método si aún no está presente:</span><span class="sxs-lookup"><span data-stu-id="e554e-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="e554e-140"><a id="monitor"></a>Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="e554e-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="e554e-141">Para comenzar a enviar datos y asegurarse de que los usuarios estén activos, debe enviar al menos una pantalla (Actividad) al back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e554e-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="e554e-142">En **MainPage.xaml.cs**, agregue la siguiente instrucción `using`:</span><span class="sxs-lookup"><span data-stu-id="e554e-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="e554e-143">using Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="e554e-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="e554e-144">Cambie la clase base de **MainPage** de **Page** a **EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="e554e-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="e554e-145">En el archivo `MainPage.xaml`:</span><span class="sxs-lookup"><span data-stu-id="e554e-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="e554e-146">a.</span><span class="sxs-lookup"><span data-stu-id="e554e-146">a.</span></span> <span data-ttu-id="e554e-147">Agregue a las declaraciones de espacios de nombres:</span><span class="sxs-lookup"><span data-stu-id="e554e-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="e554e-148">b.</span><span class="sxs-lookup"><span data-stu-id="e554e-148">b.</span></span> <span data-ttu-id="e554e-149">Reemplace **Page** en el nombre de etiqueta XML por **engagement:EngagementPageOverlay**.</span><span class="sxs-lookup"><span data-stu-id="e554e-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e554e-150">Si la página invalida el método `OnNavigatedTo`, no olvide llamar a `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="e554e-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="e554e-151">De lo contrario, la actividad no se notifica (`EngagementPage` llama a `StartActivity` dentro de su método `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="e554e-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="e554e-152">Esto es especialmente importante en un proyecto de Windows Phone cuando la plantilla predeterminada tiene un método `OnNavigatedTo` .</span><span class="sxs-lookup"><span data-stu-id="e554e-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="e554e-153">Para **aplicaciones universales de Windows 10**, use el método recomendado en la sección "Método recomendado: sobrecarga de las clases Page" de [Informes avanzados con el SDK de Engagement para aplicaciones universales de Windows](mobile-engagement-windows-store-advanced-reporting.md), en lugar del que se mencionó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e554e-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="e554e-154"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="e554e-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="e554e-155"><a id="integrate-push"></a>Habilitación de las notificaciones de inserción y la mensajería en aplicación</span><span class="sxs-lookup"><span data-stu-id="e554e-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="e554e-156">Mobile Engagement permite interactuar y llegar a los usuarios mediante notificaciones push y mensajería en la aplicación en el contexto de las campañas.</span><span class="sxs-lookup"><span data-stu-id="e554e-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="e554e-157">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e554e-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="e554e-158">En las secciones siguientes se instala la aplicación para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="e554e-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="e554e-159">Habilitar la aplicación para recibir notificaciones de inserción de WNS</span><span class="sxs-lookup"><span data-stu-id="e554e-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="e554e-160">En el archivo , en la pestaña `Package.appxmanifest`Aplicación**, en** Notificaciones**, seleccione** Sí**** en **Capacidad de aviso:**.</span><span class="sxs-lookup"><span data-stu-id="e554e-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="e554e-161">Inicializar el SDK de REACH</span><span class="sxs-lookup"><span data-stu-id="e554e-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="e554e-162">En `App.xaml.cs`, llame a **EngagementReach.Instance.Init();** en la función **InitEngagement** inmediatamente después de la inicialización del agente:</span><span class="sxs-lookup"><span data-stu-id="e554e-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="e554e-163">Está listo para enviar una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="e554e-163">You're ready to send a toast.</span></span> <span data-ttu-id="e554e-164">Ahora comprobaremos que ha llevado a cabo correctamente esta integración básica.</span><span class="sxs-lookup"><span data-stu-id="e554e-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="e554e-165">Concesión de acceso a Mobile Engagement para enviar notificaciones</span><span class="sxs-lookup"><span data-stu-id="e554e-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="e554e-166">Abra el [Centro de desarrollo de Tienda Windows] en el explorador web, inicie sesión y cree una cuenta, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e554e-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="e554e-167">Haga clic en **Panel** en la esquina superior derecha y, luego, haga clic en **Crear una nueva aplicación** en el menú del panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="e554e-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="e554e-168">Cree la aplicación mediante la reserva de su nombre.</span><span class="sxs-lookup"><span data-stu-id="e554e-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="e554e-169">Una vez creada la aplicación, navegue a **Servicios -> Notificaciones push** en el menú izquierdo.</span><span class="sxs-lookup"><span data-stu-id="e554e-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="e554e-170">En la sección Notificaciones push, haga clic en el vínculo **sitio de Live Services**.</span><span class="sxs-lookup"><span data-stu-id="e554e-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="e554e-171">Desplácese a la sección de credenciales de inserción.</span><span class="sxs-lookup"><span data-stu-id="e554e-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="e554e-172">Asegúrese de que se encuentra en la sección **Configuración de aplicaciones** y, luego, copie su **SID del paquete** y **Secreto del cliente**</span><span class="sxs-lookup"><span data-stu-id="e554e-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="e554e-173">Navegue a **Configuración** en el portal de Mobile Engagement y haga clic en la sección **Inserción nativa** de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="e554e-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="e554e-174">Luego, haga clic en el botón **Editar** para especificar el **identificador de seguridad de paquete (SID)** y su **clave secreta**, como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="e554e-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="e554e-175">Por último, asegúrese de que asoció la aplicación de Visual Studio a esta aplicación creada en la tienda de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e554e-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="e554e-176">Haga clic en **Asociar aplicación con la Tienda** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e554e-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="e554e-177"><a id="send"></a>Enviar una notificación a su aplicación</span><span class="sxs-lookup"><span data-stu-id="e554e-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="e554e-178">Si se ejecuta la aplicación, verá una notificación en aplicación.</span><span class="sxs-lookup"><span data-stu-id="e554e-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="e554e-179">De lo contrario, si la aplicación está cerrada, verá una notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="e554e-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="e554e-180">Si ve una notificación en aplicación, pero no una notificación del sistema, y la aplicación se ejecuta en modo de depuración en Visual Studio, pruebe **Eventos del ciclo de vida -> Suspender** en la barra de herramientas para asegurarse de que la aplicación está realmente suspendida.</span><span class="sxs-lookup"><span data-stu-id="e554e-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="e554e-181">Si acaba de hacer clic en el botón de inicio mientras se depura la aplicación en Visual Studio, no siempre se suspenderá y, mientras vea la notificación como desde la aplicación, no se mostrará como notificación del sistema.</span><span class="sxs-lookup"><span data-stu-id="e554e-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="e554e-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="e554e-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="e554e-183">[Centro de desarrollo de Tienda Windows]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="e554e-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
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
