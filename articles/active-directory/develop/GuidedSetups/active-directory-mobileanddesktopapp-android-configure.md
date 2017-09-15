---
title: "Introducción a Android en Azure AD v2: configuración | Microsoft Docs"
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
ms.openlocfilehash: 945b09ccdb7537987da33d32d94a3ccacd829ffd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="0d41a-103">Creación de una aplicación (proceso rápido)</span><span class="sxs-lookup"><span data-stu-id="0d41a-103">Create an application (Express)</span></span>
<span data-ttu-id="0d41a-104">Ahora tiene que registrar la aplicación en el *Portal de registro de aplicaciones de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="0d41a-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="0d41a-105">Registre la aplicación en el [Portal de registro de aplicaciones de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure).</span><span class="sxs-lookup"><span data-stu-id="0d41a-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="0d41a-106">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0d41a-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="0d41a-107">Asegúrese de que está activada la opción de configuración paso a paso.</span><span class="sxs-lookup"><span data-stu-id="0d41a-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="0d41a-108">Siga las instrucciones para obtener el identificador de aplicación y péguelo en el código.</span><span class="sxs-lookup"><span data-stu-id="0d41a-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="0d41a-109">Adición de la información de registro de la aplicación a la solución (avanzado)</span><span class="sxs-lookup"><span data-stu-id="0d41a-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="0d41a-110">Ahora tiene que registrar la aplicación en el *Portal de registro de aplicaciones de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="0d41a-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="0d41a-111">Vaya al [Portal de registro de aplicaciones de Microsoft](https://apps.dev.microsoft.com/portal/register-app) para registrar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d41a-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="0d41a-112">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="0d41a-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="0d41a-113">Asegúrese de que está desactivada la opción de configuración paso a paso.</span><span class="sxs-lookup"><span data-stu-id="0d41a-113">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="0d41a-114">Haga clic en `Add Platform`, a continuación, seleccione `Native Application` y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="0d41a-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="0d41a-115">Abra `MainActivity` (en `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="0d41a-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="0d41a-116">Reemplace *[escriba el id. de aplicación aquí]* en la línea que empieza con `final static String CLIENT_ID` por el identificador de aplicación que acaba de registrar:</span><span class="sxs-lookup"><span data-stu-id="0d41a-116">Replace the *[Enter the application Id here]* in the line starting with `final static String CLIENT_ID` with the application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="0d41a-117">Abra `AndroidManifest.xml` (en `app` > `manifests`) Agregue la actividad siguiente al nodo `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="0d41a-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="0d41a-118">De este modo se registra un `BrowserTabActivity` para permitir que el sistema operativo reanude la aplicación después de completar la autenticación:</span><span class="sxs-lookup"><span data-stu-id="0d41a-118">This registers a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>
</li>
</ol>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="0d41a-119">En `BrowserTabActivity`, reemplace `[Enter the application Id here]` por el identificador de aplicación.</span><span class="sxs-lookup"><span data-stu-id="0d41a-119">In the `BrowserTabActivity`, replace `[Enter the application Id here]` with the application ID.</span></span>
</li>
</ol>
