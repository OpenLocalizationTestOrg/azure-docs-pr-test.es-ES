---
title: 'Azure Active Directory B2C: Registro de aplicaciones | Microsoft Docs'
description: "¿Cómo tooregister la aplicación con Azure Active Directory B2C"
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
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a><span data-ttu-id="dc94d-103">Azure Active Directory B2C: Registro de la aplicación</span><span class="sxs-lookup"><span data-stu-id="dc94d-103">Azure Active Directory B2C: Register your application</span></span>

<span data-ttu-id="dc94d-104">Este inicio rápido le ayuda a registrar una aplicación en un inquilino de Microsoft Azure Active Directory (Azure AD) B2C en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="dc94d-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="dc94d-105">Cuando haya terminado, la aplicación se registra para su uso en el inquilino de hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="dc94d-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc94d-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="dc94d-106">Prerequisites</span></span>

<span data-ttu-id="dc94d-107">toobuild una aplicación que acepta consumidor registrarse e iniciar sesión, necesita primero la aplicación de hello tooregister con un inquilino de Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="dc94d-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="dc94d-108">Obtener su propio inquilino mediante el uso de pasos de hello descritos en [crear un inquilino de Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dc94d-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="dc94d-109">Aplicaciones creadas a partir de la hoja de Azure AD B2C Hola Hola portal de Azure deben administrarse desde Hola misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="dc94d-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="dc94d-110">Si edita las aplicaciones de B2C Hola con PowerShell u otro portal, que se convierten en no compatibles y no funcionan con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="dc94d-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="dc94d-111">Ver detalles de hello [errores en aplicaciones](#faulted-apps) sección.</span><span class="sxs-lookup"><span data-stu-id="dc94d-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="dc94d-112">Desplácese tooB2C configuración</span><span class="sxs-lookup"><span data-stu-id="dc94d-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="dc94d-113">Inicie sesión en toohello [portal de Azure](https://portal.azure.com/) como Hola administrador Global del inquilino de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="dc94d-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

<span data-ttu-id="dc94d-114">Elija los pasos siguientes en función de tipo de aplicación Hola que va a registrar:</span><span class="sxs-lookup"><span data-stu-id="dc94d-114">Choose next steps based on hello application type you are registering:</span></span>

* [<span data-ttu-id="dc94d-115">Registro de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="dc94d-115">Register a web application</span></span>](#register-a-web-app)
* [<span data-ttu-id="dc94d-116">Registro de una API web</span><span class="sxs-lookup"><span data-stu-id="dc94d-116">Register a web API</span></span>](#register-a-web-api)
* [<span data-ttu-id="dc94d-117">Registro de una aplicación móvil o nativa</span><span class="sxs-lookup"><span data-stu-id="dc94d-117">Register a mobile or native application</span></span>](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a><span data-ttu-id="dc94d-118">Registro de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="dc94d-118">Register a web app</span></span>

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

<span data-ttu-id="dc94d-119">Si la aplicación web llama a una API web protegida por Azure AD B2C, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dc94d-119">If your web application calls a web API secured by Azure AD B2C, perform these steps:</span></span>
   1. <span data-ttu-id="dc94d-120">Crear un secreto de aplicación va toohello **claves** hoja y haga clic en hello **generar clave** botón.</span><span class="sxs-lookup"><span data-stu-id="dc94d-120">Create an application secret by going toohello **Keys** blade and clicking hello **Generate Key** button.</span></span> <span data-ttu-id="dc94d-121">Tome nota de hello **clave de aplicación** valor.</span><span class="sxs-lookup"><span data-stu-id="dc94d-121">Make note of hello **App key** value.</span></span> <span data-ttu-id="dc94d-122">Utilice el valor de hello como secreto de aplicación hello en el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="dc94d-122">You use hello value as hello application secret in your application's code.</span></span>
   2. <span data-ttu-id="dc94d-123">Haga clic en **Acceso de API**, en **Agregar** y seleccione la API web y los ámbitos (permisos).</span><span class="sxs-lookup"><span data-stu-id="dc94d-123">Click **API Access**, click **Add**, and select your web API and scopes (permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="dc94d-124">Un **secreto de aplicación** es una credencial de seguridad importante y debe protegerse correctamente.</span><span class="sxs-lookup"><span data-stu-id="dc94d-124">An **Application Secret** is an important security credential, and should be secured appropriately.</span></span>
> 

[<span data-ttu-id="dc94d-125">Saltar demasiado**pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="dc94d-125">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-web-api"></a><span data-ttu-id="dc94d-126">Registro de una API web</span><span class="sxs-lookup"><span data-stu-id="dc94d-126">Register a web API</span></span>

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

<span data-ttu-id="dc94d-127">Haga clic en **publicado ámbitos** tooadd más ámbitos según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="dc94d-127">Click **Published scopes** tooadd more scopes as necessary.</span></span> <span data-ttu-id="dc94d-128">De forma predeterminada, se define el ámbito de "user_impersonation" Hola.</span><span class="sxs-lookup"><span data-stu-id="dc94d-128">By default, hello "user_impersonation" scope is defined.</span></span> <span data-ttu-id="dc94d-129">ámbito user_impersonation de Hello ofrece otras tooaccess de capacidad de las aplicaciones Hola esta api en nombre de usuario que inició sesión Hola.</span><span class="sxs-lookup"><span data-stu-id="dc94d-129">hello user_impersonation scope gives other applications hello ability tooaccess this api on behalf of hello signed-in user.</span></span> <span data-ttu-id="dc94d-130">Si lo desea, se puede quitar el ámbito de hello user_impersonation.</span><span class="sxs-lookup"><span data-stu-id="dc94d-130">If you wish, hello user_impersonation scope can be removed.</span></span>

[<span data-ttu-id="dc94d-131">Saltar demasiado**pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="dc94d-131">Jump too**next steps**</span></span>](#next-steps)

## <a name="register-a-mobile-or-native-app"></a><span data-ttu-id="dc94d-132">Registro de una aplicación móvil o nativa</span><span class="sxs-lookup"><span data-stu-id="dc94d-132">Register a mobile or native app</span></span>

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[<span data-ttu-id="dc94d-133">Saltar demasiado**pasos siguientes**</span><span class="sxs-lookup"><span data-stu-id="dc94d-133">Jump too**next steps**</span></span>](#next-steps)

## <a name="limitations"></a><span data-ttu-id="dc94d-134">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="dc94d-134">Limitations</span></span>

### <a name="choosing-a-web-app-or-api-reply-url"></a><span data-ttu-id="dc94d-135">Selección de una dirección URL de respuesta de la aplicación web o API</span><span class="sxs-lookup"><span data-stu-id="dc94d-135">Choosing a web app or api reply URL</span></span>

<span data-ttu-id="dc94d-136">Actualmente, las aplicaciones que se registran con Azure AD B2C son conjunto restringido tooa limitado de valores de dirección URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="dc94d-136">Currently, apps that are registered with Azure AD B2C are restricted tooa limited set of reply URL values.</span></span> <span data-ttu-id="dc94d-137">Hola respuesta dirección URL para aplicaciones web y servicios debe comenzar con el esquema de hello `https`, y responden a todos los valores de dirección URL deben compartir un único dominio DNS.</span><span class="sxs-lookup"><span data-stu-id="dc94d-137">hello reply URL for web apps and services must begin with hello scheme `https`, and all reply URL values must share a single DNS domain.</span></span> <span data-ttu-id="dc94d-138">Por ejemplo, no puede registrar una aplicación web con una de estas direcciones URL de respuesta:</span><span class="sxs-lookup"><span data-stu-id="dc94d-138">For example, you cannot register a web app that has one of these reply URLs:</span></span>

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="dc94d-139">sistema de registro de Hello compara Hola de nombre DNS completo de hello existente respuesta URL toohello nombre DNS de la dirección URL de respuesta de Hola que va a agregar.</span><span class="sxs-lookup"><span data-stu-id="dc94d-139">hello registration system compares hello whole DNS name of hello existing reply URL toohello DNS name of hello reply URL that you are adding.</span></span> <span data-ttu-id="dc94d-140">tooadd Hola nombre DNS de Hello solicitud produce un error si se cumple alguna de hello condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="dc94d-140">hello request tooadd hello DNS name fails if either of hello following conditions is true:</span></span>

* <span data-ttu-id="dc94d-141">nombre DNS completo de Hola Hola nueva URL de respuesta no coincide con el nombre DNS de Hola Hola existente URL de respuesta.</span><span class="sxs-lookup"><span data-stu-id="dc94d-141">hello whole DNS name of hello new reply URL does not match hello DNS name of hello existing reply URL.</span></span>
* <span data-ttu-id="dc94d-142">nombre DNS completo de Hola Hola nueva URL de respuesta no es un subdominio de hello URL de respuesta existente.</span><span class="sxs-lookup"><span data-stu-id="dc94d-142">hello whole DNS name of hello new reply URL is not a subdomain of hello existing reply URL.</span></span>

<span data-ttu-id="dc94d-143">Por ejemplo, si hello aplicación tiene esta dirección URL de respuesta:</span><span class="sxs-lookup"><span data-stu-id="dc94d-143">For example, if hello app has this reply URL:</span></span>

`https://login.contoso.com`

<span data-ttu-id="dc94d-144">Puede agregar tooit, similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc94d-144">You can add tooit, like this:</span></span>

`https://login.contoso.com/new`

<span data-ttu-id="dc94d-145">En este caso, el nombre DNS de hello coincide exactamente.</span><span class="sxs-lookup"><span data-stu-id="dc94d-145">In this case, hello DNS name matches exactly.</span></span> <span data-ttu-id="dc94d-146">O bien, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="dc94d-146">Or, you can do this:</span></span>

`https://new.login.contoso.com`

<span data-ttu-id="dc94d-147">En este caso, está haciendo referencia subdominio DNS de tooa de login.contoso.com. Si desea toohave una aplicación con inicio de sesión east.contoso.com y west.contoso.com-inicio de sesión como responder a las direcciones URL, debe agregar estas direcciones URL de respuesta en este orden:</span><span class="sxs-lookup"><span data-stu-id="dc94d-147">In this case, you're referring tooa DNS subdomain of login.contoso.com. If you want toohave an app that has login-east.contoso.com and login-west.contoso.com as reply URLs, you must add those reply URLs in this order:</span></span>

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

<span data-ttu-id="dc94d-148">Puede agregar Hola dos últimos porque son subdominios Hola primera URL de respuesta, contoso.com.</span><span class="sxs-lookup"><span data-stu-id="dc94d-148">You can add hello latter two because they are subdomains of hello first reply URL, contoso.com.</span></span>

### <a name="choosing-a-native-app-redirect-uri"></a><span data-ttu-id="dc94d-149">Selección de un identificador URI de redireccionamiento de una aplicación nativa</span><span class="sxs-lookup"><span data-stu-id="dc94d-149">Choosing a native app redirect URI</span></span>

<span data-ttu-id="dc94d-150">Hay dos consideraciones importantes al elegir un URI de redirección para aplicaciones móviles o nativas:</span><span class="sxs-lookup"><span data-stu-id="dc94d-150">There are two important considerations when choosing a redirect URI for mobile/native applications:</span></span>

* <span data-ttu-id="dc94d-151">**Único**: esquema de Hola de URI de redireccionamiento de hello debe ser único para todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dc94d-151">**Unique**: hello scheme of hello redirect URI should be unique for every application.</span></span> <span data-ttu-id="dc94d-152">En nuestro ejemplo (com.onmicrosoft.contoso.appname://redirect/path), se utiliza com.onmicrosoft.contoso.appname como esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc94d-152">In our example (com.onmicrosoft.contoso.appname://redirect/path), we use com.onmicrosoft.contoso.appname as hello scheme.</span></span> <span data-ttu-id="dc94d-153">Se recomienda seguir este patrón.</span><span class="sxs-lookup"><span data-stu-id="dc94d-153">We recommend following this pattern.</span></span> <span data-ttu-id="dc94d-154">Si dos aplicaciones comparten Hola mismo esquema, hello usuario ve un cuadro de diálogo "elegir la aplicación".</span><span class="sxs-lookup"><span data-stu-id="dc94d-154">If two applications share hello same scheme, hello user sees a "choose app" dialog.</span></span> <span data-ttu-id="dc94d-155">Si el usuario de hello realiza una opción incorrecta, se produce un error de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="dc94d-155">If hello user makes an incorrect choice, hello login fails.</span></span>
* <span data-ttu-id="dc94d-156">**Completo**: el URI de redirección debe tener un esquema y una ruta de acceso.</span><span class="sxs-lookup"><span data-stu-id="dc94d-156">**Complete**: Redirect URI must have a scheme and a path.</span></span> <span data-ttu-id="dc94d-157">ruta de acceso de Hello debe contener al menos una barra diagonal después de dominio de hello (por ejemplo, //contoso/ funciona y se produce un error de //contoso).</span><span class="sxs-lookup"><span data-stu-id="dc94d-157">hello path must contain at least one forward slash after hello domain (for example, //contoso/ works and //contoso fails).</span></span>

<span data-ttu-id="dc94d-158">Asegúrese de que no hay ningún carácter especial como carácter de subrayado en hello uri de redireccionamiento.</span><span class="sxs-lookup"><span data-stu-id="dc94d-158">Ensure there are no special characters like underscores in hello redirect uri.</span></span>

### <a name="faulted-apps"></a><span data-ttu-id="dc94d-159">Aplicaciones con errores</span><span class="sxs-lookup"><span data-stu-id="dc94d-159">Faulted apps</span></span>

<span data-ttu-id="dc94d-160">Las aplicaciones B2C NO se deben editar:</span><span class="sxs-lookup"><span data-stu-id="dc94d-160">B2C applications should NOT be edited:</span></span>

* <span data-ttu-id="dc94d-161">En otros portales de administración de aplicaciones, como el [Portal de Azure clásico](https://manage.windowsazure.com/) o el [Portal de registro de aplicaciones](https://apps.dev.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="dc94d-161">On other application management portals such as the [Azure classic portal](https://manage.windowsazure.com/) & the [Application Registration Portal](https://apps.dev.microsoft.com/).</span></span>
* <span data-ttu-id="dc94d-162">Con la API Graph o PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc94d-162">Using Graph API or PowerShell</span></span>

<span data-ttu-id="dc94d-163">Si edita la aplicación hello B2C tal y como se ha descrito anteriormente e intente tooedit nuevo en la hoja de características de Azure AD B2C hello en Hola portal de Azure, se convierte en una aplicación con errores y la aplicación ya no es utilizable con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="dc94d-163">If you edit hello B2C application as described above and try tooedit it again in hello Azure AD B2C features blade on hello Azure portal, it becomes a faulted app, and your application is no longer usable with Azure AD B2C.</span></span> <span data-ttu-id="dc94d-164">Tiene toodelete Hola aplicación y vuelva a crearlo.</span><span class="sxs-lookup"><span data-stu-id="dc94d-164">You have toodelete hello application and create it again.</span></span>

<span data-ttu-id="dc94d-165">aplicación de hello toodelete, vaya toohello [Portal de registro de aplicación](https://apps.dev.microsoft.com/) y eliminar la aplicación hello no existe.</span><span class="sxs-lookup"><span data-stu-id="dc94d-165">toodelete hello app, go toohello [Application Registration Portal](https://apps.dev.microsoft.com/) and delete hello application there.</span></span> <span data-ttu-id="dc94d-166">En orden para hello aplicación toobe visible, necesitará propietario de hello toobe de aplicación hello (y no solo un administrador de inquilinos de hello).</span><span class="sxs-lookup"><span data-stu-id="dc94d-166">In order for hello application toobe visible, you need toobe hello owner of hello application (and not just an admin of hello tenant).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc94d-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dc94d-167">Next steps</span></span>

<span data-ttu-id="dc94d-168">Ahora que tiene una aplicación registrada con Azure AD B2C, puede realizar uno de [nuestros tutoriales de inicio rápido](active-directory-b2c-overview.md#get-started) tooget activos y en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="dc94d-168">Now that you have an application registered with Azure AD B2C, you can complete one of [our quick-start tutorials](active-directory-b2c-overview.md#get-started) tooget up and running.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dc94d-169">Crear una aplicación web de ASP.NET con registro, inicio de sesión y restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="dc94d-169">Create an ASP.NET web app with sign-up, sign-in, and password reset</span></span>](active-directory-b2c-devquickstarts-web-dotnet-susi.md)