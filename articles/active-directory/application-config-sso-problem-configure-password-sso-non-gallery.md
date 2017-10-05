---
title: "Problema en la configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería | Microsoft Docs"
description: "Comprender los problemas más comunes a los que se enfrentan los usuarios al configurar un inicio de sesión único con contraseña para las aplicaciones ajenas a la galería que no figuran en la Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: 9c76b6f3495e2dd759a156fcef97b57aece8d632
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="ff4de-103">Problema en la configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="ff4de-103">Problem configuring password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="ff4de-104">Este artículo le ayuda a conocer los problemas habituales a los que se enfrentan los usuarios al configurar un **inicio de sesión único con contraseña** con una aplicación ajena a la galería.</span><span class="sxs-lookup"><span data-stu-id="ff4de-104">This article help you to understand the common problems people face when configuring **Password single sign-on** with a non-gallery application.</span></span>

## <a name="how-to-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ff4de-105">Captura de campos de inicio de sesión para una aplicación</span><span class="sxs-lookup"><span data-stu-id="ff4de-105">How to capture sign-in fields for an application</span></span>

<span data-ttu-id="ff4de-106">La captura de campos de inicio de sesión solo es posible en páginas de inicio de sesión compatibles con HTML y **no se admite para páginas de inicio de sesión no estándar**, como aquellas que usan Flash u otras tecnologías incompatibles con HTML.</span><span class="sxs-lookup"><span data-stu-id="ff4de-106">Sign-in field capture is only supported for HTML-enabled sign-in pages and is **not supported for non-standard sign-in pages**, like those that use Flash, or other non-HTML-enabled technologies.</span></span>

<span data-ttu-id="ff4de-107">Existen dos maneras de capturar campos de inicio de sesión para aplicaciones personalizadas:</span><span class="sxs-lookup"><span data-stu-id="ff4de-107">There are two ways you can capture sign-in fields for your custom applications:</span></span>

-   <span data-ttu-id="ff4de-108">Captura automática de campos de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ff4de-108">Automatic sign-in field capture</span></span>

-   <span data-ttu-id="ff4de-109">Captura manual de campos de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="ff4de-109">Manual sign-in field capture</span></span>

<span data-ttu-id="ff4de-110">La **captura automática de campos de inicio de sesión** funciona bien con la mayoría de las páginas de inicio de sesión compatibles con HTML si usan **identificadores DIV conocidos para el campo de entrada de nombre de usuario y contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-110">**Automatic sign-in field capture** works well with most HTML-enabled sign-in pages, if they use **well-known DIV IDs for the username and password input** field.</span></span> <span data-ttu-id="ff4de-111">Este procedimiento realiza un barrido del HTML en la página para encontrar identificadores DIV que cumplen determinados criterios y, a continuación, guarda esos metadatos para esta aplicación, de forma que las contraseñas puedan reproducirse en ella posteriormente.</span><span class="sxs-lookup"><span data-stu-id="ff4de-111">The way this works is by scraping the HTML on the page to find DIV IDs that match certain criteria and by then saving that metadata for this application so we can replay passwords to it later.</span></span>

<span data-ttu-id="ff4de-112">La **captura manual de campos de inicio de sesión** puede utilizarse en el caso de que el **proveedor de la aplicación no etiquete** los campos de entrada que se utilizan para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ff4de-112">**Manual sign-in field capture** can be used in the case that the application **vendor does not label** the input fields used for sign in.</span></span> <span data-ttu-id="ff4de-113">La captura manual de campos de inicio de sesión también puede utilizarse en el caso de que el **proveedor presente varios campos** que no puedan detectarse automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ff4de-113">Manual sign-in field capture can also be used in the case when the **vendor renders multiple fields** which cannot be auto-detected.</span></span> <span data-ttu-id="ff4de-114">Azure AD puede almacenar datos de tantos campos como haya en la página de inicio de sesión, siempre que se indique dónde se encuentran esos campos en la página.</span><span class="sxs-lookup"><span data-stu-id="ff4de-114">Azure AD can store data for as many fields as are on the sign in page, so long as you tell us where those fields are on the page.</span></span>

<span data-ttu-id="ff4de-115">Por lo general, **si la captura automática de campos de inicio de sesión no funciona, se recomienda siempre probar la opción manual.**</span><span class="sxs-lookup"><span data-stu-id="ff4de-115">In general, **if automatic sign-in field capture does not work, we always suggest trying the manual option.**</span></span>

### <a name="how-to-automatically-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ff4de-116">Captura automática de campos de inicio de sesión para una aplicación</span><span class="sxs-lookup"><span data-stu-id="ff4de-116">How to automatically capture sign-in fields for an application</span></span>

<span data-ttu-id="ff4de-117">Para configurar **Inicio de sesión único basado en contraseña** para una aplicación con la **captura automática de campos de inicio de sesión**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ff4de-117">To configure **Password-based Single Sign-on** for an application using **automatic sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="ff4de-118">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ff4de-119">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="ff4de-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ff4de-120">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ff4de-121">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff4de-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ff4de-122">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ff4de-122">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="ff4de-123">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="ff4de-123">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ff4de-124">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ff4de-124">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ff4de-125">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff4de-125">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ff4de-126">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-126">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ff4de-127">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-127">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ff4de-128">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ff4de-128">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ff4de-129">**Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL que proporcione**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-129">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="ff4de-130">Haga clic en el botón **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="ff4de-130">Click the **Save** button.</span></span>

11. <span data-ttu-id="ff4de-131">Una vez hecho esto, se cargará automáticamente esa dirección URL con un cuadro de entrada de un nombre de usuario y una contraseña y se le permitirá usar Azure AD para transmitir de forma segura las contraseñas de esa aplicación mediante la extensión de explorador del panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ff4de-131">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span>

## <a name="how-to-manually-capture-sign-in-fields-for-an-application"></a><span data-ttu-id="ff4de-132">Captura manual de campos de inicio de sesión para una aplicación</span><span class="sxs-lookup"><span data-stu-id="ff4de-132">How to manually capture sign-in fields for an application</span></span>

<span data-ttu-id="ff4de-133">Para capturar manualmente los campos de inicio de sesión, primero debe tener instalada la extensión del explorador del panel de acceso y **no utilizar el modo InPrivate, incógnito o privado.**</span><span class="sxs-lookup"><span data-stu-id="ff4de-133">To manually capture sign in fields, you must first have the Access Panel Browser extension installed and **not be running in inPrivate, incognito, or private mode.**</span></span> <span data-ttu-id="ff4de-134">Para instalar la extensión del explorador, siga los pasos descritos en la sección [Cómo instalar la extensión de explorador del Panel de acceso](#i-cannot-manually-detect-sign-in-fields-for-my-application).
.</span><span class="sxs-lookup"><span data-stu-id="ff4de-134">To install the browser extension, follow the steps in the [How to install the Access Panel Browser extension](#i-cannot-manually-detect-sign-in-fields-for-my-application) section.</span></span>

<span data-ttu-id="ff4de-135">Para configurar **Inicio de sesión único basado en contraseña** para una aplicación con la **captura manual de campos de inicio de sesión**, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ff4de-135">To configure **Password-based Single Sign-on** for an application using **manual sign-in field capture**, follow the steps below:</span></span>

1.  <span data-ttu-id="ff4de-136">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-136">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="ff4de-137">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="ff4de-137">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="ff4de-138">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-138">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="ff4de-139">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ff4de-139">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="ff4de-140">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="ff4de-140">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="ff4de-141">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="ff4de-141">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="ff4de-142">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ff4de-142">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="ff4de-143">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff4de-143">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="ff4de-144">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-144">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="ff4de-145">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-145">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="ff4de-146">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="ff4de-146">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="ff4de-147">**Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL que proporcione**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-147">**Ensure the sign in fields are visible at the URL you provide**.</span></span>

10. <span data-ttu-id="ff4de-148">Haga clic en el botón **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="ff4de-148">Click the **Save** button.</span></span>

11. <span data-ttu-id="ff4de-149">Una vez hecho esto, se cargará automáticamente esa dirección URL con un cuadro de entrada de un nombre de usuario y una contraseña y se le permitirá usar Azure AD para transmitir de forma segura las contraseñas de esa aplicación mediante la extensión de explorador del panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ff4de-149">Once you do that, we’ll automatically scrape that URL for a username and password input box and allow you to use Azure AD to securely transmit passwords to that application using the access panel browser extension.</span></span> <span data-ttu-id="ff4de-150">En el caso de que se produzca un error, puede **cambiar el modo de inicio de sesión para usar la captura manual de campos de inicio de sesión** siguiendo con el paso 12.</span><span class="sxs-lookup"><span data-stu-id="ff4de-150">In the case that this fails, you can **change the sign-in mode to use manual sign-in field capture** by continuing to step 12.</span></span>

12. <span data-ttu-id="ff4de-151">Haga clic en **Establecer configuración de inicio de sesión único con contraseña de &lt;nombre de la aplicación&gt;**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-151">click **Configure &lt;appname&gt; Password Single Sign-on Settings**.</span></span>

13. <span data-ttu-id="ff4de-152">Seleccione la opción de configuración **Detectar campos de inicio de sesión manualmente**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-152">Select the **Manually detect sign-in fields** configuration option.</span></span>

14. <span data-ttu-id="ff4de-153">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-153">Click **Ok**.</span></span>

15. <span data-ttu-id="ff4de-154">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-154">Click **Save**.</span></span>

16. <span data-ttu-id="ff4de-155">Siga las instrucciones en pantalla para usar el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ff4de-155">Follow the on screen instructions to use the Access Panel.</span></span>

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a><span data-ttu-id="ff4de-156">Error "No pudimos encontrar ningún campo de inicio de sesión en esa URL"</span><span class="sxs-lookup"><span data-stu-id="ff4de-156">I see a “We couldn’t find any sign-in fields at that URL” error</span></span>

<span data-ttu-id="ff4de-157">Este error aparece cuando no funciona la detección automática de campos de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="ff4de-157">You see this error when automatic detection of sign-in fields fails.</span></span> <span data-ttu-id="ff4de-158">Para resolver este problema, pruebe la detección manual de campos de inicio de sesión mediante los pasos descritos en la sección [Captura manual de campos de inicio de sesión para una aplicación](#how-to-manually-capture-sign-in-fields-for-an-application).</span><span class="sxs-lookup"><span data-stu-id="ff4de-158">To resolve this issue, try manual sign-in field detection by following the steps in the [How to manually capture sign-in fields for an application](#how-to-manually-capture-sign-in-fields-for-an-application) section.</span></span>

## <a name="i-see-an-unable-to-save-single-sign-on-configuration-error"></a><span data-ttu-id="ff4de-159">Error "No se puede guardar la configuración del inicio de sesión único"</span><span class="sxs-lookup"><span data-stu-id="ff4de-159">I see an “Unable to save Single Sign-on configuration” error</span></span>

<span data-ttu-id="ff4de-160">En algunos casos poco frecuentes, puede producirse un error al actualizar la configuración del inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="ff4de-160">In certain rare cases, updating the single sign-on configuration can fail.</span></span> <span data-ttu-id="ff4de-161">Para resolver este problema, intente guardar la configuración del inicio de sesión único de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ff4de-161">TO resolve this try saving the single sign-on configuration again.</span></span>

<span data-ttu-id="ff4de-162">Si el problema persiste, abra un caso de soporte técnico y proporcione la información recopilada en las secciones [Visualización de los detalles de una notificación del portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [Obtención de ayuda mediante el envío de detalles de la notificación a un ingeniero de soporte técnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer).</span><span class="sxs-lookup"><span data-stu-id="ff4de-162">If this continues to fail consistently, open a support case and provide the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections.</span></span>

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a><span data-ttu-id="ff4de-163">No se detectan manualmente campos de inicio de sesión para mi aplicación</span><span class="sxs-lookup"><span data-stu-id="ff4de-163">I cannot manually detect sign in fields for my application</span></span>

<span data-ttu-id="ff4de-164">Entre los comportamientos que pueden observarse cuando la detección manual no funciona se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff4de-164">Some of the behaviors you might see when manual detection is not working include:</span></span>

-   <span data-ttu-id="ff4de-165">El proceso de captura manual parece haber funcionado, pero los campos capturados no son correctos.</span><span class="sxs-lookup"><span data-stu-id="ff4de-165">The manual capture process appeared to work, but the fields captured were not correct</span></span>

-   <span data-ttu-id="ff4de-166">No se resaltan los campos correspondientes al realizar el proceso de captura.</span><span class="sxs-lookup"><span data-stu-id="ff4de-166">The right fields don’t get highlighted when performing the capture process</span></span>

-   <span data-ttu-id="ff4de-167">El proceso de captura me dirige a la página de inicio de sesión de la aplicación según lo previsto, pero no ocurre nada.</span><span class="sxs-lookup"><span data-stu-id="ff4de-167">The capture process takes me to the application’s login page as expected, but nothing happens</span></span>

-   <span data-ttu-id="ff4de-168">La captura manual parece funcionar, pero el SSO no se realiza cuando los usuarios acceden a la aplicación desde el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ff4de-168">Manual capture appears to work, but SSO doesn’t happen when my users navigate to the application from the Access Panel.</span></span>

<span data-ttu-id="ff4de-169">Compruebe lo siguiente si se produce alguno de estos problemas:</span><span class="sxs-lookup"><span data-stu-id="ff4de-169">check the following if you encounter any of these issues:</span></span>

-   <span data-ttu-id="ff4de-170">Asegúrese de tener **instalada** y **habilitada** la versión más reciente de la extensión del explorador del panel de acceso, para lo que debe seguir los pasos descritos en la sección [Cómo instalar la extensión de explorador del Panel de acceso](#how-to-install-the-access-panel-browser-extension).</span><span class="sxs-lookup"><span data-stu-id="ff4de-170">Ensure that you have the latest version of the access panel browser extension **installed** and **enabled** by following the steps in the [How to install the Access Panel Browser extension](#how-to-install-the-access-panel-browser-extension) section.</span></span>

-   <span data-ttu-id="ff4de-171">Asegúrese de que el explorador no se encuentre en los modos **InPrivate, incógnito o privado** mientras se realiza el proceso de captura.</span><span class="sxs-lookup"><span data-stu-id="ff4de-171">Ensure that you are not attempting the capture process while your browser in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="ff4de-172">La extensión del panel de acceso no es compatible con estos modos.</span><span class="sxs-lookup"><span data-stu-id="ff4de-172">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="ff4de-173">Asegúrese de que los usuarios no intentan iniciar sesión en la aplicación desde el panel de acceso en **los modos incógnito, InPrivate o privado**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-173">Ensure that your users are not trying to sign in to the application from the access panel while in **incognito, inPrivate, or Private mode**.</span></span> <span data-ttu-id="ff4de-174">La extensión del panel de acceso no es compatible con estos modos.</span><span class="sxs-lookup"><span data-stu-id="ff4de-174">The access panel extension is not supported in these modes.</span></span>

-   <span data-ttu-id="ff4de-175">Intente realizar el proceso de captura manual de nuevo, asegurándose de que los marcadores rojos se encuentren sobre los campos correctos.</span><span class="sxs-lookup"><span data-stu-id="ff4de-175">Try the manual capture process again, ensuring the red markers are over the correct fields.</span></span>

-   <span data-ttu-id="ff4de-176">Si el proceso de captura manual parece no responder o la página de inicio de sesión no hace nada (caso 3 anterior), intente realizar el proceso de captura manual de nuevo.</span><span class="sxs-lookup"><span data-stu-id="ff4de-176">If the manual capture process seems to hang, or the sign in page doesn’t do anything (case 3 above), try the manual capture process again.</span></span> <span data-ttu-id="ff4de-177">Sin embargo, esta vez, tras completar el proceso, presione el botón **F12** para abrir la consola del desarrollador del explorador.</span><span class="sxs-lookup"><span data-stu-id="ff4de-177">But, this time after completing the process, press the **F12** button to open your browser’s developer console.</span></span> <span data-ttu-id="ff4de-178">Una vez allí, abra la **consola** y escriba **window.location=”&lt;escriba la dirección URL de inicio de sesión especificada al configurar la aplicación&gt;”** y, a continuación, presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-178">Once there, open the **console** and type **window.location=”&lt;enter the sign in url you specified when configuring the app&gt;”** and then press **Enter**.</span></span> <span data-ttu-id="ff4de-179">De este modo, se forzará una redirección de página que finalizará el proceso de captura y almacenará los campos que se han capturado.</span><span class="sxs-lookup"><span data-stu-id="ff4de-179">This force a page redirect which end the capture process and store the fields that have been captured.</span></span>

<span data-ttu-id="ff4de-180">Si ninguno de estos métodos funciona, podemos ayudarle.</span><span class="sxs-lookup"><span data-stu-id="ff4de-180">If none of these approaches work for you, we can help.</span></span> <span data-ttu-id="ff4de-181">Abra un caso de soporte técnico en el que explique todo lo que ha intentado, además de proporcionar la información recopilada en las secciones [Visualización de los detalles de una notificación del portal](#i-cannot-manually-detect-sign-in-fields-for-my-application) y [Obtención de ayuda mediante el envío de detalles de la notificación a un ingeniero de soporte técnico](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) (si corresponde).</span><span class="sxs-lookup"><span data-stu-id="ff4de-181">Open a support case with the details of what you tried, as well as the information gathered in the [How to see the details of a portal notification](#i-cannot-manually-detect-sign-in-fields-for-my-application) and [How to get help by sending notification details to a support engineer](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) sections (if applicable).</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="ff4de-182">Cómo instalar la extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="ff4de-182">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="ff4de-183">Para instalar la extensión de explorador del Panel de acceso, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="ff4de-183">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="ff4de-184">Abra el [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores admitidos e inicie sesión como **usuario** en su instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff4de-184">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="ff4de-185">Haga clic en una **aplicación de SSO con contraseña** en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="ff4de-185">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="ff4de-186">En el mensaje que le pregunta si desea instalar el software, seleccione **Instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-186">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="ff4de-187">Se le dirigirá al vínculo de descarga en función del explorador.</span><span class="sxs-lookup"><span data-stu-id="ff4de-187">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="ff4de-188">**Agregue** la extensión al explorador.</span><span class="sxs-lookup"><span data-stu-id="ff4de-188">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="ff4de-189">Si el explorador lo solicita, seleccione **Habilitar** o **Permitir** la extensión.</span><span class="sxs-lookup"><span data-stu-id="ff4de-189">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="ff4de-190">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="ff4de-190">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="ff4de-191">Inicie sesión en el panel de acceso y vea si puede **iniciar** las aplicaciones de SSO con contraseña.</span><span class="sxs-lookup"><span data-stu-id="ff4de-191">Sign in into the Access Panel and see if you can **launch** your password-SSO applications.</span></span>

<span data-ttu-id="ff4de-192">También puede descargar la extensión para Chrome y Firefox desde los siguientes vínculos directos:</span><span class="sxs-lookup"><span data-stu-id="ff4de-192">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="ff4de-193">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="ff4de-193">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="ff4de-194">Extensión del panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="ff4de-194">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="ff4de-195">Visualización de los detalles de una notificación del portal</span><span class="sxs-lookup"><span data-stu-id="ff4de-195">How to see the details of a portal notification</span></span>

<span data-ttu-id="ff4de-196">Puede ver los detalles de cualquier notificación del portal si sigue los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="ff4de-196">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="ff4de-197">Haga clic en el icono de **notificaciones** (la campana) de la esquina superior derecha de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ff4de-197">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="ff4de-198">Seleccione cualquier notificación con un estado de **Error** (aquellas con un icono (!) de color rojo situado junto a ellas).</span><span class="sxs-lookup"><span data-stu-id="ff4de-198">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

  ><span data-ttu-id="ff4de-199">[NOTA] No puede hacer clic en notificaciones con un estado **Correcto** o **En curso**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-199">!NOTE] You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
  >
  >

3.  <span data-ttu-id="ff4de-200">Esto hace que se abra la hoja **Detalles de la notificación**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-200">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="ff4de-201">Utilice esta información para conocer más detalles acerca del problema.</span><span class="sxs-lookup"><span data-stu-id="ff4de-201">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="ff4de-202">Si aún necesita ayuda, también puede compartir esta información con un ingeniero de soporte técnico o el grupo de producto para obtener ayuda.</span><span class="sxs-lookup"><span data-stu-id="ff4de-202">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="ff4de-203">Haga clic en el **icono** de **copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto.</span><span class="sxs-lookup"><span data-stu-id="ff4de-203">Click the **copy** **icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="ff4de-204">Obtención de ayuda mediante el envío de detalles de la notificación a un ingeniero de soporte técnico</span><span class="sxs-lookup"><span data-stu-id="ff4de-204">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="ff4de-205">Es muy importante que comparta **todos los detalles que se muestran a continuación** con un ingeniero de soporte técnico si necesita ayuda, para que pueda ayudarle rápidamente.</span><span class="sxs-lookup"><span data-stu-id="ff4de-205">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="ff4de-206">Puede hacer esto fácilmente **realizando una captura de pantalla** o haciendo clic en el **icono Copiar error**, que se encuentra a la derecha del cuadro de texto **Copiar error**.</span><span class="sxs-lookup"><span data-stu-id="ff4de-206">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="ff4de-207">Explicación de los detalles de la notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-207">Notification Details Explained</span></span>

<span data-ttu-id="ff4de-208">A continuación se explica más en profundidad lo que significa cada uno de los elementos de notificación y se dan ejemplos de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="ff4de-208">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="ff4de-209">Elementos esenciales de notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-209">Essential Notification Items</span></span>

-   <span data-ttu-id="ff4de-210">**Título**: el título descriptivo de la notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-210">**Title** – the descriptive title of the notification</span></span>

    -   <span data-ttu-id="ff4de-211">Por ejemplo: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="ff4de-211">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="ff4de-212">**Descripción**: la descripción de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-212">**Description** – the description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="ff4de-213">Por ejemplo: **la dirección url interna especificada ya se está usando en otra aplicación**</span><span class="sxs-lookup"><span data-stu-id="ff4de-213">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="ff4de-214">**Identificador de notificación**: el identificador único de la notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-214">**Notification Id** – the unique id of the notification</span></span>

    -   <span data-ttu-id="ff4de-215">Por ejemplo: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="ff4de-215">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="ff4de-216">**Identificador de solicitud de cliente**: el identificador de solicitud específico generado por el explorador</span><span class="sxs-lookup"><span data-stu-id="ff4de-216">**Client Request Id** – the specific request id made by your browser</span></span>

    -   <span data-ttu-id="ff4de-217">Por ejemplo: **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="ff4de-217">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="ff4de-218">**Marca de tiempo UTC**: la marca de tiempo durante la que tuvo lugar la notificación, en formato UTC</span><span class="sxs-lookup"><span data-stu-id="ff4de-218">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

    -   <span data-ttu-id="ff4de-219">Por ejemplo: **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="ff4de-219">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="ff4de-220">**Identificador de transacción interno**: el identificador interno que podemos utilizar para buscar el error en nuestros sistemas</span><span class="sxs-lookup"><span data-stu-id="ff4de-220">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

    -   <span data-ttu-id="ff4de-221">Por ejemplo: **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="ff4de-221">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="ff4de-222">**UPN**: el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-222">**UPN** – the user who performed the operation</span></span>

    -   <span data-ttu-id="ff4de-223">Por ejemplo: **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="ff4de-223">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="ff4de-224">**Identificador de inquilino**: el identificador único del inquilino del que formaba parte el usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-224">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

    -   <span data-ttu-id="ff4de-225">Por ejemplo: **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="ff4de-225">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="ff4de-226">**Identificador de objeto de usuario**: el identificador único del usuario que realizó la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-226">**User object Id** – the unique ID of the user who performed the operation</span></span>

    -   <span data-ttu-id="ff4de-227">Por ejemplo: **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="ff4de-227">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="ff4de-228">Elementos detallados de notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-228">Detailed Notification Items</span></span>

-   <span data-ttu-id="ff4de-229">**Nombre para mostrar**: **(puede estar vacío)** un nombre para mostrar más detallado del error</span><span class="sxs-lookup"><span data-stu-id="ff4de-229">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

    -   <span data-ttu-id="ff4de-230">Por ejemplo*: **Configuración del proxy de aplicación**</span><span class="sxs-lookup"><span data-stu-id="ff4de-230">Example *– **Application proxy settings**</span></span>

-   <span data-ttu-id="ff4de-231">**Estado**: el estado específico de la notificación</span><span class="sxs-lookup"><span data-stu-id="ff4de-231">**Status** – the specific status of the notification</span></span>

    -   <span data-ttu-id="ff4de-232">Por ejemplo*: **Error**</span><span class="sxs-lookup"><span data-stu-id="ff4de-232">Example *– **Failed**</span></span>

-   <span data-ttu-id="ff4de-233">**Identificador de objeto**: **(puede estar vacío)** el identificador del objeto en el que se realizó la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-233">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

    -   <span data-ttu-id="ff4de-234">Por ejemplo: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="ff4de-234">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="ff4de-235">**Detalles**: la descripción detallada de lo que se produjo como resultado de la operación</span><span class="sxs-lookup"><span data-stu-id="ff4de-235">**Details** – the detailed description of what occurred as a result of the operation</span></span>

    -   <span data-ttu-id="ff4de-236">Por ejemplo: **la dirección url interna 'http://bing.com/' no es válida puesto que ya está en uso**</span><span class="sxs-lookup"><span data-stu-id="ff4de-236">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="ff4de-237">**Copiar error**: haga clic en el **icono de copia** situado a la derecha del cuadro de texto **Copiar error** para copiar todos los detalles de la notificación para compartirlos con un ingeniero de soporte técnico o un grupo de producto</span><span class="sxs-lookup"><span data-stu-id="ff4de-237">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

    -   <span data-ttu-id="ff4de-238">Por ejemplo: ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="ff4de-238">Example – ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff4de-239">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ff4de-239">Next steps</span></span>
[<span data-ttu-id="ff4de-240">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="ff4de-240">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

