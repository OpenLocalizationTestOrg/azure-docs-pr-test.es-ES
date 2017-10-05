---
title: "Incorporación de nuevos usuarios en Azure Active Directory | Microsoft Docs"
description: "Explica cómo agregar nuevos usuarios o cambiar la información del usuario en Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="1eb54-103">Incorporación de nuevos usuarios o de usuarios con cuentas de Microsoft en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eb54-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="1eb54-104">Agregue usuarios para rellenar su directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-104">Add users to populate your directory.</span></span> <span data-ttu-id="1eb54-105">Este artículo explica cómo agregar nuevos usuarios a su organización y cómo agregar a aquellos usuarios que tienen cuentas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1eb54-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="1eb54-106">Para más información sobre cómo agregar usuarios de otros directorios en Azure Active Directory o cómo agregar usuarios de empresas asociadas, consulte [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="1eb54-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="1eb54-107">De forma predeterminada, los usuarios agregados no tienen permisos de administrador, pero puede asignárselos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="1eb54-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1eb54-108">Microsoft recomienda administrar Azure AD con el [Centro de administración de Azure AD](https://aad.portal.azure.com) en Azure Portal en lugar de usar el portal de Azure clásico al que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1eb54-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="1eb54-109">Para agregar un usuario en el centro de administración de Azure AD, consulte [Adición de nuevos usuarios a Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1eb54-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="1eb54-110">Adición de un usuario</span><span class="sxs-lookup"><span data-stu-id="1eb54-110">Add a user</span></span>
1. <span data-ttu-id="1eb54-111">Inicie sesión en el [Portal de Azure clásico](https://manage.windowsazure.com) con una cuenta que sea administrador global para el directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1eb54-112">Haga clic en **Active Directory**y seleccione el nombre del directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="1eb54-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="1eb54-113">Seleccione la pestaña **Usuarios** y, después, en la barra de comandos, seleccione **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="1eb54-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="1eb54-114">En la página **Proporcione información sobre este usuario**, elija una de estas opciones en **Tipo de usuario**:</span><span class="sxs-lookup"><span data-stu-id="1eb54-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="1eb54-115">**Nuevo usuario de la organización** : agrega una nueva cuenta de usuario al directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="1eb54-116">**Usuario con una cuenta de Microsoft existente** : agrega una cuenta de consumidor de Microsoft existente a su directorio (por ejemplo, una cuenta de Outlook).</span><span class="sxs-lookup"><span data-stu-id="1eb54-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="1eb54-117">En función del **tipo de usuario**, escriba un nombre de usuario (para un nuevo usuario) o una dirección de correo electrónico (para un usuario con una cuenta de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1eb54-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="1eb54-118">En la página **Perfiles** del usuario, especifique el nombre, los apellidos y un nombre descriptivo, así como un rol de usuario en la lista **Roles**.</span><span class="sxs-lookup"><span data-stu-id="1eb54-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="1eb54-119">Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="1eb54-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="1eb54-120">Especifique si se debe **habilitar Multi-Factor Authentication** para el usuario.</span><span class="sxs-lookup"><span data-stu-id="1eb54-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="1eb54-121">En la página **Obtener contraseña temporal**, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1eb54-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1eb54-122">Si su organización usa más de un dominio, debe tener en cuenta los siguientes problemas al agregar una cuenta de usuario:</span><span class="sxs-lookup"><span data-stu-id="1eb54-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="1eb54-123">Para agregar cuentas de usuario con el mismo nombre principal de usuario (UPN) en todos los dominios, agregue **primero**, por ejemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido de** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1eb54-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="1eb54-124">**No** agregue geoffgrisso@contoso.com antes de geoffgrisso@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1eb54-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="1eb54-125">Este orden es importante y puede ser complicado de deshacer.</span><span class="sxs-lookup"><span data-stu-id="1eb54-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="1eb54-126">Cambiar la información de usuario</span><span class="sxs-lookup"><span data-stu-id="1eb54-126">Change user information</span></span>
<span data-ttu-id="1eb54-127">Puede cambiar los atributos de usuario, excepto el id. objeto.</span><span class="sxs-lookup"><span data-stu-id="1eb54-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="1eb54-128">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-128">Open your directory.</span></span>
2. <span data-ttu-id="1eb54-129">Seleccione la pestaña **Usuarios** y, después, el nombre para mostrar del usuario que quiere cambiar.</span><span class="sxs-lookup"><span data-stu-id="1eb54-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="1eb54-130">Termine los cambios y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1eb54-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="1eb54-131">Si el usuario que está intentando cambiar está sincronizado con el servicio de Active Directory local, no puede cambiar la información del usuario mediante este procedimiento.</span><span class="sxs-lookup"><span data-stu-id="1eb54-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="1eb54-132">Para cambiar el usuario, utilice las herramientas de administración locales de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eb54-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="1eb54-133">Limitaciones y administración de usuarios invitados</span><span class="sxs-lookup"><span data-stu-id="1eb54-133">Guest user management and limitations</span></span>
<span data-ttu-id="1eb54-134">Las cuentas de invitado son usuarios de otros directorios que se invitaron a su directorio para que tuvieran acceso a documentos de SharePoint, aplicaciones u otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb54-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="1eb54-135">Una cuenta de invitado en su directorio tiene el atributo UserType establecido en "Guest" (Invitado).</span><span class="sxs-lookup"><span data-stu-id="1eb54-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="1eb54-136">Los usuarios normales (específicamente, los miembros del directorio) tienen el valor de UserType "Miembro".</span><span class="sxs-lookup"><span data-stu-id="1eb54-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="1eb54-137">Los invitados tienen un conjunto limitado de derechos en el directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="1eb54-138">Estos derechos limitan la capacidad de los invitados para obtener información acerca de otros usuarios en el directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="1eb54-139">Sin embargo, los usuarios invitados todavía pueden interactuar con los usuarios y los grupos asociados a los recursos en los que trabajan.</span><span class="sxs-lookup"><span data-stu-id="1eb54-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="1eb54-140">Los usuarios invitados pueden:</span><span class="sxs-lookup"><span data-stu-id="1eb54-140">Guest users can:</span></span>

* <span data-ttu-id="1eb54-141">Ver otros usuarios y grupos asociados a una suscripción de Azure a la que están asignados</span><span class="sxs-lookup"><span data-stu-id="1eb54-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="1eb54-142">Ver los miembros de grupos a los que pertenecen</span><span class="sxs-lookup"><span data-stu-id="1eb54-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="1eb54-143">Buscar otros usuarios en el directorio, si conocen su dirección de correo electrónico completa</span><span class="sxs-lookup"><span data-stu-id="1eb54-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="1eb54-144">Ver solo un conjunto limitado de atributos de los usuarios que buscan: el nombre para mostrar, la dirección de correo electrónico, el nombre principal de usuario (UPN) y la foto en miniatura.</span><span class="sxs-lookup"><span data-stu-id="1eb54-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="1eb54-145">Obtención de una lista de los dominios verificados del directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="1eb54-146">Dar su consentimiento a aplicaciones, concediéndoles el mismo acceso que tienen los miembros en su directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="1eb54-147">Establecimiento de las directivas de acceso del usuario invitado</span><span class="sxs-lookup"><span data-stu-id="1eb54-147">Set guest user access policies</span></span>
<span data-ttu-id="1eb54-148">La pestaña **Configurar** de un directorio incluye opciones para controlar el acceso de los usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="1eb54-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="1eb54-149">Un administrador global de directorios solo puede cambiar estas opciones en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="1eb54-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="1eb54-150">Actualmente no hay ningún método de PowerShell o de API.</span><span class="sxs-lookup"><span data-stu-id="1eb54-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="1eb54-151">Para abrir la pestaña **Configurar** del Portal de Azure clásico, seleccione **Active Directory** y luego el nombre del directorio.</span><span class="sxs-lookup"><span data-stu-id="1eb54-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Configuración de Azure Active Directory][1]

<span data-ttu-id="1eb54-153">A continuación, puede editar las opciones para controlar el acceso de usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="1eb54-153">Then you can edit the options to control access for guest users.</span></span>

![opciones de control de acceso para usuarios invitados][2]

## <a name="whats-next"></a><span data-ttu-id="1eb54-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1eb54-155">What's next</span></span>
* [<span data-ttu-id="1eb54-156">Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eb54-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="1eb54-157">Administración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb54-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="1eb54-158">Administración de contraseñas en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb54-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="1eb54-159">Administración de grupos en Azure AD</span><span class="sxs-lookup"><span data-stu-id="1eb54-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
