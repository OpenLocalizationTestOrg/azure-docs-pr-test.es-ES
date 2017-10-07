---
title: grupo de aaaRestore un eliminado Office 365 en Azure Active Directory | Documentos de Microsoft
description: "¿Cómo toorestore un grupo eliminado y ver grupos pueden restaurarse, permamnently eliminación un grupo en Azure Active Directory"
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
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="950d3-103">Restauración de un grupo eliminado de Office 365 en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="950d3-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="950d3-104">Cuando se elimina un grupo de Office 365 en hello Azure Active Directory (Azure AD), grupo de hello eliminado es retenido pero no está visible durante 30 días desde la fecha de eliminación de Hola.</span><span class="sxs-lookup"><span data-stu-id="950d3-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="950d3-105">Esto es para que el grupo de Hola y su contenido se puede restaurar si es necesario.</span><span class="sxs-lookup"><span data-stu-id="950d3-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="950d3-106">Esta funcionalidad está restringida exclusivamente tooOffice 365 grupos en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="950d3-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="950d3-107">No está disponible para los grupos de seguridad ni los grupos de distribución.</span><span class="sxs-lookup"><span data-stu-id="950d3-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="950d3-108">No utilice `Remove-MsolGroup` porque purga grupo Hola permanentemente.</span><span class="sxs-lookup"><span data-stu-id="950d3-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="950d3-109">Utilice siempre `Remove-AzureADMSGroup` grupo toodelete un Office 365.</span><span class="sxs-lookup"><span data-stu-id="950d3-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="950d3-110">se requieren permisos de Hello toorestore un grupo puede ser cualquiera de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="950d3-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="950d3-111">Rol</span><span class="sxs-lookup"><span data-stu-id="950d3-111">Role</span></span>  | <span data-ttu-id="950d3-112">Permisos</span><span class="sxs-lookup"><span data-stu-id="950d3-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="950d3-113">Administrador de la compañía, Soporte para asociados de nivel 2 y Administradores de servicio de Intune</span><span class="sxs-lookup"><span data-stu-id="950d3-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="950d3-114">Puede restaurar cualquier grupo eliminado de Office 365</span><span class="sxs-lookup"><span data-stu-id="950d3-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="950d3-115">Administrador de cuenta de usuario y Soporte para asociados de nivel 1</span><span class="sxs-lookup"><span data-stu-id="950d3-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="950d3-116">Puede restaurar cualquier grupo de Office 365 eliminado excepto los toohello asignado el rol de administrador de la compañía</span><span class="sxs-lookup"><span data-stu-id="950d3-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="950d3-117">Usuario</span><span class="sxs-lookup"><span data-stu-id="950d3-117">User</span></span> | <span data-ttu-id="950d3-118">Puede restaurar cualquier grupo eliminado de Office 365 de su propiedad</span><span class="sxs-lookup"><span data-stu-id="950d3-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="950d3-119">Hola Vista elimina grupos de Office 365 toorestore disponible</span><span class="sxs-lookup"><span data-stu-id="950d3-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="950d3-120">Hola siguientes cmdlets puede ser utilizados tooview Hola elimina grupos tooverify que Hola uno o aquellos que le interesa que no aún se hayan permanentemente purgados.</span><span class="sxs-lookup"><span data-stu-id="950d3-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="950d3-121">Estos cmdlets forman parte del programa Hola a [módulo de PowerShell de Azure AD](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="950d3-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="950d3-122">Para obtener más información acerca de este módulo puede encontrarse en hello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0) artículo.</span><span class="sxs-lookup"><span data-stu-id="950d3-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="950d3-123">Ejecute hello siguiente cmdlet toodisplay de eliminar todos los grupos de Office 365 en el inquilino que son toorestore seguirá estando disponible.</span><span class="sxs-lookup"><span data-stu-id="950d3-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="950d3-124">Como alternativa, si sabe objectID Hola de un grupo específico (y puede obtenerlo de cmdlet de hello en el paso 1), ejecución Hola después tooverify de cmdlet que Hola específico grupo eliminado no todavía permanentemente purgado.</span><span class="sxs-lookup"><span data-stu-id="950d3-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="950d3-125">Cómo toorestore el grupo de Office 365 eliminado</span><span class="sxs-lookup"><span data-stu-id="950d3-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="950d3-126">Una vez que haya verificado de que ese grupo de hello es toorestore seguirá estando disponible, restaure grupo Hola eliminado con uno de los pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="950d3-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="950d3-127">Si el grupo de hello contiene documentos, sitios de SP u otros objetos persistentes, podría tardar hasta too24 horas toofully restaurar un grupo y su contenido.</span><span class="sxs-lookup"><span data-stu-id="950d3-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="950d3-128">Ejecución hello siguientes cmdlet toorestore Hola grupo y su contenido.</span><span class="sxs-lookup"><span data-stu-id="950d3-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="950d3-129">Como alternativa, hello siguiente cmdlet se puede ejecutar toopermanently quitar grupo de hello eliminado.</span><span class="sxs-lookup"><span data-stu-id="950d3-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="950d3-130">¿Cómo se puede saber si funcionó?</span><span class="sxs-lookup"><span data-stu-id="950d3-130">How do you know this worked?</span></span>
<span data-ttu-id="950d3-131">tooverify que ha restaurado correctamente un grupo de Office 365, ejecute hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay información sobre el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="950d3-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="950d3-132">Después de la restauración de hello completar la solicitud:</span><span class="sxs-lookup"><span data-stu-id="950d3-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="950d3-133">Hola grupo aparecerá en la barra de navegación izquierdo de hello en Exchange</span><span class="sxs-lookup"><span data-stu-id="950d3-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="950d3-134">plan de Hello para el grupo de hello aparecerá en Planificador</span><span class="sxs-lookup"><span data-stu-id="950d3-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="950d3-135">Los sitios de SharePoint y su contenido estarán disponibles</span><span class="sxs-lookup"><span data-stu-id="950d3-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="950d3-136">grupo de Hello son accesibles desde cualquiera de los puntos de conexión de Exchange de Hola y otras cargas de trabajo de Office 365 que admiten los grupos de Office 365</span><span class="sxs-lookup"><span data-stu-id="950d3-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="950d3-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="950d3-137">Next steps</span></span>
<span data-ttu-id="950d3-138">En estos artículos se proporciona información adicional sobre los grupos de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="950d3-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="950d3-139">Consulta de los grupos existentes</span><span class="sxs-lookup"><span data-stu-id="950d3-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="950d3-140">Administración de la configuración de un grupo</span><span class="sxs-lookup"><span data-stu-id="950d3-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="950d3-141">Administrar miembros de un grupo</span><span class="sxs-lookup"><span data-stu-id="950d3-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="950d3-142">Administrar la pertenencia a grupos</span><span class="sxs-lookup"><span data-stu-id="950d3-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="950d3-143">Administrar reglas dinámicas de los usuarios de un grupo</span><span class="sxs-lookup"><span data-stu-id="950d3-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
