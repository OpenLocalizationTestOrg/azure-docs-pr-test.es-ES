---
title: "aaaAzure AD v2 ASP.NET Web Server Introducción - Config | Documentos de Microsoft"
description: "Implementación de inicio de sesión de Microsoft en una solución ASP.NET con una aplicación basada en un explorador web tradicional mediante el estándar OpenID Connect"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="bb917-103">Creación de una aplicación (proceso rápido)</span><span class="sxs-lookup"><span data-stu-id="bb917-103">Create an application (Express)</span></span>
<span data-ttu-id="bb917-104">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="bb917-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bb917-105">Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="bb917-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="bb917-106">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="bb917-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="bb917-107">Asegúrese de que está activada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="bb917-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="bb917-108">Siga las instrucciones de hello tooadd una aplicación de tooyour de dirección URL de redireccionamiento</span><span class="sxs-lookup"><span data-stu-id="bb917-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="bb917-109">Agregar la solución de tooyour información de registro de aplicación (avanzado)</span><span class="sxs-lookup"><span data-stu-id="bb917-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="bb917-110">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="bb917-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="bb917-111">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación</span><span class="sxs-lookup"><span data-stu-id="bb917-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="bb917-112">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="bb917-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="bb917-113">Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="bb917-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="bb917-114">Haga clic en `Add Platform` y luego en `Web`.</span><span class="sxs-lookup"><span data-stu-id="bb917-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="bb917-115">Volver atrás tooVisual Studio y, en el Explorador de soluciones, seleccione el proyecto de Hola y mire la ventana de propiedades de hello (si no ve una ventana de propiedades, presione F4)</span><span class="sxs-lookup"><span data-stu-id="bb917-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="bb917-116">Cambiar también SSL habilitado`True`</span><span class="sxs-lookup"><span data-stu-id="bb917-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="bb917-117">Copiar dirección URL de SSL de Hola y agregar esta lista de toohello de dirección URL de URL de redireccionamiento en la lista del Portal de registro de hello de URL de redireccionamiento:</span><span class="sxs-lookup"><span data-stu-id="bb917-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Propiedades del proyecto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="bb917-119">Agregue los siguiente hello en `web.config` ubicado en carpeta de raíz de hello en sección Hola `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="bb917-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="bb917-120">Reemplace `ClientId` con hello que acaba de registrar el identificador de aplicación</span><span class="sxs-lookup"><span data-stu-id="bb917-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="bb917-121">Reemplace `redirectUri` con hello dirección URL de SSL del proyecto</span><span class="sxs-lookup"><span data-stu-id="bb917-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
