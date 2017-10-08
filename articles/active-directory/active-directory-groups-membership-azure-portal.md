---
title: grupos de hello aaaManage su grupo pertenece tooin Azure Active Directory | Documentos de Microsoft
description: "Los grupos pueden contener otros grupos en Azure Active Directory. Le mostramos cómo toomanage esas pertenencias."
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
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="9fc12-104">Administrar grupos de toowhich que pertenece un grupo en el inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fc12-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="9fc12-105">Los grupos pueden contener otros grupos en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fc12-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="9fc12-106">Le mostramos cómo toomanage esas pertenencias.</span><span class="sxs-lookup"><span data-stu-id="9fc12-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="9fc12-107">¿Cómo se puede encontrar grupos de hello de que mi grupo es un miembro?</span><span class="sxs-lookup"><span data-stu-id="9fc12-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="9fc12-108">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fc12-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="9fc12-109">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="9fc12-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="9fc12-111">En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.</span><span class="sxs-lookup"><span data-stu-id="9fc12-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="9fc12-113">En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="9fc12-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="9fc12-114">En hello **grupo - *groupname***  hoja, seleccione **las pertenencias a grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fc12-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Hoja de pertenencia a grupo de apertura Hola](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="9fc12-116">tooadd el grupo como miembro de otro grupo, en hello **de grupo: las pertenencias a grupos** hoja, seleccione hello **agregar** comando.</span><span class="sxs-lookup"><span data-stu-id="9fc12-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="9fc12-117">Seleccione un grupo de hello **Seleccionar grupo** hoja y, a continuación, seleccione hello **seleccione** situado en parte inferior de Hola de hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fc12-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="9fc12-118">Puede agregar el grupo de una tooonly a la vez.</span><span class="sxs-lookup"><span data-stu-id="9fc12-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="9fc12-119">Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias.</span><span class="sxs-lookup"><span data-stu-id="9fc12-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="9fc12-120">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="9fc12-120">No wildcard characters are accepted in that box.</span></span>

   ![Adición de una pertenencia a grupos](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="9fc12-122">tooremove el grupo como miembro de otro grupo, en hello **de grupo: las pertenencias a grupos** hoja, seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="9fc12-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="9fc12-123">En hello ***groupname*** hoja, seleccione hello **quitar** comando y confirme su elección en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fc12-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Comando de eliminación de pertenencia a grupo](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="9fc12-125">Cuando termine de cambiar las pertenencias a grupos de su grupo, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9fc12-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9fc12-126">Información adicional</span><span class="sxs-lookup"><span data-stu-id="9fc12-126">Additional information</span></span>
<span data-ttu-id="9fc12-127">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9fc12-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9fc12-128">Ver los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="9fc12-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9fc12-129">Crear un nuevo grupo y agregar miembros</span><span class="sxs-lookup"><span data-stu-id="9fc12-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="9fc12-130">Administrar la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="9fc12-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="9fc12-131">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="9fc12-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="9fc12-132">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="9fc12-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
