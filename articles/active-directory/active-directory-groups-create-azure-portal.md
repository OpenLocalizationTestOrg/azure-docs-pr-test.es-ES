---
title: aaaCreate un grupo de usuarios de Active Directory de Azure | Documentos de Microsoft
description: "¿Cómo toocreate un grupo en Azure Active Directory y agregue el grupo de miembros toohello"
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="16bc9-103">Creación de un grupo y adición de miembros en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="16bc9-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16bc9-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="16bc9-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="16bc9-105">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="16bc9-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="16bc9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16bc9-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="16bc9-107">Este artículo se explica cómo toocreate y rellenar un nuevo grupo en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16bc9-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="16bc9-108">Utilice una tarea de administración de grupo tooperform como la asignación de licencias o permisos tooa número de usuarios o dispositivos a la vez.</span><span class="sxs-lookup"><span data-stu-id="16bc9-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="16bc9-109">¿Cómo se crea un grupo?</span><span class="sxs-lookup"><span data-stu-id="16bc9-109">How do I create a group?</span></span>
1. <span data-ttu-id="16bc9-110">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con una cuenta que sea un administrador global para el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="16bc9-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="16bc9-111">Seleccione **más servicios**, escriba **usuarios y grupos** en Hola cuadro de texto y, a continuación, seleccione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="16bc9-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Apertura de Administración de usuarios](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="16bc9-113">En hello **usuarios y grupos** hoja, seleccione **todos los grupos de**.</span><span class="sxs-lookup"><span data-stu-id="16bc9-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Hoja de apertura Hola grupos](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="16bc9-115">En hello **a los usuarios y grupos: todos los grupos de** hoja, seleccione hello **agregar** comando.</span><span class="sxs-lookup"><span data-stu-id="16bc9-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Al seleccionar el comando Add Hola](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="16bc9-117">En hello **grupo** hoja, agregue un nombre y una descripción para el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="16bc9-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="16bc9-118">tooselect tooadd toohello grupo de miembros, seleccione **asignado** en hello **tipo de pertenencia** cuadro y, a continuación, seleccione **miembros**.</span><span class="sxs-lookup"><span data-stu-id="16bc9-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="16bc9-119">Para obtener más información acerca de cómo toomanage Hola pertenencia de un grupo de forma dinámica, consulte [utilizando atributos toocreate reglas de pertenencia a grupos avanzadas](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="16bc9-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Seleccionar miembros tooadd](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="16bc9-121">En hello **miembros** hoja, seleccione uno o más usuarios o dispositivos grupo de toohello tooadd y seleccione hello **seleccione** situado en la parte inferior de Hola de hello hoja tooadd les toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="16bc9-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="16bc9-122">Hola **usuario** cuadro filtra Hola presentación de acuerdo con la parte de un nombre de usuario o dispositivo tooany de entrada de búsqueda de coincidencias.</span><span class="sxs-lookup"><span data-stu-id="16bc9-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="16bc9-123">No se aceptan caracteres comodín en el cuadro.</span><span class="sxs-lookup"><span data-stu-id="16bc9-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="16bc9-124">Cuando termine de agregar el grupo de miembros toohello, seleccione **crear** en hello **grupo** hoja.</span><span class="sxs-lookup"><span data-stu-id="16bc9-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Creación de la confirmación de grupo](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="16bc9-126">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16bc9-126">Next steps</span></span>
<span data-ttu-id="16bc9-127">Estos artículos proporcionan información adicional sobre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16bc9-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="16bc9-128">Consulta de los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="16bc9-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="16bc9-129">Administración de la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="16bc9-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="16bc9-130">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="16bc9-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="16bc9-131">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="16bc9-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="16bc9-132">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="16bc9-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
