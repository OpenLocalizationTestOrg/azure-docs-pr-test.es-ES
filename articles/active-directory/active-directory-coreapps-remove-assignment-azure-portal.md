---
title: "Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory | Microsoft Docs"
description: "Cómo eliminar la asignación del acceso de un usuario o grupo de una aplicación empresarial en Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="7feac-103">Eliminación de asignaciones de usuario o grupo de una aplicación empresarial en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7feac-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="7feac-104">Evitar que se asigne acceso a un usuario o grupo a una de sus aplicaciones empresariales en Azure Active Directory (Azure AD) es fácil.</span><span class="sxs-lookup"><span data-stu-id="7feac-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="7feac-105">Debe tener los permisos adecuados para administrar la aplicación de empresa y debe ser administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7feac-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="7feac-106">¿Cómo se puede eliminar una asignación de grupo o usuario?</span><span class="sxs-lookup"><span data-stu-id="7feac-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="7feac-107">Inicie sesión en [Azure Portal](https://portal.azure.com) con una cuenta que tenga el rol de administrador global en el directorio.</span><span class="sxs-lookup"><span data-stu-id="7feac-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7feac-108">Seleccione **Más servicios**, escriba **Azure Active Directory** en el cuadro de texto y presione **ENTRAR**.</span><span class="sxs-lookup"><span data-stu-id="7feac-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="7feac-109">En la hoja **Azure Active Directory - *nombreDelDirectorio*** (es decir, la hoja de Azure AD del directorio que está administrando), seleccione **Aplicaciones empresariales**.</span><span class="sxs-lookup"><span data-stu-id="7feac-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Apertura de Enterprise apps (Aplicaciones empresariales)](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="7feac-111">En la hoja **Aplicaciones empresariales**, seleccione **Todas las aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="7feac-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="7feac-112">Verá una lista de las aplicaciones que puede administrar.</span><span class="sxs-lookup"><span data-stu-id="7feac-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="7feac-113">En la hoja **Enterprise applications (Aplicaciones empresariales) - Todas las aplicaciones** , seleccione una aplicación.</span><span class="sxs-lookup"><span data-stu-id="7feac-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="7feac-114">En la hoja ***appname*** (es decir, la hoja con el nombre de la aplicación seleccionada en el título), seleccione **Usuarios y grupos**.</span><span class="sxs-lookup"><span data-stu-id="7feac-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Selección de usuarios o grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="7feac-116">En la hoja ***appname*** **- Asignación de usuarios y grupos**, seleccione uno o varios usuarios o grupos y, luego, seleccione el comando**Quitar**.</span><span class="sxs-lookup"><span data-stu-id="7feac-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="7feac-117">Confirme la decisión en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="7feac-117">Confirm your decision at the prompt.</span></span>

    ![Selección del comando Eliminar](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="7feac-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7feac-119">Next steps</span></span>
* [<span data-ttu-id="7feac-120">Ver todos mis grupos</span><span class="sxs-lookup"><span data-stu-id="7feac-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="7feac-121">Asignar un usuario o grupo a una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="7feac-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="7feac-122">Deshabilitar los inicios de sesión de los usuarios de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="7feac-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="7feac-123">Cambio del nombre o el logotipo de una aplicación empresarial</span><span class="sxs-lookup"><span data-stu-id="7feac-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
