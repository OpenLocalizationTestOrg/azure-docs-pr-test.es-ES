---
title: "aaaCreate una conexión a Internet cargar equilibrador - CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el Administrador de recursos en Hola CLI de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="4d0a9-103">Creación de un equilibrador de carga de internet mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4d0a9-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d0a9-104">Portal</span><span class="sxs-lookup"><span data-stu-id="4d0a9-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="4d0a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d0a9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="4d0a9-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4d0a9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="4d0a9-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="4d0a9-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4d0a9-108">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="4d0a9-109">También puede [Obtenga información acerca de cómo el equilibrador mediante la implementación clásica de la carga de toocreate una conexión a Internet](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4d0a9-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="4d0a9-110">Implementar soluciones de hello mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4d0a9-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="4d0a9-111">Hola pasos muestra cómo toocreate una conexión a Internet cargar equilibrador con Azure Resource Manager CLI.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="4d0a9-112">Con Azure Resource Manager se crea y se configuran individualmente cada recurso, a continuación, reunir toocreate un recurso.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="4d0a9-113">Debe crear y configurar Hola después objetos toodeploy un equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="4d0a9-114">Configuración de direcciones IP de front-end: contiene direcciones IP públicas para el tráfico de red entrante.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="4d0a9-115">Grupo de direcciones de back-end - contiene interfaces de red (NIC) de tráfico de red de tooreceive de máquinas virtuales de Hola Hola equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="4d0a9-116">Reglas de equilibrio de carga - contiene reglas de asignación de un puerto público en tooport de equilibrador de carga de hello en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="4d0a9-117">Reglas NAT de entrada: contiene las reglas de asignación de un puerto público en el puerto de tooa de equilibrador de carga de Hola para una máquina virtual específica en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="4d0a9-118">Sondea: contiene toocheck disponibilidad de sondeos que se usan de mantenimiento de instancias de máquinas virtuales en el grupo de direcciones de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="4d0a9-119">Para más información, consulte [Compatibilidad de Azure Resource Manager con Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="4d0a9-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="4d0a9-120">Configurar la CLI toouse el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="4d0a9-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="4d0a9-121">Si nunca ha utilizado la CLI de Azure, consulte [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) y siga las instrucciones de hello punto toohello donde seleccionar su cuenta de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="4d0a9-122">Ejecute hello **configuración azure modo** modo de administrador de tooResource de comandos tooswitch, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="4d0a9-123">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="4d0a9-124">Crear una red virtual y una dirección IP pública para el grupo de direcciones IP de front-end de Hola</span><span class="sxs-lookup"><span data-stu-id="4d0a9-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="4d0a9-125">Crear una red virtual (VNet) con el nombre *NRPVnet* en ubicación de UU hello mediante un grupo de recursos denominado *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="4d0a9-126">Cree una subred llamada *NRPVnetSubnet* con un bloque CIDR de 10.0.0.0/24 en *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="4d0a9-127">Crear una dirección IP pública denominada *NRPPublicIP* toobe utilizado por un grupo IP front-end con el nombre DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando hello siguiente utiliza el tipo de asignación estático de Hola y tiempo de inactividad de 4 minutos.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="4d0a9-128">equilibrador de carga de Hello utilizará la etiqueta de Hola de dominio de la dirección IP pública de hello como su FQDN.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="4d0a9-129">Este un cambio de implementación clásica, que utiliza el servicio de nube de hello como Hola nombre de dominio completo (FQDN) de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="4d0a9-130">En este ejemplo, hello FQDN es *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="4d0a9-131">Crear un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4d0a9-131">Create a load balancer</span></span>

<span data-ttu-id="4d0a9-132">Hello siguiente comando crea un equilibrador de carga con el nombre *NRPlb* en hello *NRPRG* grupo de recursos de hello *UU* ubicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="4d0a9-133">Creación de un grupo de direcciones IP de front-end y un grupo de direcciones de back-end</span><span class="sxs-lookup"><span data-stu-id="4d0a9-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="4d0a9-134">En este ejemplo se muestra cómo toocreate Hola grupo IP front-end que recibe el tráfico de red entrante de hello en hello equilibrador de carga y Hola grupo de direcciones IP de back-end que grupo front-end de hello envía tráfico de red con equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="4d0a9-135">Cree un grupo IP front-end asociar IP pública Hola creado en el paso anterior de Hola y equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="4d0a9-136">Configurar un grupo de direcciones de back-end utiliza tooreceive el tráfico entrante de grupo de direcciones IP de front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="4d0a9-137">Crear reglas de equilibrador de carga, reglas NAT y sondeo</span><span class="sxs-lookup"><span data-stu-id="4d0a9-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="4d0a9-138">Este ejemplo crea Hola siguientes elementos.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-138">This example creates hello following items.</span></span>

* <span data-ttu-id="4d0a9-139">regla de NAT tootranslate todo el tráfico entrante en el puerto 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4d0a9-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="4d0a9-140">regla de NAT tootranslate todo el tráfico entrante en el puerto 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="4d0a9-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="4d0a9-141">un toobalance de regla de equilibrador de carga todo el tráfico entrante en el puerto 80 tooport 80 en hello direcciones de grupo de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="4d0a9-142">un estado de mantenimiento de sondeo regla toocheck hello en una página denominada *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="4d0a9-143"><sup>1</sup> reglas NAT son la instancia de máquina virtual específica de tooa asociado detrás de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="4d0a9-144">tráfico de red de Hola que llegan en el puerto 21 se envía la máquina virtual específica de tooa en el puerto asociado con esta regla NAT de 22.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="4d0a9-145">Debe especificar un protocolo (UDP o TCP) para una regla NAT.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="4d0a9-146">Ambos protocolos no se pueden asignar toohello mismo puerto.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="4d0a9-147">Crear hello las reglas NAT.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="4d0a9-148">Cree una regla de equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="4d0a9-149">Cree un sondeo de estado.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="4d0a9-150">Compruebe la configuración.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="4d0a9-151">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="4d0a9-152">Cree tarjetas NIC</span><span class="sxs-lookup"><span data-stu-id="4d0a9-152">Create NICs</span></span>

<span data-ttu-id="4d0a9-153">Necesita toocreate NIC (o modificar los existentes) y asociarlos a tooNAT reglas, reglas de equilibrador de carga y sondeos.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="4d0a9-154">Cree una NIC denominada *nic1 de carga equilibrada puede*y asociar con hello *rdp1* NAT hello y regla *NRPbackendpool* grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="4d0a9-155">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="4d0a9-156">Cree una NIC denominada *nic2 de carga equilibrada puede*y asociar con hello *rdp2* NAT hello y regla *NRPbackendpool* grupo de direcciones de back-end.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="4d0a9-157">Crear una máquina virtual (VM) con el nombre *web1*y asociar con hello NIC denominado *nic1 de carga equilibrada puede*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="4d0a9-158">Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4d0a9-159">Hola a las máquinas virtuales en un toobe de necesidad de equilibrador de carga en el mismo conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="4d0a9-160">Use `azure availset create` toocreate un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="4d0a9-161">salida de Hello debe ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="4d0a9-162">mensaje informativo de Hello **se trata de una NIC sin publicIP configurado** se espera desde que hello NIC creó Hola equilibrador de carga conecta tooInternet utilizando la dirección IP pública de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="4d0a9-163">Desde hello *nic1 de carga equilibrada puede* NIC está asociado con hello *rdp1* regla de NAT, puede conectar demasiado*web1* mediante RDP a través del puerto 3441 en equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="4d0a9-164">Crear una máquina virtual (VM) con el nombre *web2*y asociar con hello NIC denominado *nic2 de carga equilibrada puede*.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="4d0a9-165">Llama a una cuenta de almacenamiento *web1nrp* se creó antes de ejecutar el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="4d0a9-166">Actualización de un equilibrador de carga existente</span><span class="sxs-lookup"><span data-stu-id="4d0a9-166">Update an existing load balancer</span></span>
<span data-ttu-id="4d0a9-167">Puede agregar reglas que hacen referencia a un equilibrador de carga existente.</span><span class="sxs-lookup"><span data-stu-id="4d0a9-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="4d0a9-168">En el siguiente ejemplo de Hola, una nueva regla de equilibrador de carga se agrega el equilibrador de carga existente tooan **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="4d0a9-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="4d0a9-169">Eliminar un equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4d0a9-169">Delete a load balancer</span></span>
<span data-ttu-id="4d0a9-170">Usar hello después comando tooremove un equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="4d0a9-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="4d0a9-171">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d0a9-171">Next steps</span></span>
[<span data-ttu-id="4d0a9-172">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="4d0a9-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="4d0a9-173">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4d0a9-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="4d0a9-174">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="4d0a9-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
