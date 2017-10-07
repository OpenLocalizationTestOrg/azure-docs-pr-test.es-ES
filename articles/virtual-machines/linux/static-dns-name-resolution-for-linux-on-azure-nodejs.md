---
title: "aaaUsing resolución en Azure de nombres DNS internos para la máquina virtual | Documentos de Microsoft"
description: "Uso de DNS interno para la resolución de nombre de máquina virtual en Azure."
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Uso de DNS interno para la resolución de nombre de máquina virtual en Azure

Este artículo muestra cómo tooset nombres de DNS interno estático para máquinas virtuales Linux mediante tarjetas NIC Virtual (VNic) y los nombres de etiqueta DNS. Los nombres de DNS estáticos se utilizan para los servicios de infraestructura permanente como un servidor de compilación Jenkins, que se usa para este documento o un servidor de Git.

Hola requisitos son:

* [una cuenta de Azure](https://azure.microsoft.com/pricing/free-trial/);
* [archivos de clave SSH pública y privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="cli-versions-toocomplete-hello-task"></a>Tarea CLI versiones toocomplete hello
Puede completar la tarea hello mediante uno de hello después de las versiones CLI:

- [Azure 1.0 de CLI](#quick-commands) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)
- [Azure 2.0 CLI](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola


## <a name="quick-commands"></a>Comandos rápidos

Si necesita tooquickly realizar la tarea hello, Hola pasos de la sección detalles comandos Hola necesarios. Obtener más información y el contexto de cada paso se encuentran rest Hola de documento de hello, [a partir de aquí](#detailed-walkthrough).  

Requisitos previos: grupo de recursos, red virtual, NSG con SSH entrante, subred.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Creación de VNic con un nombre de DNS interno estático

Hola `-r` cli marca indica que etiqueta de configuración Hola DNS, que proporciona Hola nombre DNS estático Hola VNic.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Implementar Hola VM en Hola de red virtual, NSG y, cuando conectan Hola VNic

Hola `-N` conecta Hola VNic toohello nueva máquina virtual durante Hola implementación tooAzure.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Tutorial detallado

Una integración completa continua y la implementación continua (CiCd) una infraestructura en Azure requiere determinados servidores de toobe servidores estáticos o de larga duración.  Se recomienda que los activos de Azure como hello las redes virtuales (redes virtuales) y grupos de seguridad de red (NSG), debe ser estáticos y larga duración recursos que rara vez se implementan.  Una vez que se ha implementado una red virtual, se puede reutilizar con nuevas implementaciones sin ninguna infraestructura de toohello afectará de forma negativa.  Agregar red estática toothis un Git servidor de repositorio y un servidor de automatización de Jenkins entrega CiCd tooyour entornos de prueba o desarrollo.  

Los nombres de DNS internos solo pueden resolverse dentro de una red virtual de Azure.  Dado que los nombres DNS de hello son internos, no son toohello puede resolver fuera de internet, proporciona la infraestructura de toohello de seguridad adicional.

_Reemplace los ejemplos por su propia nomenclatura._

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

Un grupo de recursos es necesario tooorganize todo el contenido se crea en este tutorial.  Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Crear red virtual de hello

Hola primer paso es toobuild Hola a las máquinas virtuales en un toolaunch de red virtual.  Hola red virtual contiene una subred para este tutorial.  Para obtener más información sobre redes virtuales de Azure, consulte [crear una red virtual mediante el uso de hello CLI de Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Crear hello NSG

Hola subred se basa detrás de un grupo de seguridad de red existente de modo que creamos hello NSG antes de hello subred.  Los NSG Azure son firewall tooa equivalente en la capa de red Hola.  Para obtener más información sobre los NSG de Azure, vea [cómo toocreate NSG en Hola CLI de Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Agregar regla de permiso de SSH entrante

Hola Linux VM necesita acceso de Hola se necesita internet para que una regla que permita el puerto de entrada tráfico 22 toobe pasa a través de la red de hello tooport 22 en hello VM de Linux.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Agregar una red virtual de toohello de subred

Las máquinas virtuales de hello red virtual deben estar ubicadas en una subred.  Cada red virtual puede tener varias subredes.  Crear una subred de Hola y asocie subred Hola Hola NSG tooadd una subred de toohello de firewall.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Hola subred ahora se agregaron dentro de la red virtual de Hola y asociada con hello NSG y regla NSG Hola.

## <a name="creating-static-dns-names"></a>Creación de nombres de DNS estáticos

Azure es muy flexible, pero toouse para nombres DNS para la resolución de nombres de las máquinas virtuales, debe toocreate como Virtual tarjetas (VNics) con DNS etiquetado de red.  VNics son importantes como poder reutilizarlos conectándolos toodifferent máquinas virtuales, lo que mantiene Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal.  Mediante el uso de DNS etiquetado en hello VNic, estamos tooenable capaz de resolución de nombres sencillos de otras máquinas virtuales en hello red virtual.  Uso de nombres que se resuelven permite otro servidor de automatización de las máquinas virtuales tooaccess Hola por nombre DNS de Hola `Jenkins` u Hola Git server como `gitrepo`.  Crear un VNic y asócielo con hello que subred creada en el paso anterior de Hola.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implementar Hola VM en la red virtual de Hola y NSG

Ahora tenemos una red virtual, una subred dentro de esa red virtual y un NSG actúa como un firewall tooprotect nuestro subred bloqueando todo el tráfico entrante excepto el puerto 22 de SSH.  Hola VM ahora pueden implementarse dentro de esta infraestructura de red existente.

Mediante Hola CLI de Azure y Hola `azure vm create` comando hello Linux VM está implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes.  Para obtener más información sobre el uso de hello CLI toodeploy una máquina virtual completa, consulte [crear un entorno completo de Linux mediante Hola CLI de Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Mediante el uso de hello CLI marcas toocall recursos existentes, se ordena hello toodeploy Azure VM dentro de la red existente Hola.  tooreiterate, una vez que se han implementado una red virtual y subred, puede dejarse como recursos estáticos o permanentes dentro de su región de Azure.  

## <a name="next-steps"></a>Pasos siguientes
* [Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
