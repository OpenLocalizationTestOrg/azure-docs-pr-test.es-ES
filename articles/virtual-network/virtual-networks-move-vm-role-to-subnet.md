---
title: "aaaMove una máquina virtual (clásica) o servicios en la nube rol instancia tooa otra subred - PowerShell de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomove máquinas virtuales (clásicas) y tooa otra subred utilizando PowerShell de instancias de rol de servicios en la nube."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a>Mover una máquina virtual (clásica) o servicios en la nube rol instancia tooa otra subred utilizando PowerShell
Puede usar PowerShell toomove las máquinas virtuales (clásicas) de una subred tooanother Hola misma red virtual (VNet). Editar el archivo CSCFG de hello, en lugar de usar PowerShell pueden mover instancias de rol.

> [!NOTE]
> Este artículo explica cómo toomove las máquinas virtuales se implementan a través de hello implementación clásica solo para el modelo.
> 
> 

¿Por qué mover máquinas virtuales tooanother subred? Migración de subred es útil cuando subred antigua hello es demasiado pequeño y no se pueden expandir debido tooexisting máquinas virtuales en ejecución en esa subred. En ese caso, puede crear una subred nueva y más grande y migrar máquinas virtuales toohello nueva subred de hello, a continuación, una vez completada la migración, puede eliminar la subred antigua vacía de Hola.

## <a name="how-toomove-a-vm-tooanother-subnet"></a>¿Cómo toomove una subred VM tooanother
toomove una máquina virtual, ejecute cmdlet de PowerShell de conjunto AzureSubnet de hello, uso de ejemplo Hola siguiente como plantilla. En el ejemplo de Hola siguiente, movemos TestVM de la subred actual, tooSubnet-2. Ser tooreflect de ejemplo de Hola tooedit seguro de su entorno. Tenga en cuenta que, siempre que se ejecute el cmdlet Update-AzureVM de hello como parte de un procedimiento, se reiniciará la máquina virtual como parte del proceso de actualización de Hola.

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

Si especifica una dirección IP estática de privada interna para la máquina virtual, tendrá tooclear esa configuración antes de poder mover tooa nueva subred VM de Hola. En ese caso, utilice el siguiente hello:

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a>toomove una subred de tooanother de instancia de rol
toomove una instancia de rol, edite hello CSCFG. En el ejemplo de Hola siguiente, movemos "Role0" en la red virtual *VNETName* de la subred actual demasiado*Subnet-2*. Dado que ya se implementó la instancia de rol de hello, simplemente cambiará nombre de subred de hello = Subnet-2. Ser tooreflect de ejemplo de Hola tooedit seguro de su entorno.

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
