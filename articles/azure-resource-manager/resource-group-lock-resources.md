---
title: cambios de tooprevent de aaaLock recursos de Azure | Documentos de Microsoft
description: Impida que los usuarios actualicen o eliminen recursos de Azure esenciales aplicando un bloqueo para todos los usuarios y roles.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a>Bloquear recursos tooprevent cambios inesperados 
Como administrador, puede que necesite toolock una suscripción, grupo de recursos o recurso tooprevent otros usuarios de su organización accidentalmente eliminen o modifiquen los recursos críticos. Puede establecer nivel de bloqueo de hello demasiado**CanNotDelete** o **ReadOnly**. 

* **CanNotDelete** significa que los usuarios autorizados todavía pueden leer y modificar un recurso, pero no pueden eliminar el recurso de Hola. 
* **ReadOnly** significa que los usuarios autorizados pueden leer un recurso, pero que no se pueden eliminar o actualizar el recurso de Hola. Este bloqueo de la aplicación es similar toorestricting todo autorizado los usuarios toohello permisos concedidos por hello **lector** rol. 

## <a name="how-locks-are-applied"></a>Cómo se aplican los bloqueos

Cuando se aplica un bloqueo en un ámbito primario, todos los recursos dentro de ese ámbito heredan Hola mismo bloqueo. Incluso los recursos que se agreguen posteriormente heredan bloqueo Hola de hello primario. bloqueo de más restrictivo de Hello en la herencia de hello tiene prioridad.

A diferencia de control de acceso basado en roles, se usa administración bloqueos tooapply una restricción a través de todos los usuarios y roles. toolearn acerca de cómo establecer permisos para usuarios y roles, consulte [el Control de acceso basado en roles de Azure](../active-directory/role-based-access-control-configure.md).

Bloqueos del Administrador de recursos aplican solo toooperations que se producen en el plano de administración de hello, que consta de las operaciones enviadas demasiado`https://management.azure.com`. bloqueos de Hello no restringen cómo recursos realizan sus propias funciones. Los cambios de recursos están restringidos, pero no así las operaciones de recursos. Por ejemplo, un bloqueo de solo lectura en una base de datos de SQL no le permitirá eliminar o modificar la base de datos de hello, pero no impiden crear, actualizar o eliminar datos en la base de datos de Hola. Se permiten las transacciones de datos porque esas operaciones no se envían demasiado`https://management.azure.com`.

Aplicar **ReadOnly** puede provocar resultados toounexpected porque algunas operaciones que parezcan como lectura operaciones realmente requieren acciones adicionales. Por ejemplo, colocar una **ReadOnly** bloqueo en una cuenta de almacenamiento impide que todos los usuarios de la lista de claves de Hola. lista de Hello operación de claves se controla a través de una solicitud POST porque Hola devuelve las claves están disponibles para las operaciones de escritura. Para obtener otro ejemplo, colocar una **ReadOnly** bloqueo en un recurso de servicio de aplicaciones evita que Explorador de servidores de Visual Studio muestre archivos de recursos de hello porque esa interacción requiere acceso de escritura.

## <a name="who-can-create-or-delete-locks-in-your-organization"></a>Quién puede crear o eliminar bloqueos en su organización
bloqueos de administración toocreate o delete, debe tener acceso demasiado`Microsoft.Authorization/*` o `Microsoft.Authorization/locks/*` acciones. De hello funciones integradas solo **propietario** y **Administrador de acceso de usuario** se conceden a esas acciones.

## <a name="portal"></a>Portal
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a>Plantilla
Hello en el ejemplo siguiente se muestra una plantilla que crea un bloqueo en una cuenta de almacenamiento. cuenta de almacenamiento de Hello en qué tooapply bloqueo Hola se proporciona como un parámetro. nombre del bloqueo de Hola Hola se crea una concatenando el nombre de recurso de hello con **/Microsoft.Authorization/** y Hola nombre del bloqueo de hello, en este caso **myLock**.

tipo de Hello proporcionado es tipo de recurso de toohello específico. Para el almacenamiento, establezca Hola tipo too"Microsoft.Storage/storageaccounts/providers/locks".

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a>PowerShell
Bloquear implementa recursos con PowerShell de Azure mediante hello [AzureRmResourceLock New](/powershell/module/azurerm.resources/new-azurermresourcelock) comando.

toolock un recurso, proporcione el nombre de hello del recurso de hello, su tipo de recurso y su nombre de grupo de recursos.

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

toolock un grupo de recursos, proporcionar nombre Hola Hola del grupo de recursos.

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

tooget información acerca de un bloqueo, utilice [AzureRmResourceLock Get](/powershell/module/azurerm.resources/get-azurermresourcelock). tooget todos los bloqueos de hello en su suscripción, use:

```powershell
Get-AzureRmResourceLock
```

tooget todos los bloqueos para un recurso, use:

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

tooget todos los bloqueos para un grupo de recursos, use:

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

PowerShell de Azure proporciona otros comandos para bloqueos de trabajo, como [conjunto AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate un bloqueo, y [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete un bloqueo.

## <a name="azure-cli"></a>CLI de Azure

Bloquear implementa recursos con CLI de Azure mediante hello [crear bloqueo az](/cli/azure/lock#create) comando.

toolock un recurso, proporcione el nombre de hello del recurso de hello, su tipo de recurso y su nombre de grupo de recursos.

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

toolock un grupo de recursos, proporcionar nombre Hola Hola del grupo de recursos.

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

tooget información acerca de un bloqueo, utilice [lista de bloqueo az](/cli/azure/lock#list). tooget todos los bloqueos de hello en su suscripción, use:

```azurecli
az lock list
```

tooget todos los bloqueos para un recurso, use:

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

tooget todos los bloqueos para un grupo de recursos, use:

```azurecli
az lock list --resource-group exampleresourcegroup
```

CLI de Azure proporciona otros comandos para bloqueos de trabajo, como [actualización de bloqueo de az](/cli/azure/lock#update) tooupdate un bloqueo, y [bloqueo az eliminar](/cli/azure/lock#delete) toodelete un bloqueo.

## <a name="rest-api"></a>API de REST
Puede bloquear los recursos implementados con hello [API de REST para bloqueos de administración](https://docs.microsoft.com/rest/api/resources/managementlocks). Hola REST API permite toocreate y eliminar bloqueos y recuperar información sobre los bloqueos existentes.

toocreate un bloqueo, ejecute:

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

ámbito de Hello podría ser una suscripción, el grupo de recursos o el recurso. Hola nombre del bloqueo es todo lo que desees bloqueo de hello toocall. Como versión de la API, use **2015-01-01**.

En la solicitud de hello, incluir un objeto JSON que especifica las propiedades de Hola de bloqueo de Hola.

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a>Pasos siguientes
* Para obtener más información sobre cómo trabajar con bloqueos de recursos, consulte [Bloqueo de los recursos de Azure](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)
* toolearn acerca de cómo organizar lógicamente los recursos, consulte [mediante etiquetas tooorganize los recursos](resource-group-using-tags.md)
* toochange un recurso reside a qué grupo de recursos, consulte [grupo de recursos de mover recursos toonew](resource-group-move-resources.md)
* Puede aplicar restricciones y convenciones a través de su suscripción con directivas personalizadas. Para obtener más información, consulte [recursos toomanage de directiva de uso y controlar el acceso](resource-manager-policy.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).

