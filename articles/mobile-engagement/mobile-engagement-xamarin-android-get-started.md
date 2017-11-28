---
title: aaaGet Started with Azure Mobile Engagement para Xamarin.Android
description: "Obtenga información acerca de cómo toouse Azure Mobile Engagement con las notificaciones de inserción para las aplicaciones de Xamarin.Android y análisis."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="58c06-103">Introducción a Azure Mobile Engagement para aplicaciones Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="58c06-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="58c06-104">Este tema muestra cómo toouse Azure Mobile Engagement toounderstand el uso de la aplicación y cómo toosend insertar los usuarios de toosegmented de notificaciones de una aplicación Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="58c06-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="58c06-105">Este tutorial muestra el escenario de difusión simple hello con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="58c06-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="58c06-106">En él, creará una aplicación vacía de Xamarin.Android que recopile datos básicos y reciba notificaciones push con Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="58c06-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="58c06-107">servicio de Azure Mobile Engagement Hola se retirará de 2018 de marzo y actualmente solo los clientes de tooexisting disponible.</span><span class="sxs-lookup"><span data-stu-id="58c06-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="58c06-108">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="58c06-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="58c06-109">Este tutorial requiere siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="58c06-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="58c06-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="58c06-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="58c06-111">También puede utilizar Visual Studio con Xamarin, pero en este tutorial se usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="58c06-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="58c06-112">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx)para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="58c06-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="58c06-113">SDK de Mobile Engagement Xamarin</span><span class="sxs-lookup"><span data-stu-id="58c06-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="58c06-114">toocomplete este tutorial, debe tener una cuenta activa de Azure.</span><span class="sxs-lookup"><span data-stu-id="58c06-114">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="58c06-115">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="58c06-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="58c06-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="58c06-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="58c06-117"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="58c06-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="58c06-118"><a id="connecting-app"></a>Conectar el back-end de aplicación toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="58c06-118"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="58c06-119">Este tutorial presenta una "la integración básica", que es Hola mínimo establecido toocollect requiere datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="58c06-119">This tutorial presents a "basic integration", which is hello minimal set required toocollect data and send a push notification.</span></span> 

<span data-ttu-id="58c06-120">Se creará una aplicación básica con la integración de Xamarin Studio toodemonstrate Hola.</span><span class="sxs-lookup"><span data-stu-id="58c06-120">We will create a basic app with Xamarin Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="58c06-121">Creación de un nuevo proyecto de Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="58c06-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="58c06-122">Iniciar **Xamarin Studio** vaya demasiado**archivo** -> **New** -> **solución**</span><span class="sxs-lookup"><span data-stu-id="58c06-122">Launch **Xamarin Studio** Go too**File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="58c06-123">Seleccione **aplicación Android** , a continuación, compruebe que el idioma de hello seleccionado es **C#** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="58c06-123">Select **Android App** then make sure hello selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="58c06-124">Rellene hello **nombre de la aplicación** hello y **identificador de la organización**.</span><span class="sxs-lookup"><span data-stu-id="58c06-124">Fill in hello **App Name** and hello **Organization Identifier**.</span></span> <span data-ttu-id="58c06-125">Asegúrese de que toocheckmark **servicios de Google Play** y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="58c06-125">Make sure toocheckmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="58c06-126">Hola de actualización **nombre del proyecto**, **nombre de la solución** y **ubicación** si es necesario y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="58c06-126">Update hello **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="58c06-127">Xamarin Studio creará la aplicación hello en el que se integrará Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="58c06-127">Xamarin Studio will create hello app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="58c06-128">Conectar el backend de interacción de tooMobile de aplicación</span><span class="sxs-lookup"><span data-stu-id="58c06-128">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="58c06-129">Haga clic en hello **paquetes** carpeta de windows de la solución de Hola y seleccione **agregar paquetes...**</span><span class="sxs-lookup"><span data-stu-id="58c06-129">Right click hello **Packages** folder in hello Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="58c06-130">Busque hello **Xamarin SDK de Microsoft Azure Mobile Engagement** y agregar soluciones tooyour.</span><span class="sxs-lookup"><span data-stu-id="58c06-130">Search for hello **Microsoft Azure Mobile Engagement Xamarin SDK** and add it tooyour solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="58c06-131">Abra **MainActivity.cs** y agregue Hola siguientes instrucciones using:</span><span class="sxs-lookup"><span data-stu-id="58c06-131">Open **MainActivity.cs** and add hello following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="58c06-132">Hola `OnCreate` método, agregue Hola después de la conexión de hello tooinitialize con Mobile Engagement back-end.</span><span class="sxs-lookup"><span data-stu-id="58c06-132">In hello `OnCreate` method, add hello following tooinitialize hello connection with Mobile Engagement backend.</span></span> <span data-ttu-id="58c06-133">Asegúrese de que tooadd su **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="58c06-133">Make sure tooadd your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="58c06-134">Agregar permisos y una declaración de servicio</span><span class="sxs-lookup"><span data-stu-id="58c06-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="58c06-135">Abra hello **Manifest.xml** archivo bajo la carpeta Propiedades de Hola.</span><span class="sxs-lookup"><span data-stu-id="58c06-135">Open up hello **Manifest.xml** file under hello Properties folder.</span></span> <span data-ttu-id="58c06-136">Seleccione la ficha origen para que actualizar origen XML de hello directamente.</span><span class="sxs-lookup"><span data-stu-id="58c06-136">Select Source tab so that you directly update hello XML source.</span></span>
2. <span data-ttu-id="58c06-137">Agregar estos toohello permisos Manifest.xml (que se pueden encontrar en hello **propiedades** carpeta) de su proyecto inmediatamente antes o después de hello `<application>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="58c06-137">Add these permissions toohello Manifest.xml (which can be found under hello **Properties** folder) of your project immediately before or after hello `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="58c06-138">Agregue siguiente Hola entre hello `<application>` y `</application>` etiquetas de servicio del agente de Hola toodeclare:</span><span class="sxs-lookup"><span data-stu-id="58c06-138">Add hello following between hello `<application>` and `</application>` tags toodeclare hello agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="58c06-139">En el código de hello que acaba de pegar, reemplace `"<Your application name>"` en etiqueta Hola.</span><span class="sxs-lookup"><span data-stu-id="58c06-139">In hello code you just pasted, replace `"<Your application name>"` in hello label.</span></span> <span data-ttu-id="58c06-140">Esto se muestra en hello **configuración** menú donde los usuarios pueden ver los servicios que se ejecutan en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="58c06-140">This is displayed in hello **Settings** menu where users can see services running on hello device.</span></span> <span data-ttu-id="58c06-141">Por ejemplo puede agregar palabra Hola "Servicio" en esa etiqueta.</span><span class="sxs-lookup"><span data-stu-id="58c06-141">You can add hello word "Service" in that label for example.</span></span>

### <a name="send-a-screen-toomobile-engagement"></a><span data-ttu-id="58c06-142">Enviar una interacción de pantalla tooMobile</span><span class="sxs-lookup"><span data-stu-id="58c06-142">Send a screen tooMobile Engagement</span></span>
<span data-ttu-id="58c06-143">En orden toostart enviando los datos y asegurarse de que los usuarios de hello están activos, debe enviar al menos una pantalla toohello Mobile Engagement back-end.</span><span class="sxs-lookup"><span data-stu-id="58c06-143">In order toostart sending data and ensuring hello users are active, you must send at least one screen toohello Mobile Engagement backend.</span></span> <span data-ttu-id="58c06-144">Para hacer esto-Asegúrese de que hello `MainActivity` hereda de `EngagementActivity` en lugar de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="58c06-144">For doing this - ensure that hello `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="58c06-145">Como alternativa, si no puede heredar de `EngagementActivity`, deberá agregar los métodos `.StartActivity` y `.EndActivity` en `OnResume` y `OnPause`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="58c06-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <span data-ttu-id="58c06-146"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="58c06-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="58c06-147"><a id="integrate-push"></a>Habilitación de notificaciones push y mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="58c06-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="58c06-148">Mobile Engagement le permite toointeract con y llegar a los usuarios con las notificaciones de inserción y en mensajería desde la aplicación en el contexto de Hola de campañas.</span><span class="sxs-lookup"><span data-stu-id="58c06-148">Mobile Engagement allows you toointeract with and REACH your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="58c06-149">Este módulo se denomina alcance en el portal de interacción móvil Hola.</span><span class="sxs-lookup"><span data-stu-id="58c06-149">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="58c06-150">Hola siguientes secciones configura su aplicación tooreceive ellos.</span><span class="sxs-lookup"><span data-stu-id="58c06-150">hello following sections sets up your app tooreceive them.</span></span>

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
