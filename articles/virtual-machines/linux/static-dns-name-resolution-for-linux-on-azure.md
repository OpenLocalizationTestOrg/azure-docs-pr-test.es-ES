---
title: "aaaUse resolución con hello Azure CLI 2.0 de nombres DNS internos para la máquina virtual | Documentos de Microsoft"
description: "Cómo red virtual toocreate tarjetas de interfaz y usar DNS interno para la resolución de nombres de máquina virtual en Azure con hello 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Creación de tarjetas de interfaz de red virtual y uso de DNS interno para la resolución de nombres de máquina virtual en Azure
Este artículo muestra cómo de nombres DNS internos estáticos del tooset para máquinas virtuales de Linux con virtual red tarjetas de interfaz (vNics) y los nombres de etiqueta DNS con hello 2.0 de CLI de Azure. También puede realizar estos pasos con hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Los nombres de DNS estáticos se utilizan para los servicios de infraestructura permanente como un servidor de compilación Jenkins, que se usa para este documento o un servidor de Git.

Hola requisitos son:

* [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);
* [archivos de clave SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Comandos rápidos
Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios. Obtener más información y el contexto de cada paso se encuentran en el resto de saludo del documento de hello, [a partir de aquí](#detailed-walkthrough). tooperform estos pasos, necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).

Requisitos previos: grupo de recursos, red virtual y subred, grupo de seguridad de red con SSH entrante.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Creación de una tarjeta de interfaz de red virtual con un nombre DNS interno estático
Crear Hola vNic con [crear nic de red az](/cli/azure/network/nic#create). Hola `--internal-dns-name` marca CLI es para la etiqueta de configuración Hola DNS, que proporciona Hola estático nombre DNS para la tarjeta de interfaz de red virtual (vNic) de Hola. Hello en el ejemplo siguiente se crea un vNic denominado `myNic`, se conecta toohello `myVnet` red virtual y crea un registro de nombre DNS interno denominado `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Implementar una máquina virtual y conéctese Hola vNic
Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hola `--nics` marca conecta Hola vNic toohello VM durante Hola implementación tooAzure. Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con discos de Azure administrados y adjuntará Hola vNic denominado `myNic` de hello anterior paso:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Una integración completa continua y la implementación continua (CiCd) una infraestructura en Azure requiere determinados servidores de toobe servidores estáticos o de larga duración. Se recomienda que los activos de Azure como Hola redes virtuales y grupos de seguridad de red son estáticos y larga duración recursos que rara vez se implementan. Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa. Posteriormente, puede agregar un servidor de repositorio de Git o un servidor de automatización Jenkins entrega CiCd toothis red virtual para los entornos de desarrollo o de prueba.  

Los nombres de DNS internos solo pueden resolverse dentro de una red virtual de Azure. Dado que los nombres DNS de hello son internos, no son toohello puede resolver fuera de internet, proporciona la infraestructura de toohello de seguridad adicional.

En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores. Los nombres de parámetros de ejemplo incluyen `myResourceGroup`, `myNic` y `myVM`.

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola
Primero, cree el grupo de recursos de hello con [crear grupo az](/cli/azure/group#create). Hello en el ejemplo siguiente se crea un grupo de recursos denominado `myResourceGroup` en hello `westus` ubicación:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Crear red virtual de Hola

Hola siguiente paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual. red virtual de Hello contiene una subred para este tutorial. Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Crear red virtual de hello con [crear red virtual de red az](/cli/azure/network/vnet#create). Hello en el ejemplo siguiente se crea una red virtual denominada `myVnet` y subred denominada `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Crear grupo de seguridad de red de hello
Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola. Para obtener más información acerca de los grupos de seguridad de red, consulte [cómo toocreate NSG en hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Crear grupo de seguridad de red de hello con [crear az red nsg](/cli/azure/network/nsg#create). Hello en el ejemplo siguiente se crea un grupo de seguridad de red denominado `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Agregar un tooallow de regla de entrada SSH
Agregar una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create). Hello en el ejemplo siguiente se crea una regla denominada `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Asociar subredes Hola Hola grupo de seguridad de red
subred de hello tooassociate con hello grupo de seguridad de red, usar [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update). Hello en el ejemplo siguiente se asocia nombre de subred de hello `mySubnet` con hello grupo de seguridad de red denominado `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Crear la tarjeta de interfaz de red virtual de Hola y nombres DNS estáticos
Azure es muy flexible, pero toouse para nombres DNS para la resolución de nombre de máquina virtual, debe tarjetas de interfaz de red virtual de toocreate (vNics) que se incluye una etiqueta DNS. vNics son importantes como poder reutilizarlos conectándolas a máquinas virtuales de toodifferent durante el ciclo de vida de hello infraestructura. Este enfoque conserva vNic Hola como un recurso estático mientras hello las máquinas virtuales puede ser temporal. Mediante el uso de DNS etiquetado de hello vNic, estamos tooenable capaz de resolución de nombres sencillos de otras máquinas virtuales en hello red virtual. Uso de nombres que se resuelven permite otro servidor de automatización de las máquinas virtuales tooaccess Hola por nombre DNS de Hola `Jenkins` u Hola Git server como `gitrepo`.  

Crear Hola vNic con [crear nic de red az](/cli/azure/network/nic#create). Hello en el ejemplo siguiente se crea un vNic denominado `myNic`, se conecta toohello `myVnet` red virtual denominada `myVnet`y crea un registro de nombre DNS interno denominado `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implementar Hola VM en la infraestructura de red virtual de Hola
Ahora tenemos una red virtual y subred, un grupo de seguridad de red que actúe como un firewall tooprotect nuestro subred bloqueando todo el tráfico entrante excepto el 22 de puerto para SSH y un vNic. Ahora se puede implementar la máquina virtual dentro de esta infraestructura de red existente.

Cree la máquina virtual con [az vm create](/cli/azure/vm#create). Hello en el ejemplo siguiente se crea una máquina virtual denominada `myVM` con discos de Azure administrados y adjuntará Hola vNic denominado `myNic` de hello anterior paso:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Mediante el uso de hello CLI marcas toocall recursos existentes, se ordena hello toodeploy Azure VM dentro de la red existente Hola. tooreiterate, una vez que se han implementado una red virtual y subred, puede dejarse como recursos estáticos o permanentes dentro de su región de Azure.  

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
