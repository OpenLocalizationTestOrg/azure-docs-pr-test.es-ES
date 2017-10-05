---
title: "Restauración de un grupo eliminado de Office 365 en Azure Active Directory | Microsoft Docs"
description: "Restauración de un grupo eliminado, visualización de grupos restaurables y eliminación permanente de un grupo en Azure Active Directory"
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
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 32d36ae96797a59bb47bf782ab038f21f231f046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="5f143-103">Restauración de un grupo eliminado de Office 365 en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f143-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="5f143-104">Cuando se elimina un grupo de Office 365 en Azure Active Directory (Azure AD), el grupo eliminado queda retenido y deja de estar visible durante 30 días a contar desde la fecha de eliminación.</span><span class="sxs-lookup"><span data-stu-id="5f143-104">When you delete an Office 365 group in the Azure Active Directory (Azure AD), the deleted group is retained but not visible for 30 days from the deletion date.</span></span> <span data-ttu-id="5f143-105">Esto es así para que el grupo y su contenido se puedan restaurar en caso de ser necesario.</span><span class="sxs-lookup"><span data-stu-id="5f143-105">This is so that the group and its contents can be restored if needed.</span></span> <span data-ttu-id="5f143-106">Esta funcionalidad está restringida exclusivamente a los grupos de Office 365 en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f143-106">This functionality is restricted exclusively to Office 365 groups in Azure AD.</span></span> <span data-ttu-id="5f143-107">No está disponible para los grupos de seguridad ni los grupos de distribución.</span><span class="sxs-lookup"><span data-stu-id="5f143-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="5f143-108">No utilice `Remove-MsolGroup` porque purga el grupo de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="5f143-108">Don't use `Remove-MsolGroup` because it purges the group permanently.</span></span> <span data-ttu-id="5f143-109">Utilice siempre `Remove-AzureADMSGroup` para eliminar un grupo de O365.</span><span class="sxs-lookup"><span data-stu-id="5f143-109">Always use `Remove-AzureADMSGroup` to delete an O365 group.</span></span> 

<span data-ttu-id="5f143-110">Los permisos necesarios para restaurar un grupo pueden ser cualquiera de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5f143-110">The permissions required to restore a group can be any of the following:</span></span>

<span data-ttu-id="5f143-111">Rol</span><span class="sxs-lookup"><span data-stu-id="5f143-111">Role</span></span>  | <span data-ttu-id="5f143-112">Permisos</span><span class="sxs-lookup"><span data-stu-id="5f143-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="5f143-113">Administrador de la compañía, Soporte para asociados de nivel 2 y Administradores de servicio de Intune</span><span class="sxs-lookup"><span data-stu-id="5f143-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="5f143-114">Puede restaurar cualquier grupo eliminado de Office 365</span><span class="sxs-lookup"><span data-stu-id="5f143-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="5f143-115">Administrador de cuenta de usuario y Soporte para asociados de nivel 1</span><span class="sxs-lookup"><span data-stu-id="5f143-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="5f143-116">Puede restaurar cualquier grupo eliminado de Office 365, excepto los asignados al rol Administrador de la compañía</span><span class="sxs-lookup"><span data-stu-id="5f143-116">Can restore any deleted Office 365 group except those assigned to the Company Administrator role</span></span> 
<span data-ttu-id="5f143-117">Usuario</span><span class="sxs-lookup"><span data-stu-id="5f143-117">User</span></span> | <span data-ttu-id="5f143-118">Puede restaurar cualquier grupo eliminado de Office 365 de su propiedad</span><span class="sxs-lookup"><span data-stu-id="5f143-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-the-deleted-office-365-groups-that-are-available-to-restore"></a><span data-ttu-id="5f143-119">Visualización de grupos eliminados de Office 365 disponibles para restauración</span><span class="sxs-lookup"><span data-stu-id="5f143-119">View the deleted Office 365 groups that are available to restore</span></span>
<span data-ttu-id="5f143-120">Los cmdlets siguientes se pueden usar para ver los grupos eliminados y comprobar que todavía no se purgaron los que le interesan.</span><span class="sxs-lookup"><span data-stu-id="5f143-120">The following cmdlets can be used to view the deleted groups to verify that the one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="5f143-121">Estos cmdlets son parte del [módulo de Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="5f143-121">These cmdlets are part of the [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="5f143-122">Puede encontrar más información sobre este módulo en el artículo sobre la [versión 2 de Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="5f143-122">More information about this module can be found in the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="5f143-123">Ejecute el cmdlet siguiente para mostrar todos los grupos eliminados de Office 365 existentes en el inquilino que todavía se pueden restaurar.</span><span class="sxs-lookup"><span data-stu-id="5f143-123">Run the following cmdlet to display all deleted Office 365 groups in your tenant that are still available to restore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="5f143-124">Como alternativa, si conoce el id. de objeto de un grupo específico (y puede obtenerlo del cmdlet del paso 1), ejecute el cmdlet siguiente para comprobar que el grupo eliminado específico todavía no se purgó de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="5f143-124">Alternately, if you know the objectID of a specific group (and you can get it from the cmdlet in step 1), run the following cmdlet to verify that the specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-to-restore-your-deleted-office-365-group"></a><span data-ttu-id="5f143-125">Procedimientos para restaurar grupos eliminados de Office 365</span><span class="sxs-lookup"><span data-stu-id="5f143-125">How to restore your deleted Office 365 group</span></span>
<span data-ttu-id="5f143-126">Una vez que haya comprobado que el grupo todavía se puede restaurar, siga uno de los pasos siguientes para restaurar el grupo eliminado.</span><span class="sxs-lookup"><span data-stu-id="5f143-126">Once you have verified that the group is still available to restore, restore the deleted group with one of the following steps.</span></span> <span data-ttu-id="5f143-127">Si el grupo contiene documentos, sitios de SP u otros objetos persistentes, el proceso completo de restauración de un grupo y su contenido podría demorar hasta 24 horas.</span><span class="sxs-lookup"><span data-stu-id="5f143-127">If the group contains documents, SP sites, or other persistent objects, it might take up to 24 hours to fully restore a group and its contents.</span></span>

1.  <span data-ttu-id="5f143-128">Ejecute el cmdlet siguiente para restaurar el grupo y su contenido.</span><span class="sxs-lookup"><span data-stu-id="5f143-128">Run the following cmdlet to restore the group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="5f143-129">Como alternativa, puede ejecutar el cmdlet siguiente para quitar el grupo eliminado de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="5f143-129">Alternatively, the following cmdlet can be run to permanently remove the deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="5f143-130">¿Cómo se puede saber si funcionó?</span><span class="sxs-lookup"><span data-stu-id="5f143-130">How do you know this worked?</span></span>
<span data-ttu-id="5f143-131">Para comprobar que restauró correctamente un grupo de Office 365, ejecute el cmdlet `Get-AzureADGroup –ObjectId <objectId>` para mostrar información sobre el grupo.</span><span class="sxs-lookup"><span data-stu-id="5f143-131">To verify that you’ve successfully restored an Office 365 group, run the `Get-AzureADGroup –ObjectId <objectId>` cmdlet to display information about the group.</span></span> <span data-ttu-id="5f143-132">Una vez que la solicitud de restauración se complete:</span><span class="sxs-lookup"><span data-stu-id="5f143-132">After the restore request is completed:</span></span>
- <span data-ttu-id="5f143-133">El grupo aparecerá en la barra de navegación izquierda de Exchange</span><span class="sxs-lookup"><span data-stu-id="5f143-133">The group will appear in the Left nav bar on Exchange</span></span>
- <span data-ttu-id="5f143-134">El plan del grupo aparecerá en Planner</span><span class="sxs-lookup"><span data-stu-id="5f143-134">The plan for the group will appear in Planner</span></span>
- <span data-ttu-id="5f143-135">Los sitios de SharePoint y su contenido estarán disponibles</span><span class="sxs-lookup"><span data-stu-id="5f143-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="5f143-136">Se podrá tener acceso al grupo desde cualquiera de los puntos de conexión de Exchange y otras cargas de trabajo de Office 365 compatibles con los grupos de Office 365</span><span class="sxs-lookup"><span data-stu-id="5f143-136">The group can be accessed from any of the Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="5f143-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5f143-137">Next steps</span></span>
<span data-ttu-id="5f143-138">En estos artículos se proporciona información adicional sobre los grupos de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5f143-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="5f143-139">Consulta de los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="5f143-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5f143-140">Administración de la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="5f143-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="5f143-141">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="5f143-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="5f143-142">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="5f143-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="5f143-143">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="5f143-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
