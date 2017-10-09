---
title: "asignación de aaaNetwork entre dos regiones de Azure en Azure Site Recovery | Documentos de Microsoft"
description: "Azure Site Recovery coordina la replicación hello, conmutación por error y recuperación de máquinas virtuales y servidores físicos. Obtenga información acerca de la conmutación por error tooAzure o un centro de datos secundaria."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 4f80c44e3f94eaf446bc01a7041d91fe34aa78d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="network-mapping-between-two-azure-regions"></a><span data-ttu-id="bfd81-104">Asignación de red entre dos regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bfd81-104">Network mapping between two Azure regions</span></span>


<span data-ttu-id="bfd81-105">Este artículo se describe cómo toomap Azure redes virtuales de dos regiones de Azure entre sí.</span><span class="sxs-lookup"><span data-stu-id="bfd81-105">This article describes how toomap Azure virtual networks of two Azure regions with each other.</span></span> <span data-ttu-id="bfd81-106">Asignación de red garantiza que cuando se crea la máquina virtual replicada en el destino de hello región de Azure, se crea en red virtual de Hola que sea asignada toovirtual red de máquina virtual de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-106">Network mapping ensures that when replicated virtual machine is created in hello target Azure region, it is created on hello virtual network that is mapped toovirtual network of hello source virtual machine.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="bfd81-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bfd81-107">Prerequisites</span></span>
<span data-ttu-id="bfd81-108">Antes de asignar redes, asegúrese de haber creado [redes virtuales de Azure](../virtual-network/virtual-networks-overview.md) en las regiones de Azure de origen y destino.</span><span class="sxs-lookup"><span data-stu-id="bfd81-108">Before you map networks make sure, you have created [Azure virtual networks](../virtual-network/virtual-networks-overview.md) in both source and target Azure regions.</span></span>

## <a name="map-networks"></a><span data-ttu-id="bfd81-109">Asignar redes</span><span class="sxs-lookup"><span data-stu-id="bfd81-109">Map networks</span></span>

<span data-ttu-id="bfd81-110">toomap una red virtual de Azure en red virtual de una región de Azure tooanother en otra región, vaya tooSite recuperación infraestructura -> asignación de red (para máquinas virtuales de Azure) y crear una asignación de red.</span><span class="sxs-lookup"><span data-stu-id="bfd81-110">toomap an Azure virtual network in one Azure region tooanother virtual network in another region, go tooSite Recovery Infrastructure -> Network Mapping (For Azure Virtual Machines) and create a network mapping.</span></span>

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping1.png)


<span data-ttu-id="bfd81-112">Hola ejemplo siguiente mi máquina virtual se está ejecutando en la región Este de Asia y se va a replica tooSoutheast Asia.</span><span class="sxs-lookup"><span data-stu-id="bfd81-112">In hello example below my virtual machine is running in East Asia region and is being replicated tooSoutheast Asia.</span></span>

<span data-ttu-id="bfd81-113">Seleccione la red de origen y de destino de hello y, a continuación, haga clic en Aceptar toocreate una asignación de red de Asia oriental tooSoutheast Asia.</span><span class="sxs-lookup"><span data-stu-id="bfd81-113">Select hello source and target network and then click OK toocreate a network mapping from East Asia tooSoutheast Asia.</span></span>

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping2.png)


<span data-ttu-id="bfd81-115">Hola mismo lo toocreate una asignación de red de tooEast sudeste de Asia oriental.</span><span class="sxs-lookup"><span data-stu-id="bfd81-115">Do hello same thing toocreate a network mapping from Southeast Asia tooEast Asia.</span></span>  
![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping3.png)


## <a name="mapping-network-when-enabling-replication"></a><span data-ttu-id="bfd81-117">Asignación de red al habilitar la replicación</span><span class="sxs-lookup"><span data-stu-id="bfd81-117">Mapping network when enabling replication</span></span>

<span data-ttu-id="bfd81-118">Si no se realizó la asignación de red al que esté replicando una máquina virtual para hello primera hora formulario una región de Azure tooanother, a continuación, puede elegir red de destino como parte del programa Hola mismo proceso.</span><span class="sxs-lookup"><span data-stu-id="bfd81-118">If network mapping is not done when you are replicating a virtual machine for hello first time form one Azure region tooanother, then you can choose target network as part of hello same process.</span></span> <span data-ttu-id="bfd81-119">Recuperación del sitio crea las asignaciones de red de área de tootarget de región de origen y de destino región toosource otra en función de esta selección.</span><span class="sxs-lookup"><span data-stu-id="bfd81-119">Site Recovery creates network mappings from source region tootarget region and from target region toosource region based on this selection.</span></span>   

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping4.png)

<span data-ttu-id="bfd81-121">De forma predeterminada, Site Recovery crea una red en la región de destino de Hola que sea idéntico toohello red de origen y mediante la adición de '-asr' como nombre de red de origen de hello toohello sufijo.</span><span class="sxs-lookup"><span data-stu-id="bfd81-121">By default, Site Recovery creates a network in hello target region that is identical toohello source network and by adding '-asr' as a suffix toohello name of hello source network.</span></span> <span data-ttu-id="bfd81-122">Puede elegir una red ya creada si hace clic en Personalizar.</span><span class="sxs-lookup"><span data-stu-id="bfd81-122">You can choose an already created network by clicking Customize.</span></span>

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping5.png)


<span data-ttu-id="bfd81-124">Si ya se realizó la asignación de red de hello, no se puede cambiar la red virtual de destino de hello mientras habilita la replicación.</span><span class="sxs-lookup"><span data-stu-id="bfd81-124">If hello network mapping is already done, you can't change hello target virtual network while enabling replication.</span></span> <span data-ttu-id="bfd81-125">toochange, modifique la asignación de red existente.</span><span class="sxs-lookup"><span data-stu-id="bfd81-125">toochange it, modify existing network mapping.</span></span>  

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/network-mapping6.png)

![Asignación de red](./media/site-recovery-network-mapping-azure-to-azure/modify-network-mapping.png)

> [!IMPORTANT]
> <span data-ttu-id="bfd81-128">Si modifica una asignación de red de la región 1 tooregion-2, asegúrese de que se modifique la asignación de red de Hola de región 2 tooregion-1 también.</span><span class="sxs-lookup"><span data-stu-id="bfd81-128">If you modify a network mapping from region-1 tooregion-2, make sure you modify hello network mapping from region-2 tooregion-1 as well.</span></span>
>
>


## <a name="subnet-selection"></a><span data-ttu-id="bfd81-129">Selección de subred</span><span class="sxs-lookup"><span data-stu-id="bfd81-129">Subnet selection</span></span>
<span data-ttu-id="bfd81-130">Subred de máquina virtual de destino de Hola se selecciona basándose en nombre de Hola de subred de Hola de máquina virtual de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-130">Subnet of hello target virtual machine is selected based on hello name of hello subnet of hello source virtual machine.</span></span> <span data-ttu-id="bfd81-131">Si no hay una subred de hello igual de nombre que el de la máquina virtual de origen de hello disponible en la red de destino de hello, se ha seleccionado para la máquina virtual de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-131">If there is a subnet of hello same name as that of hello source virtual machine available in hello target network, then that is chosen for hello target virtual machine.</span></span> <span data-ttu-id="bfd81-132">Si no hay ninguna subred con hello mismo nombre de red de destino de hello, a continuación, se elige alfabéticamente primera subred Hola subred de destino.</span><span class="sxs-lookup"><span data-stu-id="bfd81-132">If there is no subnet with hello same name in hello target network, then alphabetically first subnet is chosen as hello target subnet.</span></span> <span data-ttu-id="bfd81-133">Puede modificar esta subred, vaya a configuración de red de máquina virtual de Hola y tooCompute.</span><span class="sxs-lookup"><span data-stu-id="bfd81-133">You can modify this subnet by going tooCompute and Network settings of hello virtual machine.</span></span>

![Modificar la subred](./media/site-recovery-network-mapping-azure-to-azure/modify-subnet.png)


## <a name="ip-address"></a><span data-ttu-id="bfd81-135">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="bfd81-135">IP address</span></span>

<span data-ttu-id="bfd81-136">Dirección IP para cada interfaz de red de Hola Hola máquina virtual de destino se elige como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bfd81-136">IP address for each of hello network interface of hello target virtual machine is chosen as follows:</span></span>

### <a name="dhcp"></a><span data-ttu-id="bfd81-137">DHCP</span><span class="sxs-lookup"><span data-stu-id="bfd81-137">DHCP</span></span>
<span data-ttu-id="bfd81-138">Si la interfaz de red de Hola de máquina virtual de origen Hola utiliza DHCP, interfaz de red de máquina virtual de destino de hello también se establece como DHCP.</span><span class="sxs-lookup"><span data-stu-id="bfd81-138">If hello network interface of hello source virtual machine is using DHCP, then network interface of hello target virtual machine is also set as DHCP.</span></span>

### <a name="static-ip"></a><span data-ttu-id="bfd81-139">IP estática</span><span class="sxs-lookup"><span data-stu-id="bfd81-139">Static IP</span></span>
<span data-ttu-id="bfd81-140">Si la interfaz de red de Hola de máquina virtual de origen Hola utiliza direcciones IP estáticas, interfaz de red de máquina virtual de destino de hello también se establece toouse direcciones IP estáticas.</span><span class="sxs-lookup"><span data-stu-id="bfd81-140">If hello network interface of hello source virtual machine is using Static IP, then network interface of hello target virtual machine is also set toouse Static IP.</span></span> <span data-ttu-id="bfd81-141">La IP estática se elige como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="bfd81-141">Static IP is chosen as follows:</span></span>

#### <a name="same-address-space"></a><span data-ttu-id="bfd81-142">Mismo espacio de direcciones</span><span class="sxs-lookup"><span data-stu-id="bfd81-142">Same address space</span></span>

<span data-ttu-id="bfd81-143">Si dispone de subred de origen de Hola y subred de destino de Hola Hola mismo espacio de direcciones, dirección IP de destino se establece igual que IP Hola Hola interfaz de red de máquina virtual de origen Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-143">If hello source subnet and hello target subnet have hello same address space, then target IP is set same as hello IP of  hello network interface of hello source virtual machine.</span></span> <span data-ttu-id="bfd81-144">Si la misma dirección de IP no está disponible, algunas la dirección IP disponible se establece como dirección IP de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-144">If same IP is not available, then some other available IP is set as hello target IP.</span></span>

#### <a name="different-address-space"></a><span data-ttu-id="bfd81-145">Distinto espacio de direcciones</span><span class="sxs-lookup"><span data-stu-id="bfd81-145">Different address space</span></span>

<span data-ttu-id="bfd81-146">Si la subred de origen de Hola y subred de destino de hello tienen espacio de direcciones diferentes, dirección IP de destino se establece como cualquier dirección IP disponible en la subred de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="bfd81-146">If hello source subnet and hello target subnet have different address space, then target IP is set as any available IP in hello target subnet.</span></span>

<span data-ttu-id="bfd81-147">Puede modificar dirección IP de destino de hello en cada interfaz de red, vaya a configuración de red de máquina virtual de Hola y tooCompute.</span><span class="sxs-lookup"><span data-stu-id="bfd81-147">You can modify hello target IP on each network interface by going tooCompute and Network settings of hello virtual machine.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfd81-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bfd81-148">Next steps</span></span>

- <span data-ttu-id="bfd81-149">Más información sobre [Networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md) (Instrucciones de redes para la replicación de máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="bfd81-149">Learn about [networking guidance for replicating Azure VMs](site-recovery-azure-to-azure-networking-guidance.md).</span></span>
