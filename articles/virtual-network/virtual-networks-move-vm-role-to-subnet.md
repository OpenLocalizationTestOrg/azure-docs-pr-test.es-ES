---
title: "Mover una máquina virtual (clásica) o una instancia de rol de Cloud Services a una subred distinta (Azure PowerShell) | Microsoft Docs"
description: "Obtenga información sobre cómo mover máquinas virtuales (clásicas) e instancias de rol de Cloud Services a una subred diferente mediante PowerShell."
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
ms.openlocfilehash: b094f8338394ef2e84cad3070936d715411326a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-to-a-different-subnet-using-powershell"></a><span data-ttu-id="826e9-103">Mover una máquina virtual (clásica) o una instancia de rol de Cloud Services a una subred diferente mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="826e9-103">Move a VM (Classic) or Cloud Services role instance to a different subnet using PowerShell</span></span>
<span data-ttu-id="826e9-104">Puede usar PowerShell para mover las máquinas virtuales (clásicas) de una subred a otra en la misma red virtual (VNet).</span><span class="sxs-lookup"><span data-stu-id="826e9-104">You can use PowerShell to move your VMs (Classic) from one subnet to another in the same virtual network (VNet).</span></span> <span data-ttu-id="826e9-105">Las instancias de rol pueden moverse si se edita el archivo CSCFG en lugar de utilizar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="826e9-105">Role instances can be moved by editing the CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="826e9-106">En este artículo se explica cómo mover máquinas virtuales implementadas solo a través del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="826e9-106">This article explains how to move VMs deployed through the classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="826e9-107">¿Por qué mover máquinas virtuales a otra subred?</span><span class="sxs-lookup"><span data-stu-id="826e9-107">Why move VMs to another subnet?</span></span> <span data-ttu-id="826e9-108">La migración de subred es útil cuando la antigua subred se queda demasiado pequeña y no se puede expandir debido a que existen máquinas virtuales en ejecución en esa subred.</span><span class="sxs-lookup"><span data-stu-id="826e9-108">Subnet migration is useful when the older subnet is too small and cannot be expanded due to existing running VMs in that subnet.</span></span> <span data-ttu-id="826e9-109">En ese caso, puede crear una subred más grande y migrar las máquinas virtuales a esa nueva subred; a continuación, una vez finalizada la migración, puede eliminar la subred antigua vacía.</span><span class="sxs-lookup"><span data-stu-id="826e9-109">In that case, you can create a new, larger subnet and migrate the VMs to the new subnet, then after migration is complete, you can delete the old empty subnet.</span></span>

## <a name="how-to-move-a-vm-to-another-subnet"></a><span data-ttu-id="826e9-110">Cómo mover una máquina virtual a otra subred</span><span class="sxs-lookup"><span data-stu-id="826e9-110">How to move a VM to another subnet</span></span>
<span data-ttu-id="826e9-111">Para mover una máquina virtual, ejecute el cmdlet de PowerShell Set-AzureSubnet, utilizando el ejemplo siguiente como plantilla.</span><span class="sxs-lookup"><span data-stu-id="826e9-111">To move a VM, run the Set-AzureSubnet PowerShell cmdlet, using the example below as a template.</span></span> <span data-ttu-id="826e9-112">En este ejemplo, movemos TestVM (máquina virtual de prueba) desde la subred actual a Subnet-2 (subred 2).</span><span class="sxs-lookup"><span data-stu-id="826e9-112">In the example below, we are moving TestVM from its present subnet, to Subnet-2.</span></span> <span data-ttu-id="826e9-113">Asegúrese de editar el ejemplo para reflejar su entorno.</span><span class="sxs-lookup"><span data-stu-id="826e9-113">Be sure to edit the example to reflect your environment.</span></span> <span data-ttu-id="826e9-114">Tenga en cuenta que siempre que ejecute el cmdlet Update-AzureVM como parte de un procedimiento, se reiniciará la máquina virtual como parte del proceso de actualización.</span><span class="sxs-lookup"><span data-stu-id="826e9-114">Note that whenever you run the Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of the update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="826e9-115">Si especificó una dirección IP privada interna estática para la máquina virtual, tendrá que borrar esa configuración para poder mover la máquina virtual a una nueva subred.</span><span class="sxs-lookup"><span data-stu-id="826e9-115">If you specified a static internal private IP for your VM, you'll have to clear that setting before you can move the VM to a new subnet.</span></span> <span data-ttu-id="826e9-116">En ese caso, utilice lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="826e9-116">In that case, use the following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="to-move-a-role-instance-to-another-subnet"></a><span data-ttu-id="826e9-117">Para mover una instancia de rol a otra subred</span><span class="sxs-lookup"><span data-stu-id="826e9-117">To move a role instance to another subnet</span></span>
<span data-ttu-id="826e9-118">Para mover una instancia de rol, edite el archivo CSCFG.</span><span class="sxs-lookup"><span data-stu-id="826e9-118">To move a role instance, edit the CSCFG file.</span></span> <span data-ttu-id="826e9-119">En este ejemplo, se mueve "Role0" (rol 0) en la red virtual *VNETName* de la subred actual a *Subnet-2* (subred 2).</span><span class="sxs-lookup"><span data-stu-id="826e9-119">In the example below, we are moving "Role0" in virtual network *VNETName* from its present subnet to *Subnet-2*.</span></span> <span data-ttu-id="826e9-120">Como ya se ha implementado la instancia de rol, solo tendrá que cambiar el nombre de la subred = Subnet-2 (subred 2).</span><span class="sxs-lookup"><span data-stu-id="826e9-120">Because the role instance was already deployed, you'll just change the Subnet name = Subnet-2.</span></span> <span data-ttu-id="826e9-121">Asegúrese de editar el ejemplo para reflejar su entorno.</span><span class="sxs-lookup"><span data-stu-id="826e9-121">Be sure to edit the example to reflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
