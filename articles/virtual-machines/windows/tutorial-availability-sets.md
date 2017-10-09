---
title: "aaaAvailability establece el tutorial para máquinas virtuales de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de hello disponibilidad conjuntos para máquinas virtuales de Windows en Azure."
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
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="3206e-103">¿Cómo se establece toouse disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-103">How toouse availability sets</span></span>

<span data-ttu-id="3206e-104">En este tutorial, obtendrá información sobre cómo la disponibilidad de hello tooincrease y la confiabilidad de las soluciones de la máquina Virtual en Azure con una capacidad de llamar conjuntos de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3206e-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="3206e-105">Conjuntos de disponibilidad Asegúrese de que las máquinas virtuales se implementan en Azure se distribuyen entre varios clústeres de hardware aislados de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="3206e-106">Esto garantiza que, si se produce un error de hardware o software dentro de Azure, solo un subjuego de las máquinas virtuales se verán afectado y que la solución general permanecerá disponible y en funcionamiento desde la perspectiva de Hola de los clientes de usarlo.</span><span class="sxs-lookup"><span data-stu-id="3206e-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="3206e-107">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="3206e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3206e-108">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-108">Create an availability set</span></span>
> * <span data-ttu-id="3206e-109">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="3206e-110">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="3206e-110">Check available VM sizes</span></span>

<span data-ttu-id="3206e-111">Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo.</span><span class="sxs-lookup"><span data-stu-id="3206e-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="3206e-112">Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="3206e-113">Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3206e-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="3206e-114">Información general sobre conjuntos de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-114">Availability set overview</span></span>

<span data-ttu-id="3206e-115">Un conjunto de disponibilidad es una capacidad de agrupación lógica que puede usar en Azure tooensure que los recursos de máquina virtual de Hola que se coloca dentro de él están aislados entre sí cuando se implementan en un centro de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="3206e-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="3206e-116">Azure garantiza que las máquinas virtuales se coloca dentro de un conjunto de disponibilidad que se ejecute en varios servidores físicos de hello, proceso racks, unidades de almacenamiento y conmutadores de red.</span><span class="sxs-lookup"><span data-stu-id="3206e-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="3206e-117">Esto garantiza que en caso de hello de un error hardware o software de Azure, solo un subconjunto de las máquinas virtuales se verán afectado, y la aplicación global se mantienen actualizados y continuar a toobe tooyour disponibles clientes.</span><span class="sxs-lookup"><span data-stu-id="3206e-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="3206e-118">Usar conjuntos de disponibilidad es una capacidad fundamental tooleverage cuando desee que las soluciones de nube confiable toobuild.</span><span class="sxs-lookup"><span data-stu-id="3206e-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="3206e-119">Veamos una solución basada en máquina virtual típica en la podría haber 4 servidores web front-end y usar 2 máquinas virtuales de back-end que hospedan una base de datos.</span><span class="sxs-lookup"><span data-stu-id="3206e-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="3206e-120">Con Azure, desearía toodefine dos conjuntos de disponibilidad antes de implementar las máquinas virtuales: conjunto de disponibilidad de uno para la capa de "web" de Hola y un conjunto de disponibilidad de nivel de "database" Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="3206e-121">Cuando se crea una nueva máquina virtual, a continuación, puede especificar el conjunto como una máquina virtual de parámetro toohello az crear comandos y Azure automáticamente asegurará de que hello las máquinas virtuales que cree en hello disponible de la disponibilidad de hello conjunto están aislados entre varios recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="3206e-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="3206e-122">Esto significa que si el hardware físico de Hola que uno de su servidor Web o máquinas virtuales del servidor de base de datos se ejecuta en tiene un problema, sabe que Hola otras instancias de servidor Web y máquinas virtuales de la base de datos seguirá ejecutándose correctamente porque están en un hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="3206e-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="3206e-123">Debe utilizar siempre los conjuntos de disponibilidad cuando se desean toodeploy las soluciones basadas en VM confiables dentro de Azure.</span><span class="sxs-lookup"><span data-stu-id="3206e-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="3206e-124">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-124">Create an availability set</span></span>

<span data-ttu-id="3206e-125">Puede crear un conjunto de disponibilidad con [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="3206e-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="3206e-126">En este ejemplo, establecemos ambos en número de dominios de actualización y error en hello *2* para el conjunto con nombre de la disponibilidad de hello *myAvailabilitySet* en hello *myResourceGroupAvailability*grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3206e-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="3206e-127">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3206e-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="3206e-128">Creación de VM dentro de un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="3206e-129">Las máquinas virtuales deben toobe creado dentro de hello disponibilidad conjunto toomake seguro de que se distribuyen correctamente a través de hardware de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="3206e-130">No se puede agregar un grupo de disponibilidad de tooan VM establecer después de crearlo.</span><span class="sxs-lookup"><span data-stu-id="3206e-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="3206e-131">hardware de Hello en una ubicación se divide en toomultiple actualizar dominios y dominios de error.</span><span class="sxs-lookup"><span data-stu-id="3206e-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="3206e-132">Un **Actualizar dominio** es un grupo de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="3206e-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="3206e-133">Máquinas virtuales en el mismo Hola **dominio de error** comparten un almacenamiento común, así como un conmutador de origen y de red común de energía.</span><span class="sxs-lookup"><span data-stu-id="3206e-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="3206e-134">Cuando se crea una máquina virtual mediante la configuración mediante [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) especificar Hola conjunto de disponibilidad mediante hello `-AvailabilitySetId` Id. del parámetro toospecify Hola Hola del conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="3206e-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="3206e-135">Crear 2 máquinas virtuales con [AzureRmVM New](/powershell/module/azurerm.compute/new-azurermvm) en conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

   # Here is where we specify hello availability set
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

<span data-ttu-id="3206e-136">Toma toocreate unos minutos y configurar las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="3206e-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="3206e-137">Cuando termine, tendrá 2 máquinas virtuales que se distribuyen a través de hello subyacente de hardware.</span><span class="sxs-lookup"><span data-stu-id="3206e-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="3206e-138">Comprobación de los tamaños de VM disponibles</span><span class="sxs-lookup"><span data-stu-id="3206e-138">Check for available VM sizes</span></span> 

<span data-ttu-id="3206e-139">Puede agregar más máquinas virtuales toohello conjunto de disponibilidad posteriormente, pero necesita tooknow qué tamaños de máquinas virtuales están disponibles en el hardware de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="3206e-140">Use [AzureRMVMSize Get](/powershell/module/azurerm.compute/get-azurermvmsize) toolist todos los tamaños disponibles de hello en hardware de Hola de clúster para el conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="3206e-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="3206e-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3206e-141">Next steps</span></span>

<span data-ttu-id="3206e-142">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="3206e-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3206e-143">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-143">Create an availability set</span></span>
> * <span data-ttu-id="3206e-144">Crear una máquina virtual en un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="3206e-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="3206e-145">Comprobar los tamaños de máquina virtual disponibles</span><span class="sxs-lookup"><span data-stu-id="3206e-145">Check available VM sizes</span></span>

<span data-ttu-id="3206e-146">Avanzar toohello toolearn de tutorial siguiente sobre conjuntos de escalas de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3206e-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3206e-147">Creación de un conjunto de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="3206e-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


