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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Agregar aplicación de tooyour de información de registro de la aplicación hello

En este paso, necesita proyecto tooyour de tooadd Hola Id. de cliente.

1.  Abra `MainActivity` (en `app` > `java` > *`{host}.{namespace}`*)
2.  Reemplace la línea hello a partir de `final static String CLIENT_ID` con:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Abra `app` > `manifests` > `AndroidManifest.xml`
4. Agregar Hola después actividad demasiado`manifest\application` nodo. En este registro un `BrowserTabActivity` tooallow Hola tooresume de sistema operativo de la aplicación después de completar la autenticación de hello:

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

### <a name="what-is-next"></a>Pasos siguientes

[Probar y validar](active-directory-mobileanddesktopapp-android-test.md)
