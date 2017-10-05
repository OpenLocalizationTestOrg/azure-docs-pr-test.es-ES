---
title: "Problema al iniciar sesión en el sitio web del Panel de acceso | Microsoft Docs"
description: "Instrucciones para solucionar problemas que pueden surgir al intentar iniciar sesión para usar el Panel de acceso."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="5dbb5-103">Problema al iniciar sesión en el sitio web del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="5dbb5-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="5dbb5-104">El Panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa en Azure Active Directory (Azure AD) vea e inicie aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="5dbb5-105">Un usuario que posee ediciones de Azure AD también puede usar las funcionalidades de administración de grupos de autoservicio y aplicaciones a través del Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="5dbb5-106">El Panel de acceso es independiente de Azure Portal y no requiere que los usuarios tengan una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="5dbb5-107">Los usuarios pueden iniciar sesión en el Panel de acceso si tienen una cuenta profesional o educativa en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="5dbb5-108">Los usuarios se pueden autenticar directamente mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="5dbb5-109">Los usuarios se pueden autenticar mediante los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="5dbb5-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="5dbb5-110">Los usuarios se pueden autenticar mediante Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="5dbb5-111">Si un usuario tiene una suscripción de Azure u Office 365 y ha estado usando el portal de Azure o una aplicación de Office 365, dicho usuario podrá usar el Panel de acceso sin problemas sin necesidad de volver a iniciar sesión de nuevo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="5dbb5-112">A los usuarios que no se han autenticado se les solicitará que inicien sesión utilizando el nombre de usuario y la contraseña de su cuenta en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="5dbb5-113">Si la organización configuró la federación, bastará con escribir el nombre de usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="5dbb5-114">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="5dbb5-114">General issues to check first</span></span> 

-   <span data-ttu-id="5dbb5-115">Asegurarse de que el usuario inicia sesión en la **dirección URL correcta**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="5dbb5-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="5dbb5-116">Asegurarse de que el explorador del usuario ha agregado la dirección URL a sus **sitios de confianza**</span><span class="sxs-lookup"><span data-stu-id="5dbb5-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="5dbb5-117">Asegurarse de que la cuenta del usuario está **habilitada** para los inicios de sesión</span><span class="sxs-lookup"><span data-stu-id="5dbb5-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="5dbb5-118">Que la cuenta del usuario **no está bloqueada**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="5dbb5-119">Que la **contraseña del usuario no ha expirado o se ha olvidado**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="5dbb5-120">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="5dbb5-121">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="5dbb5-122">Que la **información de contacto de autenticación** del usuario está actualizada para permitir la aplicación de directivas de Multi-Factor Authentication o de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="5dbb5-123">Que se intenta borrar también las cookies del explorador y volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="5dbb5-124">Cumplimiento de los requisitos del explorador para el Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="5dbb5-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="5dbb5-125">El Panel de acceso requiere un explorador compatible con JavaScript y que tenga habilitado CSS.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="5dbb5-126">Para usar el inicio de sesión único (SSO) basado en contraseña en el Panel de acceso, se debe instalar la extensión del Panel de acceso en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="5dbb5-127">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="5dbb5-128">Para el SSO basado en contraseña, los exploradores del usuario final pueden ser:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="5dbb5-129">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="5dbb5-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="5dbb5-130">Edge en Windows 10 Anniversary Edition o posterior</span><span class="sxs-lookup"><span data-stu-id="5dbb5-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="5dbb5-131">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="5dbb5-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="5dbb5-132">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="5dbb5-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="5dbb5-133">Problemas con la cuenta del usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-133">Problems with the user’s account</span></span>

<span data-ttu-id="5dbb5-134">El acceso al Panel de acceso se puede bloquear debido a un problema con la cuenta del usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="5dbb5-135">A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="5dbb5-136">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dbb5-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="5dbb5-137">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="5dbb5-138">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="5dbb5-139">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="5dbb5-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="5dbb5-140">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="5dbb5-141">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="5dbb5-142">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="5dbb5-143">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="5dbb5-144">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="5dbb5-145">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5dbb5-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="5dbb5-146">Para comprobar si una cuenta de usuario existe, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-147">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-148">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-149">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-150">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-151">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-151">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-152">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-153">Compruebe las propiedades del objeto de usuario para asegurarse de que se muestran como esperaba y no falta ningún dato.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="5dbb5-154">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-154">Check a user’s account status</span></span>

<span data-ttu-id="5dbb5-155">Para comprobar el estado de la cuenta de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-156">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-157">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-158">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-159">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-160">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-160">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-161">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-162">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-162">click **Profile**.</span></span>

8.  <span data-ttu-id="5dbb5-163">En **Configuración**, asegúrese de que **Bloquear inicio de sesión** esté establecido en **No**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="5dbb5-164">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-164">Reset a user’s password</span></span>

<span data-ttu-id="5dbb5-165">Para restablecer la contraseña de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-166">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-167">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-168">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-169">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-170">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-170">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-171">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-172">Haga clic en el botón **Restablecer contraseña** situado en la parte superior de la hoja de usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="5dbb5-173">Haga clic en el botón **Restablecer contraseña** en la hoja **Restablecer contraseña** que aparece.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="5dbb5-174">Copie la **contraseña temporal** o **escriba una contraseña nueva** para el usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="5dbb5-175">Comunique esta nueva contraseña al usuario, quien deberá cambiarla durante el siguiente inicio de sesión en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="5dbb5-176">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="5dbb5-176">Enable self-service password reset</span></span>

<span data-ttu-id="5dbb5-177">Para habilitar el autoservicio de restablecimiento de contraseña, siga estos pasos de implementación:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="5dbb5-178">Permitir que los usuarios restablezcan sus contraseñas de Azure AD
</span><span class="sxs-lookup"><span data-stu-id="5dbb5-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="5dbb5-179">Permitir que los usuarios restablezcan o cambien sus contraseñas de AD locales</span><span class="sxs-lookup"><span data-stu-id="5dbb5-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="5dbb5-180">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="5dbb5-181">Para comprobar el estado de la autenticación multifactor de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-182">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-183">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-184">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-185">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-186">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-186">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-187">Haga clic en el botón **Multi-Factor Authentication** en la parte superior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="5dbb5-188">Después de que se ha cargado el **Portal de administración de Multi-factor Authentication**, asegúrese de que se encuentra en la pestaña **Usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="5dbb5-189">Para encontrar el usuario, filtre u ordene la lista de usuarios, o realice búsquedas en ella.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="5dbb5-190">Seleccione el usuario de la lista de usuarios y **habilite**, **deshabilite** o **exija** autenticación multifactor, según desee.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="5dbb5-191">Si un usuario se encuentra en un estado **Exigido**, puede establecerlo en **Deshabilitado** temporalmente para permitirle volver a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="5dbb5-192">Una vez de vuelta, puede cambiar de nuevo su estado a **Habilitado** para solicitarle que vuelva a registrar su información de contacto durante su siguiente inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="5dbb5-193">Como alternativa, puede seguir los pasos descritos en [Comprobar la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) para comprobar o establecer estos datos por ellos.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="5dbb5-194">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="5dbb5-195">Para comprobar la información de contacto de autenticación de un usuario para Multi-factor Authentication, acceso condicional y protección de identidad, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-196">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-197">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-198">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-199">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-200">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-200">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-201">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-202">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-202">click **Profile**.</span></span>

8.  <span data-ttu-id="5dbb5-203">Desplácese hacia abajo hasta **Información de contacto para la autenticación**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="5dbb5-204">**Revise** los datos registrados para el usuario y actualícelos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="5dbb5-205">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-205">Check a user’s group memberships</span></span>

<span data-ttu-id="5dbb5-206">Para comprobar la pertenencia a grupos de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-207">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-208">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-209">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-210">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-211">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-211">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-212">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-213">Haga clic en **Grupos** para ver de qué grupos es miembro el usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="5dbb5-214">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="5dbb5-215">Para comprobar las licencias asignadas de un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-216">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-217">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-218">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-219">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-220">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-220">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-221">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-222">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="5dbb5-223">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="5dbb5-223">Assign a user a license</span></span> 

<span data-ttu-id="5dbb5-224">Para asignar una licencia a un usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="5dbb5-225">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="5dbb5-226">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="5dbb5-227">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="5dbb5-228">Haga clic en **Usuarios y grupos** en el menú de navegación.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="5dbb5-229">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-229">click **All users**.</span></span>

6.  <span data-ttu-id="5dbb5-230">**Busque** el usuario en el que está interesado y **haga clic en la fila** para seleccionarlo.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="5dbb5-231">Haga clic en **Licencias** para ver qué licencias tiene asignadas actualmente el usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="5dbb5-232">Haga clic en el botón **Asignar**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="5dbb5-233">Seleccione **uno o más productos** en la lista de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="5dbb5-234">**Opcional**: Haga clic en el elemento **Opciones de asignación** para asignar productos de forma granular.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="5dbb5-235">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="5dbb5-236">Haga clic en el botón **Asignar** para asignar estas licencias a este usuario.</span><span class="sxs-lookup"><span data-stu-id="5dbb5-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="5dbb5-237">Si después de seguir estos pasos el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="5dbb5-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="5dbb5-238">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="5dbb5-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="5dbb5-239">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="5dbb5-239">Correlation error ID</span></span>

-   <span data-ttu-id="5dbb5-240">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="5dbb5-240">UPN (user email address)</span></span>

-   <span data-ttu-id="5dbb5-241">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="5dbb5-241">Tenant ID</span></span>

-   <span data-ttu-id="5dbb5-242">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="5dbb5-242">Browser type</span></span>

-   <span data-ttu-id="5dbb5-243">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="5dbb5-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="5dbb5-244">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="5dbb5-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dbb5-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5dbb5-245">Next steps</span></span>
[<span data-ttu-id="5dbb5-246">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="5dbb5-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
