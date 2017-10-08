---
title: "aaaProblem configuración del inicio de sesión único en contraseña para una aplicación no Galería | Documentos de Microsoft"
description: "Comprender la cara de personas de problemas comunes de hello al configurar un inicio de sesión único de contraseña para las aplicaciones no Galería personalizadas que no aparecen en hello Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="407cf-103">Problema en la configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="407cf-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="407cf-104">En este artículo le ayudará toounderstand Hola comunes problemas se enfrentan los usuarios al configurar **contraseña inicio de sesión único** con una aplicación no Galería.</span><span class="sxs-lookup"><span data-stu-id="407cf-104">This article help you toounderstand hello common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-toocapture-sign-in-fields-for-an-application"></a><span data-ttu-id="407cf-105">Cómo iniciar sesión toocapture campos para una aplicación</span><span class="sxs-lookup"><span data-stu-id="407cf-105">How toocapture sign-in fields for an application</span></span>

<span data-ttu-id="407cf-106">La captura de campos de inicio de sesión solo es posible en páginas de inicio de sesión compatibles con HTML y **no se admite para páginas de inicio de sesión no estándar**, como aquellas que usan Flash u otras tecnologías incompatibles con HTML.</span><span class="sxs-lookup"><span data-stu-id="407cf-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="407cf-107">Existen dos maneras de capturar campos de inicio de sesión para aplicaciones personalizadas:</span><span class="sxs-lookup"><span data-stu-id="407cf-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="407cf-108">Captura automática de campos de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="407cf-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="407cf-109">Captura manual de campos de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="407cf-109">Manual sign-in field capture</span></span>

<span data-ttu-id="407cf-110">**Captura de campo de inicio de sesión automático** funciona bien con la mayoría basadas en HTML en el inicio de sesión de las páginas, si usan **identificadores conocidos de DIV Hola nombre de usuario y una contraseña de entrada** campo.</span><span class="sxs-lookup"><span data-stu-id="407cf-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for hello username and password input** field.</span></span> <span data-ttu-id="407cf-111">Hola que esto funciona de forma Hola de barrido de HTML en la página de hello toofind identificadores DIV que cumplan ciertos criterios y, a continuación, guardando que los metadatos para esta aplicación para podemos reproducir contraseñas tooit más tarde.</span><span class="sxs-lookup"><span data-stu-id="407cf-111">hello way this works is by scraping hello HTML on hello page toofind DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords tooit later.</span></span>

<span data-ttu-id="407cf-112">**Captura de campo de inicio de sesión manual** puede usarse en caso de Hola que Hola aplicación **proveedor no etiqueta** Hola campos utilizados para el inicio de sesión de entrada.</span><span class="sxs-lookup"><span data-stu-id="407cf-112">**Manual sign-in field capture** can be used in hello case that hello application **vendor does not label** hello input fields used for sign in.</span></span> <span data-ttu-id="407cf-113">Captura de campo de inicio de sesión manual también puede usarse en caso de hello cuando hello **proveedor presenta varios campos** que no puede ser detectado automáticamente.</span><span class="sxs-lookup"><span data-stu-id="407cf-113">Manual sign-in field capture can also be used in hello case when hello **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="407cf-114">Azure AD puede almacenar datos para como muchos campos cuando estén en hello iniciar sesión en la página, siempre y cuando Díganos que esos campos se encuentran en página Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-114">Azure AD can store data for as many fields as are on hello sign in page, so long as you tell us where those fields are on hello page.</span></span>

<span data-ttu-id="407cf-115">En general, **si captura del campo de inicio de sesión automático no funciona, siempre se recomienda tratar de opción manual de Hola.**</span><span class="sxs-lookup"><span data-stu-id="407cf-115">In general, **if automatic sign-in field capture does not work, we always suggest trying hello manual option.**</span></span>

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="407cf-116">¿Cómo tooautomatically capturar campos de inicio de sesión para una aplicación</span><span class="sxs-lookup"><span data-stu-id="407cf-116">How tooautomatically capture sign-in fields for an application</span></span>

<span data-ttu-id="407cf-117">tooconfigure **basado en contraseña Single Sign-on** para una aplicación con **captura automática de inicio de sesión en campos**, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="407cf-117">tooconfigure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="407cf-118">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="407cf-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="407cf-119">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="407cf-120">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="407cf-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="407cf-121">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="407cf-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="407cf-122">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="407cf-122">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="407cf-123">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="407cf-123">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="407cf-124">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="407cf-124">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="407cf-125">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="407cf-125">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="407cf-126">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="407cf-126">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="407cf-127">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="407cf-127">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="407cf-128">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="407cf-128">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="407cf-129">**Asegúrese de inicio de sesión de hello en los campos está visible en la dirección URL de hello proporcionas**.</span><span class="sxs-lookup"><span data-stu-id="407cf-129">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="407cf-130">Haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="407cf-130">Click hello **Save** button.</span></span>

11. <span data-ttu-id="407cf-131">Una vez que lo hace, se podrá extraer automáticamente esa dirección URL para un nombre de usuario y una contraseña cuadro de entrada y le permite toosecurely de Azure AD toouse transmitir aplicación toothat de contraseñas con la extensión de explorador del panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span>

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="407cf-132">¿Cómo toomanually capturar campos de inicio de sesión para una aplicación</span><span class="sxs-lookup"><span data-stu-id="407cf-132">How toomanually capture sign-in fields for an application</span></span>

<span data-ttu-id="407cf-133">inicio de sesión de captura de toomanually en campos, en primer lugar debe tener extensión de explorador del Panel de acceso de hello instalada y **no se esté ejecutando en modo de inPrivate, incognito o privado.**</span><span class="sxs-lookup"><span data-stu-id="407cf-133">toomanually capture sign in fields, you must first have hello Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="407cf-134">extensión del navegador tooinstall hello, siga los pasos de Hola Hola [cómo tooinstall Hola extensión de explorador del Panel de acceso](#i-cannot-manually-detect-sign-in-fields-for-my-application) sección.</span><span class="sxs-lookup"><span data-stu-id="407cf-134">tooinstall hello browser extension, follow hello steps in hello [How tooinstall hello Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="407cf-135">tooconfigure **basado en contraseña Single Sign-on** para una aplicación con **captura manual campo**, siga estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="407cf-135">tooconfigure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow hello steps below:</span></span>

1.  <span data-ttu-id="407cf-136">Abra hello [ **Portal de Azure** ](https://portal.azure.com/) e inicie sesión como un **administrador Global** o **Co-administrador.**</span><span class="sxs-lookup"><span data-stu-id="407cf-136">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="407cf-137">Hola abierto **extensión de Azure Active Directory** haciendo clic en **más servicios** final Hola del menú de navegación izquierdo principal Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-137">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="407cf-138">Escriba en **"Azure Active Directory**" en el cuadro de búsqueda del filtro de Hola y Hola seleccione **Azure Active Directory** elemento.</span><span class="sxs-lookup"><span data-stu-id="407cf-138">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="407cf-139">Haga clic en **aplicaciones empresariales** desde el menú de navegación izquierdo de hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="407cf-139">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="407cf-140">Haga clic en **todas las aplicaciones** tooview una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="407cf-140">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="407cf-141">Si no ve la aplicación hello que le interese mostrar aquí, usar hello **filtro** control parte superior de Hola de hello **lista de todas las aplicaciones** conjunto hello y **mostrar** opción demasiado **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="407cf-141">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="407cf-142">Seleccionar aplicación hello desea tooconfigure inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="407cf-142">Select hello application you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="407cf-143">Una vez que se carga la aplicación hello, haga clic en hello **inicio de sesión único** del menú de navegación izquierdo de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="407cf-143">Once hello application loads, click hello **Single sign-on** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="407cf-144">Modo de hello seleccione **sesión basada en contraseña.**</span><span class="sxs-lookup"><span data-stu-id="407cf-144">Select hello mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="407cf-145">Escriba hello **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="407cf-145">Enter hello **Sign-on URL**.</span></span> <span data-ttu-id="407cf-146">Se trata de dirección URL de Hola donde los usuarios escribir su toosign en nombre de usuario y contraseña a.</span><span class="sxs-lookup"><span data-stu-id="407cf-146">This is hello URL where users enter their username and password toosign in to.</span></span> <span data-ttu-id="407cf-147">**Asegúrese de inicio de sesión de hello en los campos está visible en la dirección URL de hello proporcionas**.</span><span class="sxs-lookup"><span data-stu-id="407cf-147">**Ensure hello sign in fields are visible at hello URL you provide**.</span></span>

10. <span data-ttu-id="407cf-148">Haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="407cf-148">Click hello **Save** button.</span></span>

11. <span data-ttu-id="407cf-149">Una vez que lo hace, se podrá extraer automáticamente esa dirección URL para un nombre de usuario y una contraseña cuadro de entrada y le permite toosecurely de Azure AD toouse transmitir aplicación toothat de contraseñas con la extensión de explorador del panel de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you toouse Azure AD toosecurely transmit passwords toothat application using hello access panel browser extension.</span></span> <span data-ttu-id="407cf-150">En caso de Hola que se produce un error, puede **Hola inicio de sesión en el modo toouse campo de inicio de sesión manual captura modificados** por continuar toostep 12.</span><span class="sxs-lookup"><span data-stu-id="407cf-150">In hello case that this fails, you can **change hello sign-in mode toouse manual sign-in field capture** by continuing toostep 12.</span></span>

12. <span data-ttu-id="407cf-151">Haga clic en **Establecer configuración de inicio de sesión único con contraseña de &lt;nombre de la aplicación&gt;**.</span><span class="sxs-lookup"><span data-stu-id="407cf-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="407cf-152">Seleccione hello **detectar manualmente los campos de inicio de sesión** opción de configuración.</span><span class="sxs-lookup"><span data-stu-id="407cf-152">Select hello **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="407cf-153">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="407cf-153">Click **Ok**.</span></span>

15. <span data-ttu-id="407cf-154">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="407cf-154">Click **Save**.</span></span>

16. <span data-ttu-id="407cf-155">Siga hello en pantalla instrucciones toouse Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="407cf-155">Follow hello on screen instructions toouse hello Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="407cf-156">Error "No pudimos encontrar ningún campo de inicio de sesión en esa URL"</span><span class="sxs-lookup"><span data-stu-id="407cf-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="407cf-157">Este error aparece cuando no funciona la detección automática de campos de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="407cf-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="407cf-158">tooresolve este problema, detección de campo de inicio de sesión manual de try por hello siguiendo los pasos de hello [cómo toomanually capturar campos de inicio de sesión para una aplicación](#how-to-manually-capture-sign-in-fields-for-an-application) sección.</span><span class="sxs-lookup"><span data-stu-id="407cf-158">tooresolve this issue, try manual sign-in field detection by following hello steps in hello [How toomanually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a><span data-ttu-id="407cf-159">Aparece un error "no se puede toosave Single Sign-on configuración"</span><span class="sxs-lookup"><span data-stu-id="407cf-159">I see an “Unable toosave Single Sign-on configuration” error</span></span>

<span data-ttu-id="407cf-160">En algunos casos poco frecuentes, actualizando la configuración de inicio de sesión único de hello puede producir un error.</span><span class="sxs-lookup"><span data-stu-id="407cf-160">In certain rare cases, updating hello single sign-on configuration can fail.</span></span> <span data-ttu-id="407cf-161">tooresolve este intente guardar Hola único inicio de sesión en configuración de nuevo.</span><span class="sxs-lookup"><span data-stu-id="407cf-161">tooresolve this try saving hello single sign-on configuration again.</span></span>

<span data-ttu-id="407cf-162">Si el problema persiste toofail de forma coherente, abrir un caso de soporte técnico y proporcione información de hello recopilada en hello [cómo toosee detalles de Hola de una notificación portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [cómo ayudar tooget mediante el envío de notificaciones detalles tooa Ingeniero de soporte técnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secciones.</span><span class="sxs-lookup"><span data-stu-id="407cf-162">If this continues toofail consistently, open a support case and provide hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="407cf-163">No se detectan manualmente campos de inicio de sesión para mi aplicación</span><span class="sxs-lookup"><span data-stu-id="407cf-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="407cf-164">Algunos de los comportamientos de Hola que puede ver al detección manual no funciona son:</span><span class="sxs-lookup"><span data-stu-id="407cf-164">Some of hello behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="407cf-165">proceso de captura manual de Hello parecía toowork pero campos Hola capturados no eran correctas</span><span class="sxs-lookup"><span data-stu-id="407cf-165">hello manual capture process appeared toowork, but hello fields captured were not correct</span></span>

-   <span data-ttu-id="407cf-166">campos de la derecha de Hello no obtener resaltan al realizar el proceso de captura de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-166">hello right fields don’t get highlighted when performing hello capture process</span></span>

-   <span data-ttu-id="407cf-167">proceso de captura de Hello toma mi página de inicio de sesión de la aplicación toohello según lo previsto, pero no ocurre nada</span><span class="sxs-lookup"><span data-stu-id="407cf-167">hello capture process takes me toohello application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="407cf-168">Captura manual aparece toowork, pero no ocurre SSO cuando mis usuarios naveguen toohello aplicación Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="407cf-168">Manual capture appears toowork, but SSO doesn’t happen when my users navigate toohello application from hello Access Panel.</span></span>

<span data-ttu-id="407cf-169">Compruebe la siguiente Hola si se produce alguno de estos problemas:</span><span class="sxs-lookup"><span data-stu-id="407cf-169">check hello following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="407cf-170">Asegúrese de que tiene la versión más reciente de Hola de extensión de explorador del panel de acceso de hello **instalado** y **habilitado** siguiendo los pasos de Hola Hola [cómo tooinstall Hola explorador del Panel de acceso extensión](#how-to-install-the-access-panel-browser-extension) sección.</span><span class="sxs-lookup"><span data-stu-id="407cf-170">Ensure that you have hello latest version of hello access panel browser extension **installed** and **enabled** by following hello steps in hello [How tooinstall hello Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="407cf-171">Asegúrese de que no intenta realizar el proceso de captura de hello mientras el explorador en **incognito, inPrivate o Private modo**.</span><span class="sxs-lookup"><span data-stu-id="407cf-171">Ensure that you are not attempting hello capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="407cf-172">no se admite la extensión del panel de acceso de Hello en estos modos.</span><span class="sxs-lookup"><span data-stu-id="407cf-172">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="407cf-173">Asegúrese de que los usuarios no están tratando de toosign en toohello aplicación desde el panel de acceso de hello en **incognito, inPrivate o Private modo**.</span><span class="sxs-lookup"><span data-stu-id="407cf-173">Ensure that your users are not trying toosign in toohello application from hello access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="407cf-174">no se admite la extensión del panel de acceso de Hello en estos modos.</span><span class="sxs-lookup"><span data-stu-id="407cf-174">hello access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="407cf-175">Inténtelo de nuevo el proceso de captura manual de hello, asegurarse de marcadores de hello rojo sobre los campos correctos de Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-175">Try hello manual capture process again, ensuring hello red markers are over hello correct fields.</span></span>

-   <span data-ttu-id="407cf-176">Si el proceso de captura manual de hello parece toohang o inicio de sesión de hello en la página no nada (caso 3 anteriormente), proceso de captura manual de hello vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="407cf-176">If hello manual capture process seems toohang, or hello sign in page doesn’t do anything (case 3 above), try hello manual capture process again.</span></span> <span data-ttu-id="407cf-177">Pero, esta vez después de completar el proceso de hello, presione hello **F12** botón tooopen la consola para desarrolladores de su explorador.</span><span class="sxs-lookup"><span data-stu-id="407cf-177">But, this time after completing hello process, press hello **F12** button tooopen your browser’s developer console.</span></span> <span data-ttu-id="407cf-178">Una vez allí, abra hello **consola** y tipo **window.location= "&lt;escriba Hola inicio de sesión en la dirección url que ha especificado al configurar la aplicación hello&gt;"** y, a continuación, presione  **Escriba**.</span><span class="sxs-lookup"><span data-stu-id="407cf-178">Once there, open hello **console** and type **window.location=”&lt;enter hello sign in url you specified when configuring hello app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="407cf-179">Esta fuerza una página redirigir que finalizar el proceso de captura de Hola y almacenar Hola campos que se han capturado.</span><span class="sxs-lookup"><span data-stu-id="407cf-179">This force a page redirect which end hello capture process and store hello fields that have been captured.</span></span>

<span data-ttu-id="407cf-180">Si ninguno de estos métodos funciona, podemos ayudarle.</span><span class="sxs-lookup"><span data-stu-id="407cf-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="407cf-181">Abra un caso de soporte técnico con los detalles de Hola de lo que ha intentado, así como información de hello recopilada en hello [cómo toosee detalles de Hola de una notificación portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [cómo ayudar tooget enviando detalles de notificación de soporte técnico de tooa ingeniería](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secciones (si procede).</span><span class="sxs-lookup"><span data-stu-id="407cf-181">Open a support case with hello details of what you tried, as well as hello information gathered in hello [How toosee hello details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How tooget help by sending notification details tooa support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a><span data-ttu-id="407cf-182">¿Cómo tooinstall Hola extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="407cf-182">How tooinstall hello Access Panel Browser extension</span></span>

<span data-ttu-id="407cf-183">Hola tooinstall extensión de explorador del Panel de acceso, siga Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="407cf-183">tooinstall hello Access Panel Browser extension, follow hello steps below:</span></span>

1.  <span data-ttu-id="407cf-184">Abra hello [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores compatibles de Hola y de inicio de sesión como un **usuario** en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407cf-184">Open hello [Access Panel](https://myapps.microsoft.com) in one of hello supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="407cf-185">Haga clic en un **aplicación SSO de contraseña** Hola Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="407cf-185">click a **password-SSO application** in hello Access Panel.</span></span>

3.  <span data-ttu-id="407cf-186">En hello símbolo del sistema que se pregunta tooinstall Hola software, seleccione **instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="407cf-186">In hello prompt asking tooinstall hello software, select **Install Now**.</span></span>

4.  <span data-ttu-id="407cf-187">Basado en el explorador es que el vínculo de descarga de toohello dirigida.</span><span class="sxs-lookup"><span data-stu-id="407cf-187">Based on your browser you be directed toohello download link.</span></span> <span data-ttu-id="407cf-188">**Agregar** tooyour Explorador de hello extensión.</span><span class="sxs-lookup"><span data-stu-id="407cf-188">**Add** hello extension tooyour browser.</span></span>

5.  <span data-ttu-id="407cf-189">Si el explorador solicita, seleccione tooeither **habilitar** o **permitir** Hola extensión.</span><span class="sxs-lookup"><span data-stu-id="407cf-189">If your browser asks, select tooeither **Enable** or **Allow** hello extension.</span></span>

6.  <span data-ttu-id="407cf-190">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="407cf-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="407cf-191">Inicie sesión en el Panel de acceso de Hola y vea si puede **iniciar** las aplicaciones de SSO de contraseña.</span><span class="sxs-lookup"><span data-stu-id="407cf-191">Sign in into hello Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="407cf-192">También puede descargar extensión Hola para Chrome y Firefox de vínculos directos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="407cf-192">You may also download hello extension for Chrome and Firefox from hello direct links below:</span></span>

-   [<span data-ttu-id="407cf-193">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="407cf-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="407cf-194">Extensión del panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="407cf-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a><span data-ttu-id="407cf-195">¿Cómo toosee detalles de Hola de una notificación de portal</span><span class="sxs-lookup"><span data-stu-id="407cf-195">How toosee hello details of a portal notification</span></span>

<span data-ttu-id="407cf-196">Puede ver detalles de Hola de cualquier notificación portal siguiendo estos pasos hello:</span><span class="sxs-lookup"><span data-stu-id="407cf-196">You can see hello details of any portal notification by following hello steps below:</span></span>

1.  <span data-ttu-id="407cf-197">Haga clic en hello **notificaciones** icono (campana Hola) en la esquina superior derecha de Hola de hello Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="407cf-197">click hello **Notifications** icon (hello bell) in hello upper right of hello Azure Portal</span></span>

2.  <span data-ttu-id="407cf-198">Seleccione cualquier notificación de un **Error** estado (aquellos con un toothem siguiente (!) de color rojo).</span><span class="sxs-lookup"><span data-stu-id="407cf-198">Select any notification in an **Error** state (those with a red (!) next toothem).</span></span>

  ><span data-ttu-id="407cf-199">[NOTA] No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.</span><span class="sxs-lookup"><span data-stu-id="407cf-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="407cf-200">Este Hola abierto **detalles de la notificación** hoja.</span><span class="sxs-lookup"><span data-stu-id="407cf-200">This open hello **Notification Details** blade.</span></span>

4.  <span data-ttu-id="407cf-201">Utilice esta información usted mismo toounderstand más detalles sobre el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="407cf-201">Use this information yourself toounderstand more details about hello problem.</span></span>

5.  <span data-ttu-id="407cf-202">Si aún necesita ayuda, también puede compartir esta información con un soporte técnico o hello grupo tooget ayuda del producto con el problema.</span><span class="sxs-lookup"><span data-stu-id="407cf-202">If you still need help, you can also share this information with a support engineer or hello product group tooget help with your problem.</span></span>

6.  <span data-ttu-id="407cf-203">Haga clic en hello **copia** **icono** toohello derecha de hello **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto.</span><span class="sxs-lookup"><span data-stu-id="407cf-203">Click hello **copy** **icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer.</span></span>

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a><span data-ttu-id="407cf-204">Cómo ayudar tooget enviando el ingeniero de soporte técnico de notificación detalles tooa</span><span class="sxs-lookup"><span data-stu-id="407cf-204">How tooget help by sending notification details tooa support engineer</span></span>

<span data-ttu-id="407cf-205">Es muy importante que use para compartir **todos los detalles que se muestran a continuación de Hola** con un ingeniero de soporte técnico si necesita ayuda, por lo que pueden ayudarle rápidamente.</span><span class="sxs-lookup"><span data-stu-id="407cf-205">It is very important that you share **all hello details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="407cf-206">Puede hacer esto fácilmente mediante **tomar una captura de pantalla,** o haciendo clic en hello **icono de error de copia**, encuentra toohello derecha de hello **error al copiar** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="407cf-206">You can do this easily by **taking a screenshot,** or by clicking hello **Copy error icon**, found toohello right of hello **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="407cf-207">Explicación de los detalles de la notificación</span><span class="sxs-lookup"><span data-stu-id="407cf-207">Notification Details Explained</span></span>

<span data-ttu-id="407cf-208">Hola a continuación explica más cada uno de los elementos de notificación de hello significa y proporciona ejemplos de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="407cf-208">hello below explains more what each of hello notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="407cf-209">Elementos esenciales de notificación</span><span class="sxs-lookup"><span data-stu-id="407cf-209">Essential Notification Items</span></span>

-   <span data-ttu-id="407cf-210">**Título** : Hola título descriptivo de la notificación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-210">**Title** – hello descriptive title of hello notification</span></span>

    -   <span data-ttu-id="407cf-211">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="407cf-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="407cf-212">**Descripción** : Hola descripción de lo que se produjo como resultado de la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-212">**Description** – hello description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="407cf-213">Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**</span><span class="sxs-lookup"><span data-stu-id="407cf-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="407cf-214">**Identificador de notificación** : Id. único de Hola de notificación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-214">**Notification Id** – hello unique id of hello notification</span></span>

    -   <span data-ttu-id="407cf-215">Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="407cf-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="407cf-216">**Id. de solicitud de cliente** : Id. de solicitud específico de hello realizado por el explorador</span><span class="sxs-lookup"><span data-stu-id="407cf-216">**Client Request Id** – hello specific request id made by your browser</span></span>

    -   <span data-ttu-id="407cf-217">Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="407cf-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="407cf-218">**Hora UTC de marca** : Hola marca de tiempo durante el cual se produjo la notificación de hello, en UTC</span><span class="sxs-lookup"><span data-stu-id="407cf-218">**Time Stamp UTC** – hello timestamp during which hello notification occurred, in UTC</span></span>

    -   <span data-ttu-id="407cf-219">Por ejemplo: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="407cf-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="407cf-220">**Id. de transacción interna** : Hola Id. interno que podemos usar error de hello toolook en nuestros sistemas</span><span class="sxs-lookup"><span data-stu-id="407cf-220">**Internal Transaction Id** – hello internal ID we can use toolook hello error up in our systems</span></span>

    -   <span data-ttu-id="407cf-221">Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="407cf-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="407cf-222">**UPN** : usuario de Hola que realizó la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-222">**UPN** – hello user who performed hello operation</span></span>

    -   <span data-ttu-id="407cf-223">Por ejemplo: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="407cf-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="407cf-224">**Identificador de inquilino** : Hola Id. único del inquilino Hola Hola usuario que realizó la operación de hello era miembro de</span><span class="sxs-lookup"><span data-stu-id="407cf-224">**Tenant Id** – hello unique ID of hello tenant that hello user who performed hello operation was a member of</span></span>

    -   <span data-ttu-id="407cf-225">Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="407cf-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="407cf-226">**Id. de objeto de usuario** : Hola identificador único del usuario de Hola que realizó la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-226">**User object Id** – hello unique ID of hello user who performed hello operation</span></span>

    -   <span data-ttu-id="407cf-227">Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="407cf-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="407cf-228">Elementos detallados de notificación</span><span class="sxs-lookup"><span data-stu-id="407cf-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="407cf-229">**Nombre para mostrar** : **(puede estar vacía)** un nombre para mostrar más detallado para el error de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-229">**Display Name** – **(can be empty)** a more detailed display name for hello error</span></span>

    -   <span data-ttu-id="407cf-230">Por ejemplo*: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="407cf-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="407cf-231">**Estado** : Hola estado específico de notificación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-231">**Status** – hello specific status of hello notification</span></span>

    -   <span data-ttu-id="407cf-232">Por ejemplo*: **Error**</span><span class="sxs-lookup"><span data-stu-id="407cf-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="407cf-233">**Id. de objeto** : **(puede estar vacía)** Hola Id. de objeto con qué Hola se realizó la operación</span><span class="sxs-lookup"><span data-stu-id="407cf-233">**Object Id** – **(can be empty)** hello object ID against which hello operation was performed</span></span>

    -   <span data-ttu-id="407cf-234">Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="407cf-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="407cf-235">**Detalles** : Hola una descripción detallada de lo que se produjo como resultado de la operación de Hola</span><span class="sxs-lookup"><span data-stu-id="407cf-235">**Details** – hello detailed description of what occurred as a result of hello operation</span></span>

    -   <span data-ttu-id="407cf-236">Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**</span><span class="sxs-lookup"><span data-stu-id="407cf-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="407cf-237">**Error al copiar** : haga clic en hello **icono de copiar** toohello derecha de Hola **error al copiar** toocopy de cuadro de texto todos los Hola tooshare de detalles de notificación con un ingeniero de grupo de soporte técnico o el producto</span><span class="sxs-lookup"><span data-stu-id="407cf-237">**Copy error** – Click hello **copy icon** toohello right of hello **Copy error** textbox toocopy all hello notification details tooshare with a support or product group engineer</span></span>

    -   <span data-ttu-id="407cf-238">Por ejemplo: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="407cf-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="407cf-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="407cf-239">Next steps</span></span>
[<span data-ttu-id="407cf-240">Proporcionan aplicaciones de tooyour de inicio de sesión único con el Proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="407cf-240">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

