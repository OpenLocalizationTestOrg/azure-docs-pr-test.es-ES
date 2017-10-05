---
title: "Publicación de aplicaciones cliente nativas: Azure AD | Microsoft Docs"
description: "Explica cómo habilitar las aplicaciones cliente nativas para comunicarse con el conector del proxy de la aplicación de Azure AD para proporcionar acceso remoto seguro a las aplicaciones locales."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="040fd-103">Habilitación de las aplicaciones cliente nativas para interactuar con el proxy de la aplicación</span><span class="sxs-lookup"><span data-stu-id="040fd-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="040fd-104">Además de las aplicaciones web, el proxy de la aplicación de Azure Active Directory también puede utilizarse para publicar las aplicaciones cliente nativas.</span><span class="sxs-lookup"><span data-stu-id="040fd-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="040fd-105">Las aplicaciones cliente nativas son distintas de las aplicaciones web porque se instalan en un dispositivo, mientras se tiene acceso a las aplicaciones web a través de un explorador.</span><span class="sxs-lookup"><span data-stu-id="040fd-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="040fd-106">El proxy de la aplicación admite aplicaciones de cliente nativo al aceptar tokens emitidos por Azure AD que se envían en encabezados HTTP de autorización estándar.</span><span class="sxs-lookup"><span data-stu-id="040fd-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relación entre los usuarios finales, Azure Active Directory y las aplicaciones publicadas](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="040fd-108">Utilice la biblioteca de Autenticación de Azure AD, que se encarga de la autenticación y admite muchos de los entornos de cliente, para publicar aplicaciones nativas.</span><span class="sxs-lookup"><span data-stu-id="040fd-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="040fd-109">El proxy de la aplicación se adapta a la [aplicación nativa para el escenario de Web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="040fd-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="040fd-110">Este artículo le guiará por los cuatro pasos para publicar una aplicación nativa con el proxy de aplicación y la biblioteca de Autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="040fd-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="040fd-111">Paso 1: Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="040fd-111">Step 1: Publish your application</span></span>
<span data-ttu-id="040fd-112">Publique su aplicación de proxy al igual que haría con cualquier otra aplicación y asigne a los usuarios el acceso a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="040fd-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="040fd-113">Para más información, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="040fd-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="040fd-114">Paso 2: Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="040fd-114">Step 2: Configure your application</span></span>
<span data-ttu-id="040fd-115">Configure su aplicación nativa de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="040fd-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="040fd-116">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="040fd-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="040fd-117">Vaya a **Azure Active Directory** > **Registros de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="040fd-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="040fd-118">Seleccione **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="040fd-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="040fd-119">Especifique un nombre para la aplicación, seleccione **Nativo** como tipo de aplicación y proporcione el URI de redirección para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="040fd-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Creación de un registro de aplicaciones](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="040fd-121">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="040fd-121">Select **Create**.</span></span>

<span data-ttu-id="040fd-122">Para más información sobre cómo crear un registro de aplicación, consulte [Integración de aplicaciones con Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="040fd-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="040fd-123">Paso 3: Conceder acceso a otras aplicaciones</span><span class="sxs-lookup"><span data-stu-id="040fd-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="040fd-124">Habilite la aplicación nativa para que se exponga a otras aplicaciones en el directorio:</span><span class="sxs-lookup"><span data-stu-id="040fd-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="040fd-125">Todavía en **Registros de aplicaciones**, seleccione la aplicación nativa que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="040fd-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="040fd-126">Seleccione **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="040fd-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="040fd-127">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="040fd-127">Select **Add**.</span></span>
4. <span data-ttu-id="040fd-128">Abra el primer paso, **Seleccionar una API**.</span><span class="sxs-lookup"><span data-stu-id="040fd-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="040fd-129">Use la barra de búsqueda para encontrar la aplicación de proxy de la aplicación que ha publicado en la primera sección.</span><span class="sxs-lookup"><span data-stu-id="040fd-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="040fd-130">Elija la aplicación y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="040fd-130">Choose that app, then click **Select**.</span></span> 

   ![Búsqueda de la aplicación de proxy](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="040fd-132">Abra el segundo paso, **Seleccionar permisos**.</span><span class="sxs-lookup"><span data-stu-id="040fd-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="040fd-133">Utilice la casilla para conceder el acceso de la aplicación nativa a la aplicación de proxy y, después, haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="040fd-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Concesión de acceso a la aplicación de proxy](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="040fd-135">Seleccione **Listo**.</span><span class="sxs-lookup"><span data-stu-id="040fd-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="040fd-136">Paso 4: Editar la biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="040fd-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="040fd-137">Edite el código de la aplicación nativa en el contexto de autenticación de Active Directory Authentication Library (ADAL) para incluir el siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="040fd-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="040fd-138">Las variables del código de ejemplo deben reemplazarse como sigue:</span><span class="sxs-lookup"><span data-stu-id="040fd-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="040fd-139">**Tenant ID** puede encontrarse en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="040fd-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="040fd-140">Vaya a **Azure Active Directory** > **Propiedades** y copie el identificador de directorio.</span><span class="sxs-lookup"><span data-stu-id="040fd-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="040fd-141">**External URL** es la dirección URL de front-end que ha especificado en la aplicación proxy.</span><span class="sxs-lookup"><span data-stu-id="040fd-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="040fd-142">Para buscar este valor, vaya a la sección **Proxy de la aplicación** de la aplicación de proxy.</span><span class="sxs-lookup"><span data-stu-id="040fd-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="040fd-143">La variable **App ID** de la aplicación nativa se encuentra en la página **Propiedades** de la aplicación nativa.</span><span class="sxs-lookup"><span data-stu-id="040fd-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="040fd-144">**Redirect URI of the native app** se puede encontrar en la página**URI de redirección** de la aplicación nativa.</span><span class="sxs-lookup"><span data-stu-id="040fd-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="040fd-145">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="040fd-145">See also</span></span>

<span data-ttu-id="040fd-146">Para más información sobre el flujo de la aplicación nativa, consulte el escenario de [Aplicación nativa a API web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="040fd-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="040fd-147">Para ver las últimas noticias y actualizaciones, consulte el [blog Application Proxy](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="040fd-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
