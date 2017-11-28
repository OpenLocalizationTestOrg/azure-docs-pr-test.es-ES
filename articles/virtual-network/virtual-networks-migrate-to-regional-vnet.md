---
title: "Migración de una red virtual de Azure (clásica) de un grupo de afinidad a una región | Microsoft Docs"
description: "Obtenga información sobre cómo migrar una red virtual (clásica) de un grupo de afinidad a una región."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 84febcb9-bb8b-4e79-ab91-865ad9de41cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: b9b3bd0f2184ac85261166d5fe2ab67e1bf319d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-a-virtual-network-classic-from-an-affinity-group-to-a-region"></a><span data-ttu-id="7b981-103">Migración de una red virtual (clásica) de un grupo de afinidad a una región</span><span class="sxs-lookup"><span data-stu-id="7b981-103">Migrate a virtual network (classic) from an affinity group to a region</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b981-104">Azure tiene dos modelos de implementación diferentes para crear y trabajar con recursos: [el Administrador de recursos y el clásico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7b981-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="7b981-105">Este artículo trata del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="7b981-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="7b981-106">Microsoft recomienda que las implementaciones más recientes usen el modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7b981-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="7b981-107">Los grupos de afinidad garantizan que los recursos creados en el mismo grupo de afinidad se hospedan físicamente en servidores que están cerca, lo que permite que estos recursos se comuniquen con mayor rapidez.</span><span class="sxs-lookup"><span data-stu-id="7b981-107">Affinity groups ensure that resources created within the same affinity group are physically hosted by servers that are close together, enabling these resources to communicate quicker.</span></span> <span data-ttu-id="7b981-108">En el pasado, los grupos de afinidad eran un requisito para crear redes virtuales (clásicas).</span><span class="sxs-lookup"><span data-stu-id="7b981-108">In the past, affinity groups were a requirement for creating virtual networks (classic).</span></span> <span data-ttu-id="7b981-109">En ese momento, el servicio de administrador de red que administraba las redes virtuales (clásicas) solo podía trabajar en un conjunto de servidores físicos o una unidad de escalado.</span><span class="sxs-lookup"><span data-stu-id="7b981-109">At that time, the network manager service that managed virtual networks (classic) could only work within a set of physical servers or scale unit.</span></span> <span data-ttu-id="7b981-110">Mejoras arquitectónicas han aumentado el ámbito de administración de red a una región.</span><span class="sxs-lookup"><span data-stu-id="7b981-110">Architectural improvements have increased the scope of network management to a region.</span></span>

<span data-ttu-id="7b981-111">Como resultado de estas mejoras de arquitectura, los grupos de afinidad ya no se recomiendan ni son necesarios para las redes virtuales (clásicas).</span><span class="sxs-lookup"><span data-stu-id="7b981-111">As a result of these architectural improvements, affinity groups are no longer recommended, or required for virtual networks (classic).</span></span> <span data-ttu-id="7b981-112">El uso de grupos de afinidad para redes virtuales (clásicas) se reemplaza por regiones.</span><span class="sxs-lookup"><span data-stu-id="7b981-112">The use of affinity groups for virtual networks (classic) is replaced by regions.</span></span> <span data-ttu-id="7b981-113">Las redes virtuales (clásicas) que están asociadas a regiones se denominan redes virtuales regionales.</span><span class="sxs-lookup"><span data-stu-id="7b981-113">Virtual networks (classic) that are associated with regions are called regional virtual networks.</span></span>

<span data-ttu-id="7b981-114">Por lo general, se recomienda no usar grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="7b981-114">We recommend that you don't use affinity groups in general.</span></span> <span data-ttu-id="7b981-115">Además del requisito de redes virtuales, también era importante usar los grupos de afinidad para asegurarse de que los recursos, por ejemplo, de proceso (clásico) y almacenamiento (clásico), se colocaran próximos entre sí.</span><span class="sxs-lookup"><span data-stu-id="7b981-115">Aside from the virtual network requirement, affinity groups were also important to use to ensure resources, such as compute (classic) and storage (classic), were placed near each other.</span></span> <span data-ttu-id="7b981-116">Sin embargo, con la arquitectura de red de Azure actual, estos requisitos de colocación ya no son necesarios.</span><span class="sxs-lookup"><span data-stu-id="7b981-116">However, with the current Azure network architecture, these placement requirements are no longer necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b981-117">Aunque es técnicamente posible crear una red virtual que está asociada a un grupo de afinidad, no hay ninguna razón para hacerlo.</span><span class="sxs-lookup"><span data-stu-id="7b981-117">Although it is still technically possible to create a virtual network that is associated with an affinity group, there is no compelling reason to do so.</span></span> <span data-ttu-id="7b981-118">Muchas características de red virtual, como los grupos de seguridad de red, solo están disponibles cuando se usa una red virtual regional y no están disponibles para las redes virtuales que están asociadas a grupos de afinidad.</span><span class="sxs-lookup"><span data-stu-id="7b981-118">Many virtual network features, such as network security groups, are only available when using a regional virtual network, and are not available for virtual networks that are associated with affinity groups.</span></span>
> 
> 

## <a name="edit-the-network-configuration-file"></a><span data-ttu-id="7b981-119">Edición del archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="7b981-119">Edit the network configuration file</span></span>

1. <span data-ttu-id="7b981-120">Exporte un archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="7b981-120">Export the network configuration file.</span></span> <span data-ttu-id="7b981-121">Para más información sobre cómo exportar un archivo de configuración de red con PowerShell o la interfaz de línea de comandos (CLI) 1.0 de Azure, consulte [Configuración de una red virtual mediante un archivo de configuración de red](virtual-networks-using-network-configuration-file.md#export).</span><span class="sxs-lookup"><span data-stu-id="7b981-121">To learn how to export a network configuration file using PowerShell or the Azure command-line interface (CLI) 1.0, see [Configure a virtual network using a network configuration file](virtual-networks-using-network-configuration-file.md#export).</span></span>
2. <span data-ttu-id="7b981-122">Edite el archivo de configuración de red, y reemplace **AffinityGroup** por **Location**.</span><span class="sxs-lookup"><span data-stu-id="7b981-122">Edit the network configuration file, replacing **AffinityGroup** with **Location**.</span></span> <span data-ttu-id="7b981-123">Especifique una [región](https://azure.microsoft.com/regions) de Azure para **Location**.</span><span class="sxs-lookup"><span data-stu-id="7b981-123">You specify an Azure [region](https://azure.microsoft.com/regions) for **Location**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7b981-124">**Location** es la región que especificó para el grupo de afinidad que está asociado a la red virtual (clásica).</span><span class="sxs-lookup"><span data-stu-id="7b981-124">The **Location** is the region that you specified for the affinity group that is associated with your virtual network (classic).</span></span> <span data-ttu-id="7b981-125">Por ejemplo, si la red virtual (clásica) está asociada a un grupo de afinidad que se encuentra en Oeste de EE. UU., al migrar, el valor de **Location** debe apuntar a Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="7b981-125">For example, if your virtual network (classic) is associated with an affinity group that is located in West US, when you migrate, your **Location** must point to West US.</span></span> 
   > 
   > 
   
    <span data-ttu-id="7b981-126">Edite las líneas siguientes del archivo de configuración de red y reemplace los valores por los suyos propios:</span><span class="sxs-lookup"><span data-stu-id="7b981-126">Edit the following lines in your network configuration file, replacing the values with your own:</span></span> 
   
    <span data-ttu-id="7b981-127">**Valor antiguo:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span><span class="sxs-lookup"><span data-stu-id="7b981-127">**Old value:** \<VirtualNetworkSitename="VNetUSWest" AffinityGroup="VNetDemoAG"\></span></span> 
   
    <span data-ttu-id="7b981-128">**Valor nuevo:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span><span class="sxs-lookup"><span data-stu-id="7b981-128">**New value:** \<VirtualNetworkSitename="VNetUSWest" Location="West US"\></span></span>
3. <span data-ttu-id="7b981-129">Guarde los cambios e [importe](virtual-networks-using-network-configuration-file.md#import) la configuración de red en Azure.</span><span class="sxs-lookup"><span data-stu-id="7b981-129">Save your changes and [import](virtual-networks-using-network-configuration-file.md#import) the network configuration to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7b981-130">Esta migración NO causa ningún tiempo de inactividad en sus servicios.</span><span class="sxs-lookup"><span data-stu-id="7b981-130">This migration does NOT cause any downtime to your services.</span></span>
> 
> 

## <a name="what-to-do-if-you-have-a-vm-classic-in-an-affinity-group"></a><span data-ttu-id="7b981-131">Qué hacer si tiene una máquina virtual (clásica= en un grupo de afinidad</span><span class="sxs-lookup"><span data-stu-id="7b981-131">What to do if you have a VM (classic) in an affinity group</span></span>
<span data-ttu-id="7b981-132">No es necesario quitar las máquinas virtuales (clásicas) que están en un grupo de afinidad de dicho grupo.</span><span class="sxs-lookup"><span data-stu-id="7b981-132">VMs (classic) that are currently in an affinity group do not need to be removed from the affinity group.</span></span> <span data-ttu-id="7b981-133">Una vez implementada una máquina virtual, se implementa en una sola unidad de escalado.</span><span class="sxs-lookup"><span data-stu-id="7b981-133">Once a VM is deployed, it is deployed to a single scale unit.</span></span> <span data-ttu-id="7b981-134">Los grupos de afinidad pueden restringir el conjunto de tamaños de máquina virtual disponibles para una nueva implementación de máquina virtual, pero cualquier máquina virtual existente que esté implementa ya está restringida al conjunto de tamaños de máquina virtual disponible en la unidad de escalado en el que se implementa la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7b981-134">Affinity groups can restrict the set of available VM sizes for a new VM deployment, but any existing VM that is deployed is already restricted to the set of VM sizes available in the scale unit in which the VM is deployed.</span></span> <span data-ttu-id="7b981-135">Dado que la máquina virtual se ha implementado en una unidad de escalado, quitar una máquina virtual de un grupo de afinidad no tiene ningún efecto en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7b981-135">Because the VM is already deployed to a scale unit, removing a VM from an affinity group has no effect on the VM.</span></span>
