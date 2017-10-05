---
title: "Integración del SDK de Android para Azure Mobile Engagement"
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="a0dd3-103">Integración de GCM con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a0dd3-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a0dd3-104">Debe seguir el procedimiento de integración descrito en el documento Integración de Engagement en Android antes de seguir con esta guía.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="a0dd3-105">Este documento es útil solo si ya integró el módulo de cobertura y el plan para insertar dispositivos de Google Play.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="a0dd3-106">Para integrar campañas de Reach en la aplicación, lea primero Integración de Engagement Reach en Android.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a0dd3-107">Introducción</span><span class="sxs-lookup"><span data-stu-id="a0dd3-107">Introduction</span></span>
<span data-ttu-id="a0dd3-108">La integración de GCM permite realizar inserciones en su aplicación.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="a0dd3-109">Las cargas GCM insertadas en el SDK siempre contienen la clave `azme` en el objeto de datos.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="a0dd3-110">Por lo tanto, si utiliza GCM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0dd3-111">Solo los dispositivos que ejecuten Android 2.2 o versiones posteriores, con Google Play instalado y con una conexión de fondo de Google habilitada, se pueden insertar mediante GCM; sin embargo, puede integrar este código de forma segura en los dispositivos no compatibles (simplemente usa representaciones).</span><span class="sxs-lookup"><span data-stu-id="a0dd3-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="a0dd3-112">Creación de un proyecto del Servicio de mensajería en la nube de Google con clave de API</span><span class="sxs-lookup"><span data-stu-id="a0dd3-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="a0dd3-113">Integración de SDK</span><span class="sxs-lookup"><span data-stu-id="a0dd3-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="a0dd3-114">Administración de registros de dispositivos</span><span class="sxs-lookup"><span data-stu-id="a0dd3-114">Managing device registrations</span></span>
<span data-ttu-id="a0dd3-115">Cada dispositivo debe enviar un comando de registro a los servidores de Google; en caso contrario, no se puede establecer la conexión.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="a0dd3-116">También puede anular el registro de un dispositivo de las notificaciones de GCM (el dispositivo se elimina automáticamente si se desinstala la aplicación).</span><span class="sxs-lookup"><span data-stu-id="a0dd3-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="a0dd3-117">Si no usa el [SDK de Google Play] o no ha enviado aún el intento de registro, puede hacer que Engagement registre el dispositivo automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="a0dd3-118">Para habilitar esta opción, agregue lo siguiente al archivo de `AndroidManifest.xml`, dentro de la etiqueta `<application/>`:</span><span class="sxs-lookup"><span data-stu-id="a0dd3-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="a0dd3-119">Comunicar el identificador de registro al servicio de inserción de Engagement y recibir notificaciones</span><span class="sxs-lookup"><span data-stu-id="a0dd3-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="a0dd3-120">Para comunicar el identificador de registro del dispositivo al servicio de inserción de Engagement y recibir notificaciones, agregue lo siguiente al archivo de `AndroidManifest.xml`, dentro de la etiqueta `<application/>` (aunque administre registros de dispositivos):</span><span class="sxs-lookup"><span data-stu-id="a0dd3-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="a0dd3-121">Asegúrese de tener los permisos siguientes en `AndroidManifest.xml` (después de la etiqueta `</application>`).</span><span class="sxs-lookup"><span data-stu-id="a0dd3-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="a0dd3-122">Conceder acceso de Mobile Engagement a la clave de API de GCM</span><span class="sxs-lookup"><span data-stu-id="a0dd3-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="a0dd3-123">Siga [esta guía](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) para conceder acceso de Mobile Engagement a la clave de API de GCM.</span><span class="sxs-lookup"><span data-stu-id="a0dd3-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="a0dd3-124">[SDK de Google Play]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="a0dd3-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
