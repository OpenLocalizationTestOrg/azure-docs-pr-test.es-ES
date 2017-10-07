---
title: "aaaAccess y seguridad en las plantillas de Azure para máquinas virtuales de Windows | Documentos de Microsoft"
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Acceso y seguridad en plantillas de Azure Resource Manager para máquinas virtuales Windows

Aplicaciones alojadas en Azure necesidad probable toobe acceso a través de hello internet o una VPN o conexión de Express Route con Azure. Con el ejemplo de aplicación de la tienda de música de hello, estará disponible en sitio web de Hola Hola internet con una dirección IP pública. Con acceso establecido, se deben proteger conexiones toohello access y aplicación toohello recursos de máquina virtual por sí mismos. Esta acceso protegido se proporciona mediante un grupo de seguridad de red. 

Este documento describe cómo se protege la aplicación de tienda de música de Hola en la plantilla de administrador de recursos de Azure de ejemplo de Hola. Se resaltan todas las dependencias y configuraciones únicas. Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager. plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Dirección IP pública
se puede utilizar tooprovide acceso público tooan recursos de Azure, un recurso de dirección IP público. La dirección IP pública puede configurarse con una dirección IP estática o dinámica. Si se utiliza una dirección dinámica, y se detiene y se cancela la asignación de máquina virtual de hello, se quita direcciones Hola. Cuando se vuelva a iniciar la máquina de hello, se puede asignar una dirección IP pública diferente. tooprevent una IP de direcciones de cambio, puede utilizar una dirección IP reservada. 

Una dirección IP pública se pueden agregar plantilla de Azure Resource Manager tooan con hello Visual Studio agregar Asistente para nuevo recurso, o mediante la inserción de un valor JSON válido en una plantilla. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [dirección IP pública](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Una dirección IP pública puede asociarse con un adaptador de red virtual o un equilibrador de carga. En este ejemplo, dado que Hola sitio Web de la tienda de música tiene una carga equilibrada entre varias máquinas virtuales, Hola dirección IP pública es toohello adjunto equilibrador de carga.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de la dirección IP pública con el equilibrador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Hello dirección IP pública como ver Hola portal de Azure. Observe que la dirección IP pública hello es equilibrador de carga de tooa asociados y no en una máquina virtual. Equilibradores de carga de red se detallan en el siguiente documento de Hola de esta serie.

![Dirección IP pública](./media/dotnet-core-3-access-security/pubip-win.png)

Para más información sobre direcciones IP públicas de Azure, consulte [Direcciones IP en Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Grupo de seguridad de red (NSG)
Una vez acceso a recursos de tooAzure establecida, este acceso debe estar limitado. En máquinas virtuales de Azure, el acceso se protege mediante un grupo de seguridad de red. Con el ejemplo de aplicación de la tienda de música de hello, todas máquinas virtuales que toohello acceso está restringido excepto a través del puerto 80 para el acceso http y el puerto 3389 para acceso RDP. Un grupo de seguridad de red pueden agregarse tooan Azure Resource Manager plantilla mediante Visual Studio agregar Asistente para nuevo recurso, Hola o insertando un valor JSON válido en una plantilla.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [grupo de seguridad de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

En este ejemplo, grupo de seguridad de red de hello está asociado con el objeto de subred Hola declarado en recursos de red Virtual de Hola. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de grupo de seguridad de red con red Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

A continuación se muestra qué grupo de seguridad de red de hello aparece de hello portal de Azure. Observe que se puede asociar un grupo de seguridad de red con una interfaz de red o subred. En este caso, hello NSG está asociado tooa subred. En esta configuración, hello las reglas de entrada aplican tooall máquinas virtuales conectadas toohello subred.

![Grupo de seguridad de red (NSG)](./media/dotnet-core-3-access-security/nsg-win.png)

Para más información sobre los grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Paso siguiente
<hr>

[Paso 3: disponibilidad y escala en plantillas de Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

