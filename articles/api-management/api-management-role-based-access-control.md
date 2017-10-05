---
title: Uso del control de acceso basado en rol en Azure API Management | Microsoft Docs
description: "Obtención de información sobre cómo usar los roles integrados y crear roles personalizados en Azure API Management"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: fa757a591d788f52d759bc24accedd3c55149ae7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-role-based-access-control-in-azure-api-management"></a><span data-ttu-id="69196-103">Uso del control de acceso basado en rol en Azure API Management</span><span class="sxs-lookup"><span data-stu-id="69196-103">How to Use Role-Based Access Control in Azure API Management</span></span>
<span data-ttu-id="69196-104">Azure API Management se basa en el control de acceso basado en rol de Azure (RBAC) para habilitar la administración de acceso detallada para servicios y entidades de API Management (por ejemplo, API y directivas).</span><span class="sxs-lookup"><span data-stu-id="69196-104">Azure API Management relies on Azure Role-Based Access Control (RBAC) to enable fine-grained access management for API Management services and entities (e.g., APIs, policies).</span></span> <span data-ttu-id="69196-105">En este artículo se proporciona información general de los roles integrados y personalizados en API Management.</span><span class="sxs-lookup"><span data-stu-id="69196-105">This article gives you an overview of the built-in and custom roles in API Management.</span></span> <span data-ttu-id="69196-106">Si desea obtener más información sobre la administración de acceso en Azure Portal, consulte [Introducción a la administración de acceso en Azure Portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).</span><span class="sxs-lookup"><span data-stu-id="69196-106">If you want more details on access management in the Azure portal, see [Get started with access management in the Azure portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)</span></span>

## <a name="built-in-roles"></a><span data-ttu-id="69196-107">Roles integrados</span><span class="sxs-lookup"><span data-stu-id="69196-107">Built-in Roles</span></span>
<span data-ttu-id="69196-108">API Management actualmente proporciona 3 roles integrados y agregará 2 roles más en un futuro próximo.</span><span class="sxs-lookup"><span data-stu-id="69196-108">API Management currently provides 3 built-in roles and will add 2 more roles in the near future.</span></span> <span data-ttu-id="69196-109">Estos roles pueden asignarse en distintos ámbitos, incluida la suscripción, el grupo de recursos y la instancia individual de API Management.</span><span class="sxs-lookup"><span data-stu-id="69196-109">These roles can be assigned at differnt scopes including subscription, resource group, and individual API Management instance.</span></span> <span data-ttu-id="69196-110">Por ejemplo, si el rol "Lector de servicios de Azure API Management" se asigna a un usuario en el nivel de grupo de recursos, el usuario tendrá acceso de lectura a todas las instancias de API Management dentro del grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="69196-110">For instance, if the "Azure API Management Service Reader" role is assigned to an user at the resource group level, then the user will have read access to all API Management instances inside the resource group.</span></span> 

<span data-ttu-id="69196-111">En la tabla siguiente se proporcionan breves descripciones de los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="69196-111">The following table provides brief descriptions of the built-in roles.</span></span> <span data-ttu-id="69196-112">Estos roles se pueden asignar mediante Azure Portal u otras herramientas, como Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), la [interfaz de la línea de comandos](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli) de Azure y la [API de REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest).</span><span class="sxs-lookup"><span data-stu-id="69196-112">You can assign these roles using the Azure Portal or other tools including Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [Command-line interface](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), and [REST API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest).</span></span> <span data-ttu-id="69196-113">Para obtener detalles sobre la asignación de roles integrados, consulte [Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).</span><span class="sxs-lookup"><span data-stu-id="69196-113">For details about how to assign built-in roles, see [Use role assignments to manage access to your Azure subscription resources](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).</span></span>

| <span data-ttu-id="69196-114">Rol</span><span class="sxs-lookup"><span data-stu-id="69196-114">Role</span></span>          | <span data-ttu-id="69196-115">Acceso de lectura<sup>[1]</sup></span><span class="sxs-lookup"><span data-stu-id="69196-115">Read access<sup>[1]</sup></span></span> | <span data-ttu-id="69196-116">Acceso de escritura<sup>[2]</sup></span><span class="sxs-lookup"><span data-stu-id="69196-116">Write access<sup>[2]</sup></span></span> | <span data-ttu-id="69196-117">Creación, eliminación y escalado del servicio, VPN y configuración de dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="69196-117">Service creation, deletion, scaling, VPN and custom domain configuration</span></span> | <span data-ttu-id="69196-118">Acceso al Portal para editores heredado</span><span class="sxs-lookup"><span data-stu-id="69196-118">Access to legacy Publsiher Portal</span></span> | <span data-ttu-id="69196-119">Descripción</span><span class="sxs-lookup"><span data-stu-id="69196-119">Description</span></span>
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| <span data-ttu-id="69196-120">Colaborador de servicio de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="69196-120">Azure API Management Service Contributor</span></span> | <span data-ttu-id="69196-121">✓</span><span class="sxs-lookup"><span data-stu-id="69196-121">✓</span></span> | <span data-ttu-id="69196-122">✓ </span><span class="sxs-lookup"><span data-stu-id="69196-122">✓</span></span> | <span data-ttu-id="69196-123">✓ </span><span class="sxs-lookup"><span data-stu-id="69196-123">✓</span></span> | <span data-ttu-id="69196-124">✓</span><span class="sxs-lookup"><span data-stu-id="69196-124">✓</span></span> | <span data-ttu-id="69196-125">Superusuario.</span><span class="sxs-lookup"><span data-stu-id="69196-125">Super user.</span></span> <span data-ttu-id="69196-126">Tiene acceso CRUD completo a los servicios y a las entidades de API Management (por ejemplo, API y directivas).</span><span class="sxs-lookup"><span data-stu-id="69196-126">Has full CRUD access to API Management services and entities (e.g., APIs, Policies).</span></span> <span data-ttu-id="69196-127">Tiene acceso al portal del editor heredado.</span><span class="sxs-lookup"><span data-stu-id="69196-127">Has access to the legacy publisher portal.</span></span> |
| <span data-ttu-id="69196-128">Lector de servicio de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="69196-128">Azure API Management Service Reader</span></span> | <span data-ttu-id="69196-129">✓</span><span class="sxs-lookup"><span data-stu-id="69196-129">✓</span></span> | | || <span data-ttu-id="69196-130">Tiene acceso de solo lectura a los servicios y a las entidades de API Management.</span><span class="sxs-lookup"><span data-stu-id="69196-130">Has read-only access to API Management services and entities.</span></span> |
| <span data-ttu-id="69196-131">Operador de servicio de Azure API Management</span><span class="sxs-lookup"><span data-stu-id="69196-131">Azure API Management Service Operator</span></span> | <span data-ttu-id="69196-132">✓</span><span class="sxs-lookup"><span data-stu-id="69196-132">✓</span></span> | | <span data-ttu-id="69196-133">✓</span><span class="sxs-lookup"><span data-stu-id="69196-133">✓</span></span> | | <span data-ttu-id="69196-134">Puede administrar servicios de API Management, pero no entidades.</span><span class="sxs-lookup"><span data-stu-id="69196-134">Can manage API Management services but not entities.</span></span>|
| <span data-ttu-id="69196-135">Editor de servicio de Azure API Management<sup>*</sup></span><span class="sxs-lookup"><span data-stu-id="69196-135">Azure API Management Service Editor<sup>*</sup></span></span> | <span data-ttu-id="69196-136">✓</span><span class="sxs-lookup"><span data-stu-id="69196-136">✓</span></span> | <span data-ttu-id="69196-137">✓</span><span class="sxs-lookup"><span data-stu-id="69196-137">✓</span></span> | |  | <span data-ttu-id="69196-138">Puede administrar entidades de API Management, pero no servicios.</span><span class="sxs-lookup"><span data-stu-id="69196-138">Can manage API Management entities but not services.</span></span>|
| <span data-ttu-id="69196-139">Administrador de contenido de Azure API Management<sup>*</sup></span><span class="sxs-lookup"><span data-stu-id="69196-139">Azure API Management Content Manager<sup>*</sup></span></span> | <span data-ttu-id="69196-140">✓</span><span class="sxs-lookup"><span data-stu-id="69196-140">✓</span></span> | | | <span data-ttu-id="69196-141">✓</span><span class="sxs-lookup"><span data-stu-id="69196-141">✓</span></span> | <span data-ttu-id="69196-142">Puede administrar el portal para desarrolladores.</span><span class="sxs-lookup"><span data-stu-id="69196-142">Can manage developer portal.</span></span> <span data-ttu-id="69196-143">Acceso de solo lectura a servicios y entidades.</span><span class="sxs-lookup"><span data-stu-id="69196-143">Read-only access to services and entities.</span></span>|

<span data-ttu-id="69196-144"><sup>[1] Acceso de lectura a los servicios y a las entidades de API Management (por ejemplo, API y directivas)</sup></span><span class="sxs-lookup"><span data-stu-id="69196-144"><sup>[1] Read access to API Management services and entities (e.g., APIs, policies)</sup></span></span>

<span data-ttu-id="69196-145"><sup>[2] Acceso de escritura a los servicios y a las identidades de API Management, excepto las operaciones siguientes: 1) Creación, eliminación y escalado de instancias 2) Configuración de VPN 3) Configuración personalizada de nombres de dominio</sup></span><span class="sxs-lookup"><span data-stu-id="69196-145"><sup>[2] Write access to API Management services and entities except following opeartions: 1) Instance creation, deletion, and scaling 2) VPN configuration  3) Custom domain name setup</sup></span></span>

<span data-ttu-id="69196-146"><sup>\* El rol Editor de servicio estará disponible una vez migrada toda la IU de administración desde el portal del editor existente a Azure Portal. El rol Administrador de contenido estará disponible después de que el portal del editor se refactorice para que solo contenga funcionalidades relacionadas con la administración del portal para desarrolladores.</sup></span><span class="sxs-lookup"><span data-stu-id="69196-146"><sup>\* The Service Editor role will be available after we migrate all admin UI from the existing publisher portal to the Azure portal. The Content Manager role will be available after the publisher portal is refactored to only contain functionalities related to managing the developer portal.</sup></span></span>  


## <a name="custom-roles"></a><span data-ttu-id="69196-147">Roles personalizados</span><span class="sxs-lookup"><span data-stu-id="69196-147">Custom Roles</span></span>
<span data-ttu-id="69196-148">Si ninguno de los roles integrados satisface sus necesidades específicas, se pueden crear roles personalizados para proporcionar administración de acceso más pormenorizada para entidades de API Management.</span><span class="sxs-lookup"><span data-stu-id="69196-148">If none of the built-in roles meet your specific needs, custom roles can be created to provide more granular access management for API Management entities.</span></span> <span data-ttu-id="69196-149">Por ejemplo, puede crear un rol personalizado que tenga acceso de solo lectura a un servicio de API Management, pero que solo tenga acceso de escritura a una API específica.</span><span class="sxs-lookup"><span data-stu-id="69196-149">For example, you can create a custom role which has read-only access to an API Management service but only has write access to one specific API.</span></span> <span data-ttu-id="69196-150">Para obtener más detalles acerca de los roles personalizados, consulte [Roles personalizados en RBAC de Azure](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles).</span><span class="sxs-lookup"><span data-stu-id="69196-150">To learn more details about custom roles, see [Custom Roles in Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles).</span></span> 

<span data-ttu-id="69196-151">Cuando crea un rol personalizado, es más fácil empezar con uno de los roles integrados.</span><span class="sxs-lookup"><span data-stu-id="69196-151">When you create a custom role, it is easier to start with one of the built-in roles.</span></span> <span data-ttu-id="69196-152">Edite los atributos para agregar los elementos Actions, NotActions o AssignableScopes y luego guarde los cambios como un nuevo rol.</span><span class="sxs-lookup"><span data-stu-id="69196-152">Edit the attributes to add the Actions, NotActions, or AssignableScopes, then save the changes as a new role.</span></span> <span data-ttu-id="69196-153">El ejemplo siguiente comienza con el rol "Lector de servicio de Azure API Managment" y crea un rol personalizado denominado "Editor de API calculadora".</span><span class="sxs-lookup"><span data-stu-id="69196-153">The following example begins with the "Azure API Managment Service Reader" role and creates a custom role called "Calculator API Editor".</span></span> <span data-ttu-id="69196-154">El rol personalizado puede asignarse únicamente a una API específica, por tanto, solo tiene acceso a dicha API.</span><span class="sxs-lookup"><span data-stu-id="69196-154">The custom role can be assigned only to a specific API therefore will only has access to that API.</span></span> 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access to Contoso APIM instance and write access to the Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of the user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a><span data-ttu-id="69196-155">Ver un vídeo de introducción</span><span class="sxs-lookup"><span data-stu-id="69196-155">Watch a Video Overview</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="69196-156">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="69196-156">Next Steps</span></span>

* <span data-ttu-id="69196-157">Más información sobre control de acceso basado en rol en Azure</span><span class="sxs-lookup"><span data-stu-id="69196-157">Learn more about Role-Based Access Control in Azure</span></span>
  * [<span data-ttu-id="69196-158">Introducción a la administración de acceso en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="69196-158">Get started with access management in the Azure portal</span></span>](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [<span data-ttu-id="69196-159">Uso de asignaciones de roles para administrar el acceso a los recursos de la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="69196-159">Use role assignments to manage access to your Azure subscription resources</span></span>](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [<span data-ttu-id="69196-160">Roles personalizados en RBAC de Azure</span><span class="sxs-lookup"><span data-stu-id="69196-160">Custom Roles in Azure RBAC</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)