---
title: una VM de Linux en Azure con varias NIC aaaCreate | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una VM de Linux con varias NIC había conectado tooit mediante plantillas de CLI de Azure o el Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Crear una máquina virtual Linux con varias NIC con hello Azure CLI 1.0
Puede crear una máquina virtual (VM) de Azure que tiene varios tooit de interfaces (NIC) que están conectados de red virtual. Un escenario común es toohave subredes diferentes para la conectividad de front-end y back-end o una red dedicada tooa supervisión o una solución de copia de seguridad. Este artículo proporciona comandos rápidos toocreate una máquina virtual con varias tooit NIC conectadas. Para obtener información detallada, incluyendo cómo toocreate varios NIC dentro de su propio Bash secuencias de comandos, obtenga más información sobre [implementar máquinas virtuales de varias NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Diferentes [tamaños de máquina virtual](sizes.md) admiten un número distinto de NIC, así que ajuste el tamaño de su máquina virtual teniendo esto en cuenta.

> [!WARNING]
> Debe adjuntar varios NIC cuando cree una máquina virtual: no se puede agregar tooan NIC existente VM con hello 1.0 de CLI de Azure. También puede [agregar tooan NIC existente VM con hello Azure CLI 2.0](multiple-nics.md). También puede [crear una máquina virtual en función de los discos virtuales original de hello](copy-vm.md) y cree varios NIC como implementar Hola máquina virtual.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#create-supporting-resources) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](multiple-nics.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="create-supporting-resources"></a>Creación de recursos de apoyo
Asegúrese de que dispone de hello [CLI de Azure](../../cli-install-nodejs.md) iniciado la sesión y utilizar el modo de administrador de recursos:

```azurecli
azure config mode arm
```

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *mystorageaccount* y *myVM*.

En primer lugar, cree un grupo de recursos. Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:

```azurecli
azure group create myResourceGroup --location eastus
```

Crear un toohold de cuenta de almacenamiento de las máquinas virtuales. Hello en el ejemplo siguiente se crea una cuenta de almacenamiento denominada *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Crear una red virtual tooconnect las máquinas virtuales se. Hello en el ejemplo siguiente se crea una red virtual denominada *myVnet* con un prefijo de dirección de *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Cree dos subredes de red virtual: una para el tráfico front-end y otra para el tráfico back-end. Hello en el ejemplo siguiente se crea dos subredes, denominados *mySubnetFrontEnd* y *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Creación y configuración de varias NIC
Encontrará más detalles acerca de [implementar varios NIC con hello Azure CLI](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluidos secuencias de comandos de proceso de Hola de bucle a través de toocreate todas las NIC de Hola.

Hello en el ejemplo siguiente se crea dos NIC, denominadas *myNic1* y *myNic2*, con una NIC conectan tooeach subred:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Normalmente se crea también un [grupo de seguridad de red](../../virtual-network/virtual-networks-nsg.md) o [equilibrador de carga](../../load-balancer/load-balancer-overview.md) toohelp administrar y distribuir el tráfico entre las máquinas virtuales. Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Enlazar el grupo de seguridad de red de NIC toohello mediante `azure network nic set`. enlaza Hello en el ejemplo siguiente se *myNic1* y *myNic2* con *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Crear una máquina virtual y adjuntar Hola NIC
Al crear Hola VM, ahora especificar varios NIC. En su lugar mediante `--nic-name` tooprovide una sola NIC, en su lugar use `--nic-names` y proporcionar una lista separada por comas de NIC. También debe tootake cuidado al seleccionar Hola tamaño de máquina virtual. No hay límite para el número total de Hola de NIC que se puede agregar tooa VM. Más información sobre los [tamaños de máquina virtual Linux](sizes.md). Hello en el ejemplo siguiente se muestra cómo toospecify varios NIC y, a continuación, en una máquina virtual cambia el tamaño que admite el uso de varias NIC (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>Creación de varias NIC con plantillas de Resource Manager
Plantillas de administrador de recursos de Azure utilizan declarativa toodefine de archivos JSON en su entorno. Puede leer la [introducción a Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Plantillas del Administrador de recursos proporcionan una manera toocreate varias instancias de un recurso durante la implementación, como la creación de varias NIC. Usa *copia* número de hello toospecify de toocreate de instancias:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Más información sobre la [creación de varias instancias mediante *copia*](../../resource-group-create-multiple.md). 

También puede usar un `copyIndex()` toothen anexar un nombre de recurso tooa número, que le permite toocreate `myNic1`, `myNic2`, etc. Hola continuación muestra un ejemplo de anexar el valor de índice de hello:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Puede leer un ejemplo completo de [cómo crear varias NIC con plantillas de Resource Manager](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Pasos siguientes
Asegúrese de que tooreview [tamaños de VM de Linux](sizes.md) al tratar de toocreating una máquina virtual con varias NIC. Pagar el número máximo de toohello de atención de NIC es compatible con el tamaño de cada máquina virtual. 

Recuerde que no se puede agregar tooan de NIC adicional existentes de la máquina virtual, debe crear todas las NIC de hello al implementar Hola máquina virtual. Tenga cuidado al planear la toomake de las implementaciones que dispone de conectividad de red de todos los Hola necesario desde el principio de Hola.

