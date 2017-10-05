---
title: "Administración de grupos de seguridad de red con Azure Portal | Microsoft Docs"
description: Aprenda a administrar grupos de seguridad de red existentes con Azure Portal.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5d55679d-57da-457c-97dc-1e1973909ee5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.openlocfilehash: e9bcf8a893ff209337f6a5763b631a22f8514e20
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="manage-nsgs-using-the-portal"></a><span data-ttu-id="56a91-103">Administración de grupos de seguridad de red mediante el portal</span><span class="sxs-lookup"><span data-stu-id="56a91-103">Manage NSGs using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="56a91-104">Portal</span><span class="sxs-lookup"><span data-stu-id="56a91-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="56a91-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56a91-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="56a91-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="56a91-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="56a91-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="56a91-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="56a91-108">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="56a91-108">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="56a91-109">Recuperar información</span><span class="sxs-lookup"><span data-stu-id="56a91-109">Retrieve Information</span></span>
<span data-ttu-id="56a91-110">Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.</span><span class="sxs-lookup"><span data-stu-id="56a91-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="56a91-111">Consultar los NSG existentes</span><span class="sxs-lookup"><span data-stu-id="56a91-111">View existing NSGs</span></span>

<span data-ttu-id="56a91-112">Para ver todos los NSG existentes en una suscripción, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-112">To view all existing NSGs in a subscription, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-113">Desde un explorador, vaya a http://portal.azure.com y, si fuera necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="56a91-113">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="56a91-114">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="56a91-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="56a91-116">Compruebe la lista de NSG en la hoja **Grupos de seguridad de red** .</span><span class="sxs-lookup"><span data-stu-id="56a91-116">Check the list of NSGs in the **Network security groups** blade.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="56a91-118">Visualización de los NSG en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="56a91-118">View NSGs in a resource group</span></span>

<span data-ttu-id="56a91-119">Para consultar la lista de NSG del grupo de recursos **RG-NSG**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-119">To view the list of NSGs in the **RG-NSG** resource group, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-120">Haga clic en **Grupos de recursos >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="56a91-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="56a91-122">En la lista de recursos, busque elementos que incluyan el icono NSG, tal como aparece en la hoja **Recursos** que se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="56a91-122">In the list of resources, look for items displaying the NSG icon, as shown in the **Resources** blade below.</span></span>

    ![Portal de Azure: NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="56a91-124">Mostrar todas las reglas de un NSG</span><span class="sxs-lookup"><span data-stu-id="56a91-124">List all rules for an NSG</span></span>

<span data-ttu-id="56a91-125">Para consultar las reglas de un NSG llamado **NSG-FrontEnd**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-125">To view the rules of an NSG named **NSG-FrontEnd**, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-126">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-126">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="56a91-127">En la pestaña **Configuración**, haga clic en **Reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="56a91-127">In the **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="56a91-129">La hoja **Reglas de seguridad de entrada** aparece como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="56a91-129">The **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="56a91-131">En la pestaña **Configuración**, haga clic en **Reglas de seguridad de salida** para ver las reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="56a91-131">In the **Settings** tab, click **Outbound security rules** to see the outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="56a91-132">Para consultar las reglas predeterminadas, haga clic en el icono **Reglas predeterminadas** que se encuentra en la parte superior de la hoja donde aparecen las reglas.</span><span class="sxs-lookup"><span data-stu-id="56a91-132">To view default rules, click the **Default rules** icon at the top of the blade that displays the rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="56a91-133">Consultar las asociaciones de NSG</span><span class="sxs-lookup"><span data-stu-id="56a91-133">View NSGs associations</span></span>

<span data-ttu-id="56a91-134">Para consultar cuáles son los recursos con los que está asociado el NSG **NSG-FrontEnd**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-134">To view what resources the **NSG-FrontEnd** NSG is associate with, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-135">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-135">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="56a91-136">En la pestaña **Configuración**, haga clic en **Subredes** para consultar cuáles son las subredes que están asociadas con el NSG.</span><span class="sxs-lookup"><span data-stu-id="56a91-136">In the **Settings** tab, click **Subnets** to view what subnets are associated to the NSG.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="56a91-138">En la pestaña **Configuración**, haga clic en **Interfaces de red** para consultar cuáles son las NIC que están asociadas con el NSG.</span><span class="sxs-lookup"><span data-stu-id="56a91-138">In the **Settings** tab, click **Network interfaces** to view what NICs are associated to the NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="56a91-139">Administrar las reglas</span><span class="sxs-lookup"><span data-stu-id="56a91-139">Manage rules</span></span>
<span data-ttu-id="56a91-140">Puede agregar reglas a un NSG existente, editar reglas existentes y quitar reglas.</span><span class="sxs-lookup"><span data-stu-id="56a91-140">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="56a91-141">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="56a91-141">Add a rule</span></span>
<span data-ttu-id="56a91-142">Para agregar una regla que permita el tráfico **de entrada** al puerto **443** desde cualquier máquina al grupo de seguridad de red **NSG-FrontEnd**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-142">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-143">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-143">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="56a91-144">En la pestaña **Configuración**, haga clic en **Reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="56a91-144">In the **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="56a91-145">En la hoja **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="56a91-145">In the **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="56a91-146">Luego, en la hoja **Agregar regla de seguridad de entrada**, rellene los valores como se muestra a continuación y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="56a91-146">Then, in the **Add inbound security rule** blade, fill the values as shown below, and then click **OK**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="56a91-148">Después de unos segundos, observe la regla nueva en la hoja **Reglas de seguridad de entrada** .</span><span class="sxs-lookup"><span data-stu-id="56a91-148">After a few seconds, notice the new rule in the **Inbound security rules** blade.</span></span>

    ![Portal de Azure: NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="56a91-150">Cambiar una regla</span><span class="sxs-lookup"><span data-stu-id="56a91-150">Change a rule</span></span>
<span data-ttu-id="56a91-151">Para cambiar la regla que creó antes para permitir el tráfico de entrada solo desde **Internet**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-151">To change the rule created above to allow inbound traffic from the **Internet** only, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-152">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-152">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="56a91-153">En la pestaña **Configuración** , haga clic en la regla que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="56a91-153">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="56a91-154">En la hoja **allow-https**, cambie la propiedad **Origen** como se muestra a continuación y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56a91-154">In the **allow-https** blade, change the **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="56a91-156">Eliminar una regla</span><span class="sxs-lookup"><span data-stu-id="56a91-156">Delete a rule</span></span>

<span data-ttu-id="56a91-157">Para eliminar la regla que creó antes, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-157">To delete the rule created above, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-158">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-158">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="56a91-159">En la pestaña **Configuración** , haga clic en la regla que se creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="56a91-159">In the **Settings** tab, click the rule created above.</span></span>
3. <span data-ttu-id="56a91-160">En la hoja **allow-https**, haga clic en **Eliminar** y en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="56a91-160">In the **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="56a91-162">Administrar las asociaciones</span><span class="sxs-lookup"><span data-stu-id="56a91-162">Manage associations</span></span>
<span data-ttu-id="56a91-163">Puede asociar un NSG a subredes y NIC.</span><span class="sxs-lookup"><span data-stu-id="56a91-163">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="56a91-164">También puede desasociar un NSG de cualquier recurso al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="56a91-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="56a91-165">Asociar un NSG a una NIC</span><span class="sxs-lookup"><span data-stu-id="56a91-165">Associate an NSG to a NIC</span></span>
<span data-ttu-id="56a91-166">Para asociar el grupo de seguridad de red **NSG-FrontEnd** a la NIC **TestNICWeb1**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-166">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-167">En la hoja **Grupos de seguridad de red** o la hoja **Recursos** que se muestra arriba, haga clic en **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-167">From the **Network security groups** blade, or the **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="56a91-168">En la pestaña **Configuración**, haga clic en **Interfaces de red** > **Asociar** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="56a91-168">In the **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="56a91-170">Desasociar un NSG de una NIC</span><span class="sxs-lookup"><span data-stu-id="56a91-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="56a91-171">Para desasociar el grupo de seguridad de red **NSG-FrontEnd** de la NIC **TestNICWeb1**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-171">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-172">En Azure Portal, haga clic en **Grupos de recursos >** > **RG-NSG** > **...** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="56a91-172">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="56a91-173">En la hoja **TestNICWeb1**, haga clic en **Cambiar seguridad...** > **Ninguna**.</span><span class="sxs-lookup"><span data-stu-id="56a91-173">In the **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="56a91-175">También puede usar esta hoja para asociar la NIC a cualquier NSG existente.</span><span class="sxs-lookup"><span data-stu-id="56a91-175">You can also use this blade to associate the NIC to any existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="56a91-176">Desasociar un NSG de una subred</span><span class="sxs-lookup"><span data-stu-id="56a91-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="56a91-177">Para desasociar el grupo de seguridad de red **NSG-FrontEnd** de la subred **FrontEnd**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-177">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-178">En Azure Portal, haga clic en **Grupos de recursos >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="56a91-178">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="56a91-179">En la hoja **Configuración**, haga clic en **Subredes** > **FrontEnd** > **Grupo de seguridad de red** > **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="56a91-179">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="56a91-181">En la hoja **FrontEnd**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56a91-181">In the **FrontEnd** blade, click **Save**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="56a91-183">Asociación de un grupo de seguridad de red a una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="56a91-183">Associate an NSG to a subnet</span></span>

<span data-ttu-id="56a91-184">Para asociar el grupo de seguridad de red **NSG-FrontEnd** a la subred **FrontEnd**, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-184">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="56a91-185">En Azure Portal, haga clic en **Grupos de recursos >** > **RG-NSG** > **...** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="56a91-185">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="56a91-186">En la hoja **Configuración**, haga clic en **Subredes** > **FrontEnd** > **Grupo de seguridad de red** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-186">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="56a91-187">En la hoja **FrontEnd**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="56a91-187">In the **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="56a91-188">También puede asociar un NSG a una subred desde la hoja **Configuración** del NSG.</span><span class="sxs-lookup"><span data-stu-id="56a91-188">You can also associate an NSG to a subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="56a91-189">Eliminación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="56a91-189">Delete an NSG</span></span>
<span data-ttu-id="56a91-190">Solo se puede eliminar un NSG que no está asociado a ningún recurso.</span><span class="sxs-lookup"><span data-stu-id="56a91-190">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="56a91-191">Para eliminar un NSG, complete los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="56a91-191">To delete an NSG, complete the following steps:.</span></span>

1. <span data-ttu-id="56a91-192">En Azure Portal, haga clic en **Grupos de recursos >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="56a91-192">From the Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="56a91-193">En la hoja **Configuración**, haga clic en **Interfaces de red**.</span><span class="sxs-lookup"><span data-stu-id="56a91-193">In the **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="56a91-194">Si aparece alguna NIC, haga clic en ella y siga el paso 2 de [Desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="56a91-194">If there are any NICs listed, click the NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="56a91-195">Repita el paso 3 para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="56a91-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="56a91-196">En la hoja **Configuración**, haga clic en **Subredes**.</span><span class="sxs-lookup"><span data-stu-id="56a91-196">In the **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="56a91-197">Si aparece alguna subred, haga clic en ella y siga los pasos 2 y 3 de [Desasociar un NSG de una subred](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="56a91-197">If there are any subnets listed, click the subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="56a91-198">Desplácese a la izquierda hasta la hoja **NSG-FrontEnd** y haga clic en **Eliminar** > **Sí**.</span><span class="sxs-lookup"><span data-stu-id="56a91-198">Scrolls left to the **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="56a91-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="56a91-200">Next steps</span></span>
* <span data-ttu-id="56a91-201">[Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.</span><span class="sxs-lookup"><span data-stu-id="56a91-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
