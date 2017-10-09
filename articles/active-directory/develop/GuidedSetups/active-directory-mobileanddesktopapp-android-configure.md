---
title: "aaaAzure AD v2 para introducción de Android: configurar | Documentos de Microsoft"
description: "Cómo puede una aplicación de Android obtener un token de acceso y llamar a las API Graph que requieren tokens de acceso desde el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creación de una aplicación (proceso rápido)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Escriba el nombre de la aplicación y su correo electrónico.
3.  Asegúrese de que está activada la opción de hello para el programa de instalación interactiva
4.  Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Agregar la solución de tooyour información de registro de aplicación (avanzado)
Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:
1. Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación
2. Escriba el nombre de la aplicación y su correo electrónico. 
3. Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva
4. Haga clic en `Add Platform`, a continuación, seleccione `Native Application` y haga clic en Guardar.
5.  Abra `MainActivity` (en `app` > `java` > *`{host}.{namespace}`*)
6.  Reemplace hello *[Escriba aplicación Id. de hello aquí]* en línea hello a partir de `final static String CLIENT_ID` con el Id. de aplicación Hola que acaba de registrar:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Abra `AndroidManifest.xml` (en `app`  >  `manifests`) Hola agregar después actividad demasiado`manifest\application` nodo. Esta forma se registra un `BrowserTabActivity` tooallow Hola tooresume de sistema operativo de la aplicación después de completar la autenticación de hello:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
Hola `BrowserTabActivity`, reemplace `[Enter hello application Id here]` con el identificador de la aplicación hello.
</li>
</ol>
