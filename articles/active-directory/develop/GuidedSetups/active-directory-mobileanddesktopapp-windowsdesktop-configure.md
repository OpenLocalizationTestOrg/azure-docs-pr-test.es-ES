---
title: "aaaAzure AD v2 escritorio Introducción a Windows - Configuración | Documentos de Microsoft"
description: "Cómo puede obtener una aplicación .NET de escritorio de Windows (XAML) un token de acceso y llamar a una API protegida por un punto de conexión de Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="ee3a8-104">Creación de una aplicación (proceso rápido)</span><span class="sxs-lookup"><span data-stu-id="ee3a8-104">Create an application (Express)</span></span>
<span data-ttu-id="ee3a8-105">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ee3a8-106">Registrar la aplicación a través de hello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="ee3a8-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="ee3a8-107">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ee3a8-108">Asegúrese de que está activada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="ee3a8-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="ee3a8-109">Siga el identificador de la aplicación de hello instrucciones tooobtain hello y péguelo en el código</span><span class="sxs-lookup"><span data-stu-id="ee3a8-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="ee3a8-110">Agregar la solución de tooyour información de registro de aplicación (avanzado)</span><span class="sxs-lookup"><span data-stu-id="ee3a8-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="ee3a8-111">Ahora deberá tooregister la aplicación Hola *Portal de registro de aplicación de Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ee3a8-112">Vaya toohello [Portal de registro de aplicación de Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister una aplicación</span><span class="sxs-lookup"><span data-stu-id="ee3a8-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="ee3a8-113">Escriba el nombre de la aplicación y su correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="ee3a8-114">Asegúrese de que está desactivada la opción de hello para el programa de instalación interactiva</span><span class="sxs-lookup"><span data-stu-id="ee3a8-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="ee3a8-115">Haga clic en `Add Platform`, a continuación, seleccione `Native Application` y haga clic en Guardar.</span><span class="sxs-lookup"><span data-stu-id="ee3a8-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="ee3a8-116">Copiar Hola GUID de Id. de aplicación, vuelva tooVisual Studio, abra `App.xaml.cs` y reemplace `your_client_id_here` con hello que acaba de registrar el identificador de aplicación:</span><span class="sxs-lookup"><span data-stu-id="ee3a8-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
