---
title: funciones de plantilla de administrador de recursos de aaaAzure - recursos | Documentos de Microsoft
description: Describe hello toouse de funciones en un tooretrieve de valores de la plantilla de Azure Resource Manager acerca de los recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Funciones de recursos para las plantillas de Azure Resource Manager

Administrador de recursos proporciona Hola siguientes funciones para obtener valores de recurso:

* [listKeys y list{Value}](#listkeys)
* [providers](#providers)
* [reference](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [suscripción](#subscription)

tooget valores de parámetros, variables o la implementación actual de hello, consulte [funciones con valores de implementación](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys y list{Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Devuelve Hola valores para cualquier tipo de recurso que admite la operación de lista Hola. el uso más común de Hello es `listKeys`. 

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| resourceName o resourceIdentifier |Sí |cadena |Identificador único para el recurso de Hola. |
| apiVersion |Sí |cadena |Versión de API de estado en tiempo de ejecución de un recurso. Por lo general, en formato de hello, **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor devuelto

Hola devuelve tiene un objeto de listKeys Hola siguiendo el formato:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Otras funciones List tienen diferentes formatos de retorno. formato de hello toosee de una función, inclúyala en hello salidas sección tal y como se muestra en la plantilla de ejemplo de Hola. 

### <a name="remarks"></a>Comentarios

Cualquier operación que comienza por **list** se puede usar como función en la plantilla. Hello las operaciones disponibles incluyen no solo listKeys, pero también las operaciones como `list`, `listAdminKeys`, y `listStatus`. Sin embargo, no puede usar **lista** las operaciones que requieren valores de hello cuerpo de la solicitud. Por ejemplo, hello [lista cuenta SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operación requiere parámetros de cuerpo de solicitud, como *signedExpiry*, por lo que no puede usar dentro de una plantilla.

toodetermine qué tipos de recursos tienen una operación de lista, deberá Hola siguientes opciones:

* Hola de vista [operaciones de API de REST](/rest/api/) para un proveedor de recursos y buscar la lista de operaciones. Por ejemplo, las cuentas de almacenamiento tienen hello [listKeys operación](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Hola de uso [AzureRmProviderOperation Get](/powershell/module/azurerm.resources/get-azurermprovideroperation) cmdlet de PowerShell. Hello en el ejemplo siguiente se obtiene todas las operaciones de lista para las cuentas de almacenamiento:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Usar hello siguiente toofilter Hola sólo la lista de operaciones de comando de CLI de Azure:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Especificar recursos de hello mediante cualquier hello [función resourceId](#resourceid), formato de Hola o `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra cómo los claves principal y secundaria de hello tooreturn de una cuenta de almacenamiento de Hola genera sección.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>providers
`providers(providerNamespace, [resourceType])`

Devuelve información acerca de un proveedor de recursos y sus tipos de recursos admitidos. Si no proporciona un tipo de recurso, función hello devuelve todos los tipos de hello admitida Hola proveedor de recursos.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| providerNamespace |Sí |cadena |Namespace del proveedor de Hola |
| resourceType |No |cadena |tipo de Hola de recurso dentro de hello especifica espacio de nombres. |

### <a name="return-value"></a>Valor devuelto

Cada tipo admitido se devuelve en hello siguiendo el formato: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Matriz de clasificación de hello devuelto no se garantiza que los valores.

### <a name="example"></a>Ejemplo

Hola de ejemplo siguiente muestra cómo toouse Hola función de proveedor:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>reference
`reference(resourceName or resourceIdentifier, [apiVersion])`

Devuelve un objeto que representa el estado de tiempo de ejecución de un recurso.

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| resourceName o resourceIdentifier |Sí |string |Nombre o identificador único de un recurso. |
| apiVersion |No |cadena |Versión de API de hello recurso específico. Incluya este parámetro cuando no se ha aprovisionado el recurso de hello dentro de la misma plantilla. Por lo general, en formato de hello, **aaaa-mm-dd**. |

### <a name="return-value"></a>Valor devuelto

Cada tipo de recurso devuelve propiedades distintas para cada función de la referencia de hello. función Hello no devuelve un solo formato predefinido. toosee Hola propiedades para un tipo de recurso, que devuelven objetos Hola Hola genera sección tal y como se muestra en el ejemplo de Hola.

### <a name="remarks"></a>Comentarios

función de la referencia de Hello deriva su valor desde un estado en tiempo de ejecución y, por tanto, no se puede usar en la sección de variables de Hola. Se puede utilizar en la sección de salidas de una plantilla. 

Mediante la función de la referencia de hello, se declara implícitamente que un recurso depende otro recurso si se aprovisionan recursos Hola al que hace referencia dentro de la misma plantilla. No es necesario propiedad dependsOn de tooalso use Hola. Hello función no se ha evalúa hasta hello recursos que se hace referencia han completado la implementación.

nombres de propiedad de hello toosee y valores para un tipo de recurso, cree una plantilla que devuelve el objeto de hello en la sección de salidas de Hola. Si tiene un recurso existente de ese tipo, la plantilla devuelve objeto Hola sin necesidad de implementar los nuevos recursos. 

Normalmente, se utiliza hello **referencia** función tooreturn un valor determinado de un objeto, como el URI del extremo de blob de Hola o el nombre de dominio completo.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Ejemplo

toodeploy y referencia de recurso de Hola Hola misma plantilla, use:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Hello en el ejemplo siguiente se hace referencia a una cuenta de almacenamiento que no está implementada en esta plantilla. Hello cuenta de almacenamiento ya existe dentro de hello mismo grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Devuelve un objeto que representa el grupo de recursos actual de Hola. 

### <a name="return-value"></a>Valor devuelto

Hola devuelve el objeto se encuentra en hello siguiendo el formato:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Comentarios

Un uso común de la función de grupo de recursos de hello es toocreate recursos Hola misma ubicación que el grupo de recursos de Hola. Hello en el ejemplo siguiente se usa Hola recursos grupo tooassign Hola ubicación de un sitio web.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Ejemplo

Hello plantilla siguiente devuelve las propiedades de Hola Hola del grupo de recursos.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Hello en el ejemplo anterior se devuelve un objeto de hello siguiendo el formato:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Devuelve Hola identificador único de un recurso. Use esta función cuando el nombre del recurso de hello es ambiguo o no se ha aprovisionado en hello misma plantilla. 

### <a name="parameters"></a>parameters

| Parámetro | Obligatorio | Tipo | Descripción |
|:--- |:--- |:--- |:--- |
| subscriptionId |No |Cadena (en formato de GUID) |Valor predeterminado es la suscripción actual de Hola. Especifique este valor cuando necesite tooretrieve un recurso en otra suscripción. |
| resourceGroupName |No |cadena |El valor predeterminado es el grupo de recursos actual. Especifique este valor cuando necesite tooretrieve un recurso en otro grupo de recursos. |
| resourceType |Sí |string |Tipo de recurso, incluido el espacio de nombres del proveedor de recursos. |
| resourceName1 |Sí |cadena |Nombre del recurso. |
| resourceName2 |No |string |Siguiente segmento de nombre de recurso si el recurso está anidado. |

### <a name="return-value"></a>Valor devuelto

identificador de Hola se devuelve en hello siguiendo el formato:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Comentarios

Hello valores de parámetro especificados dependen de si el recurso de hello está en hello mismo grupo de recursos y la suscripción como la implementación actual de Hola.

recursos de hello tooget el Id. de una cuenta de almacenamiento en hello mismo suscripción y el grupo de recursos, use:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

Id. de recurso de hello tooget para una cuenta de almacenamiento en Hola misma suscripción, pero un grupo de recursos diferente, utilice:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Id. de recurso de hello tooget para una cuenta de almacenamiento en una suscripción diferente y el grupo de recursos, use:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

Id. de recurso de hello tooget para una base de datos en otro grupo de recursos, use:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

A menudo, necesita toouse esta función si usa una cuenta de almacenamiento o red virtual en un grupo de recursos alternativos. Hello en el ejemplo siguiente se muestra cómo fácilmente se puede utilizar un recurso de un grupo de recursos externos:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se devuelve Hola Id. de recurso para una cuenta de almacenamiento en grupo de recursos de hello:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hola de salida de hello anterior ejemplo con valores predeterminados de hello es:

| Nombre | Tipo | Valor |
| ---- | ---- | ----- |
| sameRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | String | /subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | String | /subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | String | /subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>suscripción
`subscription()`

Devuelve detalles acerca de la suscripción de hello para la implementación actual de Hola. 

### <a name="return-value"></a>Valor devuelto

función Hello devuelve Hola siguiendo el formato:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Ejemplo

Hello en el ejemplo siguiente se muestra hello suscripción función llamado en la sección de salidas de Hola. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Pasos siguientes
* Para obtener una descripción de las secciones de hello en una plantilla de Azure Resource Manager, consulte [plantillas del Administrador de recursos de Azure de creación](resource-group-authoring-templates.md).
* toomerge varias plantillas, consulte [mediante plantillas vinculadas con el Administrador de recursos de Azure](resource-group-linked-templates.md).
* tooiterate un número especificado de veces al crear un tipo de recurso, vea [crear varias instancias de recursos en el Administrador de recursos de Azure](resource-group-create-multiple.md).
* toosee cómo toodeploy plantilla de Hola que haya creado, vea [implementar una aplicación con la plantilla de Azure Resource Manager](resource-group-template-deploy.md).

