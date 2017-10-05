---
title: "Problemas de inicio de sesión en una aplicación desde el panel de acceso | Microsoft Docs"
description: "Cómo solucionar problemas de acceso a una aplicación desde el Panel de acceso de Microsoft Azure AD de myapps.microsoft.com"
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
ms.openlocfilehash: 188a00db59b0aa8d26facc678fb52d96272183b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-application-from-the-access-panel"></a><span data-ttu-id="7539c-103">Problemas de inicio de sesión en una aplicación desde el panel de acceso</span><span class="sxs-lookup"><span data-stu-id="7539c-103">Problems signing in to an application from the access panel</span></span>

<span data-ttu-id="7539c-104">El Panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa de Azure Active Directory (Azure AD) vea e inicie las aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="7539c-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="7539c-105">Estas aplicaciones se configuran en nombre del usuario en el portal de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7539c-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="7539c-106">La aplicación debe configurarse correctamente y asignarse al usuario o al grupo del que el usuario es miembro para poder ver la aplicación en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7539c-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="7539c-107">El tipo de aplicaciones que un usuario puede ver se dividen en las siguientes categorías:</span><span class="sxs-lookup"><span data-stu-id="7539c-107">The type of apps a user may be seeing fall in the following categories:</span></span>

-   <span data-ttu-id="7539c-108">Aplicaciones de Office 365</span><span class="sxs-lookup"><span data-stu-id="7539c-108">Office 365 Applications</span></span>

-   <span data-ttu-id="7539c-109">Aplicaciones de Microsoft y de terceros configuradas con SSO basado en federación</span><span class="sxs-lookup"><span data-stu-id="7539c-109">Microsoft and third-party applications configured with federation-based SSO</span></span>

-   <span data-ttu-id="7539c-110">Aplicaciones de SSO basado en contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-110">Password-based SSO applications</span></span>

-   <span data-ttu-id="7539c-111">Aplicaciones con soluciones SSO existentes</span><span class="sxs-lookup"><span data-stu-id="7539c-111">Applications with existing SSO solutions</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="7539c-112">Problemas generales para comprobar primero</span><span class="sxs-lookup"><span data-stu-id="7539c-112">General issues to check first</span></span>

-   <span data-ttu-id="7539c-113">Que se usa un **explorador** que cumpla los requisitos mínimos del Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7539c-113">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="7539c-114">Que se ha agregado la dirección URL de la aplicación a los **sitios de confianza** del explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-114">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="7539c-115">Que la aplicación está **configurada** correctamente.</span><span class="sxs-lookup"><span data-stu-id="7539c-115">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="7539c-116">Que la cuenta del usuario está **habilitada** para los inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-116">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="7539c-117">Que la cuenta del usuario **no está bloqueada**.</span><span class="sxs-lookup"><span data-stu-id="7539c-117">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="7539c-118">Que la **contraseña del usuario no ha expirado o se ha olvidado**.</span><span class="sxs-lookup"><span data-stu-id="7539c-118">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="7539c-119">Que **Multi-Factor Authentication** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-119">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="7539c-120">Que una **directiva de acceso condicional** o una directiva de **protección de identidad** no bloquea el acceso del usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-120">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="7539c-121">Que la **información de contacto de autenticación** del usuario está actualizada para permitir la aplicación de directivas de Multi-Factor Authentication o de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="7539c-121">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="7539c-122">Que se intenta borrar también las cookies del explorador y volver a iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-122">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="7539c-123">Cumplimiento de los requisitos del explorador para el Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="7539c-123">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="7539c-124">El Panel de acceso requiere un explorador compatible con JavaScript y que tenga habilitado CSS.</span><span class="sxs-lookup"><span data-stu-id="7539c-124">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="7539c-125">Para usar el inicio de sesión único (SSO) basado en contraseña en el Panel de acceso, se debe instalar la extensión del Panel de acceso en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-125">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="7539c-126">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="7539c-126">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="7539c-127">Para el SSO basado en contraseña, los exploradores del usuario final pueden ser:</span><span class="sxs-lookup"><span data-stu-id="7539c-127">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="7539c-128">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="7539c-128">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="7539c-129">Edge en Windows 10 Anniversary Edition o posterior</span><span class="sxs-lookup"><span data-stu-id="7539c-129">Edge on Windows 10 Anniversary Edition or later</span></span>

-   <span data-ttu-id="7539c-130">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="7539c-130">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="7539c-131">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="7539c-131">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="7539c-132">Cómo instalar la extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="7539c-132">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="7539c-133">Para instalar la extensión de explorador del Panel de acceso, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-133">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-134">Abra el [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores admitidos e inicie sesión como **usuario** en su instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7539c-134">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="7539c-135">Haga clic en una **aplicación de SSO con contraseña** en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7539c-135">Click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="7539c-136">En el mensaje que le pregunta si desea instalar el software, seleccione **Instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="7539c-136">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="7539c-137">Se le dirigirá al vínculo de descarga en función del explorador.</span><span class="sxs-lookup"><span data-stu-id="7539c-137">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="7539c-138">**Agregue** la extensión al explorador.</span><span class="sxs-lookup"><span data-stu-id="7539c-138">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="7539c-139">Si el explorador lo solicita, seleccione **Habilitar** o **Permitir** la extensión.</span><span class="sxs-lookup"><span data-stu-id="7539c-139">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="7539c-140">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="7539c-140">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="7539c-141">Inicie sesión en el Panel de acceso y vea si puede **iniciar** las aplicaciones de SSO con contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-141">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="7539c-142">También puede descargar la extensión para Chrome y Edge desde los siguientes vínculos directos:</span><span class="sxs-lookup"><span data-stu-id="7539c-142">You may also download the extension for Chrome and Edge from the direct links below:</span></span>

-   [<span data-ttu-id="7539c-143">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="7539c-143">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="7539c-144">Extensión del Panel de acceso para Edge</span><span class="sxs-lookup"><span data-stu-id="7539c-144">Edge Access Panel Extension</span></span>](https://www.microsoft.com/store/apps/9pc9sckkzk84)

## <a name="how-to-configure-federated-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="7539c-145">Configuración del inicio de sesión único federado para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-145">How to configure federated single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="7539c-146">Todas las aplicaciones de la galería de Azure AD habilitadas con funcionalidad de Enterprise Single Sign-On tienen un tutorial paso a paso disponible.</span><span class="sxs-lookup"><span data-stu-id="7539c-146">All application in the Azure AD gallery enabled with Enterprise Single Sign-On capability has a step-by-step tutorial available.</span></span> <span data-ttu-id="7539c-147">Para instrucciones detalladas paso a paso, acceda a la [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/).</span><span class="sxs-lookup"><span data-stu-id="7539c-147">You can access the [List of tutorials on how to integrate SaaS apps with Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saas-tutorial-list/) for a detail step-by-step guidance.</span></span>

<span data-ttu-id="7539c-148">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-148">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="7539c-149">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-149">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="7539c-150">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="7539c-150">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="7539c-151">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-151">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="7539c-152">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-152">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="7539c-153">Configuración de los valores de los metadatos de Azure AD en la aplicación (URL de inicio de sesión, emisor, URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="7539c-153">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configure-single-sign-on-for-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="7539c-154">Asignación de usuarios a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-154">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="7539c-155">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="7539c-156">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-157">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="7539c-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="7539c-158">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-159">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-160">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-161">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7539c-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="7539c-162">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="7539c-163">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="7539c-164">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="7539c-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="7539c-165">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="7539c-166">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-single-sign-on-for-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="7539c-167">Configuración del inicio de sesión único para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-167">Configure single sign-on for an application from the Azure AD gallery</span></span>

<span data-ttu-id="7539c-168">Para configurar el inicio de sesión único para una aplicación, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7539c-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-169"><span id="_Hlk477187909" class="anchor"><span id="_Hlk477001983" class="anchor"></span></span>Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-170">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-171">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-172">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-173">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7539c-174">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-175">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7539c-176">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-177">En la lista desplegable **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="7539c-177">Select **SAML-based Sign-on** from the **Mode** dropdown.</span></span>

9.  <span data-ttu-id="7539c-178">Especifique los valores obligatorios en **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="7539c-178">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="7539c-179">El proveedor de la aplicación le proporcionará estos valores.</span><span class="sxs-lookup"><span data-stu-id="7539c-179">You should get these values from the application vendor.</span></span>

   1. <span data-ttu-id="7539c-180">Para configurar la aplicación como SSO iniciado por el SP, la dirección URL de inicio de sesión es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="7539c-180">To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span> <span data-ttu-id="7539c-181">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7539c-181">For some applications, the Identifier is also a required value.</span></span>

   2. <span data-ttu-id="7539c-182">Para configurar la aplicación como SSO iniciado por el IdP, la dirección URL de respuesta es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="7539c-182">To configure the application as IdP-initiated SSO, the Reply URL it’s a required value.</span></span> <span data-ttu-id="7539c-183">En algunas aplicaciones, el identificador también es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="7539c-183">For some applications, the Identifier is also a required value.</span></span>

10. <span data-ttu-id="7539c-184">**Opcional:** haga clic en **Mostrar configuración avanzada de URL** si desea ver los valores opcionales.</span><span class="sxs-lookup"><span data-stu-id="7539c-184">**Optional:** click **Show advanced URL settings** if you want to see the non-required values.</span></span>

11. <span data-ttu-id="7539c-185">En **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7539c-185">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

12. <span data-ttu-id="7539c-186">**Opcional:** haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-186">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7539c-187">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="7539c-187">To add an attribute:</span></span>

   1. <span data-ttu-id="7539c-188">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="7539c-188">click **Add attribute**.</span></span> <span data-ttu-id="7539c-189">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="7539c-189">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="7539c-190">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-190">Click **Save.**</span></span> <span data-ttu-id="7539c-191">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="7539c-191">You see the new attribute in the table.</span></span>

13. <span data-ttu-id="7539c-192">Haga clic en **Configurar &lt;nombre de la aplicación&gt;** para acceder a documentación sobre cómo configurar el inicio de sesión único en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-192">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="7539c-193">Además, tiene las direcciones URL de los metadatos y el certificado necesario para la instalación de SSO con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-193">Also, you has the metadata URLs and certificate required to setup SSO with the application.</span></span>

14. <span data-ttu-id="7539c-194">Para guardar la configuración, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-194">Click **Save** to save the configuration.</span></span>

15. <span data-ttu-id="7539c-195">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-195">Assign users to the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="7539c-196">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-196">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="7539c-197">Para seleccionar el identificador de usuario o agregar atributos de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-197">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-198">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-199">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-200">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-201">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-202">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-202">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7539c-203">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7539c-203">If you do not see the application you want to show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-204">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-204">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7539c-205">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-206">En la sección **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7539c-206">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="7539c-207">La opción seleccionada debe coincidir con el valor esperado de la aplicación para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-207">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7539c-208">AD Azure selecciona el formato del atributo NameID (Identificador de usuario) en función del valor seleccionado o del formato que solicite la aplicación en el elemento AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="7539c-208">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="7539c-209">Para más información, visite la sección NameIDPolicy del artículo [Protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="7539c-209">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
    >
    >

9.  <span data-ttu-id="7539c-210">Para agregar atributos de usuario, haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-210">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7539c-211">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="7539c-211">To add an attribute:</span></span>

   1. <span data-ttu-id="7539c-212">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="7539c-212">click **Add attribute**.</span></span> <span data-ttu-id="7539c-213">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="7539c-213">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="7539c-214">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-214">Click **Save.**</span></span> <span data-ttu-id="7539c-215">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="7539c-215">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="7539c-216">Descarga del certificado o los metadatos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-216">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="7539c-217">Para descargar el certificado o los metadatos de la aplicación de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-217">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-218">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-218">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-219">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-219">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-220">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-220">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-221">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-221">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-222">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-222">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7539c-223">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-223">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-224">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-224">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7539c-225">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-225">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-226">Vaya a la sección **Certificado de firma de SAML** y haga clic en el valor de la columna **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-226">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7539c-227">Según lo que necesite la aplicación para configurar el inicio de sesión único, verá la opción para descargar el archivo XML de metadatos o el certificado.</span><span class="sxs-lookup"><span data-stu-id="7539c-227">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="7539c-228">Azure AD no proporciona una dirección URL para obtener los metadatos.</span><span class="sxs-lookup"><span data-stu-id="7539c-228">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="7539c-229">Solo se pueden recuperar como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="7539c-229">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-federated-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7539c-230">Configuración del inicio de sesión único federado para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="7539c-230">How to configure federated single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7539c-231">Para configurar una aplicación ajena a la galería, debe tener Azure AD Premium y que la aplicación admita SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="7539c-231">To configure a non-gallery application, you need to have Azure AD premium and the application supports SAML 2.0.</span></span> <span data-ttu-id="7539c-232">Para más información acerca de las versiones de Azure AD, visite [Precios de Azure AD](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="7539c-232">For more information about Azure AD versions, visit [Azure AD pricing](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

-   [<span data-ttu-id="7539c-233">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="7539c-233">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>](#configuring-single-sign-on)

-   [<span data-ttu-id="7539c-234">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-234">Select User Identifier and add user attributes to be sent to the application</span></span>](#select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application)

-   [<span data-ttu-id="7539c-235">Recuperación de los metadatos y el certificado de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-235">Retrieve Azure AD metadata and certificate</span></span>](#download-the-azure-ad-metadata-or-certificate)

-   [<span data-ttu-id="7539c-236">Configuración de los valores de los metadatos de Azure AD en la aplicación (URL de inicio de sesión, emisor, URL de cierre de sesión y certificado)</span><span class="sxs-lookup"><span data-stu-id="7539c-236">Configure Azure AD metadata values in the application (Sign on URL, Issuer, Logout URL and certificate)</span></span>](#configuring-single-sign-on)

### <a name="configure-the-applications-metadata-values-in-azure-ad-sign-on-url-identifier-reply-url"></a><span data-ttu-id="7539c-237">Configuración de los valores de los metadatos de la aplicación en Azure AD (URL de inicio de sesión, identificador, URL de respuesta)</span><span class="sxs-lookup"><span data-stu-id="7539c-237">Configure the application’s metadata values in Azure AD (Sign on URL, Identifier, Reply URL)</span></span>

<span data-ttu-id="7539c-238">Para configurar el inicio de sesión único para una aplicación ajena a la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-238">To configure single sign-on for an application that is not in the Azure AD gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-239">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-239">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-240">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-240">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-241">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-241">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-242">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-242">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-243">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7539c-243">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="7539c-244">En la sección **Agregar aplicación propia**, haga clic en **Aplicación situada fuera de la galería**</span><span class="sxs-lookup"><span data-stu-id="7539c-244">click **Non-gallery application** in the **Add your own app** section</span></span>

7.  <span data-ttu-id="7539c-245">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="7539c-245">Enter the name of the application in the **Name** textbox.</span></span>

8.  <span data-ttu-id="7539c-246">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-246">Click **Add** button, to add the application.</span></span>

9.  <span data-ttu-id="7539c-247">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-247">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

10. <span data-ttu-id="7539c-248">En la lista desplegable **Modo**, seleccione **Inicio de sesión basado en SAML**.</span><span class="sxs-lookup"><span data-stu-id="7539c-248">Select **SAML-based Sign-on** in the **Mode** dropdown</span></span>

11. <span data-ttu-id="7539c-249">Especifique los valores obligatorios en **Dominio y direcciones URL**.</span><span class="sxs-lookup"><span data-stu-id="7539c-249">Enter the required values in **Domain and URLs.**</span></span> <span data-ttu-id="7539c-250">El proveedor de la aplicación le proporcionará estos valores.</span><span class="sxs-lookup"><span data-stu-id="7539c-250">You should get these values from the application vendor.</span></span>

  1. <span data-ttu-id="7539c-251">Para configurar la aplicación como SSO iniciado por el IdP, escriba la dirección URL de respuesta y el identificador.</span><span class="sxs-lookup"><span data-stu-id="7539c-251">To configure the application as IdP-initiated SSO, enter the Reply URL and the Identifier.</span></span>

  2. <span data-ttu-id="7539c-252">**Opcional:** para configurar la aplicación como SSO iniciado por el SP, la dirección URL de inicio de sesión es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="7539c-252">**Optional:** To configure the application as SP-initiated SSO, the Sign on URL it’s a required value.</span></span>

12. <span data-ttu-id="7539c-253">En **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7539c-253">In the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

13. <span data-ttu-id="7539c-254">**Opcional:** haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-254">**Optional:** click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7539c-255">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="7539c-255">To add an attribute:</span></span>

   1. <span data-ttu-id="7539c-256">Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="7539c-256">click **Add attribute**.</span></span> <span data-ttu-id="7539c-257">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="7539c-257">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   2. <span data-ttu-id="7539c-258">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-258">Click **Save.**</span></span> <span data-ttu-id="7539c-259">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="7539c-259">You see the new attribute in the table.</span></span>

14. <span data-ttu-id="7539c-260">Haga clic en **Configurar &lt;nombre de la aplicación&gt;** para acceder a documentación sobre cómo configurar el inicio de sesión único en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-260">click **Configure &lt;application name&gt;** to access documentation on how to configure single sign-on in the application.</span></span> <span data-ttu-id="7539c-261">Además, tiene las direcciones URL de Azure AD y los certificados necesarios para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-261">Also, you has Azure AD URLs and certificate required for the application.</span></span>

### <a name="select-user-identifier-and-add-user-attributes-to-be-sent-to-the-application"></a><span data-ttu-id="7539c-262">Selección del identificador de usuario e incorporación de los atributos de usuario para enviarlos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-262">Select User Identifier and add user attributes to be sent to the application</span></span>

<span data-ttu-id="7539c-263">Para seleccionar el identificador de usuario o agregar atributos de usuario, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-263">To select the User Identifier or add user attributes, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-264">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-264">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-265">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-265">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-266">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-266">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-267">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-267">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-268">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-268">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7539c-269">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-269">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-270">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-270">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7539c-271">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-271">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-272">En la sección **Atributos de usuario**, seleccione el identificador único para los usuarios de la lista desplegable **Identificador de usuario**.</span><span class="sxs-lookup"><span data-stu-id="7539c-272">Under the **User attributes** section, select the unique identifier for your users in the **User Identifier** dropdown.</span></span> <span data-ttu-id="7539c-273">La opción seleccionada debe coincidir con el valor esperado de la aplicación para autenticar al usuario.</span><span class="sxs-lookup"><span data-stu-id="7539c-273">The selected option needs to match the expected value in the application to authenticate the user.</span></span>

   >[!NOTE]
   ><span data-ttu-id="7539c-274">AD Azure selecciona el formato del atributo NameID (Identificador de usuario) en función del valor seleccionado o del formato que solicite la aplicación en el elemento AuthRequest de SAML.</span><span class="sxs-lookup"><span data-stu-id="7539c-274">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="7539c-275">Para más información, visite la sección NameIDPolicy del artículo [Protocolo SAML de inicio de sesión único](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest).</span><span class="sxs-lookup"><span data-stu-id="7539c-275">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>
   >
   >

9.  <span data-ttu-id="7539c-276">Para agregar atributos de usuario, haga clic en **Ver y editar todos los demás atributos de usuario** para editar los atributos que se enviarán a la aplicación en el token de SAML cuando el usuario inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-276">To add user attributes, click **View and edit all other user attributes** to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7539c-277">Para agregar un atributo:</span><span class="sxs-lookup"><span data-stu-id="7539c-277">To add an attribute:</span></span>

   <span data-ttu-id="7539c-278">1. Haga clic en **Agregar atributo**.</span><span class="sxs-lookup"><span data-stu-id="7539c-278">1.click **Add attribute**.</span></span> <span data-ttu-id="7539c-279">Escriba el **Nombre** y seleccione el **Valor** de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="7539c-279">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   <span data-ttu-id="7539c-280">2. Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-280">2 Click **Save.**</span></span> <span data-ttu-id="7539c-281">En la tabla verá el nuevo atributo.</span><span class="sxs-lookup"><span data-stu-id="7539c-281">You see the new attribute in the table.</span></span>

### <a name="download-the-azure-ad-metadata-or-certificate"></a><span data-ttu-id="7539c-282">Descarga del certificado o los metadatos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-282">Download the Azure AD metadata or certificate</span></span>

<span data-ttu-id="7539c-283">Para descargar el certificado o los metadatos de la aplicación de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-283">To download the application metadata or certificate from Azure AD, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-284">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **Administrador global** o **Coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-284">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-285">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-285">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-286">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-286">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-287">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-287">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-288">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-288">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7539c-289">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-289">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-290">Seleccione la aplicación para la que ha configurado el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-290">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="7539c-291">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-291">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-292">Vaya a la sección **Certificado de firma de SAML** y haga clic en el valor de la columna **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-292">Go to **SAML Signing Certificate** section, then click **Download** column value.</span></span> <span data-ttu-id="7539c-293">Según lo que necesite la aplicación para configurar el inicio de sesión único, verá la opción para descargar el archivo XML de metadatos o el certificado.</span><span class="sxs-lookup"><span data-stu-id="7539c-293">Depending on what the application requires configuring single sign-on, you see either the option to download the Metadata XML or the Certificate.</span></span>

    <span data-ttu-id="7539c-294">Azure AD no proporciona una dirección URL para obtener los metadatos.</span><span class="sxs-lookup"><span data-stu-id="7539c-294">Azure AD doesn’t provide a URL to get the metadata.</span></span> <span data-ttu-id="7539c-295">Solo se pueden recuperar como un archivo XML.</span><span class="sxs-lookup"><span data-stu-id="7539c-295">The metadata can only be retrieved as a XML file.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="7539c-296">Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-296">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="7539c-297">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-297">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="7539c-298">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-298">Add an application from the Azure AD gallery</span></span>](#add-an-application)

-   [<span data-ttu-id="7539c-299">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-299">Configure the application for password single sign-on</span></span>](#configure-the-application)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="7539c-300">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="7539c-300">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="7539c-301">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-301">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-302">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="7539c-302">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="7539c-303">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-303">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-304">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-304">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-305">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-305">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-306">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7539c-306">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="7539c-307">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-307">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="7539c-308">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-308">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="7539c-309">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="7539c-309">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="7539c-310">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-310">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="7539c-311">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-311">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="7539c-312">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-312">Configure the application for password single sign-on</span></span>

<span data-ttu-id="7539c-313">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-313">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-314">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-314">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-315">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-315">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-316">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-316">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-317">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-317">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-318">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-318">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="7539c-319">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-319">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-320">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="7539c-320">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="7539c-321">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-321">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-322">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7539c-322">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="7539c-323">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-323">Assign users to the application.</span></span>

10. <span data-ttu-id="7539c-324">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7539c-324">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="7539c-325">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="7539c-325">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="7539c-326">Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="7539c-326">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="7539c-327">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-327">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="7539c-328">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="7539c-328">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="7539c-329">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-329">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="7539c-330">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="7539c-330">Add a non-gallery application</span></span>

<span data-ttu-id="7539c-331">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-331">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-332">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="7539c-332">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="7539c-333">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-333">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-334">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-334">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-335">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-335">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-336">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7539c-336">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="7539c-337">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="7539c-337">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="7539c-338">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="7539c-338">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="7539c-339">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="7539c-339">Select **Add.**</span></span>

<span data-ttu-id="7539c-340">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-340">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="7539c-341">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="7539c-341">Configure the application for password single sign-on</span></span>

<span data-ttu-id="7539c-342">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7539c-342">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-343">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="7539c-343">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7539c-344">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-344">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-345">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-345">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-346">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-346">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-347">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-347">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="7539c-348">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-348">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-349">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="7539c-349">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7539c-350">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-350">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-351">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="7539c-351">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="7539c-352">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="7539c-352">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="7539c-353">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="7539c-353">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="7539c-354">Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7539c-354">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="7539c-355">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-355">Assign users to the application.</span></span>

11. <span data-ttu-id="7539c-356">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="7539c-356">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="7539c-357">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="7539c-357">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="7539c-358">Asignación de un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="7539c-358">How to assign a user to an application directly</span></span>

<span data-ttu-id="7539c-359">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="7539c-359">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="7539c-360">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="7539c-360">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7539c-361">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="7539c-361">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7539c-362">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7539c-362">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7539c-363">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7539c-363">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7539c-364">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7539c-364">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7539c-365">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="7539c-365">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7539c-366">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="7539c-366">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="7539c-367">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-367">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7539c-368">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7539c-368">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="7539c-369">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="7539c-369">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="7539c-370">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="7539c-370">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="7539c-371">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="7539c-371">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="7539c-372">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="7539c-372">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="7539c-373">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="7539c-373">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="7539c-374">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7539c-374">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="7539c-375">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="7539c-375">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="7539c-376">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="7539c-376">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="7539c-377">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="7539c-377">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="7539c-378">Si después de seguir estos pasos, el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="7539c-378">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="7539c-379">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="7539c-379">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="7539c-380">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="7539c-380">Correlation error ID</span></span>

-   <span data-ttu-id="7539c-381">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="7539c-381">UPN (user email address)</span></span>

-   <span data-ttu-id="7539c-382">TenantID</span><span class="sxs-lookup"><span data-stu-id="7539c-382">TenantID</span></span>

-   <span data-ttu-id="7539c-383">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="7539c-383">Browser type</span></span>

-   <span data-ttu-id="7539c-384">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="7539c-384">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="7539c-385">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="7539c-385">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="7539c-386">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7539c-386">Next steps</span></span>
[<span data-ttu-id="7539c-387">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="7539c-387">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

