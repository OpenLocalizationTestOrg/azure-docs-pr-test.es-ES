---
title: "equilibrador de carga de aaaCreate una conexión a Internet con IPv6 - CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un Internet orientados al equilibrador de carga con IPv6 en el Administrador de recursos de Azure en Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, Azure Load Balancer, pila doble, dirección ip pública, ipv6 nativo, móvil, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="f1ec2-104">Crear una red orientada hacia el equilibrador de carga con IPv6 en Azure Resource Manager mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f1ec2-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1ec2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1ec2-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="f1ec2-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f1ec2-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="f1ec2-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="f1ec2-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="f1ec2-108">Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP)</span><span class="sxs-lookup"><span data-stu-id="f1ec2-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="f1ec2-109">equilibrador de carga de Hello proporciona alta disponibilidad mediante la distribución de tráfico entrante entre instancias de servicio de estado de servicios en la nube o máquinas virtuales en un conjunto de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="f1ec2-110">Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="f1ec2-111">Escenario de implementación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f1ec2-111">Example deployment scenario</span></span>

<span data-ttu-id="f1ec2-112">Hello siguiente diagrama ilustra Hola solución equilibrio de carga que se implementarán mediante la plantilla de ejemplo de Hola se describe en este artículo.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="f1ec2-114">En este escenario, creará hello Azure recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="f1ec2-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="f1ec2-115">dos máquinas virtuales (VM)</span><span class="sxs-lookup"><span data-stu-id="f1ec2-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="f1ec2-116">una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas</span><span class="sxs-lookup"><span data-stu-id="f1ec2-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="f1ec2-117">un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="f1ec2-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="f1ec2-118">un conjunto de disponibilidad toothat contiene máquinas virtuales de hello dos</span><span class="sxs-lookup"><span data-stu-id="f1ec2-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="f1ec2-119">dos equilibrio reglas toomap Hola VIP toohello privados extremos públicos de carga</span><span class="sxs-lookup"><span data-stu-id="f1ec2-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="f1ec2-120">Implementar soluciones de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f1ec2-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="f1ec2-121">Hola pasos muestra cómo toocreate una conexión a Internet cargar equilibrador con Azure Resource Manager CLI.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="f1ec2-122">Con el Administrador de recursos de Azure, cada recurso se crea y configura de forma individual y, a continuación, reunir toocreate un recurso.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="f1ec2-123">toodeploy un equilibrador de carga, se crea y configura Hola siguientes objetos:</span><span class="sxs-lookup"><span data-stu-id="f1ec2-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="f1ec2-124">Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="f1ec2-125">Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="f1ec2-126">Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="f1ec2-127">Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="f1ec2-128">Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="f1ec2-129">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f1ec2-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="f1ec2-130">Configurar la toouse de entorno de CLI Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1ec2-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="f1ec2-131">En este ejemplo, se está ejecutando herramientas CLI de hello en una ventana de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="f1ec2-132">No estamos utilizando cmdlets de PowerShell de Azure de hello, sin embargo, los usamos capacidades tooimprove legibilidad y reutilización de secuencias de comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="f1ec2-133">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f1ec2-134">Ejecute hello **configuración azure modo** modo de comando tooswitch tooResource Manager.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f1ec2-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f1ec2-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f1ec2-136">Inicie sesión en tooAzure y obtener una lista de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="f1ec2-137">Escriba sus credenciales de Azure cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="f1ec2-138">Seleccionar suscripción Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="f1ec2-139">Tome nota del identificador de la suscripción de hello para el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="f1ec2-140">Configurar variables de PowerShell para su uso con los comandos de CLI de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="f1ec2-141">Creación de un grupo de recursos, un equilibrador de carga, una red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="f1ec2-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="f1ec2-142">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f1ec2-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="f1ec2-143">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f1ec2-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="f1ec2-144">Cree una red virtual (VNet)</span><span class="sxs-lookup"><span data-stu-id="f1ec2-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="f1ec2-145">Cree dos subredes en esta red virtual</span><span class="sxs-lookup"><span data-stu-id="f1ec2-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="f1ec2-146">Crear direcciones IP públicas para el grupo de servidores front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="f1ec2-147">Establecer las variables de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="f1ec2-148">Crear un público Hola front-end IP grupo de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f1ec2-149">equilibrador de carga de Hello usa la etiqueta de Hola de dominio de la dirección IP pública de hello como su FQDN.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="f1ec2-150">Este un cambio de implementación clásico, que utiliza el nombre de servicio de nube de hello como Hola FQDN del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="f1ec2-151">En este ejemplo, hello FQDN es *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="f1ec2-152">Creación de grupos de servidores front-end y back-end</span><span class="sxs-lookup"><span data-stu-id="f1ec2-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="f1ec2-153">Este ejemplo crea el grupo IP front-end Hola que recibe el tráfico de red entrante de hello en el equilibrador de carga de Hola y grupo de direcciones IP de back-end de Hola donde grupo front-end de hello envía tráfico de red con equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="f1ec2-154">Establecer las variables de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="f1ec2-155">Cree un grupo IP front-end asociar IP pública Hola creado en el paso anterior de Hola y equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="f1ec2-156">Crear reglas de carga Equilibrada, las reglas NAT y sondeo Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="f1ec2-157">Este ejemplo crea Hola siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="f1ec2-157">This example creates hello following items:</span></span>

* <span data-ttu-id="f1ec2-158">un toocheck de regla de sondeo para el puerto de la conectividad tooTCP 80</span><span class="sxs-lookup"><span data-stu-id="f1ec2-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="f1ec2-159">un dispositivo NAT regla tootranslate todo el tráfico entrante en el puerto 3389 tooport 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f1ec2-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="f1ec2-160">un dispositivo NAT regla tootranslate todo el tráfico entrante en el puerto 3391 tooport 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f1ec2-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="f1ec2-161">un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="f1ec2-162"><sup>1</sup> reglas NAT son la instancia de máquina virtual específica de tooa asociado detrás de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="f1ec2-163">máquina virtual específica de toohello y el puerto asociado con la regla NAT de hello, se envía tráfico de red de Hola que llegan en el puerto 3389.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="f1ec2-164">Debe especificar un protocolo (UDP o TCP) para una regla NAT.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="f1ec2-165">Ambos protocolos no se pueden asignar toohello mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="f1ec2-166">Establecer las variables de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="f1ec2-167">Crear el sondeo de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-167">Create hello probe</span></span>

    <span data-ttu-id="f1ec2-168">Hello en el ejemplo siguiente se crea un sondeo TCP comprueba para el puerto TCP de tooback final conectividad 80 cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="f1ec2-169">Marcará los recursos de back-end de hello disponible después de dos errores consecutivos.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="f1ec2-170">Crear reglas NAT de entrada que permiten las conexiones RDP toohello recursos de back-end</span><span class="sxs-lookup"><span data-stu-id="f1ec2-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="f1ec2-171">Crear reglas que envían el tráfico de puertos de back-end de toodifferent dependiendo de qué solicitud de Hola de front-end que recibió de un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f1ec2-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="f1ec2-172">Compruebe la configuración</span><span class="sxs-lookup"><span data-stu-id="f1ec2-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="f1ec2-173">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f1ec2-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="f1ec2-174">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="f1ec2-174">Create NICs</span></span>

<span data-ttu-id="f1ec2-175">Crear NIC y asociarlos tooNAT reglas, reglas de equilibrador de carga y sondeos.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="f1ec2-176">Establecer las variables de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="f1ec2-177">Cree una NIC para cada back-end y agregue una configuración de IPv6</span><span class="sxs-lookup"><span data-stu-id="f1ec2-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="f1ec2-178">Crear recursos de máquina virtual de back-end de Hola y asociar cada NIC</span><span class="sxs-lookup"><span data-stu-id="f1ec2-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="f1ec2-179">toocreate las máquinas virtuales, debe tener una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="f1ec2-180">Equilibrio de carga, las máquinas virtuales de hello necesitan a toobe miembros de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="f1ec2-181">Para obtener más información sobre cómo crear máquinas virtuales, consulte [Creación de una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f1ec2-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="f1ec2-182">Establecer las variables de PowerShell de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="f1ec2-183">Este ejemplo utiliza Hola username y password para máquinas virtuales de hello en texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="f1ec2-184">Adecuada se debe tener cuidado al utilizando credenciales de hello claro.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="f1ec2-185">Para obtener un método más seguro de controlar las credenciales en PowerShell, vea hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="f1ec2-186">Crear conjunto de cuenta y la disponibilidad de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="f1ec2-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="f1ec2-187">Puede usar una cuenta de almacenamiento existente al crear hello las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="f1ec2-188">Hola siguiente comando crea una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="f1ec2-189">A continuación, crear conjunto de disponibilidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="f1ec2-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="f1ec2-190">Crear máquinas virtuales de hello con NIC Hola asociado</span><span class="sxs-lookup"><span data-stu-id="f1ec2-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="f1ec2-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f1ec2-191">Next steps</span></span>

[<span data-ttu-id="f1ec2-192">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="f1ec2-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="f1ec2-193">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f1ec2-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f1ec2-194">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="f1ec2-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
