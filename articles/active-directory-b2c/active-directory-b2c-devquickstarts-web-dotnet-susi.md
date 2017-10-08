---
title: aaaAzure B2C de Active Directory | Documentos de Microsoft
description: "Cómo generar perfiles toobuild una aplicación web que tiene sesión-up/inicio de sesión de, editar y restableció la contraseña mediante Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: barbaraselden
ms.assetid: 30261336-d7a5-4a6d-8c1a-7943ad76ed25
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/17/2017
ms.author: parakhj
ms.openlocfilehash: 187f99a8dd50d212de4f0517f552cdbbe5a8edf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="6afeb-103">Creación de una aplicación web de ASP.NET con procesos de registro e inicio de sesión, edición de perfil y restablecimiento de contraseña de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6afeb-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="6afeb-104">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="6afeb-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6afeb-105">Agregar la aplicación web de Azure AD B2C identidad características tooyour</span><span class="sxs-lookup"><span data-stu-id="6afeb-105">Add Azure AD B2C identity features tooyour web app</span></span>
> * <span data-ttu-id="6afeb-106">Registrar la aplicación web en el directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6afeb-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="6afeb-107">Crear una directiva de registro e inicio de sesión de usuario, edición de perfil y restablecimiento de contraseña para la aplicación web</span><span class="sxs-lookup"><span data-stu-id="6afeb-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6afeb-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6afeb-108">Prerequisites</span></span>

- <span data-ttu-id="6afeb-109">Debe conectarse la tooan B2C inquilino cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="6afeb-109">You must connect your B2C Tenant tooan Azure account.</span></span> <span data-ttu-id="6afeb-110">Puede crear una cuenta de Azure gratuita [aquí](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="6afeb-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="6afeb-111">Necesita [Microsoft Visual Studio](https://www.visualstudio.com/) o un programa tooview y modificar el código de ejemplo de Hola similar.</span><span class="sxs-lookup"><span data-stu-id="6afeb-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program tooview and modify hello sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="6afeb-112">Creación de un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="6afeb-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="6afeb-113">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="6afeb-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="6afeb-114">Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="6afeb-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="6afeb-115">Si aún no tiene uno, cree un directorio B2C antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="6afeb-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="6afeb-116">Necesita tooconnect Hola B2C inquilino tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="6afeb-116">You need tooconnect hello B2C Tenant tooyour Azure subscription.</span></span> <span data-ttu-id="6afeb-117">Después de seleccionar **crear**, seleccione hello **toomy vínculo un B2C existente de AD de Azure inquilino suscripción de Azure** opción y, a continuación, en hello **inquilino de Azure AD B2C** de lista desplegable, seleccione inquilino de Hello desea tooassociate.</span><span class="sxs-lookup"><span data-stu-id="6afeb-117">After selecting **Create**, select hello **Link an existing Azure AD B2C Tenant toomy Azure subscription** option, and then in hello **Azure AD B2C Tenant** drop down, select hello tenant you want tooassociate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="6afeb-118">Creación y registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="6afeb-118">Create and register an application</span></span>

<span data-ttu-id="6afeb-119">A continuación, es necesario toocreate y registrar la aplicación hello en el directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="6afeb-119">Next, you need toocreate and register hello app in your B2C directory.</span></span> <span data-ttu-id="6afeb-120">Esto proporciona información que Azure AD B2C necesita toosecurely comunicarse con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-120">This provides information that Azure AD B2C needs toosecurely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="6afeb-121">Cuando haya terminado, tendrá una API y una aplicación nativa en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="6afeb-122">Creación de directivas en el inquilino B2C</span><span class="sxs-lookup"><span data-stu-id="6afeb-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="6afeb-123">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6afeb-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6afeb-124">Este ejemplo de código contiene tres experiencias de identidad: **registro e inicio de sesión**, **edición de perfil** y **restablecimiento de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="6afeb-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="6afeb-125">Deberá toocreate una directiva de cada tipo, tal y como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6afeb-125">You need toocreate one policy of each type, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6afeb-126">Para cada directiva, ser seguro de atributo de nombre de visualización de tooselect Hola o notificación y toocopy hacia abajo el nombre de saludo de la directiva para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="6afeb-126">For each policy, be sure tooselect hello Display name attribute or claim, and toocopy down hello name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="6afeb-127">Incorporación de sus proveedores de identidades</span><span class="sxs-lookup"><span data-stu-id="6afeb-127">Add your identity providers</span></span>

<span data-ttu-id="6afeb-128">En la configuración, seleccione **Proveedores de identidades** y elija Registro de nombre de usuario o Registro por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6afeb-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="6afeb-129">Creación de una directiva de registro o de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="6afeb-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="6afeb-130">Creación de una directiva de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="6afeb-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="6afeb-131">Crear una directiva de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="6afeb-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="6afeb-132">Después de crear las directivas, está listo toobuild la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-132">After you create your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="6afeb-133">Descargar código de muestra de Hola</span><span class="sxs-lookup"><span data-stu-id="6afeb-133">Download hello sample code</span></span>

<span data-ttu-id="6afeb-134">código de Hello para este tutorial se mantiene en [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="6afeb-134">hello code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="6afeb-135">Puede clonar el ejemplo hello ejecutando:</span><span class="sxs-lookup"><span data-stu-id="6afeb-135">You can clone hello sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="6afeb-136">Después de descargar el código de ejemplo de Hola, inició tooget de archivo .sln de hello abrir Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6afeb-136">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="6afeb-137">archivo de solución de Hello contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="6afeb-137">hello solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="6afeb-138">`TaskWebApp`es Hola aplicación web MVC que Hola usuario interactúa con.</span><span class="sxs-lookup"><span data-stu-id="6afeb-138">`TaskWebApp` is hello MVC web application that hello user interacts with.</span></span> <span data-ttu-id="6afeb-139">`TaskService`es la API de web back-end de la aplicación hello que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="6afeb-139">`TaskService` is hello app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="6afeb-140">Este artículo describe solo hello `TaskWebApp` aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-140">This article will only discuss hello `TaskWebApp` application.</span></span> <span data-ttu-id="6afeb-141">toolearn cómo toobuild `TaskService` con Azure AD B2C, consulte [nuestro tutorial de api web de .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="6afeb-141">toolearn how toobuild `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-toouse-your-tenant-and-policies"></a><span data-ttu-id="6afeb-142">Actualizar código toouse las directivas y su inquilino</span><span class="sxs-lookup"><span data-stu-id="6afeb-142">Update code toouse your tenant and policies</span></span>

<span data-ttu-id="6afeb-143">Nuestro ejemplo es toouse configurado Hola directivas e ID de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="6afeb-143">Our sample is configured toouse hello policies and client ID of our demo tenant.</span></span> <span data-ttu-id="6afeb-144">tooconnect se tooyour propio inquilino, necesita tooopen `web.config` en hello `TaskWebApp` de proyectos y Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="6afeb-144">tooconnect it tooyour own tenant, you need tooopen `web.config` in hello `TaskWebApp` project and replace hello following values:</span></span>

* <span data-ttu-id="6afeb-145">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="6afeb-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="6afeb-146">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="6afeb-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="6afeb-147">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="6afeb-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="6afeb-148">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="6afeb-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="6afeb-149">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="6afeb-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="6afeb-150">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="6afeb-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-hello-app"></a><span data-ttu-id="6afeb-151">Inicie la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="6afeb-151">Launch hello app</span></span>
<span data-ttu-id="6afeb-152">Desde dentro de Visual Studio, iniciar aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6afeb-152">From within Visual Studio, launch hello app.</span></span> <span data-ttu-id="6afeb-153">Navegar por pestaña de la lista de tareas pendientes de toohello y Hola tenga en cuenta que es la dirección URl: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*& client_id = *YourclientID*...</span><span class="sxs-lookup"><span data-stu-id="6afeb-153">Navigate toohello To-Do List tab, and note hello URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="6afeb-154">Registrarse para la aplicación hello utilizando su nombre de usuario o la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="6afeb-154">Sign up for hello app by using your email address or user name.</span></span> <span data-ttu-id="6afeb-155">Cerrar sesión, a continuación, inicie sesión de nuevo y editar el perfil de Hola o restablecer la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-155">Sign out, then sign in again and edit hello profile or reset hello password.</span></span> <span data-ttu-id="6afeb-156">Cierre la sesión y iníciela con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="6afeb-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="6afeb-157">Agregar IDP sociales</span><span class="sxs-lookup"><span data-stu-id="6afeb-157">Add social IDPs</span></span>

<span data-ttu-id="6afeb-158">Actualmente, la aplicación hello admite solo los usuarios registrarse e iniciar sesión mediante el uso de **cuentas locales**; cuentas almacenadas en el directorio B2C que usan un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="6afeb-158">Currently, hello app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="6afeb-159">Con Azure AD B2C, puede agregar compatibilidad con otros **proveedores de identidades** (IDP) sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="6afeb-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="6afeb-160">tooadd sociales IDPs tooyour aplicación, para comenzar, siga Hola detallada instrucciones que aparecen en estos artículos.</span><span class="sxs-lookup"><span data-stu-id="6afeb-160">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="6afeb-161">Para cada IDP desea toosupport, necesita tooregister una aplicación en ese sistema y obtener un identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="6afeb-161">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="6afeb-162">Configurar Facebook como una IDP</span><span class="sxs-lookup"><span data-stu-id="6afeb-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="6afeb-163">Configurar Google como una IDP</span><span class="sxs-lookup"><span data-stu-id="6afeb-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="6afeb-164">Configurar Amazon como una IDP</span><span class="sxs-lookup"><span data-stu-id="6afeb-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="6afeb-165">Configurar LinkedIn como una IDP</span><span class="sxs-lookup"><span data-stu-id="6afeb-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="6afeb-166">Después de agregar tooyour de proveedores de identidad de hello directory B2C, edición de los tres directivas tooinclude Hola IDPs nueva, como se describe en hello [artículo de referencia de directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6afeb-166">After you add hello identity providers tooyour B2C directory, edit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="6afeb-167">Después de guardar las directivas, vuelva a ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6afeb-167">After you save your policies, run hello app again.</span></span>  <span data-ttu-id="6afeb-168">Debería ver Hola que IDPS nueva se agregan como opciones de inicio de sesión y suscripción en cada una de sus experiencias de identidad.</span><span class="sxs-lookup"><span data-stu-id="6afeb-168">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="6afeb-169">Puede experimentar con las directivas y observar el efecto de hello en la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6afeb-169">You can experiment with your policies and observe hello effect on your sample app.</span></span> <span data-ttu-id="6afeb-170">Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro.</span><span class="sxs-lookup"><span data-stu-id="6afeb-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="6afeb-171">Experimente para ver cómo se combinan las directivas, las solicitudes de autenticación y OWIN.</span><span class="sxs-lookup"><span data-stu-id="6afeb-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="6afeb-172">Tutorial de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="6afeb-172">Sample code walkthrough</span></span>
<span data-ttu-id="6afeb-173">Hola las secciones siguientes muestra cómo se configura el código de aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-173">hello following sections show you how hello sample application code is configured.</span></span> <span data-ttu-id="6afeb-174">Puede usar dicho tutorial como guía en su futuro desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6afeb-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="6afeb-175">Incorporación de compatibilidad con la autenticación</span><span class="sxs-lookup"><span data-stu-id="6afeb-175">Add authentication support</span></span>

<span data-ttu-id="6afeb-176">Ahora puede configurar su toouse aplicación Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6afeb-176">You can now configure your app toouse Azure AD B2C.</span></span> <span data-ttu-id="6afeb-177">La aplicación se comunica con Azure AD B2C mediante el envío de solicitudes de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="6afeb-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="6afeb-178">las solicitudes de Hello dictan la experiencia del usuario Hola tooexecute desea que la aplicación especificando la directiva Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-178">hello requests dictate hello user experience your app wants tooexecute by specifying hello policy.</span></span> <span data-ttu-id="6afeb-179">Puede usar toosend de biblioteca de Microsoft OWIN estas solicitudes, ejecutar las directivas, administrar sesiones de usuario y mucho más.</span><span class="sxs-lookup"><span data-stu-id="6afeb-179">You can use Microsoft's OWIN library toosend these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="6afeb-180">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="6afeb-180">Install OWIN</span></span>

<span data-ttu-id="6afeb-181">toobegin, Agregar proyecto toohello de paquetes de NuGet de middleware de hello OWIN mediante Hola consola de administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6afeb-181">toobegin, add hello OWIN middleware NuGet packages toohello project by using hello Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="6afeb-182">Agregar una clase de inicio de OWIN</span><span class="sxs-lookup"><span data-stu-id="6afeb-182">Add an OWIN startup class</span></span>

<span data-ttu-id="6afeb-183">Agrega una clase de inicio OWIN toohello API denominado `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="6afeb-183">Add an OWIN startup class toohello API called `Startup.cs`.</span></span>  <span data-ttu-id="6afeb-184">Haga doble clic en el proyecto de hello, seleccione **agregar** y **nuevo elemento**y, a continuación, busque OWIN.</span><span class="sxs-lookup"><span data-stu-id="6afeb-184">Right-click on hello project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="6afeb-185">middleware de OWIN Hola invocará hello `Configuration(…)` método cuando se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-185">hello OWIN middleware will invoke hello `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="6afeb-186">En nuestro ejemplo, hemos cambiado declaración de clase de hello demasiado`public partial class Startup` e implementado Hola otra parte de la clase hello en `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="6afeb-186">In our sample, we changed hello class declaration too`public partial class Startup` and implemented hello other part of hello class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="6afeb-187">Hola interior `Configuration` método, agregamos una llamada demasiado`ConfigureAuth`, que se define en `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="6afeb-187">Inside hello `Configuration` method, we added a call too`ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="6afeb-188">Después de las modificaciones de hello, `Startup.cs` Hola siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="6afeb-188">After hello modifications, `Startup.cs` looks like hello following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // hello OWIN middleware will invoke this method when hello app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of hello class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-hello-authentication-middleware"></a><span data-ttu-id="6afeb-189">Configurar el middleware de autenticación Hola</span><span class="sxs-lookup"><span data-stu-id="6afeb-189">Configure hello authentication middleware</span></span>

<span data-ttu-id="6afeb-190">Archivo abierto hello `App_Start\Startup.Auth.cs` e implementar hello `ConfigureAuth(...)` método.</span><span class="sxs-lookup"><span data-stu-id="6afeb-190">Open hello file `App_Start\Startup.Auth.cs` and implement hello `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="6afeb-191">Hola parámetros que se proporciona en `OpenIdConnectAuthenticationOptions` actuar como coordenadas para su toocommunicate de aplicación con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6afeb-191">hello parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="6afeb-192">Si no especifica ciertos parámetros, usará el valor de predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-192">If you do not specify certain parameters, it will use hello default value.</span></span> <span data-ttu-id="6afeb-193">Por ejemplo, no especificamos hello `ResponseType` en el ejemplo de Hola, Hola por lo que el valor predeterminado `code id_token` se utilizarán en cada tooAzure de solicitud saliente AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6afeb-193">For example, we do not specify hello `ResponseType` in hello sample, so hello default value `code id_token` will be used in each outgoing request tooAzure AD B2C.</span></span>

<span data-ttu-id="6afeb-194">También deberá tooset la autenticación de la cookie.</span><span class="sxs-lookup"><span data-stu-id="6afeb-194">You also need tooset up cookie authentication.</span></span> <span data-ttu-id="6afeb-195">Hola OpenID Connect middleware que usa las sesiones de usuario del toomaintain de cookies, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="6afeb-195">hello OpenID Connect middleware uses cookies toomaintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure hello OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate hello metadata address using hello tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify hello callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify hello claims toovalidate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify hello scope by appending all of hello scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement hello "Notification" methods...
}
```

<span data-ttu-id="6afeb-196">En `OpenIdConnectAuthenticationOptions` los casos anteriores, definimos un conjunto de funciones de devolución de llamada para notificaciones específicas que son recibidas por el middleware de OpenID Connect Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by hello OpenID Connect middleware.</span></span> <span data-ttu-id="6afeb-197">Estos comportamientos se definen mediante un `OpenIdConnectAuthenticationNotifications` objeto y almacenan en hello `Notifications` variable.</span><span class="sxs-lookup"><span data-stu-id="6afeb-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into hello `Notifications` variable.</span></span> <span data-ttu-id="6afeb-198">En nuestro ejemplo, se definen tres devoluciones de llamada diferentes según el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-198">In our sample, we define three different callbacks depending on hello event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="6afeb-199">Uso de distintas directivas</span><span class="sxs-lookup"><span data-stu-id="6afeb-199">Using different policies</span></span>

<span data-ttu-id="6afeb-200">Hola `RedirectToIdentityProvider` notificación se desencadena cuando se realiza una solicitud tooAzure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="6afeb-200">hello `RedirectToIdentityProvider` notification is triggered whenever a request is made tooAzure AD B2C.</span></span> <span data-ttu-id="6afeb-201">En función de devolución de llamada de hello `OnRedirectToIdentityProvider`, comprobamos Hola llamada de salida si lo deseamos toouse una directiva diferente.</span><span class="sxs-lookup"><span data-stu-id="6afeb-201">In hello callback function `OnRedirectToIdentityProvider`, we check in hello outgoing call if we want toouse a different policy.</span></span> <span data-ttu-id="6afeb-202">En orden toodo restablecer o editar un perfil de una contraseña, necesita directiva correspondiente de hello toouse como directiva en lugar de directiva de "Inicio de sesión o inicio de sesión" predeterminada Hola de restablecimiento de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-202">In order toodo a password reset or edit a profile, you need toouse hello corresponding policy such as hello password reset policy instead of hello default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="6afeb-203">En nuestro ejemplo, cuando un usuario desea tooreset contraseña de Hola o editar el perfil de hello, agregamos directiva Hola se prefiere toouse en contexto OWIN de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-203">In our sample, when a user wants tooreset hello password or edit hello profile, we add hello policy we prefer toouse into hello OWIN context.</span></span> <span data-ttu-id="6afeb-204">Esto puede realizarse mediante acciones Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6afeb-204">That can be done by doing hello following:</span></span>

```CSharp
    // Let hello middleware know you are trying toouse hello edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="6afeb-205">Se puede implementar la función de devolución de llamada de hello `OnRedirectToIdentityProvider` haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="6afeb-205">And you can implement hello callback function `OnRedirectToIdentityProvider` by doing hello following:</span></span>

```CSharp
/*
*  On each call tooAzure AD B2C, check if a policy (e.g. hello profile edit or password reset policy) has been specified in hello OWIN context.
*  If so, use that policy when making hello call. Also, don't request a code (since it won't be needed).
*/
private Task OnRedirectToIdentityProvider(RedirectToIdentityProviderNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    var policy = notification.OwinContext.Get<string>("Policy");

    if (!string.IsNullOrEmpty(policy) && !policy.Equals(DefaultPolicy))
    {
        notification.ProtocolMessage.Scope = OpenIdConnectScopes.OpenId;
        notification.ProtocolMessage.ResponseType = OpenIdConnectResponseTypes.IdToken;
        notification.ProtocolMessage.IssuerAddress = notification.ProtocolMessage.IssuerAddress.Replace(DefaultPolicy, policy);
    }

    return Task.FromResult(0);
}
```

### <a name="handling-authorization-codes"></a><span data-ttu-id="6afeb-206">Control de códigos de autorización</span><span class="sxs-lookup"><span data-stu-id="6afeb-206">Handling authorization codes</span></span>

<span data-ttu-id="6afeb-207">Hola `AuthorizationCodeReceived` notificación se desencadena cuando se recibe un código de autorización.</span><span class="sxs-lookup"><span data-stu-id="6afeb-207">hello `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="6afeb-208">middleware de OpenID Connect de Hello no admite códigos de intercambio para los tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="6afeb-208">hello OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="6afeb-209">Puede intercambiar manualmente código de hello para el token de hello en una función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="6afeb-209">You can manually exchange hello code for hello token in a callback function.</span></span> <span data-ttu-id="6afeb-210">Para obtener más información, vea hello [documentación](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica cómo.</span><span class="sxs-lookup"><span data-stu-id="6afeb-210">For more information, please look at hello [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="6afeb-211">Control de errores</span><span class="sxs-lookup"><span data-stu-id="6afeb-211">Handling errors</span></span>

<span data-ttu-id="6afeb-212">Hola `AuthenticationFailed` notificación se desencadena cuando se produce un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-212">hello `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="6afeb-213">En su método de devolución de llamada, puede controlar los errores de hello como desee.</span><span class="sxs-lookup"><span data-stu-id="6afeb-213">In its callback method, you can handle hello errors as you wish.</span></span> <span data-ttu-id="6afeb-214">Sin embargo, debe agregar una comprobación para el código de error de hello `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="6afeb-214">You should however add a check for hello error code `AADB2C90118`.</span></span> <span data-ttu-id="6afeb-215">Durante la ejecución de Hola de directiva "Inicio de sesión o inicio de sesión" Hola, usuario de hello tiene Hola oportunidad tooselect una **¿olvidó su contraseña?** vínculo.</span><span class="sxs-lookup"><span data-stu-id="6afeb-215">During hello execution of hello "Sign-up or Sign-in" policy, hello user has hello opportunity tooselect a **Forgot your password?** link.</span></span> <span data-ttu-id="6afeb-216">En este caso, Azure AD B2C envía la aplicación ese código de error que indica que la aplicación realice una solicitud mediante la directiva de restablecimiento de contraseña de hello en su lugar.</span><span class="sxs-lookup"><span data-stu-id="6afeb-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using hello password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by hello authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle hello error code that Azure AD B2C throws when trying tooreset a password from hello login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If hello user clicked hello reset password link, redirect toohello reset password route
        notification.Response.Redirect("/Account/ResetPassword");
    }
    else if (notification.Exception.Message == "access_denied")
    {
        notification.Response.Redirect("/");
    }
    else
    {
        notification.Response.Redirect("/Home/Error?message=" + notification.Exception.Message);
    }

    return Task.FromResult(0);
}
```

### <a name="send-authentication-requests-tooazure-ad"></a><span data-ttu-id="6afeb-217">Enviar solicitudes de autenticación tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="6afeb-217">Send authentication requests tooAzure AD</span></span>

<span data-ttu-id="6afeb-218">La aplicación ya está configurada correctamente toocommunicate con Azure AD B2C con el protocolo de autenticación de OpenID Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-218">Your app is now properly configured toocommunicate with Azure AD B2C by using hello OpenID Connect authentication protocol.</span></span> <span data-ttu-id="6afeb-219">OWIN administra los detalles de Hola de transmitir mensajes de autenticación, validar los tokens de Azure AD B2C y mantener la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="6afeb-219">OWIN manages hello details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="6afeb-220">Lo único que queda es tooinitiate flujo de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="6afeb-220">All that remains is tooinitiate each user's flow.</span></span>

<span data-ttu-id="6afeb-221">Cuando un usuario selecciona **arriba/inicio de sesión del inicio de sesión**, **Editar perfil**, o **de restablecimiento de contraseña** en la aplicación web de hello, se invoca la acción de hello asociado en `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="6afeb-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in hello web app, hello associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign up or sign in
*/
public void SignUpSignIn()
{
    // Use hello default policy tooprocess hello sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting tooedit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let hello middleware know you are trying toouse hello edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set hello page tooredirect tooafter editing hello profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting tooreset a password
*/
public void ResetPassword()
{
    // Let hello middleware know you are trying toouse hello reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set hello page tooredirect tooafter changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="6afeb-222">También puede usar OWIN toosign usuario Hola desde la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6afeb-222">You can also use OWIN toosign out hello user from hello app.</span></span> <span data-ttu-id="6afeb-223">En `Controllers\AccountController.cs`, tenemos:</span><span class="sxs-lookup"><span data-stu-id="6afeb-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting toosign out
*/
public void SignOut()
{
    // toosign out hello user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="6afeb-224">En suma tooexplicitly invocar una directiva, puede usar un `[Authorize]` etiqueta en los controladores que se ejecuta una directiva si el usuario de hello no ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="6afeb-224">In addition tooexplicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if hello user is not signed in.</span></span> <span data-ttu-id="6afeb-225">Abra `Controllers\HomeController.cs` y agregue hello `[Authorize]` controlador de notificaciones de etiqueta toohello.</span><span class="sxs-lookup"><span data-stu-id="6afeb-225">Open `Controllers\HomeController.cs` and add hello `[Authorize]` tag toohello claims controller.</span></span>  <span data-ttu-id="6afeb-226">OWIN selecciona Hola última directiva que se configuró cuando hello `[Authorize]` se alcanza la etiqueta.</span><span class="sxs-lookup"><span data-stu-id="6afeb-226">OWIN selects hello last policy configured when hello `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use hello Authorize decorator tooexecute a certain policy if hello user is not already signed into hello app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="6afeb-227">Mostrar información de usuario</span><span class="sxs-lookup"><span data-stu-id="6afeb-227">Display user information</span></span>

<span data-ttu-id="6afeb-228">Cuando los usuarios se autentican mediante el uso de OpenID Connect, Azure AD B2C devuelve una aplicación de toohello token de identificador que contiene **notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="6afeb-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token toohello app that contains **claims**.</span></span> <span data-ttu-id="6afeb-229">Estos son aserciones sobre usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="6afeb-229">These are assertions about hello user.</span></span> <span data-ttu-id="6afeb-230">Puede usar toopersonalize de notificaciones de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6afeb-230">You can use claims toopersonalize your app.</span></span>

<span data-ttu-id="6afeb-231">Abra hello `Controllers\HomeController.cs` archivo.</span><span class="sxs-lookup"><span data-stu-id="6afeb-231">Open hello `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="6afeb-232">Puede tener acceso a notificaciones de usuario en los controladores a través de hello `ClaimsPrincipal.Current` objeto de entidad de seguridad.</span><span class="sxs-lookup"><span data-stu-id="6afeb-232">You can access user claims in your controllers via hello `ClaimsPrincipal.Current` security principal object.</span></span>

```CSharp
// Controllers\HomeController.cs

[Authorize]
public ActionResult Claims()
{
    Claim displayName = ClaimsPrincipal.Current.FindFirst(ClaimsPrincipal.Current.Identities.First().NameClaimType);
    ViewBag.DisplayName = displayName != null ? displayName.Value : string.Empty;
    return View();
}
```

<span data-ttu-id="6afeb-233">Puede tener acceso a cualquier notificación que recibe la aplicación Hola igual manera.</span><span class="sxs-lookup"><span data-stu-id="6afeb-233">You can access any claim that your application receives in hello same way.</span></span>  <span data-ttu-id="6afeb-234">Una lista de todas las notificaciones de hello recibe de la aplicación hello está disponible para usted en hello **notificaciones** página.</span><span class="sxs-lookup"><span data-stu-id="6afeb-234">A list of all hello claims hello app receives is available for you on hello **Claims** page.</span></span>
