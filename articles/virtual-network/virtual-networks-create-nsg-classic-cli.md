---
title: "aaaHow toocreate NSG en modo clásico mediante Hola CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate e implementar los NSG en el modo clásico mediante Hola CLI de Azure"
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="eb0f0-103">Cómo toocreate NSG (clásicos) en Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="eb0f0-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="eb0f0-104">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="eb0f0-105">También puede [crear NSG en el modelo de implementación del Administrador de recursos de hello](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="eb0f0-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="eb0f0-106">comandos de CLI de Azure de ejemplo de Hola a continuación esperan un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="eb0f0-107">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola por [crear una red virtual](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="eb0f0-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="eb0f0-108">¿Cómo toocreate Hola NSG para la subred de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="eb0f0-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="eb0f0-109">toocreate un NSG denominado denominado **front-end de NSG** en función de escenario Hola anterior, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="eb0f0-110">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="eb0f0-111">Ejecute hello  **`azure config mode`**  tooswitch tooclassic modo de comandos, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="eb0f0-112">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="eb0f0-113">Ejecute hello  **`azure network nsg create`**  comando toocreate un NSG.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="eb0f0-114">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="eb0f0-115">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-115">Parameters:</span></span>
   
   * <span data-ttu-id="eb0f0-116">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-116">**-l (or --location)**.</span></span> <span data-ttu-id="eb0f0-117">Región de Azure donde hello nuevo NSG se creará.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="eb0f0-118">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="eb0f0-119">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-119">**-n (or --name)**.</span></span> <span data-ttu-id="eb0f0-120">Nombre de hello nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-120">Name for hello new NSG.</span></span> <span data-ttu-id="eb0f0-121">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="eb0f0-122">Ejecute hello  **`azure network nsg rule create`**  comando toocreate una regla que permita acceso tooport 3389 (RDP) de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="eb0f0-123">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="eb0f0-124">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-124">Parameters:</span></span>
   
   * <span data-ttu-id="eb0f0-125">**- a (o --nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="eb0f0-126">Nombre del NSG de hello en qué Hola se creará la regla.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="eb0f0-127">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="eb0f0-128">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-128">**-n (or --name)**.</span></span> <span data-ttu-id="eb0f0-129">Nombre de nueva regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-129">Name for hello new rule.</span></span> <span data-ttu-id="eb0f0-130">En este escenario, *rdp-rule*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="eb0f0-131">**-c (o --action)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-131">**-c (or --action)**.</span></span> <span data-ttu-id="eb0f0-132">Nivel de acceso para la regla de hello (denegar o permitir).</span><span class="sxs-lookup"><span data-stu-id="eb0f0-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="eb0f0-133">**-p (o --protocol)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="eb0f0-134">Protocolo (Tcp, Udp o *) para la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="eb0f0-135">**-r (o --type)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-135">**-r (or --type)**.</span></span> <span data-ttu-id="eb0f0-136">Dirección de conexión (Entrante o Saliente).</span><span class="sxs-lookup"><span data-stu-id="eb0f0-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="eb0f0-137">**-y (o --priority)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-137">**-y (or --priority)**.</span></span> <span data-ttu-id="eb0f0-138">Prioridad de la regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="eb0f0-139">**-f (o --source-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="eb0f0-140">Prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="eb0f0-141">**-o (o --source-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="eb0f0-142">Puerto de origen, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-142">Source port, or port range.</span></span>
   * <span data-ttu-id="eb0f0-143">**-e (o --destination-address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="eb0f0-144">Prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="eb0f0-145">**-u (o --destination-port-range)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="eb0f0-146">Puerto de destino, o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="eb0f0-147">Ejecute hello  **`azure network nsg rule create`**  comando toocreate una regla que permita acceso tooport 80 (HTTP) de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="eb0f0-148">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="eb0f0-149">Ejecute hello  **`azure network nsg subnet add`**  subred de front-end de comando toolink hello NSG toohello.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="eb0f0-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="eb0f0-151">Cómo toocreate hello NSG para volver Hola finalizar subred</span><span class="sxs-lookup"><span data-stu-id="eb0f0-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="eb0f0-152">toocreate un NSG denominado denominado *back-end de NSG* en función de escenario Hola anterior, siga estos pasos Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="eb0f0-153">Ejecute hello  **`azure network nsg create`**  comando toocreate un NSG.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="eb0f0-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="eb0f0-155">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-155">Parameters:</span></span>
   
   * <span data-ttu-id="eb0f0-156">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-156">**-l (or --location)**.</span></span> <span data-ttu-id="eb0f0-157">Región de Azure donde hello nuevo NSG se creará.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="eb0f0-158">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="eb0f0-159">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-159">**-n (or --name)**.</span></span> <span data-ttu-id="eb0f0-160">Nombre de hello nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-160">Name for hello new NSG.</span></span> <span data-ttu-id="eb0f0-161">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="eb0f0-162">Ejecute hello  **`azure network nsg rule create`**  comando toocreate una regla que permita acceso tooport 1433 (SQL) de la subred de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="eb0f0-163">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="eb0f0-164">Ejecute hello  **`azure network nsg rule create`**  comando toocreate una regla que deniegue toohello de acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="eb0f0-165">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="eb0f0-166">Ejecute hello  **`azure network nsg subnet add`**  comando toolink hello NSG toohello volver finalizar subred.</span><span class="sxs-lookup"><span data-stu-id="eb0f0-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="eb0f0-167">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="eb0f0-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

