---
title: "Creación de un equilibrador de carga con conexión a Internet con IPv6: CLI de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo crear un equilibrador de carga orientado a Internet con IPv6 en Azure Resource Manager con la CLI de Azure"
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="a54c4-104">Creación de un equilibrador de carga orientado a Internet con IPv6 en Azure Resource Manager con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a54c4-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a54c4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="a54c4-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a54c4-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="a54c4-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="a54c4-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="a54c4-108">Azure Load Balancer es un equilibrador de carga de nivel 4 (TCP y UDP)</span><span class="sxs-lookup"><span data-stu-id="a54c4-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="a54c4-109">que distribuye proporcionando una alta disponibilidad el tráfico entrante entre las instancias de servicio correctas de los servicios en la nube o las máquinas virtuales de un conjunto de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="a54c4-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="a54c4-110">Azure Load Balancer también pueden presentar prestar servicios en varios puertos, varias direcciones IP o ambos.</span><span class="sxs-lookup"><span data-stu-id="a54c4-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="a54c4-111">Escenario de implementación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a54c4-111">Example deployment scenario</span></span>

<span data-ttu-id="a54c4-112">En el siguiente diagrama se ilustra la solución de equilibrio de carga que se implementa mediante la plantilla de ejemplo descrita en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a54c4-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Escenario del equilibrador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="a54c4-114">En este escenario creará los siguientes recursos de Azure:</span><span class="sxs-lookup"><span data-stu-id="a54c4-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="a54c4-115">dos máquinas virtuales (VM)</span><span class="sxs-lookup"><span data-stu-id="a54c4-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="a54c4-116">una interfaz de red virtual para cada máquina virtual con las direcciones IPv4 e IPv6 asignadas</span><span class="sxs-lookup"><span data-stu-id="a54c4-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="a54c4-117">un equilibrador de carga orientado a Internet con una dirección IP pública IPv4 e IPv6</span><span class="sxs-lookup"><span data-stu-id="a54c4-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="a54c4-118">un conjunto de disponibilidad con las dos máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="a54c4-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="a54c4-119">dos reglas de equilibrio de carga para asignar las VIP públicas a los puntos de conexión privados</span><span class="sxs-lookup"><span data-stu-id="a54c4-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="a54c4-120">Implementación de la solución mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="a54c4-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="a54c4-121">Los pasos siguientes muestran cómo crear un equilibrador de carga orientado a Internet mediante Azure Resource Manager con la CLI.</span><span class="sxs-lookup"><span data-stu-id="a54c4-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="a54c4-122">Con Azure Resource Manager, cada recurso se crea y configura de forma individual, y luego se juntan para crear un recurso.</span><span class="sxs-lookup"><span data-stu-id="a54c4-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="a54c4-123">Para implementar un equilibrador de carga, debe crear y configurar los siguientes objetos:</span><span class="sxs-lookup"><span data-stu-id="a54c4-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="a54c4-124">Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="a54c4-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="a54c4-125">Grupo de direcciones de back-end: contiene interfaces de red (NIC) para que las máquinas virtuales reciban tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a54c4-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="a54c4-126">Reglas de equilibrio de carga: contiene reglas que asignan un puerto público en el equilibrador de carga al del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="a54c4-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="a54c4-127">Reglas NAT de entrada: contiene reglas que asignan un puerto público en el equilibrador de carga a un puerto para una máquina virtual específica en el grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="a54c4-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="a54c4-128">Sondeos: contiene los sondeos de estado que se usan para comprobar la disponibilidad de las instancias de las máquinas virtuales del grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="a54c4-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="a54c4-129">Para más información, consulte [Compatibilidad de Azure Resource Manager con el equilibrador de carga](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a54c4-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="a54c4-130">Configuración del entorno de CLI para usar Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a54c4-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="a54c4-131">En este ejemplo, ejecutamos las herramientas de la CLI en una ventana Comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a54c4-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="a54c4-132">No usamos los cmdlets de Azure PowerShell, pero utilizamos las capacidades de scripting de PowerShell para mejorar la legibilidad y reutilización.</span><span class="sxs-lookup"><span data-stu-id="a54c4-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="a54c4-133">Si nunca ha usado la CLI de Azure, consulte [Instalación y configuración de la CLI de Azure](../cli-install-nodejs.md) y siga las instrucciones hasta el punto donde deba seleccionar su cuenta y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="a54c4-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a54c4-134">Ejecute el comando **azure config mode** para cambiar al modo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a54c4-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="a54c4-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="a54c4-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="a54c4-136">Inicie sesión en Azure y obtenga una lista de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="a54c4-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="a54c4-137">Escriba sus credenciales de Azure cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="a54c4-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="a54c4-138">Seleccione la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="a54c4-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="a54c4-139">Tome nota del Id. de suscripción para el siguiente paso.</span><span class="sxs-lookup"><span data-stu-id="a54c4-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="a54c4-140">Configure variables de PowerShell para usarlas con los comandos de la CLI.</span><span class="sxs-lookup"><span data-stu-id="a54c4-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="a54c4-141">Creación de un grupo de recursos, un equilibrador de carga, una red virtual y subredes</span><span class="sxs-lookup"><span data-stu-id="a54c4-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="a54c4-142">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a54c4-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="a54c4-143">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a54c4-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="a54c4-144">Cree una red virtual (VNet)</span><span class="sxs-lookup"><span data-stu-id="a54c4-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="a54c4-145">Cree dos subredes en esta red virtual</span><span class="sxs-lookup"><span data-stu-id="a54c4-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="a54c4-146">Creación de direcciones IP públicas para el grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="a54c4-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="a54c4-147">Configure las variables de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="a54c4-148">Cree una dirección IP pública para el grupo de servidores front-end</span><span class="sxs-lookup"><span data-stu-id="a54c4-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a54c4-149">El equilibrador de carga usa la etiqueta de dominio de la dirección IP pública como su FQDN.</span><span class="sxs-lookup"><span data-stu-id="a54c4-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="a54c4-150">Esto representa un cambio en la implementación clásica, que usa el nombre del servicio en la nube como el FQDN del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a54c4-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="a54c4-151">En este ejemplo, el FQDN es *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="a54c4-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="a54c4-152">Creación de grupos de servidores front-end y back-end</span><span class="sxs-lookup"><span data-stu-id="a54c4-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="a54c4-153">En este ejemplo se crea el grupo de direcciones IP de front-end que recibe el tráfico de red que entra al equilibrador de carga y el grupo de direcciones IP de back-end donde el grupo de servidores front-end envía el tráfico de red con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="a54c4-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="a54c4-154">Configure las variables de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="a54c4-155">Cree un grupo de direcciones IP de front-end mediante la asociación de la dirección IP pública creada en el paso anterior y el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a54c4-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="a54c4-156">Creación del sondeo, las reglas NAT y las reglas del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a54c4-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="a54c4-157">En este ejemplo se crean los siguientes elementos:</span><span class="sxs-lookup"><span data-stu-id="a54c4-157">This example creates the following items:</span></span>

* <span data-ttu-id="a54c4-158">una regla de sondeo para comprobar la conectividad con el puerto TCP 80</span><span class="sxs-lookup"><span data-stu-id="a54c4-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="a54c4-159">una regla NAT para trasladar todo el tráfico entrante del puerto 3389 al puerto 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a54c4-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="a54c4-160">una regla NAT para trasladar todo el tráfico entrante del puerto 3391 al puerto 3389 para RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="a54c4-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="a54c4-161">Una regla de equilibrador de carga para equilibrar todo el tráfico entrante del puerto 80 al puerto 80 en las direcciones del grupo de back-end.</span><span class="sxs-lookup"><span data-stu-id="a54c4-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="a54c4-162"><sup>1</sup> Las reglas NAT están asociadas a una instancia de máquina virtual específica detrás del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a54c4-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="a54c4-163">El tráfico de red que llega al puerto 3389 se envía a la máquina virtual específica y el puerto asociado a la regla NAT.</span><span class="sxs-lookup"><span data-stu-id="a54c4-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="a54c4-164">Debe especificar un protocolo (UDP o TCP) para una regla NAT.</span><span class="sxs-lookup"><span data-stu-id="a54c4-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="a54c4-165">Los dos protocolos no se pueden asignar al mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="a54c4-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="a54c4-166">Configure las variables de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="a54c4-167">Elaboración del sondeo</span><span class="sxs-lookup"><span data-stu-id="a54c4-167">Create the probe</span></span>

    <span data-ttu-id="a54c4-168">En el siguiente ejemplo se crea un sondeo TCP que comprueba la conectividad con el puerto TCP 80 de back-end cada 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="a54c4-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="a54c4-169">Marcará el recurso de back-end no disponible tras dos errores consecutivos.</span><span class="sxs-lookup"><span data-stu-id="a54c4-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="a54c4-170">Cree reglas NAT de entrada que permitan conexiones RDP a los recursos de back-end</span><span class="sxs-lookup"><span data-stu-id="a54c4-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="a54c4-171">Cree reglas de equilibrador de carga que envíen tráfico a distintos puertos de back-end dependiendo de qué front-end recibió la solicitud</span><span class="sxs-lookup"><span data-stu-id="a54c4-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="a54c4-172">Compruebe la configuración</span><span class="sxs-lookup"><span data-stu-id="a54c4-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="a54c4-173">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="a54c4-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="a54c4-174">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="a54c4-174">Create NICs</span></span>

<span data-ttu-id="a54c4-175">Cree tarjetas NIC y asócielas a reglas NAT, reglas de equilibrador de carga y sondeos.</span><span class="sxs-lookup"><span data-stu-id="a54c4-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="a54c4-176">Configure las variables de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="a54c4-177">Cree una NIC para cada back-end y agregue una configuración de IPv6</span><span class="sxs-lookup"><span data-stu-id="a54c4-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="a54c4-178">Creación de los recursos de la máquina virtual de back-end y conexión de cada NIC</span><span class="sxs-lookup"><span data-stu-id="a54c4-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="a54c4-179">Para crear máquinas virtuales, debe tener una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a54c4-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="a54c4-180">Para el equilibrio de carga, es necesario que las máquinas virtuales formen parte de un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54c4-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="a54c4-181">Para obtener más información sobre cómo crear máquinas virtuales, consulte [Creación de una máquina virtual de Azure con PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a54c4-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="a54c4-182">Configure las variables de PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54c4-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="a54c4-183">En este ejemplo se usan el nombre de usuario y contraseña de las máquinas virtuales en texto no cifrado.</span><span class="sxs-lookup"><span data-stu-id="a54c4-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="a54c4-184">Al usar credenciales sin cifrar, debe prestarse la atención adecuada.</span><span class="sxs-lookup"><span data-stu-id="a54c4-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="a54c4-185">Para ver un método más seguro de administración de credenciales en PowerShell, consulte el cmdlet [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a54c4-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="a54c4-186">Creación de la cuenta de almacenamiento y el conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="a54c4-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="a54c4-187">Puede usar una cuenta de almacenamiento existente al crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="a54c4-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="a54c4-188">El siguiente comando crea una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a54c4-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="a54c4-189">A continuación, cree el conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="a54c4-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="a54c4-190">Creación de las máquinas virtuales con las NIC asociadas</span><span class="sxs-lookup"><span data-stu-id="a54c4-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="a54c4-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a54c4-191">Next steps</span></span>

[<span data-ttu-id="a54c4-192">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="a54c4-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="a54c4-193">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a54c4-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="a54c4-194">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="a54c4-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
