---
title: "aaaCreate una máquina virtual (clásica) con varias NIC mediante PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate y configurar las máquinas virtuales con varias NIC con PowerShell."
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
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="f8de0-103">Creación de una máquina virtual (clásica) con varias NIC</span><span class="sxs-lookup"><span data-stu-id="f8de0-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="f8de0-104">Puede crear máquinas virtuales (VM) en Azure y conectar múltiples tooeach (NIC) de interfaces de red de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f8de0-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="f8de0-105">Tener varias NIC es un requisito para muchos dispositivos virtuales de red, por ejemplo, las soluciones de optimización de WAN y de entrega de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f8de0-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="f8de0-106">Varias NIC también aportan aislamiento del tráfico entre ellas.</span><span class="sxs-lookup"><span data-stu-id="f8de0-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Varias NIC para máquina virtual](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="f8de0-108">Hola ilustración, se muestra una máquina virtual con tres NICs, cada uno conectado tooa otra subred.</span><span class="sxs-lookup"><span data-stu-id="f8de0-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8de0-109">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f8de0-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f8de0-110">Este artículo incluye el uso de modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8de0-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="f8de0-111">Microsoft recomienda que las implementaciones más recientes usen Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f8de0-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="f8de0-112">VIP a través de Internet (implementaciones clásicas) solo se admite en la NIC de Hola "predeterminada".</span><span class="sxs-lookup"><span data-stu-id="f8de0-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="f8de0-113">Hay solo una dirección IP de toohello de VIP de NIC de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f8de0-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="f8de0-114">En estos momentos, no se admiten direcciones IP públicas (implementaciones clásicas) de nivel de instancia (LPIP) para máquinas virtuales con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="f8de0-115">Hola orden de NIC de Hola desde dentro de hello VM será aleatorio y también podría cambiar en todas las actualizaciones de infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8de0-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="f8de0-116">Sin embargo, direcciones IP de Hola y Hola MAC de ethernet correspondiente permanecerán direcciones Hola igual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="f8de0-117">Por ejemplo, suponga **Eth1** tiene la dirección IP 10.1.0.100 y la dirección MAC 00-0D-3A-B0-39-0D; después de una actualización de la infraestructura de Azure y un reinicio, se podría cambiar demasiado**Eth2**, pero Hola IP y MAC emparejamiento will permanecen Hola igual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="f8de0-118">Cuando un reinicio es iniciado por el cliente, Hola orden de NIC seguirá siendo Hola igual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="f8de0-119">Hello dirección para cada NIC en cada máquina virtual debe estar ubicado en una subred, varias NIC en una sola máquina virtual cada uno se puede asignar direcciones que se encuentran en Hola misma subred.</span><span class="sxs-lookup"><span data-stu-id="f8de0-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="f8de0-120">Hola tamaño de máquina virtual determina el número de Hola de NIC que se pueden crear para una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="f8de0-121">Hola de referencia [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) y [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tamaños de VM artículos toodetermine cuántas NIC es compatible con el tamaño de cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="f8de0-122">Grupos de seguridad de red (NSG)</span><span class="sxs-lookup"><span data-stu-id="f8de0-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="f8de0-123">En una implementación del Administrador de recursos, cualquier NIC de una máquina virtual puede asociarse a un grupo de seguridad de red (NSG), incluyendo cualquier NIC de una máquina virtual que tenga varias NIC habilitadas.</span><span class="sxs-lookup"><span data-stu-id="f8de0-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="f8de0-124">Si una NIC se asigna una dirección de una subred que está asociado con un NSG subred hello, a continuación, hello reglas en NSG la subred de hello también aplican toothat equipo NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="f8de0-125">En subredes tooassociating de suma con NSG, también puede asociar una NIC con un NSG.</span><span class="sxs-lookup"><span data-stu-id="f8de0-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="f8de0-126">Si una subred está asociada con un NSG y una NIC en esa subred individualmente asociada a un NSG, se aplican las reglas NSG de hello asociado en **flujo orden** según la dirección de toohello del tráfico de Hola que se pasa dentro o fuera de Hola NIC:</span><span class="sxs-lookup"><span data-stu-id="f8de0-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="f8de0-127">**El tráfico entrante** cuyo destino es hello NIC en cuestión fluyen primero a través de la subred hello, desencadenar reglas NSG de la subred de hello, antes de pasar a Hola NIC, a continuación, desencadenar reglas de NSG Hola NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="f8de0-128">**El tráfico saliente** cuyo origen es hello NIC en cuestión fluyen primero en salir de hello NIC, desencadenar reglas NSG del NIC hello, antes de pasar a través de la subred de hello, a continuación, desencadenar reglas de NSG Hola la subred.</span><span class="sxs-lookup"><span data-stu-id="f8de0-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="f8de0-129">Obtenga más información sobre [grupos de seguridad de red](virtual-networks-nsg.md) y cómo se aplican en función de las asociaciones toosubnets, las máquinas virtuales y NIC...</span><span class="sxs-lookup"><span data-stu-id="f8de0-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="f8de0-130">¿Cómo tooConfigure una VM de NIC múltiples en una implementación clásica</span><span class="sxs-lookup"><span data-stu-id="f8de0-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="f8de0-131">instrucciones de Hola a continuación le ayudará a crear una VM de NIC con 3 NIC múltiples: una NIC predeterminada y dos NIC adicionales.</span><span class="sxs-lookup"><span data-stu-id="f8de0-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="f8de0-132">pasos de configuración de Hello creará una máquina virtual que se configurarán según el fragmento de archivo de configuración de servicio de toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8de0-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

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
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="f8de0-133">Necesita Hola siguiendo los requisitos previos antes de intentar toorun comandos de PowerShell de hello en el ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f8de0-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="f8de0-134">Una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8de0-134">An Azure subscription.</span></span>
* <span data-ttu-id="f8de0-135">Una red virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="f8de0-135">A configured virtual network.</span></span> <span data-ttu-id="f8de0-136">Para obtener más información sobre redes virtuales, consulte [Información general sobre redes virtuales](virtual-networks-overview.md) .</span><span class="sxs-lookup"><span data-stu-id="f8de0-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="f8de0-137">versión más reciente de Hola de Azure PowerShell descargado e instalado.</span><span class="sxs-lookup"><span data-stu-id="f8de0-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="f8de0-138">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f8de0-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f8de0-139">toocreate una máquina virtual con varias NIC, Hola completa siguiendo los pasos, escriba cada comando en una única sesión de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f8de0-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="f8de0-140">Seleccione una imagen de máquina virutal en la galería de imágenes de máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8de0-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="f8de0-141">Tenga en cuenta que las imágenes cambian con frecuencia y están disponibles por región.</span><span class="sxs-lookup"><span data-stu-id="f8de0-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="f8de0-142">Hello imagen especificada en el siguiente ejemplo de Hola puede cambiar o puede no estar en su región, por lo que toospecify imagen de Hola que se necesita.</span><span class="sxs-lookup"><span data-stu-id="f8de0-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="f8de0-143">Creación de una configuración de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f8de0-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="f8de0-144">Crear el inicio de sesión de administrador de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="f8de0-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="f8de0-145">Agregar configuración de máquina virtual de toohello NIC adicional.</span><span class="sxs-lookup"><span data-stu-id="f8de0-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="f8de0-146">Especifique una subred de Hola y dirección IP para la NIC de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f8de0-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="f8de0-147">Crear Hola VM en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f8de0-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="f8de0-148">Hola red virtual que especifique aquí debe existir (como se menciona en los requisitos previos de hello).</span><span class="sxs-lookup"><span data-stu-id="f8de0-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="f8de0-149">ejemplo de Hola siguiente especifica una red virtual denominada **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="f8de0-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="f8de0-150">Limitaciones</span><span class="sxs-lookup"><span data-stu-id="f8de0-150">Limitations</span></span>
<span data-ttu-id="f8de0-151">Hola siguientes limitaciones es aplicable al uso de varias NIC:</span><span class="sxs-lookup"><span data-stu-id="f8de0-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="f8de0-152">Las máquinas virtuales con varias NIC deben crearse en redes virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="f8de0-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="f8de0-153">Las máquinas virtuales que no son de redes virtuales no se pueden configurar con varias NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="f8de0-154">Todas las máquinas virtuales en la disponibilidad de un conjunto necesidad toouse varios NIC o una NIC único.</span><span class="sxs-lookup"><span data-stu-id="f8de0-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="f8de0-155">En un conjunto de disponibilidad no puede haber una combinación de máquinas virtuales de varias NIC y de NIC única.</span><span class="sxs-lookup"><span data-stu-id="f8de0-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="f8de0-156">Para las máquinas virtuales de un servicio en la nube se aplican las mismas reglas.</span><span class="sxs-lookup"><span data-stu-id="f8de0-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="f8de0-157">Varias NIC máquinas virtuales, no están necesarios que toohave Hola el mismo número de NIC, siempre y cuando cada uno de ellos tiene al menos dos.</span><span class="sxs-lookup"><span data-stu-id="f8de0-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="f8de0-158">Una máquina virtual con una NIC única no se puede configurar con varias NIC (y viceversa) una vez implementada si no se elimina y se vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="f8de0-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="f8de0-159">NIC secundarias tener acceso a subredes de tooother</span><span class="sxs-lookup"><span data-stu-id="f8de0-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="f8de0-160">De forma predeterminada la NIC secundarias no se configurarán con una puerta de enlace predeterminada, debido toowhich flujo de tráfico de hello en hello NIC secundarias será toobe limitado en hello misma subred.</span><span class="sxs-lookup"><span data-stu-id="f8de0-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="f8de0-161">Si desean que los usuarios de hello tooenable secundaria NIC tootalk fuera de su propia subred, necesitarán tooadd una entrada de hello enrutamiento tabla tooconfigure Hola puerta de enlace como se describe a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8de0-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="f8de0-162">Las máquinas virtuales creadas antes de julio de 2015 pueden tener una puerta de enlace predeterminada configurada para todas las NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="f8de0-163">Hola puerta de enlace predeterminada NIC secundarias no se quitará hasta que estas máquinas virtuales se reinician.</span><span class="sxs-lookup"><span data-stu-id="f8de0-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="f8de0-164">En los sistemas operativos que utilizan Hola modelo enrutamiento de host no seguro, como Linux, puede interrumpir la conectividad a Internet si el tráfico de entrada y salida hello usa NIC diferentes.</span><span class="sxs-lookup"><span data-stu-id="f8de0-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="f8de0-165">Configurar las máquinas virtuales de Windows</span><span class="sxs-lookup"><span data-stu-id="f8de0-165">Configure Windows VMs</span></span>
<span data-ttu-id="f8de0-166">Suponga que tiene una máquina virtual de Windows con dos NIC, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="f8de0-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="f8de0-167">Dirección IP de la NIC principal: 192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="f8de0-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="f8de0-168">Dirección IP de la NIC secundaria: 192.168.2.5</span><span class="sxs-lookup"><span data-stu-id="f8de0-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="f8de0-169">tabla de rutas de IPv4 de Hola para esta máquina virtual sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8de0-169">hello IPv4 route table for this VM would look like this:</span></span>

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

<span data-ttu-id="f8de0-170">Tenga en cuenta que esa ruta de hello predeterminada (0.0.0.0) es sólo toohello disponibles de NIC principal</span><span class="sxs-lookup"><span data-stu-id="f8de0-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="f8de0-171">No será capaz de tooaccess recursos externos a subred Hola para hello secundaria NIC, tal como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="f8de0-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="f8de0-172">tooadd enrutar el valor predeterminado de Hola NIC secundaria, siga los pasos de Hola a continuación:</span><span class="sxs-lookup"><span data-stu-id="f8de0-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="f8de0-173">Desde un símbolo del sistema, ejecute el comando de Hola por debajo del número de índice de hello tooidentify de hello NIC secundaria:</span><span class="sxs-lookup"><span data-stu-id="f8de0-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="f8de0-174">Observe la segunda entrada de hello en la tabla de hello, con un índice de 27 (en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="f8de0-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="f8de0-175">Hola desde línea de comandos, ejecute hello **Agregar ruta** comando tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="f8de0-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="f8de0-176">En este ejemplo, está especificando 192.168.2.1 como Hola puerta de enlace predeterminada Hola NIC secundaria:</span><span class="sxs-lookup"><span data-stu-id="f8de0-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="f8de0-177">conectividad de tootest atrás toohello símbolo e intenta tooping una subred distinta de Hola NIC secundaria como se muestra int eh ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="f8de0-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="f8de0-178">También puede comprobar su hello toocheck de tabla de ruta recién agregado ruta, tal y como se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="f8de0-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="f8de0-179">Configurar máquinas virtuales de Linux</span><span class="sxs-lookup"><span data-stu-id="f8de0-179">Configure Linux VMs</span></span>
<span data-ttu-id="f8de0-180">Para máquinas virtuales de Linux, puesto que comportamiento predeterminado de hello utiliza host débil enrutamiento, es recomendable que Hola NIC secundarias son flujos de tootraffic restringida solo dentro de hello misma subred.</span><span class="sxs-lookup"><span data-stu-id="f8de0-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="f8de0-181">Sin embargo, si determinados escenarios exigen conectividad exterior de la subred hello, los usuarios deben habilitar tooensure de enrutamiento basada en directivas que Hola entrada y usos de tráfico de salida Hola mismo NIC.</span><span class="sxs-lookup"><span data-stu-id="f8de0-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8de0-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f8de0-182">Next steps</span></span>
* <span data-ttu-id="f8de0-183">Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación del Administrador de recursos](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="f8de0-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="f8de0-184">Implemente [máquinas virtuales MultiNIC en un escenario de aplicación de 2 niveles en una implementación clásica](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f8de0-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

