---
title: "Creación de un conjunto de disponibilidad de VM en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear un conjunto de disponibilidad administrado o no administrado para sus máquinas virtuales mediante Azure PowerShell o el portal con el modelo de implementación de Resource Manager."
keywords: conjunto de disponibilidad
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a3db8659-ace8-4e78-8b8c-1e75c04c042c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e813ade8e105169f21138ed8a8eafda1ff39f42e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="increase-vm-availability-by-creating-an-azure-availability-set"></a><span data-ttu-id="20b22-104">Aumento de la disponibilidad de máquinas virtuales mediante la creación de un conjunto de disponibilidad de Azure</span><span class="sxs-lookup"><span data-stu-id="20b22-104">Increase VM availability by creating an Azure availability set</span></span> 
<span data-ttu-id="20b22-105">Los conjuntos de disponibilidad proporcionan redundancia en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="20b22-105">Availability sets provide redundancy to your application.</span></span> <span data-ttu-id="20b22-106">Se recomienda agrupar dos máquinas virtuales o más en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20b22-106">We recommend that you group two or more virtual machines in an availability set.</span></span> <span data-ttu-id="20b22-107">Esta configuración garantiza que durante un evento de mantenimiento planeado o no planeado, al menos una máquina virtual estará disponible y cumplirá el 99,95% de los niveles de servicio contratados de Azure.</span><span class="sxs-lookup"><span data-stu-id="20b22-107">This configuration ensures that during either a planned or unplanned maintenance event, at least one virtual machine will be available and meet the 99.95% Azure SLA.</span></span> <span data-ttu-id="20b22-108">Para obtener más información, consulte [Acuerdo de Nivel de Servicio para máquinas virtuales](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="20b22-108">For more information, see the [SLA for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20b22-109">Las VM deben crearse en el mismo grupo de recursos que el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20b22-109">VMs must be created in the same resource group as the availability set.</span></span>
> 

<span data-ttu-id="20b22-110">Si quiere que la VM pase a formar parte de un conjunto de disponibilidad, debe crear el conjunto de disponibilidad primero o mientras crea la primera VM en el conjunto.</span><span class="sxs-lookup"><span data-stu-id="20b22-110">If you want your VM to be part of an availability set, you need to create the availability set first or while you are creating your first VM in the set.</span></span> <span data-ttu-id="20b22-111">Si la VM va a utilizar Managed Disks, el conjunto de disponibilidad debe crearse como un conjunto de disponibilidad administrado.</span><span class="sxs-lookup"><span data-stu-id="20b22-111">If your VM will be using Managed Disks, the availability set must be created as a managed availability set.</span></span>

<span data-ttu-id="20b22-112">Para más información sobre la creación y el uso de conjuntos de disponibilidad, consulte [Administración de la disponibilidad de las máquinas virtuales](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="20b22-112">For more information about creating and using availability sets, see [Manage the availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="use-the-portal-to-create-an-availability-set-before-creating-your-vms"></a><span data-ttu-id="20b22-113">Uso del portal para crear un conjunto de disponibilidad antes de crear las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="20b22-113">Use the portal to create an availability set before creating your VMs</span></span>
1. <span data-ttu-id="20b22-114">En el menú del concentrador, haga clic en **Examinar** y seleccione **Conjuntos de disponibilidad**.</span><span class="sxs-lookup"><span data-stu-id="20b22-114">In the hub menu, click **Browse** and select **Availability sets**.</span></span>
2. <span data-ttu-id="20b22-115">En la hoja **Conjuntos de disponibilidad**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="20b22-115">On the **Availability sets blade**, click **Add**.</span></span>
   
    ![Captura de pantalla que muestra el botón Agregar para crear un nuevo conjunto de disponibilidad.](./media/create-availability-set/add-availability-set.png)
3. <span data-ttu-id="20b22-117">En la hoja **Crear conjunto de disponibilidad** , rellene la información del conjunto.</span><span class="sxs-lookup"><span data-stu-id="20b22-117">On the **Create availability set** blade, complete the information for your set.</span></span>
   
    ![Captura de pantalla que muestra la información que debe especificar para crear el conjunto de disponibilidad.](./media/create-availability-set/create-availability-set.png)
   
   * <span data-ttu-id="20b22-119">**Nombre** : el nombre debe tener entre 1 y 80 caracteres y estar formado por números, letras, puntos, guiones y caracteres de subrayado.</span><span class="sxs-lookup"><span data-stu-id="20b22-119">**Name** - the name should be 1-80 characters made up of numbers, letters, periods, underscores and dashes.</span></span> <span data-ttu-id="20b22-120">El primer carácter deben ser una letra o un número.</span><span class="sxs-lookup"><span data-stu-id="20b22-120">The first character must be a letter or number.</span></span> <span data-ttu-id="20b22-121">El último carácter debe ser una letra, un número o un carácter de subrayado.</span><span class="sxs-lookup"><span data-stu-id="20b22-121">The last character must be a letter, number or underscore.</span></span>
   * <span data-ttu-id="20b22-122">**Dominios de error** : los dominios de error definen un grupo de máquinas virtuales que comparten un origen de alimentación y un interruptor de red comunes.</span><span class="sxs-lookup"><span data-stu-id="20b22-122">**Fault domains** - fault domains define the group of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="20b22-123">De forma predeterminada, las máquinas virtuales están separadas entre tres dominios de error como máximo y pueden cambiarse a 1, 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="20b22-123">By default, the VMs  are separated across up to three fault domains and can be changed to between 1 and 3.</span></span>
   * <span data-ttu-id="20b22-124">**Dominios de actualización**: de forma predeterminada se asignan cinco dominios de actualización y este valor se puede establecer en un número entre 1 y 20.</span><span class="sxs-lookup"><span data-stu-id="20b22-124">**Update domains** -  five update domains are assigned by default and this can be set to between 1 and 20.</span></span> <span data-ttu-id="20b22-125">Los dominios de actualización indican grupos de máquinas virtuales y hardware físico subyacente que se pueden reiniciar al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="20b22-125">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="20b22-126">Por ejemplo, si especificamos cinco dominios de actualización, cuando se configuran más de cinco máquinas virtuales dentro de un único conjunto de disponibilidad, la sexta máquina virtual se colocará en el mismo dominio de actualización que la primera, la séptima en el mismo que la segunda y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="20b22-126">For example, if we specify five update domains, when more than five virtual machines are configured within a single Availability Set, the sixth virtual machine will be placed into the same update domain as the first virtual machine, the seventh in the same UD as the second virtual machine, and so on.</span></span> <span data-ttu-id="20b22-127">El orden de los reinicios puede no ser secuencial, pero solo un dominio de actualización se reiniciará de manera simultánea.</span><span class="sxs-lookup"><span data-stu-id="20b22-127">The order of the reboots may not be sequential, but only one update domain will be rebooted at a time.</span></span>
   * <span data-ttu-id="20b22-128">**Suscripción** : si tiene varias suscripciones, seleccione la que quiera usar.</span><span class="sxs-lookup"><span data-stu-id="20b22-128">**Subscription** - select the subscription to use if you have more than one.</span></span>
   * <span data-ttu-id="20b22-129">**Grupo de recursos** : seleccione un grupo de recursos existente; para ello, haga clic en la flecha y seleccione un grupo de recursos de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20b22-129">**Resource group** - select an existing resource group by clicking the arrow and selecting a resource group from the drop down.</span></span> <span data-ttu-id="20b22-130">Otra manera de crear un nuevo grupo de recursos es escribir un nombre.</span><span class="sxs-lookup"><span data-stu-id="20b22-130">You can also create a new resource group by typing in a name.</span></span> <span data-ttu-id="20b22-131">El nombre puede contener cualquiera de los siguientes caracteres: letras, números, puntos, guiones, caracteres de subrayado y paréntesis de apertura o cierre.</span><span class="sxs-lookup"><span data-stu-id="20b22-131">The name can contain any of the following characters: letters, numbers, periods, dashes, underscores and opening or closing parenthesis.</span></span> <span data-ttu-id="20b22-132">El nombre no puede terminar con un punto.</span><span class="sxs-lookup"><span data-stu-id="20b22-132">The name cannot end in a period.</span></span> <span data-ttu-id="20b22-133">Todas las máquinas virtuales del grupo de disponibilidad deben crearse en el mismo grupo de recursos que el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="20b22-133">All of the VMs in the availability group need to be created in the same resource group as the availability set.</span></span>
   * <span data-ttu-id="20b22-134">**Ubicación** : seleccione una ubicación de la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="20b22-134">**Location** - select a location from the drop-down.</span></span>
   * <span data-ttu-id="20b22-135">**Administrado**: seleccione *Sí* para crear un conjunto de disponibilidad administrado para usarlo con las VM que usan Managed Disks para el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="20b22-135">**Managed** - select *Yes* to create a managed availability set to use with VMs that use Managed Disks for storage.</span></span> <span data-ttu-id="20b22-136">Seleccione **No** si las VM que formarán parte del conjunto usan discos no administrados en una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="20b22-136">Select **No** if the VMs that will be in the set use unmanaged disks in a storage account.</span></span>
   
4. <span data-ttu-id="20b22-137">Cuando haya terminado de especificar la información, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="20b22-137">When you are done entering the information, click **Create**.</span></span> 

## <a name="use-the-portal-to-create-a-virtual-machine-and-an-availability-set-at-the-same-time"></a><span data-ttu-id="20b22-138">Uso del portal para crear una máquina virtual y un conjunto de disponibilidad al mismo tiempo</span><span class="sxs-lookup"><span data-stu-id="20b22-138">Use the portal to create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="20b22-139">Si va a crear una nueva máquina virtual mediante el portal, también puede crear un nuevo conjunto de disponibilidad para la máquina virtual mientras crea la primera máquina virtual del conjunto.</span><span class="sxs-lookup"><span data-stu-id="20b22-139">If you are creating a new VM using the portal, you can also create a new availability set for the VM while you create the first VM in the set.</span></span> <span data-ttu-id="20b22-140">Si decide usar Managed Disks para la VM, se creará un conjunto de disponibilidad administrado.</span><span class="sxs-lookup"><span data-stu-id="20b22-140">If you choose to use Managed Disks for your VM, a managed availability set will be created.</span></span>

![Captura de pantalla que muestra el proceso para crear un nuevo conjunto de disponibilidad mientras crea la máquina virtual.](./media/create-availability-set/new-vm-avail-set.png)

## <a name="add-a-new-vm-to-an-existing-availability-set-in-the-portal"></a><span data-ttu-id="20b22-142">Incorporación de una nueva VM a un conjunto de disponibilidad existente en el portal</span><span class="sxs-lookup"><span data-stu-id="20b22-142">Add a new VM to an existing availability set in the portal</span></span>
<span data-ttu-id="20b22-143">Para cada máquina virtual adicional que cree que debe pertenecer al conjunto, asegúrese de que la crea en el mismo **grupo de recursos** y luego seleccione el conjunto de disponibilidad existente en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="20b22-143">For each additional VM that you create that should belong in the set, make sure that you create it in the same **resource group** and then select the existing availability set in Step 3.</span></span> 

![Captura de pantalla que muestra cómo seleccionar un conjunto de disponibilidad existente para la máquina virtual.](./media/create-availability-set/add-vm-to-set.png)

## <a name="use-powershell-to-create-an-availability-set"></a><span data-ttu-id="20b22-145">Uso de PowerShell para crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="20b22-145">Use PowerShell to create an availability set</span></span>
<span data-ttu-id="20b22-146">En este ejemplo se crea un conjunto de disponibilidad denominado **myAvailabilitySet** en el grupo de recursos **myResourceGroup** en la ubicación **Oeste de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="20b22-146">This example creates an availability set named **myAvailabilitySet** in the **myResourceGroup** resource group in the **West US** location.</span></span> <span data-ttu-id="20b22-147">Esto se debe hacer antes de crear la primera máquina virtual que estará en el conjunto.</span><span class="sxs-lookup"><span data-stu-id="20b22-147">This needs to be done before you create the first VM that will be in the set.</span></span>

<span data-ttu-id="20b22-148">Antes de comenzar, asegúrese de que tiene la última versión del módulo AzureRM.Compute de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20b22-148">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="20b22-149">Ejecute el siguiente comando para realizar la instalación.</span><span class="sxs-lookup"><span data-stu-id="20b22-149">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="20b22-150">Para más información, consulte [Azure PowerShell Versioning](/powershell/azure/overview) (Control de versiones de Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="20b22-150">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


<span data-ttu-id="20b22-151">Si usa discos administrados para las VM, escriba:</span><span class="sxs-lookup"><span data-stu-id="20b22-151">If you are using managed disks for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" -managed
```

<span data-ttu-id="20b22-152">Si usa sus propias cuentas de almacenamiento para las VM, escriba:</span><span class="sxs-lookup"><span data-stu-id="20b22-152">If you are using your own storage accounts for your VMs, type:</span></span>

```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "myResourceGroup" '
    -Name "myAvailabilitySet" -Location "West US" 
```

<span data-ttu-id="20b22-153">Para más información, consulte [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="20b22-153">For more information, see [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="20b22-154">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="20b22-154">Troubleshooting</span></span>
* <span data-ttu-id="20b22-155">Al crear una máquina virtual, si el conjunto de disponibilidad que quiere no está en la lista desplegable en el portal, puede que lo haya creado en otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20b22-155">When you create a VM, if the availability set you want isn't in the drop-down list in the portal you may have created it in a different resource group.</span></span> <span data-ttu-id="20b22-156">Si no conoce el grupo de recursos de su conjunto de disponibilidad, vaya al menú del concentrador y haga clic en Examinar > Conjuntos de disponibilidad para ver una lista de los conjuntos de disponibilidad y los grupos de recursos a los que pertenecen.</span><span class="sxs-lookup"><span data-stu-id="20b22-156">If you don't know the resource group for your availability set, go to the hub menu and click Browse > Availability sets to see a list of your availability sets and which resource groups they belong to.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20b22-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="20b22-157">Next steps</span></span>
<span data-ttu-id="20b22-158">Agregue almacenamiento adicional a la máquina virtual mediante la adición de un [disco de datos](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)adicional.</span><span class="sxs-lookup"><span data-stu-id="20b22-158">Add additional storage to your VM by adding an additional [data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

