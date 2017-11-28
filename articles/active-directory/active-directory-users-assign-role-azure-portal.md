---
title: "Asignación de un usuario a roles de administrador en Azure Active Directory | Microsoft Docs"
description: "Explica cómo cambiar la información administrativa de los usuarios en Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: bfadf133154488f9827cfbeaa98ddb0eb84b52f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="0ca0f-103">Asignación de un usuario a roles de administrador en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0ca0f-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="0ca0f-104">En este artículo se explica cómo asignar un rol administrativo a un usuario en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0ca0f-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0ca0f-105">Para obtener más información sobre cómo agregar nuevos usuarios en su organización, consulte [Incorporación de nuevos usuarios a Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0ca0f-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="0ca0f-106">De forma predeterminada, los usuarios agregados no tienen permisos de administrador, pero puede asignárselos en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="0ca0f-107">Asignar de un rol a un usuario</span><span class="sxs-lookup"><span data-stu-id="0ca0f-107">Assign a role to a user</span></span>
1. <span data-ttu-id="0ca0f-108">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="0ca0f-109">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="0ca0f-111">En la hoja **Usuarios y grupos**, seleccione **Todos los usuarios**.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-111">On the **Users and groups** blade, select **All users**.</span></span>

   ![Apertura de la hoja Todos los usuarios](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="0ca0f-113">En la hoja **Usuarios y grupos - Todos los usuarios** , seleccione un usuario de la lista.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-113">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="0ca0f-114">En la hoja del usuario seleccionado, seleccione**Rol del directorio**, y, luego, asigne al usuario un rol de la lista **Rol del directorio**.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-114">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="0ca0f-115">Para obtener más información acerca de los roles del usuario y el administrador, consulte [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0ca0f-115">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Asignación de un rol a un usuario](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="0ca0f-117">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0ca0f-117">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ca0f-118">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0ca0f-118">Next steps</span></span>
* [<span data-ttu-id="0ca0f-119">Adición de un usuario</span><span class="sxs-lookup"><span data-stu-id="0ca0f-119">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="0ca0f-120">Restablecer una contraseña de usuario en el nuevo Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0ca0f-120">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="0ca0f-121">Cambiar la información de trabajo de un usuario</span><span class="sxs-lookup"><span data-stu-id="0ca0f-121">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="0ca0f-122">Administrar perfiles de usuario</span><span class="sxs-lookup"><span data-stu-id="0ca0f-122">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="0ca0f-123">Eliminar un usuario de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0ca0f-123">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
