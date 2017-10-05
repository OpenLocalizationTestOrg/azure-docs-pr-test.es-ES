---
title: "Problemas al iniciar sesión en una aplicación de la galería de Azure AD configurada para inicio de sesión único | Microsoft Docs"
description: "Describe áreas problemáticas que proporcionan instrucciones para solucionar problemas relacionados con el inicio de sesión en aplicaciones de la galería de Azure AD configuradas para inicio de sesión único con contraseña"
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
ms.openlocfilehash: c90b61812affb7e7af05cf3e302d045958da59be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="problems-signing-in-to-an-azure-ad-gallery-application-configured-for-password-single-sign-on"></a><span data-ttu-id="71044-103">Problemas al iniciar sesión en una aplicación de la galería de Azure AD configurada para inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="71044-103">Problems signing in to an Azure AD Gallery application configured for password single sign-on</span></span>

<span data-ttu-id="71044-104">El Panel de acceso es un portal basado en web que permite que un usuario con una cuenta profesional o educativa en Azure Active Directory (Azure AD) vea e inicie aplicaciones basadas en la nube a las que el administrador de Azure AD le ha concedido acceso.</span><span class="sxs-lookup"><span data-stu-id="71044-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="71044-105">Un usuario que posee ediciones de Azure AD también puede usar las funcionalidades de administración de grupos de autoservicio y aplicaciones a través del Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="71044-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="71044-106">El Panel de acceso es independiente de Azure Portal y no requiere que los usuarios tengan una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="71044-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="71044-107">Para usar el inicio de sesión único (SSO) basado en contraseña en el Panel de acceso, se debe instalar la extensión del Panel de acceso en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="71044-107">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="71044-108">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="71044-108">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="71044-109">Cumplimiento de los requisitos del explorador para el Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="71044-109">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="71044-110">El Panel de acceso requiere un explorador compatible con JavaScript y que tenga habilitado CSS.</span><span class="sxs-lookup"><span data-stu-id="71044-110">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="71044-111">Para usar el inicio de sesión único (SSO) basado en contraseña en el Panel de acceso, se debe instalar la extensión del Panel de acceso en el explorador del usuario.</span><span class="sxs-lookup"><span data-stu-id="71044-111">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="71044-112">Esta extensión se descarga automáticamente cuando un usuario selecciona una aplicación que está configurada para SSO basado en contraseña.</span><span class="sxs-lookup"><span data-stu-id="71044-112">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="71044-113">Para el SSO basado en contraseña, los exploradores del usuario final pueden ser:</span><span class="sxs-lookup"><span data-stu-id="71044-113">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="71044-114">Internet Explorer 8, 9, 10, 11 (en Windows 7 o posterior)</span><span class="sxs-lookup"><span data-stu-id="71044-114">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="71044-115">Chrome (en Windows 7 o posterior y en Mac OS X o posterior)</span><span class="sxs-lookup"><span data-stu-id="71044-115">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="71044-116">Firefox 26.0 o posterior (en Windows XP SP2 o posterior y en Mac OS X 10.6 o posterior)</span><span class="sxs-lookup"><span data-stu-id="71044-116">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>

>[!NOTE]
><span data-ttu-id="71044-117">La extensión de SSO basada en contraseña está disponible para Edge en Windows 10 cuando se admiten extensiones de explorador para Edge.</span><span class="sxs-lookup"><span data-stu-id="71044-117">The password-based SSO extension become available for Edge in Windows 10 when browser extensions become supported for Edge.</span></span>
>
>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="71044-118">Cómo instalar la extensión de explorador del Panel de acceso</span><span class="sxs-lookup"><span data-stu-id="71044-118">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="71044-119">Para instalar la extensión de explorador del Panel de acceso, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="71044-119">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="71044-120">Abra el [Panel de acceso](https://myapps.microsoft.com) en uno de los exploradores admitidos e inicie sesión como **usuario** en su instancia de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71044-120">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="71044-121">Haga clic en una **aplicación de SSO con contraseña** en el Panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="71044-121">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="71044-122">En el mensaje que le pregunta si desea instalar el software, seleccione **Instalar ahora**.</span><span class="sxs-lookup"><span data-stu-id="71044-122">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="71044-123">Se le dirigirá al vínculo de descarga en función del explorador.</span><span class="sxs-lookup"><span data-stu-id="71044-123">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="71044-124">**Agregue** la extensión al explorador.</span><span class="sxs-lookup"><span data-stu-id="71044-124">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="71044-125">Si el explorador lo solicita, seleccione **Habilitar** o **Permitir** la extensión.</span><span class="sxs-lookup"><span data-stu-id="71044-125">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="71044-126">Una vez instalada, **reinicie** la sesión del explorador.</span><span class="sxs-lookup"><span data-stu-id="71044-126">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="71044-127">Inicie sesión en el Panel de acceso y vea si puede **iniciar** las aplicaciones de SSO con contraseña</span><span class="sxs-lookup"><span data-stu-id="71044-127">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="71044-128">También puede descargar la extensión para Chrome y Firefox desde los siguientes vínculos directos:</span><span class="sxs-lookup"><span data-stu-id="71044-128">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="71044-129">Extensión del Panel de acceso para Chrome</span><span class="sxs-lookup"><span data-stu-id="71044-129">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="71044-130">Extensión del Panel de acceso para Firefox</span><span class="sxs-lookup"><span data-stu-id="71044-130">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="setting-up-a-group-policy-for-internet-explorer"></a><span data-ttu-id="71044-131">Configuración de una directiva de grupo para Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="71044-131">Setting up a group policy for Internet Explorer</span></span>

<span data-ttu-id="71044-132">Puede configurar una directiva de grupo que le permita instalar de forma remota la extensión del Panel de acceso para Internet Explorer en las máquinas de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="71044-132">You can setup a group policy that allow you to remotely install the Access Panel extension for Internet Explorer on your users' machines.</span></span>

<span data-ttu-id="71044-133">Los requisitos previos son:</span><span class="sxs-lookup"><span data-stu-id="71044-133">The prerequisites include:</span></span>

-   <span data-ttu-id="71044-134">Configuró [Servicios de dominio de Active Directory](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx)y unió los equipos de los usuarios a su dominio.</span><span class="sxs-lookup"><span data-stu-id="71044-134">You have set up [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), and you have joined your users' machines to your domain.</span></span>

-   <span data-ttu-id="71044-135">Debe tener el permiso "Editar configuración" para editar el objeto de directiva de grupo (GPO).</span><span class="sxs-lookup"><span data-stu-id="71044-135">You must have the "Edit settings" permission to edit the Group Policy Object (GPO).</span></span> <span data-ttu-id="71044-136">De forma predeterminada, los miembros de los siguientes grupos de seguridad poseen este permiso: Administradores de dominio, Administradores de organización y Propietarios del creador de directivas de grupo.</span><span class="sxs-lookup"><span data-stu-id="71044-136">By default, members of the following security groups have this permission: Domain Administrators, Enterprise Administrators, and Group Policy Creator Owners.</span></span> <span data-ttu-id="71044-137">[Más información](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="71044-137">[Learn more](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx).</span></span>

<span data-ttu-id="71044-138">Siga el tutorial [Implementación de la extensión de panel de acceso para Internet Explorer mediante la directiva de grupo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) para obtener instrucciones paso a paso sobre cómo configurar la directiva de grupo e implementarla en los usuarios.</span><span class="sxs-lookup"><span data-stu-id="71044-138">Follow the tutorial [How to Deploy the Access Panel Extension for Internet Explorer using Group Policy](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-group-policy) for step by step instructions on how to configure the group policy and deploy it to users.</span></span>

## <a name="troubleshoot-the-access-panel-in-internet-explorer"></a><span data-ttu-id="71044-139">Solución de problemas del Panel de acceso en Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="71044-139">Troubleshoot the Access Panel in Internet Explorer</span></span>

<span data-ttu-id="71044-140">Siga la guía de [Solución de problemas de la extensión del Panel de acceso para Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) para acceder a la herramienta de diagnóstico, junto con instrucciones paso a paso sobre cómo configurar la extensión para IE.</span><span class="sxs-lookup"><span data-stu-id="71044-140">Follow the [Troubleshoot the Access Panel Extension for Internet Explorer](https://docs.microsoft.com/azure/active-directory/active-directory-saas-ie-Troubleshoot) guide for access a diagnostics tool and step by step instructions on configuring the extension for IE.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="71044-141">Cómo configurar el inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="71044-141">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="71044-142">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="71044-142">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="71044-143">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="71044-143">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="71044-144">Configurar la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="71044-144">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="71044-145">Asignar usuarios a la aplicación</span><span class="sxs-lookup"><span data-stu-id="71044-145">Assign users to the application</span></span>](#assign-users-to-the-application)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="71044-146">Incorporar una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="71044-146">Add a non-gallery application</span></span>

<span data-ttu-id="71044-147">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="71044-147">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="71044-148">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="71044-148">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="71044-149">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="71044-149">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="71044-150">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71044-150">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="71044-151">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71044-151">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="71044-152">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="71044-152">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="71044-153">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="71044-153">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="71044-154">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="71044-154">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="71044-155">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="71044-155">Select **Add.**</span></span>

<span data-ttu-id="71044-156">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71044-156">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="71044-157">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="71044-157">Configure the application for password single sign-on</span></span>

<span data-ttu-id="71044-158">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="71044-158">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="71044-159">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="71044-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="71044-160">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="71044-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="71044-161">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71044-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="71044-162">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71044-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="71044-163">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71044-163">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="71044-164">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="71044-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="71044-165">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="71044-165">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="71044-166">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71044-166">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="71044-167">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="71044-167">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="71044-168">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="71044-168">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="71044-169">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="71044-169">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="71044-170">Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="71044-170">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="71044-171">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71044-171">Assign users to the application.</span></span>

11. <span data-ttu-id="71044-172">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="71044-172">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="71044-173">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="71044-173">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

### <a name="assign-users-to-the-application"></a><span data-ttu-id="71044-174">Asignar usuarios a la aplicación</span><span class="sxs-lookup"><span data-stu-id="71044-174">Assign users to the application</span></span>

<span data-ttu-id="71044-175">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="71044-175">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="71044-176">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="71044-176">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="71044-177">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="71044-177">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="71044-178">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71044-178">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="71044-179">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71044-179">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="71044-180">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="71044-180">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="71044-181">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="71044-181">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="71044-182">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="71044-182">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="71044-183">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71044-183">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="71044-184">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="71044-184">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="71044-185">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="71044-185">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="71044-186">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="71044-186">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="71044-187">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="71044-187">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="71044-188">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="71044-188">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="71044-189">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="71044-189">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="71044-190">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="71044-190">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="71044-191">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="71044-191">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="71044-192">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="71044-192">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="71044-193">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="71044-193">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="71044-194">Si después de seguir estos pasos, el problema no se ha resuelto,</span><span class="sxs-lookup"><span data-stu-id="71044-194">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="71044-195">abra una incidencia de soporte técnico con la información siguiente si está disponible:</span><span class="sxs-lookup"><span data-stu-id="71044-195">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="71044-196">Id. de error de correlación</span><span class="sxs-lookup"><span data-stu-id="71044-196">Correlation error ID</span></span>

-   <span data-ttu-id="71044-197">UPN (dirección de correo electrónico del usuario)</span><span class="sxs-lookup"><span data-stu-id="71044-197">UPN (user email address)</span></span>

-   <span data-ttu-id="71044-198">TenantID</span><span class="sxs-lookup"><span data-stu-id="71044-198">TenantID</span></span>

-   <span data-ttu-id="71044-199">Tipo de explorador</span><span class="sxs-lookup"><span data-stu-id="71044-199">Browser type</span></span>

-   <span data-ttu-id="71044-200">Zona horaria y hora/período de tiempo durante el que se produce el error</span><span class="sxs-lookup"><span data-stu-id="71044-200">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="71044-201">Seguimientos de Fiddler</span><span class="sxs-lookup"><span data-stu-id="71044-201">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="71044-202">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="71044-202">Next steps</span></span>
[<span data-ttu-id="71044-203">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="71044-203">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

