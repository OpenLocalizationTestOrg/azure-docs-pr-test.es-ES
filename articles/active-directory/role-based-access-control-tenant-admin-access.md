---
title: "administración de aaaTenant elevar acceso - Azure AD | Documentos de Microsoft"
description: Este tema describe Hola integrada en roles para el control de acceso basado en roles (RBAC).
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
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="1b405-103">Elevación del acceso como administrador de inquilinos con Control de acceso basado en rol</span><span class="sxs-lookup"><span data-stu-id="1b405-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="1b405-104">El control de acceso basado en rol ayuda a los administradores de inquilinos a obtener elevaciones temporales de acceso para que puedan conceder permisos superiores a lo normal.</span><span class="sxs-lookup"><span data-stu-id="1b405-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="1b405-105">Un administrador de inquilinos puede elevar su propio rol de administrador de acceso de usuario de toohello cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="1b405-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="1b405-106">Ese rol otorga hello toogrant de permisos de administrador de inquilinos mismo u otros roles en hello ámbito "/".</span><span class="sxs-lookup"><span data-stu-id="1b405-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="1b405-107">Esta característica es importante porque permite a inquilino hello toosee administrador que todos Hola suscripciones que existen en una organización.</span><span class="sxs-lookup"><span data-stu-id="1b405-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="1b405-108">También permite automatización aplicaciones (por ejemplo, facturación y auditoría) tooaccess todas las suscripciones de Hola y proporcionar una vista precisa del estado de Hola de organización de hello para la administración de activos o de facturación.</span><span class="sxs-lookup"><span data-stu-id="1b405-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="1b405-109">Cómo toouse elevateAccess toogive inquilinos acceso</span><span class="sxs-lookup"><span data-stu-id="1b405-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="1b405-110">proceso básico de Hello funciona con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="1b405-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="1b405-111">Con REST, llame a *elevateAccess*, que concede Hola rol de administrador de acceso de usuario en "/" definir el ámbito.</span><span class="sxs-lookup"><span data-stu-id="1b405-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="1b405-112">Crear un [asignación de roles](/rest/api/authorization/roleassignments) tooassign cualquier rol en cualquier ámbito.</span><span class="sxs-lookup"><span data-stu-id="1b405-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="1b405-113">Hola siguiente ejemplo muestra propiedades de Hola para asignar Hola rol lector en "/" ámbito:</span><span class="sxs-lookup"><span data-stu-id="1b405-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="1b405-114">Mientras sea administrador de accesos de usuario, también podrá eliminar asignaciones de roles en el ámbito "/".</span><span class="sxs-lookup"><span data-stu-id="1b405-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="1b405-115">Revoque sus privilegios de administrador de accesos de usuario hasta que se vuelva a necesitar.</span><span class="sxs-lookup"><span data-stu-id="1b405-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="1b405-116">¿Cómo tooundo Hola elevateAccess acción</span><span class="sxs-lookup"><span data-stu-id="1b405-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="1b405-117">Cuando se llama a *elevateAccess* crear una asignación de roles por sí mismo, por lo que toorevoke los privilegios necesita toodelete Hola asignación.</span><span class="sxs-lookup"><span data-stu-id="1b405-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="1b405-118">Llame a [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) donde roleName = toodetermine de administrador de acceso de usuario Hola nombre GUID del rol de administrador de acceso de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b405-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="1b405-119">respuesta de Hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="1b405-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
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

    <span data-ttu-id="1b405-120">Guardar Hola GUID de hello *nombre* parámetro, en este caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="1b405-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="1b405-121">Llame a [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), donde principalId = su propia ObjectId.</span><span class="sxs-lookup"><span data-stu-id="1b405-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="1b405-122">Esta acción muestra todas las asignaciones de sus inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b405-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="1b405-123">Busque Hola uno donde hello ámbito es "/" y hello RoleDefinitionId termina con el rol de hello nombre GUID que se encuentra en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="1b405-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="1b405-124">asignación de roles de Hello debería tener este aspecto:</span><span class="sxs-lookup"><span data-stu-id="1b405-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="1b405-125">Una vez más, guardar Hola GUID de hello *nombre* parámetro, en este caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="1b405-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="1b405-126">Por último, llame a [roleAssignments DELETE](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) donde roleAssignmentId = Hola nombre GUID que se encuentra en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="1b405-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b405-127">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b405-127">Next steps</span></span>

- <span data-ttu-id="1b405-128">Obtener más información sobre la [administración del control de acceso basado en rol con REST](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="1b405-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="1b405-129">[Administrar asignaciones de acceso](role-based-access-control-manage-assignments.md) Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="1b405-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
