---
title: Control de acceso basado en aaaRole con REST - Azure AD | Documentos de Microsoft
description: "Administración del control de acceso basado en roles con hello API de REST"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Administrar el Control de acceso basado en roles con hello API de REST
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [CLI de Azure](role-based-access-control-manage-access-azure-cli.md)
> * [API DE REST](role-based-access-control-manage-access-rest.md)

Control de acceso basado en roles (RBAC) en hello portal de Azure y API de Azure Resource Manager le ayuda a administrar la suscripción de tooyour de acceso y recursos en un nivel específico. Con esta característica, puede conceder acceso a los usuarios, grupos o entidades de servicio de Active Directory mediante la asignación de algunos toothem de roles en un ámbito determinado.

## <a name="list-all-role-assignments"></a>Lista de todas las asignaciones de roles
Muestra todas las asignaciones de roles de hello en hello especificado ámbito y subscopes.

las asignaciones de roles de toolist, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/read` operación en el ámbito de Hola. Todas las funciones integradas de Hola se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **obtener** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{api-version}* por 2015-07-01.
3. Reemplace *{filter}* con la condición de Hola que desea que la lista de asignaciones de rol de tooapply toofilter Hola:

   * Lista de las asignaciones de roles para solo hello especifican ámbito, sin incluir las asignaciones de roles de hello en subscopes:`atScope()`    
   * Lista de las asignaciones de roles para solo un usuario, un grupo o una aplicación determinados: `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Lista de asignaciones de roles para un usuario específico, incluidas las heredadas de grupos | `assignedTo('{objectId of user}')`

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a>Obtención de información sobre una asignación de roles
Obtiene información sobre una asignación de roles única especificada por el identificador de asignación de rol de Hola.

tooget obtener información acerca de una asignación de roles, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/read` operación. Todas las funciones integradas de Hola se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **obtener** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{role-assignment-id}* con identificador GUID de Hola Hola de asignación de roles.
3. Reemplace *{api-version}* por 2015-07-01.

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a>Creación de una asignación de roles
Crear una función de asignación en hello especificado ámbito para hello especifica la concesión Hola especificado rol principal.

toocreate una asignación de roles, debe tener acceso demasiado`Microsoft.Authorization/roleAssignments/write` operación. De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **colocar** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello en el que desea toocreate las asignaciones de roles de Hola. Cuando se crea una asignación de roles en un ámbito primario, todos los ámbitos secundarios heredan Hola misma asignación de roles. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1   
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{role-assignment-id}* con un nuevo GUID, que se convierte en identificador GUID de Hola Hola nuevas de asignación de roles.
3. Reemplace *{api-version}* por 2015-07-01.

En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Nombre del elemento | Obligatorio | Tipo | Description |
| --- | --- | --- | --- |
| roleDefinitionId |Sí |String |identificador de Hello del rol de Hola. formato de Hola de identificador hello es:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Sí |String |Id. de objeto de entidad de seguridad de hello Azure AD (usuario, grupo o entidad de servicio) se asigna el rol de hello toowhich. |

### <a name="response"></a>Response
Código de estado: 201

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a>Eliminación de una asignación de roles
Eliminar una asignación de roles en hello especifica ámbito.

toodelete una asignación de roles, debe tener acceso toohello `Microsoft.Authorization/roleAssignments/delete` operación. De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **eliminar** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello en el que desea toocreate las asignaciones de roles de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{role-assignment-id}* con el Id. de asignación de rol de hello GUID.
3. Reemplace *{api-version}* por 2015-07-01.

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a>Lista de todos los roles
Enumera todos los roles de Hola que están disponibles para la asignación en hello especificada ámbito.

roles de toolist, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/read` operación en el ámbito de Hola. Todas las funciones integradas de Hola se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **obtener** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello para el que desea toolist roles Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{api-version}* por 2015-07-01.
3. Reemplace *{filter}* con condición de Hola que tooapply toofilter Hola mi lista de deseos de roles:

   * Lista de roles disponibles para la asignación en hello especifica ámbito y cualquiera de sus ámbitos secundarios:`atScopeAndBelow()`
   * Buscar un rol con un nombre para mostrar exacto: `roleName%20eq%20'{role-display-name}'`. Usar la forma de codificación de dirección URL de Hola de hello exacta DisplayName del rol de Hola. Por ejemplo, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a>Obtención de información sobre un rol
Obtiene información sobre un solo rol especificado por el identificador de definición de rol de Hola. tooget información acerca de una única función utilizando su nombre para mostrar, consulte [enumera todos los roles](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget obtener información acerca de una función, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/read` operación. Todas las funciones integradas de Hola se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **obtener** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello para el que desea toolist las asignaciones de roles de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{identificador de definición de rol}* con identificador GUID de Hola Hola de definición del rol.
3. Reemplace *{api-version}* por 2015-07-01.

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a>Creación de un rol personalizado
Cree un rol personalizado.

toocreate un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/write` operación en todos los hello `AssignableScopes`. De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **colocar** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con hello primera *AssignableScope* de roles personalizados de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles.

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{identificador de definición de rol}* con un nuevo GUID, que se convierte en identificador GUID de Hola de nuevo rol personalizado de Hola.
3. Reemplace *{api-version}* por 2015-07-01.

En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nombre del elemento | Obligatorio | Tipo | Description |
| --- | --- | --- | --- |
| name |Sí |String |Identificador GUID de rol personalizada hello. |
| properties.roleName |Sí |String |Nombre para mostrar del rol personalizado Hola. Tamaño máximo: 128 caracteres. |
| properties.description |No |String |Descripción del rol personalizado Hola. Tamaño máximo: 1024 caracteres. |
| properties.type |Sí |String |Establecer demasiado "CustomRole." |
| properties.permissions.actions |yes |String[] |Una matriz de acción cadenas especificando las operaciones de hello concedidas por roles personalizados de Hola. |
| properties.permissions.notActions |No |String[] |Una matriz de cadenas de acción especificar Hola operaciones tooexclude de las operaciones de hello concedidos por roles personalizados de Hola. |
| properties.assignableScopes |yes |String[] |Una matriz de ámbitos en qué Hola se puede usar el rol personalizado. |

### <a name="response"></a>Response
Código de estado: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a>Actualización de un rol personalizado
Modifique un rol personalizado.

toomodify un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/write` operación en todos los hello `AssignableScopes`. De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **colocar** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con hello primera *AssignableScope* de roles personalizados de Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{identificador de definición de rol}* con identificador GUID de Hola de roles personalizados de Hola.
3. Reemplace *{api-version}* por 2015-07-01.

En el cuerpo de solicitud de hello, proporcionar valores de hello en hello siguiendo el formato:

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| Nombre del elemento | Obligatorio | Tipo | Description |
| --- | --- | --- | --- |
| name |Sí |String |Identificador GUID de rol personalizada hello. |
| properties.roleName |Sí |String |Nombre para mostrar de hello rol personalizado actualizó. |
| properties.description |No |String |Descripción de hello rol personalizado actualizó. |
| properties.type |Sí |String |Establecer demasiado "CustomRole." |
| properties.permissions.actions |yes |String[] |Una matriz de cadenas de acción especificar Hola Hola de toowhich de operaciones había actualizado concede acceso de roles personalizados. |
| properties.permissions.notActions |No |String[] |Una matriz de acción cadenas especificando Hola operaciones tooexclude de las operaciones de hello qué Hola actualiza concesiones de roles personalizados. |
| properties.assignableScopes |yes |String[] |Una matriz de ámbitos en qué Hola se puede usar el rol personalizado actualizado. |

### <a name="response"></a>Response
Código de estado: 201

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a>Eliminación de un rol personalizado
Elimine un rol personalizado.

toodelete un rol personalizado, debe tener acceso demasiado`Microsoft.Authorization/roleDefinitions/delete` operación en todos los hello `AssignableScopes`. De hello funciones integradas solo *propietario* y *Administrador de acceso de usuario* se conceden acceso toothis operación. Para obtener más información sobre las asignaciones de roles y la administración del acceso a los recursos de Azure, consulte [Control de acceso basado en roles de Azure](role-based-access-control-configure.md).

### <a name="request"></a>Solicitud
Hola de uso **eliminar** método con hello siguiente URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Dentro de hello URI, realice Hola siguiendo las sustituciones toocustomize la solicitud:

1. Reemplace *{scope}* con ámbito de hello en el que desea definición de roles de toodelete Hola. Hello en los ejemplos siguientes muestra cómo toospecify Hola ámbito para los diferentes niveles:

   * Suscripción: /subscriptions/{subscription-id}  
   * Grupo de recursos: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1  
   * Recurso: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Reemplace *{identificador de definición de rol}* con identificación de definición de rol de hello GUID de rol personalizada hello.
3. Reemplace *{api-version}* por 2015-07-01.

### <a name="response"></a>Respuesta
Código de estado: 200

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
