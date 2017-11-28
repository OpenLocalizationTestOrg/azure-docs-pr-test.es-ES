---
title: "Creación de grupos de seguridad de red: CLI de Azure 1.0 | Microsoft Docs"
description: Aprenda a crear e implementar grupos de seguridad de red mediante la CLI de Azure 1.0.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="c4d93-103">Creación de grupos de seguridad de red con la CLI de Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="c4d93-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c4d93-104">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="c4d93-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="c4d93-105">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="c4d93-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="c4d93-106">[CLI de Azure 1.0](#how-to-create-the-nsg-for-the-front-end-subnet): la CLI para los modelos de implementación clásico y de Resource Manager (este artículo)</span><span class="sxs-lookup"><span data-stu-id="c4d93-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c4d93-107">[CLI de Azure 2.0](virtual-networks-create-nsg-arm-cli.md): la CLI de última generación para el modelo de implementación de administración de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c4d93-108">Este artículo trata sobre el modelo de implementación del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="c4d93-109">También puede [crear grupos de seguridad de red en el modelo de implementación clásica](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c4d93-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c4d93-110">En los siguientes comandos de CLI de Azure de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="c4d93-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="c4d93-111">Creación del grupo de seguridad de red para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="c4d93-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="c4d93-112">Para crear un grupo de seguridad de red denominado *NSG-FrontEnd* según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="c4d93-113">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c4d93-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c4d93-114">Ejecuta el comando **azure config mode** para cambiar al modo de Administrador de recursos, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="c4d93-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="c4d93-115">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="c4d93-116">Ejecute el comando **azure network nsg create** para crear un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c4d93-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="c4d93-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="c4d93-118">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="c4d93-118">Parameters:</span></span>
   
   * <span data-ttu-id="c4d93-119">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="c4d93-120">Nombre del grupo de recursos donde se creará el grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="c4d93-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="c4d93-121">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="c4d93-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="c4d93-122">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-122">**-l (or --location)**.</span></span> <span data-ttu-id="c4d93-123">Región de Azure donde se creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="c4d93-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="c4d93-124">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="c4d93-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="c4d93-125">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-125">**-n (or --name)**.</span></span> <span data-ttu-id="c4d93-126">Nombre del nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c4d93-126">Name for the new NSG.</span></span> <span data-ttu-id="c4d93-127">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c4d93-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="c4d93-128">Ejecute el comando **azure network nsg rule create** para crear una regla que permita el acceso al puerto 3389 (RDP) desde Internet.</span><span class="sxs-lookup"><span data-stu-id="c4d93-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="c4d93-129">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="c4d93-130">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="c4d93-130">Parameters:</span></span>
   
   * <span data-ttu-id="c4d93-131">**- a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="c4d93-132">Nombre del grupo de seguridad de red en el que se creará la regla.</span><span class="sxs-lookup"><span data-stu-id="c4d93-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="c4d93-133">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c4d93-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="c4d93-134">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-134">**-n (or --name)**.</span></span> <span data-ttu-id="c4d93-135">Nombre de la nueva regla.</span><span class="sxs-lookup"><span data-stu-id="c4d93-135">Name for the new rule.</span></span> <span data-ttu-id="c4d93-136">En este escenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="c4d93-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="c4d93-137">**-c (o--access)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-137">**-c (or --access)**.</span></span> <span data-ttu-id="c4d93-138">Nivel de acceso de la regla (Denegar o Permitir).</span><span class="sxs-lookup"><span data-stu-id="c4d93-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="c4d93-139">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="c4d93-140">Protocolo (Tcp, Udp o *) para la regla.</span><span class="sxs-lookup"><span data-stu-id="c4d93-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="c4d93-141">**- r (o --direction)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-141">**-r (or --direction)**.</span></span> <span data-ttu-id="c4d93-142">Dirección de conexión (Entrante o Saliente).</span><span class="sxs-lookup"><span data-stu-id="c4d93-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="c4d93-143">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-143">**-y (or --priority)**.</span></span> <span data-ttu-id="c4d93-144">Prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="c4d93-144">Priority for the rule.</span></span>
   * <span data-ttu-id="c4d93-145">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="c4d93-146">Prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="c4d93-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c4d93-147">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="c4d93-148">Puerto de origen, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-148">Source port, or port range.</span></span>
   * <span data-ttu-id="c4d93-149">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="c4d93-150">Prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="c4d93-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c4d93-151">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="c4d93-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="c4d93-152">Puerto de destino, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="c4d93-153">Ejecute el comando **azure network nsg rule create** para crear una regla que permita el acceso al puerto 80 (HTTP) desde Internet.</span><span class="sxs-lookup"><span data-stu-id="c4d93-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="c4d93-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="c4d93-155">Ejecute el comando **azure network vnet subnet set** para vincular el grupo de seguridad de red a la subred front-end.</span><span class="sxs-lookup"><span data-stu-id="c4d93-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="c4d93-156">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="c4d93-157">Creación del grupo de seguridad de red para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="c4d93-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="c4d93-158">Para crear un grupo de seguridad de red denominado *NSG-BackEnd* según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c4d93-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="c4d93-159">Ejecute el comando **azure network nsg create** para crear un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c4d93-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="c4d93-160">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="c4d93-161">Ejecute el comando **azure network nsg rule create** para crear una regla que permita el acceso al puerto 1433 (SQL) desde la subred front-end.</span><span class="sxs-lookup"><span data-stu-id="c4d93-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="c4d93-162">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="c4d93-163">Ejecute el comando **azure network nsg rule create** para crear una regla que deniegue el acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="c4d93-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="c4d93-164">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="c4d93-165">Ejecute el comando **azure network vnet subnet set** para vincular el grupo de seguridad de red a la subred back-end.</span><span class="sxs-lookup"><span data-stu-id="c4d93-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="c4d93-166">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="c4d93-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

