---
title: "aaaProblem iniciar sesión en el sitio Web de panel de acceso toohello | Documentos de Microsoft"
description: Problemas de tootroubleshoot de instrucciones que pueden surgir al intentar toosign en toouse Hola Panel de acceso
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
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a><span data-ttu-id="3213c-103">Problema al iniciar sesión en el sitio Web de panel de acceso toohello</span><span class="sxs-lookup"><span data-stu-id="3213c-103">Problem signing in toohello access panel website</span></span>

<span data-ttu-id="3213c-104">Hola Panel de acceso es un portal basado en web que permite un usuario que tiene una empresa o centro educativo Administrador de la cuenta en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que hello Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="3213c-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="3213c-105">Un usuario que tenga las ediciones de Azure AD también puede utilizar grupos de autoservicio y capacidades de administración de aplicaciones a través de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="3213c-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="3213c-106">Hola Panel de acceso es independiente de hello portal de Azure y no requiere que los usuarios toohave una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3213c-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="3213c-107">Los usuarios puedan iniciar sesión en toohello Panel de acceso si tienen una cuenta profesional o educativa en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3213c-107">Users can sign in toohello Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="3213c-108">Los usuarios se pueden autenticar directamente mediante Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3213c-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="3213c-109">Los usuarios se pueden autenticar mediante los Servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="3213c-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="3213c-110">Los usuarios se pueden autenticar mediante Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3213c-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="3213c-111">Si un usuario tiene una suscripción para Azure u Office 365 y ha estado usando Hola portal de Azure o una aplicación de Office 365, será capaz de toouse Hola Panel de acceso sin problemas sin necesidad de toosign de nuevo.</span><span class="sxs-lookup"><span data-stu-id="3213c-111">If a user has a subscription for Azure or Office 365 and has been using hello Azure portal or an Office 365 application, they'll be able toouse hello Access Panel seamlessly without needing toosign in again.</span></span> <span data-ttu-id="3213c-112">Los usuarios autenticados no sea toosign solicitada en mediante Hola username y password para su cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3213c-112">Users who are not authenticated be prompted toosign in by using hello username and password for their account in Azure AD.</span></span> <span data-ttu-id="3213c-113">Si la organización de hello ha configurado federación, escriba el nombre de usuario de Hola es suficiente.</span><span class="sxs-lookup"><span data-stu-id="3213c-113">If hello organization has configured federation, typing hello username is sufficient.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="3213c-114">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="3213c-114">General issues toocheck first</span></span> 

-   <span data-ttu-id="3213c-115">Asegúrese de que el usuario de hello es iniciar sesión en toohello **corríjala**: <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="3213c-115">Make sure hello user is signing in toohello **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="3213c-116">Asegúrese de que el explorador del usuario de hello agregada tooits de dirección URL de Hola **sitios de confianza**</span><span class="sxs-lookup"><span data-stu-id="3213c-116">Make sure hello user’s browser has added hello URL tooits **trusted sites**</span></span>

-   <span data-ttu-id="3213c-117">Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="3213c-117">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="3213c-118">Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="3213c-118">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="3213c-119">Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**</span><span class="sxs-lookup"><span data-stu-id="3213c-119">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="3213c-120">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="3213c-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="3213c-121">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="3213c-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="3213c-122">Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="3213c-122">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="3213c-123">Asegúrese de tooalso seguro intente borrar las cookies del explorador y vuelva a probar toosign en.</span><span class="sxs-lookup"><span data-stu-id="3213c-123">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="3213c-124">Se cumplen los requisitos de explorador para hello Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="3213c-124">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="3213c-125">Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS.</span><span class="sxs-lookup"><span data-stu-id="3213c-125">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="3213c-126">toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-126">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="3213c-127">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="3213c-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="3213c-128">Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:</span><span class="sxs-lookup"><span data-stu-id="3213c-128">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="3213c-129">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="3213c-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="3213c-130">Edge en Windows 10 Anniversary Edition o posterior</span><span class="sxs-lookup"><span data-stu-id="3213c-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="3213c-131">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="3213c-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="3213c-132">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="3213c-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-hello-users-account"></a><span data-ttu-id="3213c-133">Problemas con la cuenta de usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="3213c-133">Problems with hello user’s account</span></span>

<span data-ttu-id="3213c-134">Acceso toohello Panel de acceso se puede bloquear debido tooa problema con la cuenta de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-134">Access toohello Access Panel can be blocked due tooa problem with hello user’s account.</span></span> <span data-ttu-id="3213c-135">A continuación se muestran algunas maneras de solucionar problemas con los usuarios y la configuración de sus cuentas:</span><span class="sxs-lookup"><span data-stu-id="3213c-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="3213c-136">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3213c-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="3213c-137">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="3213c-138">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="3213c-139">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="3213c-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="3213c-140">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="3213c-141">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="3213c-142">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="3213c-143">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="3213c-144">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="3213c-145">Comprobar si existe una cuenta de usuario en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3213c-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="3213c-146">toocheck si está presente, una cuenta de usuario siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3213c-146">toocheck if a user’s account is present, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-147">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-147">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-148">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-148">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-149">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-149">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-150">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-150">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-151">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-151">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-152">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-152">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-153">Compruebe las propiedades de Hola de hello usuario objeto toobe seguro de que se muestran como esperaba y no existe ningún dato.</span><span class="sxs-lookup"><span data-stu-id="3213c-153">Check hello properties of hello user object toobe sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="3213c-154">Comprobar el estado de la cuenta de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-154">Check a user’s account status</span></span>

<span data-ttu-id="3213c-155">toocheck un usuario de estado de la cuenta, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3213c-155">toocheck a user’s account status, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-156">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-156">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-157">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-157">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-158">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-158">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-159">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-159">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-160">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-160">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-161">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-161">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-162">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="3213c-162">click **Profile**.</span></span>

8.  <span data-ttu-id="3213c-163">En **configuración** Asegúrese de que **bloque iniciar sesión en** se establece demasiado**No**.</span><span class="sxs-lookup"><span data-stu-id="3213c-163">Under **Settings** ensure that **Block sign in** is set too**No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="3213c-164">Restablecer la contraseña de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-164">Reset a user’s password</span></span>

<span data-ttu-id="3213c-165">tooreset contraseña de un usuario, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="3213c-165">tooreset a user’s password, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-166">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-166">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-167">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-167">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-168">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-168">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-169">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-169">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-170">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-170">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-171">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-171">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-172">Haga clic en hello **de restablecimiento de contraseña** situado en la parte superior de Hola de hoja de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-172">click hello **Reset password** button at hello top of hello user blade.</span></span>

8.  <span data-ttu-id="3213c-173">Haga clic en hello **de restablecimiento de contraseña** botón en hello **de restablecimiento de contraseña** hoja que aparece.</span><span class="sxs-lookup"><span data-stu-id="3213c-173">click hello **Reset password** button on hello **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="3213c-174">Hola copia **contraseña temporal** o **escriba una contraseña nueva** para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-174">Copy hello **temporary password** or **enter a new password** for hello user.</span></span>

10. <span data-ttu-id="3213c-175">Este nuevo usuario toohello de contraseña se comunican, requiere toochange esta contraseña durante su próximo iniciar sesión en tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3213c-175">Communicate this new password toohello user, they be required toochange this password during their next sign in tooAzure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="3213c-176">Habilitar el autoservicio de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="3213c-176">Enable self-service password reset</span></span>

<span data-ttu-id="3213c-177">contraseña de autoservicio de tooenable restablecer, siga los pasos de implementación de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="3213c-177">tooenable self-service password reset, follow hello deployment steps below:</span></span>

-   [<span data-ttu-id="3213c-178">Habilitar usuarios tooreset sus contraseñas de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3213c-178">Enable users tooreset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="3213c-179">Habilitar usuarios tooreset o cambiar sus contraseñas locales de Active Directory</span><span class="sxs-lookup"><span data-stu-id="3213c-179">Enable users tooreset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="3213c-180">Comprobar el estado de la autenticación multifactor de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="3213c-181">toocheck un usuario de multifactor estado de autenticación, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="3213c-181">toocheck a user’s multi-factor authentication status, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-182">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-182">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-183">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-183">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-184">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-184">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-185">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-185">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-186">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-186">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-187">Haga clic en hello **la autenticación multifactor** situado en la parte superior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-187">click hello **Multi-Factor Authentication** button at hello top of hello blade.</span></span>

7.  <span data-ttu-id="3213c-188">Una vez Hola **Portal de administración de Multi-factor Authentication** cargas, asegúrese de que esté en hello **usuarios** ficha.</span><span class="sxs-lookup"><span data-stu-id="3213c-188">Once hello **Multi-Factor Authentication Administration Portal** loads, ensure you are on hello **Users** tab.</span></span>

8.  <span data-ttu-id="3213c-189">Busque el usuario de hello en lista de Hola de usuarios por búsqueda, el filtrado u ordenación.</span><span class="sxs-lookup"><span data-stu-id="3213c-189">Find hello user in hello list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="3213c-190">Usuario seleccione Hola Hola usuarios de lista y **habilitar**, **deshabilitar**, o **aplicar** la autenticación multifactor según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3213c-190">Select hello user from hello list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3213c-191">Si un usuario pertenece a un **forzado** estado, puede establecerlos demasiado**deshabilitado** temporalmente toolet volverlos a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="3213c-191">If a user is in an **Enforced** state, you may set them too**Disabled** temporarily toolet them back into their account.</span></span> <span data-ttu-id="3213c-192">Una vez que estén en, a continuación, puede cambiar su estado demasiado**habilitado** nuevo toorequire les toore su información de contacto durante su próximo iniciar sesión en el registro.</span><span class="sxs-lookup"><span data-stu-id="3213c-192">Once they are back in, you can then change their state too**Enabled** again toorequire them toore-register their contact information during their next sign in.</span></span> <span data-ttu-id="3213c-193">Como alternativa, puede seguir los pasos de Hola Hola [Compruebe la información de contacto de autenticación de un usuario](#check-a-users-authentication-contact-info) tooverify o establecer estos datos para ellos.</span><span class="sxs-lookup"><span data-stu-id="3213c-193">Alternatively, you can follow hello steps in hello [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) tooverify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="3213c-194">Comprobar la información de contacto de autenticación de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="3213c-195">toocheck autenticación de un usuario, póngase en contacto con información usada para la autenticación multifactor, acceso condicional, protección de identidad y de restablecimiento de contraseña, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3213c-195">toocheck a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-196">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-196">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-197">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-197">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-198">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-198">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-199">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-199">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-200">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-200">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-201">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-201">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-202">Haga clic en **Perfil**.</span><span class="sxs-lookup"><span data-stu-id="3213c-202">click **Profile**.</span></span>

8.  <span data-ttu-id="3213c-203">Desplácese hacia abajo demasiado**información de contacto de autenticación**.</span><span class="sxs-lookup"><span data-stu-id="3213c-203">Scroll down too**Authentication contact info**.</span></span>

9.  <span data-ttu-id="3213c-204">**Revisión** datos Hola registrado para el usuario de Hola y actualizar según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="3213c-204">**Review** hello data registered for hello user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="3213c-205">Comprobar la pertenencia a grupos de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-205">Check a user’s group memberships</span></span>

<span data-ttu-id="3213c-206">toocheck un usuario de pertenencia a grupos, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="3213c-206">toocheck a user’s group memberships, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-207">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-207">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-208">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-208">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-209">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-209">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-210">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-210">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-211">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-211">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-212">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-212">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-213">Haga clic en **grupos** toosee que agrupa usuario hello es un miembro de.</span><span class="sxs-lookup"><span data-stu-id="3213c-213">click **Groups** toosee which groups hello user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="3213c-214">Comprobar las licencias asignadas de un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="3213c-215">toocheck un usuario había asignado licencias, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="3213c-215">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-216">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-216">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-217">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-217">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-218">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-218">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-219">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-219">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-220">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-220">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-221">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-221">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-222">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="3213c-222">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="3213c-223">Asignar una licencia a un usuario</span><span class="sxs-lookup"><span data-stu-id="3213c-223">Assign a user a license</span></span> 

<span data-ttu-id="3213c-224">tooassign un usuario tooa de licencias, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3213c-224">tooassign a license tooa user, follow hello steps below:</span></span>

1.  <span data-ttu-id="3213c-225">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="3213c-225">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3213c-226">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-226">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3213c-227">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="3213c-227">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3213c-228">Haga clic en **usuarios y grupos** en el menú de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="3213c-228">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="3213c-229">Haga clic en **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="3213c-229">click **All users**.</span></span>

6.  <span data-ttu-id="3213c-230">**Búsqueda** para el usuario de Hola que le interesen y **haga clic en la fila de hello** tooselect.</span><span class="sxs-lookup"><span data-stu-id="3213c-230">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="3213c-231">Haga clic en **licencias** toosee qué usuario de hello licencias actualmente tiene asignada.</span><span class="sxs-lookup"><span data-stu-id="3213c-231">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

8.  <span data-ttu-id="3213c-232">Haga clic en hello **asignar** botón.</span><span class="sxs-lookup"><span data-stu-id="3213c-232">click hello **Assign** button.</span></span>

9.  <span data-ttu-id="3213c-233">Seleccione **uno o más productos** en lista de Hola de productos disponibles.</span><span class="sxs-lookup"><span data-stu-id="3213c-233">Select **one or more products** from hello list of available products.</span></span>

10. <span data-ttu-id="3213c-234">**Opcional** haga clic en hello **opciones de asignación** elemento toogranularly asignar productos.</span><span class="sxs-lookup"><span data-stu-id="3213c-234">**Optional** click hello **assignment options** item toogranularly assign products.</span></span> <span data-ttu-id="3213c-235">Cuando haya finalizado este procedimiento, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="3213c-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="3213c-236">Haga clic en hello **asignar** botón tooassign estos usuario toothis de licencias.</span><span class="sxs-lookup"><span data-stu-id="3213c-236">Click hello **Assign** button tooassign these licenses toothis user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="3213c-237">Si estos pasos no resuelven el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="3213c-237">If these troubleshooting steps do not resolve hello issue</span></span>

<span data-ttu-id="3213c-238">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="3213c-238">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="3213c-239">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="3213c-239">Correlation error ID</span></span>

-   <span data-ttu-id="3213c-240">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="3213c-240">UPN (user email address)</span></span>

-   <span data-ttu-id="3213c-241">Id. de inquilino</span><span class="sxs-lookup"><span data-stu-id="3213c-241">Tenant ID</span></span>

-   <span data-ttu-id="3213c-242">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="3213c-242">Browser type</span></span>

-   <span data-ttu-id="3213c-243">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="3213c-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3213c-244">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="3213c-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3213c-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3213c-245">Next steps</span></span>
[<span data-ttu-id="3213c-246">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="3213c-246">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
