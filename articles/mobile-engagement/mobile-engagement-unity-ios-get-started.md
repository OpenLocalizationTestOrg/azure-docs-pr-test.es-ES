---
title: "aaaGet Started with Azure Mobile Engagement para la implementación de iOS de Unity"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para las aplicaciones de Unity implementar dispositivos tooiOS."
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
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="62eb4-103">Introducción a Azure Mobile Engagement para la implementación de Unity para iOS</span><span class="sxs-lookup"><span data-stu-id="62eb4-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="62eb4-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación de Unity al implementar el dispositivo iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="62eb4-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="62eb4-105">Este tutorial se utiliza Hola clásico Unity poner un tutorial de bola como punto de partida de Hola.</span><span class="sxs-lookup"><span data-stu-id="62eb4-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="62eb4-106">Debe seguir los pasos de hello en este [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar con hello integración de Mobile Engagement se muestran en el tutorial de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="62eb4-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="62eb4-107">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="62eb4-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="62eb4-108">Editor de Unity</span><span class="sxs-lookup"><span data-stu-id="62eb4-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="62eb4-109">SDK de Unity para Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="62eb4-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="62eb4-110">Editor de XCode</span><span class="sxs-lookup"><span data-stu-id="62eb4-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="62eb4-111">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb4-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="62eb4-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="62eb4-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="62eb4-113">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="62eb4-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="62eb4-114"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación iOS</span><span class="sxs-lookup"><span data-stu-id="62eb4-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="62eb4-115"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="62eb4-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="62eb4-116">Importar paquete de Unity Hola</span><span class="sxs-lookup"><span data-stu-id="62eb4-116">Import hello Unity package</span></span>
1. <span data-ttu-id="62eb4-117">Descargar hello [paquete de Mobile Engagement Unity](https://aka.ms/azmeunitysdk) y lo guarda en la máquina local tooyour.</span><span class="sxs-lookup"><span data-stu-id="62eb4-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="62eb4-118">Vaya demasiado**activos -> Importar paquete -> paquete personalizado** y el paquete de hello seleccione descargado en hello por encima del paso.</span><span class="sxs-lookup"><span data-stu-id="62eb4-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="62eb4-119">Asegúrese de que se seleccionan todos los archivos y haga clic en el botón **Import** (Importar).</span><span class="sxs-lookup"><span data-stu-id="62eb4-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="62eb4-120">Una vez que la importación es correcta, verá los archivos SDK de hello importado en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="62eb4-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="62eb4-121">Actualizar hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="62eb4-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="62eb4-122">Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **IOS\_conexión\_cadena** con la cadena de conexión de hello obtenido anteriormente de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="62eb4-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="62eb4-123">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="62eb4-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="62eb4-124">Configurar la aplicación hello para el seguimiento básico</span><span class="sxs-lookup"><span data-stu-id="62eb4-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="62eb4-125">Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición.</span><span class="sxs-lookup"><span data-stu-id="62eb4-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="62eb4-126">Agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="62eb4-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="62eb4-127">Agregar Hola después toohello `Start()` (método)</span><span class="sxs-lookup"><span data-stu-id="62eb4-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="62eb4-128">Implementar y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="62eb4-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="62eb4-129">Conectar una máquina de tooyour de dispositivo de iOS.</span><span class="sxs-lookup"><span data-stu-id="62eb4-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="62eb4-130">Abra **File -> Build Settings** (Archivo -> Configuración de compilación).</span><span class="sxs-lookup"><span data-stu-id="62eb4-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="62eb4-131">Seleccione **iOS** y, después, haga clic en **Switch Platform** (Cambiar plataforma).</span><span class="sxs-lookup"><span data-stu-id="62eb4-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="62eb4-132">Haga clic en **Player settings** (Configuración del Reproductor) y proporcione un identificador de agrupación de trabajos válido.</span><span class="sxs-lookup"><span data-stu-id="62eb4-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="62eb4-133">Por último, haga clic en **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="62eb4-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="62eb4-134">Es posible que más frecuentes tooprovide un paquete de iOS de carpeta nombre toostore Hola.</span><span class="sxs-lookup"><span data-stu-id="62eb4-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="62eb4-135">Si todo va bien, se compilará el proyecto de Hola y debería abrirlo de en la aplicación de XCode.</span><span class="sxs-lookup"><span data-stu-id="62eb4-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="62eb4-136">Asegúrese de que ese hello **identificador de paquete** es correcto en el proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="62eb4-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="62eb4-137">Ahora ejecutar aplicación hello en XCode para que el paquete de hello es dispositivo conectado tooyour implementado y debería ver su juego Unity en su teléfono.</span><span class="sxs-lookup"><span data-stu-id="62eb4-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="62eb4-138"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="62eb4-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="62eb4-139"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="62eb4-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="62eb4-140">Mobile Engagement le permite toointeract con los usuarios y alcance con notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="62eb4-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="62eb4-141">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="62eb4-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="62eb4-142">No tiene toodo ninguna configuración adicional en las notificaciones de tooreceive de aplicación y ya está configurado para él.</span><span class="sxs-lookup"><span data-stu-id="62eb4-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

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
