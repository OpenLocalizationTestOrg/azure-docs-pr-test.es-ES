---
title: "aaaAzure AD v2 JS SPA guiada por el programa de instalación: configurar | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones SPA de JavaScript a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="7a7ab-103">Registrar su aplicación</span><span class="sxs-lookup"><span data-stu-id="7a7ab-103">Register your application</span></span>

<span data-ttu-id="7a7ab-104">Hay varias maneras toocreate una aplicación, seleccione uno de ellos:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="7a7ab-105">Opción 1: Registro de la aplicación (modo Rápido)</span><span class="sxs-lookup"><span data-stu-id="7a7ab-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="7a7ab-106">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="7a7ab-107">Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="7a7ab-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="7a7ab-108">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7a7ab-109">Asegúrese de opción de hello seguro *el programa de instalación interactiva* está activada</span><span class="sxs-lookup"><span data-stu-id="7a7ab-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="7a7ab-110">Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código</span><span class="sxs-lookup"><span data-stu-id="7a7ab-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="7a7ab-111">Opción 2: Registro de la aplicación (modo Avanzado)</span><span class="sxs-lookup"><span data-stu-id="7a7ab-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="7a7ab-112">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación</span><span class="sxs-lookup"><span data-stu-id="7a7ab-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="7a7ab-113">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="7a7ab-114">Asegúrese de opción de hello seguro *el programa de instalación interactiva* está desactivada</span><span class="sxs-lookup"><span data-stu-id="7a7ab-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="7a7ab-115">Haga clic en `Add Platform` y luego en `Web`.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="7a7ab-116">Agregar hello `Redirect URL` que corresponden a direcciones URL de la aplicación toohello basándose en el servidor web.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="7a7ab-117">Vea las secciones de Hola a continuación para obtener instrucciones sobre cómo tooset / obtener la dirección URL de redireccionamiento de hello en Visual Studio y Python.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="7a7ab-118">Haga clic en *Guardar*</span><span class="sxs-lookup"><span data-stu-id="7a7ab-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="7a7ab-119">Instrucciones en Visual Studio para obtener la dirección URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="7a7ab-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="7a7ab-120">Siga Hola instrucciones tooobtain la dirección URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="7a7ab-121">En *el Explorador de soluciones*, seleccione el proyecto de Hola y mire hello `Properties` ventana (si no ve una ventana de propiedades, presione `F4`)</span><span class="sxs-lookup"><span data-stu-id="7a7ab-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="7a7ab-122">Copiar valor de Hola de `URL` toohello Portapapeles:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="7a7ab-123">![Propiedades del proyecto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="7a7ab-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="7a7ab-124">Cambiar atrás toohello *Portal de registro de aplicación* y pegue el valor de Hola como un `Redirect URL` y haga clic en 'Guardar'</span><span class="sxs-lookup"><span data-stu-id="7a7ab-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="7a7ab-125">Configuración de la dirección URL de redireccionamiento para Python</span><span class="sxs-lookup"><span data-stu-id="7a7ab-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="7a7ab-126">Para Python, puede establecer el puerto de servidor web de Hola a través de la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="7a7ab-127">Este programa de instalación guiada utiliza el puerto de hello 8080 para referencia pero Siéntase libre toouse cualquier puerto disponible.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="7a7ab-128">En cualquier caso, siga instrucciones hello tooset una dirección URL de redireccionamiento en información de registro de aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="7a7ab-129">Cambiar toohello Atrás *Portal de registro de aplicación* y establecer `http://localhost:8080/` como un `Redirect URL`, o usar `http://localhost:[port]/` si usa un puerto TCP personalizado (donde *[puerto]* es el puerto TCP personalizado Hola número) y haga clic en 'Guardar'</span><span class="sxs-lookup"><span data-stu-id="7a7ab-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="7a7ab-130">Configuración de JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="7a7ab-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="7a7ab-131">Cree un archivo denominado `msalconfig.js` que contiene información de registro de aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="7a7ab-132">Si usas el proyecto de Visual Studio, seleccione hello (carpeta raíz del proyecto), haga clic en y seleccione: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="7a7ab-133">Asígnele el nombre `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="7a7ab-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="7a7ab-134">Agregar Hola después código tooyour `msalconfig.js` archivo:</span><span class="sxs-lookup"><span data-stu-id="7a7ab-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="7a7ab-135">Reemplace <code>Enter_the_Application_Id_here</code> con hello que acaba de registrar el identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="7a7ab-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
