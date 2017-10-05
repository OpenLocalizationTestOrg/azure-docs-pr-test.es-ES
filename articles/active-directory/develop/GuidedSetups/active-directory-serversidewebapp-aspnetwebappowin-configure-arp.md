---
title: "Introducción al servidor web de ASP.NET de Azure AD v2: configuración | Microsoft Docs"
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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="dcf1c-103">Configuración de la aplicación web ASP.NET con la información de registro de la aplicación</span><span class="sxs-lookup"><span data-stu-id="dcf1c-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="dcf1c-104">En este paso, se configura el proyecto para usar SSL y, a continuación, se usa la dirección URL de SSL para configurar la información de registro de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dcf1c-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="dcf1c-105">Después, se agrega la información de registro de la aplicación a la solución a través de *web.config*.</span><span class="sxs-lookup"><span data-stu-id="dcf1c-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="dcf1c-106">En el Explorador de soluciones, seleccione el proyecto y fíjese en la ventana `Properties` (si no ve una ventana de propiedades, presione F4).</span><span class="sxs-lookup"><span data-stu-id="dcf1c-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="dcf1c-107">Cambie `SSL Enabled` a `True`.</span><span class="sxs-lookup"><span data-stu-id="dcf1c-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="dcf1c-108">Copie el valor de `SSL URL` anterior y péguelo en el campo `Redirect URL` en la parte superior de esta página; a continuación, haga clic en *Actualizar*:</span><span class="sxs-lookup"><span data-stu-id="dcf1c-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="dcf1c-109">![Propiedades del proyecto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="dcf1c-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="dcf1c-110">Agregue lo siguiente en el archivo `web.config` ubicado en la carpeta raíz, en la sección `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="dcf1c-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
