---
title: "aaaCreate una máquina virtual con una dirección pública estática de IP - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una máquina virtual con una estática pública IP dirección utilizando hello Azure interfaz de línea de comandos (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Crear una máquina virtual con una dirección IP pública estática con hello 2.0 de CLI de Azure

> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI de Azure 2.0](virtual-network-deploy-static-pip-arm-cli.md)
> * [CLI de Azure 1.0](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Plantilla](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (clásico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Crear hello VM

Puede completar esta tarea mediante Hola CLI de Azure 2.0 (en este artículo) o hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Hola valores en "" para recursos de creación de variables de hello en los pasos de Hola que sigan con la configuración del escenario de Hola. Cambiar los valores de hello, según corresponda para su entorno.

1. Instalar hello [CLI de Azure 2.0](/cli/azure/install-az-cli2) si no se ha instalado.
2. Crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux siguiendo los pasos de Hola Hola [crear un par de claves de públicas y privado de SSH para máquinas virtuales Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Desde un shell de comandos, inicio de sesión con el comando hello `az login`.
4. Crear Hola VM mediante la ejecución de script de Hola que sigue en un equipo Linux o Mac. Hola Azure dirección IP pública, la red virtual, la interfaz de red y recursos de máquina virtual deben existir en hello igual ubicación. Aunque recursos hello no tienen todas tooexist Hola mismo grupo de recursos, en la siguiente secuencia de comandos lo hacen de Hola.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Además toocreating una máquina virtual, el script de Hola crea:
- Una prima única administra disco de forma predeterminada, pero tiene otras opciones para el tipo de disco de Hola que se puede crear. Hola de lectura [crear una VM de Linux con hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artículo para obtener más información.
- Una red virtual, una subred, una NIC y recursos de dirección IP pública. Como alternativa, puede usar una red virtual, una subred, una NIC o una dirección IP pública *existentes*. toolearn cómo toouse existentes recursos de red en lugar de crear recursos adicionales, escriba `az vm create -h`.

## <a name = "validate"></a>Validación de la creación de máquinas virtuales y de dirección IP pública

1. Escriba el comando hello `az resource list --resouce-group IaaSStory --output table` toosee una lista de recursos de hello creado por el script de Hola. Debería haber cinco recursos Hola devolvía los resultados: interfaz, disco, dirección IP pública, red virtual y una máquina virtual de la red.
2. Escriba el comando hello `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Hola devolvía los resultados, anote el valor de Hola de **IpAddress** y ese valor Hola de **PublicIpAllocationMethod** es *estático*.
3. Antes de ejecutar el siguiente comando de hello, quitar hello <>, reemplace *nombre de usuario* con nombre de Hola que usó para hello **nombre de usuario** variable en el script de Hola y reemplazar *ipAddress* con hello **ipAddress** del paso anterior Hola. Siguiente ejecución Hola comando tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Quitar Hola VM y recursos asociados

Se recomienda que elimine recursos de hello creados en este ejercicio, si no usa en producción. Los recursos de máquina virtual, dirección IP pública y disco incurren en gastos, cuando se están aprovisionando. recursos de hello tooremove creados durante este ejercicio, Hola completa pasos:

1. recursos de hello tooview en grupo de recursos de hello, ejecute hello `az resource list --resource-group IaaSStory` comando.
2. Confirme que no hay recursos en grupo de recursos de hello, que no sea de recursos de hello creados por script de Hola en este artículo. 
3. toodelete todos los recursos creados en este ejercicio, ejecute hello `az group delete -n IaaSStory` comando. comando de Hello elimina el grupo de recursos de Hola y contiene todos los recursos de Hola.

## <a name="next-steps"></a>Pasos siguientes

Tráfico de red puede fluir tooand de hello que crea la VM en este artículo. Puede definir reglas entrantes y salientes en un NSG limitan el tráfico de Hola que puede fluir tooand de interfaz de red de hello, subred hello o ambos. más información acerca de los NSG, leer hello toolearn [información general NSG](virtual-networks-nsg.md) artículo.
