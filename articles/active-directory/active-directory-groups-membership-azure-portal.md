---
title: "Administración de los grupos a los que pertenece un grupo en Azure Active Directory | Microsoft Docs"
description: "Los grupos pueden contener otros grupos en Azure Active Directory. Aquí se muestra cómo administrar las pertenencias a grupos."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="b5a50-104">Administración de los grupos a los que pertenece un grupo en el inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5a50-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="b5a50-105">Los grupos pueden contener otros grupos en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5a50-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="b5a50-106">Aquí se muestra cómo administrar las pertenencias a grupos.</span><span class="sxs-lookup"><span data-stu-id="b5a50-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="b5a50-107">¿Cómo puedo encontrar los grupos de los que es miembro mi grupo?</span><span class="sxs-lookup"><span data-stu-id="b5a50-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="b5a50-108">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="b5a50-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="b5a50-109">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b5a50-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="b5a50-111">En la hoja **Usuarios y grupos**, seleccione **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="b5a50-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura de la hoja Grupos](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="b5a50-113">En la hoja **Usuarios y grupos - Todos los grupos** seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="b5a50-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="b5a50-114">En la hoja **Grupo - *nombre del grupo*** seleccione **Pertenencia a grupos**.</span><span class="sxs-lookup"><span data-stu-id="b5a50-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Apertura de la hoja Pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="b5a50-116">Para agregar un grupo como miembro de otro grupo, en la hoja **Grupo - Pertenencia a grupos** seleccione el comando **Agregar** comando.</span><span class="sxs-lookup"><span data-stu-id="b5a50-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="b5a50-117">Seleccione un grupo de la hoja **Seleccionar grupo** y, después, haga clic en el botón **Seleccionar** situado en la parte inferior de dicha hoja.</span><span class="sxs-lookup"><span data-stu-id="b5a50-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="b5a50-118">Solo se pueden agregar grupos a otros grupos de uno en uno.</span><span class="sxs-lookup"><span data-stu-id="b5a50-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="b5a50-119">El cuadro **Usuario** filtra la visualización en función de si coincide lo que ha escrito con cualquier parte del nombre de un usuario o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b5a50-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="b5a50-120">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="b5a50-120">No wildcard characters are accepted in that box.</span></span>

   ![Adición de una pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="b5a50-122">Para quitar un grupo como miembro de otro grupo, en la hoja **Grupo - Pertenencia a grupos** , seleccione uno.</span><span class="sxs-lookup"><span data-stu-id="b5a50-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="b5a50-123">En la hoja ***nombreDelGrupo***, seleccione el comando **Quitar** y confirme la elección en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b5a50-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Comando de eliminación de pertenencia a grupo](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="b5a50-125">Cuando termine de cambiar las pertenencias a grupos de su grupo, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="b5a50-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="b5a50-126">Información adicional</span><span class="sxs-lookup"><span data-stu-id="b5a50-126">Additional information</span></span>
<span data-ttu-id="b5a50-127">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5a50-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="b5a50-128">Ver los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="b5a50-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b5a50-129">Crear un nuevo grupo y agregar miembros</span><span class="sxs-lookup"><span data-stu-id="b5a50-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="b5a50-130">Administrar la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="b5a50-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="b5a50-131">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="b5a50-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="b5a50-132">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="b5a50-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
