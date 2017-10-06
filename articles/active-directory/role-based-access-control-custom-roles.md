---
title: aaaCreate roles personalizados para RBAC de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toodefine de roles personalizados con Control de acceso de Azure Role-Based para una administración más pormenorizada de identidad en la suscripción de Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Creación de roles personalizados para el control de acceso basado en roles de Azure
Crear un rol personalizado en el Control de acceso de Azure Role-Based (RBAC) si ninguna de las funciones integradas de hello satisface sus necesidades de acceso específico. Roles personalizados pueden crearse con [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [interfaz de línea de comandos de Azure](role-based-access-control-manage-access-azure-cli.md) (CLI), hello y [API de REST](role-based-access-control-manage-access-rest.md). Al igual que las funciones integradas, puede asignar roles personalizados toousers, grupos y aplicaciones en la suscripción, grupo de recursos y ámbitos de recursos. Los roles personalizados se almacenan en un inquilino de Azure AD y se pueden compartir entre suscripciones.

Cada inquilino puede crear los roles personalizados too2000. 

Hello en el ejemplo siguiente se muestra una función personalizada para la supervisión y reiniciar máquinas virtuales:

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Acciones
Hola **acciones** propiedad de un rol personalizado especifica hello Azure operaciones toowhich Hola función concede acceso. Se trata de una colección de cadenas de operación que identifican a las operaciones protegibles de proveedores de recursos de Azure. Las cadenas de operación seguir el formato de Hola de `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Las cadenas de operación que contienen caracteres comodín (\*) conceder acceso tooall operaciones que coinciden con la cadena de la operación de Hola. Por ejemplo:

* `*/read`concede acceso a las operaciones de tooread para todos los tipos de recursos de todos los proveedores de recursos de Azure.
* `Microsoft.Compute/*`concede acceso a las operaciones de tooall para todos los tipos de recursos de proveedor de recursos de Microsoft.Compute Hola.
* `Microsoft.Network/*/read`concede acceso a las operaciones de tooread para todos los tipos de recursos de proveedor de recursos de Microsoft.Network Hola de Azure.
* `Microsoft.Compute/virtualMachines/*`concede acceso a las operaciones de tooall de máquinas virtuales y sus tipos de recursos secundarios.
* `Microsoft.Web/sites/restart/Action`concede acceso a sitios Web de toorestart.

Use `Get-AzureRmProviderOperation` (en PowerShell) o `azure provider operations show` (en CLI de Azure) operaciones toolist de proveedores de recursos de Azure. También puede usar estas cadenas de operación de comodín tooexpand y tooverify de comandos que una cadena de la operación es válida.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Captura de pantalla de PowerShell: Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Captura de pantalla de la CLI de Azure: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Hola de uso **NotActions** propiedad si conjunto Hola de operaciones que desea tooallow se define más fácilmente mediante la exclusión de operaciones restringidas. Hello acceso concedido por un rol personalizado se calcula restando hello **NotActions** las operaciones de hello **acciones** operaciones.

> [!NOTE]
> Si un usuario está asignado un rol que excluye una operación en **NotActions**y se le asigna un segundo rol que concede acceso toohello es la misma operación, el usuario de hello permite tooperform esa operación. **NotActions** no es una instrucción deny de regla: es simplemente una toocreate de forma adecuada un conjunto de operaciones permitidas cuando las operaciones concretas necesitan toobe excluido.
>
>

## <a name="assignablescopes"></a>Ámbitos asignables
Hola **AssignableScopes** propiedad del rol personalizado Hola especifica los ámbitos de hello (suscripciones, grupos de recursos o recursos) dentro de qué Hola está disponible para la asignación de roles personalizados. Puede realizar disponibles para la asignación de roles personalizados de hello en suscripciones de hello solo o la experiencia de los grupos de recursos que requieren la base de datos y no el usuario de acumulación de elementos de rest de Hola de suscripciones de Hola o grupos de recursos.

Ejemplos de ámbitos asignables válidos son:

* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - pone a disposición para la asignación de rol de hello en dos suscripciones.
* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - pone a disposición para la asignación de rol de hello en una sola suscripción.
* "/ suscripciones/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/red" - hace Hola roles disponibles para la asignación solo en el grupo de recursos de red de Hola.

> [!NOTE]
> Tiene que utilizar al menos una suscripción, grupo de recursos o identificador de recurso.
>
>

## <a name="custom-roles-access-control"></a>Control de acceso de roles personalizados
Hola **AssignableScopes** propiedad de roles personalizados de hello también controla quién puede ver, modificar y eliminar el rol de Hola.

* ¿Quién puede crear un rol personalizado?
    Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden crear roles personalizados para su uso en esos ámbitos.
    usuario que crea el rol de Hola Hola necesita toobe capaz de tooperform `Microsoft.Authorization/roleDefinition/write` operación en todos los hello **AssignableScopes** del rol de Hola.
* ¿Quién puede modificar un rol personalizado?
    Los propietarios (y administradores del acceso de los usuarios) de las suscripciones, los grupos de recursos y los recursos pueden modificar roles personalizados en esos ámbitos. Los usuarios necesitan toobe tooperform capaz de hello `Microsoft.Authorization/roleDefinition/write` operación en todos los hello **AssignableScopes** de un rol personalizado.
* ¿Quién puede ver los roles personalizados?
    Todos los roles integrados de RBAC de Azure permiten ver los roles que están disponibles para la asignación. Los usuarios que pueden realizar hello `Microsoft.Authorization/roleDefinition/read` operación en un ámbito puede ver los roles RBAC Hola que están disponibles para la asignación en ese ámbito.

## <a name="see-also"></a>Otras referencias
* [Control de acceso basado en roles](role-based-access-control-configure.md): comience a usar RBAC en hello portal de Azure.
* Obtenga información acerca de cómo tener acceso toomanage con:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [CLI de Azure](role-based-access-control-manage-access-azure-cli.md)
  * [API DE REST](role-based-access-control-manage-access-rest.md)
* [Funciones integradas](role-based-access-built-in-roles.md): obtener detalles acerca de los roles de Hola que vienen en RBAC.
