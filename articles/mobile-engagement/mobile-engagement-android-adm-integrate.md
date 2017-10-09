---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="c0241-103">¿Cómo tooIntegrate ADM con interacción</span><span class="sxs-lookup"><span data-stu-id="c0241-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c0241-104">Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.</span><span class="sxs-lookup"><span data-stu-id="c0241-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="c0241-105">Este documento solamente resulta útil si ya integrado Hola alcance módulo y el plan toopush Amazon dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c0241-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="c0241-106">las campañas de Reach toointegrate en su aplicación, lea primero cómo tooIntegrate interacción alcanzar en Android.</span><span class="sxs-lookup"><span data-stu-id="c0241-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="c0241-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="c0241-107">Introduction</span></span>
<span data-ttu-id="c0241-108">Integración de ADM permite su toobe aplicación insertado al elegir como destino dispositivos Android de Amazon.</span><span class="sxs-lookup"><span data-stu-id="c0241-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="c0241-109">Cargas ADM insertados toohello SDK siempre contienen hello `azme` clave en el objeto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c0241-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="c0241-110">Por lo tanto, si usa ADM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.</span><span class="sxs-lookup"><span data-stu-id="c0241-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0241-111">Solo los dispositivos Kindle de Amazon que ejecutan Android 4.0.3 o versiones posteriores son compatibles con la mensajería de dispositivos de Amazon; Sin embargo, puede integrar este código de forma segura en otros dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c0241-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="c0241-112">Suscríbase tooADM</span><span class="sxs-lookup"><span data-stu-id="c0241-112">Sign up tooADM</span></span>
<span data-ttu-id="c0241-113">Si aún no lo ha hecho, debe habilitar ADM en su cuenta de Amazon.</span><span class="sxs-lookup"><span data-stu-id="c0241-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="c0241-114">procedimiento de Hola se detalla en: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="c0241-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="c0241-115">Al completar el procedimiento de hello, obtendrá:</span><span class="sxs-lookup"><span data-stu-id="c0241-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="c0241-116">OAuth credenciales (un identificador de cliente y un secreto de cliente) para toopush capaz de contratación toobe los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c0241-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="c0241-117">Una clave de API que se debe integrar en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c0241-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="c0241-118">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="c0241-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="c0241-119">Administración de registros de dispositivos</span><span class="sxs-lookup"><span data-stu-id="c0241-119">Managing device registrations</span></span>
<span data-ttu-id="c0241-120">Cada dispositivo debe enviar un toohello de comando de registro servidores ADM, en caso contrario, no se puede acceder a ellas.</span><span class="sxs-lookup"><span data-stu-id="c0241-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="c0241-121">Si ya utiliza hello [biblioteca de cliente ADM]y ya tienen [integrado ADM] puede ir directamente tooandroid-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="c0241-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="c0241-122">Si no ha integrado ADM aún, interacción tiene un tooenable de manera más sencilla en la aplicación:</span><span class="sxs-lookup"><span data-stu-id="c0241-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="c0241-123">Edite su archivo `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="c0241-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="c0241-124">Agregue Hola espacio de nombres de Amazon, debe empezar el archivo hello similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c0241-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="c0241-125">Hola interior `<application/>` etiqueta, agregue esta sección:</span><span class="sxs-lookup"><span data-stu-id="c0241-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="c0241-126">Después de agregar la etiqueta de amazon hello, habrá un error de compilación si el destino de compilación del proyecto está por debajo de Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="c0241-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="c0241-127">Tendrá que toouse una **Android 2.1 +** destino de compilación (no se preocupe, todavía puede tener un `minSdkVersion` establecer too4).</span><span class="sxs-lookup"><span data-stu-id="c0241-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="c0241-128">Integrar Hola clave de API de ADM como un recurso siguiendo [este procedimiento].</span><span class="sxs-lookup"><span data-stu-id="c0241-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="c0241-129">Siga las instrucciones de Hola de las secciones siguientes se Hola.</span><span class="sxs-lookup"><span data-stu-id="c0241-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="c0241-130">Comunicarse con el servicio de inserción de interacción de toohello de Id. de registro y recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="c0241-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="c0241-131">En orden toocommunicate Hola Id. del registro de hello dispositivo toohello interacción de inserción del servicio y recibir sus notificaciones, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiquetar (incluso si se utiliza ADM sin interacción):</span><span class="sxs-lookup"><span data-stu-id="c0241-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="c0241-132">Asegúrese de tener Hola los siguientes permisos en su `AndroidManifest.xml` (antes de hello `</application>` etiqueta).</span><span class="sxs-lookup"><span data-stu-id="c0241-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="c0241-133">Conceder credenciales de OAuth de Engagement</span><span class="sxs-lookup"><span data-stu-id="c0241-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="c0241-134">Envíe sus credenciales de OAuth (Id. de cliente y secreto de cliente) en el Portal de interacción. </span><span class="sxs-lookup"><span data-stu-id="c0241-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteca de cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrado ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[este procedimiento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
