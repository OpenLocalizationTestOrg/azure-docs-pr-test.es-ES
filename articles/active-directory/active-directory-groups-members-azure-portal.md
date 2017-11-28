---
title: miembros de hello aaaManage para un grupo en Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo tooadd o quitar usuarios y dispositivos de un grupo en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="0bac4-103">Administración de la pertenencia a grupos de los usuarios del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bac4-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="0bac4-104">Este artículo explica cómo toomanage Hola a los miembros de un grupo en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bac4-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="0bac4-105">¿Cómo buscar a los miembros de Hola y administrarlos?</span><span class="sxs-lookup"><span data-stu-id="0bac4-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="0bac4-106">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bac4-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="0bac4-107">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="0bac4-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="0bac4-109">En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.</span><span class="sxs-lookup"><span data-stu-id="0bac4-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="0bac4-111">En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="0bac4-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="0bac4-112">En hello **grupo - *groupname***  hoja, seleccione **miembros**.</span><span class="sxs-lookup"><span data-stu-id="0bac4-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Hoja de los miembros de Hola de apertura](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="0bac4-114">grupo de toohello miembros tooadd, en hello **grupo - miembros** hoja, seleccione **agregar miembros**.</span><span class="sxs-lookup"><span data-stu-id="0bac4-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Comando Agregar miembros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="0bac4-116">En hello **miembros** hoja, seleccione uno o más usuarios o dispositivos grupo de toohello tooadd y seleccione hello **seleccione** situado en la parte inferior de Hola de hello hoja tooadd les toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="0bac4-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="0bac4-117">Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias.</span><span class="sxs-lookup"><span data-stu-id="0bac4-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="0bac4-118">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="0bac4-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="0bac4-119">tooremove miembros del grupo de hello, en hello **grupo - miembros** hoja, seleccione un miembro.</span><span class="sxs-lookup"><span data-stu-id="0bac4-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="0bac4-120">En hello ***membername*** hoja, seleccione hello **quitar** comando y confirme su elección en el símbolo del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="0bac4-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Comando Quitar miembros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="0bac4-122">Cuando termine de modificar los miembros del grupo de hello, seleccione **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0bac4-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="0bac4-123">Información adicional</span><span class="sxs-lookup"><span data-stu-id="0bac4-123">Additional information</span></span>
<span data-ttu-id="0bac4-124">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bac4-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="0bac4-125">Ver los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="0bac4-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="0bac4-126">Crear un nuevo grupo y agregar miembros</span><span class="sxs-lookup"><span data-stu-id="0bac4-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="0bac4-127">Administrar la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="0bac4-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="0bac4-128">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="0bac4-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="0bac4-129">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="0bac4-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
