---
title: "Conexión de una red virtual a otra red virtual: CLI de Azure | Microsoft Docs"
description: "Este artículo le guía por la conexión de redes virtuales entre sí por medio de Azure Resource Manager y la CLI de Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: ae42f661b39e8b6170fd415d758404fb33009ccc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="c1297-103">Configuración de una conexión de puerta de enlace de VPN de red virtual a red virtual mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c1297-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="c1297-104">En este artículo se explica cómo crear una conexión de VPN Gateway entre redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c1297-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="c1297-105">Las redes virtuales pueden estar en la misma región o en distintas, así como pertenecer a una única suscripción o a varias.</span><span class="sxs-lookup"><span data-stu-id="c1297-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="c1297-106">Al conectar redes virtuales de distintas suscripciones, estas no necesitan estar asociadas con el mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1297-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="c1297-107">Los pasos descritos en este artículo se aplican al modelo de implementación de Resource Manager y usan la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1297-107">The steps in this article apply to the Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="c1297-108">También se puede crear esta configuración con una herramienta o modelo de implementación distintos, mediante la selección de una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1297-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1297-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1297-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="c1297-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1297-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="c1297-111">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c1297-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="c1297-112">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c1297-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="c1297-113">Conexión de diferentes modelos de implementación - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1297-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="c1297-114">Conexión de diferentes modelos de implementación - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1297-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="c1297-115">La conexión de una red virtual a otra es muy parecida a la conexión de una red virtual a una ubicación de un sitio local.</span><span class="sxs-lookup"><span data-stu-id="c1297-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="c1297-116">Ambos tipos de conectividad usan una puerta de enlace de VPN para proporcionar un túnel seguro con IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="c1297-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="c1297-117">Si las redes virtuales están en la misma región, podría pensar en conectarlas mediante emparejamiento de VNET.</span><span class="sxs-lookup"><span data-stu-id="c1297-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="c1297-118">El emparejamiento de VNET no usa VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="c1297-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="c1297-119">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c1297-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="c1297-120">Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="c1297-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="c1297-121">Esto permite establecer topologías de red que combinan la conectividad entre entornos locales con la conectividad entre redes virtuales, como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1297-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Acerca de las conexiones](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="c1297-123"><a name="why"></a>¿Por qué debería conectarse a redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="c1297-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="c1297-124">Puede que desee conectar redes virtuales por las siguientes razones:</span><span class="sxs-lookup"><span data-stu-id="c1297-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="c1297-125">**Presencia geográfica y redundancia geográfica entre regiones**</span><span class="sxs-lookup"><span data-stu-id="c1297-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="c1297-126">Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="c1297-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="c1297-127">Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1297-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="c1297-128">Por ejemplo, puede configurar AlwaysOn de SQL con grupos de disponibilidad distribuidos en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1297-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="c1297-129">**Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**</span><span class="sxs-lookup"><span data-stu-id="c1297-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="c1297-130">Dentro de la misma región, se pueden configurar aplicaciones de niveles múltiples con varias redes virtuales conectadas entre sí para cumplir requisitos administrativos o de aislamiento.</span><span class="sxs-lookup"><span data-stu-id="c1297-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="c1297-131">Para más información acerca de las conexiones de red virtual a red virtual, consulte [P+F sobre conexiones de red virtual a red virtual](#faq) al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c1297-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="c1297-132">¿Qué serie de pasos debo seguir?</span><span class="sxs-lookup"><span data-stu-id="c1297-132">Which set of steps should I use?</span></span>

<span data-ttu-id="c1297-133">En este artículo, verá dos conjuntos de pasos diferentes.</span><span class="sxs-lookup"><span data-stu-id="c1297-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="c1297-134">Un conjunto de pasos para [redes virtuales que residen en la misma suscripción](#samesub) y otro para [redes virtuales que residen en suscripciones diferentes](#difsub).</span><span class="sxs-lookup"><span data-stu-id="c1297-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="c1297-135"><a name="samesub"></a>Conexión de redes virtuales que están en la misma suscripción</span><span class="sxs-lookup"><span data-stu-id="c1297-135"><a name="samesub"></a>Connect VNets that are in the same subscription</span></span>

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="c1297-137">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c1297-137">Before you begin</span></span>

<span data-ttu-id="c1297-138">Antes de empezar, instale la versión más reciente de los comandos de la CLI (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="c1297-138">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="c1297-139">Para más información sobre la instalación de los comandos de la CLI, consulte [Instalación de la CLI de Azure 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c1297-139">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="c1297-140"><a name="Plan"></a>Planeamiento de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="c1297-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="c1297-141">En los pasos siguientes, se crearán dos redes virtuales junto con sus subredes de puerta de enlace y configuraciones correspondientes.</span><span class="sxs-lookup"><span data-stu-id="c1297-141">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="c1297-142">A continuación crearemos una conexión VPN entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c1297-142">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="c1297-143">Es importante planear los intervalos de direcciones IP para la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="c1297-143">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="c1297-144">Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen.</span><span class="sxs-lookup"><span data-stu-id="c1297-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="c1297-145">En estos ejemplos, no se incluye ningún servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="c1297-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="c1297-146">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="c1297-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="c1297-147">En los ejemplos usamos los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c1297-147">We use the following values in the examples:</span></span>

<span data-ttu-id="c1297-148">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="c1297-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="c1297-149">Nombre de red virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="c1297-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="c1297-150">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="c1297-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="c1297-151">Ubicación: Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="c1297-151">Location: East US</span></span>
* <span data-ttu-id="c1297-152">TestVNet1: 10.11.0.0/16 y 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c1297-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="c1297-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="c1297-154">Backend: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="c1297-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="c1297-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="c1297-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="c1297-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="c1297-157">Dirección IP pública: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="c1297-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="c1297-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="c1297-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="c1297-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="c1297-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="c1297-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="c1297-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="c1297-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="c1297-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="c1297-162">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="c1297-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="c1297-163">Nombre de red virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="c1297-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="c1297-164">TestVNet2: 10.41.0.0/16 y 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c1297-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="c1297-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="c1297-166">Backend: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="c1297-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="c1297-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="c1297-168">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="c1297-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="c1297-169">Ubicación: Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="c1297-169">Location: West US</span></span>
* <span data-ttu-id="c1297-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="c1297-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="c1297-171">Dirección IP pública: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="c1297-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="c1297-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="c1297-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="c1297-173">Conexión: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="c1297-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="c1297-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="c1297-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="c1297-175"><a name="Connect"></a>Paso 1: Conexión a la suscripción</span><span class="sxs-lookup"><span data-stu-id="c1297-175"><a name="Connect"></a>Step 1 - Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="c1297-176"><a name="TestVNet1"></a>Paso 2: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="c1297-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="c1297-177">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1297-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="c1297-178">Cree TestVNet1 y las subredes para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-178">Create TestVNet1 and the subnets for TestVNet1.</span></span> <span data-ttu-id="c1297-179">En este ejemplo se crea una red virtual denominada TestVNet1 y una subred llamada FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="c1297-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="c1297-180">Cree otro espacio de direcciones para la subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="c1297-180">Create an additional address space for the backend subnet.</span></span> <span data-ttu-id="c1297-181">Tenga en cuenta que, en este paso, se especifican tanto el espacio de direcciones que se creó antes como el adicional que se va a agregar.</span><span class="sxs-lookup"><span data-stu-id="c1297-181">Notice that in this step, we specify both the address space that we created earlier, and the additional address space that we want to add.</span></span> <span data-ttu-id="c1297-182">Esto se debe a que el comando [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) sobrescribe la configuración anterior.</span><span class="sxs-lookup"><span data-stu-id="c1297-182">This is because the [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites the previous settings.</span></span> <span data-ttu-id="c1297-183">Asegúrese de especificar todos los prefijos de direcciones cuando use este comando.</span><span class="sxs-lookup"><span data-stu-id="c1297-183">Make sure to specify all of the address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="c1297-184">Cree la subred de back-end.</span><span class="sxs-lookup"><span data-stu-id="c1297-184">Create the backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="c1297-185">Cree la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c1297-185">Create the gateway subnet.</span></span> <span data-ttu-id="c1297-186">Asegúrese de que la subred de puerta de enlace se llame "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="c1297-186">Notice that the gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="c1297-187">Este nombre es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="c1297-187">This name is required.</span></span> <span data-ttu-id="c1297-188">En este ejemplo, la subred de la puerta de enlace está usando un /27.</span><span class="sxs-lookup"><span data-stu-id="c1297-188">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="c1297-189">Aunque es posible crear una subred de puerta de enlace tan pequeña como /29, se recomienda que cree una subred mayor que incluya más direcciones seleccionando al menos /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="c1297-189">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="c1297-190">Esto permitirá suficientes direcciones para dar cabida a posibles configuraciones adicionales que desee en el futuro.</span><span class="sxs-lookup"><span data-stu-id="c1297-190">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="c1297-191">Solicite que se asigne una dirección IP pública a la puerta de enlace que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="c1297-191">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="c1297-192">Observe que AllocationMethod es dinámico.</span><span class="sxs-lookup"><span data-stu-id="c1297-192">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="c1297-193">No puede especificar la dirección IP que desea usar.</span><span class="sxs-lookup"><span data-stu-id="c1297-193">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="c1297-194">Se asigna dinámicamente a la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c1297-194">It's dynamically allocated to your gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="c1297-195">Cree la puerta de enlace de red virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-195">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="c1297-196">Las configuraciones VNet a VNet requieren un VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="c1297-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="c1297-197">Si este comando se ejecuta con el parámetro '--no-wait', no se verán los comentarios o resultados.</span><span class="sxs-lookup"><span data-stu-id="c1297-197">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="c1297-198">El parámetro "--no-wait" permite que la puerta de enlace se cree en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="c1297-198">The '--no-wait' parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="c1297-199">No significa que se termine de crear la puerta de enlace de VPN de inmediato.</span><span class="sxs-lookup"><span data-stu-id="c1297-199">It does not mean that the VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="c1297-200">Se suelen tardar 45 minutos o más en crear una puerta de enlace, según la SKU de puerta de enlace que se use.</span><span class="sxs-lookup"><span data-stu-id="c1297-200">Creating a gateway can often take 45 minutes or more, depending on the gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="c1297-201"><a name="TestVNet4"></a>Paso 3: Creación y configuración de TestVNet4</span><span class="sxs-lookup"><span data-stu-id="c1297-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="c1297-202">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1297-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="c1297-203">Cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="c1297-204">Cree subredes adicionales para TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="c1297-205">Cree la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c1297-205">Create the gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="c1297-206">Solicite una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="c1297-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="c1297-207">Cree la puerta de enlace de la red virtual TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-207">Create the TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="c1297-208"><a name="createconnect"></a>Paso 4: Creación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="c1297-208"><a name="createconnect"></a>Step 4 - Create the connections</span></span>

<span data-ttu-id="c1297-209">Ahora tiene dos redes virtuales con puertas de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="c1297-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="c1297-210">El siguiente paso consiste en crear conexiones de puerta de enlace de VPN entre las puertas de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c1297-210">The next step is to create VPN gateway connections between the virtual network gateways.</span></span> <span data-ttu-id="c1297-211">Si usó los ejemplos anteriores, las puertas de enlace de red virtual se encuentran en grupos de recursos distintos.</span><span class="sxs-lookup"><span data-stu-id="c1297-211">If you used the examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="c1297-212">Cuando las puertas de enlace están en grupos de recursos distintos, debe identificar y especificar los identificadores de recursos para cada puerta de enlace al establecer una conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-212">When gateways are in different resource groups, you need to identify and specify the resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="c1297-213">Si sus redes virtuales están en el mismo grupo de recursos, puede usar el [segundo conjunto de instrucciones](#samerg) porque no es necesario especificar los identificadores de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1297-213">If your VNets are in the same resource group, you can use the [second set of instructions](#samerg) because you don't need to specify the resource IDs.</span></span>

### <span data-ttu-id="c1297-214"><a name="diffrg"></a>Conexión de redes virtuales que residen en grupos de recursos distintos</span><span class="sxs-lookup"><span data-stu-id="c1297-214"><a name="diffrg"></a>To connect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="c1297-215">Obtenga el id. de recurso de VNet1GW de la salida del comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1297-215">Get the Resource ID of VNet1GW from the output of the following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="c1297-216">En la salida, busque la línea "id:".</span><span class="sxs-lookup"><span data-stu-id="c1297-216">In the output, find the "id:" line.</span></span> <span data-ttu-id="c1297-217">Los valores entrecomillados se necesitan para crear la conexión en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="c1297-217">The values within the quotes are needed to create the connection in the next section.</span></span> <span data-ttu-id="c1297-218">Copie estos valores en un editor de texto, como el Bloc de notas, para que pueda pegarlos fácilmente al crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-218">Copy these values to a text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="c1297-219">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1297-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="c1297-220">Copie los valores después de **"id":** dentro de las comillas.</span><span class="sxs-lookup"><span data-stu-id="c1297-220">Copy the values after **"id":** within the quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="c1297-221">Obtenga el id. de recurso de VNet4GW y copie los valores en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="c1297-221">Get the Resource ID of VNet4GW and copy the values to a text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="c1297-222">Cree la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-222">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="c1297-223">En este paso, creará la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-223">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="c1297-224">Se hace referencia a una clave compartida en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c1297-224">There is a shared key referenced in the examples.</span></span> <span data-ttu-id="c1297-225">Puede utilizar sus propios valores para la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="c1297-225">You can use your own values for the shared key.</span></span> <span data-ttu-id="c1297-226">Lo importante es que la clave compartida coincida en ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="c1297-226">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="c1297-227">Se tardará unos momentos en terminar de crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-227">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="c1297-228">Cree la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-228">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="c1297-229">Este paso es similar al anterior, salvo en que se crea la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-229">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="c1297-230">Asegúrese de que coincidan las claves compartidas.</span><span class="sxs-lookup"><span data-stu-id="c1297-230">Make sure the shared keys match.</span></span> <span data-ttu-id="c1297-231">Se tarda unos minutos en establecer la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-231">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="c1297-232">Compruebe las conexiones.</span><span class="sxs-lookup"><span data-stu-id="c1297-232">Verify your connections.</span></span> <span data-ttu-id="c1297-233">Consulte [Comprobación de las conexiones](#verify).</span><span class="sxs-lookup"><span data-stu-id="c1297-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="c1297-234"><a name="samerg"></a>Para conectar redes virtuales que residen en el mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c1297-234"><a name="samerg"></a>To connect VNets that reside in the same resource group</span></span>

1. <span data-ttu-id="c1297-235">Cree la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-235">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="c1297-236">En este paso, creará la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="c1297-236">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="c1297-237">Tenga en cuenta que los grupos de recursos son iguales en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c1297-237">Notice the resource groups are the same in the examples.</span></span> <span data-ttu-id="c1297-238">También verá una clave compartida a la que se hace referencia en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="c1297-238">You also see a shared key referenced in the examples.</span></span> <span data-ttu-id="c1297-239">Puede usar sus propios valores para la clave compartida, pero esta debe coincidir en ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="c1297-239">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="c1297-240">Se tardará unos momentos en terminar de crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-240">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="c1297-241">Cree la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-241">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="c1297-242">Este paso es similar al anterior, salvo en que se crea la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-242">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="c1297-243">Asegúrese de que coincidan las claves compartidas.</span><span class="sxs-lookup"><span data-stu-id="c1297-243">Make sure the shared keys match.</span></span> <span data-ttu-id="c1297-244">Se tarda unos minutos en establecer la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-244">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="c1297-245">Compruebe las conexiones.</span><span class="sxs-lookup"><span data-stu-id="c1297-245">Verify your connections.</span></span> <span data-ttu-id="c1297-246">Consulte [Comprobación de las conexiones](#verify).</span><span class="sxs-lookup"><span data-stu-id="c1297-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="c1297-247"><a name="difsub"></a>Conexión de redes virtuales que están en suscripciones diferentes</span><span class="sxs-lookup"><span data-stu-id="c1297-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="c1297-249">En este escenario, conectaremos TestVNet1 y TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="c1297-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="c1297-250">Las redes virtuales residen en suscripciones distintas.</span><span class="sxs-lookup"><span data-stu-id="c1297-250">The VNets reside different subscriptions.</span></span> <span data-ttu-id="c1297-251">Las suscripciones no necesitan estar asociadas con el mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c1297-251">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="c1297-252">Los pasos para esta configuración permiten agregar una conexión de red virtual a red virtual adicional para poder conectar TestVNet1 a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="c1297-252">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span></span>

### <span data-ttu-id="c1297-253"><a name="TestVNet1diff"></a>Paso 5: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="c1297-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="c1297-254">Estas instrucciones son una continuación de los pasos descritos en las secciones anteriores.</span><span class="sxs-lookup"><span data-stu-id="c1297-254">These instructions continue from the steps in the preceding sections.</span></span> <span data-ttu-id="c1297-255">Tiene que completar el [paso 1](#Connect) y el [paso 2](#TestVNet1) para crear y configurar TestVNet1 y VPN Gateway para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="c1297-256">Para esta configuración, no se necesita crear TestVNet4 de la sección anterior, aunque, si la creó, no entrará en conflicto con estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c1297-256">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="c1297-257">Cuando haya completado el paso 1 y el 2, continúe con el paso 6 (a continuación).</span><span class="sxs-lookup"><span data-stu-id="c1297-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="c1297-258"><a name="verifyranges"></a>Paso 6: Comprobación de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="c1297-258"><a name="verifyranges"></a>Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="c1297-259">Cuando cree conexiones adicionales, es importante asegurarse de que el espacio de direcciones IP de la red virtual nueva no se solape con ninguno de los demás intervalos de redes virtuales o de puertas de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="c1297-259">When creating additional connections, it's important to verify that the IP address space of the new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="c1297-260">En este ejercicio, use los siguientes valores para TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="c1297-260">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="c1297-261">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="c1297-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="c1297-262">Nombre de red virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="c1297-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="c1297-263">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="c1297-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="c1297-264">Ubicación: Japón Oriental</span><span class="sxs-lookup"><span data-stu-id="c1297-264">Location: Japan East</span></span>
* <span data-ttu-id="c1297-265">TestVNet5: 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c1297-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="c1297-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="c1297-267">Backend: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c1297-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="c1297-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="c1297-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="c1297-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="c1297-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="c1297-270">Dirección IP pública: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="c1297-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="c1297-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="c1297-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="c1297-272">Conexión: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="c1297-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="c1297-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="c1297-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="c1297-274"><a name="TestVNet5"></a>Paso 7: Creación y configuración de TestVNet5</span><span class="sxs-lookup"><span data-stu-id="c1297-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="c1297-275">Este paso debe realizarse en el contexto de la nueva suscripción, Suscripción 5.</span><span class="sxs-lookup"><span data-stu-id="c1297-275">This step must be done in the context of the new subscription, Subscription 5.</span></span> <span data-ttu-id="c1297-276">Es posible que esta parte la realice el administrador de otra organización que posea la suscripción.</span><span class="sxs-lookup"><span data-stu-id="c1297-276">This part may be performed by the administrator in a different organization that owns the subscription.</span></span> <span data-ttu-id="c1297-277">Para cambiar entre suscripciones, use "az account list --all" para obtener una lista de las suscripciones disponibles para su cuenta y después use "az account set --subscription <subscriptionID>" para cambiar a la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="c1297-277">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="c1297-278">Asegúrese de que está conectados a Suscripción 5 y cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1297-278">Make sure you are connected to Subscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="c1297-279">Cree TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="c1297-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="c1297-280">Agregue subredes.</span><span class="sxs-lookup"><span data-stu-id="c1297-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="c1297-281">Agregue la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c1297-281">Add the gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="c1297-282">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="c1297-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="c1297-283">Creación de la puerta de enlace de TestVNet5</span><span class="sxs-lookup"><span data-stu-id="c1297-283">Create the TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="c1297-284"><a name="connections5"></a>Paso 8: Creación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="c1297-284"><a name="connections5"></a>Step 8 - Create the connections</span></span>

<span data-ttu-id="c1297-285">Este paso se divide en dos sesiones de la CLI marcadas como **[Suscripción 1]** y **[Suscripción 5]** porque las puertas de enlace están en suscripciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="c1297-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because the gateways are in the different subscriptions.</span></span> <span data-ttu-id="c1297-286">Para cambiar entre suscripciones, use "az account list --all" para obtener una lista de las suscripciones disponibles para su cuenta y después use "az account set --subscription <subscriptionID>" para cambiar a la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="c1297-286">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="c1297-287">**[Suscripción 1]** Inicie sesión y conéctese a Suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="c1297-287">**[Subscription 1]** Log in and connect to Subscription 1.</span></span> <span data-ttu-id="c1297-288">Ejecute el siguiente comando para obtener el nombre y el identificador de la puerta de enlace de la salida:</span><span class="sxs-lookup"><span data-stu-id="c1297-288">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="c1297-289">Copie la salida para "id:".</span><span class="sxs-lookup"><span data-stu-id="c1297-289">Copy the output for "id:".</span></span> <span data-ttu-id="c1297-290">Envíe el identificador y el nombre de la puerta de enlace de red virtual (VNet1GW) al administrador de Suscripción 5 por correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="c1297-290">Send the ID and the name of the VNet gateway (VNet1GW) to the administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="c1297-291">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1297-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="c1297-292">**[Suscripción 5]** Inicie sesión y conéctese a Suscripción 5.</span><span class="sxs-lookup"><span data-stu-id="c1297-292">**[Subscription 5]** Log in and connect to Subscription 5.</span></span> <span data-ttu-id="c1297-293">Ejecute el siguiente comando para obtener el nombre y el identificador de la puerta de enlace de la salida:</span><span class="sxs-lookup"><span data-stu-id="c1297-293">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="c1297-294">Copie la salida para "id:".</span><span class="sxs-lookup"><span data-stu-id="c1297-294">Copy the output for "id:".</span></span> <span data-ttu-id="c1297-295">Envíe el identificador y el nombre de la puerta de enlace de red virtual (VNet5GW) al administrador de Suscripción 1 por correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="c1297-295">Send the ID and the name of the VNet gateway (VNet5GW) to the administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="c1297-296">**[Suscripción 1]** En este paso, va a crear la conexión de TestVNet1 a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="c1297-296">**[Subscription 1]** In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="c1297-297">Puede usar sus propios valores para la clave compartida, pero esta debe coincidir en ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="c1297-297">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="c1297-298">Se tardará unos momentos en terminar de crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="c1297-298">Creating a connection can take a short while to complete.</span></span> <span data-ttu-id="c1297-299">Asegúrese de conectarse a la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="c1297-299">Make sure you connect to Subscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="c1297-300">**[Suscripción 5]** Este paso es similar al anterior, salvo en que se crea la conexión de TestVNet5 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c1297-300">**[Subscription 5]** This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="c1297-301">Asegúrese de que las claves compartidas coincidan y que se conecta a Suscripción 5.</span><span class="sxs-lookup"><span data-stu-id="c1297-301">Make sure that the shared keys match and that you connect to Subscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="c1297-302"><a name="verify"></a>Comprobación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="c1297-302"><a name="verify"></a>Verify the connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="c1297-303"><a name="faq"></a>P+F sobre conexiones de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="c1297-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c1297-304">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c1297-304">Next steps</span></span>

* <span data-ttu-id="c1297-305">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="c1297-305">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c1297-306">Para más información, consulte la [documentación sobre máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="c1297-306">For more information, see the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c1297-307">Para más información acerca de BGP, consulte [Información general de BGP](vpn-gateway-bgp-overview.md) y [Configuración de BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c1297-307">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
