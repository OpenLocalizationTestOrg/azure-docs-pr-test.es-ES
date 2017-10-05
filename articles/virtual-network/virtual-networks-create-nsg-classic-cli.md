---
title: "Creación de grupos de seguridad de red en el modo clásico mediante la CLI de Azure | Microsoft Docs"
description: "Aprenda a crear e implementar grupos de seguridad de red en modo clásico mediante la CLI de Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="152f2-103">Creación de grupos de seguridad de red (modo clásico) en la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="152f2-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="152f2-104">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="152f2-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="152f2-105">También puede [crear grupos de seguridad de red con el modelo de implementación del Administrador de recursos](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="152f2-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="152f2-106">En los siguientes comandos de CLI de Azure de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="152f2-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="152f2-107">Si desea ejecutar los comandos tal y como aparecen en este documento, compile primero el entorno de prueba mediante la [creación de una red virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="152f2-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="152f2-108">Creación del grupo de seguridad de red para la subred front-end</span><span class="sxs-lookup"><span data-stu-id="152f2-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="152f2-109">Para crear un grupo de seguridad de red denominado **NSG-FrontEnd** según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="152f2-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="152f2-110">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="152f2-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="152f2-111">Ejecute el comando **`azure config mode`** para cambiar al modo clásico, como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="152f2-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="152f2-112">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="152f2-113">Ejecute el comando **`azure network nsg create`** para crear un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="152f2-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="152f2-114">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="152f2-115">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="152f2-115">Parameters:</span></span>
   
   * <span data-ttu-id="152f2-116">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-116">**-l (or --location)**.</span></span> <span data-ttu-id="152f2-117">Región de Azure donde se creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="152f2-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="152f2-118">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="152f2-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="152f2-119">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-119">**-n (or --name)**.</span></span> <span data-ttu-id="152f2-120">Nombre del nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="152f2-120">Name for the new NSG.</span></span> <span data-ttu-id="152f2-121">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="152f2-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="152f2-122">Ejecute el comando **`azure network nsg rule create`** para crear una regla que permita el acceso al puerto 3389 (RDP) desde Internet.</span><span class="sxs-lookup"><span data-stu-id="152f2-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="152f2-123">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="152f2-124">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="152f2-124">Parameters:</span></span>
   
   * <span data-ttu-id="152f2-125">**- a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="152f2-126">Nombre del grupo de seguridad de red en el que se creará la regla.</span><span class="sxs-lookup"><span data-stu-id="152f2-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="152f2-127">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="152f2-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="152f2-128">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-128">**-n (or --name)**.</span></span> <span data-ttu-id="152f2-129">Nombre de la nueva regla.</span><span class="sxs-lookup"><span data-stu-id="152f2-129">Name for the new rule.</span></span> <span data-ttu-id="152f2-130">En este escenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="152f2-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="152f2-131">**-c (o --action)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-131">**-c (or --action)**.</span></span> <span data-ttu-id="152f2-132">Nivel de acceso de la regla (Denegar o Permitir).</span><span class="sxs-lookup"><span data-stu-id="152f2-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="152f2-133">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="152f2-134">Protocolo (Tcp, Udp o *) para la regla.</span><span class="sxs-lookup"><span data-stu-id="152f2-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="152f2-135">**-r (o --type)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-135">**-r (or --type)**.</span></span> <span data-ttu-id="152f2-136">Dirección de conexión (Entrante o Saliente).</span><span class="sxs-lookup"><span data-stu-id="152f2-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="152f2-137">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-137">**-y (or --priority)**.</span></span> <span data-ttu-id="152f2-138">Prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="152f2-138">Priority for the rule.</span></span>
   * <span data-ttu-id="152f2-139">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="152f2-140">Prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="152f2-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="152f2-141">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="152f2-142">Puerto de origen, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="152f2-142">Source port, or port range.</span></span>
   * <span data-ttu-id="152f2-143">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="152f2-144">Prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="152f2-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="152f2-145">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="152f2-146">Puerto de destino, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="152f2-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="152f2-147">Ejecute el comando **`azure network nsg rule create`** para crear una regla que permita el acceso al puerto 80 (HTTP) desde Internet.</span><span class="sxs-lookup"><span data-stu-id="152f2-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="152f2-148">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="152f2-149">Ejecute el comando **`azure network nsg subnet add`** para vincular el grupo de seguridad de red a la subred front-end.</span><span class="sxs-lookup"><span data-stu-id="152f2-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="152f2-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="152f2-151">Creación del grupo de seguridad de red para la subred back-end</span><span class="sxs-lookup"><span data-stu-id="152f2-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="152f2-152">Para crear un grupo de seguridad de red denominado *NSG-BackEnd* según el escenario anterior, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="152f2-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="152f2-153">Ejecute el comando **`azure network nsg create`** para crear un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="152f2-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="152f2-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="152f2-155">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="152f2-155">Parameters:</span></span>
   
   * <span data-ttu-id="152f2-156">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-156">**-l (or --location)**.</span></span> <span data-ttu-id="152f2-157">Región de Azure donde se creará la red virtual.</span><span class="sxs-lookup"><span data-stu-id="152f2-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="152f2-158">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="152f2-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="152f2-159">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="152f2-159">**-n (or --name)**.</span></span> <span data-ttu-id="152f2-160">Nombre del nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="152f2-160">Name for the new NSG.</span></span> <span data-ttu-id="152f2-161">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="152f2-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="152f2-162">Ejecute el comando **`azure network nsg rule create`** para crear una regla que permita el acceso al puerto 1433 (SQL) desde la subred front-end.</span><span class="sxs-lookup"><span data-stu-id="152f2-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="152f2-163">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="152f2-164">Ejecute el comando **`azure network nsg rule create`** para crear una regla que deniegue el acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="152f2-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="152f2-165">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="152f2-166">Ejecute el comando **`azure network nsg subnet add`** para vincular el grupo de seguridad de red a la subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="152f2-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="152f2-167">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="152f2-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

