---
title: "Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD | Microsoft Docs"
description: "Configuración de una aplicación para el inicio de sesión único con contraseña cuando ya figura en la galería de aplicaciones de Azure AD"
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
ms.openlocfilehash: d4dc110eb25c3e550ac4663d28e626a696b58f62
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="95125-103">Configuración del inicio de sesión único con contraseña para una aplicación de la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95125-103">How to configure password single sign-on for an Azure AD Gallery application</span></span>

<span data-ttu-id="95125-104">Cuando se agrega una aplicación desde la [galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), tiene la opción de elegir cómo desea que los usuarios inicien sesión en esa aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-104">When you add an application from the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), you have the choice of how you want your users to sign in to that application.</span></span> <span data-ttu-id="95125-105">Puede configurar esta opción en cualquier momento seleccionando el elemento de navegación **Inicio de sesión único** en una aplicación de empresa en [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95125-105">You can configure this choice at any time by selecting the **Single Sign-on** navigation item on an Enterprise Application in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="95125-106">Uno de los métodos de inicio de sesión único que tiene a su disposición es la opción de [inicio de sesión único con contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="95125-106">One of the single sign-on methods available to you is the [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) option.</span></span> <span data-ttu-id="95125-107">Representa una excelente manera de empezar a integrar aplicaciones en Azure AD rápidamente, y le permite lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="95125-107">This is a great way to get started integrating applications into Azure AD quickly, and allows you to:</span></span>

-   <span data-ttu-id="95125-108">Habilitar el **inicio de sesión único para los usuarios** almacenando y reproduciendo de forma segura los nombres de usuario y contraseñas para la aplicación que ha integrado con Azure AD</span><span class="sxs-lookup"><span data-stu-id="95125-108">Enable **Single Sign-on for your users** by securely storing and replaying usernames and passwords for the application you’ve integrated with Azure AD</span></span>

-   <span data-ttu-id="95125-109">**Admitir las aplicaciones que requieren varios campos de inicio de sesión** para aplicaciones que requieren más que solo los campos de nombre de usuario y contraseña para iniciar sesión</span><span class="sxs-lookup"><span data-stu-id="95125-109">**Support applications that require multiple sign-in fields** for applications that require more than just username and password fields to sign in</span></span>

-   <span data-ttu-id="95125-110">**Personalizar las etiquetas** de los campos de entrada de nombre de usuario y contraseña que los usuarios ven en el [panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) cuando escriben sus credenciales</span><span class="sxs-lookup"><span data-stu-id="95125-110">**Customize the labels** of the username and password input fields your users see on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) when they enter their credentials</span></span>

-   <span data-ttu-id="95125-111">Permitir a los **usuarios** proporcionar sus propios nombres de usuario y contraseñas para las cuentas de aplicación existentes que están escribiendo manualmente en el [panel de acceso de la aplicación](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span><span class="sxs-lookup"><span data-stu-id="95125-111">Allow your **users** to provide their own usernames and passwords for any existing application accounts they are typing in manually on the [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)</span></span>

-   <span data-ttu-id="95125-112">Permitir que un **miembro del grupo de negocios** especifique los nombres de usuario y contraseñas que se asignan a un usuario mediante el uso de la característica [Acceso de autoservicio a las aplicaciones](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access)</span><span class="sxs-lookup"><span data-stu-id="95125-112">Allow a **member of the business group** to specify the usernames and passwords assigned to a user by using the [Self-Service Application Access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) feature</span></span>

-   <span data-ttu-id="95125-113">Permitir que un **administrador** especifique los nombres de usuario y contraseñas que se asignan a un usuario mediante la característica Actualizar credenciales al [asignar un usuario a una aplicación](#assign-a-user-to-an-application-directly)</span><span class="sxs-lookup"><span data-stu-id="95125-113">Allow an **administrator** to specify the usernames and passwords assigned to a user by using the Update Credentials feature when [assigning a user to an application](#assign-a-user-to-an-application-directly)</span></span>

-   <span data-ttu-id="95125-114">Permitir que un **administrador** especifique el nombre de usuario o la contraseña compartidos que utilizan un grupo de personas mediante la característica Actualizar credenciales al [asignar un grupo a una aplicación](#assign-an-application-to-a-group-directly)</span><span class="sxs-lookup"><span data-stu-id="95125-114">Allow an **administrator** to specify the shared username or password used by a group of people by using the Update Credentials feature when [assigning a group to an application](#assign-an-application-to-a-group-directly)</span></span>

<span data-ttu-id="95125-115">A continuación se describe cómo habilitar [el inicio de sesión único con contraseña](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) en una aplicación que ya está en la [galería de aplicaciones de Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="95125-115">Below describes how you can enable [Password-Based Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) to an application that is already in the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).</span></span>

## <a name="overview-of-steps-required"></a><span data-ttu-id="95125-116">Información general sobre los pasos necesarios</span><span class="sxs-lookup"><span data-stu-id="95125-116">Overview of steps required</span></span>
<span data-ttu-id="95125-117">Para configurar una aplicación desde la galería de Azure AD, realice los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="95125-117">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="95125-118">Incorporación de una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95125-118">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-azure-ad-gallery)

-   [<span data-ttu-id="95125-119">Configurar la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="95125-119">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

-   [<span data-ttu-id="95125-120">Asignar la aplicación a un usuario o un grupo</span><span class="sxs-lookup"><span data-stu-id="95125-120">Assign the application to a user or a group</span></span>](#assign-the-application-to-a-user-or-a-group)

    -   [<span data-ttu-id="95125-121">Asignar un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="95125-121">Assign a user to an application directly</span></span>](#assign-a-user-to-an-application-directly)

    -   [<span data-ttu-id="95125-122">Asignar una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="95125-122">Assign an application to a group directly</span></span>](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="95125-123">Agregar una aplicación desde la galería de Azure AD</span><span class="sxs-lookup"><span data-stu-id="95125-123">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="95125-124">Para agregar una aplicación desde la galería de Azure AD, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95125-124">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="95125-125">Abra [Azure Portal](https://portal.azure.com) e inicie sesión como **administrador global** o **coadministrador**</span><span class="sxs-lookup"><span data-stu-id="95125-125">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**</span></span>

2.  <span data-ttu-id="95125-126">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="95125-126">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95125-127">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95125-127">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95125-128">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95125-128">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95125-129">Haga clic en el botón **Agregar** situado en la esquina superior derecha de la hoja **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="95125-129">click the **Add** button at the top-right corner on the **Enterprise Applications** blade</span></span>

6.  <span data-ttu-id="95125-130">En el cuadro de texto **Escriba un nombre** de la sección **Agregar desde la galería**, escriba el nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-130">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application</span></span>

7.  <span data-ttu-id="95125-131">Seleccione la aplicación que desea configurar para el inicio de sesión único.</span><span class="sxs-lookup"><span data-stu-id="95125-131">Select the application you want to configure for single sign-on</span></span>

8.  <span data-ttu-id="95125-132">Antes de agregar la aplicación, puede cambiar su nombre en el cuadro de texto **Nombre**.</span><span class="sxs-lookup"><span data-stu-id="95125-132">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="95125-133">Haga clic en el botón **Agregar** para agregar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-133">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="95125-134">Tras un breve período, podrá ver la hoja de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-134">After a short period, you be able to see the application’s configuration blade.</span></span>

## <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="95125-135">Configuración de la aplicación para el inicio de sesión único con contraseña</span><span class="sxs-lookup"><span data-stu-id="95125-135">Configure the application for password single sign-on</span></span>

<span data-ttu-id="95125-136">Para configurar el inicio de sesión único para una aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="95125-136">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="95125-137">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global** o **coadministrador**.</span><span class="sxs-lookup"><span data-stu-id="95125-137">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="95125-138">Abra la **extensión de Azure Active Directory** haciendo clic en **More services** (Más servicios) en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="95125-138">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95125-139">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95125-139">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95125-140">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95125-140">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95125-141">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="95125-141">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="95125-142">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="95125-142">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="95125-143">Seleccionar la aplicación que desea configurar para el inicio de sesión único</span><span class="sxs-lookup"><span data-stu-id="95125-143">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="95125-144">Cuando se cargue la aplicación, haga clic en **Inicio de sesión único** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-144">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95125-145">Seleccione el modo de **Inicio de sesión con contraseña**.</span><span class="sxs-lookup"><span data-stu-id="95125-145">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="95125-146">[Asigne usuarios a la aplicación](#assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="95125-146">[Assign users to the application](#assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="95125-147">Además, también puede proporcionar credenciales en nombre del usuario; para ello, seleccione las filas de los usuarios, haga clic en **Actualizar credenciales** y escriba el nombre de usuario y la contraseña en nombre de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="95125-147">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="95125-148">En caso contrario, se solicitará a los usuarios que especifiquen ellos mismos las credenciales al inicio.</span><span class="sxs-lookup"><span data-stu-id="95125-148">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="assign-a-user-to-an-application-directly"></a><span data-ttu-id="95125-149">Asignar un usuario a una aplicación directamente</span><span class="sxs-lookup"><span data-stu-id="95125-149">Assign a user to an application directly</span></span>

<span data-ttu-id="95125-150">Para asignar uno o varios usuarios a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95125-150">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="95125-151">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="95125-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95125-152">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="95125-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95125-153">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95125-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95125-154">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95125-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95125-155">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="95125-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="95125-156">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="95125-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="95125-157">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="95125-157">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="95125-158">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-158">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95125-159">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="95125-159">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="95125-160">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="95125-160">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="95125-161">Escriba el **nombre completo** o la **dirección de correo electrónico** del usuario al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="95125-161">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="95125-162">Mantenga el puntero sobre el **usuario** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="95125-162">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="95125-163">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del usuario para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="95125-163">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="95125-164">**Opcional:** si desea **agregar más de un usuario**, escriba otro **nombre completo** o **dirección de correo electrónico** en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="95125-164">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="95125-165">Cuando haya terminado de seleccionar usuarios, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-165">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="95125-166">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los usuarios que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="95125-166">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="95125-167">Haga clic en el botón **Asignar** para asignar la aplicación a los usuarios seleccionados.</span><span class="sxs-lookup"><span data-stu-id="95125-167">Click the **Assign** button to assign the application to the selected users.</span></span>

## <a name="assign-an-application-to-a-group-directly"></a><span data-ttu-id="95125-168">Asignar una aplicación a un grupo directamente</span><span class="sxs-lookup"><span data-stu-id="95125-168">Assign an application to a group directly</span></span>

<span data-ttu-id="95125-169">Para asignar uno o varios grupos a una aplicación directamente, siga los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="95125-169">To assign one or more groups to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="95125-170">Abra [**Azure Portal**](https://portal.azure.com/) e inicie sesión como **administrador global**.</span><span class="sxs-lookup"><span data-stu-id="95125-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="95125-171">Abra la **extensión de Azure Active Directory** haciendo clic en **Más servicios** en la parte inferior del menú de navegación izquierdo principal.</span><span class="sxs-lookup"><span data-stu-id="95125-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="95125-172">Escriba **"Azure Active Directory**" en el cuadro de búsqueda de filtrado y seleccione el elemento **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="95125-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="95125-173">Haga clic en **Aplicaciones empresariales** en el menú de navegación izquierdo de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="95125-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="95125-174">Haga clic en **Todas las aplicaciones** para ver una lista de todas las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="95125-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="95125-175">Si no ve la aplicación que desea que aparezca aquí, use el control **Filtro** de la parte superior de la lista **Todas las aplicaciones** y establezca la opción **Mostrar** en **Todas las aplicaciones.**</span><span class="sxs-lookup"><span data-stu-id="95125-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="95125-176">Seleccione la aplicación que desea asignar a un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="95125-176">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="95125-177">Cuando se cargue la aplicación, haga clic en **Usuarios y grupos** desde el menú de navegación izquierdo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-177">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="95125-178">Haga clic en el botón **Agregar** en la parte superior de la lista **Usuarios y grupos** para abrir la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="95125-178">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="95125-179">Haga clic en el selector **Usuarios y grupos** de la hoja **Agregar asignación**.</span><span class="sxs-lookup"><span data-stu-id="95125-179">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="95125-180">Escriba el **nombre completo** del grupo al que quiere asignar en el cuadro de búsqueda **Buscar por nombre o dirección de correo**.</span><span class="sxs-lookup"><span data-stu-id="95125-180">Type in the **full group name** of the group you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="95125-181">Mantenga el puntero sobre el **grupo** en la lista para que aparezca una **casilla**.</span><span class="sxs-lookup"><span data-stu-id="95125-181">Hover over the **group** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="95125-182">Haga clic en la casilla situada junto a la foto o el logotipo del perfil del grupo para agregar ese usuario a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="95125-182">Click the checkbox next to the group’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="95125-183">**Opcional**: si desea **agregar más de un grupo**, escriba otro **nombre de grupo completo** o en el cuadro de búsqueda **Buscar por nombre o dirección de correo** y haga clic en la casilla para agregar ese grupo a la lista de **seleccionados**.</span><span class="sxs-lookup"><span data-stu-id="95125-183">**Optional:** If you would like to **add more than one group**, type in another **full group name** into the **Search by name or email address** search box, and click the checkbox to add this group to the **Selected** list.</span></span>

13. <span data-ttu-id="95125-184">Cuando haya terminado de seleccionar grupos, haga clic en el botón **Seleccionar** para agregarlos a la lista de usuarios y grupos que se asignarán a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="95125-184">When you are finished selecting groups, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="95125-185">**Opcional:** haga clic en el selector **Seleccionar rol** de la hoja **Agregar asignación** para seleccionar un rol que se asignará a los grupos que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="95125-185">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the groups you have selected.</span></span>

15. <span data-ttu-id="95125-186">Haga clic en el botón **Asignar** para asignar la aplicación a los grupos seleccionados.</span><span class="sxs-lookup"><span data-stu-id="95125-186">Click the **Assign** button to assign the application to the selected groups.</span></span>

<span data-ttu-id="95125-187">Tras un breve período, los usuarios que seleccionó podrán iniciar estas aplicaciones en el panel de acceso.</span><span class="sxs-lookup"><span data-stu-id="95125-187">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95125-188">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="95125-188">Next steps</span></span>
[<span data-ttu-id="95125-189">Proporcionar un inicio de sesión único a las aplicaciones con el proxy de aplicación</span><span class="sxs-lookup"><span data-stu-id="95125-189">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
