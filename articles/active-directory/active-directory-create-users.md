---
title: aaaAdd nuevos usuarios tooAzure Active Directory | Documentos de Microsoft
description: "Explica cómo tooadd nuevos usuarios o cambiar la información de usuario en Azure Active Directory."
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
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="16176-103">Agregar nuevos usuarios o los usuarios con tooAzure de cuentas de Microsoft Active Directory</span><span class="sxs-lookup"><span data-stu-id="16176-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="16176-104">Agregue los usuarios toopopulate en el directorio.</span><span class="sxs-lookup"><span data-stu-id="16176-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="16176-105">Este artículo se explica cómo tooadd nuevos usuarios de su organización y cómo los usuarios de tooadd que tienen cuentas de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="16176-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="16176-106">Para más información sobre cómo agregar usuarios de otros directorios en Azure Active Directory o cómo agregar usuarios de empresas asociadas, consulte [Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="16176-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="16176-107">Usuarios agregados no tienen permisos de administrador de forma predeterminada, pero puede asignar roles toothem en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="16176-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16176-108">Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo.</span><span class="sxs-lookup"><span data-stu-id="16176-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="16176-109">Para tooadd un usuario en el centro de administración de hello Azure AD, vea [agregar nuevos usuarios tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16176-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="16176-110">Adición de un usuario</span><span class="sxs-lookup"><span data-stu-id="16176-110">Add a user</span></span>
1. <span data-ttu-id="16176-111">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="16176-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="16176-112">Seleccione **Active Directory**y, a continuación, seleccione nombre de hello del directorio de su organización.</span><span class="sxs-lookup"><span data-stu-id="16176-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="16176-113">Seleccione hello **usuarios** ficha y, a continuación, en la barra de comandos de hello, seleccione **Agregar usuario**.</span><span class="sxs-lookup"><span data-stu-id="16176-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="16176-114">En hello **envíenos comentarios acerca de este usuario** página, en **tipo de usuario**, seleccione:</span><span class="sxs-lookup"><span data-stu-id="16176-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="16176-115">**Nuevo usuario de la organización** : agrega una nueva cuenta de usuario al directorio.</span><span class="sxs-lookup"><span data-stu-id="16176-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="16176-116">**Usuario con una cuenta Microsoft existente** : agrega un directorio de tooyour de cuenta de consumidor de Microsoft existente (por ejemplo, una cuenta de Outlook)</span><span class="sxs-lookup"><span data-stu-id="16176-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="16176-117">En función del **tipo de usuario**, escriba un nombre de usuario (para un nuevo usuario) o una dirección de correo electrónico (para un usuario con una cuenta de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="16176-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="16176-118">En el usuario de hello **perfil** , proporcione un nombre y apellido, un nombre descriptivo y un rol de usuario de hello **Roles** lista.</span><span class="sxs-lookup"><span data-stu-id="16176-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="16176-119">Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="16176-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="16176-120">Especifique si demasiado**habilitar la autenticación multifactor** para el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="16176-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="16176-121">En hello **obtener contraseña temporal** página, seleccione **crear**.</span><span class="sxs-lookup"><span data-stu-id="16176-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16176-122">Si su organización usa más de un dominio, debe conocer Hola problemas siguientes cuando se agrega una cuenta de usuario:</span><span class="sxs-lookup"><span data-stu-id="16176-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="16176-123">cuentas de usuario de tooadd con Hola mismo nombre principal de usuario (UPN) entre dominios, **primer** agregar, por ejemplo, geoffgrisso@contoso.onmicrosoft.com, **seguido** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="16176-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="16176-124">**No** agregue geoffgrisso@contoso.com antes de geoffgrisso@contoso.onmicrosoft.com. Este orden es importante y puede ser tooundo complicada.</span><span class="sxs-lookup"><span data-stu-id="16176-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="16176-125">Cambiar la información de usuario</span><span class="sxs-lookup"><span data-stu-id="16176-125">Change user information</span></span>
<span data-ttu-id="16176-126">Puede cambiar cualquier atributo de usuario excepto Hola Id. de objeto.</span><span class="sxs-lookup"><span data-stu-id="16176-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="16176-127">Abra el directorio.</span><span class="sxs-lookup"><span data-stu-id="16176-127">Open your directory.</span></span>
2. <span data-ttu-id="16176-128">Seleccione hello **usuarios** ficha y nombre para mostrar, a continuación, seleccione Hola de Hola usuario desea toochange.</span><span class="sxs-lookup"><span data-stu-id="16176-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="16176-129">Termine los cambios y, a continuación, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="16176-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="16176-130">Si el usuario de Hola que va a cambiar está sincronizado con los servicios de Active Directory local, no se puede cambiar la información de usuario de hello mediante este procedimiento.</span><span class="sxs-lookup"><span data-stu-id="16176-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="16176-131">usuario de hello toochange, usar las herramientas de administración de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="16176-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="16176-132">Limitaciones y administración de usuarios invitados</span><span class="sxs-lookup"><span data-stu-id="16176-132">Guest user management and limitations</span></span>
<span data-ttu-id="16176-133">Las cuentas de invitado son usuarios de otros directorios que eran tooyour invitados directorio tooaccess los documentos de SharePoint, aplicaciones u otros recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="16176-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="16176-134">Una cuenta de invitado en el directorio tiene el atributo de UserType subyacente establecido demasiado "Invitado".</span><span class="sxs-lookup"><span data-stu-id="16176-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="16176-135">Los usuarios normales (específicamente, los miembros del directorio) tienen el atributo de UserType de Hola "Member".</span><span class="sxs-lookup"><span data-stu-id="16176-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="16176-136">Los invitados tienen un conjunto limitado de derechos en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="16176-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="16176-137">Estos derechos limitan la capacidad de Hola para obtener información de toodiscover invitados acerca de otros usuarios en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="16176-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="16176-138">Sin embargo, los usuarios invitados todavía pueden interactuar con hello usuarios y grupos asociados con los recursos de hello trabajan en.</span><span class="sxs-lookup"><span data-stu-id="16176-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="16176-139">Los usuarios invitados pueden:</span><span class="sxs-lookup"><span data-stu-id="16176-139">Guest users can:</span></span>

* <span data-ttu-id="16176-140">Ver otros usuarios y grupos asociados con un toowhich de suscripción de Azure que están asignados</span><span class="sxs-lookup"><span data-stu-id="16176-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="16176-141">Ver a miembros de Hola de toowhich de grupos que pertenecen</span><span class="sxs-lookup"><span data-stu-id="16176-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="16176-142">Buscar otros usuarios en el directorio de hello, si saben dirección de correo electrónico completa de hello del usuario de Hola</span><span class="sxs-lookup"><span data-stu-id="16176-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="16176-143">Ver solo un conjunto limitado de atributos de usuarios de Hola que buscan--toodisplay limitado nombre, dirección de correo electrónico, nombre principal de usuario (UPN) y foto en miniatura</span><span class="sxs-lookup"><span data-stu-id="16176-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="16176-144">Obtener una lista de dominios comprobados en directorio Hola</span><span class="sxs-lookup"><span data-stu-id="16176-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="16176-145">Tooapplications de consentimiento, concediéndoles Hola mismo acceso que tienen miembros en el directorio</span><span class="sxs-lookup"><span data-stu-id="16176-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="16176-146">Establecimiento de las directivas de acceso del usuario invitado</span><span class="sxs-lookup"><span data-stu-id="16176-146">Set guest user access policies</span></span>
<span data-ttu-id="16176-147">Hola **configurar** ficha de un directorio incluye opciones toocontrol acceso para usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="16176-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="16176-148">Un administrador global de directorios solo puede cambiar estas opciones en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="16176-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="16176-149">Actualmente no hay ningún método de PowerShell o de API.</span><span class="sxs-lookup"><span data-stu-id="16176-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="16176-150">Hola tooopen **configurar** ficha hello Azure seleccione portal, clásico **Active Directory**y, a continuación, seleccione nombre de hello del directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="16176-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![Configuración de Azure Active Directory][1]

<span data-ttu-id="16176-152">A continuación, puede editar el acceso de toocontrol de opciones de Hola para usuarios invitados.</span><span class="sxs-lookup"><span data-stu-id="16176-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![opciones de control de acceso para usuarios invitados][2]

## <a name="whats-next"></a><span data-ttu-id="16176-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16176-154">What's next</span></span>
* [<span data-ttu-id="16176-155">Incorporación de usuarios de otros directorios o compañías asociadas en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16176-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="16176-156">Administración de Azure AD</span><span class="sxs-lookup"><span data-stu-id="16176-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="16176-157">Administración de contraseñas en Azure AD</span><span class="sxs-lookup"><span data-stu-id="16176-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="16176-158">Administración de grupos en Azure AD</span><span class="sxs-lookup"><span data-stu-id="16176-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
