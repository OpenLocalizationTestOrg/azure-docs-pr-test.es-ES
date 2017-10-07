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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>¿Cómo tooIntegrate GCM con Mobile Engagement
> [!IMPORTANT]
> Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.
> 
> Este documento solamente resulta útil si se Hola que ya están integrados llegar a toopush de módulo y plan de Google Play los dispositivos. las campañas de Reach toointegrate en su aplicación, lea primero cómo tooIntegrate interacción alcanzar en Android.
> 
> 

## <a name="introduction"></a>Introducción
Integración de GCM permite su toobe de aplicación que se inserta.

Cargas GCM insertados toohello SDK siempre contienen hello `azme` clave en el objeto de datos de Hola. Por lo tanto, si utiliza GCM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.

> [!IMPORTANT]
> Solo los dispositivos que ejecuten Android 2.2 o versiones posteriores, con Google Play instalado y con una conexión de fondo de Google habilitada, se pueden insertar mediante GCM; sin embargo, puede integrar este código de forma segura en los dispositivos no compatibles (simplemente usa representaciones).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Creación de un proyecto del Servicio de mensajería en la nube de Google con clave de API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Integración de SDK
### <a name="managing-device-registrations"></a>Administración de registros de dispositivos
Cada dispositivo debe enviar un toohello de comando de registro servidores de Google, en caso contrario, no se puede acceder a ellas.

También puede anular el registro de un dispositivo de notificaciones de GCM (dispositivo Hola se elimina automáticamente si se desinstala la aplicación hello).

Si no utiliza [SDK de Google Play] o ya no enviar intención de registro de hello, puede hacer que la contratación registrar dispositivo Hola automáticamente para usted.

tooenable, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiqueta:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicarse con el servicio de inserción de interacción de toohello de Id. de registro y recibir notificaciones
En orden toocommunicate Hola Id. del registro de hello dispositivo toohello interacción de inserción del servicio y recibir sus notificaciones, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiquetar (incluso si se administran registros de dispositivos):

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

Asegúrese de tener Hola los siguientes permisos en su `AndroidManifest.xml` (después de hello `</application>` etiqueta).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>GRANT Mobile Engagement acceso tooyour clave de API GCM
Siga [esta guía](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement acceso tooyour clave de API GCM.

[SDK de Google Play]:https://developers.google.com/cloud-messaging/android/start
