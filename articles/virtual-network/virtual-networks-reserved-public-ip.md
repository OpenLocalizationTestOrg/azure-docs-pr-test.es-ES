---
title: "aaaManage Azure reservado de direcciones IP (clásico) - PowerShell | Documentos de Microsoft"
description: "Comprender las direcciones IP reservadas (clásico) y cómo toomanage mediante PowerShell."
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
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="af5b2-103">Direcciones IP reservadas (clásico)</span><span class="sxs-lookup"><span data-stu-id="af5b2-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="af5b2-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="af5b2-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="af5b2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="af5b2-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="af5b2-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="af5b2-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="af5b2-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="af5b2-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="af5b2-108">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="af5b2-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="af5b2-109">Las direcciones IP en Azure se dividen en dos categorías: dinámicas y reservadas.</span><span class="sxs-lookup"><span data-stu-id="af5b2-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="af5b2-110">Las direcciones IP públicas administradas por Azure son dinámicas de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="af5b2-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="af5b2-111">Ese decir Hola dirección IP usada para un servicio de nube determinado (VIP) o tooaccess que una máquina virtual o instancia de rol directamente (ILPIP) puede cambiar de tiempo tootime, cuando los recursos se apague o detenidos (desasignados).</span><span class="sxs-lookup"><span data-stu-id="af5b2-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="af5b2-112">direcciones IP de tooprevent cambie, puede reservar una dirección IP.</span><span class="sxs-lookup"><span data-stu-id="af5b2-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="af5b2-113">Direcciones IP reservadas se puede utilizar como una VIP, asegurarse de esa dirección IP de Hola para servicio de nube de hello sigue siendo Hola mismo, incluso cuando los recursos se cierran o detenida (desasignada).</span><span class="sxs-lookup"><span data-stu-id="af5b2-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="af5b2-114">Además, puede convertir existente IP dinámicas que se utiliza como una dirección IP de tooa reservado de VIP.</span><span class="sxs-lookup"><span data-stu-id="af5b2-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af5b2-115">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="af5b2-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="af5b2-116">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="af5b2-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="af5b2-117">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="af5b2-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="af5b2-118">Obtenga información acerca de cómo tooreserve una estática pública IP dirección utilizando Hola [modelo de implementación del Administrador de recursos](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="af5b2-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="af5b2-119">direcciones toolearn más información acerca de IP en Azure, lea hello [direcciones IP](virtual-network-ip-addresses-overview-classic.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="af5b2-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="af5b2-120">¿Cuándo se necesita una IP reservada?</span><span class="sxs-lookup"><span data-stu-id="af5b2-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="af5b2-121">**Desea tooensure que Hola IP está reservada en su suscripción**.</span><span class="sxs-lookup"><span data-stu-id="af5b2-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="af5b2-122">Si desea tooreserve una dirección IP que no se libera de su suscripción bajo ninguna circunstancia, debe usar una IP pública reservada.</span><span class="sxs-lookup"><span data-stu-id="af5b2-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="af5b2-123">**Desea que su toostay IP con el servicio de nube incluso a través detenido o desasignado (máquinas virtuales) del estado**.</span><span class="sxs-lookup"><span data-stu-id="af5b2-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="af5b2-124">Si desea que su toobe servicio acceso mediante una dirección IP que no cambia, incluso cuando la nube de máquinas virtuales en hello servicio se hayan cerrado o detener (desasignado).</span><span class="sxs-lookup"><span data-stu-id="af5b2-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="af5b2-125">**Desea que el tráfico saliente desde Azure use una dirección IP predecible de tooensure**.</span><span class="sxs-lookup"><span data-stu-id="af5b2-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="af5b2-126">Puede que tenga el tráfico local firewall configurado tooallow solo desde direcciones IP específicas.</span><span class="sxs-lookup"><span data-stu-id="af5b2-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="af5b2-127">Al reservar una dirección IP, sabrá que la IP de origen de Hola de direcciones y no es necesario tooupdate las reglas del firewall debido a cambios IP tooan.</span><span class="sxs-lookup"><span data-stu-id="af5b2-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="af5b2-128">P+F</span><span class="sxs-lookup"><span data-stu-id="af5b2-128">FAQ</span></span>
1. <span data-ttu-id="af5b2-129">¿Puedo usar una IP reservada para todos los servicios de Azure?</span><span class="sxs-lookup"><span data-stu-id="af5b2-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="af5b2-130">No.</span><span class="sxs-lookup"><span data-stu-id="af5b2-130">No.</span></span> <span data-ttu-id="af5b2-131">Las IP reservadas solo pueden usarse para máquinas virtuales y roles de instancia del servicio en la nube que se hayan expuesto a través de una VIP.</span><span class="sxs-lookup"><span data-stu-id="af5b2-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="af5b2-132">¿Cuántas direcciones IP reservadas puedo tener?</span><span class="sxs-lookup"><span data-stu-id="af5b2-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="af5b2-133">Para obtener más información, vea hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="af5b2-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="af5b2-134">¿Hay un cargo por las IP reservadas?</span><span class="sxs-lookup"><span data-stu-id="af5b2-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="af5b2-135">A veces.</span><span class="sxs-lookup"><span data-stu-id="af5b2-135">Sometimes.</span></span> <span data-ttu-id="af5b2-136">Para obtener más detalles, consulte hello [detalles de precios de la dirección de IP reservada](http://go.microsoft.com/fwlink/?LinkID=398482) página.</span><span class="sxs-lookup"><span data-stu-id="af5b2-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="af5b2-137">¿Cómo se reserva una dirección IP?</span><span class="sxs-lookup"><span data-stu-id="af5b2-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="af5b2-138">Puede usar PowerShell, hello [API de REST de administración de Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), o hello [portal de Azure](https://portal.azure.com) tooreserve una dirección IP en una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="af5b2-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="af5b2-139">Una dirección IP reservada es suscripción tooyour asociado.</span><span class="sxs-lookup"><span data-stu-id="af5b2-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="af5b2-140">¿Puedo usar una IP reservada con redes virtuales basadas en grupos de afinidad?</span><span class="sxs-lookup"><span data-stu-id="af5b2-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="af5b2-141">No.</span><span class="sxs-lookup"><span data-stu-id="af5b2-141">No.</span></span> <span data-ttu-id="af5b2-142">Las IP reservadas solo se admiten en redes virtuales regionales.</span><span class="sxs-lookup"><span data-stu-id="af5b2-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="af5b2-143">Las IP reservadas no se admiten para redes virtuales asociadas a grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="af5b2-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="af5b2-144">Para obtener más información sobre cómo asociar una red virtual a una región o un grupo de afinidad, vea hello [acerca de las redes virtuales regionales y grupos de afinidad](virtual-networks-migrate-to-regional-vnet.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="af5b2-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="af5b2-145">Administración de VIP reservadas</span><span class="sxs-lookup"><span data-stu-id="af5b2-145">Manage reserved VIPs</span></span>

<span data-ttu-id="af5b2-146">Asegúrese de que haya instalado y configurado PowerShell siguiendo los pasos de Hola Hola [instalar y configurar PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="af5b2-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="af5b2-147">Para poder usar direcciones IP reservadas, se debe agregar suscripción tooyour.</span><span class="sxs-lookup"><span data-stu-id="af5b2-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="af5b2-148">toocreate una dirección IP reservada del grupo de Hola de IP pública de direcciones disponibles en hello *Central US* ubicación, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="af5b2-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="af5b2-149">Sin embargo, tenga en cuenta que no puede especificar qué IP se va a reservar.</span><span class="sxs-lookup"><span data-stu-id="af5b2-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="af5b2-150">tooview ¿qué direcciones IP están reservadas en su suscripción, ejecute hello siguiente comando de PowerShell y observe los valores de hello en *ReservedIPName* y *dirección*:</span><span class="sxs-lookup"><span data-stu-id="af5b2-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="af5b2-151">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="af5b2-151">Expected output:</span></span>

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
><span data-ttu-id="af5b2-152">Cuando se crea una dirección IP reservada con PowerShell, no puede especificar una dirección IP Hola reservado de recursos grupo toocreate en.</span><span class="sxs-lookup"><span data-stu-id="af5b2-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="af5b2-153">Azure lo coloca automáticamente en un grupo de recursos llamado *Default-Networking*.</span><span class="sxs-lookup"><span data-stu-id="af5b2-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="af5b2-154">Si crea la dirección IP de hello reservado mediante hello [portal de Azure](http://portal.azure.com), puede especificar cualquier grupo de recursos que elija.</span><span class="sxs-lookup"><span data-stu-id="af5b2-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="af5b2-155">Si creas Hola reservado IP en un grupo de recursos distinto de *predeterminado redes* sin embargo, cada vez que se hace referencia a Hola dirección IP reservada con comandos como `Get-AzureReservedIP` y `Remove-AzureReservedIP`, debe hacer referencia el nombre de hello *Nombre del grupo de recursos reservados-ip-nombre del grupo*.</span><span class="sxs-lookup"><span data-stu-id="af5b2-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="af5b2-156">Por ejemplo, si creas una IP reservada denominada *myReservedIP* en un grupo de recursos denominado *myResourceGroup*, debe hacer referencia a nombre Hola de IP de hello reservado como *myResourceGroup de grupo myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="af5b2-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="af5b2-157">Una vez que se reserva una dirección IP, permanece asociado tooyour suscripción hasta que la elimine.</span><span class="sxs-lookup"><span data-stu-id="af5b2-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="af5b2-158">toodelete una dirección IP reservada, Hola ejecución siguiente comando de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="af5b2-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="af5b2-159">Reservar la dirección IP de Hola de un servicio de nube existente</span><span class="sxs-lookup"><span data-stu-id="af5b2-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="af5b2-160">Puede reservar dirección IP de Hola de un servicio de nube existente mediante la adición de hello `-ServiceName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="af5b2-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="af5b2-161">dirección IP de hello tooreserve de un servicio de nube *TestService* en hello *Central US* ubicación, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="af5b2-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="af5b2-162">Asociar un reservada IP tooa nuevo servicio de nube</span><span class="sxs-lookup"><span data-stu-id="af5b2-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="af5b2-163">Hello siguiente script crea una dirección de IP reservada nuevas, a continuación, lo asocia el nuevo servicio de nube tooa denominado *TestService*.</span><span class="sxs-lookup"><span data-stu-id="af5b2-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="af5b2-164">Cuando se crea un toouse IP reservada con un servicio de nube, seguir haciendo referencia toohello VM mediante el uso de *VIP:&lt;número de puerto >* para las comunicaciones entrantes.</span><span class="sxs-lookup"><span data-stu-id="af5b2-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="af5b2-165">Reservar una dirección IP no significa que puede conectarse directamente toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af5b2-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="af5b2-166">Hello IP reservada se asigna en la nube toohello servicio ese hello en la máquina virtual se ha implementado en.</span><span class="sxs-lookup"><span data-stu-id="af5b2-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="af5b2-167">Si desea tooconnect tooa máquina virtual por medio de IP directamente, deberá tooconfigure una IP pública a nivel de instancia.</span><span class="sxs-lookup"><span data-stu-id="af5b2-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="af5b2-168">Una dirección IP pública de nivel de instancia es un tipo de IP pública (denominado un ILPIP) que se asigna directamente tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="af5b2-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="af5b2-169">No se puede reservar.</span><span class="sxs-lookup"><span data-stu-id="af5b2-169">It cannot be reserved.</span></span> <span data-ttu-id="af5b2-170">Para obtener más información, lea hello [IP pública de nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="af5b2-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="af5b2-171">Eliminación de una dirección IP reservada de una implementación en ejecución</span><span class="sxs-lookup"><span data-stu-id="af5b2-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="af5b2-172">una dirección IP reservada tooremove agregado tooa nuevo servicio en la nube, ejecute el siguiente comando de PowerShell de hello:</span><span class="sxs-lookup"><span data-stu-id="af5b2-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="af5b2-173">Quitar una dirección IP reservada de una implementación en ejecución no quita la reserva de Hola desde su suscripción.</span><span class="sxs-lookup"><span data-stu-id="af5b2-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="af5b2-174">Simplemente libera Hola IP toobe utilizado por otro recurso de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="af5b2-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="af5b2-175">Asociar un tooa IP reservada ejecutando implementación</span><span class="sxs-lookup"><span data-stu-id="af5b2-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="af5b2-176">Hello siguientes comandos crean un servicio de nube denominado *TestService2* con una nueva máquina virtual denominada *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="af5b2-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="af5b2-177">Hola existente reservado IP denominado *MyReservedIP* es, a continuación, el servicio en la nube toohello asociado.</span><span class="sxs-lookup"><span data-stu-id="af5b2-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="af5b2-178">Asociar un servicio de nube de tooa IP reservado mediante un archivo de configuración de servicio</span><span class="sxs-lookup"><span data-stu-id="af5b2-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="af5b2-179">También puede asociar un servicio de nube de tooa IP reservado mediante un archivo de configuración (CSCFG) de servicio.</span><span class="sxs-lookup"><span data-stu-id="af5b2-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="af5b2-180">Hello xml de ejemplo siguiente muestra cómo tooconfigure una toouse de servicio de nube una VIP reservada denominado *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="af5b2-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="af5b2-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="af5b2-181">Next steps</span></span>
* <span data-ttu-id="af5b2-182">Comprender cómo [el direccionamiento IP](virtual-network-ip-addresses-overview-classic.md) funciona en el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="af5b2-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="af5b2-183">Obtenga más información acerca de las [direcciones IP privadas reservadas](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="af5b2-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="af5b2-184">Obtenga más información acerca de las [direcciones IP públicas de nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="af5b2-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

