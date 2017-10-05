---
title: 'Azure Active Directory B2C: Registro de aplicaciones | Microsoft Docs'
description: "Registro de la aplicación con Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: 3d4fe2fa10d848c8b29e4d22d284c0d378f07ae0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="0db57-103">Azure Active Directory B2C: Registro de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0db57-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="0db57-104">Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0db57-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="0db57-105">Cuando haya terminado, la aplicación se habrá registrado para su uso en el inquilino de Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="0db57-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0db57-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0db57-106">Prerequisites</span></span>

<span data-ttu-id="0db57-107">Para crear una aplicación que acepte registros e inicios de sesión de consumidores, primero deberá registrarla en un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="0db57-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="0db57-108">Para obtener su propio inquilino, siga los pasos descritos en [Creación de un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0db57-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="0db57-109">Las aplicaciones creadas en la hoja de Azure AD B2C de Azure Portal se deben administrar desde la misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="0db57-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="0db57-110">Si edita las aplicaciones B2C mediante PowerShell u otro portal, dejan de ser compatibles y no funcionan con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0db57-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="0db57-111">Consulte los detalles en la sección [Aplicaciones con errores](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="0db57-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="0db57-112">Ir a la configuración de B2C</span><span class="sxs-lookup"><span data-stu-id="0db57-112">Navigate to B2C settings</span></span>

<span data-ttu-id="0db57-113">Inicie sesión en [Azure Portal](https://portal.azure.com/) como administrador global del inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="0db57-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="0db57-114">Elija los pasos siguientes en función del tipo de aplicación que vaya a registrar:</span><span class="sxs-lookup"><span data-stu-id="0db57-114">Choose next steps based on the application type you are registering:</span></span>

* [<span data-ttu-id="0db57-115">Registro de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="0db57-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="0db57-116">Registro de una API web</span><span class="sxs-lookup"><span data-stu-id="0db57-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="0db57-117">Registro de una aplicación móvil o nativa</span><span class="sxs-lookup"><span data-stu-id="0db57-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="0db57-118">Registro de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="0db57-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="0db57-119">Si la aplicación web llama a una API web protegida por Azure AD B2C, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="0db57-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="0db57-120">Cree un secreto de aplicación, para lo cual debe ir a la hoja **Claves** y hacer clic en el botón **Generar clave**.</span><span class="sxs-lookup"><span data-stu-id="0db57-120">Create an application secret by going to the **Keys** blade and clicking the **Generate Key** button.</span></span> <span data-ttu-id="0db57-121">Anote el valor de la **Clave de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="0db57-121">Make note of the **App key** value.</span></span> <span data-ttu-id="0db57-122">Use el valor como secreto de aplicación en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0db57-122">You use the value as the application secret in your application's code.</span></span>
   2. <span data-ttu-id="0db57-123">Haga clic en **Acceso de API**, en **Agregar** y seleccione la API web y los ámbitos (permisos).</span><span class="sxs-lookup"><span data-stu-id="0db57-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="0db57-124">Un **secreto de aplicación** es una credencial de seguridad importante y debe protegerse correctamente.</span><span class="sxs-lookup"><span data-stu-id="0db57-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="0db57-125">Saltar a los **pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="0db57-125">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="0db57-126">Registro de una API web</span><span class="sxs-lookup"><span data-stu-id="0db57-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="0db57-127">Haga clic en **Ámbitos publicados** para agregar más ámbitos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0db57-127">Click **Published scopes** to add more scopes as necessary.</span></span> <span data-ttu-id="0db57-128">De forma predeterminada, se definirá el ámbito de "user_impersonation".</span><span class="sxs-lookup"><span data-stu-id="0db57-128">By default, the "user_impersonation" scope is defined.</span></span> <span data-ttu-id="0db57-129">Este ámbito proporciona a otras aplicaciones la capacidad de tener acceso a esta API en nombre del usuario que ha iniciado la sesión.</span><span class="sxs-lookup"><span data-stu-id="0db57-129">The user_impersonation scope gives other applications the ability to access this api on behalf of the signed-in user.</span></span> <span data-ttu-id="0db57-130">Si lo desea, se puede eliminar el ámbito user_impersonation.</span><span class="sxs-lookup"><span data-stu-id="0db57-130">If you wish, the user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="0db57-131">Saltar a los **pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="0db57-131">Jump to **next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="0db57-132">Registro de una aplicación móvil o nativa</span><span class="sxs-lookup"><span data-stu-id="0db57-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="0db57-133">Saltar a los **pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="0db57-133">Jump to **next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="0db57-134">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="0db57-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="0db57-135">Selección de una dirección URL de respuesta de la aplicación web o API</span><span class="sxs-lookup"><span data-stu-id="0db57-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="0db57-136">Actualmente, las aplicaciones registradas en Azure AD B2C están restringidas a un conjunto limitado de valores de direcciones URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="0db57-136">Currently, apps that are registered with Azure AD B2C are restricted to a limited set of reply URL values.</span></span> <span data-ttu-id="0db57-137">La dirección URL de respuesta de aplicaciones y servicios web debe comenzar por el esquema `https`, y todos los valores de dicha dirección deben compartir un único dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="0db57-137">The reply URL for web apps and services must begin with the scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="0db57-138">Por ejemplo, no puede registrar una aplicación web con una de estas direcciones URL de respuesta:</span><span class="sxs-lookup"><span data-stu-id="0db57-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="0db57-139">El sistema de registro compara el nombre DNS completo de la dirección URL de respuesta existente con el nombre DNS de la dirección URL de respuesta que va a agregar.</span><span class="sxs-lookup"><span data-stu-id="0db57-139">The registration system compares the whole DNS name of the existing reply URL to the DNS name of the reply URL that you are adding.</span></span> <span data-ttu-id="0db57-140">La solicitud para agregar el nombre DNS presentará un error si se cumple alguna de las condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="0db57-140">The request to add the DNS name fails if either of the following conditions is true:</span></span>

* <span data-ttu-id="0db57-141">Si el nombre DNS completo de la nueva dirección URL de respuesta no coincide con el nombre DNS de la dirección URL de respuesta existente.</span><span class="sxs-lookup"><span data-stu-id="0db57-141">The whole DNS name of the new reply URL does not match the DNS name of the existing reply URL.</span></span>
* <span data-ttu-id="0db57-142">Si el nombre DNS completo de la nueva dirección URL de respuesta no es un subdominio de la dirección URL de respuesta existente.</span><span class="sxs-lookup"><span data-stu-id="0db57-142">The whole DNS name of the new reply URL is not a subdomain of the existing reply URL.</span></span>

<span data-ttu-id="0db57-143">Por ejemplo, si la aplicación tiene esta dirección URL de respuesta:</span><span class="sxs-lookup"><span data-stu-id="0db57-143">For example, if the app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="0db57-144">Puede agregarla del modo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0db57-144">You can add to it, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="0db57-145">En este caso, el nombre DNS es una coincidencia exacta.</span><span class="sxs-lookup"><span data-stu-id="0db57-145">In this case, the DNS name matches exactly.</span></span> <span data-ttu-id="0db57-146">O bien, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0db57-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="0db57-147">En este caso, hace referencia a un subdominio DNS de login.contoso.com. Si desea que una aplicación tenga login-east.contoso.com y login-west.contoso.com como direcciones URL de respuesta, debe agregar dichas direcciones en este orden:</span><span class="sxs-lookup"><span data-stu-id="0db57-147">In this case, you're referring to a DNS subdomain of login.contoso.com. If you want to have an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="0db57-148">Puede agregar las dos últimas porque son subdominios de la primera URL de respuesta, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0db57-148">You can add the latter two because they are subdomains of the first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="0db57-149">Selección de un identificador URI de redireccionamiento de una aplicación nativa</span><span class="sxs-lookup"><span data-stu-id="0db57-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="0db57-150">Hay dos consideraciones importantes al elegir un URI de redirección para aplicaciones móviles o nativas:</span><span class="sxs-lookup"><span data-stu-id="0db57-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="0db57-151">**Único**: el esquema del identificador URI de redirección debe ser único para todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0db57-151">**Unique**: The scheme of the redirect URI should be unique for every application.</span></span> <span data-ttu-id="0db57-152">En nuestro ejemplo (com.onmicrosoft.contoso.appname://redirect/path), se usa com.onmicrosoft.contoso.appname como esquema.</span><span class="sxs-lookup"><span data-stu-id="0db57-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as the scheme.</span></span> <span data-ttu-id="0db57-153">Se recomienda seguir este patrón.</span><span class="sxs-lookup"><span data-stu-id="0db57-153">We recommend following this pattern.</span></span> <span data-ttu-id="0db57-154">Si dos aplicaciones comparten el mismo esquema, el usuario verá un cuadro de diálogo de "elección de aplicación".</span><span class="sxs-lookup"><span data-stu-id="0db57-154">If two applications share the same scheme, the user sees a "choose app" dialog.</span></span> <span data-ttu-id="0db57-155">Si el usuario realiza una elección incorrecta, no será posible iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="0db57-155">If the user makes an incorrect choice, the login fails.</span></span>
* <span data-ttu-id="0db57-156">**Completo**: el URI de redirección debe tener un esquema y una ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="0db57-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="0db57-157">La ruta de acceso debe contener al menos una barra diagonal después del dominio (por ejemplo, //contoso/ será válido, pero si se escribe //contoso, se producirá un error).</span><span class="sxs-lookup"><span data-stu-id="0db57-157">The path must contain at least one forward slash after the domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="0db57-158">Asegúrese de que no haya ningún carácter especial, como el carácter de subrayado, en el identificador URI de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="0db57-158">Ensure there are no special characters like underscores in the redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="0db57-159">Aplicaciones con errores</span><span class="sxs-lookup"><span data-stu-id="0db57-159">Faulted apps</span></span>

<span data-ttu-id="0db57-160">Las aplicaciones B2C NO se deben editar:</span><span class="sxs-lookup"><span data-stu-id="0db57-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="0db57-161">En otros portales de administración de aplicaciones, como el [Portal de Azure clásico](https://manage.windowsazure.com/) o el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="0db57-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="0db57-162">Con la API Graph o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0db57-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="0db57-163">Si edita la aplicación B2C tal y como se ha descrito anteriormente e intenta editarla de nuevo en la hoja de características de Azure AD B2C en Azure Portal, se convertirá en una aplicación con errores y ya no se podrá usar con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="0db57-163">If you edit the B2C application as described above and try to edit it again in the Azure AD B2C features blade on the Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="0db57-164">Tendrá que eliminar la aplicación y volver a crearla.</span><span class="sxs-lookup"><span data-stu-id="0db57-164">You have to delete the application and create it again.</span></span>

<span data-ttu-id="0db57-165">Para eliminar la aplicación, vaya al [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/) y elimínela desde allí.</span><span class="sxs-lookup"><span data-stu-id="0db57-165">To delete the app, go to the [Application Registration Portal](https://apps.dev.microsoft.com/) and delete the application there.</span></span> <span data-ttu-id="0db57-166">Para que la aplicación esté visible, debe ser el propietario de la misma (y no solo un administrador del inquilino).</span><span class="sxs-lookup"><span data-stu-id="0db57-166">In order for the application to be visible, you need to be the owner of the application (and not just an admin of the tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0db57-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0db57-167">Next steps</span></span>

<span data-ttu-id="0db57-168">Ahora que tiene una aplicación registrada en Azure AD B2C, puede completar uno de [nuestros tutoriales de inicio rápido](active-directory-b2c-overview.md#get-started) para ponerse en marcha rápidamente.</span><span class="sxs-lookup"><span data-stu-id="0db57-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) to get up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0db57-169">Crear una aplicación web de ASP.NET con registro, inicio de sesión y restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="0db57-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)