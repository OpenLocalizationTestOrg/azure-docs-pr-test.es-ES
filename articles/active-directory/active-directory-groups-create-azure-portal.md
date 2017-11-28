---
title: "Creación de un grupo para usuarios de Azure Active Directory | Microsoft Docs"
description: Procedimiento para crear un grupo en Azure Active Directory y agregar miembros al grupo
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="5cde2-103">Creación de un grupo y adición de miembros en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5cde2-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5cde2-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5cde2-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="5cde2-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="5cde2-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="5cde2-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5cde2-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="5cde2-107">En este artículo se explica cómo crear y rellenar un nuevo grupo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cde2-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="5cde2-108">Use un grupo para realizar tareas de administración, como asignar licencias o permisos a un número de usuarios o dispositivos a la vez.</span><span class="sxs-lookup"><span data-stu-id="5cde2-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="5cde2-109">¿Cómo se crea un grupo?</span><span class="sxs-lookup"><span data-stu-id="5cde2-109">How do I create a group?</span></span>
1. <span data-ttu-id="5cde2-110">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="5cde2-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="5cde2-111">Seleccione **Más servicios**, escriba **Usuarios** y grupos en el cuadro de texto y, después, presione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="5cde2-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="5cde2-113">En la hoja **Usuarios y grupos**, seleccione **Todos los grupos**.</span><span class="sxs-lookup"><span data-stu-id="5cde2-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Apertura de la hoja Grupos](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="5cde2-115">En la hoja **Usuarios y grupos - Todos los grupos**, seleccione el comando **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5cde2-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Selección del comando Agregar](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="5cde2-117">En la hoja **Grupo** , agregue un nombre y una descripción para el nuevo grupo.</span><span class="sxs-lookup"><span data-stu-id="5cde2-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="5cde2-118">Para seleccionar los miembros que se agregarán al grupo, seleccione **Asignado** en el cuadro **Membership type** (Tipo de pertenencia a grupos) y luego seleccione **Miembros**.</span><span class="sxs-lookup"><span data-stu-id="5cde2-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="5cde2-119">Para obtener más información sobre cómo administrar la pertenencia de un grupo de forma dinámica, consulte el artículo sobre el [uso de atributos para crear reglas avanzadas de pertenencias a grupo](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5cde2-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selección de miembros para agregar](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="5cde2-121">En la hoja **Miembros**, seleccione uno o varios usuarios o dispositivos que quiera agregar al grupo y, luego, haga clic en el botón **Seleccionar** situado en la parte inferior de la hoja para agregarlos.</span><span class="sxs-lookup"><span data-stu-id="5cde2-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="5cde2-122">El cuadro **Usuario** filtra la visualización en función de si coincide lo que ha escrito con cualquier parte del nombre de un usuario o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5cde2-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="5cde2-123">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="5cde2-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="5cde2-124">Cuando termine de agregar miembros al grupo, seleccione **Crear** en la hoja **Grupo**.</span><span class="sxs-lookup"><span data-stu-id="5cde2-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Creación de la confirmación de grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="5cde2-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5cde2-126">Next steps</span></span>
<span data-ttu-id="5cde2-127">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5cde2-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="5cde2-128">Consulta de los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="5cde2-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5cde2-129">Administración de la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="5cde2-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="5cde2-130">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="5cde2-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="5cde2-131">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="5cde2-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="5cde2-132">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="5cde2-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
