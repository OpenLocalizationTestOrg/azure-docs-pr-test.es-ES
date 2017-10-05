---
title: "Creación de grupos de seguridad de red (Azure Portal) | Microsoft Docs"
description: "Obtenga información sobre cómo crear e implementar grupos de seguridad de red mediante Azure Portal."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 5bc8fc2e-1e81-40e2-8231-0484cd5605cb
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 865032f350735d35668bb199ccf1ef3f0fae81de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-portal"></a><span data-ttu-id="8905f-103">Creación de grupos de seguridad de red con Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8905f-103">Create network security groups using the Azure portal</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8905f-104">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8905f-104">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="8905f-105">También puede [crear grupos de seguridad de red en el modelo de implementación clásica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="8905f-105">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="8905f-106">En los siguientes comandos de PowerShell de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="8905f-106">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="8905f-107">Si desea ejecutar los comandos tal y como aparecen en este documento, cree primero el entorno de prueba mediante la implementación de [esta plantilla](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), haga clic en **Implementar en Azure**, reemplace los valores de parámetro predeterminados si es necesario y siga las instrucciones del portal.</span><span class="sxs-lookup"><span data-stu-id="8905f-107">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span> <span data-ttu-id="8905f-108">En los pasos siguientes se emplea **RG-GSN** como nombre del grupo de recursos en el que se implementó la plantilla.</span><span class="sxs-lookup"><span data-stu-id="8905f-108">The steps below use **RG-NSG** as the name of the resource group the template was deployed to.</span></span>

## <a name="create-the-nsg-frontend-nsg"></a><span data-ttu-id="8905f-109">Creación del grupo de seguridad de red NSG-FrontEnd</span><span class="sxs-lookup"><span data-stu-id="8905f-109">Create the NSG-FrontEnd NSG</span></span>
<span data-ttu-id="8905f-110">Para crear el grupo de seguridad de red **NSG-FrontEnd** según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="8905f-110">To create the **NSG-FrontEnd** NSG as shown in the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="8905f-111">Desde un explorador, vaya a http://portal.azure.com y, si fuera necesario, inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8905f-111">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="8905f-112">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="8905f-112">Click **Browse >** > **Network Security Groups**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure11.png)
3. <span data-ttu-id="8905f-114">En la hoja **Grupos de seguridad de red**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8905f-114">In the **Network security groups** blade, click **Add**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure12.png)
4. <span data-ttu-id="8905f-116">En la hoja **Crear grupo de seguridad de red**, cree un grupo de seguridad de red denominado *NSG-FrontEnd* en el grupo de recursos *RG-NSG* y, después, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="8905f-116">In the **Create network security group** blade, create an NSG named *NSG-FrontEnd* in the *RG-NSG* resource group, and then click **Create**.</span></span>
   
    ![Portal de Azure - NSG](./media/virtual-networks-create-nsg-arm-pportal/figure13.png)

## <a name="create-rules-in-an-existing-nsg"></a><span data-ttu-id="8905f-118">Creación de reglas en un grupo de seguridad de red existente</span><span class="sxs-lookup"><span data-stu-id="8905f-118">Create rules in an existing NSG</span></span>
<span data-ttu-id="8905f-119">Para crear reglas en un grupo de seguridad de red existente desde el Portal de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="8905f-119">To create rules in an existing NSG from the Azure portal, follow the steps below.</span></span>

1. <span data-ttu-id="8905f-120">Haga clic en **Examinar >** > **Grupos de seguridad de red**.</span><span class="sxs-lookup"><span data-stu-id="8905f-120">Click **Browse >** > **Network security groups**.</span></span>
2. <span data-ttu-id="8905f-121">En la lista de grupos de seguridad de red, haga clic en **NSG-FrontEnd** > **Reglas de seguridad de entrada**</span><span class="sxs-lookup"><span data-stu-id="8905f-121">In the list of NSGs, click **NSG-FrontEnd** > **Inbound security rules**</span></span>
   
    ![Portal de Azure - NSG-FrontEnd](./media/virtual-networks-create-nsg-arm-pportal/figure2.png)
3. <span data-ttu-id="8905f-123">En la lista de **Reglas de seguridad de entrada**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8905f-123">In the list of **Inbound security rules**, click **Add**.</span></span>
   
    ![Portal de Azure - Agregar regla](./media/virtual-networks-create-nsg-arm-pportal/figure3.png)
4. <span data-ttu-id="8905f-125">En la hoja **Agregar regla de seguridad de entrada**, cree una regla denominada *web-rule* con prioridad de *200* que permita el acceso a través de *TCP* al puerto *80* a cualquier VM desde cualquier origen y, luego, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8905f-125">In the **Add inbound security rule** blade, create a rule named *web-rule* with priority of *200* allowing access via *TCP* to port *80* to any VM from any source, and then click **OK**.</span></span> <span data-ttu-id="8905f-126">Observe que la mayoría de estas configuraciones son ya valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="8905f-126">Notice that most of these settings are default values already.</span></span>
   
    ![Portal de Azure - Configuración de la regla](./media/virtual-networks-create-nsg-arm-pportal/figure4.png)
5. <span data-ttu-id="8905f-128">Después de unos segundos, verá la nueva regla en el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="8905f-128">After a few seconds you will see the new rule in the NSG.</span></span>
   
    ![Portal de Azure - Nueva regla](./media/virtual-networks-create-nsg-arm-pportal/figure5.png)
6. <span data-ttu-id="8905f-130">Repita los pasos hasta el sexto para crear una regla de entrada denominada *rdp-rule* con una prioridad de *250* que permita el acceso a través de *TCP* al puerto *3389* a cualquier VM desde cualquier origen.</span><span class="sxs-lookup"><span data-stu-id="8905f-130">Repeat steps  to 6 to create an inbound rule named *rdp-rule* with a priority of *250* allowing access via *TCP* to port *3389* to any VM from any source.</span></span>

## <a name="associate-the-nsg-to-the-frontend-subnet"></a><span data-ttu-id="8905f-131">Asociación del grupo de seguridad de red a la subred FrontEnd</span><span class="sxs-lookup"><span data-stu-id="8905f-131">Associate the NSG to the FrontEnd subnet</span></span>
1. <span data-ttu-id="8905f-132">Haga clic en **Examinar >** > **Grupos de recursos** > **RG-NSG**.</span><span class="sxs-lookup"><span data-stu-id="8905f-132">Click **Browse >** > **Resource groups** > **RG-NSG**.</span></span>
2. <span data-ttu-id="8905f-133">En la hoja **RG-NSG**, haga clic en **…** > **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="8905f-133">In the **RG-NSG** blade, click **...** > **TestVNet**.</span></span>
   
    ![Portal de Azure - TestVNet](./media/virtual-networks-create-nsg-arm-pportal/figure14.png)
3. <span data-ttu-id="8905f-135">En la hoja **Configuración**, haga clic en **Subredes** > **FrontEnd** > **Grupo de seguridad de red** > **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="8905f-135">In the **Settings** blade, click **Subnets** > **FrontEnd** > **Network security group** > **NSG-FrontEnd**.</span></span>
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure15.png)
4. <span data-ttu-id="8905f-137">En la hoja **FrontEnd**, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="8905f-137">In the **FrontEnd** blade, click **Save**.</span></span>
   
    ![Portal de Azure - Configuración de la subred](./media/virtual-networks-create-nsg-arm-pportal/figure16.png)

## <a name="create-the-nsg-backend-nsg"></a><span data-ttu-id="8905f-139">Creación del grupo de seguridad de red NSG-BackEnd</span><span class="sxs-lookup"><span data-stu-id="8905f-139">Create the NSG-BackEnd NSG</span></span>
<span data-ttu-id="8905f-140">Para crear el grupo de seguridad de red **NSG-BackEnd** y asociarlo a la subred **BackEnd**, siga los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="8905f-140">To create the **NSG-BackEnd** NSG and associate it to the **BackEnd** subnet, follow the steps below.</span></span>

1. <span data-ttu-id="8905f-141">Repita los pasos que se describen en [Creación del grupo de seguridad de red NSG-FrontEnd](#Create-the-NSG-FrontEnd-NSG) para crear un NSG llamado *NSG-BackEnd*</span><span class="sxs-lookup"><span data-stu-id="8905f-141">Repeat the steps in [Create the NSG-FrontEnd NSG](#Create-the-NSG-FrontEnd-NSG) to create an NSG named *NSG-BackEnd*</span></span>
2. <span data-ttu-id="8905f-142">Repita los pasos que se describen en [Creación de reglas en un grupo de seguridad de red existente](#Create-rules-in-an-existing-NSG) para crear las reglas **de entrada** que aparecen en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="8905f-142">Repeat the steps in [Create rules in an existing NSG](#Create-rules-in-an-existing-NSG) to create the **inbound** rules in the table below.</span></span>
   
   | <span data-ttu-id="8905f-143">Regla de entrada</span><span class="sxs-lookup"><span data-stu-id="8905f-143">Inbound rule</span></span> | <span data-ttu-id="8905f-144">Regla de salida</span><span class="sxs-lookup"><span data-stu-id="8905f-144">Outbound rule</span></span> |
   | --- | --- |
   | ![Portal de Azure - Regla de entrada](./media/virtual-networks-create-nsg-arm-pportal/figure17.png) |![Portal de Azure - Regla de salida](./media/virtual-networks-create-nsg-arm-pportal/figure18.png) |
3. <span data-ttu-id="8905f-147">Repita los pasos que se describen en [Asociación del grupo de seguridad de red a la subred FrontEnd](#Associate-the-NSG-to-the-FrontEnd-subnet) para asociar el grupo de seguridad de red **NSG-Backend** a la subred **BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="8905f-147">Repeat the steps in [Associate the NSG to the FrontEnd subnet](#Associate-the-NSG-to-the-FrontEnd-subnet) to associate the **NSG-Backend** NSG to the **BackEnd** subnet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8905f-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8905f-148">Next Steps</span></span>
* <span data-ttu-id="8905f-149">Información sobre cómo [administrar grupos de seguridad de red existentes](virtual-network-manage-nsg-arm-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8905f-149">Learn how to [manage existing NSGs](virtual-network-manage-nsg-arm-portal.md)</span></span>
* <span data-ttu-id="8905f-150">[Habilite el registro](virtual-network-nsg-manage-log.md) para los grupos de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="8905f-150">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

