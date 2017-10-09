---
title: "aaaCreate un emparejamiento de red virtual de Azure - Administrador de recursos - misma suscripción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un emparejamiento de red virtual entre redes virtuales creado mediante el Administrador de recursos que existen en hello misma suscripción de Azure."
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
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="1b572-103">Creación de un emparejamiento de redes virtuales: Resource Manager, misma suscripción</span><span class="sxs-lookup"><span data-stu-id="1b572-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="1b572-104">En este tutorial, aprenderá toocreate una emparejamiento entre redes virtuales creadas mediante el Administrador de recursos de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="1b572-105">Ambas redes virtuales residen en hello misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="1b572-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="1b572-106">Emparejamiento dos redes virtuales permite recursos en diferentes redes virtuales toocommunicate entre sí con Hola mismo ancho de banda y latencia como si estuvieran recursos Hola Hola misma red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="1b572-107">Obtenga más información sobre el [Emparejamiento de redes virtuales](virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b572-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="1b572-108">Hello pasos toocreate un emparejamiento de red virtual son diferentes, dependiendo de si son redes virtuales de hello en hello iguales o distinto, suscripciones y que [modelo de implementación de Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello las redes virtuales se crean a través de.</span><span class="sxs-lookup"><span data-stu-id="1b572-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="1b572-109">Obtenga información acerca de cómo toocreate un virtual red emparejamiento en otros escenarios, haga clic en el escenario de Hola de hello en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="1b572-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="1b572-110">Modelo de implementación de Azure</span><span class="sxs-lookup"><span data-stu-id="1b572-110">Azure deployment model</span></span>  | <span data-ttu-id="1b572-111">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="1b572-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="1b572-112">Ambas mediante Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b572-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="1b572-113">Diferentes</span><span class="sxs-lookup"><span data-stu-id="1b572-113">Different</span></span>|
|[<span data-ttu-id="1b572-114">Una mediante Resource Manager y la otra, clásico</span><span class="sxs-lookup"><span data-stu-id="1b572-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="1b572-115">Iguales</span><span class="sxs-lookup"><span data-stu-id="1b572-115">Same</span></span>|
|[<span data-ttu-id="1b572-116">Una mediante Resource Manager y la otra, clásico</span><span class="sxs-lookup"><span data-stu-id="1b572-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="1b572-117">Diferentes</span><span class="sxs-lookup"><span data-stu-id="1b572-117">Different</span></span>|

<span data-ttu-id="1b572-118">No se puede crear un intercambio de tráfico de red virtual entre dos redes virtuales que se implementan a través del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="1b572-119">Un intercambio de tráfico de red virtual solo puede crearse entre dos redes virtuales que existen en hello misma región de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b572-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="1b572-120">Si necesita tooconnect las redes virtuales que se crearon a través del modelo de implementación clásica de hello, o que existen en diferentes regiones de Azure, puede usar un Azure [puerta de enlace VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Hola redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1b572-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="1b572-121">Puede usar hello [portal de Azure](#portal), hello Azure [interfaz de línea de comandos](#cli) (CLI), Azure [PowerShell](#powershell), o un [plantilla de Azure Resource Manager](#template) toocreate un emparejamiento de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="1b572-122">Haga clic en cualquiera de hello anterior herramienta vínculos toogo directamente toohello los pasos para crear un intercambio de tráfico de red virtual mediante la herramienta de elección.</span><span class="sxs-lookup"><span data-stu-id="1b572-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="1b572-123"><a name="portal"></a>Creación de emparejamiento: Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b572-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="1b572-124">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b572-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1b572-125">cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="1b572-126">Vea hello [permisos](#permissions) sección de este artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1b572-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="1b572-127">Haga clic en **+ Nuevo**, **Redes** y, luego, en **Red virtual**.</span><span class="sxs-lookup"><span data-stu-id="1b572-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="1b572-128">Hola **crear red virtual** hoja, escriba, o seleccionar los valores de hello después de la configuración, haga clic en **crear**:</span><span class="sxs-lookup"><span data-stu-id="1b572-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="1b572-129">**Nombre**: *myVnet1*</span><span class="sxs-lookup"><span data-stu-id="1b572-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="1b572-130">**Espacio de direcciones**: *10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1b572-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="1b572-131">**Nombre de subred**: *default*</span><span class="sxs-lookup"><span data-stu-id="1b572-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1b572-132">**Intervalo de direcciones de subred**: *10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1b572-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="1b572-133">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="1b572-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1b572-134">**Grupo de recursos**: seleccione **Crear nuevo** y escriba *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1b572-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="1b572-135">**Ubicación**: *este de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="1b572-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="1b572-136">Complete los pasos 2 y 3, vuelva a especificar Hola después los valores en el paso 3:</span><span class="sxs-lookup"><span data-stu-id="1b572-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="1b572-137">**Nombre**: *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="1b572-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="1b572-138">**Espacio de direcciones**: *10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="1b572-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="1b572-139">**Nombre de subred**: *default*</span><span class="sxs-lookup"><span data-stu-id="1b572-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="1b572-140">**Intervalo de direcciones de subred**: *10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="1b572-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="1b572-141">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="1b572-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="1b572-142">**Grupo de recursos**: seleccione **Usar existente** y seleccione *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="1b572-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="1b572-143">**Ubicación**: *este de EE. UU.*</span><span class="sxs-lookup"><span data-stu-id="1b572-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="1b572-144">Hola **buscar recursos** cuadro parte superior de hello del portal de hello, tipo *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="1b572-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="1b572-145">Haga clic en **myResourceGroup** cuando aparece en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="1b572-146">Aparece una hoja de hello **myresourcegroup** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1b572-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="1b572-147">grupo de recursos de Hello contiene Hola dos redes virtuales creadas en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="1b572-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="1b572-148">Haga clic en **myVNet1**.</span><span class="sxs-lookup"><span data-stu-id="1b572-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="1b572-149">Hola **myVnet1** hoja que aparece, haga clic en **emparejamientos** en lista vertical de Hola de opciones en la parte izquierda de la hoja de Hola de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="1b572-150">Hola **myVnet1 - emparejamientos** hoja que aparece, haga clic en **+ agregar**</span><span class="sxs-lookup"><span data-stu-id="1b572-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="1b572-151">Hola **agregar emparejamiento** hoja que aparece, escriba, o seleccione Hola siguientes opciones, haga clic en **Aceptar**:</span><span class="sxs-lookup"><span data-stu-id="1b572-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="1b572-152">**Nombre**: *myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="1b572-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="1b572-153">**Modelo de implementación de red virtual**: seleccione **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="1b572-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="1b572-154">**Suscripción**: seleccione la suscripción</span><span class="sxs-lookup"><span data-stu-id="1b572-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="1b572-155">**Red virtual**: haga clic en **Elegir una red virtual** y, luego, en **myVnet2**.</span><span class="sxs-lookup"><span data-stu-id="1b572-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="1b572-156">**Permitir acceso a red virtual:** asegúrese de que esté seleccionada la opción **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="1b572-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="1b572-157">En este tutorial no se usa ninguna otra configuración.</span><span class="sxs-lookup"><span data-stu-id="1b572-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="1b572-158">leer toolearn sobre todas las opciones de intercambio de tráfico, [administrar emparejamientos de red virtual](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1b572-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="1b572-159">Tras hacer clic en **Aceptar** en el paso anterior de hello, Hola **agregar emparejamiento** hoja se cierra y vea hello **myVnet1 - emparejamientos** hoja de nuevo.</span><span class="sxs-lookup"><span data-stu-id="1b572-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="1b572-160">Después de unos segundos, Hola emparejamiento que ha creado aparece en la hoja de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="1b572-161">**Inicia** aparece en hello **estado EMPAREJAMIENTO** columna para hello **myVnet1ToMyVnet2** emparejamiento se creó.</span><span class="sxs-lookup"><span data-stu-id="1b572-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="1b572-162">Ha emparejar tooVnet2 Vnet1, pero ahora debe del mismo nivel myVnet2 toomyVnet1.</span><span class="sxs-lookup"><span data-stu-id="1b572-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="1b572-163">Hola emparejamiento debe crearse en ambas direcciones tooenable recursos en hello toocommunicate de redes virtuales entre sí.</span><span class="sxs-lookup"><span data-stu-id="1b572-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="1b572-164">Complete nuevamente los pasos del 5 al 10 para myVnet2.</span><span class="sxs-lookup"><span data-stu-id="1b572-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="1b572-165">Nombre hello emparejamiento *myVnet2ToMyVnet1*.</span><span class="sxs-lookup"><span data-stu-id="1b572-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="1b572-166">Unos pocos segundos después de hacer clic **Aceptar** toocreate Hola emparejamiento para MyVnet2, hello **myVnet2ToMyVnet1** emparejamiento que acaba de crear aparece con **conectado** en hello  **ESTADO de EMPAREJAMIENTO** columna.</span><span class="sxs-lookup"><span data-stu-id="1b572-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="1b572-167">Complete nuevamente los pasos del 5 al 7 para MyVnet1.</span><span class="sxs-lookup"><span data-stu-id="1b572-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="1b572-168">Hola **estado EMPAREJAMIENTO** para hello **myVnet1ToVNet2** emparejamiento ahora también es **conectado**.</span><span class="sxs-lookup"><span data-stu-id="1b572-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="1b572-169">Hola emparejamiento se ha establecido correctamente después de ver **conectado** en hello **estado EMPAREJAMIENTO** columna para ambas redes virtuales en el emparejamiento de Hola de.</span><span class="sxs-lookup"><span data-stu-id="1b572-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="1b572-170">**Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.</span><span class="sxs-lookup"><span data-stu-id="1b572-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="1b572-171">**Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete-portal) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b572-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="1b572-172">Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1b572-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="1b572-173">Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="1b572-174">Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="1b572-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1b572-175">Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1b572-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="1b572-176"><a name="cli"></a>Creación de emparejamiento: CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1b572-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="1b572-177">Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="1b572-177">hello following script:</span></span>

- <span data-ttu-id="1b572-178">Requiere hello Azure CLI versión 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="1b572-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1b572-179">versión de hello toofind, ejecute hello `az --version` comando.</span><span class="sxs-lookup"><span data-stu-id="1b572-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="1b572-180">Si necesita tooupgrade, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b572-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="1b572-181">Funciona en un shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="1b572-181">Works in a Bash shell.</span></span> <span data-ttu-id="1b572-182">Para opciones sobre cómo ejecutar las secuencias de comandos de CLI de Azure en el cliente de Windows, vea [ejecuta Hola CLI de Azure en Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b572-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="1b572-183">En lugar de instalar Hola CLI y sus dependencias, puede usar Hola Shell en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b572-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="1b572-184">Hola Shell en la nube de Azure es un shell de Bash gratuito que se puede ejecutar directamente dentro de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b572-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="1b572-185">Tiene hello Azure CLI preinstalado y configurado toouse con su cuenta.</span><span class="sxs-lookup"><span data-stu-id="1b572-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="1b572-186">Haga clic en hello **Pruébelo** botón en el script de Hola que se indica a continuación, que invoca un Shell en la nube que registra se puede iniciar sesión en tooyour cuenta de Azure con.</span><span class="sxs-lookup"><span data-stu-id="1b572-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="1b572-187">tooexecute hello secuencia de comandos, haga clic en hello **copia** botón y pegue el contenido de hello en el Shell de nube.</span><span class="sxs-lookup"><span data-stu-id="1b572-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="1b572-188">Cree un grupo de recursos y dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1b572-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

2. <span data-ttu-id="1b572-189">Crear una red virtual emparejamiento entre las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="1b572-190">Después de ejecuta el script de Hola, revise los emparejamientos de Hola para cada red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="1b572-191">Hola anterior vuelva a ejecutar comando, reemplazando *myVnet1* con *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="1b572-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="1b572-192">salida de Hello de ambos comandos muestra **conectado** en hello **PeeringState** columna.</span><span class="sxs-lookup"><span data-stu-id="1b572-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="1b572-193">Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1b572-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="1b572-194">Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="1b572-195">Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="1b572-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1b572-196">Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1b572-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="1b572-197">**Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.</span><span class="sxs-lookup"><span data-stu-id="1b572-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="1b572-198">**Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-cli) en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b572-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="1b572-199"><a name="powershell"></a>Creación de emparejamiento: PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b572-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="1b572-200">Instale Hola la versión más reciente de hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo.</span><span class="sxs-lookup"><span data-stu-id="1b572-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="1b572-201">Si está tooAzure nuevo PowerShell, consulte [Introducción a Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1b572-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="1b572-202">toostart una sesión de PowerShell, vaya demasiado**iniciar**, escriba **powershell**y, a continuación, haga clic en **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1b572-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="1b572-203">En PowerShell, inicie sesión en tooAzure escribiendo hello `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="1b572-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="1b572-204">cuenta de Hello con que utiliza para iniciar sesión debe tener Hola permisos necesarios toocreate un emparejamiento de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="1b572-205">Vea hello [permisos](#permissions) sección de este artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1b572-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="1b572-206">Cree un grupo de recursos y dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="1b572-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="1b572-207">script de Hola tooexecute, copia Hola siguiente script, péguelo en PowerShell y presione `Enter` después de hello última línea aparece en la pantalla de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="1b572-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
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

5. <span data-ttu-id="1b572-208">Crear una red virtual emparejamiento entre las dos redes virtuales de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="1b572-209">Siguiente Hola de copia de scripts, pegue en tooPowerShell y, a continuación, presione `Enter` después de hello última línea aparece en la pantalla de bienvenida:</span><span class="sxs-lookup"><span data-stu-id="1b572-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="1b572-210">subredes de hello tooreview para la red virtual de hello, copia Hola comando siguiente, pegue en tooPowerShell y, a continuación, presione `Enter`:</span><span class="sxs-lookup"><span data-stu-id="1b572-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="1b572-211">Hola anterior vuelva a ejecutar comando, reemplazando *myVnet1* con *myVnet2*.</span><span class="sxs-lookup"><span data-stu-id="1b572-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="1b572-212">salida de Hello de ambos comandos muestra **conectado** en hello **PeeringState** columna.</span><span class="sxs-lookup"><span data-stu-id="1b572-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="1b572-213">**Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.</span><span class="sxs-lookup"><span data-stu-id="1b572-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="1b572-214">**Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de [eliminar recursos](#delete-powershell) en este artículo.</span><span class="sxs-lookup"><span data-stu-id="1b572-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="1b572-215">Los recursos de Azure que se crea en cualquier red virtual están capaz de toocommunicate entre sí a través de sus direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="1b572-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="1b572-216">Si usas la resolución de nombres de Azure predeterminado para las redes virtuales de hello, Hola recursos en redes virtuales de hello no están tooresolve capaz de nombres a través de redes virtuales Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="1b572-217">Si desea tooresolve nombres a través de redes virtuales en un emparejamiento, debe crear su propio servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="1b572-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="1b572-218">Obtenga información acerca de cómo tooset una [resolución de nombres con su propio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span><span class="sxs-lookup"><span data-stu-id="1b572-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="1b572-219"><a name="template"></a>Creación de emparejamiento: plantilla de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1b572-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="1b572-220">Consulte [Creación de un emparejamiento de red virtual](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) mediante una plantilla de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1b572-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="1b572-221">Las instrucciones están proporcionados con la plantilla de hello para la implementación de plantilla de hello utilizando Hola portal de Azure, PowerShell u Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b572-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="1b572-222">Registro en la herramienta toowhichever elige toodeploy Hola plantilla con el uso de una cuenta que tenga Hola permisos necesarios toocreate un emparejamiento de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="1b572-223">Vea hello [permisos](#permissions) sección de este artículo para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="1b572-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="1b572-224">**Opcional**: aunque no se trata la creación de máquinas virtuales en este tutorial, puede crear una máquina virtual en cada red virtual y conectarse desde una máquina virtual toohello otras toovalidate conectividad.</span><span class="sxs-lookup"><span data-stu-id="1b572-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="1b572-225">**Opcional**: recursos de hello toodelete que creará en este tutorial, Hola completa los pasos de hello [eliminar recursos](#delete) sección de este artículo, mediante Hola Hola CLI de Azure, PowerShell o portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1b572-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="1b572-226"><a name="permissions"></a>Permisos</span><span class="sxs-lookup"><span data-stu-id="1b572-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="1b572-227">cuentas de Hello que usar toocreate un emparejamiento de red virtual deben tener rol necesarios de Hola o permisos.</span><span class="sxs-lookup"><span data-stu-id="1b572-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="1b572-228">Por ejemplo, si se emparejamiento dos redes virtuales denominadas VNet1 y VNet2, su cuenta se debe asignar Hola después de función mínima o los permisos para cada red virtual:</span><span class="sxs-lookup"><span data-stu-id="1b572-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="1b572-229">Red virtual</span><span class="sxs-lookup"><span data-stu-id="1b572-229">Virtual network</span></span>|<span data-ttu-id="1b572-230">Rol</span><span class="sxs-lookup"><span data-stu-id="1b572-230">Role</span></span>|<span data-ttu-id="1b572-231">Permisos</span><span class="sxs-lookup"><span data-stu-id="1b572-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="1b572-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="1b572-232">VNet1</span></span>|[<span data-ttu-id="1b572-233">Colaborador de la red</span><span class="sxs-lookup"><span data-stu-id="1b572-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1b572-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="1b572-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="1b572-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="1b572-235">VNet2</span></span>|[<span data-ttu-id="1b572-236">Colaborador de la red</span><span class="sxs-lookup"><span data-stu-id="1b572-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="1b572-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="1b572-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="1b572-238">Obtenga más información sobre [roles integrados](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) y asignar permisos específicos demasiado[roles personalizados](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (solo el Administrador de recursos).</span><span class="sxs-lookup"><span data-stu-id="1b572-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="1b572-239"><a name="delete"></a>Eliminación de recursos</span><span class="sxs-lookup"><span data-stu-id="1b572-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="1b572-240">Cuando haya terminado este tutorial, conviene toodelete recursos de Hola que creó en el tutorial de hello, por lo que no se incurre en cargos por uso.</span><span class="sxs-lookup"><span data-stu-id="1b572-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="1b572-241">Eliminación de un grupo de recursos, también elimina todos los recursos que se encuentran en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1b572-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="1b572-242"><a name="delete-portal"></a>Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b572-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="1b572-243">En el cuadro de búsqueda del portal de hello, escriba **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1b572-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="1b572-244">En los resultados de la búsqueda de hello, haga clic en **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1b572-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="1b572-245">En hello **myResourceGroup** hoja, haga clic en hello **eliminar** icono.</span><span class="sxs-lookup"><span data-stu-id="1b572-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="1b572-246">eliminación de hello tooconfirm, Hola **Hola nombre del grupo de recursos de tipo** cuadro, escriba **myResourceGroup**y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="1b572-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="1b572-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b572-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="1b572-248">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1b572-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="1b572-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b572-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="1b572-250">Escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="1b572-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="1b572-251">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1b572-251">Next steps</span></span>

- <span data-ttu-id="1b572-252">Conozca en profundidad las [restricciones y comportamientos importantes del emparejamiento de redes virtuales](virtual-network-manage-peering.md#requirements-and-constraints) antes de crear un emparejamiento de redes virtuales para su uso en el entorno de producción.</span><span class="sxs-lookup"><span data-stu-id="1b572-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="1b572-253">Conozca toda la [configuración de emparejamiento de redes virtuales](virtual-network-manage-peering.md#create-a-peering).</span><span class="sxs-lookup"><span data-stu-id="1b572-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="1b572-254">Obtenga información acerca de cómo demasiado[crear un concentrador y radio de la topología de red](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) con intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="1b572-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
