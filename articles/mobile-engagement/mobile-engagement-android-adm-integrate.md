---
title: "Integración del SDK de Android para Azure Mobile Engagement"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="582c1-103">Integración de ADM con Engagement</span><span class="sxs-lookup"><span data-stu-id="582c1-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="582c1-104">Debe seguir el procedimiento de integración descrito en el documento Integración de Engagement en Android antes de seguir con esta guía.</span><span class="sxs-lookup"><span data-stu-id="582c1-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="582c1-105">Este documento es útil solo si ya integró el módulo de cobertura y el plan para insertar dispositivos de Amazon.</span><span class="sxs-lookup"><span data-stu-id="582c1-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="582c1-106">Para integrar campañas de Reach en la aplicación, lea primero Integración de Engagement Reach en Android.</span><span class="sxs-lookup"><span data-stu-id="582c1-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="582c1-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="582c1-107">Introduction</span></span>
<span data-ttu-id="582c1-108">La integración de ADM permite la inserción de la aplicación cuando tenga como destino dispositivos Android de Amazon.</span><span class="sxs-lookup"><span data-stu-id="582c1-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="582c1-109">Las cargas ADM insertadas en el SDK siempre contienen la clave `azme` en el objeto de datos.</span><span class="sxs-lookup"><span data-stu-id="582c1-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="582c1-110">Por lo tanto, si usa ADM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.</span><span class="sxs-lookup"><span data-stu-id="582c1-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="582c1-111">Solo los dispositivos Kindle de Amazon que ejecutan Android 4.0.3 o versiones posteriores son compatibles con la mensajería de dispositivos de Amazon; Sin embargo, puede integrar este código de forma segura en otros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="582c1-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="582c1-112">Suscribirse a ADM</span><span class="sxs-lookup"><span data-stu-id="582c1-112">Sign up to ADM</span></span>
<span data-ttu-id="582c1-113">Si aún no lo ha hecho, debe habilitar ADM en su cuenta de Amazon.</span><span class="sxs-lookup"><span data-stu-id="582c1-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="582c1-114">El procedimiento se detalla en: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="582c1-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="582c1-115">Una vez finalizado el procedimiento, obtiene:</span><span class="sxs-lookup"><span data-stu-id="582c1-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="582c1-116">Credenciales de OAuth (un identificador de cliente y un secreto de cliente) para que Engagement puede realizar inserciones en sus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="582c1-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="582c1-117">Una clave de API que se debe integrar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="582c1-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="582c1-118">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="582c1-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="582c1-119">Administración de registros de dispositivos</span><span class="sxs-lookup"><span data-stu-id="582c1-119">Managing device registrations</span></span>
<span data-ttu-id="582c1-120">Cada dispositivo debe enviar un comando de registro a los servidores de ADM; en caso contrario, no se puede establecer contacto con ellos.</span><span class="sxs-lookup"><span data-stu-id="582c1-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="582c1-121">Si ya usa la [biblioteca de cliente ADM] y ya ha [integrado ADM], puede ir directamente a android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="582c1-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="582c1-122">Si aún no ha integrado ADM, Engagement tiene una forma más sencilla de habilitarlo en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="582c1-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="582c1-123">Edite su archivo `AndroidManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="582c1-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="582c1-124">Agregue el espacio para nombres de Amazon; el archivo debería empezar así:</span><span class="sxs-lookup"><span data-stu-id="582c1-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="582c1-125">Dentro de la etiqueta `<application/>` , agregue esta sección:</span><span class="sxs-lookup"><span data-stu-id="582c1-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="582c1-126">Después de agregar la etiqueta de Amazon, puede tener un error de compilación si su destino de compilación del proyecto es inferior a Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="582c1-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="582c1-127">Debe usar un destino de compilación **Android 2.1+** (no se preocupe, aún puede disponer de `minSdkVersion` establecido en 4).</span><span class="sxs-lookup"><span data-stu-id="582c1-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="582c1-128">Integre la clave de API de ADM como un recurso siguiendo [este procedimiento].</span><span class="sxs-lookup"><span data-stu-id="582c1-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="582c1-129">A continuación, siga las instrucciones de las secciones siguientes.</span><span class="sxs-lookup"><span data-stu-id="582c1-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="582c1-130">Comunicar el identificador de registro al servicio de inserción de Engagement y recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="582c1-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="582c1-131">Para comunicar el identificador de registro del dispositivo al servicio de inserción de Engagement y recibir sus notificaciones, agregue lo siguiente al archivo de `AndroidManifest.xml`, dentro de la etiqueta `<application/>` (incluso si usa ADM sin Engagement):</span><span class="sxs-lookup"><span data-stu-id="582c1-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="582c1-132">Asegúrese de tener los permisos siguientes en el `AndroidManifest.xml` (antes de la etiqueta `</application>`).</span><span class="sxs-lookup"><span data-stu-id="582c1-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="582c1-133">Conceder credenciales de OAuth de Engagement</span><span class="sxs-lookup"><span data-stu-id="582c1-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="582c1-134">Envíe sus credenciales de OAuth (Id. de cliente y secreto de cliente) en el Portal de interacción. </span><span class="sxs-lookup"><span data-stu-id="582c1-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="582c1-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="582c1-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="582c1-136">[biblioteca de cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="582c1-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="582c1-137">[integrado ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="582c1-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="582c1-138">[este procedimiento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="582c1-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
