---
title: aaaCreate de red de grupos de seguridad - 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar grupos de seguridad de red mediante Hola 1.0 de CLI de Azure."
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
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="083b0-103">Crear grupos de seguridad mediante Azure CLI 1.0 Hola de red</span><span class="sxs-lookup"><span data-stu-id="083b0-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="083b0-104">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="083b0-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="083b0-105">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="083b0-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="083b0-106">[Azure 1.0 de CLI](#how-to-create-the-nsg-for-the-front-end-subnet) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="083b0-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="083b0-107">[Azure 2.0 CLI](virtual-networks-create-nsg-arm-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="083b0-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="083b0-108">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="083b0-109">También puede [crear NSG en el modelo de implementación clásica de hello](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="083b0-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="083b0-110">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="083b0-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="083b0-111">¿Cómo toocreate Hola NSG para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="083b0-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="083b0-112">toocreate un NSG denominado denominado *front-end de NSG* en función de escenario Hola anterior, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="083b0-113">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="083b0-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="083b0-114">Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="083b0-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="083b0-115">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="083b0-116">Ejecute hello **crear red de azure nsg** comando toocreate un NSG.</span><span class="sxs-lookup"><span data-stu-id="083b0-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="083b0-117">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="083b0-118">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="083b0-118">Parameters:</span></span>
   
   * <span data-ttu-id="083b0-119">**-g (o --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="083b0-120">Nombre del grupo de recursos de Hola donde se creará hello NSG.</span><span class="sxs-lookup"><span data-stu-id="083b0-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="083b0-121">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="083b0-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="083b0-122">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-122">**-l (or --location)**.</span></span> <span data-ttu-id="083b0-123">Región de Azure donde hello nuevo NSG se creará.</span><span class="sxs-lookup"><span data-stu-id="083b0-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="083b0-124">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="083b0-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="083b0-125">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-125">**-n (or --name)**.</span></span> <span data-ttu-id="083b0-126">Nombre de hello nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="083b0-126">Name for hello new NSG.</span></span> <span data-ttu-id="083b0-127">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="083b0-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="083b0-128">Ejecute hello **crear regla de nsg de red de azure** comando toocreate una regla que permita acceso tooport 3389 (RDP) de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="083b0-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="083b0-129">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="083b0-130">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="083b0-130">Parameters:</span></span>
   
   * <span data-ttu-id="083b0-131">**- a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="083b0-132">Nombre del NSG de hello en qué Hola se creará la regla.</span><span class="sxs-lookup"><span data-stu-id="083b0-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="083b0-133">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="083b0-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="083b0-134">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-134">**-n (or --name)**.</span></span> <span data-ttu-id="083b0-135">Nombre de nueva regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-135">Name for hello new rule.</span></span> <span data-ttu-id="083b0-136">En este escenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="083b0-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="083b0-137">**-c (o--access)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-137">**-c (or --access)**.</span></span> <span data-ttu-id="083b0-138">Nivel de acceso para la regla de hello (denegar o permitir).</span><span class="sxs-lookup"><span data-stu-id="083b0-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="083b0-139">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="083b0-140">Protocolo (Tcp, Udp o *) para la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="083b0-141">**- r (o --direction)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-141">**-r (or --direction)**.</span></span> <span data-ttu-id="083b0-142">Dirección de conexión (Entrante o Saliente).</span><span class="sxs-lookup"><span data-stu-id="083b0-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="083b0-143">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-143">**-y (or --priority)**.</span></span> <span data-ttu-id="083b0-144">Prioridad de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="083b0-145">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="083b0-146">Prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="083b0-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="083b0-147">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="083b0-148">Puerto de origen, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="083b0-148">Source port, or port range.</span></span>
   * <span data-ttu-id="083b0-149">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="083b0-150">Prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="083b0-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="083b0-151">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="083b0-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="083b0-152">Puerto de destino, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="083b0-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="083b0-153">Ejecute hello **crear regla de nsg de red de azure** comando toocreate una regla que permita acceso tooport 80 (HTTP) de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="083b0-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="083b0-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="083b0-155">Ejecute hello **conjunto de subredes de red virtual de red de azure** subred de front-end de comando toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="083b0-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="083b0-156">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
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

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="083b0-157">Cómo toocreate hello NSG para volver Hola finalizar subred</span><span class="sxs-lookup"><span data-stu-id="083b0-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="083b0-158">toocreate un NSG denominado denominado *back-end de NSG* en función de escenario Hola anterior, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="083b0-159">Ejecute hello **crear red de azure nsg** comando toocreate un NSG.</span><span class="sxs-lookup"><span data-stu-id="083b0-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="083b0-160">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
2. <span data-ttu-id="083b0-161">Ejecute hello **crear regla de nsg de red de azure** comando toocreate una regla que permita acceso tooport 1433 (SQL) de la subred de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="083b0-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="083b0-162">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="083b0-163">Ejecute hello **crear regla de nsg de red de azure** comando toocreate una regla que deniegue el acceso toohello Internet desde.</span><span class="sxs-lookup"><span data-stu-id="083b0-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="083b0-164">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="083b0-165">Ejecute hello **conjunto de subredes de red virtual de red de azure** comando toolink hello NSG toohello volver finalizar subred.</span><span class="sxs-lookup"><span data-stu-id="083b0-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="083b0-166">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="083b0-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
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

