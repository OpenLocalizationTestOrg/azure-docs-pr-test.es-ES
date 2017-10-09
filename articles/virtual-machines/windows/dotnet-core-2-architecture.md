---
title: aaaDeploying recursos de proceso de Windows con las plantillas de administrador de recursos de Azure | Documentos de Microsoft
description: "Tutorial de DotNet Core para máquinas virtuales de Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Arquitectura de aplicaciones con plantillas de Azure Resource Manager para máquinas virtuales Windows

Al desarrollar una implementación de Azure Resource Manager, los requisitos de proceso necesitan toobe asignado tooAzure recursos y servicios. Si una aplicación consta de varios extremos de http, una base de datos y un servicio de caché de datos, hello recursos de Azure que hospedan cada uno de estos componentes debe toobe racionalizado. Por ejemplo, la aplicación de tienda de música de ejemplo de Hola incluye una aplicación web que se hospeda en una máquina virtual y una base de datos SQL, que se hospeda en la base de datos SQL de Azure. 

Este documento describe cómo se configuran los recursos de proceso de hello tienda de música en la plantilla de administrador de recursos de Azure de ejemplo de Hola. Se resaltan todas las dependencias y configuraciones únicas. Para la mejor experiencia de hello, implementar previamente una instancia de hello solución tooyour suscripción de Azure y trabajar junto con la plantilla de hello Azure Resource Manager. plantilla de Hello completa puede encontrarse aquí: [implementación de la tienda de música en Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Máquina virtual
aplicación de la tienda de música de Hello incluye una aplicación web donde los clientes pueden examinar y comprar música. Aunque hay varios servicios de Azure que pueden hospedar aplicaciones web, en este ejemplo se utiliza una máquina virtual. Mediante la plantilla de tienda de música de ejemplo de Hola, se implementa una máquina virtual, instalar un servidor web y sitio Web de tienda de música de hello instalado y configurado. Para simplificar hello en este artículo, se detalla solamente la implementación de máquina virtual Hola. configuración de Hola de servidor web de Hola y aplicación hello se detalla en un artículo de una versión posterior.

Puede agregarse a una máquina virtual de plantilla tooa mediante Visual Studio Agregar recurso nuevo asistente, o mediante la inserción de un valor JSON válido en la plantilla de implementación de Hola Hola. Al implementar una máquina virtual, también se necesitan varios recursos relacionados. Si usa la plantilla de Visual Studio toocreate hello, estos recursos se crean automáticamente. Si manualmente creando plantilla hello, estos recursos deben toobe insertarse y configurarse.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [JSON de la máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

Una vez implementado, propiedades de la máquina virtual de hello pueden verse en hello portal de Azure.

![Máquina virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Cuenta de almacenamiento
Las cuentas de almacenamiento tienen numerosas funcionalidades y opciones de almacenamiento. Para el contexto de Hola de máquinas virtuales de Azure, una cuenta de almacenamiento contiene discos duros virtuales de Hola de máquina virtual de Hola y los discos de datos adicionales. ejemplo de la tienda de música de Hello incluye un almacenamiento cuenta toohold Hola disco duro virtual de cada máquina virtual en la implementación de Hola. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [cuenta de almacenamiento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Una cuenta de almacenamiento está asociado a una máquina virtual dentro de la declaración de plantilla de administrador de recursos de Hola de máquina virtual de Hola. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [asociación de la máquina Virtual y cuenta de almacenamiento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Después de la implementación, la cuenta de almacenamiento de hello puede verse en hello portal de Azure.

![Cuenta de almacenamiento](./media/dotnet-core-2-architecture/storacct-win.png)

Hacer clic en el contenedor de blob de cuenta de almacenamiento de hello, se puede ver archivo de disco duro virtual de hello para cada máquina virtual implementada con plantilla Hola.

![Unidades de disco duro virtuales](./media/dotnet-core-2-architecture/vhd-win.png)

Para más información sobre Azure Storage, consulte [Documentación de Almacenamiento](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Virtual Network
Si una máquina virtual requiere que las redes internas como Hola capacidad toocommunicate con otras máquinas virtuales y recursos de Azure, se requiere una red Virtual de Azure.  Una red virtual no hacer accesible a través de máquina virtual de Hola Hola internet. La conectividad pública requiere una dirección IP pública, que se detalla más adelante en esta serie.

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [subredes y red Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

Desde el portal de Azure hello, red virtual de hello es similar a Hola después de la imagen. Observe que todas las máquinas virtuales implementadas con plantilla hello toohello adjunto de red virtual.

![Virtual Network](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interfaz de red
 Una interfaz de red conecta a una red virtual de máquina virtual tooa, más concretamente tooa máscara de subred que se ha definido en la red virtual de Hola. 

 Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [interfaz de red](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Cada recurso de la máquina virtual incluye un perfil de red. interfaz de red de Hello está asociado a la máquina virtual de hello en este perfil.  

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [perfil de red de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

Desde el portal de Azure hello, interfaz de red de hello es similar a Hola después de la imagen. dirección IP interna de Hola y asociación de la máquina virtual de hello pueden verse en el recurso de interfaz de red de Hola.

![Interfaz de red](./media/dotnet-core-2-architecture/nic-win.png)

Para más información acerca de Azure Virtual Network, consulte [Documentación de Red virtual](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Azure SQL Database
Además tooa virtual machine hospedar sitios Web de la tienda de música de hello, una base de datos de SQL Azure es base de datos de implementada toohost Hola tienda de música. ventaja de Hola de con la base de datos de SQL Azure aquí es que no es necesario un segundo conjunto de máquinas virtuales, y escala y disponibilidad están integradas en el servicio Hola.

Una base de datos de SQL Azure se puede agregar utilizando Hola Visual Studio Agregar recurso nuevo asistente, o mediante la inserción de un valor JSON válido en una plantilla. Hola recurso de SQL Server incluye un nombre de usuario y una contraseña que se le conceden derechos administrativos en la instancia de SQL Hola. Además, se agrega un recurso de firewall de base de datos SQL. De forma predeterminada, las aplicaciones hospedadas en Azure son capaz de tooconnect con la instancia de SQL Hola. aplicación externa de tooallow tal una SQL Server Management studio tooconnect toohello instancia de SQL, firewall de hello debe toobe configurado. Para simplificar Hola demostración de la tienda de música de hello, la configuración predeterminada de hello es correcto. 

Siga este ejemplo JSON de vínculo toosee Hola dentro de la plantilla de administrador de recursos de hello: [base de datos de SQL Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Una vista de base de datos de MusicStore tal como se muestra en el portal de Azure de Hola y Hola SQL server.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Para más información sobre la implementación de Azure SQL Database, consulte [Documentación de Base de datos SQL](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Paso siguiente
<hr>

[Paso 2: acceso y seguridad en plantillas de Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

