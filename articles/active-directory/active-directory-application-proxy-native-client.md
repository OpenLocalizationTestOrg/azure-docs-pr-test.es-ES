---
title: las aplicaciones cliente nativas aaaPublish - Azure AD | Documentos de Microsoft
description: "Explica cómo tooenable toocommunicate de aplicaciones de cliente nativo con el conector del Proxy de aplicación de Azure AD tooprovide el acceso remoto seguro tooyour local las aplicaciones."
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
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="4b77a-103">Cómo tooenable toointeract de aplicaciones de cliente nativo con el proxy de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4b77a-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="4b77a-104">En las aplicaciones de tooweb de adición, Proxy de aplicación de Azure Active Directory también pueden ser toopublish usa las aplicaciones cliente nativas.</span><span class="sxs-lookup"><span data-stu-id="4b77a-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="4b77a-105">Las aplicaciones cliente nativas son distintas de las aplicaciones web porque se instalan en un dispositivo, mientras se tiene acceso a las aplicaciones web a través de un explorador.</span><span class="sxs-lookup"><span data-stu-id="4b77a-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="4b77a-106">El proxy de la aplicación admite aplicaciones de cliente nativo al aceptar tokens emitidos por Azure AD que se envían en encabezados HTTP de autorización estándar.</span><span class="sxs-lookup"><span data-stu-id="4b77a-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relación entre los usuarios finales, Azure Active Directory y las aplicaciones publicadas](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="4b77a-108">Usar hello Azure biblioteca de autenticación de AD, que se encarga de autenticación y admite muchos entornos del cliente, las aplicaciones nativas toopublish.</span><span class="sxs-lookup"><span data-stu-id="4b77a-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="4b77a-109">Proxy de aplicación se adapta a hello [escenario de aplicación nativa tooWeb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="4b77a-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="4b77a-110">Este artículo le guiará a través de hello cuatro pasos toopublish una aplicación nativa con hello biblioteca de autenticación de Azure AD y Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b77a-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="4b77a-111">Paso 1: Publicación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4b77a-111">Step 1: Publish your application</span></span>
<span data-ttu-id="4b77a-112">Publicar la aplicación proxy tal y como lo haría con cualquier otra aplicación y asignar usuarios tooaccess la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b77a-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="4b77a-113">Para más información, consulte [Publicación de aplicaciones mediante el proxy de aplicación de Azure AD](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="4b77a-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="4b77a-114">Paso 2: Configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="4b77a-114">Step 2: Configure your application</span></span>
<span data-ttu-id="4b77a-115">Configure su aplicación nativa de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="4b77a-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="4b77a-116">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b77a-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4b77a-117">Navegue demasiado**Azure Active Directory** > **registros de aplicación**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="4b77a-118">Seleccione **Nuevo registro de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="4b77a-119">Especifique un nombre para la aplicación, seleccione **nativo** como tipo de aplicación Hola y proporcionar Hola URI de redireccionamiento para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b77a-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Creación de un registro de aplicaciones](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="4b77a-121">Seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-121">Select **Create**.</span></span>

<span data-ttu-id="4b77a-122">Para más información sobre cómo crear un registro de aplicación, consulte [Integración de aplicaciones con Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="4b77a-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="4b77a-123">Paso 3: Aplicaciones conceder acceso tooother</span><span class="sxs-lookup"><span data-stu-id="4b77a-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="4b77a-124">Habilitar las aplicaciones de toobe expuesta tooother aplicación nativa de hello en el directorio:</span><span class="sxs-lookup"><span data-stu-id="4b77a-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="4b77a-125">Todavía en **registros de aplicación**, seleccione Hola nueva aplicación nativa que acaba de crear.</span><span class="sxs-lookup"><span data-stu-id="4b77a-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="4b77a-126">Seleccione **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="4b77a-127">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-127">Select **Add**.</span></span>
4. <span data-ttu-id="4b77a-128">Primer paso Hola abierto, **seleccionar una API**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="4b77a-129">Usar Hola búsqueda barra toofind Hola Proxy de aplicación aplicación que se publicó en la primera sección de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b77a-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="4b77a-130">Elija la aplicación y haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-130">Choose that app, then click **Select**.</span></span> 

   ![Busque la aplicación de proxy de hello](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="4b77a-132">Segundo paso Hola abierto, **seleccione permisos**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="4b77a-133">Usar la aplicación de proxy de aplicación nativa acceso tooyour de hello casilla toogrant, a continuación, haga clic en **seleccione**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Conceder acceso tooproxy aplicación](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="4b77a-135">Seleccione **Listo**.</span><span class="sxs-lookup"><span data-stu-id="4b77a-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="4b77a-136">Paso 4: Editar Hola biblioteca de autenticación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b77a-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="4b77a-137">Editar código de aplicación nativa de hello en contexto de autenticación de Hola de Hola biblioteca de autenticación de Active Directory (ADAL) tooinclude Hola siguiente texto:</span><span class="sxs-lookup"><span data-stu-id="4b77a-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="4b77a-138">variables de Hello en el código de ejemplo de Hola deben reemplazarse como sigue:</span><span class="sxs-lookup"><span data-stu-id="4b77a-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="4b77a-139">**Identificador de inquilino** puede encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="4b77a-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="4b77a-140">Navegue demasiado**Azure Active Directory** > **propiedades** y copia Hola Id. de directorio.</span><span class="sxs-lookup"><span data-stu-id="4b77a-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="4b77a-141">**Dirección URL externa** es dirección URL de front-end de Hola que escribió en hello Proxy de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4b77a-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="4b77a-142">toofind este valor, vaya toohello **proxy de aplicación** sección de la aplicación de proxy de hello.</span><span class="sxs-lookup"><span data-stu-id="4b77a-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="4b77a-143">**Identificador de la aplicación** de hello aplicación nativa puede encontrarse en hello **propiedades** página de aplicación nativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b77a-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="4b77a-144">**URI de redireccionamiento de la aplicación nativa de hello** puede encontrarse en hello **URI de redireccionamiento** página de aplicación nativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="4b77a-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="4b77a-145">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="4b77a-145">See also</span></span>

<span data-ttu-id="4b77a-146">Para obtener más información acerca del flujo de la aplicación nativa de hello, consulte [aplicación nativa tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="4b77a-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="4b77a-147">Para obtener las actualizaciones y noticias más recientes de hello, visite hello [blog de Proxy de aplicación](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="4b77a-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
