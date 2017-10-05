---
title: "Asignación de un usuario o un grupo a una aplicación empresarial en Azure Active Directory | Microsoft Docs"
description: "Procedimiento para seleccionar una aplicación empresarial para asignarla a un usuario o un grupo en la versión preliminar de Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="9fc52-103">Asignación de un usuario o un grupo a una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9fc52-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="9fc52-104">Asignar un usuario o un grupo a una aplicación empresarial de Azure Active Directory (Azure AD) es fácil.</span><span class="sxs-lookup"><span data-stu-id="9fc52-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9fc52-105">Debe tener los permisos adecuados para administrar la aplicación de empresa y debe ser administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="9fc52-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="9fc52-106">¿Cómo se asigna a los usuarios acceso a una aplicación empresarial?</span><span class="sxs-lookup"><span data-stu-id="9fc52-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="9fc52-107">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="9fc52-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9fc52-108">Seleccione **Más servicios**, escriba Azure Active Directory en el cuadro de texto y seleccione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="9fc52-109">En la hoja **Azure Active Directory - *nombreDelDirectorio*** (es decir, la hoja de Azure AD del directorio que está administrando), seleccione **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="9fc52-111">En la hoja **Aplicaciones empresariales**, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="9fc52-112">Verá una lista de las aplicaciones que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="9fc52-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="9fc52-113">En la hoja **Enterprise applications (Aplicaciones empresariales) - Todas las aplicaciones** , seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fc52-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="9fc52-114">En la hoja ***nombre de la aplicación*** (es decir, la hoja con el nombre de la aplicación seleccionada en el título), seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selección del comando Todas las aplicaciones](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="9fc52-116">En la hoja ***nombreDeAplicación*** **- User & Group Assignment** (Asignación de usuario y de grupo), seleccione el comando **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="9fc52-117">En la hoja **Agregar asignación**, seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Asignación de un usuario o un grupo a la aplicación](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="9fc52-119">En la hoja **Usuarios y grupos**, seleccione uno o varios usuarios o grupos de la lista y luego haga clic en el botón **Seleccionar** de la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9fc52-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="9fc52-120">En la hoja **Agregar asignación**, seleccione **Rol**.</span><span class="sxs-lookup"><span data-stu-id="9fc52-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="9fc52-121">Después, en la hoja **Seleccionar rol**, seleccione el rol que desea aplicar a los usuarios o grupos seleccionados, y luego haga clic en el botón **Aceptar** de la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9fc52-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="9fc52-122">En la hoja **Agregar asignación**, haga clic en el botón **Asignar** de la parte inferior de la hoja.</span><span class="sxs-lookup"><span data-stu-id="9fc52-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="9fc52-123">Los usuarios o grupos asignados tendrán definidos los permisos por el rol seleccionado para esta aplicación empresarial.</span><span class="sxs-lookup"><span data-stu-id="9fc52-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fc52-124">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fc52-124">Next steps</span></span>
* [<span data-ttu-id="9fc52-125">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="9fc52-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9fc52-126">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9fc52-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="9fc52-127">Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9fc52-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="9fc52-128">Cambio del nombre o el logotipo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="9fc52-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
