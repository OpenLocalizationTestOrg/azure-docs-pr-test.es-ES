---
title: "plantillas de conjunto de aaaLearn acerca de la escala de máquinas virtuales | Documentos de Microsoft"
description: "Obtenga información acerca de toocreate una escala mínima viable establece plantilla para conjuntos de escalas de máquina virtual"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Más información sobre las plantillas de conjuntos de escalado de máquinas virtuales
[Plantillas de administrador de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) es una excelente manera toodeploy grupos de recursos relacionados. Esta serie de tutoriales se muestra cómo toocreate una escala mínima viable establece plantilla y cómo toomodify esta toosuit plantilla diversos escenarios. Todos los ejemplos proceden de este [repositorio de GitHub](https://github.com/gatneil/mvss). 

Esta plantilla es previsto toobe simple. Para obtener ejemplos más completos de escala definir plantillas, consulte hello [repositorio de GitHub de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) y busque las carpetas que contienen la cadena de hello `vmss`.

Si ya está familiarizado con la creación de plantillas, puede omitir toohello toosee de sección "Pasos siguientes" ¿cómo toomodify esta plantilla.

## <a name="review-hello-template"></a>Plantilla de Hola de revisión

Usar GitHub tooreview nuestra escala mínima viable establece plantilla, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

En este tutorial, se examina Hola diff (`git diff master minimum-viable-scale-set`) toocreate Hola mínimo viable conjunto de escalado de plantilla parte por parte.

## <a name="define-schema-and-contentversion"></a>Definición de $schema y contentVersion
En primer lugar, definimos `$schema` y `contentVersion` en plantilla Hola. Hola `$schema` elemento define la versión de Hola de idioma de plantilla de Hola y se utiliza para el resaltado de sintaxis de Visual Studio y las características de validación similar. Hola `contentVersion` elemento no se usa en Azure. En su lugar, le ayuda a realizar un seguimiento de la versión de la plantilla de Hola.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Definición de parámetros
Después, definimos dos parámetros, `adminUsername` y `adminPassword`. Los parámetros son valores que especifique en el momento de saludo de la implementación. Hola `adminUsername` parámetro es simplemente una `string` tipo, sino también porque `adminPassword` es un secreto, proporcionamos a tipo `securestring`. Más adelante, estos parámetros se pasan a la configuración de conjunto de escalado de Hola.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Definición de variables
Plantillas de administrador de recursos también le permiten definir toobe de variables que se usará más adelante en la plantilla de Hola. El ejemplo no utiliza las variables, por lo que hemos dejado objeto JSON de hello vacía.

```json
  "variables": {},
```

## <a name="define-resources"></a>Definición de recursos
A continuación figura la sección de recursos de Hola de plantilla de Hola. Aquí, definir lo que realmente desea toodeploy. A diferencia de `parameters` y `variables` (que son objetos), `resources` es una lista JSON de objetos JSON.

```json
   "resources": [
```

Todos los recursos requieren las propiedades `type`, `name`, `apiVersion` y `location`. El primer recurso de este ejemplo tiene el tipo `Microsft.Network/virtualNetwork`, el nombre `myVnet` y el valor de apiVersion `2016-03-30`. (versión API toofind hello más reciente para un tipo de recurso, vea hello [documentación de la API de REST de Azure](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Especificación de ubicación
ubicación de hello toospecify para la red virtual de hello, usamos un [función de plantilla de administrador de recursos](../azure-resource-manager/resource-group-template-functions.md). Esta función debe estar entre comillas y corchetes de la siguiente manera: `"[<template-function>]"`. En este caso, usamos hello `resourceGroup` función. Toma ningún argumento y devuelve un objeto JSON con metadatos sobre esta implementación se está implementando en el grupo de recursos de Hola. grupo de recursos de Hola se establece por usuario de hello en tiempo de Hola de implementación. Después, se índice en este objeto JSON con `.location` ubicación de hello tooget desde un objeto JSON Hola.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Especificación de las propiedades de la red virtual
Cada recurso de administrador de recursos tiene su propio `properties` sección de recursos de toohello específico de configuraciones. En este caso, especificamos red virtual Hola debe tener una subred con el intervalo de direcciones IP privadas de hello `10.0.0.0/16`. Un conjunto de escalado siempre está dentro de una subred, y no puede abarcar subredes.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Incorporación de la lista dependsOn
Además requiere toohello `type`, `name`, `apiVersion`, y `location` propiedades, cada recurso pueden tener una función opcional `dependsOn` lista de cadenas. Esta lista especifica qué otros recursos de esta implementación deben finalizar antes de implementar este recurso.

En este caso, hay solo un elemento de lista de hello, red virtual de hello del anterior ejemplo de Hola. Especificamos esta dependencia porque escala Hola conjunto requiere Hola red tooexist antes de crear todas las máquinas virtuales. De esta manera, conjunto de escalas de hello puede dar a estas direcciones IP privadas de máquinas virtuales de intervalo de direcciones IP de hello especificado anteriormente hello en Propiedades de red. formato de Hola de cada cadena en la lista de dependsOn de hello es `<type>/<name>`. Use Hola mismo `type` y `name` usado previamente en la definición de recursos de red virtual de Hola.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Especificación de propiedades de conjunto de escalado
Conjuntos de escalas tienen muchas propiedades para personalizar las máquinas virtuales de hello en el conjunto de escalas de Hola. Para obtener una lista completa de estas propiedades, vea hello [conjunto de escalado de documentación de la API de REST](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). En ese tutorial solo establecemos algunas propiedades de uso frecuente.
### <a name="supply-vm-size-and-capacity"></a>Suministro de capacidad y tamaño de máquina virtual
escala de Hello establece necesidades tooknow qué tamaño de VM toocreate ("nombre de sku") y cuántos tal toocreate de máquinas virtuales ("capacidad de sku"). toosee los tamaños de VM están disponibles, vea hello [documentación de tamaños de máquina virtual](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Elección del tipo de actualizaciones
conjunto de escalas de Hello también debe tooknow cómo toohandle se actualiza en el conjunto de escalas de Hola. En estos momentos hay dos opciones, `Manual` y `Automatic`. Para obtener más información sobre las diferencias de hello entre dos hello, consulte la documentación de hello en [cómo tooupgrade un conjunto de escalado de](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Elección del sistema operativo de la máquina virtual
escala de Hello establece necesidades tooknow qué tooput de sistema operativo en máquinas virtuales de Hola. En este caso, creamos hello las máquinas virtuales con una imagen de 16.04 LTS Ubuntu totalmente revisada.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Especificación de computerNamePrefix
conjunto de escalas de Hello implementa varias máquinas virtuales. En lugar de especificar el nombre de cada máquina virtual, especificamos `computerNamePrefix`. Hello conjunto de escalas de anexa un prefijo de toohello de índice para cada máquina virtual, por lo que los nombres de las VM tienen el formato de hello `<computerNamePrefix>_<auto-generated-index>`.

En hello siguiente fragmento de código, utilizamos parámetros Hola de antes de tooset Hola administrador username y password para todas las máquinas virtuales en el conjunto de escalas de Hola. Hacer esto con hello `parameters` función de plantilla. Esta función toma una cadena que especifica qué tooand toorefer de parámetro genera el valor de Hola para ese parámetro.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Especificación de la red de máquina virtual
Por último, necesitamos toospecify configuración de red de Hola para máquinas virtuales de hello en el conjunto de escalas de Hola. En este caso, únicamente se necesita toospecify Hola identificador de subred de Hola que creó anteriormente. Esto indica a escala Hola establece tooput interfaces de red de hello en esta subred.

Puede obtener Id. de Hola de red virtual de Hola que contiene la subred de hello mediante el uso de hello `resourceId` función de plantilla. Esta función toma el tipo de Hola y el nombre de un recurso y devuelve Hola identificador completo de ese recurso. Este identificador tiene forma de hello:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Sin embargo, identificador de Hola de red virtual de hello no es suficiente. Debe especificar la subred específica de Hola que Hola máquinas virtuales deben estar en el conjunto de escala. toodo, concatenar `/subnets/mySubnet` toohello identificador de red virtual de Hola. resultado de Hello es Id. de hello completo de la subred de Hola. Realice esta concatenación con hello `concat` función, que toma una serie de cadenas y devuelve su concatenación.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Pasos siguientes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
