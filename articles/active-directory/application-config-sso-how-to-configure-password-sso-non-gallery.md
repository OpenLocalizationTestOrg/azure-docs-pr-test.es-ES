---
title: "Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería | Microsoft Docs"
description: "Configuración de una aplicación personalizada ajena para el inicio de sesión único con contraseña cuando no aparece en la Galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: f629ec99824199306ebf825901beaa99d83d434d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="e650f-103">Configuración del inicio de sesión único con contraseña para una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="e650f-103">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="e650f-104">Además de las opciones que se encuentran en la Galería de aplicaciones de Azure AD, también puede agregar una **aplicación ajena a la galería** cuando la aplicación que desea no aparece ahí.</span><span class="sxs-lookup"><span data-stu-id="e650f-104">In addition to the choices found within the Azure AD Application Gallery, you also have the option to add a **non-gallery application** when the application you want is not listed there.</span></span> <span data-ttu-id="e650f-105">Con esta funcionalidad, puede agregar cualquier aplicación que ya exista en su organización, o bien cualquier aplicación de terceros que puedan usar desde un proveedor que aún no forme parte de la [Galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="e650f-105">Using this capability, you can add any application that already exists in your organization, or any third-party application that you might use from a vendor who is not already part of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

<span data-ttu-id="e650f-106">Una vez agregada una aplicación ajena a la galería, puede configurar el método de inicio de sesión único que usa esta aplicación seleccionando el elemento de navegación **Inicio de sesión único** en una aplicación de empresa en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e650f-106">Once you add a non-gallery application, you can then configure the Single sign-on method this application uses by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="e650f-107">Uno de los métodos de inicio de sesión único que tiene a su disposición es la opción [Inicio de sesión único basado en contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="e650f-107">One of the Single Sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="e650f-108">Con la experiencia de **agregar una aplicación ajena a la galería**, puede integrar cualquier aplicación que represente un nombre de usuario basado en HTML y el campo de contraseña de entrada, incluso si no está en nuestro conjunto de aplicaciones previamente integradas.</span><span class="sxs-lookup"><span data-stu-id="e650f-108">With the **add a non-gallery application** experience, you can integrate any application that renders an HTML-based username and password input field, even if it is not in our set of pre-integrated applications.</span></span>

<span data-ttu-id="e650f-109">El modo de funcionamiento es mediante una tecnología de barrido de páginas que forma parte de la extensión Access Panel que permiten la detección automática de los campos de entrada de nombre de usuario y contraseña, almacénelos de forma segura para la instancia de la aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="e650f-109">The way this works is by a page scraping technology that is part of the Access Panel extension that allows us to auto-detect username and password input fields, store them securely for your specific application instance.</span></span> <span data-ttu-id="e650f-110">A continuación, reproduzca de forma segura los nombres de usuario y contraseñas en esos campos cuando un usuario navegue a esa aplicación en el panel de acceso de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-110">Then securely replay usernames and passwords to those fields when a user navigates to that application on the application access panel.</span></span>

<span data-ttu-id="e650f-111">Representa una excelente manera de empezar a integrar cualquier tipo de aplicación en Azure AD rápidamente, y permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e650f-111">This is a great way to get started integrating any kind of application into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="e650f-112">Integrar **cualquier aplicación del mundo** con el inquilino de Azure AD, siempre y cuando represente un campo de entrada de usuario y contraseña HTML.</span><span class="sxs-lookup"><span data-stu-id="e650f-112">Integrate **any application in the world** with your Azure AD tenant, so long as it renders an HTML username and password input field</span></span>

-   <span data-ttu-id="e650f-113">Habilitar el **inicio de sesión único para los usuarios** almacenando y reproduciendo de forma segura los nombres de usuario y contraseñas para la aplicación que ha integrado con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e650f-113">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="e650f-114">**Detectar automáticamente los campos de entrada** de cualquier aplicación y detectarlos manualmente con la extensión del explorador Access Panel, en caso de que la detección automática no los encuentre.</span><span class="sxs-lookup"><span data-stu-id="e650f-114">**Auto-detect input** fields for any application and allow you to manually detect those fields using the Access Panel Browser Extension, in case auto-detection does not find them</span></span>

-   <span data-ttu-id="e650f-115">**Admitir aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que no solo requieren los campos de nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="e650f-115">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="e650f-116">**Personalizar las etiquetas** de los campos de entrada de nombre de usuario y contraseña que los usuarios ven en el [panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriben sus credenciales</span><span class="sxs-lookup"><span data-stu-id="e650f-116">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="e650f-117">Permitir a los **usuarios** proporcionar sus propios nombres de usuario y contraseñas para las cuentas de aplicación existentes que están escribiendo manualmente en el [panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="e650f-117">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="e650f-118">Permitir que un **miembro del grupo de negocios** especifique los nombres de usuario y contraseñas que se asignan a un usuario mediante el uso de la característica [Acceso de autoservicio a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="e650f-118">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="e650f-119">Permitir que un **administrador** especifique los nombres de usuario y contraseñas que se asignan a un usuario mediante la característica Actualizar credenciales al [asignar un usuario a una aplicación](#_How_to_configure_1)</span><span class="sxs-lookup"><span data-stu-id="e650f-119">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#_How_to_configure_1)</span></span>

-   <span data-ttu-id="e650f-120">Permitir que un **administrador** especifique el nombre de usuario o la contraseña compartidos que utilizan un grupo de personas mediante la característica Actualizar credenciales al [asignar un grupo a una aplicación](#assign-an-application-to-a-group-directly).</span><span class="sxs-lookup"><span data-stu-id="e650f-120">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="e650f-121">A continuación se describe cómo habilitar el [inicio de sesión único con contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) en una aplicación que agregue mediante la experiencia de **agregar una aplicación ajena a la galería**.</span><span class="sxs-lookup"><span data-stu-id="e650f-121">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to any application that you add using the **add a non-gallery application** experience.</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="e650f-122">Información general sobre los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="e650f-122">Overview of steps required</span></span>

<span data-ttu-id="e650f-123">Para configurar una aplicación desde la galería de Azure AD, necesita seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e650f-123">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="e650f-124">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="e650f-124">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="e650f-125">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="e650f-125">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="e650f-126">Asignar la aplicación a un usuario o un grupo</span><span class="sxs-lookup"><span data-stu-id="e650f-126">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="e650f-127">Asignar un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="e650f-127">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="e650f-128">Asignación de una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="e650f-128">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-a-non-gallery-application"></a><span data-ttu-id="e650f-129">Incorporación de una aplicación ajena a la galería</span><span class="sxs-lookup"><span data-stu-id="e650f-129">Add a non-gallery application</span></span>

<span data-ttu-id="e650f-130">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e650f-130">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="e650f-131">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="e650f-131">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="e650f-132">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e650f-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e650f-133">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e650f-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e650f-134">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e650f-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e650f-135">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="e650f-135">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="e650f-136">Haga clic en **Aplicación situada fuera de la galería**.</span><span class="sxs-lookup"><span data-stu-id="e650f-136">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="e650f-137">Escriba el nombre de la aplicación en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="e650f-137">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="e650f-138">Seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="e650f-138">Select **Add.**</span></span>

<span data-ttu-id="e650f-139">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-139">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="e650f-140">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="e650f-140">Configure the application for password single sign-on</span></span>

<span data-ttu-id="e650f-141">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="e650f-141">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="e650f-142">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="e650f-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="e650f-143">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e650f-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e650f-144">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e650f-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e650f-145">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e650f-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e650f-146">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e650f-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e650f-147">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e650f-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e650f-148">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="e650f-148">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="e650f-149">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-149">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e650f-150">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="e650f-150">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="e650f-151">Escriba la **dirección URL de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e650f-151">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="e650f-152">Es la dirección URL en la que los usuarios escriben su nombre de usuario y contraseña para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="e650f-152">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="e650f-153">Asegúrese de que los campos de inicio de sesión estén visibles en la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="e650f-153">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="e650f-154">Asigne usuarios a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-154">Assign users to the application.</span></span>

11. <span data-ttu-id="e650f-155">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="e650f-155">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="e650f-156">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="e650f-156">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="e650f-157">Asignar un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="e650f-157">Assign a user to an application directly</span></span>

<span data-ttu-id="e650f-158">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e650f-158">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="e650f-159">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="e650f-159">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e650f-160">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e650f-160">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e650f-161">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e650f-161">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e650f-162">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e650f-162">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e650f-163">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e650f-163">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e650f-164">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e650f-164">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e650f-165">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="e650f-165">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="e650f-166">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-166">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e650f-167">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e650f-167">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e650f-168">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e650f-168">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e650f-169">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="e650f-169">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e650f-170">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="e650f-170">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="e650f-171">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="e650f-171">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="e650f-172">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="e650f-172">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="e650f-173">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-173">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="e650f-174">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="e650f-174">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="e650f-175">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e650f-175">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="e650f-176">Asignar una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="e650f-176">Assign an application to a group directly</span></span>

<span data-ttu-id="e650f-177">Para asignar uno o varios grupos a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e650f-177">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="e650f-178">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="e650f-178">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e650f-179">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="e650f-179">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e650f-180">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e650f-180">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e650f-181">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e650f-181">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e650f-182">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e650f-182">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="e650f-183">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="e650f-183">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="e650f-184">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="e650f-184">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="e650f-185">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-185">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="e650f-186">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e650f-186">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="e650f-187">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="e650f-187">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="e650f-188">Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="e650f-188">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="e650f-189">Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="e650f-189">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="e650f-190">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="e650f-190">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="e650f-191">**Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="e650f-191">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="e650f-192">Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="e650f-192">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="e650f-193">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="e650f-193">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="e650f-194">Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="e650f-194">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="e650f-195">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="e650f-195">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e650f-196">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e650f-196">Next steps</span></span>
[<span data-ttu-id="e650f-197">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="e650f-197">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
