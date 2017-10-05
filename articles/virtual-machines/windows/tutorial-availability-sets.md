---
title: "Tutorial de conjuntos de disponibilidad para máquinas virtuales de Windows en Azure | Microsoft Docs"
description: "Obtenga información sobre los conjuntos de disponibilidad para máquinas virtuales de Windows en Azure."
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="690f4-103">Cómo usar conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-103">How to use availability sets</span></span>

<span data-ttu-id="690f4-104">En este tutorial, obtendrá información sobre cómo aumentar la disponibilidad y confiabilidad de las soluciones de máquina virtual en Azure mediante una funcionalidad denominada "conjuntos de disponibilidad".</span><span class="sxs-lookup"><span data-stu-id="690f4-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="690f4-105">Los conjuntos de disponibilidad garantizan que las máquinas virtuales implementadas en Azure se distribuyan entre varios clústeres de hardware aislados.</span><span class="sxs-lookup"><span data-stu-id="690f4-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="690f4-106">De este modo, se asegura de que, si se produce un error de hardware o software en Azure, solo un subconjunto de las máquinas virtuales se verá afectado, y que la solución estará disponible y en funcionamiento para los clientes.</span><span class="sxs-lookup"><span data-stu-id="690f4-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="690f4-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="690f4-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="690f4-108">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-108">Create an availability set</span></span>
> * <span data-ttu-id="690f4-109">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="690f4-110">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="690f4-110">Check available VM sizes</span></span>

<span data-ttu-id="690f4-111">Para realizar este tutorial es necesaria la versión 3.6 del módulo de Azure PowerShell, o cualquier versión posterior.</span><span class="sxs-lookup"><span data-stu-id="690f4-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="690f4-112">Ejecute ` Get-Module -ListAvailable AzureRM` para encontrar la versión.</span><span class="sxs-lookup"><span data-stu-id="690f4-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="690f4-113">Si necesita actualizarla, consulte [Instalación del módulo de Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="690f4-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="690f4-114">Información general sobre conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-114">Availability set overview</span></span>

<span data-ttu-id="690f4-115">Un conjunto de disponibilidad es una funcionalidad de agrupación lógica que puede usar en Azure para asegurarse de que los recursos de máquina virtual que coloque en dicho conjunto de disponibilidad estén aislados entre sí cuando se implementen en un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="690f4-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="690f4-116">Azure garantiza que las máquinas virtuales colocados en un conjunto de disponibilidad se ejecuten en varios servidores físicos, grupos de proceso, unidades de almacenamiento y conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="690f4-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="690f4-117">De este modo, se garantiza que si se produce un error de hardware o software de Azure, solo un subconjunto de las máquinas virtuales se verá afectado, y que la aplicación se mantendrá actualizada y seguirá estando disponible para los clientes.</span><span class="sxs-lookup"><span data-stu-id="690f4-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="690f4-118">Usar conjuntos de disponibilidad es una funcionalidad fundamental que debe tener en cuenta para crear soluciones en la nube confiables.</span><span class="sxs-lookup"><span data-stu-id="690f4-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="690f4-119">Veamos una solución basada en máquina virtual típica en la podría haber 4 servidores web front-end y usar 2 máquinas virtuales de back-end que hospedan una base de datos.</span><span class="sxs-lookup"><span data-stu-id="690f4-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="690f4-120">Con Azure, desea definir 2 conjuntos de disponibilidad antes de implementar las máquinas virtuales: un conjunto de disponibilidad para el nivel de "web" y otro para el nivel de "base de datos".</span><span class="sxs-lookup"><span data-stu-id="690f4-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="690f4-121">Al crear una máquina virtual, podrá especificar el conjunto de disponibilidad como un parámetro en el comando az vm create, y Azure garantizará automáticamente que las máquinas virtuales que cree en el conjunto de disponibilidad estén aisladas en varios recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="690f4-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="690f4-122">Esto significa que si el hardware físico que está ejecutando una de sus máquinas virtuales del servidor web o del servidor de base de datos tiene un problema, sabrá que las demás instancias de las máquinas virtuales del servidor de base de datos y del servidor web seguirán ejecutándose correctamente porque están en un hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="690f4-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="690f4-123">Siempre debe utilizar los conjuntos de disponibilidad cuando quiera implementar soluciones basadas en máquinas virtuales confiables en Azure.</span><span class="sxs-lookup"><span data-stu-id="690f4-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="690f4-124">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-124">Create an availability set</span></span>

<span data-ttu-id="690f4-125">Puede crear un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="690f4-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="690f4-126">En este ejemplo, se establece el número de dominios de actualización y error en *2* para el conjunto de disponibilidad denominado *myAvailabilitySet* en el grupo de recursos *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="690f4-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="690f4-127">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="690f4-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="690f4-128">Creación de VM dentro de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="690f4-129">Las máquinas virtuales deben crearse en el conjunto de disponibilidad para asegurarse de que se distribuyan correctamente en el hardware.</span><span class="sxs-lookup"><span data-stu-id="690f4-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="690f4-130">No se puede agregar una máquina virtual existente a un conjunto de disponibilidad después de crearla.</span><span class="sxs-lookup"><span data-stu-id="690f4-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="690f4-131">El hardware de una ubicación está dividido en varios dominios de actualización y de error.</span><span class="sxs-lookup"><span data-stu-id="690f4-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="690f4-132">Un **dominio de actualización** es un grupo de máquinas virtuales y hardware físico subyacente que se pueden reiniciar al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="690f4-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="690f4-133">Las máquinas virtuales en el mismo **dominio de error** comparten un almacenamiento común, así como una fuente de alimentación y un conmutador de red comunes.</span><span class="sxs-lookup"><span data-stu-id="690f4-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="690f4-134">Cuando se crea una VM mediante [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), se especifica el conjunto de disponibilidad mediante el parámetro `-AvailabilitySetId` para especificar el identificador del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="690f4-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="690f4-135">Cree 2 VM con [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) en el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="690f4-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify the availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="690f4-136">Se tarda unos minutos en crear y configurar ambas VM.</span><span class="sxs-lookup"><span data-stu-id="690f4-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="690f4-137">Cuando se acabe, tendrá 2 máquinas virtuales distribuidas en el hardware subyacente.</span><span class="sxs-lookup"><span data-stu-id="690f4-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="690f4-138">Comprobación de los tamaños de VM disponibles</span><span class="sxs-lookup"><span data-stu-id="690f4-138">Check for available VM sizes</span></span> 

<span data-ttu-id="690f4-139">Se pueden agregar más máquinas virtuales al conjunto de disponibilidad posteriormente, pero debe saber qué tamaños de máquina virtual están disponibles en el hardware.</span><span class="sxs-lookup"><span data-stu-id="690f4-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="690f4-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) para enumerar todos los tamaños disponibles en el clúster de hardware para el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="690f4-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="690f4-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="690f4-141">Next steps</span></span>

<span data-ttu-id="690f4-142">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="690f4-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="690f4-143">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-143">Create an availability set</span></span>
> * <span data-ttu-id="690f4-144">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="690f4-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="690f4-145">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="690f4-145">Check available VM sizes</span></span>

<span data-ttu-id="690f4-146">Avance al siguiente tutorial para informarse sobre los conjuntos de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="690f4-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="690f4-147">Creación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="690f4-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


