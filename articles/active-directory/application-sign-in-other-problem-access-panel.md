---
title: "aaaProblems iniciar sesión en la aplicación de tooan desde el panel de acceso de Hola | Documentos de Microsoft"
description: "Cómo los problemas de tootroubleshoot acceso a una aplicación de Hola Panel de acceso de Microsoft Azure AD en myapps.microsoft.com"
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
ms.reviewer: japere
ms.openlocfilehash: 346c4da06416bb9b330bdd5b1201253af19ba58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-from-hello-access-panel"></a><span data-ttu-id="e25b6-103">Problemas para iniciar sesión en la aplicación tooan desde el panel de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-103">Problems signing in tooan application from hello access panel</span></span>

<span data-ttu-id="e25b6-104">Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="e25b6-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="e25b6-105">Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="e25b6-106">aplicación Hello debe configurarse correctamente y asignado toohello usuario o un grupo de usuario de hello es miembro de la aplicación de hello toosee Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e25b6-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="e25b6-107">tipo Hello de aplicaciones posible que un usuario esté viendo se dividen en hello siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="e25b6-107">hello type of apps a user may be seeing fall in hello following categories:</span></span>

-   <span data-ttu-id="e25b6-108">Aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="e25b6-108">Office 365 Applications</span></span>

-   <span data-ttu-id="e25b6-109">Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación</span><span class="sxs-lookup"><span data-stu-id="e25b6-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="e25b6-110">Aplicaciones de SSO basado en contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="e25b6-111">Aplicaciones con soluciones SSO existentes</span><span class="sxs-lookup"><span data-stu-id="e25b6-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="e25b6-112">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="e25b6-112">General issues toocheck first</span></span>

-   <span data-ttu-id="e25b6-113">Asegúrese de que el uso de un **explorador** que cumple los requisitos mínimos de Hola para hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e25b6-113">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="e25b6-114">Asegúrese de explorador del usuario de hello agregada URL Hola de hello aplicación tooits **sitios de confianza**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-114">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="e25b6-115">Asegúrese de que es de aplicación de hello toocheck **configurado** correctamente.</span><span class="sxs-lookup"><span data-stu-id="e25b6-115">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="e25b6-116">Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="e25b6-116">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="e25b6-117">Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-117">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="e25b6-118">Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-118">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="e25b6-119">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="e25b6-120">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="e25b6-121">Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="e25b6-121">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="e25b6-122">Asegúrese de tooalso seguro intente borrar las cookies del explorador y vuelva a probar toosign en.</span><span class="sxs-lookup"><span data-stu-id="e25b6-122">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="meeting-browser-requirements-for-hello-access-panel"></a><span data-ttu-id="e25b6-123">Se cumplen los requisitos de explorador para hello Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="e25b6-123">Meeting browser requirements for hello Access Panel</span></span>

<span data-ttu-id="e25b6-124">Hola Panel de acceso requiere un explorador que admita JavaScript y se han habilitado de CSS.</span><span class="sxs-lookup"><span data-stu-id="e25b6-124">hello Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="e25b6-125">toouse basada en contraseña inicio de sesión único (SSO) en el Panel de acceso, extensión del Panel de acceso de Hola Hola debe instalarse en el explorador del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-125">toouse password-based single sign-on (SSO) in hello Access Panel, hello Access Panel extension must be installed in hello user’s browser.</span></span> <span data-ttu-id="e25b6-126">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="e25b6-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="e25b6-127">Para el SSO basado en contraseña, pueden ser Hola exploradores de los usuarios:</span><span class="sxs-lookup"><span data-stu-id="e25b6-127">For password-based SSO, hello end user’s browsers can be:</span></span>

-   <span data-ttu-id="e25b6-128">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="e25b6-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="e25b6-129">Edge en Windows 10 Anniversary Edition o posterior</span><span class="sxs-lookup"><span data-stu-id="e25b6-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="e25b6-130">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="e25b6-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="e25b6-131">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="e25b6-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="e25b6-132">¿Cómo tooinstall Hola extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="e25b6-132">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="e25b6-133">Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e25b6-133">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-134">Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e25b6-134">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="e25b6-135">Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e25b6-135">Click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="e25b6-136">En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-136">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="e25b6-137">Basado en el explorador es que el vínculo de descarga de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="e25b6-137">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="e25b6-138">**Agregar** tooyour Explorador de hello extensión.</span><span class="sxs-lookup"><span data-stu-id="e25b6-138">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="e25b6-139">Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="e25b6-139">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="e25b6-140">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="e25b6-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="e25b6-141">Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-141">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="e25b6-142">También puede descargar extensión Hola para Chrome y borde de vínculos directos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="e25b6-142">You may also download hello extension for Chrome and Edge from hello direct links below:</span></span>

-   [<span data-ttu-id="e25b6-143">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="e25b6-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="e25b6-144">Extensión del Panel de acceso para Edge</span><span class="sxs-lookup"><span data-stu-id="e25b6-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-tooconfigure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="e25b6-145">¿Cómo tooconfigure federado inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e25b6-145">How tooconfigure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="e25b6-146">Todas las aplicaciones en Galería de Azure AD Hola habilitada con capacidad de Enterprise Single Sign-On tienen un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="e25b6-146">All application in hello Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="e25b6-147">Puede tener acceso a hello [lista de tutoriales sobre cómo toointegrate aplicaciones de SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) para obtener instrucciones paso a paso detallados.</span><span class="sxs-lookup"><span data-stu-id="e25b6-147">You can access hello [List of tutorials on how toointegrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="e25b6-148">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="e25b6-148">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e25b6-149">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-149">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="e25b6-150">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="e25b6-150">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="e25b6-151">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="e25b6-151">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="e25b6-152">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e25b6-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="e25b6-153">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="e25b6-153">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="e25b6-154">Asignar a usuarios de aplicación toohello</span><span class="sxs-lookup"><span data-stu-id="e25b6-154">Assign users toohello application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e25b6-155">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e25b6-156">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-157">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="e25b6-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e25b6-158">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-159">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-160">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-161">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="e25b6-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e25b6-162">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="e25b6-163">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="e25b6-164">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e25b6-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="e25b6-165">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e25b6-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="e25b6-166">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e25b6-167">Configurar inicio de sesión único para una aplicación desde la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-167">Configure single sign-on for an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e25b6-168">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-170">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-171">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-172">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-173">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e25b6-174">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-175">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-176">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-177">Seleccione **sesión basado en SAML** de hello **modo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e25b6-177">Select **SAML-based Sign-on** from hello **Mode** dropdown.</span></span>

9.  <span data-ttu-id="e25b6-178">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-178">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="e25b6-179">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-179">You should get these values from hello application vendor.</span></span>

   1. <span data-ttu-id="e25b6-180">aplicación de hello tooconfigure como SSO iniciado por el SP, Hola inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-180">tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span> <span data-ttu-id="e25b6-181">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="e25b6-181">For some applications, hello Identifier is also a required value.</span></span>

   2. <span data-ttu-id="e25b6-182">aplicación de hello tooconfigure como SSO iniciado por IdP, Hola dirección URL de respuesta es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-182">tooconfigure hello application as IdP-initiated SSO, hello Reply URL it’s a required value.</span></span> <span data-ttu-id="e25b6-183">En algunas aplicaciones, Hola identificador también es un valor obligatorio.</span><span class="sxs-lookup"><span data-stu-id="e25b6-183">For some applications, hello Identifier is also a required value.</span></span>

10. <span data-ttu-id="e25b6-184">**Opcional:** haga clic en **mostrar avanzadas de configuración de direcciones URL** si desea que los valores no sean necesarios de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="e25b6-184">**Optional:** click **Show advanced URL settings** if you want toosee hello non-required values.</span></span>

11. <span data-ttu-id="e25b6-185">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e25b6-185">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="e25b6-186">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="e25b6-186">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e25b6-187">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="e25b6-187">tooadd an attribute:</span></span>

   1. <span data-ttu-id="e25b6-188">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-188">click **Add attribute**.</span></span> <span data-ttu-id="e25b6-189">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-189">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e25b6-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-190">Click **Save.**</span></span> <span data-ttu-id="e25b6-191">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-191">You see hello new attribute in hello table.</span></span>

13. <span data-ttu-id="e25b6-192">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-192">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="e25b6-193">Además, tendrá las direcciones URL de metadatos de Hola y requiere un certificado toosetup SSO con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-193">Also, you has hello metadata URLs and certificate required toosetup SSO with hello application.</span></span>

14. <span data-ttu-id="e25b6-194">Haga clic en **guardar** configuración de toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-194">Click **Save** toosave hello configuration.</span></span>

15. <span data-ttu-id="e25b6-195">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-195">Assign users toohello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="e25b6-196">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="e25b6-196">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="e25b6-197">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-197">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-198">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-199">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-200">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-201">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-202">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-202">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e25b6-203">Si no ve la aplicación hello desea tooshow aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-203">If you do not see hello application you want tooshow up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-204">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-204">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-205">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-206">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e25b6-206">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="e25b6-207">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-207">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="e25b6-208">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="e25b6-208">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="e25b6-209">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="e25b6-209">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="e25b6-210">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="e25b6-210">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e25b6-211">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="e25b6-211">tooadd an attribute:</span></span>

   1. <span data-ttu-id="e25b6-212">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-212">click **Add attribute**.</span></span> <span data-ttu-id="e25b6-213">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-213">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e25b6-214">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-214">Click **Save.**</span></span> <span data-ttu-id="e25b6-215">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-215">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="e25b6-216">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="e25b6-216">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="e25b6-217">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e25b6-217">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-218">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-218">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-219">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-219">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-220">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-220">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-221">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-221">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-222">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-222">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e25b6-223">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-223">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-224">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-224">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-225">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-225">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-226">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="e25b6-226">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="e25b6-227">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="e25b6-227">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="e25b6-228">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="e25b6-228">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="e25b6-229">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="e25b6-229">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e25b6-230">¿Cómo tooconfigure federado inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="e25b6-230">How tooconfigure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e25b6-231">una aplicación no Galería tooconfigure, necesita toohave Azure AD premium y aplicación hello es compatible con SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="e25b6-231">tooconfigure a non-gallery application, you need toohave Azure AD premium and hello application supports SAML 2.0.</span></span> <span data-ttu-id="e25b6-232">Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="e25b6-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="e25b6-233">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="e25b6-233">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="e25b6-234">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="e25b6-234">Select User Identifier and add user attributes toobe sent toohello application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="e25b6-235">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e25b6-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="e25b6-236">Configurar los valores de metadatos de Azure AD de la aplicación hello (inicio de sesión en la dirección URL, emisor, dirección URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="e25b6-236">Configure Azure AD metadata values in hello application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-hello-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="e25b6-237">Configurar valores de metadatos de la aplicación hello en Azure AD (inicio de sesión en la dirección URL de respuesta de dirección URL, identificador)</span><span class="sxs-lookup"><span data-stu-id="e25b6-237">Configure hello application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="e25b6-238">tooconfigure inicio de sesión único para una aplicación que no está en la Galería de Azure AD de hello, siga Hola pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e25b6-238">tooconfigure single sign-on for an application that is not in hello Azure AD gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-239">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-239">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-240">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-240">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-241">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-241">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-242">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-242">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-243">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="e25b6-243">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e25b6-244">Haga clic en **aplicación gallery no** en hello **agregar su propia aplicación** sección</span><span class="sxs-lookup"><span data-stu-id="e25b6-244">click **Non-gallery application** in hello **Add your own app** section</span></span>

7.  <span data-ttu-id="e25b6-245">Escriba el nombre de Hola de aplicación Hola Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e25b6-245">Enter hello name of hello application in hello **Name** textbox.</span></span>

8.  <span data-ttu-id="e25b6-246">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e25b6-246">Click **Add** button, tooadd hello application.</span></span>

9.  <span data-ttu-id="e25b6-247">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-247">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="e25b6-248">Seleccione **sesión basado en SAML** en hello **modo** desplegable</span><span class="sxs-lookup"><span data-stu-id="e25b6-248">Select **SAML-based Sign-on** in hello **Mode** dropdown</span></span>

11. <span data-ttu-id="e25b6-249">Especifique los valores de hello necesario en **dominio y las direcciones URL.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-249">Enter hello required values in **Domain and URLs.**</span></span> <span data-ttu-id="e25b6-250">Deberá obtener estos valores del proveedor de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-250">You should get these values from hello application vendor.</span></span>

  1. <span data-ttu-id="e25b6-251">aplicación de hello tooconfigure como SSO iniciado por IdP, escriba Hola dirección URL de respuesta y Hola identificador.</span><span class="sxs-lookup"><span data-stu-id="e25b6-251">tooconfigure hello application as IdP-initiated SSO, enter hello Reply URL and hello Identifier.</span></span>

  2. <span data-ttu-id="e25b6-252">**Opcional:** Hola de aplicación de hello tooconfigure como SSO iniciado por el SP, inicio de sesión en la dirección URL es un valor necesario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-252">**Optional:** tooconfigure hello application as SP-initiated SSO, hello Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="e25b6-253">Hola **atributos de usuario**, seleccione Hola identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e25b6-253">In hello **User attributes**, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="e25b6-254">**Opcional:** haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="e25b6-254">**Optional:** click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e25b6-255">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="e25b6-255">tooadd an attribute:</span></span>

   1. <span data-ttu-id="e25b6-256">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-256">click **Add attribute**.</span></span> <span data-ttu-id="e25b6-257">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-257">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   2. <span data-ttu-id="e25b6-258">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-258">Click **Save.**</span></span> <span data-ttu-id="e25b6-259">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-259">You see hello new attribute in hello table.</span></span>

14. <span data-ttu-id="e25b6-260">Haga clic en **configurar &lt;nombre de la aplicación&gt;**  tooaccess documentación sobre cómo tooconfigure inicio de sesión único en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-260">click **Configure &lt;application name&gt;** tooaccess documentation on how tooconfigure single sign-on in hello application.</span></span> <span data-ttu-id="e25b6-261">Además, tiene las direcciones URL de Azure AD y certificados necesarios para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-261">Also, you has Azure AD URLs and certificate required for hello application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-toobe-sent-toohello-application"></a><span data-ttu-id="e25b6-262">Seleccione el identificador de usuario y agregar usuario atributos toobe enviado toohello aplicación</span><span class="sxs-lookup"><span data-stu-id="e25b6-262">Select User Identifier and add user attributes toobe sent toohello application</span></span>

<span data-ttu-id="e25b6-263">tooselect Hola identificador de usuario o agregar atributos de usuario, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-263">tooselect hello User Identifier or add user attributes, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-264">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-264">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-265">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-265">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-266">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-266">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-267">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-267">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-268">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-268">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e25b6-269">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-269">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-270">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-270">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-271">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-271">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-272">En hello **atributos de usuario** Hola de sección, seleccione un identificador único para los usuarios en hello **identificador de usuario** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e25b6-272">Under hello **User attributes** section, select hello unique identifier for your users in hello **User Identifier** dropdown.</span></span> <span data-ttu-id="e25b6-273">Hello opción seleccionada debe toomatch Hola esperado valor en hello aplicación tooauthenticate Hola del usuario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-273">hello selected option needs toomatch hello expected value in hello application tooauthenticate hello user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e25b6-274">Azure formato AD seleccione Hola Hola NameID atributo (identificador de usuario) en función de valor de hello seleccionado u Hola formato solicitado por la aplicación hello en hello AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="e25b6-274">Azure AD select hello format for hello NameID attribute (User Identifier) based on hello value selected or hello format requested by hello application in hello SAML AuthRequest.</span></span> <span data-ttu-id="e25b6-275">Para obtener más información, visite el artículo de hello [protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) en hello sección NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="e25b6-275">For more information visit hello article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under hello section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="e25b6-276">atributos de usuario de tooadd, haga clic en **ver y editar todos los demás atributos de usuario** tooedit Hola atributos toobe enviado toohello aplicación en el token SAML de hello al usuario iniciar sesión en.</span><span class="sxs-lookup"><span data-stu-id="e25b6-276">tooadd user attributes, click **View and edit all other user attributes** tooedit hello attributes toobe sent toohello application in hello SAML token when user sign in.</span></span>

   <span data-ttu-id="e25b6-277">tooadd un atributo:</span><span class="sxs-lookup"><span data-stu-id="e25b6-277">tooadd an attribute:</span></span>

   <span data-ttu-id="e25b6-278">1. Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-278">1.click **Add attribute**.</span></span> <span data-ttu-id="e25b6-279">Escriba hello **nombre** y Hola Hola seleccione **valor** de lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-279">Enter hello **Name** and hello select hello **Value** from hello dropdown.</span></span>

   <span data-ttu-id="e25b6-280">2. Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-280">2 Click **Save.**</span></span> <span data-ttu-id="e25b6-281">Verá el nuevo atributo de hello en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-281">You see hello new attribute in hello table.</span></span>

### <a name="download-hello-azure-ad-metadata-or-certificate"></a><span data-ttu-id="e25b6-282">Descargar los metadatos de Azure AD de Hola o certificado</span><span class="sxs-lookup"><span data-stu-id="e25b6-282">Download hello Azure AD metadata or certificate</span></span>

<span data-ttu-id="e25b6-283">metadatos de la aplicación hello toodownload o certificado de Azure AD, siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="e25b6-283">toodownload hello application metadata or certificate from Azure AD, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-284">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-284">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-285">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-285">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-286">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-286">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-287">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-287">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-288">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-288">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="e25b6-289">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-289">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-290">Seleccionar aplicación hello ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-290">Select hello application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-291">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-291">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-292">Vaya demasiado**el certificado de firma de SAML** sección, a continuación, haga clic en **descargar** valor de la columna.</span><span class="sxs-lookup"><span data-stu-id="e25b6-292">Go too**SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="e25b6-293">Dependiendo de qué aplicación hello es necesario configurar el inicio de sesión único, vea cualquier toodownload de opción Hola Hola Metadata XML u Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="e25b6-293">Depending on what hello application requires configuring single sign-on, you see either hello option toodownload hello Metadata XML or hello Certificate.</span></span>

    <span data-ttu-id="e25b6-294">Azure AD no proporciona la dirección URL tooget Hola metadatos.</span><span class="sxs-lookup"><span data-stu-id="e25b6-294">Azure AD doesn’t provide a URL tooget hello metadata.</span></span> <span data-ttu-id="e25b6-295">solo se pueden recuperar metadatos de Hola como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="e25b6-295">hello metadata can only be retrieved as a XML file.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="e25b6-296">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e25b6-296">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="e25b6-297">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="e25b6-297">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e25b6-298">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-298">Add an application from hello Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="e25b6-299">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-299">Configure hello application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="e25b6-300">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-300">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="e25b6-301">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-301">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-302">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="e25b6-302">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e25b6-303">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-303">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-304">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-304">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-305">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-305">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-306">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="e25b6-306">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e25b6-307">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre Hola de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="e25b6-307">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application</span></span>

7.  <span data-ttu-id="e25b6-308">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e25b6-308">Select hello application you want tooconfigure for single sign-on</span></span>

8.  <span data-ttu-id="e25b6-309">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e25b6-309">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="e25b6-310">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e25b6-310">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="e25b6-311">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-311">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="e25b6-312">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-312">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="e25b6-313">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-313">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-314">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-314">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-315">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-315">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-316">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-316">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-317">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-317">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-318">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-318">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="e25b6-319">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-319">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-320">Seleccione la aplicación hello desea tooconfigure inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="e25b6-320">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="e25b6-321">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-321">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-322">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-322">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e25b6-323">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-323">Assign users toohello application.</span></span>

10. <span data-ttu-id="e25b6-324">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-324">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="e25b6-325">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="e25b6-325">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e25b6-326">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="e25b6-326">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e25b6-327">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="e25b6-327">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e25b6-328">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="e25b6-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="e25b6-329">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-329">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="e25b6-330">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="e25b6-330">Add a non-gallery application</span></span>

<span data-ttu-id="e25b6-331">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-331">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-332">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**</span><span class="sxs-lookup"><span data-stu-id="e25b6-332">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e25b6-333">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-333">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-334">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-334">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-335">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-335">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-336">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja</span><span class="sxs-lookup"><span data-stu-id="e25b6-336">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e25b6-337">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="e25b6-338">Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="e25b6-338">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="e25b6-339">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-339">Select **Add.**</span></span>

<span data-ttu-id="e25b6-340">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-340">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="e25b6-341">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="e25b6-341">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="e25b6-342">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-342">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-343">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-343">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e25b6-344">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-344">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-345">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-345">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-346">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-346">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-347">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-347">click **All Applications** tooview a list of all your applications.</span></span>

 * <span data-ttu-id="e25b6-348">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-348">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-349">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e25b6-349">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="e25b6-350">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-350">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-351">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-351">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e25b6-352">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-352">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="e25b6-353">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="e25b6-353">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="e25b6-354">Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="e25b6-354">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="e25b6-355">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-355">Assign users toohello application.</span></span>

11. <span data-ttu-id="e25b6-356">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-356">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="e25b6-357">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="e25b6-357">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="e25b6-358">¿Cómo tooassign directamente una aplicación de tooan de usuario</span><span class="sxs-lookup"><span data-stu-id="e25b6-358">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="e25b6-359">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="e25b6-359">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="e25b6-360">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-360">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e25b6-361">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="e25b6-361">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e25b6-362">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="e25b6-362">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e25b6-363">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e25b6-363">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e25b6-364">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e25b6-364">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="e25b6-365">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e25b6-365">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="e25b6-366">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="e25b6-366">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="e25b6-367">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e25b6-367">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e25b6-368">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="e25b6-368">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e25b6-369">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="e25b6-369">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e25b6-370">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="e25b6-370">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e25b6-371">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="e25b6-371">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="e25b6-372">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="e25b6-372">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="e25b6-373">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="e25b6-373">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="e25b6-374">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="e25b6-374">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="e25b6-375">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="e25b6-375">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="e25b6-376">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e25b6-376">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="e25b6-377">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e25b6-377">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="e25b6-378">Si estos pasos no Hola resolver el problema de Hola</span><span class="sxs-lookup"><span data-stu-id="e25b6-378">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="e25b6-379">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="e25b6-379">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="e25b6-380">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="e25b6-380">Correlation error ID</span></span>

-   <span data-ttu-id="e25b6-381">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="e25b6-381">UPN (user email address)</span></span>

-   <span data-ttu-id="e25b6-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="e25b6-382">TenantID</span></span>

-   <span data-ttu-id="e25b6-383">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="e25b6-383">Browser type</span></span>

-   <span data-ttu-id="e25b6-384">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="e25b6-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="e25b6-385">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="e25b6-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="e25b6-386">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e25b6-386">Next steps</span></span>
[<span data-ttu-id="e25b6-387">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="e25b6-387">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

