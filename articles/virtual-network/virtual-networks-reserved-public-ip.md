---
title: "Administración de direcciones IP reservadas (clásico) de Azure mediante PowerShell | Microsoft Docs"
description: "Conozca las direcciones IP reservadas (clásico) y cómo administrarlas mediante PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 5e9c83cebec96c6bc8afd53b0c637d7af899746f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="8fc78-103">Direcciones IP reservadas (clásico)</span><span class="sxs-lookup"><span data-stu-id="8fc78-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fc78-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8fc78-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="8fc78-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8fc78-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="8fc78-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="8fc78-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="8fc78-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="8fc78-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="8fc78-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="8fc78-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="8fc78-109">Las direcciones IP en Azure se dividen en dos categorías: dinámicas y reservadas.</span><span class="sxs-lookup"><span data-stu-id="8fc78-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="8fc78-110">Las direcciones IP públicas administradas por Azure son dinámicas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8fc78-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="8fc78-111">Esto significa que la dirección IP usada para un determinado servicio en la nube (VIP) o para tener acceso a una máquina virtual o instancia de rol directamente (ILPIP) puede cambiar de vez en cuando, cuando los recursos se cierran o detienen (desasignan).</span><span class="sxs-lookup"><span data-stu-id="8fc78-111">That means that the IP address used for a given cloud service (VIP) or to access a VM or role instance directly (ILPIP) can change from time to time, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="8fc78-112">Para impedir que cambien las direcciones IP, puede reservar una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="8fc78-112">To prevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="8fc78-113">La IP reservadas únicamente puede usarse como una VIP, lo que garantiza que la dirección IP para el servicio en la nube siga siendo la misma incluso cuando se cierran o detienen (desasignan) recursos.</span><span class="sxs-lookup"><span data-stu-id="8fc78-113">Reserved IPs can be used only as a VIP, ensuring that the IP address for the cloud service remains the same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="8fc78-114">Además, se puede convertir direcciones IP dinámicas existentes utilizadas como una VIP en una IP reservada.</span><span class="sxs-lookup"><span data-stu-id="8fc78-114">Furthermore, you can convert existing dynamic IPs used as a VIP to a reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8fc78-115">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8fc78-116">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="8fc78-116">This article covers using the classic deployment model.</span></span> <span data-ttu-id="8fc78-117">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8fc78-117">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8fc78-118">Obtenga información sobre cómo reservar una dirección IP pública estática con el [modelo de implementación de Resource Manager](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-118">Learn how to reserve a static public IP address using the [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="8fc78-119">Para más información sobre las direcciones IP en Azure, lea el artículo sobre [direcciones IP](virtual-network-ip-addresses-overview-classic.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-119">To learn more about IP addresses in Azure, read the [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="8fc78-120">¿Cuándo se necesita una IP reservada?</span><span class="sxs-lookup"><span data-stu-id="8fc78-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="8fc78-121">**Para asegurarse de que la dirección IP está reservada en su suscripción**.</span><span class="sxs-lookup"><span data-stu-id="8fc78-121">**You want to ensure that the IP is reserved in your subscription**.</span></span> <span data-ttu-id="8fc78-122">Si desea reservar una dirección IP que no se libera de su suscripción bajo ninguna circunstancia, debe usar una dirección IP pública reservada.</span><span class="sxs-lookup"><span data-stu-id="8fc78-122">If you want to reserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="8fc78-123">**Desea que su IP permanezca con el servicio en la nube incluso en el estado detenido o desasignado (máquina virtual)**.</span><span class="sxs-lookup"><span data-stu-id="8fc78-123">**You want your IP to stay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="8fc78-124">Si desea tener acceso al servicio mediante una dirección IP que no cambia incluso cuando las máquinas virtuales en el servicio en la nube se cierran o detienen (desasignan).</span><span class="sxs-lookup"><span data-stu-id="8fc78-124">If you want your service to be accessed by using an IP address that doesn't change, even when VMs in the cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="8fc78-125">**Desea estar seguro de que el tráfico saliente de Azure usa una dirección IP predecible**.</span><span class="sxs-lookup"><span data-stu-id="8fc78-125">**You want to ensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="8fc78-126">Es posible que haya configurado un firewall local para permitir solo tráfico procedente de direcciones IP específicas.</span><span class="sxs-lookup"><span data-stu-id="8fc78-126">You may have your on-premises firewall configured to allow only traffic from specific IP addresses.</span></span> <span data-ttu-id="8fc78-127">Al reservar una dirección IP, sabe la dirección IP de origen y no tiene que actualizar las reglas de firewall debido a un cambio de dirección IP.</span><span class="sxs-lookup"><span data-stu-id="8fc78-127">By reserving an IP, you know the source IP address, and don't need to update your firewall rules due to an IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="8fc78-128">P+F</span><span class="sxs-lookup"><span data-stu-id="8fc78-128">FAQ</span></span>
1. <span data-ttu-id="8fc78-129">¿Puedo usar una IP reservada para todos los servicios de Azure?</span><span class="sxs-lookup"><span data-stu-id="8fc78-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="8fc78-130">No.</span><span class="sxs-lookup"><span data-stu-id="8fc78-130">No.</span></span> <span data-ttu-id="8fc78-131">Las IP reservadas solo pueden usarse para máquinas virtuales y roles de instancia del servicio en la nube que se hayan expuesto a través de una VIP.</span><span class="sxs-lookup"><span data-stu-id="8fc78-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="8fc78-132">¿Cuántas direcciones IP reservadas puedo tener?</span><span class="sxs-lookup"><span data-stu-id="8fc78-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="8fc78-133">Para obtener más información, consulte el [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="8fc78-133">For details, see the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="8fc78-134">¿Hay un cargo por las IP reservadas?</span><span class="sxs-lookup"><span data-stu-id="8fc78-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="8fc78-135">A veces.</span><span class="sxs-lookup"><span data-stu-id="8fc78-135">Sometimes.</span></span> <span data-ttu-id="8fc78-136">Para detalles sobre los precios, consulte la página [Detalles de precios de las direcciones IP reservadas](http://go.microsoft.com/fwlink/?LinkID=398482).</span><span class="sxs-lookup"><span data-stu-id="8fc78-136">For pricing details, see the [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="8fc78-137">¿Cómo se reserva una dirección IP?</span><span class="sxs-lookup"><span data-stu-id="8fc78-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="8fc78-138">Puede usar PowerShell, la [API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o la [portal de Azure](https://portal.azure.com) para reservar una dirección IP en una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="8fc78-138">You can use PowerShell, the [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or the [Azure portal](https://portal.azure.com) to reserve an IP address in an Azure region.</span></span> <span data-ttu-id="8fc78-139">Hay una dirección IP reservada asociada a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="8fc78-139">A reserved IP address is associated to your subscription.</span></span>
5. <span data-ttu-id="8fc78-140">¿Puedo usar una IP reservada con redes virtuales basadas en grupos de afinidad?</span><span class="sxs-lookup"><span data-stu-id="8fc78-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="8fc78-141">No.</span><span class="sxs-lookup"><span data-stu-id="8fc78-141">No.</span></span> <span data-ttu-id="8fc78-142">Las IP reservadas solo se admiten en redes virtuales regionales.</span><span class="sxs-lookup"><span data-stu-id="8fc78-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="8fc78-143">Las IP reservadas no se admiten para redes virtuales asociadas a grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="8fc78-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="8fc78-144">Para más información sobre cómo asociar una red virtual a una región o un grupo de afinidad, consulte el artículo [Redes virtuales regionales y grupos de afinidad](virtual-networks-migrate-to-regional-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-144">For more information about associating a VNet with a region or affinity group, see the [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="8fc78-145">Administración de VIP reservadas</span><span class="sxs-lookup"><span data-stu-id="8fc78-145">Manage reserved VIPs</span></span>

<span data-ttu-id="8fc78-146">Asegúrese de que ha instalado y configurado Azure PowerShell completando los pasos del artículo [Install and configure PowerShell](/powershell/azure/overview) (Instalación y configuración de PowerShell).</span><span class="sxs-lookup"><span data-stu-id="8fc78-146">Ensure you have installed and configured PowerShell by completing the steps in the [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="8fc78-147">Para poder usar IP reservadas, debe agregarlo a su suscripción.</span><span class="sxs-lookup"><span data-stu-id="8fc78-147">Before you can use reserved IPs, you must add it to your subscription.</span></span> <span data-ttu-id="8fc78-148">Para crear una IP reservada del grupo de direcciones IP públicas disponibles en la ubicación *Centro de EE. UU.*, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="8fc78-148">To create a reserved IP from the pool of public IP addresses available in the *Central US* location, run the following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="8fc78-149">Sin embargo, tenga en cuenta que no puede especificar qué IP se va a reservar.</span><span class="sxs-lookup"><span data-stu-id="8fc78-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="8fc78-150">Para ver qué direcciones IP están reservadas en su suscripción, ejecute el siguiente comando de PowerShell y observe los valores de *ReservedIPName* y *Dirección*:</span><span class="sxs-lookup"><span data-stu-id="8fc78-150">To view what IP addresses are reserved in your subscription, run the following PowerShell command, and notice the values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="8fc78-151">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="8fc78-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="8fc78-152">Cuando crea una dirección IP reservada con PowerShell, no puede especificar un grupo de recursos en el cual crear la IP reservada.</span><span class="sxs-lookup"><span data-stu-id="8fc78-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group to create the reserved IP in.</span></span> <span data-ttu-id="8fc78-153">Azure lo coloca automáticamente en un grupo de recursos llamado *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="8fc78-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="8fc78-154">Si crea la IP reservada con [Azure Portal](http://portal.azure.com), puede especificar cualquier grupo de recursos que elija.</span><span class="sxs-lookup"><span data-stu-id="8fc78-154">If you create the reserved IP using the [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="8fc78-155">Sin embargo, si crea la IP reservada en un grupo de recursos distinto de *Default-Networking*, cada vez que haga referencia a la IP reservada con comandos como `Get-AzureReservedIP` y `Remove-AzureReservedIP`, debe hacer referencia al nombre *Group resource-group-name reserved-ip-name*.</span><span class="sxs-lookup"><span data-stu-id="8fc78-155">If you create the reserved IP in a resource group other than *Default-Networking* however, whenever you reference the reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference the name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="8fc78-156">Por ejemplo, si crea una IP reservada llamada *myReservedIP* en un grupo de recursos denominado *myResourceGroup*, debe hacer referencia al nombre de la IP reservada como *Group myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="8fc78-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference the name of the reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="8fc78-157">Una vez reservada una IP, permanece asociada a su suscripción hasta que la elimine.</span><span class="sxs-lookup"><span data-stu-id="8fc78-157">Once an IP is reserved, it remains associated to your subscription until you delete it.</span></span> <span data-ttu-id="8fc78-158">Para eliminar una IP reservada, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8fc78-158">To delete a reserved IP, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-the-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="8fc78-159">Reserva de la dirección IP de un servicio en la nube existente</span><span class="sxs-lookup"><span data-stu-id="8fc78-159">Reserve the IP address of an existing cloud service</span></span>
<span data-ttu-id="8fc78-160">Puede reservar la dirección IP de un servicio en la nube existente mediante el parámetro `-ServiceName`.</span><span class="sxs-lookup"><span data-stu-id="8fc78-160">You can reserve the IP address of an existing cloud service by adding the `-ServiceName` parameter.</span></span> <span data-ttu-id="8fc78-161">Para reservar la dirección IP de un servicio en la nube *TestService* en la ubicación *Centro de EE. UU.*, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8fc78-161">To reserve the IP address of a cloud service *TestService* in the *Central US* location, run the following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-to-a-new-cloud-service"></a><span data-ttu-id="8fc78-162">Asociación de una IP reservada a un nuevo servicio en la nube</span><span class="sxs-lookup"><span data-stu-id="8fc78-162">Associate a reserved IP to a new cloud service</span></span>
<span data-ttu-id="8fc78-163">El script siguiente crea una nueva dirección IP reservada y, a continuación, la asocia a un nuevo servicio en la nube denominado *TestService*.</span><span class="sxs-lookup"><span data-stu-id="8fc78-163">The following script creates a new reserved IP, then associates it to a new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="8fc78-164">Cuando se crea una IP reservada para usarla con un servicio en la nube, todavía es necesario hacer referencia a la máquina virtual mediante *VIP:&lt;número de puerto>* para las comunicaciones entrantes.</span><span class="sxs-lookup"><span data-stu-id="8fc78-164">When you create a reserved IP to use with a cloud service, you still refer to the VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="8fc78-165">Reservar una dirección IP no significa que pueda conectarse directamente a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8fc78-165">Reserving an IP does not mean you can connect to the VM directly.</span></span> <span data-ttu-id="8fc78-166">La IP reservada se asigna al servicio en la nube en el que se ha implementado la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8fc78-166">The reserved IP is assigned to the cloud service that the VM has been deployed to.</span></span> <span data-ttu-id="8fc78-167">Si desea conectarse directamente a una máquina virtual mediante la dirección IP, tendrá que configurar una dirección IP pública a nivel de instancia.</span><span class="sxs-lookup"><span data-stu-id="8fc78-167">If you want to connect to a VM by IP directly, you have to configure an instance-level public IP.</span></span> <span data-ttu-id="8fc78-168">Una dirección IP pública a nivel de instancia es un tipo de dirección IP pública (denominada ILPIP) que se asigna directamente a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8fc78-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly to your VM.</span></span> <span data-ttu-id="8fc78-169">No se puede reservar.</span><span class="sxs-lookup"><span data-stu-id="8fc78-169">It cannot be reserved.</span></span> <span data-ttu-id="8fc78-170">Para más información, lea el artículo [Dirección IP pública a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-170">For more information, read the [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="8fc78-171">Eliminación de una dirección IP reservada de una implementación en ejecución</span><span class="sxs-lookup"><span data-stu-id="8fc78-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="8fc78-172">Para quitar una IP reservada que se agregó a un servicio en la nube nuevo, ejecute el siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8fc78-172">To remove a reserved IP added to a new cloud service, run the following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="8fc78-173">Quitar una IP reservada de una implementación en ejecución, no se elimina la reserva de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8fc78-173">Removing a reserved IP from a running deployment does not remove the reservation from your subscription.</span></span> <span data-ttu-id="8fc78-174">Simplemente libera la dirección IP que será usada por otro recurso de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="8fc78-174">It simply frees the IP to be used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-to-a-running-deployment"></a><span data-ttu-id="8fc78-175">Asociación de una dirección IP reservada a una implementación en ejecución</span><span class="sxs-lookup"><span data-stu-id="8fc78-175">Associate a reserved IP to a running deployment</span></span>
<span data-ttu-id="8fc78-176">Los comandos siguientes crean un servicio en la nube denominado *TestService2* con una máquina virtual nueva llamada *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="8fc78-176">The following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="8fc78-177">La IP reservada existente llamada *MyReservedIP* se asocia al servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="8fc78-177">The existing reserved IP named *MyReservedIP* is then associated to the cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-to-a-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="8fc78-178">Asociación de una dirección IP reservada a un servicio en la nube mediante un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="8fc78-178">Associate a reserved IP to a cloud service by using a service configuration file</span></span>
<span data-ttu-id="8fc78-179">También puede asociar una IP reservada a un servicio en la nube mediante un archivo de configuración de servicio (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="8fc78-179">You can also associate a reserved IP to a cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="8fc78-180">El xml de ejemplo siguiente muestra cómo configurar un servicio en la nube para que use una VIP reservada denominada *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="8fc78-180">The following sample xml shows how to configure a cloud service to use a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="8fc78-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8fc78-181">Next steps</span></span>
* <span data-ttu-id="8fc78-182">Descubra cómo funcionan las [direcciones IP](virtual-network-ip-addresses-overview-classic.md) en el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="8fc78-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="8fc78-183">Obtenga más información acerca de las [direcciones IP privadas reservadas](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="8fc78-184">Obtenga más información acerca de las [direcciones IP públicas de nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="8fc78-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

