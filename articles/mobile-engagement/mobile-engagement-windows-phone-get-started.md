---
title: aaaGet a trabajar con aplicaciones de Azure Mobile Engagement para Windows Phone Silverlight
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement a las notificaciones de inserción y de análisis para las aplicaciones de Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a><span data-ttu-id="7d8ec-103">Introducción a Azure Mobile Engagement para aplicaciones Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7d8ec-103">Get started with Azure Mobile Engagement for Windows Phone Silverlight apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="7d8ec-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de aplicaciones y el envío de inserción a los usuarios toosegmented de notificaciones de una aplicación de Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Phone Silverlight application.</span></span>
<span data-ttu-id="7d8ec-105">Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="7d8ec-106">En él, puede crear una aplicación de Windows Phone Silverlight vacía que recopila datos básicos y recibe notificaciones de inserción mediante el Servicio de notificaciones de inserción de Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-106">In it, you create a blank Windows Phone Silverlight app that collects basic data and receives push notifications using Microsoft Push Notification Service (MPNS).</span></span>

> [!NOTE]
> <span data-ttu-id="7d8ec-107">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="7d8ec-108">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

> [!NOTE]
> <span data-ttu-id="7d8ec-109">Los proyectos de Windows Phone 8.1 y de la versión anterior no son compatibles con Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-109">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="7d8ec-110">Para más información, consulte [Compatibilidad y destinatarios de la plataforma de Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-110">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="7d8ec-111">Si desea usar Windows Phone 8.1 (no de Silverlight), consulte toohello [tutorial universales de Windows](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-111">If you are targeting Windows Phone 8.1 (non-Silverlight), refer toohello [Windows Universal tutorial](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>
> 
> 

<span data-ttu-id="7d8ec-112">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-112">This tutorial requires hello following:</span></span>

* <span data-ttu-id="7d8ec-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7d8ec-113">Visual Studio 2013</span></span>
* <span data-ttu-id="7d8ec-114">[MicrosoftAzure.MobileEngagement]</span><span class="sxs-lookup"><span data-stu-id="7d8ec-114">[MicrosoftAzure.MobileEngagement] Nuget package</span></span>

> [!NOTE]
> <span data-ttu-id="7d8ec-115">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-115">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="7d8ec-116">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-116">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7d8ec-117">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).</span></span>
> 
> 

## <span data-ttu-id="7d8ec-118"><a id="setup-azme"></a>Configurar Mobile Engagement para su aplicación de Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7d8ec-118"><a id="setup-azme"></a>Setup Mobile Engagement for your Windows Phone app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="7d8ec-119"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7d8ec-119"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="7d8ec-120">Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-120">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="7d8ec-121">Encontrará documentación de integración completa de Hola Hola [integración de Windows Phone SDK de Mobile Engagement](mobile-engagement-windows-phone-sdk-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7d8ec-121">hello complete integration documentation can be found in hello [Mobile Engagement Windows Phone SDK integration](mobile-engagement-windows-phone-sdk-overview.md)</span></span>

<span data-ttu-id="7d8ec-122">Se creará una aplicación básica con la integración de Visual Studio toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-122">We will create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-windows-phone-silverlight-project"></a><span data-ttu-id="7d8ec-123">Crear un nuevo proyecto de Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7d8ec-123">Create a new Windows Phone Silverlight project</span></span>
<span data-ttu-id="7d8ec-124">Hello siguientes pasos supone Hola uso de Visual Studio 2015 aunque Hola pasos son similares en versiones anteriores de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-124">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="7d8ec-125">Inicie Visual Studio y en hello **inicio** pantalla, seleccione **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-125">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="7d8ec-126">En el menú emergente de hello, seleccione **Windows 8** -> **de Windows Phone** -> **aplicación vacía (Windows Phone Silverlight)**.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-126">In hello pop-up, select **Windows 8** -> **Windows Phone** -> **Blank App (Windows Phone Silverlight)**.</span></span> <span data-ttu-id="7d8ec-127">Rellene la aplicación hello **nombre** y **nombre de la solución**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-127">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>
   
    ![][1]
3. <span data-ttu-id="7d8ec-128">Puede elegir tootarget o **Windows Phone 8.0** o **Windows Phone 8.1**.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-128">You can choose tootarget either **Windows Phone 8.0** or **Windows Phone 8.1**.</span></span>

<span data-ttu-id="7d8ec-129">Ahora ha creado una nueva aplicación de Windows Phone Silverlight en la que se integrará hello Azure Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-129">You have now created a new Windows Phone Silverlight app into which we will integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a><span data-ttu-id="7d8ec-130">Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7d8ec-130">Connect your app toohello Mobile Engagement backend</span></span>
1. <span data-ttu-id="7d8ec-131">Instalar hello [MicrosoftAzure.MobileEngagement] paquete de nuget en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-131">Install hello [MicrosoftAzure.MobileEngagement] nuget package in your project.</span></span>
2. <span data-ttu-id="7d8ec-132">Abra `WMAppManifest.xml` (en la carpeta de propiedades de hello) y asegúrese de que se declara siguiente hello (agregarlas si no lo son) en hello `<Capabilities />` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-132">Open `WMAppManifest.xml` (under hello Properties folder) and make sure hello following are declared (add them if they are not) in hello `<Capabilities />` tag:</span></span>
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. <span data-ttu-id="7d8ec-133">Ahora, pegue la cadena de conexión de Hola que copió anteriormente para la aplicación de interacción móvil y péguelo en hello `Resources\EngagementConfiguration.xml` archivo entre hello `<connectionString>` y `</connectionString>` etiquetas:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-133">Now paste hello connection string that you copied earlier for your Mobile Engagement app and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>
   
    ![][3]
4. <span data-ttu-id="7d8ec-134">Hola `App.xaml.cs` archivo:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-134">In hello `App.xaml.cs` file:</span></span>
   
    <span data-ttu-id="7d8ec-135">a.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-135">a.</span></span> <span data-ttu-id="7d8ec-136">Agregar hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-136">Add hello `using` statement:</span></span>
   
            using Microsoft.Azure.Engagement;
   
    <span data-ttu-id="7d8ec-137">b.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-137">b.</span></span> <span data-ttu-id="7d8ec-138">Inicializar Hola SDK en hello `Application_Launching` método:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-138">Initialize hello SDK in hello `Application_Launching` method:</span></span>
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    <span data-ttu-id="7d8ec-139">c.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-139">c.</span></span> <span data-ttu-id="7d8ec-140">Inserte el siguiente de Hola Hola `Application_Activated`:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-140">Insert hello following in hello `Application_Activated`:</span></span>
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <span data-ttu-id="7d8ec-141"><a id="monitor"></a>Habilitación de la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="7d8ec-141"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="7d8ec-142">En orden toostart enviando los datos y asegurarse de que los usuarios de hello activos, debe enviar al menos un backend de interacción móvil toohello de pantalla (actividad).</span><span class="sxs-lookup"><span data-stu-id="7d8ec-142">In order toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="7d8ec-143">Hola MainPage.xaml.cs, agregue hello `using` instrucción:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-143">In hello MainPage.xaml.cs, add hello `using` statement:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="7d8ec-144">Reemplace la clase base hello de **MainPage**, que es anterior **PhoneApplicationPage**, con **EngagementPage**.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-144">Replace hello base class of **MainPage**, which is before **PhoneApplicationPage**, with **EngagementPage**.</span></span>
   
        class MainPage : EngagementPage 
3. <span data-ttu-id="7d8ec-145">En el archivo `MainPage.xml`:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-145">In your `MainPage.xml` file:</span></span>
   
    <span data-ttu-id="7d8ec-146">a.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-146">a.</span></span> <span data-ttu-id="7d8ec-147">Agregue las declaraciones de espacios de nombres tooyour:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-147">Add tooyour namespaces declarations:</span></span>
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    <span data-ttu-id="7d8ec-148">b.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-148">b.</span></span> <span data-ttu-id="7d8ec-149">Reemplace `phone:PhoneApplicationPage` en nombre de etiqueta XML de hello con `engagement:EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-149">Replace `phone:PhoneApplicationPage` in hello XML tag name with `engagement:EngagementPage`.</span></span>

## <span data-ttu-id="7d8ec-150"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="7d8ec-150"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="7d8ec-151"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="7d8ec-151"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="7d8ec-152">Mobile Engagement le permite toointeract y llegar a los usuarios con las notificaciones de inserción y en la aplicación de mensajería en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-152">Mobile Engagement allows you toointeract and reach your users with Push Notifications and in-app Messaging in hello context of campaigns.</span></span> <span data-ttu-id="7d8ec-153">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-153">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="7d8ec-154">Hello las secciones siguientes configure su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-154">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a><span data-ttu-id="7d8ec-155">Habilitar la tooreceive de la aplicación notificaciones de inserción de MPNS</span><span class="sxs-lookup"><span data-stu-id="7d8ec-155">Enable your app tooreceive MPNS Push Notifications</span></span>
<span data-ttu-id="7d8ec-156">Agregar nueva tooyour capacidades `WMAppManifest.xml` archivo:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-156">Add new Capabilities tooyour `WMAppManifest.xml` file:</span></span>

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="7d8ec-157">Inicializar Hola REACH SDK</span><span class="sxs-lookup"><span data-stu-id="7d8ec-157">Initialize hello REACH SDK</span></span>
1. <span data-ttu-id="7d8ec-158">En `App.xaml.cs`, llame a `EngagementReach.Instance.Init();` en hello **Application_Launching** función, justo después de la inicialización del agente de hello:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-158">In `App.xaml.cs`, call `EngagementReach.Instance.Init();` in hello **Application_Launching** function, right after hello agent initialization:</span></span>
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. <span data-ttu-id="7d8ec-159">En `App.xaml.cs`, llame a `EngagementReach.Instance.OnActivated(e);` en hello **Application_Activated** función, justo después de la inicialización del agente de hello:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-159">In `App.xaml.cs`, call `EngagementReach.Instance.OnActivated(e);` in hello **Application_Activated** function, right after hello agent initialization:</span></span>
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

<span data-ttu-id="7d8ec-160">Está listo.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-160">You're all set.</span></span> <span data-ttu-id="7d8ec-161">Ahora comprobaremos que ha llevado a cabo correctamente esta integración básica.</span><span class="sxs-lookup"><span data-stu-id="7d8ec-161">Now we will verify that you have correctly cried out this basic integration.</span></span>

## <span data-ttu-id="7d8ec-162"><a id="send"></a>Enviar una aplicación de tooyour de notificación</span><span class="sxs-lookup"><span data-stu-id="7d8ec-162"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="7d8ec-163">Ahora debería ver una notificación en el dispositivo que se mostrará como una notificación en la aplicación si aplicación hello está abierto en caso contrario, como una notificación del sistema como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7d8ec-163">You should now see a notification on your device which will show up as an in-app notification if hello app is open otherwise as a toast notification like hello following:</span></span> 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
