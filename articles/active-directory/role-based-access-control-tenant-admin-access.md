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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Elevación del acceso como administrador de inquilinos con Control de acceso basado en rol

El control de acceso basado en rol ayuda a los administradores de inquilinos a obtener elevaciones temporales de acceso para que puedan conceder permisos superiores a lo normal. Un administrador de inquilinos puede elevar su propio rol de administrador de acceso de usuario de toohello cuando sea necesario. Ese rol otorga hello toogrant de permisos de administrador de inquilinos mismo u otros roles en hello ámbito "/".

Esta característica es importante porque permite a inquilino hello toosee administrador que todos Hola suscripciones que existen en una organización. También permite automatización aplicaciones (por ejemplo, facturación y auditoría) tooaccess todas las suscripciones de Hola y proporcionar una vista precisa del estado de Hola de organización de hello para la administración de activos o de facturación.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Cómo toouse elevateAccess toogive inquilinos acceso

proceso básico de Hello funciona con hello pasos:

1. Con REST, llame a *elevateAccess*, que concede Hola rol de administrador de acceso de usuario en "/" definir el ámbito.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Crear un [asignación de roles](/rest/api/authorization/roleassignments) tooassign cualquier rol en cualquier ámbito. Hola siguiente ejemplo muestra propiedades de Hola para asignar Hola rol lector en "/" ámbito:

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

3. Mientras sea administrador de accesos de usuario, también podrá eliminar asignaciones de roles en el ámbito "/".

4. Revoque sus privilegios de administrador de accesos de usuario hasta que se vuelva a necesitar.


## <a name="how-tooundo-hello-elevateaccess-action"></a>¿Cómo tooundo Hola elevateAccess acción

Cuando se llama a *elevateAccess* crear una asignación de roles por sí mismo, por lo que toorevoke los privilegios necesita toodelete Hola asignación.

1.  Llame a [roleDefinitions GET](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) donde roleName = toodetermine de administrador de acceso de usuario Hola nombre GUID del rol de administrador de acceso de usuario de Hola. respuesta de Hello debería tener este aspecto:

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

    Guardar Hola GUID de hello *nombre* parámetro, en este caso **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Llame a [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), donde principalId = su propia ObjectId. Esta acción muestra todas las asignaciones de sus inquilino de Hola. Busque Hola uno donde hello ámbito es "/" y hello RoleDefinitionId termina con el rol de hello nombre GUID que se encuentra en el paso 1. asignación de roles de Hello debería tener este aspecto:

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

    Una vez más, guardar Hola GUID de hello *nombre* parámetro, en este caso **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Por último, llame a [roleAssignments DELETE](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) donde roleAssignmentId = Hola nombre GUID que se encuentra en el paso 2.

## <a name="next-steps"></a>Pasos siguientes

- Obtener más información sobre la [administración del control de acceso basado en rol con REST](role-based-access-control-manage-access-rest.md)

- [Administrar asignaciones de acceso](role-based-access-control-manage-assignments.md) Hola portal de Azure
