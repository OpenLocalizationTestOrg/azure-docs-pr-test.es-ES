---
title: "Implementar máquinas virtuales con varias NIC (clásica) mediante PowerShell | Microsoft Docs"
description: "Aprenda a crear y configurar máquinas virtuales con varias tarjetas NIC mediante PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 68ccc1cac22e593b099729fe68c6bee63df44d9b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="41b5f-103">Creación de una máquina virtual (clásica) con varias NIC</span><span class="sxs-lookup"><span data-stu-id="41b5f-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="41b5f-104">Puede crear máquinas virtuales (VM) en Azure y asociar varias interfaces de red (NIC) a cada una de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="41b5f-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="41b5f-105">Tener varias NIC es un requisito para muchos dispositivos virtuales de red, por ejemplo, las soluciones de optimización de WAN y de entrega de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="41b5f-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="41b5f-106">Varias NIC también aportan aislamiento del tráfico entre ellas.</span><span class="sxs-lookup"><span data-stu-id="41b5f-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Varias NIC para máquina virtual](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="41b5f-108">La figura anterior muestra una máquina virtual con tres NIC, cada una de ellas conectada a una subred diferente.</span><span class="sxs-lookup"><span data-stu-id="41b5f-108">The figure shows a VM with three NICs, each connected to a different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41b5f-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="41b5f-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="41b5f-110">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="41b5f-110">This article covers using the classic deployment model.</span></span> <span data-ttu-id="41b5f-111">Microsoft recomienda que las implementaciones más recientes usen Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41b5f-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="41b5f-112">La VIP accesible desde Internet (implementaciones clásicas) solo se admite en la NIC marcada como "predeterminada".</span><span class="sxs-lookup"><span data-stu-id="41b5f-112">Internet-facing VIP (classic deployments) is only supported on the "default" NIC.</span></span> <span data-ttu-id="41b5f-113">Solo hay una VIP a la IP de la NIC predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41b5f-113">There is only one VIP to the IP of the default NIC.</span></span>
* <span data-ttu-id="41b5f-114">En estos momentos, no se admiten direcciones IP públicas (implementaciones clásicas) de nivel de instancia (LPIP) para máquinas virtuales con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="41b5f-115">El orden de las NIC desde la máquina virtual será aleatorio y también podría cambiar en todas las actualizaciones de infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b5f-115">The order of the NICs from inside the VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="41b5f-116">Sin embargo, las direcciones IP y las direcciones MAC Ethernet correspondientes seguirán siendo las mismas.</span><span class="sxs-lookup"><span data-stu-id="41b5f-116">However, the IP addresses, and the corresponding ethernet MAC addresses will remain the same.</span></span> <span data-ttu-id="41b5f-117">Por ejemplo, suponga que **Eth1** tiene la dirección IP 10.1.0.100 y la dirección MAC 00-0D-3A-B0-39-0D; después de una actualización de la infraestructura de Azure y de reiniciar el equipo, se podría cambiar a **Eth2**, pero el emparejamiento de la IP y la MAC seguirá siendo el mismo.</span><span class="sxs-lookup"><span data-stu-id="41b5f-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed to **Eth2**, but the IP and MAC pairing will remain the same.</span></span> <span data-ttu-id="41b5f-118">Cuando es un cliente quien ejecuta un reinicio, el orden de NIC seguirá siendo el mismo.</span><span class="sxs-lookup"><span data-stu-id="41b5f-118">When a restart is customer-initiated, the NIC order will remain the same.</span></span>
* <span data-ttu-id="41b5f-119">La dirección de cada NIC en cada máquina virtual debe estar ubicada en una subred; las direcciones que se encuentran en la misma subred se pueden asignar a cada una de las varias NIC de una sola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b5f-119">The address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in the same subnet.</span></span>
* <span data-ttu-id="41b5f-120">El tamaño de la máquina virtual determina el número de las NIC que se puede crear para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b5f-120">The VM size determines the number of NICS that you can create for a VM.</span></span> <span data-ttu-id="41b5f-121">Consulte los artículos sobre el tamaño de las máquinas virtuales [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para determinar cuántas NIC admite cada tamaño.</span><span class="sxs-lookup"><span data-stu-id="41b5f-121">Reference the [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles to determine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="41b5f-122">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="41b5f-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="41b5f-123">En una implementación del Administrador de recursos, cualquier NIC de una máquina virtual puede asociarse a un grupo de seguridad de red (NSG), incluyendo cualquier NIC de una máquina virtual que tenga varias NIC habilitadas.</span><span class="sxs-lookup"><span data-stu-id="41b5f-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="41b5f-124">Si a una NIC se le asigna una dirección dentro de una subred que está asociada a un NSG, las reglas de NSG de la subred también se aplican a esa NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-124">If a NIC is assigned an address within a subnet where the subnet is associated with an NSG, then the rules in the subnet’s NSG also apply to that NIC.</span></span> <span data-ttu-id="41b5f-125">Además de asociar subredes a NSG, también puede asociar una NIC a un NSG.</span><span class="sxs-lookup"><span data-stu-id="41b5f-125">In addition to associating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="41b5f-126">Si una subred está asociada a un NSG y una NIC dentro de esa subred está asociada individualmente a un NSG, las reglas asociadas de NSG se aplican en **orden de flujo** según la dirección del tráfico que se pasa dentro o fuera de la NIC:</span><span class="sxs-lookup"><span data-stu-id="41b5f-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, the associated NSG rules are applied in **flow order** according to the direction of the traffic being passed into or out of the NIC:</span></span>

* <span data-ttu-id="41b5f-127">**tráfico entrante** cuyo destino es la NIC en cuestión fluye primero a través de la subred y desencadena las reglas de NSG de la subred antes de pasar a la NIC y desencadenar las reglas de NSG de la NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-127">**Incoming traffic** whose destination is the NIC in question flows first through the subnet, triggering the subnet’s NSG rules, before passing into the NIC, then triggering the NIC’s NSG rules.</span></span>
* <span data-ttu-id="41b5f-128">**tráfico de salida** cuyo origen es la NIC en cuestión fluye primero fuera de la NIC, desencadenando reglas de NSG de la NIC, antes de pasar a la subred y desencadenar reglas de NSG de la subred.</span><span class="sxs-lookup"><span data-stu-id="41b5f-128">**Outgoing traffic** whose source is the NIC in question flows first out from the NIC, triggering the NIC’s NSG rules, before passing through the subnet, then triggering the subnet’s NSG rules.</span></span>

<span data-ttu-id="41b5f-129">Obtener más información sobre los [Grupos de seguridad de red](virtual-networks-nsg.md) y cómo se aplican en función de las asociaciones de subredes, las máquinas virtuales y las NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations to subnets, VMs, and NICs..</span></span>

## <a name="how-to-configure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="41b5f-130">Cómo configurar una máquina virtual con varias NIC en una implementación clásica</span><span class="sxs-lookup"><span data-stu-id="41b5f-130">How to Configure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="41b5f-131">Las instrucciones siguientes le ayudarán a crear una máquina virtual de varias NIC con 3 NIC: una NIC predeterminada y dos NIC adicionales.</span><span class="sxs-lookup"><span data-stu-id="41b5f-131">The instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="41b5f-132">Los pasos de configuración crearán una máquina virtual que se configurará según el fragmento de archivo de configuración de servicio siguiente:</span><span class="sxs-lookup"><span data-stu-id="41b5f-132">The configuration steps will create a VM that will be configured according to the service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over the remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="41b5f-133">Necesitará cumplir los siguientes requisitos previos antes de poder ejecutar los comandos de PowerShell del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="41b5f-133">You need the following prerequisites before trying to run the PowerShell commands in the example.</span></span>

* <span data-ttu-id="41b5f-134">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b5f-134">An Azure subscription.</span></span>
* <span data-ttu-id="41b5f-135">Una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="41b5f-135">A configured virtual network.</span></span> <span data-ttu-id="41b5f-136">Para obtener más información sobre redes virtuales, consulte [Información general sobre redes virtuales](virtual-networks-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="41b5f-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="41b5f-137">La versión más reciente de Azure PowerShell descargada e instalada.</span><span class="sxs-lookup"><span data-stu-id="41b5f-137">The latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="41b5f-138">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41b5f-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="41b5f-139">Para crear una máquina virtual con varias NIC, complete los pasos siguientes escribiendo cada comando en una única sesión de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41b5f-139">To create a VM with multiple NICs, complete the following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="41b5f-140">Seleccione una imagen de máquina virutal en la galería de imágenes de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b5f-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="41b5f-141">Tenga en cuenta que las imágenes cambian con frecuencia y están disponibles por región.</span><span class="sxs-lookup"><span data-stu-id="41b5f-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="41b5f-142">La imagen especificada en el ejemplo siguiente puede cambiar o puede no estar presente en su región, así que asegúrese de especificar la imagen que necesita.</span><span class="sxs-lookup"><span data-stu-id="41b5f-142">The image specified in the example below may change or might not be in your region, so be sure to specify the image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="41b5f-143">Creación de una configuración de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="41b5f-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="41b5f-144">Cree el inicio de sesión de administrador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="41b5f-144">Create the default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="41b5f-145">Agregue NIC adicionales a la configuración de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="41b5f-145">Add additional NICs to the VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="41b5f-146">Especifique la subred y la dirección IP de la NIC predeterminada.</span><span class="sxs-lookup"><span data-stu-id="41b5f-146">Specify the subnet and IP address for the default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="41b5f-147">Cree la máquina virtual en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="41b5f-147">Create the VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="41b5f-148">La red virtual que especifique aquí debe existir previamente (tal como se indicó en los requisitos previos).</span><span class="sxs-lookup"><span data-stu-id="41b5f-148">The VNet that you specify here must already exist (as mentioned in the prerequisites).</span></span> <span data-ttu-id="41b5f-149">En el ejemplo siguiente se especifica una red virtual denominada **MultiNIC VNet**.</span><span class="sxs-lookup"><span data-stu-id="41b5f-149">The example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="41b5f-150">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="41b5f-150">Limitations</span></span>
<span data-ttu-id="41b5f-151">Se aplican las siguientes limitaciones al usar varias NIC:</span><span class="sxs-lookup"><span data-stu-id="41b5f-151">The following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="41b5f-152">Las máquinas virtuales con varias NIC deben crearse en redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="41b5f-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="41b5f-153">Las máquinas virtuales que no son de redes virtuales no se pueden configurar con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="41b5f-154">Todas las máquinas virtuales de un conjunto de disponibilidad deben usar varias NIC o una NIC única.</span><span class="sxs-lookup"><span data-stu-id="41b5f-154">All VMs in an availability set need to use either multiple NICs or a single NIC.</span></span> <span data-ttu-id="41b5f-155">En un conjunto de disponibilidad no puede haber una combinación de máquinas virtuales de varias NIC y de NIC única.</span><span class="sxs-lookup"><span data-stu-id="41b5f-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="41b5f-156">Para las máquinas virtuales de un servicio en la nube se aplican las mismas reglas.</span><span class="sxs-lookup"><span data-stu-id="41b5f-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="41b5f-157">No es necesario que las máquinas virtuales de varias NIC tengan el mismo número de tarjetas NIC, siempre y cuando cada una tenga al menos dos.</span><span class="sxs-lookup"><span data-stu-id="41b5f-157">For multiple NIC VMs, they aren't required to have the same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="41b5f-158">Una máquina virtual con una NIC única no se puede configurar con varias NIC (y viceversa) una vez implementada si no se elimina y se vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="41b5f-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-to-other-subnets"></a><span data-ttu-id="41b5f-159">Acceso de las NIC secundarias a otras subredes</span><span class="sxs-lookup"><span data-stu-id="41b5f-159">Secondary NICs access to other subnets</span></span>
<span data-ttu-id="41b5f-160">De forma predeterminada, las NIC secundarias no se configurarán con una puerta de enlace predeterminada, por lo que el flujo de tráfico en ellas se limitará para que esté dentro de la misma subred.</span><span class="sxs-lookup"><span data-stu-id="41b5f-160">By default secondary NICs will not be configured with a default gateway, due to which the traffic flow on the secondary NICs will be limited to be within the same subnet.</span></span> <span data-ttu-id="41b5f-161">Si los usuarios desean habilitar las NIC secundarias para comunicarse fuera de su propia subred, tendrán que agregar una entrada en la tabla de enrutamiento para configurar la puerta de enlace, tal y como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="41b5f-161">If the users want to enable secondary NICs to talk outside their own subnet, they will need to add an entry in the routing table to configure the gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="41b5f-162">Las máquinas virtuales creadas antes de julio de 2015 pueden tener una puerta de enlace predeterminada configurada para todas las NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="41b5f-163">La puerta de enlace predeterminada para las NIC secundarias no se quitará hasta que se hayan reiniciado estas máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="41b5f-163">The default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="41b5f-164">En los sistemas operativos que usan el modelo de enrutamiento de host no seguro (como Linux), la conectividad a Internet se puede interrumpir si el tráfico de entrada y salida usa NIC diferentes.</span><span class="sxs-lookup"><span data-stu-id="41b5f-164">In Operating systems that use the weak host routing model, such as Linux, Internet connectivity can break if the ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="41b5f-165">Configurar las máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="41b5f-165">Configure Windows VMs</span></span>
<span data-ttu-id="41b5f-166">Suponga que tiene una máquina virtual de Windows con dos NIC, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="41b5f-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="41b5f-167">Dirección IP de la NIC principal: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="41b5f-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="41b5f-168">Dirección IP de la NIC secundaria: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="41b5f-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="41b5f-169">La tabla de enrutamiento de IPv4 para esta máquina virtual tendría este aspecto:</span><span class="sxs-lookup"><span data-stu-id="41b5f-169">The IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="41b5f-170">Tenga en cuenta que la ruta predeterminada (0.0.0.0) sólo está disponible para la NIC principal.</span><span class="sxs-lookup"><span data-stu-id="41b5f-170">Notice that the default route (0.0.0.0) is only available to the primary NIC.</span></span> <span data-ttu-id="41b5f-171">No podrá obtener acceso a recursos externos a la subred de la NIC secundaria, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="41b5f-171">You will not be able to access resources outside the subnet for the secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="41b5f-172">Para agregar una ruta predeterminada en la NIC secundaria, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="41b5f-172">To add a default route on the secondary NIC, follow the steps below:</span></span>

1. <span data-ttu-id="41b5f-173">Desde un símbolo del sistema, ejecute el comando siguiente para identificar el número de índice de la NIC secundaria:</span><span class="sxs-lookup"><span data-stu-id="41b5f-173">From a command prompt, run the command below to identify the index number for the secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="41b5f-174">Busque la segunda entrada en la tabla con un índice de 27 (en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="41b5f-174">Notice the second entry in the table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="41b5f-175">Desde el símbolo del sistema, ejecute el comando **route add** tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="41b5f-175">From the command prompt, run the **route add** command as shown below.</span></span> <span data-ttu-id="41b5f-176">En este ejemplo, está especificando 192.168.2.1 como puerta de enlace predeterminada para la NIC secundaria:</span><span class="sxs-lookup"><span data-stu-id="41b5f-176">In this example, you are specifying 192.168.2.1 as the default gateway for the secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="41b5f-177">Para probar la conectividad, vuelva al símbolo del sistema e intente hacer ping en una subred distinta de la NIC secundaria, tal y como se muestra en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="41b5f-177">To test connectivity, go back to the command prompt and try to ping a different subnet from the secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="41b5f-178">Asimismo, puede consultar la tabla de rutas para comprobar la ruta recién agregada, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="41b5f-178">You can also check your route table to check the newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="41b5f-179">Configurar máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="41b5f-179">Configure Linux VMs</span></span>
<span data-ttu-id="41b5f-180">En cuanto a las máquinas virtuales de Linux, puesto que el comportamiento predeterminado está usando el enrutamiento del host no seguro, le recomendamos restrinja el flujo de tráfico de las NIC secundarias para que permanezca dentro de la misma subred.</span><span class="sxs-lookup"><span data-stu-id="41b5f-180">For Linux VMs, since the default behavior uses weak host routing, we recommend that the secondary NICs are restricted to traffic flows only within the same subnet.</span></span> <span data-ttu-id="41b5f-181">Sin embargo, si ciertos escenarios exigen que tenga conectividad fuera de la subred, los usuarios deben habilitar el enrutamiento basado en las directivas para asegurarse de que el tráfico de entrada y salida utiliza la misma NIC.</span><span class="sxs-lookup"><span data-stu-id="41b5f-181">However if certain scenarios demand connectivity outside the subnet, users should enable policy based routing to ensure that the ingress and egress traffic uses the same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41b5f-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="41b5f-182">Next steps</span></span>
* <span data-ttu-id="41b5f-183">Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="41b5f-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="41b5f-184">Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación clásica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="41b5f-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

