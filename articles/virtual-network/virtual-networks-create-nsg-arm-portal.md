---
title: grupos de seguridad de red aaaManage - portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage grupos de seguridad de red mediante Hola portal de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: faee5ac8-f4c4-4f97-ade5-197a37aad496
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 53fb29e60cbc2a535f6cf03e430d9e703e97b216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-portal"></a><span data-ttu-id="44ba8-103">Administrar grupos de seguridad de red mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="44ba8-103">Manage network security groups using hello Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="44ba8-104">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="44ba8-104">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="44ba8-105">También puede [crear NSG en el modelo de implementación clásica de hello](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="44ba8-105">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="44ba8-106">ejemplo de Hola PowerShell comandos siguientes esperan un entorno simple ya creado se basa en escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="44ba8-106">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="44ba8-107">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de hello implementando [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), haga clic en **implementar tooAzure**, reemplace los valores de parámetros predeterminados de Hola Si fuera necesario y siga las instrucciones de hello en Hola portal.</span><span class="sxs-lookup"><span data-stu-id="44ba8-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span> <span data-ttu-id="44ba8-108">Hola los pasos a continuación use **NSG RG** como nombre de Hola de plantilla de Hola de grupo de recursos de Hola se implementó en.</span><span class="sxs-lookup"><span data-stu-id="44ba8-108">hello steps below use **RG-NSG** as hello name of hello resource group hello template was deployed to.</span></span>

## <a name="create-hello-nsg-frontend-nsg"></a><span data-ttu-id="44ba8-109">Crear hello front-end de NSG NSG</span><span class="sxs-lookup"><span data-stu-id="44ba8-109">Create hello NSG-FrontEnd NSG</span></span>
<span data-ttu-id="44ba8-110">Hola toocreate **front-end de NSG** NSG a como se muestra en el escenario de hello anterior, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="44ba8-110">toocreate hello **NSG-FrontEnd** NSG as shown in hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="44ba8-111">Desde un explorador, navegue toohttp://portal.azure.com y, si es necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="44ba8-111">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="44ba8-112">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="44ba8-114">Hola **grupos de seguridad de red** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-114">In hello **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="44ba8-116">Hola **crear grupo de seguridad de red** hoja, crear un NSG denominado *front-end de NSG* en hello *RG-NSG* grupo de recursos y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-116">In hello **Create network security group** blade, create an NSG named *NSG-FrontEnd* in hello *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="44ba8-118">Creación de reglas en un grupo de seguridad de red existente</span><span class="sxs-lookup"><span data-stu-id="44ba8-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="44ba8-119">reglas de toocreate en un NSG existente de hello portal de Azure, siga Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="44ba8-119">toocreate rules in an existing NSG from hello Azure portal, follow hello steps below.</span></span>

1. <span data-ttu-id="44ba8-120">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="44ba8-121">En la lista de Hola de NSG, haga clic en **front-end de NSG** > **reglas de seguridad de entrada**</span><span class="sxs-lookup"><span data-stu-id="44ba8-121">In hello list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal de Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="44ba8-123">En la lista de Hola de **reglas de seguridad de entrada**, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-123">In hello list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal de Azure - Agregar regla](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="44ba8-125">Hola **Agregar regla de seguridad de entrada** hoja, crear una regla denominada *regla web* con prioridad de *200* permitir el acceso a través de *TCP* tooport *80* tooany VM desde cualquier origen y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-125">In hello **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* tooport *80* tooany VM from any source, and then click **OK**.</span></span> <span data-ttu-id="44ba8-126">Observe que la mayoría de estas configuraciones son ya valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="44ba8-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal de Azure - Configuración de la regla](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="44ba8-128">Después de unos segundos se verá la nueva regla de Hola Hola NSG.</span><span class="sxs-lookup"><span data-stu-id="44ba8-128">After a few seconds you will see hello new rule in hello NSG.</span></span>
   
    ![Portal de Azure - Nueva regla](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="44ba8-130">Repita los pasos too6 toocreate una regla de entrada denominada *rdp-rule* con una prioridad de *250* permitir el acceso a través de *TCP* tooport *3389* tooany máquina virtual desde cualquier origen.</span><span class="sxs-lookup"><span data-stu-id="44ba8-130">Repeat steps  too6 toocreate an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* tooport *3389* tooany VM from any source.</span></span>

## <a name="associate-hello-nsg-toohello-frontend-subnet"></a><span data-ttu-id="44ba8-131">Asociar la subred de front-end de hello NSG toohello</span><span class="sxs-lookup"><span data-stu-id="44ba8-131">Associate hello NSG toohello FrontEnd subnet</span></span>
1. <span data-ttu-id="44ba8-132">Haga clic en **Examinar >** > **Grupos de recursos** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="44ba8-133">Hola **RG-NSG** hoja, haga clic en **...**   >  **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-133">In hello **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal de Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="44ba8-135">Hola **configuración** hoja, haga clic en **subredes** > **front-end** > **grupo de seguridad de red**  >  **NSG-front-end**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-135">In hello **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="44ba8-137">Hola **front-end** hoja, haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="44ba8-137">In hello **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-hello-nsg-backend-nsg"></a><span data-ttu-id="44ba8-139">Crear hello NSG de back-end de NSG</span><span class="sxs-lookup"><span data-stu-id="44ba8-139">Create hello NSG-BackEnd NSG</span></span>
<span data-ttu-id="44ba8-140">Hola toocreate **back-end de NSG** NSG y asociarlo toohello **back-end** subred, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="44ba8-140">toocreate hello **NSG-BackEnd** NSG and associate it toohello **BackEnd** subnet, follow hello steps below.</span></span>

1. <span data-ttu-id="44ba8-141">Hola Repita los pasos de [crear Hola front-end de NSG NSG](#Create-the-NSG-FrontEnd-NSG) toocreate un NSG denominado *NSG-back-end*</span><span class="sxs-lookup"><span data-stu-id="44ba8-141">Repeat hello steps in [Create hello NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) toocreate an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="44ba8-142">Hola Repita los pasos de [crear reglas en un NSG existente](#Create-rules-in-an-existing-NSG) toocreate hello **entrada** reglas de hello tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="44ba8-142">Repeat hello steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) toocreate hello **inbound** rules in hello table below.</span></span>
   
   | <span data-ttu-id="44ba8-143">Regla de entrada</span><span class="sxs-lookup"><span data-stu-id="44ba8-143">Inbound rule</span></span> | <span data-ttu-id="44ba8-144">Regla de salida</span><span class="sxs-lookup"><span data-stu-id="44ba8-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal de Azure - Regla de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal de Azure - Regla de salida](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="44ba8-147">Hola Repita los pasos de [asociar la subred de front-end de hello NSG toohello](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **back-end de NSG** NSG toohello **back-end** subred.</span><span class="sxs-lookup"><span data-stu-id="44ba8-147">Repeat hello steps in [Associate hello NSG toohello FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) tooassociate hello **NSG-Backend** NSG toohello **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44ba8-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="44ba8-148">Next Steps</span></span>
* <span data-ttu-id="44ba8-149">Obtenga información acerca de cómo demasiado[administrar NSG existentes](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="44ba8-149">Learn how too[manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="44ba8-150">[Habilite el registro](virtual-network-nsg-manage-log.md) para los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="44ba8-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

