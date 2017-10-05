---
title: "Elevación del acceso para administradores de inquilinos - Azure AD | Microsoft Docs"
description: En este tema se describen los roles integrados para el control de acceso basado en roles (RBAC).
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="7a1b0-103">Elevación del acceso como administrador de inquilinos con Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="7a1b0-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="7a1b0-104">El control de acceso basado en rol ayuda a los administradores de inquilinos a obtener elevaciones temporales de acceso para que puedan conceder permisos superiores a lo normal.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="7a1b0-105">Un administrador de inquilinos puede elevarse el permiso así mismo al rol de administrador de acceso de usuario cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="7a1b0-106">Ese rol otorga al administrador de inquilinos permisos para concederse a sí mismo otros roles en el ámbito "/".</span><span class="sxs-lookup"><span data-stu-id="7a1b0-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="7a1b0-107">Esta característica es importante porque permite al administrador de inquilinos ver todas las suscripciones que existen en una organización.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="7a1b0-108">También permite a las aplicaciones de automatización (por ejemplo, facturación y auditoría) tener acceso a todas las suscripciones y proporcionar una vista precisa del estado de la organización en la administración de recursos o de facturación.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="7a1b0-109">Uso de elevateAccess para ofrecer acceso de inquilino</span><span class="sxs-lookup"><span data-stu-id="7a1b0-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="7a1b0-110">El proceso básico funciona con los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="7a1b0-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="7a1b0-111">Mediante REST, llame a *elevateAccess*, que le concede el rol de administrador de acceso de usuario en el ámbito "/".</span><span class="sxs-lookup"><span data-stu-id="7a1b0-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="7a1b0-112">Cree una [asignación de roles](/rest/api/authorization/roleassignments) para asignar cualquier rol en cualquier ámbito.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="7a1b0-113">En el ejemplo siguiente se muestran las propiedades para asignar el rol de lector en el ámbito "/":</span><span class="sxs-lookup"><span data-stu-id="7a1b0-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="7a1b0-114">Mientras sea administrador de accesos de usuario, también podrá eliminar asignaciones de roles en el ámbito "/".</span><span class="sxs-lookup"><span data-stu-id="7a1b0-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="7a1b0-115">Revoque sus privilegios de administrador de accesos de usuario hasta que se vuelva a necesitar.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="7a1b0-116">Deshacer la acción elevateAccess</span><span class="sxs-lookup"><span data-stu-id="7a1b0-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="7a1b0-117">Cuando se llama a *elevateAccess*, se crea una asignación de roles para usted mismo, por lo que para revocar esos privilegios debe eliminar la asignación.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="7a1b0-118">Llame a [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get), donde roleName = Administrador de accesos de usuario para determinar el GUID del nombre del rol de administrador de accesos de usuario.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="7a1b0-119">La respuesta debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7a1b0-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="7a1b0-120">Guarde el GUID del parámetro *name*, en este caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="7a1b0-121">Llame a [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), donde principalId = su propia ObjectId.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="7a1b0-122">Esto muestra todas las asignaciones en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="7a1b0-123">Busque aquella donde el ámbito es "/" y el RoleDefinitionId termina con el GUID del nombre de rol que encontró en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="7a1b0-124">La asignación de roles debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="7a1b0-124">The role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="7a1b0-125">Una vez más, guarde el GUID del parámetro *name*, en este caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="7a1b0-126">Por último, llame a [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById), donde roleAssignmentId = el GUID del nombre que encontró en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="7a1b0-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a1b0-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7a1b0-127">Next steps</span></span>

- <span data-ttu-id="7a1b0-128">Obtener más información sobre la [administración del control de acceso basado en rol con REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="7a1b0-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="7a1b0-129">[Administrar asignaciones de acceso](role-based-access-control-manage-assignments.md) en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a1b0-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
