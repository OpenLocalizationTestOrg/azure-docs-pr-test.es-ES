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
# <a name="how-toointegrate-adm-with-engagement"></a>¿Cómo tooIntegrate ADM con interacción
> [!IMPORTANT]
> Debe seguir el procedimiento de integración de hello descrito en hello cómo documentar tooIntegrate interacción en Android antes de seguir a esta guía.
> 
> Este documento solamente resulta útil si ya integrado Hola alcance módulo y el plan toopush Amazon dispositivos. las campañas de Reach toointegrate en su aplicación, lea primero cómo tooIntegrate interacción alcanzar en Android.
> 
> 

## <a name="introduction"></a>Introducción
Integración de ADM permite su toobe aplicación insertado al elegir como destino dispositivos Android de Amazon.

Cargas ADM insertados toohello SDK siempre contienen hello `azme` clave en el objeto de datos de Hola. Por lo tanto, si usa ADM para otra finalidad en la aplicación, puede filtrar las inserciones basándose en esa clave.

> [!IMPORTANT]
> Solo los dispositivos Kindle de Amazon que ejecutan Android 4.0.3 o versiones posteriores son compatibles con la mensajería de dispositivos de Amazon; Sin embargo, puede integrar este código de forma segura en otros dispositivos.
> 
> 

## <a name="sign-up-tooadm"></a>Suscríbase tooADM
Si aún no lo ha hecho, debe habilitar ADM en su cuenta de Amazon.

procedimiento de Hola se detalla en: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Al completar el procedimiento de hello, obtendrá:

* OAuth credenciales (un identificador de cliente y un secreto de cliente) para toopush capaz de contratación toobe los dispositivos.
* Una clave de API que se debe integrar en la aplicación.

## <a name="sdk-integration"></a>Integración de SDK
### <a name="managing-device-registrations"></a>Administración de registros de dispositivos
Cada dispositivo debe enviar un toohello de comando de registro servidores ADM, en caso contrario, no se puede acceder a ellas.

Si ya utiliza hello [biblioteca de cliente ADM]y ya tienen [integrado ADM] puede ir directamente tooandroid-sdk-adm-receive.

Si no ha integrado ADM aún, interacción tiene un tooenable de manera más sencilla en la aplicación:

Edite su archivo `AndroidManifest.xml`:

* Agregue Hola espacio de nombres de Amazon, debe empezar el archivo hello similar al siguiente:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Hola interior `<application/>` etiqueta, agregue esta sección:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Después de agregar la etiqueta de amazon hello, habrá un error de compilación si el destino de compilación del proyecto está por debajo de Android 2.1. Tendrá que toouse una **Android 2.1 +** destino de compilación (no se preocupe, todavía puede tener un `minSdkVersion` establecer too4).
* Integrar Hola clave de API de ADM como un recurso siguiendo [este procedimiento].

Siga las instrucciones de Hola de las secciones siguientes se Hola.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicarse con el servicio de inserción de interacción de toohello de Id. de registro y recibir notificaciones
En orden toocommunicate Hola Id. del registro de hello dispositivo toohello interacción de inserción del servicio y recibir sus notificaciones, agregar Hola después tooyour `AndroidManifest.xml` archivo, dentro de hello `<application/>` etiquetar (incluso si se utiliza ADM sin interacción):

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

Asegúrese de tener Hola los siguientes permisos en su `AndroidManifest.xml` (antes de hello `</application>` etiqueta).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Conceder credenciales de OAuth de Engagement
Envíe sus credenciales de OAuth (Id. de cliente y secreto de cliente) en el Portal de interacción. 

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[biblioteca de cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrado ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[este procedimiento]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
