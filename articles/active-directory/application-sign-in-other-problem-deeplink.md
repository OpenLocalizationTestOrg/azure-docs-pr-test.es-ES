---
title: "Problemas de inicio de sesión con un vínculo profundo en una aplicación | Microsoft Docs"
description: "Cómo solucionar problemas de acceso a una aplicación desde una dirección URL de vínculo profundo con Azure AD"
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
ms.openlocfilehash: 798015ab68afc65378cffc75afec9c7f91fc1926
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="baf30-103">Problemas de inicio de sesión con un vínculo profundo en una aplicación</span><span class="sxs-lookup"><span data-stu-id="baf30-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="baf30-104">El Panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa de Azure Active Directory (Azure AD) vea e inicie las aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="baf30-105">Estas aplicaciones se configuran en nombre del usuario en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baf30-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="baf30-106">La aplicación debe configurarse correctamente y asignarse al usuario o al grupo del que el usuario es miembro para poder ver la aplicación en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="baf30-107">Las direcciones URL de acceso de usuario o vínculos profundos son vínculos que los usuarios pueden utilizar para acceder a sus aplicaciones de SSO con contraseña directamente desde las barras de dirección URL de los exploradores.</span><span class="sxs-lookup"><span data-stu-id="baf30-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="baf30-108">Al ir a este vínculo, los usuarios pueden iniciar sesión automáticamente en la aplicación sin tener que ir primero al Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="baf30-109">Se trata del mismo vínculo que los usuarios utilizan para acceder a estas aplicaciones desde el iniciador de la aplicación de Office 365.</span><span class="sxs-lookup"><span data-stu-id="baf30-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="baf30-110">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="baf30-110">General issues to check first</span></span>

-   <span data-ttu-id="baf30-111">Que se usa un **explorador** que cumpla los requisitos mínimos del Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="baf30-112">Que se ha agregado la dirección URL de la aplicación a los **sitios de confianza** del explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="baf30-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="baf30-113">Que la aplicación está **configurada** correctamente.</span><span class="sxs-lookup"><span data-stu-id="baf30-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="baf30-114">Que la cuenta del usuario está **habilitada** para los inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="baf30-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="baf30-115">Que la cuenta del usuario **no está bloqueada**.</span><span class="sxs-lookup"><span data-stu-id="baf30-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="baf30-116">Que la **contraseña del usuario no ha expirado o se ha olvidado**.</span><span class="sxs-lookup"><span data-stu-id="baf30-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="baf30-117">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="baf30-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="baf30-118">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="baf30-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="baf30-119">Que la **información de contacto de autenticación** del usuario está actualizada para permitir la aplicación de directivas de Multi-Factor Authentication o de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="baf30-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="baf30-120">Que se intenta borrar también las cookies del explorador y volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="baf30-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="baf30-121">Comprobación del vínculo profundo</span><span class="sxs-lookup"><span data-stu-id="baf30-121">Checking the deeplink</span></span>

<span data-ttu-id="baf30-122">Para comprobar si tiene el vínculo profundo correcto, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-123">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="baf30-124">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-125">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-126">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-127">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf30-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="baf30-128">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="baf30-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="baf30-129">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="baf30-130">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="baf30-131">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="baf30-132">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="baf30-133">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf30-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="baf30-134">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="baf30-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="baf30-135">Seleccione la aplicación para la cual desea comprobar el vínculo profundo.</span><span class="sxs-lookup"><span data-stu-id="baf30-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="baf30-136">Busque la etiqueta **URL de acceso de usuario**.</span><span class="sxs-lookup"><span data-stu-id="baf30-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="baf30-137">El vínculo profundo debe coincidir con esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="baf30-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="baf30-138">Cómo instalar la extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="baf30-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="baf30-139">Para instalar la extensión de explorador del Panel de acceso, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-140">Abra el [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores admitidos e inicie sesión como **usuario** en su instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="baf30-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="baf30-141">Haga clic en una **aplicación de SSO con contraseña** en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="baf30-142">En el mensaje que le pregunta si desea instalar el software, seleccione **Instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="baf30-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="baf30-143">Se le dirigirá al vínculo de descarga en función del explorador.</span><span class="sxs-lookup"><span data-stu-id="baf30-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="baf30-144">**Agregue** la extensión al explorador.</span><span class="sxs-lookup"><span data-stu-id="baf30-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="baf30-145">Si el explorador lo solicita, seleccione **Habilitar** o **Permitir** la extensión.</span><span class="sxs-lookup"><span data-stu-id="baf30-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="baf30-146">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="baf30-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="baf30-147">Inicie sesión en el Panel de acceso y vea si puede **iniciar** las aplicaciones de SSO con contraseña</span><span class="sxs-lookup"><span data-stu-id="baf30-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="baf30-148">También puede descargar la extensión para Chrome y Firefox desde los siguientes vínculos directos:</span><span class="sxs-lookup"><span data-stu-id="baf30-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="baf30-149">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="baf30-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="baf30-150">Extensión del Panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="baf30-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="baf30-151">Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baf30-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="baf30-152">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="baf30-153">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baf30-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="baf30-154">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="baf30-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="baf30-155">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="baf30-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="baf30-156">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-157">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="baf30-158">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-159">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-160">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-161">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="baf30-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="baf30-162">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="baf30-163">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="baf30-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="baf30-164">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="baf30-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="baf30-165">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="baf30-166">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="baf30-167">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="baf30-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="baf30-168">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-169">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="baf30-170">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-171">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-172">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-173">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf30-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="baf30-174">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="baf30-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="baf30-175">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="baf30-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="baf30-176">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="baf30-177">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="baf30-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="baf30-178">[Asigne usuarios a la aplicación](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="baf30-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="baf30-179">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="baf30-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="baf30-180">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="baf30-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="baf30-181">Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="baf30-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="baf30-182">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="baf30-183">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="baf30-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="baf30-184">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="baf30-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="baf30-185">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="baf30-185">Add a non-gallery application</span></span>

<span data-ttu-id="baf30-186">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-187">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="baf30-188">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-189">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-190">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-191">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="baf30-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="baf30-192">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="baf30-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="baf30-193">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="baf30-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="baf30-194">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="baf30-194">Select **Add.**</span></span>

<span data-ttu-id="baf30-195">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="baf30-196">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="baf30-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="baf30-197">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="baf30-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-198">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="baf30-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="baf30-199">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-200">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-201">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-202">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf30-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="baf30-203">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="baf30-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="baf30-204">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="baf30-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="baf30-205">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="baf30-206">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="baf30-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="baf30-207">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="baf30-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="baf30-208">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="baf30-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="baf30-209">Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="baf30-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="baf30-210">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-210">Assign users to the application.</span></span>

11. <span data-ttu-id="baf30-211">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="baf30-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="baf30-212">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="baf30-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="baf30-213">Asignación de un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="baf30-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="baf30-214">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="baf30-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="baf30-215">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="baf30-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="baf30-216">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="baf30-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="baf30-217">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="baf30-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="baf30-218">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="baf30-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="baf30-219">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="baf30-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="baf30-220">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="baf30-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="baf30-221">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="baf30-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="baf30-222">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="baf30-223">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="baf30-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="baf30-224">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="baf30-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="baf30-225">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="baf30-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="baf30-226">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="baf30-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="baf30-227">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="baf30-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="baf30-228">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="baf30-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="baf30-229">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="baf30-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="baf30-230">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="baf30-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="baf30-231">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="baf30-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="baf30-232">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="baf30-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="baf30-233">Si después de seguir estos pasos el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="baf30-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="baf30-234">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="baf30-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="baf30-235">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="baf30-235">Correlation error ID</span></span>

-   <span data-ttu-id="baf30-236">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="baf30-236">UPN (user email address)</span></span>

-   <span data-ttu-id="baf30-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="baf30-237">TenantID</span></span>

-   <span data-ttu-id="baf30-238">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="baf30-238">Browser type</span></span>

-   <span data-ttu-id="baf30-239">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="baf30-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="baf30-240">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="baf30-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="baf30-241">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="baf30-241">Next steps</span></span>
[<span data-ttu-id="baf30-242">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="baf30-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
