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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="b28bb-103">Agregar aplicación de tooyour de información de registro de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="b28bb-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="b28bb-104">En este paso, necesita proyecto tooyour de tooadd Hola Id. de cliente.</span><span class="sxs-lookup"><span data-stu-id="b28bb-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="b28bb-105">Abra `MainActivity` (en `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="b28bb-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="b28bb-106">Reemplace la línea hello a partir de `final static String CLIENT_ID` con:</span><span class="sxs-lookup"><span data-stu-id="b28bb-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="b28bb-107">Abra `app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="b28bb-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="b28bb-108">Agregar Hola después actividad demasiado`manifest\application` nodo.</span><span class="sxs-lookup"><span data-stu-id="b28bb-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="b28bb-109">En este registro un `BrowserTabActivity` tooallow Hola tooresume de sistema operativo de la aplicación después de completar la autenticación de hello:</span><span class="sxs-lookup"><span data-stu-id="b28bb-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

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

### <a name="what-is-next"></a><span data-ttu-id="b28bb-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b28bb-110">What is Next</span></span>

[<span data-ttu-id="b28bb-111">Probar y validar</span><span class="sxs-lookup"><span data-stu-id="b28bb-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
