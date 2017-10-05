---
title: "Introducción a Azure Mobile Engagement para la implementación de Unity para iOS"
description: "Aprenda a usar Azure Mobile Engagement con los análisis y las notificaciones push para aplicaciones de Unity que se implementan en dispositivos de iOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="4686f-103">Introducción a Azure Mobile Engagement para la implementación de Unity para iOS</span><span class="sxs-lookup"><span data-stu-id="4686f-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="4686f-104">En este tema se muestra cómo usar Azure Mobile Engagement para comprender el uso de su aplicación y cómo enviar notificaciones push a usuarios segmentados de una aplicación de Unity durante la implementación en un dispositivo de iOS.</span><span class="sxs-lookup"><span data-stu-id="4686f-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="4686f-105">Este tutorial utiliza el tutorial de iniciación clásico de Unity como punto de partida.</span><span class="sxs-lookup"><span data-stu-id="4686f-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="4686f-106">Debe seguir los pasos de este [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar con la integración de Mobile Engagement que se muestra en el tutorial siguiente.</span><span class="sxs-lookup"><span data-stu-id="4686f-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="4686f-107">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4686f-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="4686f-108">Editor de Unity</span><span class="sxs-lookup"><span data-stu-id="4686f-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="4686f-109">SDK de Unity para Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4686f-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="4686f-110">Editor de XCode</span><span class="sxs-lookup"><span data-stu-id="4686f-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="4686f-111">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="4686f-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="4686f-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4686f-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4686f-113">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="4686f-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="4686f-114"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="4686f-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="4686f-115"><a id="connecting-app"></a>Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4686f-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="4686f-116">Importación del paquete de Unity</span><span class="sxs-lookup"><span data-stu-id="4686f-116">Import the Unity package</span></span>
1. <span data-ttu-id="4686f-117">Descargue el [paquete de Unity para Mobile Engagement](https://aka.ms/azmeunitysdk) y guárdelo en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="4686f-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="4686f-118">Vaya a **Assets -> Import Package -> Custom Package** (Recursos -> Importar paquete -> Paquete personalizado) y seleccione el paquete que descargó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="4686f-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="4686f-119">Asegúrese de que se seleccionan todos los archivos y haga clic en el botón **Import** (Importar).</span><span class="sxs-lookup"><span data-stu-id="4686f-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="4686f-120">Una vez que la importación termina correctamente, verá los archivos del SDK importados en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4686f-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="4686f-121">Actualización de EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="4686f-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="4686f-122">Abra el archivo de script **EngagementConfiguration** desde la carpeta del SDK y actualice **IOS\_CONNECTION\_STRING** con la cadena de conexión que obtuvo anteriormente en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4686f-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="4686f-123">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="4686f-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="4686f-124">Configuración de la aplicación para un seguimiento básico</span><span class="sxs-lookup"><span data-stu-id="4686f-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="4686f-125">Abra el script **Playercontroller** asociado al objeto Player para su edición.</span><span class="sxs-lookup"><span data-stu-id="4686f-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="4686f-126">Agregue la siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="4686f-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="4686f-127">Agregue lo siguiente al método `Start()`.</span><span class="sxs-lookup"><span data-stu-id="4686f-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="4686f-128">Implementación y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4686f-128">Deploy and run the app</span></span>
1. <span data-ttu-id="4686f-129">Conecte un dispositivo iOS al equipo.</span><span class="sxs-lookup"><span data-stu-id="4686f-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="4686f-130">Abra **File -> Build Settings** (Archivo -> Configuración de compilación).</span><span class="sxs-lookup"><span data-stu-id="4686f-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="4686f-131">Seleccione **iOS** y, después, haga clic en **Switch Platform** (Cambiar plataforma).</span><span class="sxs-lookup"><span data-stu-id="4686f-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="4686f-132">Haga clic en **Player settings** (Configuración del Reproductor) y proporcione un identificador de agrupación de trabajos válido.</span><span class="sxs-lookup"><span data-stu-id="4686f-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="4686f-133">Por último, haga clic en **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="4686f-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="4686f-134">Se le pedirá que proporcione un nombre de carpeta para almacenar el paquete de iOS.</span><span class="sxs-lookup"><span data-stu-id="4686f-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="4686f-135">Si todo va bien, se compilará el proyecto y se abrirá en la aplicación de XCode.</span><span class="sxs-lookup"><span data-stu-id="4686f-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="4686f-136">Asegúrese de que el **identificador de la agrupación de trabajos** es correcto en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="4686f-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="4686f-137">Ejecute la aplicación en XCode para que el paquete se implemente en su dispositivo conectado y con eso debería ver ya el juego de Unity en el teléfono.</span><span class="sxs-lookup"><span data-stu-id="4686f-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="4686f-138"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="4686f-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="4686f-139"><a id="integrate-push"></a>Habilitación de las notificaciones push y la mensajería en aplicación</span><span class="sxs-lookup"><span data-stu-id="4686f-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="4686f-140">Mobile Engagement permite interactuar y llegar mediante notificaciones push y mensajería en la aplicación en el contexto de las campañas.</span><span class="sxs-lookup"><span data-stu-id="4686f-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="4686f-141">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4686f-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="4686f-142">No tiene que realizar ninguna configuración adicional en la aplicación para recibir notificaciones ya que ya está configurado para ello.</span><span class="sxs-lookup"><span data-stu-id="4686f-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
