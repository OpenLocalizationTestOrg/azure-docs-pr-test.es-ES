---
title: "aaaProblems tooan aplicación de galería de Azure AD configurada para la contraseña de inicio de sesión inicio de sesión único | Documentos de Microsoft"
description: "Se describen las áreas problemáticas que proporcionan instrucciones tootroubleshoot emite toosigning relacionado en tooAzure configuradas para inicio de sesión único en la contraseña de aplicaciones de galería de AD"
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
ms.openlocfilehash: f53ef4176db37dc6b1da2d61027155a6ba8f331e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="426be-103">Problemas para iniciar sesión en tooan configurado para inicio de sesión único en la contraseña de aplicación de galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="426be-103">Problems signing in tooan Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="426be-104">Hola Panel de acceso es un portal basado en web que permite un usuario que tiene una empresa o centro educativo Administrador de la cuenta en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que hello Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="426be-104">hello Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) tooview and launch cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="426be-105">Un usuario que tenga las ediciones de Azure AD también puede utilizar grupos de autoservicio y capacidades de administración de aplicaciones a través de hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="426be-105">A user who has Azure AD editions can also use self-service group and app management capabilities through hello Access Panel.</span></span> <span data-ttu-id="426be-106">Hola Panel de acceso es independiente de hello portal de Azure y no requiere que los usuarios toohave una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="426be-106">hello Access Panel is separate from hello Azure portal and does not require users toohave an Azure subscription.</span></span>

<span data-ttu-id="426be-107">toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-107">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="426be-108">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="426be-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="426be-109">Se cumplen los requisitos de explorador para hello Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="426be-109">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="426be-110">Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS.</span><span class="sxs-lookup"><span data-stu-id="426be-110">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="426be-111">toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-111">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="426be-112">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="426be-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="426be-113">Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:</span><span class="sxs-lookup"><span data-stu-id="426be-113">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="426be-114">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="426be-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="426be-115">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="426be-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="426be-116">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="426be-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="426be-117">extensión SSO basada en contraseña de Hello están disponibles para los bordes del 10 de Windows cuando se convierten en admite las extensiones del explorador de Edge.</span><span class="sxs-lookup"><span data-stu-id="426be-117">hello password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="426be-118">¿Cómo tooinstall Hola extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="426be-118">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="426be-119">Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="426be-119">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="426be-120">Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426be-120">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="426be-121">Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="426be-121">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="426be-122">En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="426be-122">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="426be-123">Basado en el explorador es que el vínculo de descarga de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="426be-123">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="426be-124">**Agregar** tooyour Explorador de hello extensión.</span><span class="sxs-lookup"><span data-stu-id="426be-124">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="426be-125">Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="426be-125">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="426be-126">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="426be-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="426be-127">Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña</span><span class="sxs-lookup"><span data-stu-id="426be-127">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="426be-128">También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="426be-128">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="426be-129">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="426be-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="426be-130">Extensión del Panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="426be-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="426be-131">Configuración de una directiva de grupo para Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="426be-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="426be-132">Puede configurar una directiva de grupo que le permiten tooremotely instalar extensión de Panel de acceso de Hola para Internet Explorer en equipos de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="426be-132">You can setup a group policy that allow you tooremotely install hello Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="426be-133">requisitos previos de Hello incluyen:</span><span class="sxs-lookup"><span data-stu-id="426be-133">hello prerequisites include:</span></span>

-   <span data-ttu-id="426be-134">Ha configurado [los servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), y se han unido a dominio de tooyour de máquinas de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="426be-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines tooyour domain.</span></span>

-   <span data-ttu-id="426be-135">Debe tener Hola "Editar configuración de" permiso tooedit Hola objeto de directiva de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="426be-135">You must have hello "Edit settings" permission tooedit hello Group Policy Object (GPO).</span></span> <span data-ttu-id="426be-136">De forma predeterminada, los miembros del programa Hola a los grupos de seguridad siguientes tienen este permiso: los administradores de dominio, los administradores de organización y propietarios del creador de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="426be-136">By default, members of hello following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="426be-137">[Más información](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="426be-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="426be-138">Siga el tutorial de hello [cómo tooDeploy Hola extensión del Panel de acceso para Internet Explorer utilizando la directiva de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obtener instrucciones paso a paso acerca de cómo tooconfigure Hola de directiva de grupo e implementarla toousers.</span><span class="sxs-lookup"><span data-stu-id="426be-138">Follow hello tutorial [How tooDeploy hello Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how tooconfigure hello group policy and deploy it toousers.</span></span>

## <a name="troubleshoot-hello-access-panel-in-internet-explorer"></a><span data-ttu-id="426be-139">Solucionar problemas de hello Panel de acceso en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="426be-139">Troubleshoot hello Access Panel in Internet Explorer</span></span>

<span data-ttu-id="426be-140">Siga hello [solucionar Hola extensión del Panel de acceso de Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guía para el acceso a una herramienta de diagnóstico y obtener instrucciones paso a paso acerca de cómo configurar la extensión de Hola para Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="426be-140">Follow hello [Troubleshoot hello Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring hello extension for IE.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="426be-141">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="426be-141">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="426be-142">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="426be-142">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="426be-143">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="426be-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="426be-144">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="426be-144">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="426be-145">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="426be-145">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="426be-146">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="426be-146">Add a non-gallery application</span></span>

<span data-ttu-id="426be-147">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="426be-147">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="426be-148">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="426be-148">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="426be-149">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-149">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="426be-150">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="426be-150">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="426be-151">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="426be-151">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="426be-152">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="426be-152">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="426be-153">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="426be-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="426be-154">Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="426be-154">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="426be-155">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="426be-155">Select **Add.**</span></span>

<span data-ttu-id="426be-156">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-156">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="426be-157">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="426be-157">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="426be-158">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="426be-158">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="426be-159">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="426be-159">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="426be-160">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-160">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="426be-161">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="426be-161">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="426be-162">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="426be-162">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="426be-163">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="426be-163">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="426be-164">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="426be-164">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="426be-165">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="426be-165">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="426be-166">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="426be-166">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="426be-167">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="426be-167">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="426be-168">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="426be-168">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="426be-169">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="426be-169">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="426be-170">Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="426be-170">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="426be-171">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="426be-171">Assign users toohello application.</span></span>

11. <span data-ttu-id="426be-172">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-172">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="426be-173">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="426be-173">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

### <a name="assign-users-toohello-application"></a><span data-ttu-id="426be-174">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="426be-174">Assign users toohello application</span></span>

<span data-ttu-id="426be-175">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="426be-175">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="426be-176">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="426be-176">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="426be-177">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="426be-177">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="426be-178">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="426be-178">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="426be-179">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="426be-179">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="426be-180">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="426be-180">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="426be-181">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="426be-181">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="426be-182">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="426be-182">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="426be-183">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="426be-183">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="426be-184">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="426be-184">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="426be-185">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="426be-185">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="426be-186">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="426be-186">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="426be-187">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="426be-187">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="426be-188">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="426be-188">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="426be-189">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="426be-189">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="426be-190">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="426be-190">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="426be-191">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="426be-191">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="426be-192">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="426be-192">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="426be-193">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="426be-193">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="426be-194">Si estos pasos no Hola resolver el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="426be-194">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="426be-195">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="426be-195">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="426be-196">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="426be-196">Correlation error ID</span></span>

-   <span data-ttu-id="426be-197">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="426be-197">UPN (user email address)</span></span>

-   <span data-ttu-id="426be-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="426be-198">TenantID</span></span>

-   <span data-ttu-id="426be-199">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="426be-199">Browser type</span></span>

-   <span data-ttu-id="426be-200">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="426be-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="426be-201">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="426be-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="426be-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="426be-202">Next steps</span></span>
[<span data-ttu-id="426be-203">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="426be-203">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

