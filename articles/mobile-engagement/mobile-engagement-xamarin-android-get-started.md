---
title: "Introducción a Azure Mobile Engagement para aplicaciones Xamarin.Android"
description: "Aprenda a usar Azure Mobile Engagement con los análisis y las notificaciones push para aplicaciones Xamarin.Android."
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
ms.openlocfilehash: 7b3d01b32c2d5a40448fc22861cd45f612238f2f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a><span data-ttu-id="87c7a-103">Introducción a Azure Mobile Engagement para aplicaciones Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="87c7a-103">Get Started with Azure Mobile Engagement for Xamarin.Android Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="87c7a-104">En este tema se muestra cómo usar Azure Mobile Engagement para comprender el uso de su aplicación y cómo enviar notificaciones push a usuarios segmentados de una aplicación Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="87c7a-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Xamarin.Android application.</span></span>
<span data-ttu-id="87c7a-105">En este tutorial se demuestra el escenario de difusión sencillo con Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="87c7a-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="87c7a-106">En él, creará una aplicación vacía de Xamarin.Android que recopile datos básicos y reciba notificaciones push con Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="87c7a-106">In it, you create a blank Xamarin.Android app that collects basic data and receives push notifications using Google Cloud Messaging (GCM).</span></span>

> [!NOTE]
> <span data-ttu-id="87c7a-107">El servicio Azure Mobile Engagement se retirará en marzo de 2018 y actualmente solo está disponible para los clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="87c7a-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="87c7a-108">Para más información, consulte [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="87c7a-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="87c7a-109">Este tutorial requiere lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="87c7a-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="87c7a-110">[Xamarin Studio](http://xamarin.com/studio).</span><span class="sxs-lookup"><span data-stu-id="87c7a-110">[Xamarin Studio](http://xamarin.com/studio).</span></span> <span data-ttu-id="87c7a-111">También puede utilizar Visual Studio con Xamarin, pero en este tutorial se usa Xamarin Studio.</span><span class="sxs-lookup"><span data-stu-id="87c7a-111">You can also use Visual Studio with Xamarin but this tutorial uses Xamarin Studio.</span></span> <span data-ttu-id="87c7a-112">Consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx)para obtener instrucciones.</span><span class="sxs-lookup"><span data-stu-id="87c7a-112">For installation instructions, see [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>
* [<span data-ttu-id="87c7a-113">SDK de Mobile Engagement Xamarin</span><span class="sxs-lookup"><span data-stu-id="87c7a-113">Mobile Engagement Xamarin SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> <span data-ttu-id="87c7a-114">Para completar este tutorial, deberá tener una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="87c7a-114">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="87c7a-115">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="87c7a-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="87c7a-116">Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="87c7a-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="87c7a-117"><a id="setup-azme"></a>Configuración de Mobile Engagement para una aplicación Android</span><span class="sxs-lookup"><span data-stu-id="87c7a-117"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="87c7a-118"><a id="connecting-app"></a>Conectar la aplicación al backend de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="87c7a-118"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="87c7a-119">En este tutorial se presenta una "integración básica", que es el conjunto mínimo necesario para recopilar los datos y enviar una notificación de inserción.</span><span class="sxs-lookup"><span data-stu-id="87c7a-119">This tutorial presents a "basic integration", which is the minimal set required to collect data and send a push notification.</span></span> 

<span data-ttu-id="87c7a-120">Crearemos una aplicación básica con Xamarin Studio para demostrar la integración.</span><span class="sxs-lookup"><span data-stu-id="87c7a-120">We will create a basic app with Xamarin Studio to demonstrate the integration.</span></span>

### <a name="create-a-new-xamarinandroid-project"></a><span data-ttu-id="87c7a-121">Creación de un nuevo proyecto de Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="87c7a-121">Create a new Xamarin.Android project</span></span>
1. <span data-ttu-id="87c7a-122">Inicie **Xamarin Studio**, vaya a **File** -> **New** -> **Solution** (Archivo -> Nuevo -> Solución).</span><span class="sxs-lookup"><span data-stu-id="87c7a-122">Launch **Xamarin Studio** Go to **File** -> **New** -> **Solution**</span></span> 
   
    ![][1]
2. <span data-ttu-id="87c7a-123">Seleccione **Android App** (Aplicación Android), asegúrese de que el lenguaje seleccionado sea **C#** y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="87c7a-123">Select **Android App** then make sure the selected language is **C#** and click **Next**.</span></span>
   
    ![][2]
3. <span data-ttu-id="87c7a-124">Rellene los valores de **App Name** (Nombre de la aplicación) y **Organization Identifier** (Identificador de organización).</span><span class="sxs-lookup"><span data-stu-id="87c7a-124">Fill in the **App Name** and the **Organization Identifier**.</span></span> <span data-ttu-id="87c7a-125">Asegúrese de marcar **Google Play Services** y luego haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="87c7a-125">Make sure to checkmark **Google Play Services** and then click **Next**.</span></span> 
   
    ![][3]
4. <span data-ttu-id="87c7a-126">Actualice los valores de **Project Name** (Nombre de proyecto), **Solution Name** (Nombre de solución) y **Location** (Ubicación) si es necesario y haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="87c7a-126">Update the **Project Name**, **Solution Name** and **Location** if required and click **Create**.</span></span>
   
    ![][4]

<span data-ttu-id="87c7a-127">Xamarin Studio crea la aplicación en la que se integrará Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="87c7a-127">Xamarin Studio will create the app in which we will integrate Mobile Engagement.</span></span> 

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="87c7a-128">Conectar la aplicación al back-end de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="87c7a-128">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="87c7a-129">Haga clic con el botón derecho en la carpeta **Packages** de las ventanas de la solución y seleccione **Add Packages...** (Agregar paquetes).</span><span class="sxs-lookup"><span data-stu-id="87c7a-129">Right click the **Packages** folder in the Solution windows and select **Add Packages...**</span></span>
   
    ![][5]
2. <span data-ttu-id="87c7a-130">Busque el **SDK de Xamarin para Microsoft Azure Mobile Engagement** y agréguelo a la solución.</span><span class="sxs-lookup"><span data-stu-id="87c7a-130">Search for the **Microsoft Azure Mobile Engagement Xamarin SDK** and add it to your solution.</span></span>  
   
    ![][6]
3. <span data-ttu-id="87c7a-131">Abra **MainActivity.cs** y agregue las siguientes instrucciones using:</span><span class="sxs-lookup"><span data-stu-id="87c7a-131">Open **MainActivity.cs** and add the following using statements:</span></span>
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. <span data-ttu-id="87c7a-132">En el método `OnCreate` , agregue el siguiente código para inicializar la conexión con el back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="87c7a-132">In the `OnCreate` method, add the following to initialize the connection with Mobile Engagement backend.</span></span> <span data-ttu-id="87c7a-133">Asegúrese de agregar su elemento **ConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="87c7a-133">Make sure to add your **ConnectionString**.</span></span> 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a><span data-ttu-id="87c7a-134">Agregar permisos y una declaración de servicio</span><span class="sxs-lookup"><span data-stu-id="87c7a-134">Add permissions and a service declaration</span></span>
1. <span data-ttu-id="87c7a-135">Abra el archivo **Manifest.xml** de la carpeta Properties (Propiedades).</span><span class="sxs-lookup"><span data-stu-id="87c7a-135">Open up the **Manifest.xml** file under the Properties folder.</span></span> <span data-ttu-id="87c7a-136">Seleccione la pestaña Source (Origen) para actualizar directamente el origen XML.</span><span class="sxs-lookup"><span data-stu-id="87c7a-136">Select Source tab so that you directly update the XML source.</span></span>
2. <span data-ttu-id="87c7a-137">Agregue estos permisos al archivo Manifest.xml (que se puede encontrar en la carpeta **Properties**) de su proyecto inmediatamente antes o después de la etiqueta `<application>`:</span><span class="sxs-lookup"><span data-stu-id="87c7a-137">Add these permissions to the Manifest.xml (which can be found under the **Properties** folder) of your project immediately before or after the `<application>` tag:</span></span>
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. <span data-ttu-id="87c7a-138">Agregue lo siguiente entre las etiquetas `<application>` y `</application>` para declarar el servicio del agente:</span><span class="sxs-lookup"><span data-stu-id="87c7a-138">Add the following between the `<application>` and `</application>` tags to declare the agent service:</span></span>
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. <span data-ttu-id="87c7a-139">En el código que acaba de pegar, reemplace `"<Your application name>"` en la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="87c7a-139">In the code you just pasted, replace `"<Your application name>"` in the label.</span></span> <span data-ttu-id="87c7a-140">Esto es lo que se muestra en el menú **Configuración** donde los usuarios pueden ver los servicios que se están ejecutando en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87c7a-140">This is displayed in the **Settings** menu where users can see services running on the device.</span></span> <span data-ttu-id="87c7a-141">Puede agregar la palabra "Servicio" a la etiqueta, por ejemplo.</span><span class="sxs-lookup"><span data-stu-id="87c7a-141">You can add the word "Service" in that label for example.</span></span>

### <a name="send-a-screen-to-mobile-engagement"></a><span data-ttu-id="87c7a-142">Enviar una pantalla a Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="87c7a-142">Send a screen to Mobile Engagement</span></span>
<span data-ttu-id="87c7a-143">Para comenzar a enviar datos y asegurarse de que los usuarios estén activos, debe enviar al menos una pantalla al back-end de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="87c7a-143">In order to start sending data and ensuring the users are active, you must send at least one screen to the Mobile Engagement backend.</span></span> <span data-ttu-id="87c7a-144">Para ello, asegúrese de que `MainActivity` hereda de `EngagementActivity`, en lugar de `Activity`.</span><span class="sxs-lookup"><span data-stu-id="87c7a-144">For doing this - ensure that the `MainActivity` inherits from `EngagementActivity` instead of `Activity`.</span></span>

    public class MainActivity : EngagementActivity

<span data-ttu-id="87c7a-145">Como alternativa, si no puede heredar de `EngagementActivity`, deberá agregar los métodos `.StartActivity` y `.EndActivity` en `OnResume` y `OnPause`, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="87c7a-145">Alternatively, if you cannot inherit from `EngagementActivity` then you must add `.StartActivity` and `.EndActivity` methods in `OnResume` and `OnPause` respectively.</span></span>  

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

## <span data-ttu-id="87c7a-146"><a id="monitor"></a>Conexión de la aplicación con la supervisión en tiempo real</span><span class="sxs-lookup"><span data-stu-id="87c7a-146"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="87c7a-147"><a id="integrate-push"></a>Habilitar las notificaciones push y la mensajería en la aplicación</span><span class="sxs-lookup"><span data-stu-id="87c7a-147"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="87c7a-148">Mobile Engagement permite interactuar y llegar por REACH a los usuarios mediante notificaciones de inserción y mensajería en la aplicación en el contexto de las campañas.</span><span class="sxs-lookup"><span data-stu-id="87c7a-148">Mobile Engagement allows you to interact with and REACH your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="87c7a-149">Este módulo se denomina REACH en el portal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="87c7a-149">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="87c7a-150">En las secciones siguientes se instala la aplicación para recibirlos.</span><span class="sxs-lookup"><span data-stu-id="87c7a-150">The following sections sets up your app to receive them.</span></span>

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
