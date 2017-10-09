---
title: "aaaCreate una máquina virtual con varias NIC - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con varias NIC con Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Crear una máquina virtual con varias NIC con hello 2.0 de CLI de Azure

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).  Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Crear hello VM

Puede completar esta tarea mediante Hola CLI de Azure 2.0 (en este artículo) o hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Hola valores en "" para recursos de creación de variables de hello en los pasos de Hola que sigan con la configuración del escenario de Hola. Cambiar los valores de hello, según corresponda para su entorno.

1. Instalar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) si no se ha instalado.
2. Crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux siguiendo los pasos de Hola Hola [crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Desde un shell de comandos, inicio de sesión con el comando hello `az login`.
4. Crear Hola VM mediante la ejecución de script de Hola que sigue en un equipo Linux o Mac. script de Hola crea un grupo de recursos, una red virtual (VNet) con dos subredes, dos NIC y una máquina virtual con hello dos NIC conectado tooit. Uno de hello NIC conectado tooone subred y se asigna una dirección IP estática pública y privada. Hello otro NIC está conectado toohello otra subred y se le asigna una dirección IP privada estática y ninguna dirección IP pública. Hola NIC, la dirección IP pública, la red virtual y recursos de máquina virtual deben existir en hello igual ubicación y la suscripción. Aunque recursos hello no tienen todas tooexist Hola mismo grupo de recursos, en la siguiente secuencia de comandos lo hacen de Hola.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Además toocreating una máquina virtual con dos NIC, crea el script de Hola:
- Una prima única administra disco de forma predeterminada, pero tiene otras opciones para el tipo de disco de Hola que se puede crear. Hola de lectura [crear una VM de Linux con hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener más información.
- Una red virtual con dos subredes y una única dirección IP pública. Como alternativa, puede usar una red virtual, una subred, una NIC o una dirección IP pública *existentes*. toolearn cómo toouse existentes recursos de red en lugar de crear recursos adicionales, escriba `az vm create -h`.

## <a name = "validate"></a>Validación de la creación de máquinas virtuales y NIC

1. Escriba el comando hello `az resource list --resouce-group Multi-NIC-VM --output table` toosee una lista de recursos de hello creado por el script de Hola. Debería haber seis recursos Hola devolvía los resultados: dos NIC, un disco, una dirección IP pública, una red virtual y una máquina virtual.
2. Escriba el comando hello `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Hola devolvía los resultados, anote el valor de Hola de **IpAddress** y ese valor Hola de **PublicIpAllocationMethod** es *estático*.
3. Antes de ejecutar el siguiente comando de hello, quitar hello <>, reemplace *nombre de usuario* con nombre de Hola que usó para hello **nombre de usuario** variable en el script de Hola y reemplazar *ipAddress* con hello **ipAddress** del paso anterior Hola. Siguiente ejecución Hola comando tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Una vez conectado toohello máquina virtual, ejecute hello `sudo ifconfig` comando toosee *eth0* y *eth1* interfaces. Cada NIC se ha asignado Hola privadas direcciones IP estáticas especificadas en el script de Hola por servidores DHCP de Azure de Hola. Hello direcciones IP y MAC asignadas toohello NIC no cambian hasta que se eliminó la MV de Hola. Se recomienda no cambiar una dirección IP dentro de un sistema operativo, tal y como puede deshabilitar el equipo de toohello de conectividad. Las direcciones IP públicas no aparecen en el sistema operativo de hello, tal como están tooand traducido de dirección de red de dirección IP privada de Hola por hello infraestructura de Azure.

## <a name= "clean-up"></a>Quitar Hola VM y recursos asociados

Se recomienda que elimine recursos de hello creados en este ejercicio, si no usa en producción. Los recursos de máquina virtual, dirección IP pública y disco incurren en gastos, cuando se están aprovisionando. recursos de hello tooremove creados durante este ejercicio, Hola completa pasos:
1. recursos de hello tooview en grupo de recursos de hello, ejecute hello `az resource list --resource-group Multi-NIC-VM` comando.
2. Confirme que no hay recursos en grupo de recursos de hello, que no sea de recursos de hello creados por script de Hola en este artículo. 
3. toodelete todos los recursos creados en este ejercicio, ejecute hello `az group delete --name Multi-NIC-VM` comando. comando de Hello elimina el grupo de recursos de Hola y contiene todos los recursos de Hola.

## <a name="next-steps"></a>Pasos siguientes

Tráfico de red puede fluir tooand de hello que crea la VM en este artículo. Puede definir reglas entrantes y salientes en un NSG limitan el tráfico de Hola que puede fluir tooand desde cada interfaz de red, cada subred o ambos. más información acerca de los NSG, leer hello toolearn [información general NSG](virtual-networks-nsg.md) artículo.
