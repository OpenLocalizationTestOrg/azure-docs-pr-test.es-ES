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
## <a name="create-an-application-express"></a><span data-ttu-id="c1e6f-103">Creación de una aplicación (proceso rápido)</span><span class="sxs-lookup"><span data-stu-id="c1e6f-103">Create an application (Express)</span></span>
<span data-ttu-id="c1e6f-104">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="c1e6f-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="c1e6f-105">Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="c1e6f-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="c1e6f-106">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c1e6f-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="c1e6f-107">Asegúrese de que está activada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="c1e6f-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="c1e6f-108">Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código</span><span class="sxs-lookup"><span data-stu-id="c1e6f-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="c1e6f-109">Agregar la solución de tooyour información de registro de aplicación (avanzado)</span><span class="sxs-lookup"><span data-stu-id="c1e6f-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="c1e6f-110">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="c1e6f-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="c1e6f-111">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación</span><span class="sxs-lookup"><span data-stu-id="c1e6f-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="c1e6f-112">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="c1e6f-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="c1e6f-113">Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="c1e6f-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="c1e6f-114">Haga clic en `Add Platform`, a continuación, seleccione `Native Application` y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="c1e6f-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="c1e6f-115">Abra `MainActivity` (en `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="c1e6f-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="c1e6f-116">Reemplace hello *[Escriba aplicación Id. de hello aquí]* en línea hello a partir de `final static String CLIENT_ID` con el Id. de aplicación Hola que acaba de registrar:</span><span class="sxs-lookup"><span data-stu-id="c1e6f-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="c1e6f-117">Abra `AndroidManifest.xml` (en `app`  >  `manifests`) Hola agregar después actividad demasiado`manifest\application` nodo.</span><span class="sxs-lookup"><span data-stu-id="c1e6f-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="c1e6f-118">Esta forma se registra un `BrowserTabActivity` tooallow Hola tooresume de sistema operativo de la aplicación después de completar la autenticación de hello:</span><span class="sxs-lookup"><span data-stu-id="c1e6f-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="c1e6f-119">Hola `BrowserTabActivity`, reemplace `[Enter hello application Id here]` con el identificador de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c1e6f-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
