---
title: "aaaAzure Mobile Engagement Android integración con el SDK"
description: "Procedimientos y actualizaciones más recientes para el SDK de Android para Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="7b438-103">¿Cómo tooIntegrate GCM con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="7b438-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7b438-104">Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.</span><span class="sxs-lookup"><span data-stu-id="7b438-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="7b438-105">Este documento solamente resulta útil si se Hola que ya están integrados llegar a toopush de módulo y plan de Google Play los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7b438-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="7b438-106">las campañas de Reach toointegrate en su aplicación, lea primero cómo tooIntegrate interacción alcanzar en Android.</span><span class="sxs-lookup"><span data-stu-id="7b438-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="7b438-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="7b438-107">Introduction</span></span>
<span data-ttu-id="7b438-108">Integración de GCM permite su toobe de aplicación que se inserta.</span><span class="sxs-lookup"><span data-stu-id="7b438-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="7b438-109">Cargas GCM insertados toohello SDK siempre contienen hello `azme` clave en el objeto de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b438-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="7b438-110">Por lo tanto, si utiliza GCM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.</span><span class="sxs-lookup"><span data-stu-id="7b438-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b438-111">Solo los dispositivos que ejecuten Android 2.2 o versiones posteriores, con Google Play instalado y con una conexión de fondo de Google habilitada, se pueden insertar mediante GCM; sin embargo, puede integrar este código de forma segura en los dispositivos no compatibles (simplemente usa representaciones).</span><span class="sxs-lookup"><span data-stu-id="7b438-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="7b438-112">Creación de un proyecto del Servicio de mensajería en la nube de Google con clave de API</span><span class="sxs-lookup"><span data-stu-id="7b438-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="7b438-113">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="7b438-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="7b438-114">Administración de registros de dispositivos</span><span class="sxs-lookup"><span data-stu-id="7b438-114">Managing device registrations</span></span>
<span data-ttu-id="7b438-115">Cada dispositivo debe enviar un toohello de comando de registro servidores de Google, en caso contrario, no se puede acceder a ellas.</span><span class="sxs-lookup"><span data-stu-id="7b438-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="7b438-116">También puede anular el registro de un dispositivo de notificaciones de GCM (dispositivo Hola se elimina automáticamente si se desinstala la aplicación hello).</span><span class="sxs-lookup"><span data-stu-id="7b438-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="7b438-117">Si no utiliza [SDK de Google Play] o ya no enviar intención de registro de hello, puede hacer que la contratación registrar dispositivo Hola automáticamente para usted.</span><span class="sxs-lookup"><span data-stu-id="7b438-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="7b438-118">tooenable, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiqueta:</span><span class="sxs-lookup"><span data-stu-id="7b438-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="7b438-119">Comunicarse con el servicio de inserción de interacción de toohello de Id. de registro y recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="7b438-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="7b438-120">En orden toocommunicate Hola Id. del registro de hello dispositivo toohello interacción de inserción del servicio y recibir sus notificaciones, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiquetar (incluso si se administran registros de dispositivos):</span><span class="sxs-lookup"><span data-stu-id="7b438-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

<span data-ttu-id="7b438-121">Asegúrese de tener Hola los siguientes permisos en su `AndroidManifest.xml` (después de hello `</application>` etiqueta).</span><span class="sxs-lookup"><span data-stu-id="7b438-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="7b438-122">GRANT Mobile Engagement acceso tooyour clave de API GCM</span><span class="sxs-lookup"><span data-stu-id="7b438-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="7b438-123">Siga [esta guía](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement acceso tooyour clave de API GCM.</span><span class="sxs-lookup"><span data-stu-id="7b438-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[SDK de Google Play]:https://developers.google.com/cloud-messaging/android/start
