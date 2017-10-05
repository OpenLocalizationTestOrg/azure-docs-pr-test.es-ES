---
title: "Creación de un emparejamiento de redes virtuales de Azure: Resource Manager, misma suscripción | Microsoft Docs"
description: Aprenda a crear un emparejamiento de redes virtuales entre redes virtuales creadas mediante Resource Manager que existen en diferentes suscripciones de Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="4e2dd-103">Creación de un emparejamiento de redes virtuales: Resource Manager, misma suscripción</span><span class="sxs-lookup"><span data-stu-id="4e2dd-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="4e2dd-104">En este tutorial aprenderá a crear un emparejamiento de redes virtuales entre dos redes virtuales creadas mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="4e2dd-105">Hay redes virtuales en la misma suscripción en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="4e2dd-106">Emparejar dos redes virtuales permite que los recursos en distintas redes virtuales se comuniquen entre sí con el mismo ancho de banda y latencia que tendrían los recursos si estuvieran en la misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="4e2dd-107">Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="4e2dd-108">Los pasos para crear un emparejamiento de redes virtuales cambian en función de si las redes virtuales se encuentran en la misma suscripción o en suscripciones diferentes, y en función del [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) con el que se han creado las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="4e2dd-109">Para más información sobre cómo crear un emparejamiento de redes virtuales en otros escenarios, haga clic en el escenario en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="4e2dd-110">Modelo de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="4e2dd-110">Azure deployment model</span></span>  | <span data-ttu-id="4e2dd-111">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="4e2dd-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="4e2dd-112">Ambas mediante Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e2dd-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="4e2dd-113">Diferentes</span><span class="sxs-lookup"><span data-stu-id="4e2dd-113">Different</span></span>|
|[<span data-ttu-id="4e2dd-114">Una mediante Resource Manager y la otra, clásico</span><span class="sxs-lookup"><span data-stu-id="4e2dd-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="4e2dd-115">Iguales</span><span class="sxs-lookup"><span data-stu-id="4e2dd-115">Same</span></span>|
|[<span data-ttu-id="4e2dd-116">Una mediante Resource Manager y la otra, clásico</span><span class="sxs-lookup"><span data-stu-id="4e2dd-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="4e2dd-117">Diferentes</span><span class="sxs-lookup"><span data-stu-id="4e2dd-117">Different</span></span>|

<span data-ttu-id="4e2dd-118">No se puede crear un emparejamiento de redes virtuales entre dos redes virtuales implementadas mediante el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="4e2dd-119">Un emparejamiento de redes virtuales solo se puede crear entre dos redes virtuales que existen en la misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="4e2dd-120">Si necesita conectar redes virtuales que se crearon a través del modelo de implementación clásico, o que existan en diferentes regiones de Azure, puede usar una instancia de [Azure VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para conectar las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="4e2dd-121">Puede usar [Azure Portal](#portal), Azure [PowerShell](#cli), la [interfaz de la línea de comandos](#powershell) (CLI) de Azure o la [plantilla de Azure Resource Manager](#template) para crear un emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) to create a virtual network peering.</span></span> <span data-ttu-id="4e2dd-122">Haga clic en cualquiera de los vínculos anteriores de herramientas para ir directamente a los pasos para crear un emparejamiento de redes virtuales con la herramienta de su preferencia.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="4e2dd-123"><a name="portal"></a>Creación de emparejamiento: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4e2dd-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="4e2dd-124">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e2dd-125">La cuenta con la que inicie sesión debe tener todos los permisos necesarios para crear un emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="4e2dd-126">Para detalles, consulte la sección [Permisos](#permissions) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="4e2dd-127">Haga clic en **+ Nuevo**, **Redes** y, luego, en **Red virtual**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="4e2dd-128">En la hoja **Crear red virtual**, escriba o seleccione valores para la configuración siguiente y, luego, haga clic en **Crear**:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="4e2dd-129">**Nombre**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="4e2dd-130">**Espacio de direcciones**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="4e2dd-131">**Nombre de subred**: *default*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4e2dd-132">**Intervalo de direcciones de subred**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="4e2dd-133">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="4e2dd-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4e2dd-134">**Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="4e2dd-135">**Ubicación**: *este de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="4e2dd-136">Complete los pasos 2 y 3 nuevamente y especifique los valores siguientes en el paso 3:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-136">Complete steps 2-3 again specifying the following values in step 3:</span></span>
    - <span data-ttu-id="4e2dd-137">**Nombre**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="4e2dd-138">**Espacio de direcciones**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="4e2dd-139">**Nombre de subred**: *default*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4e2dd-140">**Intervalo de direcciones de subred**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="4e2dd-141">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="4e2dd-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4e2dd-142">**Grupo de recursos**: seleccione **Usar existente** y seleccione *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="4e2dd-143">**Ubicación**: *este de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="4e2dd-144">En el cuadro **Buscar recursos** en la parte superior del portal, escriba *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-144">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="4e2dd-145">Haga clic en **myResourceGroup** cuando aparezca en los resultados de la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-145">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="4e2dd-146">Aparece una hoja para el grupo de recursos **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-146">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="4e2dd-147">El grupo de recursos contiene las dos redes virtuales que se crearon en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-147">The resource group contains the two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="4e2dd-148">Haga clic en **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="4e2dd-149">En la hoja **myVnet1** que aparece, haga clic en **Emparejamientos** en la lista vertical de opciones que aparece al lado izquierdo de la hoja.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-149">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
8. <span data-ttu-id="4e2dd-150">En la hoja **myVnet1 - Peerings** (myVnet1: emparejamientos) que aparece, haga clic en **+ Agregar**</span><span class="sxs-lookup"><span data-stu-id="4e2dd-150">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="4e2dd-151">En la hoja **Agregar emparejamiento** que aparece, escriba o seleccione las opciones siguientes y, luego, haga clic en **Aceptar**:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-151">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="4e2dd-152">**Nombre**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="4e2dd-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="4e2dd-153">**Modelo de implementación de red virtual**: seleccione **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="4e2dd-154">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="4e2dd-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="4e2dd-155">**Red virtual**: haga clic en **Elegir una red virtual** y, luego, en **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="4e2dd-156">**Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="4e2dd-157">En este tutorial no se usa ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="4e2dd-158">Para conocer todas las configuraciones de emparejamiento, lea [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering) (Administración de emparejamientos de redes virtuales).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-158">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="4e2dd-159">Una vez que hace clic en **Aceptar** en el paso anterior, se cierra la hoja **Agregar emparejamiento** y se vuelve a mostrar la hoja **myVnet1 - Peerings** (myVnet1: emparejamientos).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-159">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="4e2dd-160">Unos segundos después, el emparejamiento que creó aparece en la hoja.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-160">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="4e2dd-161">El estado **Iniciado** aparece en la columna **ESTADO DE EMPAREJAMIENTO** correspondiente al emparejamiento **myVnet1ToMyVnet2** que creó.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-161">**Initiated** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="4e2dd-162">Emparejó Vnet1 con Vnet2, pero ahora debe emparejar myVnet2 con myVnet1.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-162">You've peered Vnet1 to Vnet2, but now you must peer myVnet2 to myVnet1.</span></span> <span data-ttu-id="4e2dd-163">Debe crear el emparejamiento en ambas direcciones para permitir que los recursos de las redes virtuales se comuniquen entre sí.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-163">The peering must be created in both directions to enable resources in the virtual networks to communicate with each other.</span></span>
11. <span data-ttu-id="4e2dd-164">Complete nuevamente los pasos del 5 al 10 para myVnet2.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="4e2dd-165">Asigne el nombre *myVnet2ToMyVnet1* al emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-165">Name the peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="4e2dd-166">Unos segundos después de hacer clic en **Aceptar** para crear el emparejamiento de MyVnet2, el emparejamiento **myVnet2ToMyVnet1** que acaba de crear aparece con el estado **Conectado** en la columna **ESTADO DE EMPAREJAMIENTO**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-166">A few seconds after clicking **OK** to create the peering for MyVnet2, the **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in the **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="4e2dd-167">Complete nuevamente los pasos del 5 al 7 para MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="4e2dd-168">**ESTADO DE EMPAREJAMIENTO** correspondiente al emparejamiento **myVnet1ToVNet2** ahora también aparece como **Conectado**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-168">The **PEERING STATUS** for the **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="4e2dd-169">El emparejamiento se establece correctamente una vez que ve el estado **Conectado** en la columna **ESTADO DE EMPAREJAMIENTO** para las dos redes virtuales del emparejamiento.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-169">The peering is successfully established after you see **Connected** in the **PEERING STATUS** column for both virtual networks in the peering.</span></span>
14. <span data-ttu-id="4e2dd-170">**Opcional**: Si bien este tutorial no aborda la creación de máquinas virtuales, puede crear una máquina virtual en cada red virtual y conectar de una máquina virtual a la otra para así validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
15. <span data-ttu-id="4e2dd-171">**Opcional**: Para eliminar los recursos que crea en este tutorial, complete los pasos que aparecen en la sección [Eliminación de recursos](#delete-portal) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-171">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="4e2dd-172">Los recursos de Azure que cree en cualquiera de las redes virtuales ahora se pueden comunicar entre sí mediante sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-172">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4e2dd-173">Si usa la resolución de nombres predeterminada de Azure para las redes virtuales, los recursos de las redes virtuales no pueden resolver nombres entre las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-173">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4e2dd-174">Si desea resolver nombres entre las redes virtuales de un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-174">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4e2dd-175">Obtenga información sobre cómo configurar la [resolución de nombres mediante su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-175">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="4e2dd-176"><a name="cli"></a>Creación de emparejamiento: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4e2dd-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="4e2dd-177">El script siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-177">The following script:</span></span>

- <span data-ttu-id="4e2dd-178">Requiere la versión 2.0.4 o posterior de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-178">Requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4e2dd-179">Para encontrar la versión, ejecute el comando `az --version`.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-179">To find the version, run the `az --version` command.</span></span> <span data-ttu-id="4e2dd-180">Si necesita actualizarla, consulte [Instalación de la CLI de Azure 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-180">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="4e2dd-181">Funciona en un shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-181">Works in a Bash shell.</span></span> <span data-ttu-id="4e2dd-182">Para ver las opciones de ejecución de scripts de la CLI de Azure en un cliente Windows, consulte [Using the Azure CLI on Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Uso de la CLI de Azure en Windows).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-182">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="4e2dd-183">En lugar de instalar la CLI y sus dependencias, puede usar Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-183">Instead of installing the CLI and its dependencies, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="4e2dd-184">Azure Cloud Shell es un shell de Bash gratuito que se puede ejecutar directamente en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="4e2dd-185">Tiene la CLI de Azure preinstalada y configurada para utilizar con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="4e2dd-186">Haga clic en el botón **Pruébelo** en el script siguiente, que invoca un Cloud Shell en el que puede iniciar sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="4e2dd-187">Para ejecutar el script, haga clic en el botón **Copiar** y pegue el contenido en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-187">To execute the script, click the **Copy** button and paste the contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="4e2dd-188">Cree un grupo de recursos y dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="4e2dd-189">Cree un emparejamiento de redes virtuales entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-189">Create a virtual network peering between the two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="4e2dd-190">Una vez que se ejecute el script, revise los emparejamientos de cada red virtual.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-190">After the script executes, review the peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="4e2dd-191">Vuelva a ejecutar el comando anterior, reemplazando *myVnet1* por *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-191">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="4e2dd-192">La salida de ambos comandos muestra **Conectado** en la columna **PeeringState**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-192">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>

     <span data-ttu-id="4e2dd-193">Los recursos de Azure que cree en cualquiera de las redes virtuales ahora se pueden comunicar entre sí mediante sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-193">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4e2dd-194">Si usa la resolución de nombres predeterminada de Azure para las redes virtuales, los recursos de las redes virtuales no pueden resolver nombres entre las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-194">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4e2dd-195">Si desea resolver nombres entre las redes virtuales de un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-195">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4e2dd-196">Obtenga información sobre cómo configurar la [resolución de nombres mediante su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-196">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="4e2dd-197">**Opcional**: Si bien este tutorial no aborda la creación de máquinas virtuales, puede crear una máquina virtual en cada red virtual y conectar de una máquina virtual a la otra para así validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
5. <span data-ttu-id="4e2dd-198">**Opcional**: para eliminar los recursos que crea en este tutorial, complete los pasos que aparecen en la sección [Eliminar recursos](#delete-cli) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-198">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="4e2dd-199"><a name="powershell"></a>Creación de emparejamiento: PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e2dd-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="4e2dd-200">Instale la versión más reciente del módulo [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-200">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="4e2dd-201">Si no está familiarizado con Azure PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-201">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4e2dd-202">Para iniciar una sesión de PowerShell, vaya a **Inicio**, escriba **powershell** y, luego, haga clic en **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-202">To start a PowerShell session, go to **Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="4e2dd-203">En PowerShell, inicie sesión en Azure con el comando `login-azurermaccount`.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-203">In PowerShell, log in to Azure by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="4e2dd-204">La cuenta con la que inicie sesión debe tener todos los permisos necesarios para crear un emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-204">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="4e2dd-205">Para detalles, consulte la sección [Permisos](#permissions) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-205">See the [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="4e2dd-206">Cree un grupo de recursos y dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="4e2dd-207">Para ejecutar el script, copie el script siguiente, péguelo en PowerShell y, a continuación, presione `Enter` después de la última línea aparece en la pantalla:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-207">To execute the script, copy the following script, paste it into PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>

    ```powershell
    # Variables for common values used throughout the script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="4e2dd-208">Cree un emparejamiento de redes virtuales entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-208">Create a virtual network peering between the two virtual networks.</span></span> <span data-ttu-id="4e2dd-209">Copie el script siguiente, péguelo en PowerShell y, a continuación, presione `Enter` después de la última línea aparece en la pantalla:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-209">Copy the following script, paste in to PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="4e2dd-210">Para revisar las subredes de la red virtual, copie el comando siguiente, péguelo en la ventana de PowerShell y presione `Enter`:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-210">To review the subnets for the virtual network, copy the following command, paste in to PowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="4e2dd-211">Vuelva a ejecutar el comando anterior, reemplazando *myVnet1* por *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-211">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="4e2dd-212">La salida de ambos comandos muestra **Conectado** en la columna **PeeringState**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-212">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>
7. <span data-ttu-id="4e2dd-213">**Opcional**: Si bien este tutorial no aborda la creación de máquinas virtuales, puede crear una máquina virtual en cada red virtual y conectar de una máquina virtual a la otra para así validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
8. <span data-ttu-id="4e2dd-214">**Opcional**: para eliminar los recursos que crea en este tutorial, complete los pasos que aparecen en la sección [Eliminar recursos](#delete-powershell) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-214">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="4e2dd-215">Los recursos de Azure que cree en cualquiera de las redes virtuales ahora se pueden comunicar entre sí mediante sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-215">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="4e2dd-216">Si usa la resolución de nombres predeterminada de Azure para las redes virtuales, los recursos de las redes virtuales no pueden resolver nombres entre las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-216">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="4e2dd-217">Si desea resolver nombres entre las redes virtuales de un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-217">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4e2dd-218">Obtenga información sobre cómo configurar la [resolución de nombres mediante su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-218">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="4e2dd-219"><a name="template"></a>Creación de emparejamiento: plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4e2dd-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="4e2dd-220">Consulte [Creación de un emparejamiento de red virtual](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) mediante una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="4e2dd-221">Las instrucciones se proporcionan con la plantilla para implementar la plantilla mediante Azure Portal, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-221">Instructions are provided with the template for deploying the template using the Azure portal, PowerShell, or the Azure CLI.</span></span> <span data-ttu-id="4e2dd-222">Inicie sesión en la herramienta que prefiera para implementar la plantilla con una cuenta que tenga los permisos necesarios para crear un emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-222">Log in to whichever tool you choose to deploy the template with using an account that has the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="4e2dd-223">Para detalles, consulte la sección [Permisos](#permissions) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-223">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="4e2dd-224">**Opcional**: Si bien este tutorial no aborda la creación de máquinas virtuales, puede crear una máquina virtual en cada red virtual y conectar de una máquina virtual a la otra para así validar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
3. <span data-ttu-id="4e2dd-225">**Opcional**: Para eliminar los recursos que crea en este tutorial, complete los pasos que aparecen en la sección [Eliminación de recursos](#delete) de este artículo, ya sea mediante Azure Portal, PowerShell o la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-225">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete) section of this article, using either the Azure portal, PowerShell, or the Azure CLI.</span></span>

## <span data-ttu-id="4e2dd-226"><a name="permissions"></a>Permisos</span><span class="sxs-lookup"><span data-stu-id="4e2dd-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="4e2dd-227">Las cuentas que use para crear un emparejamiento de redes virtuales deben tener el rol o los permisos necesarios.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-227">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="4e2dd-228">Por ejemplo, si está emparejando dos redes virtuales denominadas VNet1 y VNet2, su cuenta debe tener asignado el rol o los permisos mínimos siguientes para cada red virtual:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="4e2dd-229">Red virtual</span><span class="sxs-lookup"><span data-stu-id="4e2dd-229">Virtual network</span></span>|<span data-ttu-id="4e2dd-230">Rol</span><span class="sxs-lookup"><span data-stu-id="4e2dd-230">Role</span></span>|<span data-ttu-id="4e2dd-231">Permisos</span><span class="sxs-lookup"><span data-stu-id="4e2dd-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="4e2dd-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="4e2dd-232">VNet1</span></span>|[<span data-ttu-id="4e2dd-233">Colaborador de la red</span><span class="sxs-lookup"><span data-stu-id="4e2dd-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4e2dd-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="4e2dd-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="4e2dd-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="4e2dd-235">VNet2</span></span>|[<span data-ttu-id="4e2dd-236">Colaborador de la red</span><span class="sxs-lookup"><span data-stu-id="4e2dd-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4e2dd-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="4e2dd-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="4e2dd-238">Obtenga más información sobre los [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y la asignación de permisos específicos a [roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="4e2dd-239"><a name="delete"></a>Eliminación de recursos</span><span class="sxs-lookup"><span data-stu-id="4e2dd-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="4e2dd-240">Cuando haya terminado este tutorial, es posible que quiera eliminar los recursos que creó en el tutorial, para no incurrir en gastos de uso.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-240">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="4e2dd-241">Al eliminar un grupo de recursos se eliminan también todos los recursos contenidos en el mismo.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-241">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="4e2dd-242"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4e2dd-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="4e2dd-243">En el cuadro de búsqueda del portal, escriba **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-243">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="4e2dd-244">En los resultados de la búsqueda, haga clic en **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-244">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="4e2dd-245">En la hoja **myResourceGroup**, haga clic en el icono **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-245">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="4e2dd-246">Para confirmar la eliminación, en el cuadro **ESCRIBA EL NOMBRE DEL GRUPO DE RECURSOS**, escriba **myResourceGroup** y, luego, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-246">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="4e2dd-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4e2dd-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="4e2dd-248">Escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-248">Enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="4e2dd-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e2dd-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="4e2dd-250">Escriba el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="4e2dd-250">Enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="4e2dd-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e2dd-251">Next steps</span></span>

- <span data-ttu-id="4e2dd-252">Conozca en profundidad las [restricciones y comportamientos importantes del emparejamiento de redes virtuales](virtual-network-manage-peering.md#requirements-and-constraints) antes de crear un emparejamiento de redes virtuales para su uso en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="4e2dd-253">Conozca toda la [configuración de emparejamiento de redes virtuales](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="4e2dd-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="4e2dd-254">Obtenga información sobre cómo [crear una topología de red de concentrador y radio](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4e2dd-254">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
