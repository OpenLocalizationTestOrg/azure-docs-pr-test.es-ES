---
title: "aaaHow tooUse Control de acceso basado en roles en la administración de API de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola roles integrados y cómo crear roles personalizados en la administración de API de Azure"
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
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>¿Cómo tooUse basada en funciones de Control de acceso en la administración de API de Azure
Administración de API de Azure se basa en la administración de acceso específica de tooenable de Control de acceso de Azure Role-Based (RBAC) para los servicios de administración de API y entidades (por ejemplo, API, las directivas). Este artículo proporciona una visión general de las funciones integradas y personalizadas de hello en administración de API. Si desea obtener más información sobre la administración de acceso en hello portal de Azure, consulte [comenzar con la administración de acceso de hello portal de Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Roles integrados
Administración de API actualmente proporciona 3 funciones integradas y agregará 2 más roles en hello futuro próximo. Estos roles pueden asignarse en distintos ámbitos, incluida la suscripción, el grupo de recursos y la instancia individual de API Management. Por ejemplo, si rol de "Lectura de servicio de administración de API de Azure" Hola se asigna a tooan usuario en el nivel de grupo de recursos de hello, a continuación, hello usuario tendrá acceso de lectura tooall administración de API instancias dentro del grupo de recursos de Hola. 

Hello tabla siguiente proporciona una breve descripción del programa Hola a funciones integradas. Puede asignar estas funciones mediante Hola Portal de Azure u otras herramientas incluido Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [interfaz de línea de comandos](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), y [API de REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Para obtener más información acerca de cómo tooassign funciones integradas, consulte [usar recursos de suscripción de Azure de rol asignaciones toomanage acceso tooyour](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rol          | Acceso de lectura<sup>[1]</sup> | Acceso de escritura<sup>[2]</sup> | Creación, eliminación y escalado del servicio, VPN y configuración de dominio personalizado | Acceso toolegacy Publsiher Portal | Descripción
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Colaborador de servicio de Azure API Management | ✓ | ✓  | ✓  | ✓ | Superusuario. Tiene completa CRUD acceso a servicios de administración de tooAPI y entidades (por ejemplo, las API, las directivas). Tiene acceso toohello publicador heredado portal. |
| Lector de servicio de Azure API Management | ✓ | | || Tiene entidades y servicios de administración de tooAPI de acceso de solo lectura. |
| Operador de servicio de Azure API Management | ✓ | | ✓ | | Puede administrar servicios de API Management, pero no entidades.|
| Editor de servicio de Azure API Management<sup>*</sup> | ✓ | ✓ | |  | Puede administrar entidades de API Management, pero no servicios.|
| Administrador de contenido de Azure API Management<sup>*</sup> | ✓ | | | ✓ | Puede administrar el portal para desarrolladores. Acceso de solo lectura tooservices y entidades.|

<sup>[1] servicios de administración de acceso de lectura tooAPI y entidades (por ejemplo, API, las directivas)</sup>

<sup>Servicios de administración de acceso de escritura de [2] tooAPI y las entidades, excepto opeartions siguiente: 1) instancia creación, eliminación y ajuste de escala en configuración de nombre de dominio VPN (2) configuración personalizada (3)</sup>

<sup>\*rol de Editor de servicio de Hello estarán disponible tras se migran todos los administradores de interfaz de usuario de hello existente publicador portal toohello portal de Azure. Hello rol Administrador de contenido estará disponible después de que se ha refactorizado portal para desarrolladores de hello tooonly contienen portal para desarrolladores de funcionalidades relacionadas toomanaging Hola.</sup>  


## <a name="custom-roles"></a>Roles personalizados
Si ninguna de las funciones integradas de hello satisfacer sus necesidades específicas, roles personalizados pueden crearse tooprovide más granulares access management para entidades de la administración de API. Por ejemplo, puede crear un rol personalizado que tiene acceso de solo lectura tooan servicio de administración de API, pero solo tiene API específica de tooone de acceso de escritura. toolearn obtener más información sobre los roles personalizados, consulte [Roles personalizados en Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Cuando se crea un rol personalizado, es más fácil toostart con una de las funciones integradas de Hola. Editar Hola atributos tooadd acciones de hello, NotActions o AssignableScopes, a continuación, guarde cambios Hola como un nuevo rol. Hello en el ejemplo siguiente se comienza con el rol de "Lector de servicio de administración de API de Azure" hello y crea un rol personalizado denominado "Editor de API de calculadora". roles personalizados de Hola se pueden asignar solo tooa que API específica por lo tanto, sólo estarán tiene acceso toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Ver un vídeo de introducción

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Pasos siguientes

* Más información sobre control de acceso basado en rol en Azure
  * [Empezar a trabajar con la administración de acceso de hello portal de Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Usar recursos de rol asignaciones toomanage acceso tooyour suscripción de Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Roles personalizados en RBAC de Azure](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
