---
title: "elemento de interfaz de usuario de VirtualNetworkCombo de aplicación administrado aaaAzure | Documentos de Microsoft"
description: Describe Hola elemento de interfaz de usuario de Microsoft.Network.VirtualNetworkCombo para administrar aplicaciones de Azure
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Elemento de la interfaz de usuario Microsoft.Network.VirtualNetworkCombo
Un grupo de controles para seleccionar una red virtual nueva o existente. Use este elemento al [crear una aplicación administrada de Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Ejemplo de interfaz de usuario
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- En tramas de alambres superior hello, usuario Hola detectado una nueva red virtual, por lo que el usuario de hello puede personalizar el prefijo de nombre y la dirección de cada subred. En este caso, la configuración de subredes es opcional.
- En tramas de alambres Hola inferior, usuario Hola se ha seleccionado una red virtual existente, por lo que debe asignar el usuario de hello cada plantilla de implementación de subred Hola requiere tooan subred. En este caso, la configuración de subredes es obligatoria.

## <a name="schema"></a>Esquema
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Comentarios
- Si se especifica, Hola primer prefijo de dirección no superpuestos de tamaño `defaultValue.addressPrefixSize` se determina automáticamente según las redes virtuales existentes en la suscripción del usuario de Hola.
- Hola valor predeterminado de `defaultValue.name` y `defaultValue.addressPrefixSize` es **null**.
- `constraints.minAddressPrefixSize` debe especificarse. Cualquier red virtual existente con un espacio de direcciones más pequeño que lo hello valor especificado no están disponibles para la selección.
- `subnets` debe especificarse y `constraints.minAddressPrefixSize` debe especificarse para cada subred.
- Al crear una nueva red virtual, prefijo de dirección de cada subred se calcula automáticamente basándose en prefijo de dirección de la red virtual de Hola y los respectivos `addressPrefixSize`.
- Si se usa una red virtual existente, las subredes menores que la `constraints.minAddressPrefixSize` respectiva no están disponibles para la selección. Además, si se especifica, las subredes que no contienen al menos `minAddressCount` direcciones disponibles no se podrán seleccionar.
es el valor predeterminado de Hello **0**. tooensure que Hola direcciones disponibles son contiguas, especifique **true** para `requireContiguousAddresses`. es el valor predeterminado de Hello **true**.
- No se admite la creación de subredes en una red virtual existente.
- Si `options.hideExisting` es **true**, usuario de hello no puede elegir una red virtual existente. es el valor predeterminado de Hello **false**.

## <a name="sample-output"></a>Salida de ejemplo
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Pasos siguientes
* Para una aplicación de toomanaged introducción, consulte [Introducción a la aplicación administrada de Azure](managed-application-overview.md).
* Para obtener definiciones una interfaz de usuario de toocreating de introducción, vea [Introducción a CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Para ver una descripción de las propiedades comunes de los elementos de interfaz de usuario, consulte [Elementos CreateUiDefinition](managed-application-createuidefinition-elements.md).
