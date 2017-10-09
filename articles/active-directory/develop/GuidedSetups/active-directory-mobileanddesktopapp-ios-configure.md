---
title: "Introducción a la aaaAzure AD v2 iOS: configurar | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones de iOS (Swift) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="fc37c-103">Creación de una aplicación (proceso rápido)</span><span class="sxs-lookup"><span data-stu-id="fc37c-103">Create an application (Express)</span></span>
<span data-ttu-id="fc37c-104">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="fc37c-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="fc37c-105">Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="fc37c-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="fc37c-106">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="fc37c-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="fc37c-107">Asegúrese de que está activada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="fc37c-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="fc37c-108">Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código</span><span class="sxs-lookup"><span data-stu-id="fc37c-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="fc37c-109">Agregar la solución de tooyour información de registro de aplicación (avanzado)</span><span class="sxs-lookup"><span data-stu-id="fc37c-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="fc37c-110">Vaya demasiado[Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="fc37c-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="fc37c-111">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="fc37c-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="fc37c-112">Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="fc37c-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="fc37c-113">Haga clic en `Add Platform`, seleccione `Native Application` y haga clic en `Save`.</span><span class="sxs-lookup"><span data-stu-id="fc37c-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="fc37c-114">Volver atrás tooXcode.</span><span class="sxs-lookup"><span data-stu-id="fc37c-114">Go back tooXcode.</span></span> <span data-ttu-id="fc37c-115">En `ViewController.swift`, reemplace la línea hello que empieza por '`let kClientID`' con el Id. de aplicación Hola que acaba de registrar:</span><span class="sxs-lookup"><span data-stu-id="fc37c-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="fc37c-116">Control + clic <code>Info.plist</code> toobring una copia de seguridad del menú contextual hello y, a continuación, haga clic en: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="fc37c-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="fc37c-117">En hello <code>dict</code> nodo raíz, agregue Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="fc37c-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="fc37c-118">Reemplace <i> <code>[Your_Application_Id_Here]</code> </i> con hello que acaba de registrar el identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="fc37c-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
