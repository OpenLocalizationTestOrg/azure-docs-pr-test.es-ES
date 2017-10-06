---
title: "aaaGet Started with Azure Mobile Engagement para Android Unity implementación"
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con análisis y notificaciones de inserción para las aplicaciones de Unity implementar dispositivos tooiOS."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="da798-103">Introducción a Azure Mobile Engagement para la implementación de Unity para Android</span><span class="sxs-lookup"><span data-stu-id="da798-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="da798-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación de Unity al implementar el dispositivo Android tooan.</span><span class="sxs-lookup"><span data-stu-id="da798-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="da798-105">Este tutorial se utiliza Hola clásico Unity poner un tutorial de bola como punto de partida de Hola.</span><span class="sxs-lookup"><span data-stu-id="da798-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="da798-106">Debe seguir los pasos de hello en este [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de continuar con hello integración de Mobile Engagement se muestran en el tutorial de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="da798-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="da798-107">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="da798-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="da798-108">Editor de Unity</span><span class="sxs-lookup"><span data-stu-id="da798-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="da798-109">SDK de Unity para Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="da798-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="da798-110">SDK de Google Android</span><span class="sxs-lookup"><span data-stu-id="da798-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="da798-111">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="da798-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="da798-112">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="da798-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="da798-113">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="da798-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="da798-114"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="da798-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="da798-115"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="da798-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="da798-116">Importar paquete de Unity Hola</span><span class="sxs-lookup"><span data-stu-id="da798-116">Import hello Unity package</span></span>
1. <span data-ttu-id="da798-117">Descargar hello [paquete de Mobile Engagement Unity](https://aka.ms/azmeunitysdk) y lo guarda en la máquina local tooyour.</span><span class="sxs-lookup"><span data-stu-id="da798-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="da798-118">Vaya demasiado**activos -> Importar paquete -> paquete personalizado** y el paquete de hello seleccione descargado en hello por encima del paso.</span><span class="sxs-lookup"><span data-stu-id="da798-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="da798-119">Asegúrese de que se seleccionan todos los archivos y haga clic en el botón **Import** (Importar).</span><span class="sxs-lookup"><span data-stu-id="da798-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="da798-120">Una vez que la importación es correcta, verá los archivos SDK de hello importado en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="da798-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="da798-121">Actualizar hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="da798-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="da798-122">Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **ANDROID\_conexión\_cadena** con cadena de conexión de hello obtuvo versiones anteriores de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="da798-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="da798-123">Guardar archivo hello</span><span class="sxs-lookup"><span data-stu-id="da798-123">Save hello file</span></span> 
3. <span data-ttu-id="da798-124">Ejecute **File -> Engagement -> Generate Android Manifest** (Archivo -> Interacción - > Generar manifiesto Android).</span><span class="sxs-lookup"><span data-stu-id="da798-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="da798-125">Se trata de complemento de hello agregada por hello SDK de Mobile Engagement y haga clic en ella se actualizará automáticamente la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="da798-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="da798-126">Hacerlo seguro tooexecute cada vez que actualice hello **EngagementConfiguration** archivo lo contrario no se reflejarán los cambios en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="da798-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="da798-127">Configurar la aplicación hello para el seguimiento básico</span><span class="sxs-lookup"><span data-stu-id="da798-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="da798-128">Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición.</span><span class="sxs-lookup"><span data-stu-id="da798-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="da798-129">Agregue Hola siguiente instrucción using:</span><span class="sxs-lookup"><span data-stu-id="da798-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="da798-130">Agregar Hola después toohello `Start()` (método)</span><span class="sxs-lookup"><span data-stu-id="da798-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="da798-131">Implementar y ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="da798-131">Deploy and run hello app</span></span>
<span data-ttu-id="da798-132">Asegúrese de que tiene instalados en su equipo antes de intentar toodeploy este dispositivo de tooyour de aplicación de Unity de SDK de Android.</span><span class="sxs-lookup"><span data-stu-id="da798-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="da798-133">Conectar una máquina de tooyour dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="da798-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="da798-134">Abra **File -> Build Settings** (Archivo -> Configuración de compilación).</span><span class="sxs-lookup"><span data-stu-id="da798-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="da798-135">Seleccione **Android** y, después, haga clic en **Switch Platform** (Cambiar plataforma).</span><span class="sxs-lookup"><span data-stu-id="da798-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="da798-136">Haga clic en **Player settings** (Configuración del Reproductor) y proporcione un identificador de agrupación de trabajos válido.</span><span class="sxs-lookup"><span data-stu-id="da798-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="da798-137">Por último, haga clic en **Build And Run**</span><span class="sxs-lookup"><span data-stu-id="da798-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="da798-138">Es posible que más frecuentes tooprovide un paquete carpeta nombre toostore Hola Android.</span><span class="sxs-lookup"><span data-stu-id="da798-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="da798-139">Si todo va bien, paquetes de saludo será implementado tooyour conectado dispositivo y se debería aparecer su juego Unity en su teléfono.</span><span class="sxs-lookup"><span data-stu-id="da798-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="da798-140"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="da798-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="da798-141"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="da798-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="da798-142">Actualizar hello EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="da798-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="da798-143">Abra hello **EngagementConfiguration** archivo de script de Hola de carpeta y actualización SDK de hello **ANDROID\_GOOGLE\_número** con hello **proyecto de Google Número** obtenido anteriormente desde el portal para desarrolladores de nube de Google Hola.</span><span class="sxs-lookup"><span data-stu-id="da798-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="da798-144">Se trata de una cadena de valor por lo que debe tooenclose seguro en comillas dobles.</span><span class="sxs-lookup"><span data-stu-id="da798-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="da798-145">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="da798-145">Save hello file.</span></span> 
3. <span data-ttu-id="da798-146">Ejecute **File -> Engagement -> Generate Android Manifest** (Archivo -> Interacción - > Generar manifiesto Android).</span><span class="sxs-lookup"><span data-stu-id="da798-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="da798-147">Se trata de complemento de hello agregada por hello SDK de Mobile Engagement y haga clic en ella se actualizará automáticamente la configuración del proyecto.</span><span class="sxs-lookup"><span data-stu-id="da798-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="da798-148">Configurar notificaciones de tooreceive aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="da798-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="da798-149">Abra hello **PlayerController** script adjunto toohello objeto del Reproductor para su edición.</span><span class="sxs-lookup"><span data-stu-id="da798-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="da798-150">Agregar Hola después toohello `Start()` (método)</span><span class="sxs-lookup"><span data-stu-id="da798-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="da798-151">Ahora que hello aplicación se actualiza, implemente y ejecute la aplicación hello en un dispositivo por instrucciones de hello proporcionadas a continuación.</span><span class="sxs-lookup"><span data-stu-id="da798-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
