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
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="89040-103">Mover una máquina virtual (clásica) o servicios en la nube rol instancia tooa otra subred utilizando PowerShell</span><span class="sxs-lookup"><span data-stu-id="89040-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="89040-104">Puede usar PowerShell toomove las máquinas virtuales (clásicas) de una subred tooanother Hola misma red virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="89040-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="89040-105">Editar el archivo CSCFG de hello, en lugar de usar PowerShell pueden mover instancias de rol.</span><span class="sxs-lookup"><span data-stu-id="89040-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="89040-106">Este artículo explica cómo toomove las máquinas virtuales se implementan a través de hello implementación clásica solo para el modelo.</span><span class="sxs-lookup"><span data-stu-id="89040-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="89040-107">¿Por qué mover máquinas virtuales tooanother subred?</span><span class="sxs-lookup"><span data-stu-id="89040-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="89040-108">Migración de subred es útil cuando subred antigua hello es demasiado pequeño y no se pueden expandir debido tooexisting máquinas virtuales en ejecución en esa subred.</span><span class="sxs-lookup"><span data-stu-id="89040-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="89040-109">En ese caso, puede crear una subred nueva y más grande y migrar máquinas virtuales toohello nueva subred de hello, a continuación, una vez completada la migración, puede eliminar la subred antigua vacía de Hola.</span><span class="sxs-lookup"><span data-stu-id="89040-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="89040-110">¿Cómo toomove una subred VM tooanother</span><span class="sxs-lookup"><span data-stu-id="89040-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="89040-111">toomove una máquina virtual, ejecute cmdlet de PowerShell de conjunto AzureSubnet de hello, uso de ejemplo Hola siguiente como plantilla.</span><span class="sxs-lookup"><span data-stu-id="89040-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="89040-112">En el ejemplo de Hola siguiente, movemos TestVM de la subred actual, tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="89040-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="89040-113">Ser tooreflect de ejemplo de Hola tooedit seguro de su entorno.</span><span class="sxs-lookup"><span data-stu-id="89040-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="89040-114">Tenga en cuenta que, siempre que se ejecute el cmdlet Update-AzureVM de hello como parte de un procedimiento, se reiniciará la máquina virtual como parte del proceso de actualización de Hola.</span><span class="sxs-lookup"><span data-stu-id="89040-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="89040-115">Si especifica una dirección IP estática de privada interna para la máquina virtual, tendrá tooclear esa configuración antes de poder mover tooa nueva subred VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="89040-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="89040-116">En ese caso, utilice el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="89040-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="89040-117">toomove una subred de tooanother de instancia de rol</span><span class="sxs-lookup"><span data-stu-id="89040-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="89040-118">toomove una instancia de rol, edite hello CSCFG.</span><span class="sxs-lookup"><span data-stu-id="89040-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="89040-119">En el ejemplo de Hola siguiente, movemos "Role0" en la red virtual *VNETName* de la subred actual demasiado*Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="89040-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="89040-120">Dado que ya se implementó la instancia de rol de hello, simplemente cambiará nombre de subred de hello = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="89040-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="89040-121">Ser tooreflect de ejemplo de Hola tooedit seguro de su entorno.</span><span class="sxs-lookup"><span data-stu-id="89040-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
