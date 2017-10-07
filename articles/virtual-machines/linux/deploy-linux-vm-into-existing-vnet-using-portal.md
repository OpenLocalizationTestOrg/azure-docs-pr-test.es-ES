---
title: "aaaDeploy máquinas virtuales de Linux en la red existente con el portal de Azure | Documentos de Microsoft"
description: Implementar una VM de Linux en una red Virtual de Azure existente mediante el portal de Hola.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a>¿Cómo toodeploy una máquina virtual de Linux en una red Virtual de Azure existente con hello portal de Azure

Este artículo muestra cómo toodeploy una máquina virtual (VM) en una red virtual (VNet). Los recursos de Azure como redes virtuales y grupos de seguridad de red deben ser recursos estáticos y de larga duración que rara vez se implementen. Una vez que se ha implementado una red virtual, se puede ser reutilizada por reimplementaciones constantes sin ninguna infraestructura de toohello afectará de forma negativa. Pensar en una red virtual como tradicional modificador de red de hardware: no tendría tooconfigure hardware completamente nuevo cambiar con cada implementación.  

Con una red virtual configurada correctamente, puede seguir el toodeploy nuevos servidores en esa red virtual una y otra vez con pocos, si lo hay, cambios necesarios durante la vigencia de Hola de hello red virtual.

## <a name="create-hello-resource-group"></a>Crear grupo de recursos de Hola

En primer lugar, cree una tooorganize de grupo de recursos todo lo que cree en este tutorial. Para más información sobre los grupos de recursos de Azure, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a>Crear red virtual de hello

A continuación, compile un hello toolaunch de red virtual las máquinas virtuales en. Hola red virtual contiene una subred y está asociado con el grupo de seguridad de red de Hola a esta subred en un paso posterior.

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a>Agregar una subred de toohello VNic

Tarjetas de red virtual (VNics) son importantes que pueda conectarse toodifferent las máquinas virtuales. Este enfoque conserva Hola VNic como un recurso estático mientras hello las máquinas virtuales puede ser temporal. Cree un VNic y asociarla a la subred de hello creado en el paso anterior de Hola.

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a>Crear grupo de seguridad de red de Hola

Grupos de seguridad de red de Azure son firewall tooa equivalente en la capa de red Hola. Para más información sobre los grupos de seguridad de red, consulte [¿Qué es un grupo de seguridad de red?](../../virtual-network/virtual-networks-nsg.md)

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Agregar regla de permiso de SSH entrante

Hola VM necesita acceso de hello internet, por lo que una regla que permita el puerto de entrada 22 tráfico toobe pasa a través de la red de hello tooport 22 en Hola se crea la máquina virtual.

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a>Asociar NSG Hola subred Hola

Con hello red virtual y subred Hola creado, asociar el grupo de seguridad de red de hello subred Hola. Los grupos de seguridad de red se pueden asociar con una subred entera o una VNic individual. Con el firewall Hola filtran el tráfico en el nivel de subred de hello, todos los VNics y hello las máquinas virtuales dentro de la subred de hello están protegidos por grupo de seguridad de red de Hola. Hello otro enfoque es Hola grupo de seguridad de red que se está asociada a solo un VNic único y la protección de una sola máquina virtual.

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implementar Hola VM en la red virtual de Hola y NSG

Uso de hello portal de Azure, Hola VM de Linux es implementado toohello grupo de recursos de Azure, red virtual, subred y VNic existentes.

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

Mediante el uso de recursos existentes de hello toochoose portal, indique a hello toodeploy Azure VM dentro de la red existente Hola. Una vez que se ha implementado una red virtual y una subred, estas pueden dejarse como recursos estáticos o permanentes dentro de su región de Azure.  

## <a name="next-steps"></a>Pasos siguientes

* [Usar un toocreate de plantilla una implementación específica de Azure Resource Manager](../windows/cli-deploy-templates.md)
* [Creación de un entorno personalizado para una máquina virtual Linux mediante el uso de comandos de la CLI de Azure directamente](create-cli-complete.md)
* [Implementación y administración de máquinas virtuales con plantillas de Azure Resource Manager y la CLI de Azure](create-ssh-secured-vm-from-template.md)
