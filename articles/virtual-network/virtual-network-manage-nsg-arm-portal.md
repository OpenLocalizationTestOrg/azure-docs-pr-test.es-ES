---
title: los NSG de aaaManage con hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage existente NSG mediante Hola portal de Azure."
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
ms.openlocfilehash: ad9a4060bd81bae4597ad5a4f59622e10cd214cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-nsgs-using-hello-portal"></a><span data-ttu-id="e636c-103">Administrar los NSG mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="e636c-103">Manage NSGs using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e636c-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e636c-104">Portal</span></span>](virtual-network-manage-nsg-arm-portal.md)
> * [<span data-ttu-id="e636c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e636c-105">PowerShell</span></span>](virtual-network-manage-nsg-arm-ps.md)
> * [<span data-ttu-id="e636c-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="e636c-106">Azure CLI</span></span>](virtual-network-manage-nsg-arm-cli.md)
>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="e636c-107">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e636c-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e636c-108">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar del modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="e636c-108">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="e636c-109">Recuperar información</span><span class="sxs-lookup"><span data-stu-id="e636c-109">Retrieve Information</span></span>
<span data-ttu-id="e636c-110">Puede consultar los NSG existentes, recuperar las reglas de un NSG existente y averiguar cuáles son los recursos a los que está asociado un NSG.</span><span class="sxs-lookup"><span data-stu-id="e636c-110">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="e636c-111">Consultar los NSG existentes</span><span class="sxs-lookup"><span data-stu-id="e636c-111">View existing NSGs</span></span>

<span data-ttu-id="e636c-112">tooview todos los existentes NSG en una suscripción completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-112">tooview all existing NSGs in a subscription, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-113">Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e636c-113">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>

2. <span data-ttu-id="e636c-114">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="e636c-114">Click **Browse >** > **Network security groups**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure1.png)

3. <span data-ttu-id="e636c-116">Comprobar lista de Hola de NSG Hola **grupos de seguridad de red** hoja.</span><span class="sxs-lookup"><span data-stu-id="e636c-116">Check hello list of NSGs in hello **Network security groups** blade.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure2.png)

### <a name="view-nsgs-in-a-resource-group"></a><span data-ttu-id="e636c-118">Visualización de los NSG en un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e636c-118">View NSGs in a resource group</span></span>

<span data-ttu-id="e636c-119">lista de Hola de tooview de NSG de hello **NSG RG** grupo de recursos, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-119">tooview hello list of NSGs in hello **RG-NSG** resource group, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-120">Haga clic en **Grupos de recursos >** > **RG-NSG** > **...**.</span><span class="sxs-lookup"><span data-stu-id="e636c-120">Click **Resource groups >** > **RG-NSG** > **...**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure3.png)

2. <span data-ttu-id="e636c-122">En la lista Hola de recursos, buscar elementos mostrando hello NSG icono, tal y como se muestra en hello **recursos** hoja a continuación.</span><span class="sxs-lookup"><span data-stu-id="e636c-122">In hello list of resources, look for items displaying hello NSG icon, as shown in hello **Resources** blade below.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure4.png)

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="e636c-124">Mostrar todas las reglas de un NSG</span><span class="sxs-lookup"><span data-stu-id="e636c-124">List all rules for an NSG</span></span>

<span data-ttu-id="e636c-125">reglas de hello tooview de un NSG denominado **NSG-front-end**completa Hola lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e636c-125">tooview hello rules of an NSG named **NSG-FrontEnd**, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-126">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-126">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="e636c-127">Hola **configuración** , haga clic en **reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="e636c-127">In hello **Settings** tab, click **Inbound security rules**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure5.png)

3. <span data-ttu-id="e636c-129">Hola **reglas de seguridad de entrada** hoja se muestra tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="e636c-129">hello **Inbound security rules** blade is displayed as shown below.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure6.png)

4. <span data-ttu-id="e636c-131">Hola **configuración** , haga clic en **reglas de seguridad de salida** toosee Hola reglas de salida.</span><span class="sxs-lookup"><span data-stu-id="e636c-131">In hello **Settings** tab, click **Outbound security rules** toosee hello outbound rules.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e636c-132">las reglas predeterminadas de tooview, haga clic en hello **reglas predeterminadas** situado en la parte superior de Hola de hoja de Hola que muestra las reglas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e636c-132">tooview default rules, click hello **Default rules** icon at hello top of hello blade that displays hello rules.</span></span>
    >

### <a name="view-nsgs-associations"></a><span data-ttu-id="e636c-133">Consultar las asociaciones de NSG</span><span class="sxs-lookup"><span data-stu-id="e636c-133">View NSGs associations</span></span>

<span data-ttu-id="e636c-134">tooview qué Hola recursos **front-end de NSG** NSG está asociado con la, completa Hola siguiendo los pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-134">tooview what resources hello **NSG-FrontEnd** NSG is associate with, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-135">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-135">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>

2. <span data-ttu-id="e636c-136">Hola **configuración** , haga clic en **subredes** tooview qué subredes son asociados toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="e636c-136">In hello **Settings** tab, click **Subnets** tooview what subnets are associated toohello NSG.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure7.png)

3. <span data-ttu-id="e636c-138">Hola **configuración** , haga clic en **interfaces de red** tooview qué NIC están asociadas toohello NSG.</span><span class="sxs-lookup"><span data-stu-id="e636c-138">In hello **Settings** tab, click **Network interfaces** tooview what NICs are associated toohello NSG.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="e636c-139">Administrar las reglas</span><span class="sxs-lookup"><span data-stu-id="e636c-139">Manage rules</span></span>
<span data-ttu-id="e636c-140">Puede agregar tooan de reglas existente NSG, editar las reglas existentes y quitar las reglas.</span><span class="sxs-lookup"><span data-stu-id="e636c-140">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="e636c-141">Agregar una regla</span><span class="sxs-lookup"><span data-stu-id="e636c-141">Add a rule</span></span>
<span data-ttu-id="e636c-142">tooadd una regla que permite **entrante** tráfico tooport **443** desde cualquier máquina toohello **front-end de NSG** NSG, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-142">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-143">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-143">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e636c-144">Hola **configuración** , haga clic en **reglas de seguridad de entrada**.</span><span class="sxs-lookup"><span data-stu-id="e636c-144">In hello **Settings** tab, click **Inbound security rules**.</span></span>
3. <span data-ttu-id="e636c-145">Hola **reglas de seguridad de entrada** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="e636c-145">In hello **Inbound security rules** blade, click **Add**.</span></span> <span data-ttu-id="e636c-146">A continuación, en hello **Agregar regla de seguridad de entrada** hoja, rellenar los valores de hello tal y como se muestra a continuación y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e636c-146">Then, in hello **Add inbound security rule** blade, fill hello values as shown below, and then click **OK**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure8.png)

    <span data-ttu-id="e636c-148">Después de unos segundos, tenga en cuenta nueva regla de Hola Hola **reglas de seguridad de entrada** hoja.</span><span class="sxs-lookup"><span data-stu-id="e636c-148">After a few seconds, notice hello new rule in hello **Inbound security rules** blade.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure9.png)

### <a name="change-a-rule"></a><span data-ttu-id="e636c-150">Cambiar una regla</span><span class="sxs-lookup"><span data-stu-id="e636c-150">Change a rule</span></span>
<span data-ttu-id="e636c-151">regla de hello toochange creada anteriormente tooallow el tráfico entrante desde hello **Internet** Hola únicamente, completar pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-151">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-152">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-152">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e636c-153">Hola **configuración** , haga clic en regla Hola creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e636c-153">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="e636c-154">Hola **https permitir** hoja, cambio hello **origen** propiedad tal y como se muestra a continuación y, a continuación, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e636c-154">In hello **allow-https** blade, change hello **Source** property as shown below, and then click **Save**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure10.png)

### <a name="delete-a-rule"></a><span data-ttu-id="e636c-156">Eliminar una regla</span><span class="sxs-lookup"><span data-stu-id="e636c-156">Delete a rule</span></span>

<span data-ttu-id="e636c-157">toodelete Hola regla creada anteriormente, completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-157">toodelete hello rule created above, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-158">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-158">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e636c-159">Hola **configuración** , haga clic en regla Hola creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e636c-159">In hello **Settings** tab, click hello rule created above.</span></span>
3. <span data-ttu-id="e636c-160">Hola **https permitir** hoja, haga clic en **eliminar**y, a continuación, haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="e636c-160">In hello **allow-https** blade, click **Delete**, and then click **Yes**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure11.png)

## <a name="manage-associations"></a><span data-ttu-id="e636c-162">Administrar las asociaciones</span><span class="sxs-lookup"><span data-stu-id="e636c-162">Manage associations</span></span>
<span data-ttu-id="e636c-163">Puede asociar un NSG toosubnets y NIC.</span><span class="sxs-lookup"><span data-stu-id="e636c-163">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="e636c-164">También puede desasociar un NSG de cualquier recurso al que está asociado.</span><span class="sxs-lookup"><span data-stu-id="e636c-164">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="e636c-165">Asociar una NIC de NSG tooa</span><span class="sxs-lookup"><span data-stu-id="e636c-165">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="e636c-166">Hola tooassociate **front-end de NSG** NSG toohello **TestNICWeb1** NIC, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-166">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-167">De hello **grupos de seguridad de red** hoja o hello **recursos** hoja mostrado anteriormente, haga clic en **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-167">From hello **Network security groups** blade, or hello **Resources** blade shown above, click **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e636c-168">Hola **configuración** , haga clic en **interfaces de red** > **asociar** > **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="e636c-168">In hello **Settings** tab, click **Network interfaces** > **Associate** > **TestNICWeb1**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure12.png)

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="e636c-170">Desasociar un NSG de una NIC</span><span class="sxs-lookup"><span data-stu-id="e636c-170">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="e636c-171">Hola toodissociate **front-end de NSG** NSG de hello **TestNICWeb1** NIC, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-171">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-172">En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestNICWeb1**.</span><span class="sxs-lookup"><span data-stu-id="e636c-172">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestNICWeb1**.</span></span>

2. <span data-ttu-id="e636c-173">Hola **TestNICWeb1** hoja, haga clic en **cambiar la seguridad...**   >  **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="e636c-173">In hello **TestNICWeb1** blade, click **Change security...** > **None**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure13.png)

> [!NOTE]
> <span data-ttu-id="e636c-175">También puede utilizar este tooany NIC de hoja tooassociate Hola existente NSG.</span><span class="sxs-lookup"><span data-stu-id="e636c-175">You can also use this blade tooassociate hello NIC tooany existing NSG.</span></span>
>

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="e636c-176">Desasociar un NSG de una subred</span><span class="sxs-lookup"><span data-stu-id="e636c-176">Dissociate an NSG from a subnet</span></span>

<span data-ttu-id="e636c-177">Hola toodissociate **front-end de NSG** NSG de hello **front-end** subred, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-177">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-178">En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e636c-178">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>

2. <span data-ttu-id="e636c-179">Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **Ninguno**.</span><span class="sxs-lookup"><span data-stu-id="e636c-179">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **None**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure14.png)

3. <span data-ttu-id="e636c-181">Hola **front-end** hoja, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e636c-181">In hello **FrontEnd** blade, click **Save**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure15.png)

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="e636c-183">Asociar una subred de tooa NSG</span><span class="sxs-lookup"><span data-stu-id="e636c-183">Associate an NSG tooa subnet</span></span>

<span data-ttu-id="e636c-184">Hola tooassociate **front-end de NSG** NSG toohello **FronEnd** subred nuevo, completa Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="e636c-184">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="e636c-185">En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="e636c-185">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **TestVNet**.</span></span>
2. <span data-ttu-id="e636c-186">Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-186">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
3. <span data-ttu-id="e636c-187">Hola **front-end** hoja, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="e636c-187">In hello **FrontEnd** blade, click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="e636c-188">También puede asociar una subred de tooa NSG de thh NSG **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="e636c-188">You can also associate an NSG tooa subnet from thh NSG's **Settings** blade.</span></span>
>

## <a name="delete-an-nsg"></a><span data-ttu-id="e636c-189">Eliminación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="e636c-189">Delete an NSG</span></span>
<span data-ttu-id="e636c-190">Sólo se puede eliminar un NSG si no tiene asociados recursos tooany.</span><span class="sxs-lookup"><span data-stu-id="e636c-190">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="e636c-191">toodelete un NSG, Hola completa pasos:.</span><span class="sxs-lookup"><span data-stu-id="e636c-191">toodelete an NSG, complete hello following steps:.</span></span>

1. <span data-ttu-id="e636c-192">En el portal de Azure hello, haga clic en **grupos de recursos >** > **RG-NSG** > **...**   >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="e636c-192">From hello Azure portal, click **Resource groups >** > **RG-NSG** > **...** > **NSG-FrontEnd**.</span></span>
2. <span data-ttu-id="e636c-193">Hola **configuración** hoja, haga clic en **interfaces de red**.</span><span class="sxs-lookup"><span data-stu-id="e636c-193">In hello **Settings** blade, click **Network interfaces**.</span></span>
3. <span data-ttu-id="e636c-194">Si no hay ninguna NIC aparece, haga clic en hello NIC y siga el paso 2 en [desasociar un NSG de una NIC](#Dissociate-an-NSG-from-a-NIC).</span><span class="sxs-lookup"><span data-stu-id="e636c-194">If there are any NICs listed, click hello NIC, and follow step 2 in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC).</span></span>
4. <span data-ttu-id="e636c-195">Repita el paso 3 para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="e636c-195">Repeat step 3 for each NIC.</span></span>
5. <span data-ttu-id="e636c-196">Hola **configuración** hoja, haga clic en **subredes**.</span><span class="sxs-lookup"><span data-stu-id="e636c-196">In hello **Settings** blade, click **Subnets**.</span></span>
6. <span data-ttu-id="e636c-197">Si no hay ninguna subred que aparece, haga clic en la subred de Hola y siga los pasos 2 y 3 en [desasociar un NSG de subred](#Dissociate-an-NSG-from-a-subnet).</span><span class="sxs-lookup"><span data-stu-id="e636c-197">If there are any subnets listed, click hello subnet and follow steps 2 and 3 in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet).</span></span>
7. <span data-ttu-id="e636c-198">Se desplaza izquierdo toohello **front-end de NSG** hoja, a continuación, haga clic en **eliminar** > **Sí**.</span><span class="sxs-lookup"><span data-stu-id="e636c-198">Scrolls left toohello **NSG-FrontEnd** blade, then click **Delete** > **Yes**.</span></span>

    ![Portal de Azure - NSG](./media/virtual-network-manage-nsg-arm-portal/figure16.png)

## <a name="next-steps"></a><span data-ttu-id="e636c-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e636c-200">Next steps</span></span>
* <span data-ttu-id="e636c-201">[Habilite el registro](virtual-network-nsg-manage-log.md) para los NSG.</span><span class="sxs-lookup"><span data-stu-id="e636c-201">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>
