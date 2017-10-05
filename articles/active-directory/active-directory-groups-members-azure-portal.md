---
title: "Administración de los miembros de un grupo en Azure Active Directory | Microsoft Docs"
description: "Cómo agregar o quitar usuarios y dispositivos de un grupo en Azure Active Directory"
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
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="2c1ea-103">Administración de la pertenencia a grupos de los usuarios del inquilino de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2c1ea-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="2c1ea-104">En este artículo se explica cómo administrar los miembros de un grupo en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2c1ea-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="2c1ea-105">¿Cómo puedo buscar miembros y administrarlos?</span><span class="sxs-lookup"><span data-stu-id="2c1ea-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="2c1ea-106">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="2c1ea-107">Seleccione **Más servicios**, escriba **Usuarios y grupos** en el cuadro de texto y presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="2c1ea-109">En la hoja **Usuarios y grupos**, seleccione **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura de la hoja Grupos](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="2c1ea-111">En la hoja **Usuarios y grupos - Todos los grupos** , seleccione un grupo.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="2c1ea-112">En la hoja **Grupo - *nombre del grupo*** , seleccione **Miembros**.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Apertura de la hoja Miembros](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="2c1ea-114">Para agregar miembros al grupo, en la hoja **Grupo - Miembros**, seleccione **Agregar miembros**.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Comando Agregar miembros](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="2c1ea-116">En la hoja **Miembros**, seleccione uno o varios usuarios o dispositivos que quiera agregar al grupo y, luego, haga clic en el botón **Seleccionar** situado en la parte inferior de la hoja para agregarlos.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="2c1ea-117">El cuadro **Usuario** filtra la visualización en función de si coincide lo que ha escrito con cualquier parte del nombre de un usuario o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="2c1ea-118">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="2c1ea-119">Para quitar miembros del grupo, en la hoja **Grupo - Miembros** , seleccione uno.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="2c1ea-120">En la hoja ***nombreDelMiembro***, seleccione el comando **Quitar** y confirme la elección en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Comando Quitar miembros](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="2c1ea-122">Cuando termine de modificar miembros del grupo, seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="2c1ea-123">Información adicional</span><span class="sxs-lookup"><span data-stu-id="2c1ea-123">Additional information</span></span>
<span data-ttu-id="2c1ea-124">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2c1ea-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="2c1ea-125">Ver los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="2c1ea-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="2c1ea-126">Crear un nuevo grupo y agregar miembros</span><span class="sxs-lookup"><span data-stu-id="2c1ea-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="2c1ea-127">Administrar la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="2c1ea-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="2c1ea-128">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="2c1ea-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="2c1ea-129">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="2c1ea-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
