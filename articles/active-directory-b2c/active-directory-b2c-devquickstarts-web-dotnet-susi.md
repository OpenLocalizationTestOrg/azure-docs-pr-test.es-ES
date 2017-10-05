---
title: Azure Active Directory B2C | Microsoft Docs
description: "Cómo crear una aplicación web que tiene procesos de registro e inicio de sesión, edición de perfil y restablecimiento de contraseña mediante Azure Active Directory B2C."
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
ms.openlocfilehash: 3144ced01b524abb035dc1c6f0cdf764bec46804
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-with-azure-active-directory-b2c-sign-up-sign-in-profile-edit-and-password-reset"></a><span data-ttu-id="41c84-103">Creación de una aplicación web de ASP.NET con procesos de registro e inicio de sesión, edición de perfil y restablecimiento de contraseña de Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="41c84-103">Create an ASP.NET web app with Azure Active Directory B2C sign-up, sign-in, profile edit, and password reset</span></span>

<span data-ttu-id="41c84-104">En este tutorial se muestra cómo realizar las siguientes acciones:</span><span class="sxs-lookup"><span data-stu-id="41c84-104">This tutorial shows you how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="41c84-105">Agregar características de identidad de Azure AD B2C a la aplicación web</span><span class="sxs-lookup"><span data-stu-id="41c84-105">Add Azure AD B2C identity features to your web app</span></span>
> * <span data-ttu-id="41c84-106">Registrar la aplicación web en el directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="41c84-106">Register your web app in your Azure AD B2C directory</span></span>
> * <span data-ttu-id="41c84-107">Crear una directiva de registro e inicio de sesión de usuario, edición de perfil y restablecimiento de contraseña para la aplicación web</span><span class="sxs-lookup"><span data-stu-id="41c84-107">Create a user sign-up/sign-in, profile edit, and password reset policy for your web app</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41c84-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="41c84-108">Prerequisites</span></span>

- <span data-ttu-id="41c84-109">Debe conectar el inquilino B2C a una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="41c84-109">You must connect your B2C Tenant to an Azure account.</span></span> <span data-ttu-id="41c84-110">Puede crear una cuenta de Azure gratuita [aquí](https://azure.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="41c84-110">You can create a free Azure account [here](https://azure.microsoft.com/en-us/).</span></span>
- <span data-ttu-id="41c84-111">Necesita [Microsoft Visual Studio](https://www.visualstudio.com/) o un programa similar para ver y modificar el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41c84-111">You need [Microsoft Visual Studio](https://www.visualstudio.com/) or a similar program to view and modify the sample code.</span></span>

## <a name="create-an-azure-ad-b2c-directory"></a><span data-ttu-id="41c84-112">Creación de un directorio de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="41c84-112">Create an Azure AD B2C directory</span></span>

<span data-ttu-id="41c84-113">Para poder usar Azure AD B2C, debe crear un directorio o inquilino.</span><span class="sxs-lookup"><span data-stu-id="41c84-113">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="41c84-114">Un directorio es un contenedor de todos los usuarios, aplicaciones, grupos, etc.</span><span class="sxs-lookup"><span data-stu-id="41c84-114">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="41c84-115">Si aún no tiene uno, cree un directorio B2C antes de continuar con esta guía.</span><span class="sxs-lookup"><span data-stu-id="41c84-115">If you don't have one already, create a B2C directory before you continue in this guide.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

> [!NOTE]
> 
> <span data-ttu-id="41c84-116">Debe conectar el inquilino B2C a su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="41c84-116">You need to connect the B2C Tenant to your Azure subscription.</span></span> <span data-ttu-id="41c84-117">Tras seleccionar **Crear**, seleccione la opción **Vincular un inquilino de Azure AD B2C existente a mi suscripción de Azure** y, a continuación, en el menú desplegable **Inquilino de Azure AD B2C**, seleccione el inquilino que desea asociar.</span><span class="sxs-lookup"><span data-stu-id="41c84-117">After selecting **Create**, select the **Link an existing Azure AD B2C Tenant to my Azure subscription** option, and then in the **Azure AD B2C Tenant** drop down, select the tenant you want to associate.</span></span>

## <a name="create-and-register-an-application"></a><span data-ttu-id="41c84-118">Creación y registro de una aplicación</span><span class="sxs-lookup"><span data-stu-id="41c84-118">Create and register an application</span></span>

<span data-ttu-id="41c84-119">A continuación, debe crear y registrar la aplicación en su directorio B2C.</span><span class="sxs-lookup"><span data-stu-id="41c84-119">Next, you need to create and register the app in your B2C directory.</span></span> <span data-ttu-id="41c84-120">Esto proporciona información que Azure AD B2C necesita para comunicarse de forma segura con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-120">This provides information that Azure AD B2C needs to securely communicate with your app.</span></span> 

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

<span data-ttu-id="41c84-121">Cuando haya terminado, tendrá una API y una aplicación nativa en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-121">When you are done, you will have both an API and a native application in your application settings.</span></span>

## <a name="create-policies-on-your-b2c-tenant"></a><span data-ttu-id="41c84-122">Creación de directivas en el inquilino B2C</span><span class="sxs-lookup"><span data-stu-id="41c84-122">Create policies on your B2C tenant</span></span>

<span data-ttu-id="41c84-123">En Azure AD B2C, cada experiencia del usuario se define mediante una [directiva](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="41c84-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="41c84-124">Este ejemplo de código contiene tres experiencias de identidad: **registro e inicio de sesión**, **edición de perfil** y **restablecimiento de contraseña**.</span><span class="sxs-lookup"><span data-stu-id="41c84-124">This code sample contains three identity experiences: **sign-up & sign-in**, **profile edit**, and **password reset**.</span></span>  <span data-ttu-id="41c84-125">Debe crear una directiva de cada tipo, como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="41c84-125">You need to create one policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="41c84-126">Para cada directiva, asegúrese de seleccionar el atributo o notificación Nombre para mostrar y de copiar el nombre de su directiva para un uso posterior.</span><span class="sxs-lookup"><span data-stu-id="41c84-126">For each policy, be sure to select the Display name attribute or claim, and to copy down the name of your policy for later use.</span></span>

### <a name="add-your-identity-providers"></a><span data-ttu-id="41c84-127">Incorporación de sus proveedores de identidades</span><span class="sxs-lookup"><span data-stu-id="41c84-127">Add your identity providers</span></span>

<span data-ttu-id="41c84-128">En la configuración, seleccione **Proveedores de identidades** y elija Registro de nombre de usuario o Registro por correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="41c84-128">From your settings, select **Identity Providers** and choose Username signup or Email signup.</span></span>

### <a name="create-a-sign-up-and-sign-in-policy"></a><span data-ttu-id="41c84-129">Creación de una directiva de registro o de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="41c84-129">Create a sign-up and sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

### <a name="create-a-profile-editing-policy"></a><span data-ttu-id="41c84-130">Creación de una directiva de edición de perfil</span><span class="sxs-lookup"><span data-stu-id="41c84-130">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

### <a name="create-a-password-reset-policy"></a><span data-ttu-id="41c84-131">Crear una directiva de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="41c84-131">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

<span data-ttu-id="41c84-132">Después de crear las directivas, ya podrá compilar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-132">After you create your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="41c84-133">Descarga del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="41c84-133">Download the sample code</span></span>

<span data-ttu-id="41c84-134">El código de este tutorial se conserva [en GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span><span class="sxs-lookup"><span data-stu-id="41c84-134">The code for this tutorial is maintained on [GitHub](https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi).</span></span> <span data-ttu-id="41c84-135">Puede clonar el ejemplo al ejecutar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41c84-135">You can clone the sample by running:</span></span>

```console
git clone https://github.com/Azure-Samples/active-directory-b2c-dotnet-webapp-and-webapi.git
```

<span data-ttu-id="41c84-136">Una vez descargado el código de ejemplo, abra el archivo .sln de Visual Studio para empezar.</span><span class="sxs-lookup"><span data-stu-id="41c84-136">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="41c84-137">El archivo de solución contiene dos proyectos: `TaskWebApp` y `TaskService`.</span><span class="sxs-lookup"><span data-stu-id="41c84-137">The solution file contains two projects: `TaskWebApp` and `TaskService`.</span></span> <span data-ttu-id="41c84-138">`TaskWebApp` es la aplicación web MVC con la que el usuario interactúa.</span><span class="sxs-lookup"><span data-stu-id="41c84-138">`TaskWebApp` is the MVC web application that the user interacts with.</span></span> <span data-ttu-id="41c84-139">`TaskService` es la API web del back-end de la aplicación que almacena la lista de tareas pendientes de cada usuario.</span><span class="sxs-lookup"><span data-stu-id="41c84-139">`TaskService` is the app's back-end web API that stores each user's to-do list.</span></span> <span data-ttu-id="41c84-140">En este artículo se describe únicamente la aplicación `TaskWebApp`.</span><span class="sxs-lookup"><span data-stu-id="41c84-140">This article will only discuss the `TaskWebApp` application.</span></span> <span data-ttu-id="41c84-141">Para más información sobre cómo crear `TaskService` con Azure AD B2C, consulte [nuestro tutorial de aplicaciones web .NET](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="41c84-141">To learn how to build `TaskService` using Azure AD B2C, see [our .NET web api tutorial](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="update-code-to-use-your-tenant-and-policies"></a><span data-ttu-id="41c84-142">Actualización del código para usar el inquilino y las directivas</span><span class="sxs-lookup"><span data-stu-id="41c84-142">Update code to use your tenant and policies</span></span>

<span data-ttu-id="41c84-143">Nuestro ejemplo está configurado para usar las directivas y el identificador de cliente de nuestro inquilino de demostración.</span><span class="sxs-lookup"><span data-stu-id="41c84-143">Our sample is configured to use the policies and client ID of our demo tenant.</span></span> <span data-ttu-id="41c84-144">Para conectarlo a su propio inquilino, debe abrir `web.config` en el proyecto `TaskWebApp` y reemplazar los valores siguientes:</span><span class="sxs-lookup"><span data-stu-id="41c84-144">To connect it to your own tenant, you need to open `web.config` in the `TaskWebApp` project and replace the following values:</span></span>

* <span data-ttu-id="41c84-145">`ida:Tenant` por el nombre del inquilino</span><span class="sxs-lookup"><span data-stu-id="41c84-145">`ida:Tenant` with your tenant name</span></span>
* <span data-ttu-id="41c84-146">`ida:ClientId` por el identificador de la aplicación de API web</span><span class="sxs-lookup"><span data-stu-id="41c84-146">`ida:ClientId` with your web app application ID</span></span>
* <span data-ttu-id="41c84-147">`ida:ClientSecret` por la clave secreta de aplicación web</span><span class="sxs-lookup"><span data-stu-id="41c84-147">`ida:ClientSecret` with your web app secret key</span></span>
* <span data-ttu-id="41c84-148">`ida:SignUpSignInPolicyId` por el nombre de directiva "Inicio de sesión o registro"</span><span class="sxs-lookup"><span data-stu-id="41c84-148">`ida:SignUpSignInPolicyId` with your "Sign-up or Sign-in" policy name</span></span>
* <span data-ttu-id="41c84-149">`ida:EditProfilePolicyId` por el nombre de la directiva "Editar perfil"</span><span class="sxs-lookup"><span data-stu-id="41c84-149">`ida:EditProfilePolicyId` with your "Edit Profile" policy name</span></span>
* <span data-ttu-id="41c84-150">`ida:ResetPasswordPolicyId` por el nombre de la directiva "Restablecer contraseña"</span><span class="sxs-lookup"><span data-stu-id="41c84-150">`ida:ResetPasswordPolicyId` with your "Reset Password" policy name</span></span>

## <a name="launch-the-app"></a><span data-ttu-id="41c84-151">Inicio de la aplicación</span><span class="sxs-lookup"><span data-stu-id="41c84-151">Launch the app</span></span>
<span data-ttu-id="41c84-152">Desde Visual Studio, inicie la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-152">From within Visual Studio, launch the app.</span></span> <span data-ttu-id="41c84-153">Vaya a la pestaña Lista de tareas pendientes y tenga en cuenta que la dirección URL es: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span><span class="sxs-lookup"><span data-stu-id="41c84-153">Navigate to the To-Do List tab, and note the URl is: https://login.microsoftonline.com/*YourTenantName*/oauth2/v2.0/authorize?p=*YourSignUpPolicyName*&client_id=*YourclientID*.....</span></span>

<span data-ttu-id="41c84-154">Regístrese en la aplicación con su dirección de correo electrónico o nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="41c84-154">Sign up for the app by using your email address or user name.</span></span> <span data-ttu-id="41c84-155">Cierre sesión, vuelva a iniciarla, edite el perfil o restablezca la contraseña.</span><span class="sxs-lookup"><span data-stu-id="41c84-155">Sign out, then sign in again and edit the profile or reset the password.</span></span> <span data-ttu-id="41c84-156">Cierre la sesión y iníciela con otro usuario diferente.</span><span class="sxs-lookup"><span data-stu-id="41c84-156">Sign out and sign in as a different user.</span></span> 

## <a name="add-social-idps"></a><span data-ttu-id="41c84-157">Agregar IDP sociales</span><span class="sxs-lookup"><span data-stu-id="41c84-157">Add social IDPs</span></span>

<span data-ttu-id="41c84-158">Actualmente, la aplicación solo admite procesos de registro e inicio de sesión de usuario mediante **cuentas locales**; cuentas almacenadas en su directorio B2C que usan el nombre y la contraseña de un usuario.</span><span class="sxs-lookup"><span data-stu-id="41c84-158">Currently, the app supports only user sign-up and sign-in by using **local accounts**; accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="41c84-159">Con Azure AD B2C, puede agregar compatibilidad con otros **proveedores de identidades** (IDP) sin cambiar el código.</span><span class="sxs-lookup"><span data-stu-id="41c84-159">By using Azure AD B2C, you can add support for other **identity providers** (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="41c84-160">Para agregar proveedores de identidades sociales a su aplicación, comience siguiendo las instrucciones detalladas en estos artículos.</span><span class="sxs-lookup"><span data-stu-id="41c84-160">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="41c84-161">Para cada proveedor de identidades que desee admitir, necesitará registrar una aplicación en ese sistema y obtener un identificador de cliente.</span><span class="sxs-lookup"><span data-stu-id="41c84-161">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="41c84-162">Configurar Facebook como una IDP</span><span class="sxs-lookup"><span data-stu-id="41c84-162">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="41c84-163">Configurar Google como una IDP</span><span class="sxs-lookup"><span data-stu-id="41c84-163">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="41c84-164">Configurar Amazon como una IDP</span><span class="sxs-lookup"><span data-stu-id="41c84-164">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="41c84-165">Configurar LinkedIn como una IDP</span><span class="sxs-lookup"><span data-stu-id="41c84-165">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="41c84-166">Después de agregar los proveedores de identidades a su directorio B2C, edite cada una de las tres directivas para incluir los nuevos proveedores de identidades, tal como se describe en el [artículo de referencia de las directivas](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="41c84-166">After you add the identity providers to your B2C directory, edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="41c84-167">Después de guardar las directivas, vuelva a ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-167">After you save your policies, run the app again.</span></span>  <span data-ttu-id="41c84-168">Debería ver los proveedores de identidades nuevos agregados como opciones de inicio de sesión y registro en cada una de sus experiencias de identidad.</span><span class="sxs-lookup"><span data-stu-id="41c84-168">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="41c84-169">Puede experimentar con las directivas y observar el efecto en la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41c84-169">You can experiment with your policies and observe the effect on your sample app.</span></span> <span data-ttu-id="41c84-170">Agregue o quite proveedores de identidades, manipule notificaciones de aplicación o cambie atributos de registro.</span><span class="sxs-lookup"><span data-stu-id="41c84-170">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="41c84-171">Experimente para ver cómo se combinan las directivas, las solicitudes de autenticación y OWIN.</span><span class="sxs-lookup"><span data-stu-id="41c84-171">Experiment until you can see how policies, authentication requests, and OWIN tie together.</span></span>

## <a name="sample-code-walkthrough"></a><span data-ttu-id="41c84-172">Tutorial de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="41c84-172">Sample code walkthrough</span></span>
<span data-ttu-id="41c84-173">En las secciones siguientes se muestra cómo está configurado el código de la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41c84-173">The following sections show you how the sample application code is configured.</span></span> <span data-ttu-id="41c84-174">Puede usar dicho tutorial como guía en su futuro desarrollo de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="41c84-174">You may use this as a guide in your future app development.</span></span>

### <a name="add-authentication-support"></a><span data-ttu-id="41c84-175">Incorporación de compatibilidad con la autenticación</span><span class="sxs-lookup"><span data-stu-id="41c84-175">Add authentication support</span></span>

<span data-ttu-id="41c84-176">Ahora puede configurar la aplicación para que use Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41c84-176">You can now configure your app to use Azure AD B2C.</span></span> <span data-ttu-id="41c84-177">La aplicación se comunica con Azure AD B2C mediante el envío de solicitudes de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="41c84-177">Your app communicates with Azure AD B2C by sending OpenID Connect authentication requests.</span></span> <span data-ttu-id="41c84-178">Las solicitudes indican la experiencia del usuario que la aplicación desea ejecutar mediante la especificación de la directiva.</span><span class="sxs-lookup"><span data-stu-id="41c84-178">The requests dictate the user experience your app wants to execute by specifying the policy.</span></span> <span data-ttu-id="41c84-179">Puede usar la biblioteca OWIN de Microsoft para enviar estas solicitudes, ejecutar directivas, administrar sesiones de usuario, etc.</span><span class="sxs-lookup"><span data-stu-id="41c84-179">You can use Microsoft's OWIN library to send these requests, execute policies, manage user sessions, and more.</span></span>

#### <a name="install-owin"></a><span data-ttu-id="41c84-180">Instalar OWIN</span><span class="sxs-lookup"><span data-stu-id="41c84-180">Install OWIN</span></span>

<span data-ttu-id="41c84-181">Para comenzar, agregue los paquetes de NuGet de middleware OWIN al proyecto mediante la Consola del Administrador de paquetes de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="41c84-181">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console.</span></span>

```Console
PM> Install-Package Microsoft.Owin.Security.OpenIdConnect
PM> Install-Package Microsoft.Owin.Security.Cookies
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

#### <a name="add-an-owin-startup-class"></a><span data-ttu-id="41c84-182">Agregar una clase de inicio de OWIN</span><span class="sxs-lookup"><span data-stu-id="41c84-182">Add an OWIN startup class</span></span>

<span data-ttu-id="41c84-183">Agregue una clase de inicio OWIN a la API llamada `Startup.cs`.</span><span class="sxs-lookup"><span data-stu-id="41c84-183">Add an OWIN startup class to the API called `Startup.cs`.</span></span>  <span data-ttu-id="41c84-184">Haga clic con el botón derecho en el proyecto, seleccione **Agregar** y **Nuevo elemento**; después, busque OWIN.</span><span class="sxs-lookup"><span data-stu-id="41c84-184">Right-click on the project, select **Add** and **New Item**, and then search for OWIN.</span></span> <span data-ttu-id="41c84-185">El middleware OWIN invocará el método `Configuration(…)` al iniciarse la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-185">The OWIN middleware will invoke the `Configuration(…)` method when your app starts.</span></span>

<span data-ttu-id="41c84-186">En nuestro ejemplo, hemos cambiado la declaración de clase a `public partial class Startup` y hemos implementado la otra parte de la clase en `App_Start\Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="41c84-186">In our sample, we changed the class declaration to `public partial class Startup` and implemented the other part of the class in `App_Start\Startup.Auth.cs`.</span></span> <span data-ttu-id="41c84-187">En el método `Configuration`, se agrega una llamada a `ConfigureAuth`, que se define en `Startup.Auth.cs`.</span><span class="sxs-lookup"><span data-stu-id="41c84-187">Inside the `Configuration` method, we added a call to `ConfigureAuth`, which is defined in `Startup.Auth.cs`.</span></span> <span data-ttu-id="41c84-188">Después de las modificaciones, `Startup.cs` es similar a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41c84-188">After the modifications, `Startup.cs` looks like the following:</span></span>

```CSharp
// Startup.cs

public partial class Startup
{
    // The OWIN middleware will invoke this method when the app starts
    public void Configuration(IAppBuilder app)
    {
        // ConfigureAuth defined in other part of the class
        ConfigureAuth(app);
    }
}
```

#### <a name="configure-the-authentication-middleware"></a><span data-ttu-id="41c84-189">Configuración del middleware de autenticación</span><span class="sxs-lookup"><span data-stu-id="41c84-189">Configure the authentication middleware</span></span>

<span data-ttu-id="41c84-190">Abra el archivo `App_Start\Startup.Auth.cs` e implemente el método `ConfigureAuth(...)`.</span><span class="sxs-lookup"><span data-stu-id="41c84-190">Open the file `App_Start\Startup.Auth.cs` and implement the `ConfigureAuth(...)` method.</span></span> <span data-ttu-id="41c84-191">Los parámetros que proporciona en `OpenIdConnectAuthenticationOptions` sirven como coordenadas para que su aplicación se comunique con Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41c84-191">The parameters you provide in `OpenIdConnectAuthenticationOptions` serve as coordinates for your app to communicate with Azure AD B2C.</span></span> <span data-ttu-id="41c84-192">Si no especifica ciertos parámetros, se usará el valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="41c84-192">If you do not specify certain parameters, it will use the default value.</span></span> <span data-ttu-id="41c84-193">Por ejemplo, se especifica el valor `ResponseType` en el ejemplo, por lo que el valor predeterminado `code id_token` se usará en cada una de las solicitudes salientes a Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41c84-193">For example, we do not specify the `ResponseType` in the sample, so the default value `code id_token` will be used in each outgoing request to Azure AD B2C.</span></span>

<span data-ttu-id="41c84-194">También debe configurar la autenticación de cookies.</span><span class="sxs-lookup"><span data-stu-id="41c84-194">You also need to set up cookie authentication.</span></span> <span data-ttu-id="41c84-195">El middleware OpenID Connect usa cookies para mantener las sesiones de usuario, entre otras cosas.</span><span class="sxs-lookup"><span data-stu-id="41c84-195">The OpenID Connect middleware uses cookies to maintain user sessions, among other things.</span></span>

```CSharp
// App_Start\Startup.Auth.cs

public partial class Startup
{
    // Initialize variables ...

    // Configure the OWIN middleware
    public void ConfigureAuth(IAppBuilder app)
    {
        app.UseCookieAuthentication(new CookieAuthenticationOptions());
        app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

        app.UseOpenIdConnectAuthentication(
            new OpenIdConnectAuthenticationOptions
            {
                // Generate the metadata address using the tenant and policy information
                MetadataAddress = String.Format(AadInstance, Tenant, DefaultPolicy),

                // These are standard OpenID Connect parameters, with values pulled from web.config
                ClientId = ClientId,
                RedirectUri = RedirectUri,
                PostLogoutRedirectUri = RedirectUri,

                // Specify the callbacks for each type of notifications
                Notifications = new OpenIdConnectAuthenticationNotifications
                {
                    RedirectToIdentityProvider = OnRedirectToIdentityProvider,
                    AuthorizationCodeReceived = OnAuthorizationCodeReceived,
                    AuthenticationFailed = OnAuthenticationFailed,
                },

                // Specify the claims to validate
                TokenValidationParameters = new TokenValidationParameters
                {
                    NameClaimType = "name"
                },

                // Specify the scope by appending all of the scopes requested into one string (seperated by a blank space)
                Scope = $"{OpenIdConnectScopes.OpenId} {ReadTasksScope} {WriteTasksScope}"
            }
        );
    }

    // Implement the "Notification" methods...
}
```

<span data-ttu-id="41c84-196">En el valor `OpenIdConnectAuthenticationOptions` anterior, definimos un conjunto de funciones de devolución de llamada para notificaciones específicas que recibe el middleware de OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="41c84-196">In `OpenIdConnectAuthenticationOptions` above, we define a set of callback functions for specific notifications that are received by the OpenID Connect middleware.</span></span> <span data-ttu-id="41c84-197">Estos comportamientos se definen con un objeto `OpenIdConnectAuthenticationNotifications` y se almacenan en la variable `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="41c84-197">These behaviors are defined using a `OpenIdConnectAuthenticationNotifications` object and stored into the `Notifications` variable.</span></span> <span data-ttu-id="41c84-198">En el ejemplo, se definen tres devoluciones de llamada distintas en función del evento.</span><span class="sxs-lookup"><span data-stu-id="41c84-198">In our sample, we define three different callbacks depending on the event.</span></span>

### <a name="using-different-policies"></a><span data-ttu-id="41c84-199">Uso de distintas directivas</span><span class="sxs-lookup"><span data-stu-id="41c84-199">Using different policies</span></span>

<span data-ttu-id="41c84-200">La notificación `RedirectToIdentityProvider` se desencadena cada vez que se realiza una solicitud a Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41c84-200">The `RedirectToIdentityProvider` notification is triggered whenever a request is made to Azure AD B2C.</span></span> <span data-ttu-id="41c84-201">En la función de devolución de llamada `OnRedirectToIdentityProvider`, protegemos la llamada saliente si deseamos usar otra directiva.</span><span class="sxs-lookup"><span data-stu-id="41c84-201">In the callback function `OnRedirectToIdentityProvider`, we check in the outgoing call if we want to use a different policy.</span></span> <span data-ttu-id="41c84-202">Para hacer un restablecimiento de contraseña o editar un perfil, se debe usar la directiva correspondiente, como la directiva de restablecimiento de contraseña en lugar de la directiva "Registro o inicio de sesión" predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41c84-202">In order to do a password reset or edit a profile, you need to use the corresponding policy such as the password reset policy instead of the default "Sign-up or Sign-in" policy.</span></span>

<span data-ttu-id="41c84-203">En nuestro ejemplo, cuando un usuario desea restablecer la contraseña o editar el perfil, se agrega la directiva que se prefiere usar en el contexto de OWIN.</span><span class="sxs-lookup"><span data-stu-id="41c84-203">In our sample, when a user wants to reset the password or edit the profile, we add the policy we prefer to use into the OWIN context.</span></span> <span data-ttu-id="41c84-204">Para ello, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41c84-204">That can be done by doing the following:</span></span>

```CSharp
    // Let the middleware know you are trying to use the edit profile policy
    HttpContext.GetOwinContext().Set("Policy", EditProfilePolicyId);
```

<span data-ttu-id="41c84-205">Además, puede implementar la función de devolución de llamada `OnRedirectToIdentityProvider` si hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41c84-205">And you can implement the callback function `OnRedirectToIdentityProvider` by doing the following:</span></span>

```CSharp
/*
*  On each call to Azure AD B2C, check if a policy (e.g. the profile edit or password reset policy) has been specified in the OWIN context.
*  If so, use that policy when making the call. Also, don't request a code (since it won't be needed).
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

### <a name="handling-authorization-codes"></a><span data-ttu-id="41c84-206">Control de códigos de autorización</span><span class="sxs-lookup"><span data-stu-id="41c84-206">Handling authorization codes</span></span>

<span data-ttu-id="41c84-207">La notificación `AuthorizationCodeReceived` se desactiva cuando se recibe un código de autorización.</span><span class="sxs-lookup"><span data-stu-id="41c84-207">The `AuthorizationCodeReceived` notification is triggered when an authorization code is received.</span></span> <span data-ttu-id="41c84-208">El middleware de OpenID Connect no admite el intercambio de códigos por tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="41c84-208">The OpenID Connect middleware does not support exchanging codes for access tokens.</span></span> <span data-ttu-id="41c84-209">Puede intercambiar manualmente el código por el token en una función de devolución de llamada.</span><span class="sxs-lookup"><span data-stu-id="41c84-209">You can manually exchange the code for the token in a callback function.</span></span> <span data-ttu-id="41c84-210">Para más información, consulte la [documentación](active-directory-b2c-devquickstarts-web-api-dotnet.md) que explica cómo hacerlo.</span><span class="sxs-lookup"><span data-stu-id="41c84-210">For more information, please look at the [documentation](active-directory-b2c-devquickstarts-web-api-dotnet.md) that explains how.</span></span>

### <a name="handling-errors"></a><span data-ttu-id="41c84-211">Control de errores</span><span class="sxs-lookup"><span data-stu-id="41c84-211">Handling errors</span></span>

<span data-ttu-id="41c84-212">La notificación `AuthenticationFailed` se desencadena si se produce un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="41c84-212">The `AuthenticationFailed` notification is triggered when authentication fails.</span></span> <span data-ttu-id="41c84-213">En su método de devolución de llamada, puede controlar los errores como desee hacerlo.</span><span class="sxs-lookup"><span data-stu-id="41c84-213">In its callback method, you can handle the errors as you wish.</span></span> <span data-ttu-id="41c84-214">Sin embargo, debe agregar una comprobación del código de error `AADB2C90118`.</span><span class="sxs-lookup"><span data-stu-id="41c84-214">You should however add a check for the error code `AADB2C90118`.</span></span> <span data-ttu-id="41c84-215">Durante la ejecución de la directiva "Registro o inicio de sesión", el usuario tiene la oportunidad de seleccionar un vínculo **¿Ha olvidado la contraseña?**.</span><span class="sxs-lookup"><span data-stu-id="41c84-215">During the execution of the "Sign-up or Sign-in" policy, the user has the opportunity to select a **Forgot your password?** link.</span></span> <span data-ttu-id="41c84-216">En este evento, Azure AD B2C envía a la aplicación ese código de error indicando que la aplicación debe realizar una solicitud con la directiva de restablecimiento de contraseña en su lugar.</span><span class="sxs-lookup"><span data-stu-id="41c84-216">In this event, Azure AD B2C sends your app that error code indicating that your app should make a request using the password reset policy instead.</span></span>

```CSharp
/*
* Catch any failures received by the authentication middleware and handle appropriately
*/
private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> notification)
{
    notification.HandleResponse();

    // Handle the error code that Azure AD B2C throws when trying to reset a password from the login page
    // because password reset is not supported by a "sign-up or sign-in policy"
    if (notification.ProtocolMessage.ErrorDescription != null && notification.ProtocolMessage.ErrorDescription.Contains("AADB2C90118"))
    {
        // If the user clicked the reset password link, redirect to the reset password route
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

### <a name="send-authentication-requests-to-azure-ad"></a><span data-ttu-id="41c84-217">Enviar solicitudes de autenticación a Azure AD</span><span class="sxs-lookup"><span data-stu-id="41c84-217">Send authentication requests to Azure AD</span></span>

<span data-ttu-id="41c84-218">Ahora la aplicación está correctamente configurada para comunicarse con Azure AD B2C mediante el protocolo de autenticación OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="41c84-218">Your app is now properly configured to communicate with Azure AD B2C by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="41c84-219">OWIN administra los detalles de la creación de mensajes de autenticación, validación de tokens de Azure AD B2C y mantenimiento de la sesión de usuario.</span><span class="sxs-lookup"><span data-stu-id="41c84-219">OWIN manages the details of crafting authentication messages, validating tokens from Azure AD B2C, and maintaining user session.</span></span> <span data-ttu-id="41c84-220">Todo lo que queda es iniciar cada flujo de usuarios.</span><span class="sxs-lookup"><span data-stu-id="41c84-220">All that remains is to initiate each user's flow.</span></span>

<span data-ttu-id="41c84-221">Cuando un usuario selecciona **Registrarse o Iniciar sesión**, **Editar perfil** o **Restablecer contraseña** en la aplicación web, se invoca la acción asociada en `Controllers\AccountController.cs`:</span><span class="sxs-lookup"><span data-stu-id="41c84-221">When a user selects **Sign up/Sign in**, **Edit profile**, or **Reset password** in the web app, the associated action is invoked in `Controllers\AccountController.cs`:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign up or sign in
*/
public void SignUpSignIn()
{
    // Use the default policy to process the sign up / sign in flow
    if (!Request.IsAuthenticated)
    {
        HttpContext.GetOwinContext().Authentication.Challenge();
        return;
    }

    Response.Redirect("/");
}

/*
*  Called when requesting to edit a profile
*/
public void EditProfile()
{
    if (Request.IsAuthenticated)
    {
        // Let the middleware know you are trying to use the edit profile policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
        HttpContext.GetOwinContext().Set("Policy", Startup.EditProfilePolicyId);

        // Set the page to redirect to after editing the profile
        var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
        HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

        return;
    }

    Response.Redirect("/");

}

/*
*  Called when requesting to reset a password
*/
public void ResetPassword()
{
    // Let the middleware know you are trying to use the reset password policy (see OnRedirectToIdentityProvider in Startup.Auth.cs)
    HttpContext.GetOwinContext().Set("Policy", Startup.ResetPasswordPolicyId);

    // Set the page to redirect to after changing passwords
    var authenticationProperties = new AuthenticationProperties { RedirectUri = "/" };
    HttpContext.GetOwinContext().Authentication.Challenge(authenticationProperties);

    return;
}
```

<span data-ttu-id="41c84-222">También puede usar OWIN para cerrar la sesión del usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-222">You can also use OWIN to sign out the user from the app.</span></span> <span data-ttu-id="41c84-223">En `Controllers\AccountController.cs`, tenemos:</span><span class="sxs-lookup"><span data-stu-id="41c84-223">In `Controllers\AccountController.cs` we have:</span></span>

```CSharp
// Controllers\AccountController.cs

/*
*  Called when requesting to sign out
*/
public void SignOut()
{
    // To sign out the user, you should issue an OpenIDConnect sign out request.
    if (Request.IsAuthenticated)
    {
        IEnumerable<AuthenticationDescription> authTypes = HttpContext.GetOwinContext().Authentication.GetAuthenticationTypes();
        HttpContext.GetOwinContext().Authentication.SignOut(authTypes.Select(t => t.AuthenticationType).ToArray());
        Request.GetOwinContext().Authentication.GetAuthenticationTypes();
    }
}
```

<span data-ttu-id="41c84-224">Además de invocar explícitamente una directiva, puede utilizar una etiqueta `[Authorize]` en los controladores que ejecuta una directiva si el usuario no ha iniciado sesión.</span><span class="sxs-lookup"><span data-stu-id="41c84-224">In addition to explicitly invoking a policy, you can use a `[Authorize]` tag in your controllers that executes a policy if the user is not signed in.</span></span> <span data-ttu-id="41c84-225">Abra `Controllers\HomeController.cs` y agregue la etiqueta `[Authorize]` al controlador de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="41c84-225">Open `Controllers\HomeController.cs` and add the `[Authorize]` tag to the claims controller.</span></span>  <span data-ttu-id="41c84-226">OWIN selecciona la última directiva configurada cuando se ejecuta la etiqueta `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="41c84-226">OWIN selects the last policy configured when the `[Authorize]` tag is hit.</span></span>

```CSharp
// Controllers\HomeController.cs

// You can use the Authorize decorator to execute a certain policy if the user is not already signed into the app.
[Authorize]
public ActionResult Claims()
{
  ...
```

### <a name="display-user-information"></a><span data-ttu-id="41c84-227">Mostrar información de usuario</span><span class="sxs-lookup"><span data-stu-id="41c84-227">Display user information</span></span>

<span data-ttu-id="41c84-228">Cuando se autentican los usuarios mediante OpenID Connect, Azure AD B2Cdevuelve un token de identificador a la aplicación que contiene **notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="41c84-228">When you authenticate users by using OpenID Connect, Azure AD B2C returns an ID token to the app that contains **claims**.</span></span> <span data-ttu-id="41c84-229">Se trata de aserciones sobre el usuario.</span><span class="sxs-lookup"><span data-stu-id="41c84-229">These are assertions about the user.</span></span> <span data-ttu-id="41c84-230">Puede usar notificaciones para personalizar su aplicación.</span><span class="sxs-lookup"><span data-stu-id="41c84-230">You can use claims to personalize your app.</span></span>

<span data-ttu-id="41c84-231">Abra el archivo `Controllers\HomeController.cs` .</span><span class="sxs-lookup"><span data-stu-id="41c84-231">Open the `Controllers\HomeController.cs` file.</span></span> <span data-ttu-id="41c84-232">Puede acceder a las notificaciones del usuario en sus controladores a través del objeto principal de seguridad `ClaimsPrincipal.Current` .</span><span class="sxs-lookup"><span data-stu-id="41c84-232">You can access user claims in your controllers via the `ClaimsPrincipal.Current` security principal object.</span></span>

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

<span data-ttu-id="41c84-233">Puede tener acceso a cualquier notificación que recibe su aplicación de la misma manera.</span><span class="sxs-lookup"><span data-stu-id="41c84-233">You can access any claim that your application receives in the same way.</span></span>  <span data-ttu-id="41c84-234">Tiene disponible una lista de todas las notificaciones que recibe la aplicación en la página **Reclamaciones** .</span><span class="sxs-lookup"><span data-stu-id="41c84-234">A list of all the claims the app receives is available for you on the **Claims** page.</span></span>
