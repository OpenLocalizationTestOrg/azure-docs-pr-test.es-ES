---
title: aaaAzure proveedores de recursos y tipos de recursos | Documentos de Microsoft
description: Describe los proveedores de recursos de Hola que admiten el Administrador de recursos, sus esquemas y las versiones disponibles de API y regiones de Hola que pueden contener recursos de Hola.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a>Tipos y proveedores de recursos

Al implementar los recursos, con frecuencia necesitan tooretrieve información acerca de proveedores de recursos de Hola y tipos. En este artículo, aprenderá a:

* Ver todos los proveedores de recursos de Azure
* Comprobar el estado de registro de un proveedor de recursos
* Registrar un proveedor de recursos
* Ver los tipos de recursos de un proveedor
* Ver las ubicaciones válidas de un tipo de recurso
* Ver las versiones de API válidas de un tipo de recurso

Puede realizar estos pasos a través del portal de hello, PowerShell o CLI de Azure.

## <a name="powershell"></a>PowerShell

toosee todos los proveedores de recursos de Azure y el estado de registro de hello para su suscripción, usan:

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

Que devuelve resultados similares a:

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola. ámbito de Hello para el registro siempre es suscripción Hola. De forma predeterminada, muchos proveedores de recursos se registran automáticamente. Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos. tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos. Esta operación se incluye en los roles de propietario y Hola colaborador.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Que devuelve resultados similares a:

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.

toosee información de un proveedor de recursos determinado, use:

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

Que devuelve resultados similares a:

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

tipos de recursos de hello toosee para un proveedor de recursos, use:

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

Que devuelve:

```powershell
batchAccounts
operations
locations
locations/quotas
```

versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola. Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST. 

versiones API tooget Hola disponibles para un tipo de recurso, use:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

Que devuelve:

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones. Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola. 

usar ubicaciones de hello admite tooget para un tipo de recurso.

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

Que devuelve:

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a>CLI de Azure
toosee todos los proveedores de recursos de Azure y el estado de registro de hello para su suscripción, usan:

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

Que devuelve resultados similares a:

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola. ámbito de Hello para el registro siempre es suscripción Hola. De forma predeterminada, muchos proveedores de recursos se registran automáticamente. Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos. tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos. Esta operación se incluye en los roles de propietario y Hola colaborador.

```azurecli
az provider register --namespace Microsoft.Batch
```

Que devuelve un mensaje que indica que el registro está en curso.

No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.

toosee información de un proveedor de recursos determinado, use:

```azurecli
az provider show --namespace Microsoft.Batch
```

Que devuelve resultados similares a:

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

tipos de recursos de hello toosee para un proveedor de recursos, use:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

Que devuelve:

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola. Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST. 

versiones API tooget Hola disponibles para un tipo de recurso, use:

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

Que devuelve:

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones. Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola. 

usar ubicaciones de hello admite tooget para un tipo de recurso.

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

Que devuelve:

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a>Portal

Seleccione todos los proveedores de recursos de Azure y el estado de registro de hello para la suscripción de toosee **suscripciones**.

![selección de suscripciones](./media/resource-manager-supported-services/select-subscriptions.png)

Elija Hola suscripción tooview.

![especificación de la suscripción](./media/resource-manager-supported-services/subscription.png)

Seleccione **proveedores de recursos** y ver la lista de Hola de proveedores de recursos disponibles.

![vista de los proveedores de recursos](./media/resource-manager-supported-services/show-resource-providers.png)

Registrar un proveedor de recursos configura el toowork de suscripción con el proveedor de recursos de Hola. ámbito de Hello para el registro siempre es suscripción Hola. De forma predeterminada, muchos proveedores de recursos se registran automáticamente. Sin embargo, puede que necesite toomanually registrar algunos proveedores de recursos. tooregister un proveedor de recursos, debe tener Hola de permiso tooperform `/register/action` operación Hola proveedor de recursos. Esta operación se incluye en los roles de propietario y Hola colaborador. Seleccione un proveedor de recursos, tooregister **registrar**.

![registro del proveedor de recursos](./media/resource-manager-supported-services/register-provider.png)

No se puede anular el registro de un proveedor de recursos si todavía dispone de tipos de recursos de ese proveedor de recursos en la suscripción.

información de toosee para un proveedor de recursos determinado, seleccione **más servicios**.

![selección de más servicios](./media/resource-manager-supported-services/more-services.png)

Busque **Resource Explorer** y selecciónelo en las opciones disponibles de Hola.

![selección de resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

Seleccione **Proveedores**.

![Selección de proveedores](./media/resource-manager-supported-services/select-providers.png)

Recursos y proveedor de recursos de hello Seleccione tipo que desea tooview.

![Selección del tipo de recurso](./media/resource-manager-supported-services/select-resource-type.png)

El Administrador de recursos se admite en todas las regiones, pero podrían no admitir recursos Hola que implementar en todas las regiones. Además, puede haber limitaciones en la suscripción que impide utilizar algunas regiones que admiten recurso Hola. Explorador de recursos de Hello muestra ubicaciones válidas para el tipo de recurso de Hola.

![Vista de las ubicaciones](./media/resource-manager-supported-services/show-locations.png)

versión de la API de Hello corresponde versión tooa de operaciones de API de REST que se publican en proveedor de recursos de Hola. Como un proveedor de recursos permite ofrecer nuevas características, lanza una nueva versión de hello API de REST. Explorador de recursos de Hello muestra las versiones de API válidas para el tipo de recurso de Hola.

![Vista de las versiones de API](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a>Pasos siguientes
* toolearn acerca de cómo crear plantillas de administrador de recursos, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toolearn sobre la implementación de recursos, consulte [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).
* operaciones de hello tooview para un proveedor de recursos, consulte [API de REST de Azure](/rest/api/).

