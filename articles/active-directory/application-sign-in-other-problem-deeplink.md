---
title: "iniciar sesión en la aplicación de tooan mediante un vínculo profundo de aaaProblems | Documentos de Microsoft"
description: "Cómo problemas tootroubleshoot obtiene acceso a una aplicación desde una dirección URL de vínculo profundo con Azure AD"
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a><span data-ttu-id="16335-103">Problemas para iniciar sesión en la aplicación tooan mediante un vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="16335-103">Problems signing in tooan application using a deeplink</span></span>

<span data-ttu-id="16335-104">Hola Panel de acceso es un portal basado en web que permite a los usuarios con un trabajo o cuenta educativa en aplicaciones de Azure Active Directory (Azure AD) tooview y de inicio en la nube que Hola Administrador de Azure AD le haya concedido acceso a.</span><span class="sxs-lookup"><span data-stu-id="16335-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="16335-105">Estas aplicaciones se configuran en nombre de usuario de hello en el portal de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="16335-106">aplicación Hello debe configurarse correctamente y asignado toohello usuario o un grupo de usuario de hello es miembro de la aplicación de hello toosee Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16335-106">hello application must be configured properly and assigned toohello user or a group hello user is a member of toosee hello application in hello Access Panel.</span></span>

<span data-ttu-id="16335-107">Acceso de usuario o vínculos profundos las direcciones URL son vínculos que los usuarios pueden usar tooaccess sus aplicaciones de SSO de contraseña directamente desde su dirección URL de exploradores barras.</span><span class="sxs-lookup"><span data-stu-id="16335-107">Deep links or User access URLs are links your users may use tooaccess their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="16335-108">Desplazándose toothis vínculo, los usuarios pueden automáticamente sesión en la aplicación hello sin tener primero toogo toohello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16335-108">By navigating toothis link, users be automatically signed into hello application without having toogo toohello Access Panel first.</span></span> <span data-ttu-id="16335-109">Se trata de hello mismo vínculo que los usuarios utilicen tooaccess estas aplicaciones desde el iniciador de la aplicación hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="16335-109">This is hello same link that users use tooaccess these applications from hello Office 365 application launcher.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="16335-110">General emite toocheck primero</span><span class="sxs-lookup"><span data-stu-id="16335-110">General issues toocheck first</span></span>

-   <span data-ttu-id="16335-111">Asegúrese de que el uso de un **explorador** que cumple los requisitos mínimos de Hola para hello Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16335-111">Make sure your using a **browser** that meets hello minimum requirements for hello Access Panel.</span></span>

-   <span data-ttu-id="16335-112">Asegúrese de explorador del usuario de hello agregada URL Hola de hello aplicación tooits **sitios de confianza**.</span><span class="sxs-lookup"><span data-stu-id="16335-112">Make sure hello user’s browser has added hello URL of hello application tooits **trusted sites**.</span></span>

-   <span data-ttu-id="16335-113">Asegúrese de que es de aplicación de hello toocheck **configurado** correctamente.</span><span class="sxs-lookup"><span data-stu-id="16335-113">Make sure toocheck hello application is **configured** correctly.</span></span>

-   <span data-ttu-id="16335-114">Asegúrese de que es la cuenta de usuario de hello **habilitado** para inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="16335-114">Make sure hello user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="16335-115">Asegúrese de que es la cuenta de usuario de hello **no está bloqueada.**</span><span class="sxs-lookup"><span data-stu-id="16335-115">Make sure hello user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="16335-116">Asegúrese de que usuario hello **contraseña no se ha caducado o se olvida.**</span><span class="sxs-lookup"><span data-stu-id="16335-116">Make sure hello user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="16335-117">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="16335-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="16335-118">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="16335-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="16335-119">Asegúrese de que un usuario **información de contacto de autenticación** es hacia arriba toodate tooallow la autenticación multifactor o acceso condicional directivas toobe aplicada.</span><span class="sxs-lookup"><span data-stu-id="16335-119">Make sure that a user’s **authentication contact info** is up toodate tooallow Multi-Factor Authentication or Conditional Access policies toobe enforced.</span></span>

-   <span data-ttu-id="16335-120">Asegúrese de tooalso seguro intente borrar las cookies del explorador y vuelva a probar toosign en.</span><span class="sxs-lookup"><span data-stu-id="16335-120">Make sure tooalso try clearing your browser’s cookies and trying toosign in again.</span></span>

## <a name="checking-hello-deeplink"></a><span data-ttu-id="16335-121">Comprobando vínculo profundo de Hola</span><span class="sxs-lookup"><span data-stu-id="16335-121">Checking hello deeplink</span></span>

<span data-ttu-id="16335-122">toocheck si dispone de vínculo profundo correcto de hello, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="16335-122">toocheck if you have hello correct deeplink, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-123">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="16335-123">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16335-124">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-124">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-125">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-125">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-126">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-126">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-127">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16335-127">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="16335-128">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="16335-128">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="16335-129">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="16335-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="16335-130">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

8.  <span data-ttu-id="16335-131">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="16335-132">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-132">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="16335-133">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16335-133">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="16335-134">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="16335-134">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

11. <span data-ttu-id="16335-135">Seleccionar aplicación de Hola Hola vínculo profundo de Hola de comprobación para la que desea.</span><span class="sxs-lookup"><span data-stu-id="16335-135">Select hello application you want hello check hello deeplink for.</span></span>

12. <span data-ttu-id="16335-136">Buscar etiqueta hello **dirección URL de acceso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="16335-136">Find hello label **User Access URL**.</span></span> <span data-ttu-id="16335-137">El vínculo profundo debe coincidir con esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="16335-137">You deeplink should match this URL.</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="16335-138">¿Cómo tooinstall Hola extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="16335-138">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="16335-139">Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="16335-139">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-140">Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="16335-140">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="16335-141">Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16335-141">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="16335-142">En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="16335-142">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="16335-143">Basado en el explorador es que el vínculo de descarga de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="16335-143">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="16335-144">**Agregar** tooyour Explorador de hello extensión.</span><span class="sxs-lookup"><span data-stu-id="16335-144">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="16335-145">Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="16335-145">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="16335-146">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="16335-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="16335-147">Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña</span><span class="sxs-lookup"><span data-stu-id="16335-147">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="16335-148">También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="16335-148">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="16335-149">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="16335-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="16335-150">Extensión del panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="16335-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="16335-151">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación de la Galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16335-151">How tooconfigure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="16335-152">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="16335-152">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="16335-153">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="16335-153">Add an application from hello Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="16335-154">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="16335-154">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a><span data-ttu-id="16335-155">Agregar una aplicación de la Galería de Azure AD Hola</span><span class="sxs-lookup"><span data-stu-id="16335-155">Add an application from hello Azure AD gallery</span></span>

<span data-ttu-id="16335-156">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="16335-156">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-157">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="16335-157">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="16335-158">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-158">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-159">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-159">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-160">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-160">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-161">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="16335-161">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="16335-162">Hola **escriba un nombre** cuadro de texto de hello **agregar a partir de la Galería de hello** sección, escriba un nombre de aplicación hello como Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-162">In hello **Enter a name** textbox from hello **Add from hello gallery** section, type hello name of hello application.</span></span>

7.  <span data-ttu-id="16335-163">Seleccionar aplicación hello tooconfigure que desee para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="16335-163">Select hello application you want tooconfigure for single sign-on.</span></span>

8.  <span data-ttu-id="16335-164">Antes de agregar la aplicación hello, puede cambiar su nombre de hello **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="16335-164">Before adding hello application, you can change its name from hello **Name** textbox.</span></span>

9.  <span data-ttu-id="16335-165">Haga clic en **agregar** button, aplicación de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="16335-165">Click **Add** button, tooadd hello application.</span></span>

<span data-ttu-id="16335-166">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-166">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="16335-167">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="16335-167">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="16335-168">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="16335-168">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-169">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="16335-169">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16335-170">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-170">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-171">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-171">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-172">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-172">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-173">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16335-173">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="16335-174">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="16335-174">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="16335-175">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="16335-175">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="16335-176">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="16335-176">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16335-177">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="16335-177">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="16335-178">[Asignar usuarios de aplicación de toohello](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="16335-178">[Assign users toohello application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="16335-179">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-179">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="16335-180">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="16335-180">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="16335-181">¿Cómo tooconfigure contraseña inicio de sesión único para una aplicación no Galería</span><span class="sxs-lookup"><span data-stu-id="16335-181">How tooconfigure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="16335-182">una aplicación desde la Galería de Azure AD de hello tooconfigure debe:</span><span class="sxs-lookup"><span data-stu-id="16335-182">tooconfigure an application from hello Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="16335-183">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="16335-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="16335-184">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="16335-184">Configure hello application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="16335-185">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="16335-185">Add a non-gallery application</span></span>

<span data-ttu-id="16335-186">tooadd una aplicación Hola Galería de Azure AD, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="16335-186">tooadd an application from hello Azure AD Gallery, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-187">Abra hello [Portal de Azure](https://portal.azure.com) e inicie sesión como un **administrador Global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="16335-187">Open hello [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="16335-188">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-188">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-189">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-189">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-190">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-190">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-191">Haga clic en hello **agregar** situado en la esquina superior derecha de hello en hello **aplicaciones empresariales** hoja.</span><span class="sxs-lookup"><span data-stu-id="16335-191">click hello **Add** button at hello top-right corner on hello **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="16335-192">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="16335-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="16335-193">Escriba el nombre de saludo de la aplicación Hola **nombre** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="16335-193">Enter hello name of your application in hello **Name** textbox.</span></span> <span data-ttu-id="16335-194">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="16335-194">Select **Add.**</span></span>

<span data-ttu-id="16335-195">Tras un breve período, es que la hoja de configuración de la aplicación pueda toosee Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-195">After a short period, you be able toosee hello application’s configuration blade.</span></span>

### <a name="configure-hello-application-for-password-single-sign-on"></a><span data-ttu-id="16335-196">Configurar la aplicación hello para el inicio de sesión único en la contraseña</span><span class="sxs-lookup"><span data-stu-id="16335-196">Configure hello application for password single sign-on</span></span>

<span data-ttu-id="16335-197">tooconfigure inicio de sesión único para una aplicación, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="16335-197">tooconfigure single sign-on for an application, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-198">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="16335-198">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="16335-199">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-199">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-200">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-200">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-201">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-201">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-202">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16335-202">click **All Applications** tooview a list of all your applications.</span></span>

    1.  <span data-ttu-id="16335-203">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="16335-203">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="16335-204">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="16335-204">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="16335-205">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="16335-205">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16335-206">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="16335-206">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="16335-207">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="16335-207">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="16335-208">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="16335-208">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="16335-209">Asegúrese de que está visible en la dirección URL de Hola Hola campos inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="16335-209">Ensure hello sign in fields are visible at hello URL.</span></span>

10. <span data-ttu-id="16335-210">Asignar a usuarios de aplicación de toohello.</span><span class="sxs-lookup"><span data-stu-id="16335-210">Assign users toohello application.</span></span>

11. <span data-ttu-id="16335-211">Además, también puede proporcionar credenciales en nombre de usuario de hello selección de filas de Hola de usuarios de Hola y haciendo clic en **las credenciales de actualización** y especificando Hola username y password en nombre de los usuarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-211">Additionally, you can also provide credentials on behalf of hello user by selecting hello rows of hello users and clicking on **Update Credentials** and entering hello username and password on behalf of hello users.</span></span> <span data-ttu-id="16335-212">En caso contrario, los usuarios ser solicitadas tooenter Hola credenciales por sí mismos tras el inicio.</span><span class="sxs-lookup"><span data-stu-id="16335-212">Otherwise, users be prompted tooenter hello credentials themselves upon launch.</span></span>

## <a name="how-tooassign-a-user-tooan-application-directly"></a><span data-ttu-id="16335-213">¿Cómo tooassign directamente una aplicación de tooan de usuario</span><span class="sxs-lookup"><span data-stu-id="16335-213">How tooassign a user tooan application directly</span></span>

<span data-ttu-id="16335-214">tooassign uno o más usuarios tooan application directamente, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="16335-214">tooassign one or more users tooan application directly, follow hello steps below:</span></span>

1.  <span data-ttu-id="16335-215">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global.**</span><span class="sxs-lookup"><span data-stu-id="16335-215">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="16335-216">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-216">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="16335-217">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="16335-217">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="16335-218">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16335-218">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="16335-219">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="16335-219">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="16335-220">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="16335-220">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="16335-221">Seleccionar aplicación hello desea tooassign una lista de hello toofrom de usuario.</span><span class="sxs-lookup"><span data-stu-id="16335-221">Select hello application you want tooassign a user toofrom hello list.</span></span>

7.  <span data-ttu-id="16335-222">Una vez que se carga la aplicación hello, haga clic en **usuarios y grupos** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="16335-222">Once hello application loads, click **Users and Groups** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="16335-223">Haga clic en hello **agregar** botón encima de hello **usuarios y grupos** Hola de lista tooopen **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="16335-223">Click hello **Add** button on top of hello **Users and Groups** list tooopen hello **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="16335-224">Haga clic en hello **usuarios y grupos** selector de hello **Agregar asignación** hoja.</span><span class="sxs-lookup"><span data-stu-id="16335-224">click hello **Users and groups** selector from hello **Add Assignment** blade.</span></span>

10. <span data-ttu-id="16335-225">Tipo de hello **nombre completo** o **dirección de correo electrónico** del usuario de hello está interesado en la asignación en hello **buscar por nombre o dirección de correo** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="16335-225">Type in hello **full name** or **email address** of hello user you are interested in assigning into hello **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="16335-226">Mantenga el mouse sobre hello **usuario** en hello lista tooreveal una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="16335-226">Hover over hello **user** in hello list tooreveal a **checkbox**.</span></span> <span data-ttu-id="16335-227">Haga clic en tooadd de foto o el logotipo de perfil de hello casilla toohello del siguiente usuario su usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="16335-227">Click hello checkbox next toohello user’s profile photo or logo tooadd your user toohello **Selected** list.</span></span>

12. <span data-ttu-id="16335-228">**Opcional:** si lo desea demasiado**agregar más de un usuario**, tipo de otro **nombre completo** o **dirección de correo electrónico** en hello **buscar por nombre o dirección de correo electrónico** cuadro de búsqueda y haga clic en hello casilla tooadd este usuario toohello **seleccionados** lista.</span><span class="sxs-lookup"><span data-stu-id="16335-228">**Optional:** If you would like too**add more than one user**, type in another **full name** or **email address** into hello **Search by name or email address** search box, and click hello checkbox tooadd this user toohello **Selected** list.</span></span>

13. <span data-ttu-id="16335-229">Cuando haya terminado de seleccionar usuarios, haga clic en hello **seleccione** botón tooadd les toohello lista de usuarios y grupos toobe asignado toohello aplicación.</span><span class="sxs-lookup"><span data-stu-id="16335-229">When you are finished selecting users, click hello **Select** button tooadd them toohello list of users and groups toobe assigned toohello application.</span></span>

14. <span data-ttu-id="16335-230">**Opcional:** haga clic en hello **Seleccionar rol** selector Hola **Agregar asignación** hoja tooselect un rol tooassign toohello usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="16335-230">**Optional:** click hello **Select Role** selector in hello **Add Assignment** blade tooselect a role tooassign toohello users you have selected.</span></span>

15. <span data-ttu-id="16335-231">Haga clic en hello **asignar** botón tooassign Hola aplicación toohello los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="16335-231">Click hello **Assign** button tooassign hello application toohello selected users.</span></span>

<span data-ttu-id="16335-232">Después de un breve período, los usuarios de Hola que seleccionó ser capaz de toolaunch estas aplicaciones en Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="16335-232">After a short period, hello users you have selected be able toolaunch these applications in hello Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="16335-233">Si estos pasos no Hola resuelva el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="16335-233">If these troubleshooting steps do not hello resolve hello issue.</span></span> 

<span data-ttu-id="16335-234">Abra una incidencia de soporte técnico con hello siguiente información si está disponible:</span><span class="sxs-lookup"><span data-stu-id="16335-234">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="16335-235">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="16335-235">Correlation error ID</span></span>

-   <span data-ttu-id="16335-236">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="16335-236">UPN (user email address)</span></span>

-   <span data-ttu-id="16335-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="16335-237">TenantID</span></span>

-   <span data-ttu-id="16335-238">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="16335-238">Browser type</span></span>

-   <span data-ttu-id="16335-239">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="16335-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="16335-240">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="16335-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="16335-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16335-241">Next steps</span></span>
[<span data-ttu-id="16335-242">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="16335-242">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
