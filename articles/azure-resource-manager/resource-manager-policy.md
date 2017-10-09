---
title: las directivas de recursos aaaAzure | Documentos de Microsoft
description: "Describe cómo se establecen las propiedades de recurso coherente de toouse Azure Resource Manager directivas tooensure durante la implementación. Se pueden aplicar directivas en grupos de suscripción o el recurso de Hola."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a>Información general sobre las directivas de recursos
Las directivas de recursos permiten tooestablish convenciones para los recursos de su organización. La definición de convenciones permite controlar los costes y administrar los recursos más fácilmente. Por ejemplo, puede especificar que se permitan solo determinados tipos de máquinas virtuales. O puede obligar a que todos los recursos tengan una etiqueta concreta. Todos los recursos secundarios heredan las directivas. Por lo tanto, si una directiva aplicada tooa grupo de recursos, es aplicable tooall recursos de hello en ese grupo de recursos.

Hay dos toounderstand conceptos acerca de las directivas:

* definición de directiva - describen cuando se aplica la directiva de Hola y qué acción tootake
* asignación de directiva, aplica ámbito tooa de la definición de la directiva Hola (suscripción o grupo de recursos)

Este tema se centra en la definición de la directiva. Para obtener información acerca de la asignación de directiva, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md) o [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).

Las directivas se evalúan al crear y actualizar los recursos (operaciones PUT y PATCH).

> [!NOTE]
> Actualmente, directiva no evalúa los tipos de recursos que no son compatibles con etiquetas, tipo y ubicación, como el tipo de recurso de hello Microsoft.Resources/deployments. Esta compatibilidad se agregará en el futuro. tooavoid problemas de compatibilidad con versiones anteriores, se debe especificar explícitamente tipo al crear directivas. Por ejemplo, una directiva de etiqueta que no especifique tipos se aplicará a todos los tipos. En ese caso, una implementación de plantilla puede producir un error si hay un recurso anidado que no es compatible con etiquetas y tipo de recurso de implementación de Hola se ha agregado toopolicy evaluación. 
> 
> 

## <a name="how-is-it-different-from-rbac"></a>¿En qué se diferencia de RBAC?
Hay algunas diferencias importantes entre directiva y control de acceso basado en roles (RBAC). RBAC se centra en las acciones del **usuario** en ámbitos diferentes. Por ejemplo, se agregan toohello rol de colaborador para un grupo de recursos en el ámbito de hello deseado, por lo que puede hacer el grupo de recursos de toothat de cambios. La directiva se centra en las propiedades de los **recursos** durante la implementación. Por ejemplo, a través de directivas, puede controlar tipos de Hola de recursos que se pueden aprovisionar. O bien, puede restringir las ubicaciones de hello en el que se pueden aprovisionar recursos Hola. A diferencia de RBAC, la directiva es un sistema que permite de manera predeterminada y niega explícitamente. 

las directivas de toouse, se debe autenticar a través de RBAC. En concreto, la cuenta necesita:

* `Microsoft.Authorization/policydefinitions/write`toodefine una directiva de permisos
* `Microsoft.Authorization/policyassignments/write`tooassign una directiva de permisos 

Estos permisos no se incluyen en hello **colaborador** rol.

## <a name="built-in-policies"></a>Directivas integradas

Azure proporciona algunas definiciones de directivas integradas que pueden reducir el número de Hola de directivas tiene toodefine. Antes de continuar con las definiciones de directiva, debe considerar si una directiva integrada ya proporciona la definición de hello que necesaria. Hola definiciones de directivas integradas son:

* Ubicaciones permitidas
* Tipos de recursos permitidos
* SKU de cuenta de almacenamiento permitida
* SKU de máquina virtual permitida
* Aplicación de etiqueta y valor predeterminado
* Aplicación de etiqueta y valor
* Tipos de recursos no permitidos
* Requisito de la versión 12.0 de SQL Server
* Requisito de cifrado de la cuenta de almacenamiento

Puede asignar cualquiera de estas directivas a través de hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), o [CLI de Azure](resource-manager-policy-create-assign.md#azure-cli).

## <a name="policy-definition-structure"></a>Estructura de definición de directiva
Usar JSON toocreate una definición de directiva. definición de la directiva de Hello contiene elementos para:

* parameters
* nombre para mostrar
* description
* regla de directiva
  * evaluación lógica
  * efecto

Hola de ejemplo siguiente muestra una directiva que limita donde se implementan los recursos:

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a>parameters
Usar parámetros ayuda a simplificar la administración de directivas reduciendo el número de Hola de definiciones de directiva. Definir una directiva para una propiedad de recurso (por ejemplo, para limitar las ubicaciones de Hola donde se pueden implementar los recursos) e incluir parámetros en la definición de Hola. A continuación, reutilizar esa definición de directiva para diferentes escenarios pasando valores diferentes (por ejemplo, para especificar un conjunto de ubicaciones para una suscripción) al asignar la directiva de Hola.

Declarará parámetros al crear las definiciones de directiva.

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

puede ser tipo Hello de un parámetro de cadena o matriz. propiedad de metadatos de Hola se utiliza para herramientas como toodisplay portal Azure simplifica la información. 

En la regla de directiva de hello, hace referencia a parámetros con hello según la sintaxis: 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a>Nombre para mostrar y descripción

Usar hello **displayName** y **descripción** tooidentify Hola definición de directiva y proporcionar un contexto para cuando se utiliza.

## <a name="policy-rule"></a>Regla de directiva

regla de directivas de Hello consta de **si** y **, a continuación,** bloques. Hola **si** bloque, definir una o varias condiciones que especifican cuando se aplica la directiva de Hola. Puede aplicar las condiciones de operadores lógicos toothese tooprecisely definir escenario de Hola para una directiva. Hola **, a continuación,** bloque, definir el efecto de Hola que tiene lugar cuando hello **si** se cumplen estas condiciones.

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a>Operadores lógicos
operadores lógicos de Hello admitido son:

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

Hola **no** sintaxis invierte el resultado de hello de condición de Hola. Hola **todo** sintaxis (toohello similar lógico **y** operación) requiere true de toobe de todas las condiciones. Hola **anyOf** sintaxis (toohello similar lógico **o** operación) requiere true de toobe uno o más condiciones.

Puede anidar los operadores lógicos. Hola siguiente ejemplo se muestra un **no** operación que está anidada dentro de un **todo** operación. 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a>Condiciones
Hola condición se evalúa como si una **campo** cumple determinados criterios. las condiciones de Hello admitido son:

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

Cuando se usa hello **como** condición, puede proporcionar un carácter comodín (*) en el valor de Hola.

Cuando se usa hello **coincide con** condición, proporcione `#` toorepresent un dígito, `?` por una letra y cualquier otro carácter toorepresent ese carácter real. Para obtener ejemplos, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).

### <a name="fields"></a>Fields
Para crear condiciones se usan campos. Un campo representa las propiedades de carga de solicitud de recursos de Hola que es usado toodescribe Hola estado del recurso de Hola.  

se admite Hola siguientes campos:

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* alias de propiedad: para obtener una lista, vea [Alias](#aliases).

### <a name="effect"></a>Efecto
La directiva admite tres tipos de efectos: `deny`, `audit` y `append`. 

* **Denegar** genera un evento en el registro de auditoría de Hola y se produce un error de solicitud de Hola
* **Auditoría** genera un evento de advertencia en el registro de auditoría, pero no se producen errores solicitud Hola
* **Anexar** agrega Hola definido por conjunto de campos toohello solicitud 

Para **anexar**, debe proporcionar Hola detalles siguientes:

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

Hola valor puede ser una cadena o un objeto con formato JSON. 

## <a name="aliases"></a>Alias

Use alias tooaccess específico de propiedades para un tipo de recurso. Los alias permiten toorestrict qué valores o condiciones que se permiten para una propiedad en un recurso. Todos los alias asigna toopaths en las diferentes versiones de API para un tipo de recurso determinado. Durante la evaluación de directivas, motor de directiva de hello Obtiene la ruta de acceso de propiedad de Hola para esa versión de API.

**Microsoft.Cache/Redis**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Cache/Redis/enableNonSslPort | Establecer si (6379) de puerto del servidor de Redis de hello ssl no está habilitado. |
| Microsoft.Cache/Redis/shardCount | Establecer número de Hola de toobe de particiones que se creó en una caché de clúster Premium.  |
| Microsoft.Cache/Redis/sku.capacity | Establecer tamaño de Hola de toodeploy de caché de Redis Hola.  |
| Microsoft.Cache/Redis/sku.family | Establecer toouse familia de SKU de Hola. |
| Microsoft.Cache/Redis/sku.name | Establecer tipo de Hola de caché en Redis toodeploy. |

**Microsoft.Cdn/profiles**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.CDN/profiles/sku.name | Nombre del conjunto de hello del programa Hola a nivel de precios. |

**Microsoft.Compute/disks**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Compute/imageOffer | Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imagePublisher | Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageSku | Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageVersion | Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine. |


**Microsoft.Compute/virtualMachines**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identificador de Hola de máquina virtual de hello imagen utilizada toocreate Hola del conjunto. |
| Microsoft.Compute/imageOffer | Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imagePublisher | Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageSku | Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageVersion | Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine. |
| Microsoft.Compute/licenseType | Establecer esa imagen Hola o disco local con licencia. Este valor solo se usa para imágenes que contienen el sistema operativo de Windows Server de Hola.  |
| Microsoft.Compute/virtualMachines/imageOffer | Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/virtualMachines/imagePublisher | Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola. |
| Microsoft.Compute/virtualMachines/imageSku | Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/virtualMachines/imageVersion | Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine. |
| Microsoft.Compute/virtualMachines/osDisk.Uri | Establecer Hola vhd URI. |
| Microsoft.Compute/virtualMachines/sku.name | Establecer tamaño de Hola de máquina virtual de Hola. |

**Microsoft.Compute/virtualMachines/extensions**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Compute/virtualMachines/extensions/publisher | Nombre del conjunto de hello del publicador de la extensión de Hola. |
| Microsoft.Compute/virtualMachines/extensions/type | Establecer tipo de Hola de extensión. |
| Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion | Establezca la versión de Hola de extensión de Hola. |

**Microsoft.Compute/virtualMachineScaleSets**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Compute/imageId | Identificador de Hola de máquina virtual de hello imagen utilizada toocreate Hola del conjunto. |
| Microsoft.Compute/imageOffer | Oferta de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imagePublisher | Publicador de Hola de conjunto de imagen de la plataforma de Hola o una imagen de marketplace usa máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageSku | Conjunto Hola SKU de imagen de la plataforma de Hola o una imagen de marketplace utiliza máquina virtual de toocreate Hola. |
| Microsoft.Compute/imageVersion | Establecer la versión de Hola de imagen de la plataforma de Hola o una imagen de marketplace usa toocreate Hola virtual machine. |
| Microsoft.Compute/licenseType | Establecer esa imagen Hola o disco local con licencia. Este valor solo se usa para imágenes que contienen el sistema operativo de Windows Server de Hola. |
| Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix | Establezca el prefijo del nombre de equipo de Hola para todas las máquinas virtuales de hello en el conjunto de escalas de Hola. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl | Conjunto Hola URI del blob de imagen de usuario. |
| Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers | Conjunto de direcciones URL de contenedor de Hola que son discos del sistema operativo toostore usado para el conjunto de escalas de Hola. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.name | Establecer tamaño de Hola de máquinas virtuales en un conjunto de escala. |
| Microsoft.Compute/VirtualMachineScaleSets/sku.tier | Establecer nivel de Hola de máquinas virtuales en un conjunto de escala. |
  
**Microsoft.Network/applicationGateways**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Network/applicationGateways/sku.name | Establecer tamaño de Hola de puerta de enlace de Hola. |

**Microsoft.Network/virtualNetworkGateways**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Network/virtualNetworkGateways/gatewayType | Establecer tipo de Hola de esta puerta de enlace de red virtual. |
| Microsoft.Network/virtualNetworkGateways/sku.name | Establecer nombre SKU de puerta de enlace de Hola. |

**Microsoft.Sql/servers**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Sql/servers/version | Establezca la versión de Hola de servidor hello. |

**Microsoft.Sql/databases**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Sql/servers/databases/edition | Establecer la edición de Hola de base de datos de Hola. |
| Microsoft.Sql/servers/databases/elasticPoolName | Nombre del conjunto de Hola de base de datos de hello grupo elástico hello es en. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveId | Establecer Hola configurado servicio objetivo Id. de nivel de base de datos de Hola. |
| Microsoft.Sql/servers/databases/requestedServiceObjectiveName | Nombre del conjunto de Hola de hello configurado objetivo de nivel de servicio de base de datos de Hola.  |

**Microsoft.Sql/elasticpools**

| Alias | Descripción |
| ----- | ----------- |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/dtu | Conjunto Hola total había compartido DTU de grupo elástico de base de datos de Hola. |
| servers/elasticpools | Microsoft.Sql/servers/elasticPools/edition | Establecer la edición de Hola de grupo elástico Hola. |

**Microsoft.Storage/storageAccounts**

| Alias | Descripción |
| ----- | ----------- |
| Microsoft.Storage/storageAccounts/accessTier | Nivel de acceso de hello del conjunto utilizado para la facturación. |
| Microsoft.Storage/storageAccounts/accountType | Establecer el nombre SKU de Hola. |
| Microsoft.Storage/storageAccounts/enableBlobEncryption | Establecer si el servicio de hello cifra los datos de hello tal y como se almacena en el servicio de almacenamiento de blob de Hola. |
| Microsoft.Storage/storageAccounts/enableFileEncryption | Establecer si el servicio de hello cifra los datos de hello tal y como se almacena en el servicio de almacenamiento de archivos de Hola. |
| Microsoft.Storage/storageAccounts/sku.name | Establecer el nombre SKU de Hola. |
| Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly | Establecer https solo tooallow servicio toostorage de tráfico. |


## <a name="policy-examples"></a>Ejemplos de directivas

Hola temas siguientes contiene ejemplos de directivas:

* Para ver ejemplos de directivas de etiqueta, consulte [Apply resource policies for tags](resource-manager-policy-tags.md) (Aplicación de directivas de recursos para etiquetas).
* Para obtener ejemplos de patrones de texto y nomenclatura, vea [Aplicación de directivas de recursos para nombres y texto](resource-manager-policy-naming-convention.md).
* Para obtener ejemplos de las directivas de almacenamiento, consulte [aplicar las cuentas de recursos directivas toostorage](resource-manager-policy-storage.md).
* Para obtener ejemplos de directivas de la máquina virtual, consulte [aplicar directivas de recursos tooLinux máquinas virtuales](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) y [aplicar directivas de recursos tooWindows máquinas virtuales](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)


## <a name="next-steps"></a>Pasos siguientes
* Después de definir una regla de directiva, debe asignarlo tooa ámbito. directivas de tooassign a través del portal de hello, vea [tooassign portal de Azure de uso y administrar las directivas de recursos](resource-manager-policy-portal.md). directivas de tooassign a través de la API de REST, PowerShell o CLI de Azure, consulte [asignar y administrar las directivas a través de la secuencia de comandos](resource-manager-policy-create-assign.md).
* Para obtener instrucciones sobre cómo las empresas pueden usar el Administrador de recursos tooeffectively administrar suscripciones, vea [scaffold Azure enterprise - regulador prescriptiva suscripción](resource-manager-subscription-governance.md).
* esquema de la directiva de Hola se publica en [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

