---
title: 'Conectar la red virtual tooanother red virtual: CLI de Azure | Documentos de Microsoft'
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="2600f-103">Configuración de una conexión de puerta de enlace de VPN de red virtual a red virtual mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2600f-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="2600f-104">Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="2600f-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="2600f-105">Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="2600f-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="2600f-106">Al conectar redes virtuales de distintas suscripciones, las suscripciones de hello no es necesario toobe asociada Hola a mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2600f-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="2600f-107">pasos de Hello en este artículo aplican el modelo de implementación del Administrador de recursos de toohello y utilizar CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="2600f-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="2600f-108">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="2600f-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2600f-109">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2600f-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="2600f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2600f-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="2600f-111">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2600f-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="2600f-112">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2600f-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="2600f-113">Conexión de diferentes modelos de implementación - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2600f-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="2600f-114">Conexión de diferentes modelos de implementación - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2600f-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="2600f-115">Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local.</span><span class="sxs-lookup"><span data-stu-id="2600f-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="2600f-116">Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2600f-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="2600f-117">Si sus redes virtuales están en hello misma región, puede que desee tooconsider conectándolos mediante el intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="2600f-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="2600f-118">El emparejamiento de VNET no usa VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="2600f-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="2600f-119">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2600f-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="2600f-120">Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="2600f-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="2600f-121">Esto le permite establecer topologías de red que combinen la conectividad entre entornos con conectividad entre redes virtuales, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="2600f-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Acerca de las conexiones](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="2600f-123"><a name="why"></a>¿Por qué debería conectarse a redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="2600f-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="2600f-124">Puede que desee tooconnect las redes virtuales para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="2600f-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="2600f-125">**Presencia geográfica y redundancia geográfica entre regiones**</span><span class="sxs-lookup"><span data-stu-id="2600f-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="2600f-126">Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="2600f-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="2600f-127">Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="2600f-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="2600f-128">Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="2600f-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="2600f-129">**Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**</span><span class="sxs-lookup"><span data-stu-id="2600f-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="2600f-130">Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas entre sí debido tooisolation o requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="2600f-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="2600f-131">Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2600f-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="2600f-132">¿Qué serie de pasos debo seguir?</span><span class="sxs-lookup"><span data-stu-id="2600f-132">Which set of steps should I use?</span></span>

<span data-ttu-id="2600f-133">En este artículo, verá dos conjuntos de pasos diferentes.</span><span class="sxs-lookup"><span data-stu-id="2600f-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="2600f-134">Un conjunto de pasos para [redes virtuales que residen en Hola misma suscripción](#samesub)y otro para [redes virtuales que residen en distintas suscripciones](#difsub).</span><span class="sxs-lookup"><span data-stu-id="2600f-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="2600f-135"><a name="samesub"></a>Conectar redes virtuales que se encuentran en hello misma suscripción</span><span class="sxs-lookup"><span data-stu-id="2600f-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="2600f-137">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2600f-137">Before you begin</span></span>

<span data-ttu-id="2600f-138">Antes de comenzar, instalar la versión más reciente de Hola de comandos de CLI de hello (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="2600f-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="2600f-139">Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2600f-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="2600f-140"><a name="Plan"></a>Planeamiento de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="2600f-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="2600f-141">Hola pasos, se crea dos redes virtuales junto con sus subredes correspondientes de la puerta de enlace y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="2600f-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="2600f-142">Creamos, a continuación, una conexión VPN entre Hola dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="2600f-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="2600f-143">Es importante tooplan intervalos de direcciones IP de hello para la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="2600f-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="2600f-144">Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen.</span><span class="sxs-lookup"><span data-stu-id="2600f-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="2600f-145">En estos ejemplos, no se incluye ningún servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2600f-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="2600f-146">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="2600f-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="2600f-147">Utilizamos Hola después los valores en los ejemplos de hello:</span><span class="sxs-lookup"><span data-stu-id="2600f-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="2600f-148">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="2600f-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="2600f-149">Nombre de red virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2600f-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="2600f-150">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="2600f-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="2600f-151">Ubicación: Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="2600f-151">Location: East US</span></span>
* <span data-ttu-id="2600f-152">TestVNet1: 10.11.0.0/16 y 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2600f-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="2600f-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="2600f-154">Backend: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="2600f-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="2600f-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="2600f-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="2600f-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="2600f-157">Dirección IP pública: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="2600f-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="2600f-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2600f-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="2600f-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="2600f-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="2600f-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="2600f-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="2600f-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2600f-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="2600f-162">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="2600f-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="2600f-163">Nombre de red virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2600f-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="2600f-164">TestVNet2: 10.41.0.0/16 y 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2600f-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="2600f-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="2600f-166">Backend: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="2600f-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="2600f-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="2600f-168">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="2600f-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="2600f-169">Ubicación: Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="2600f-169">Location: West US</span></span>
* <span data-ttu-id="2600f-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="2600f-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="2600f-171">Dirección IP pública: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="2600f-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="2600f-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2600f-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="2600f-173">Conexión: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="2600f-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="2600f-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2600f-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="2600f-175"><a name="Connect"></a>Paso 1: conectar tooyour suscripción</span><span class="sxs-lookup"><span data-stu-id="2600f-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="2600f-176"><a name="TestVNet1"></a>Paso 2: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2600f-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="2600f-177">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2600f-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="2600f-178">Crear subredes hello y TestVNet1 para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="2600f-179">En este ejemplo se crea una red virtual denominada TestVNet1 y una subred llamada FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="2600f-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="2600f-180">Crear un espacio de direcciones adicionales para la subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="2600f-181">Tenga en cuenta que en este paso, se especifique tanto espacio de direcciones de Hola que hemos creado con anterioridad y Hola espacio de direcciones adicional que deseamos tooadd.</span><span class="sxs-lookup"><span data-stu-id="2600f-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="2600f-182">Esto es porque hello [actualizar la red virtual de red az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando sobrescribe la configuración anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="2600f-183">Asegúrese de toospecify seguro todos Hola prefijos de dirección cuando se usa este comando.</span><span class="sxs-lookup"><span data-stu-id="2600f-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="2600f-184">Crear una subred de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="2600f-185">Crear una subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-185">Create hello gateway subnet.</span></span> <span data-ttu-id="2600f-186">Tenga en cuenta que esa subred de puerta de enlace de hello es denominada "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="2600f-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="2600f-187">Este nombre es obligatorio.</span><span class="sxs-lookup"><span data-stu-id="2600f-187">This name is required.</span></span> <span data-ttu-id="2600f-188">En este ejemplo, la subred de puerta de enlace de hello está usando un /27.</span><span class="sxs-lookup"><span data-stu-id="2600f-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="2600f-189">Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluye direcciones más si se selecciona al menos /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="2600f-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="2600f-190">Esto le permitirá suficientes direcciones tooaccommodate posibles configuraciones adicionales que puede querer en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="2600f-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="2600f-191">Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="2600f-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="2600f-192">Tenga en cuenta que hello AllocationMethod es dinámico.</span><span class="sxs-lookup"><span data-stu-id="2600f-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="2600f-193">No se puede especificar la dirección IP de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="2600f-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="2600f-194">Es puerta de enlace de tooyour asignada dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="2600f-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="2600f-195">Crear puerta de enlace de red virtual de Hola para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="2600f-196">Las configuraciones VNet a VNet requieren un VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="2600f-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="2600f-197">Si ejecuta este comando usando hello '--sin - wait' parámetro, no ve los comentarios o la salida.</span><span class="sxs-lookup"><span data-stu-id="2600f-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="2600f-198">Hello '--sin - wait' parámetro permite toocreate de puerta de enlace de hello en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="2600f-199">No significa que esa puerta de enlace VPN de hello finaliza la creación de inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="2600f-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="2600f-200">Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello SKU que usar.</span><span class="sxs-lookup"><span data-stu-id="2600f-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="2600f-201"><a name="TestVNet4"></a>Paso 3: Creación y configuración de TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2600f-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="2600f-202">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2600f-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="2600f-203">Cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2600f-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="2600f-204">Cree subredes adicionales para TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2600f-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="2600f-205">Crear una subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="2600f-206">Solicite una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2600f-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="2600f-207">Crear puerta de enlace de red virtual de hello TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2600f-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="2600f-208"><a name="createconnect"></a>Paso 4: crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="2600f-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="2600f-209">Ahora tiene dos redes virtuales con puertas de enlace de VPN.</span><span class="sxs-lookup"><span data-stu-id="2600f-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="2600f-210">Hola siguiente paso es toocreate las conexiones de puerta de enlace VPN entre puertas de enlace de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="2600f-211">Si ha utilizado ejemplos de hello anteriores, las puertas de enlace de red virtual se encuentran en distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="2600f-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="2600f-212">Cuando las puertas de enlace están en distintos grupos de recursos, es necesario tooidentify y especifique el Id. de recurso de Hola para cada puerta de enlace al establecer una conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="2600f-213">Si sus redes virtuales están en hello mismo grupo de recursos, puede usar hello [segundo conjunto de instrucciones](#samerg) porque no necesita Id. de recurso de hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="2600f-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="2600f-214"><a name="diffrg"></a>tooconnect redes virtuales que residen en distintos grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="2600f-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="2600f-215">Obtener Id. de recurso de VNet1GW Hola de salida de hello de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="2600f-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="2600f-216">En la salida de hello, encontrar Hola "Id.:" línea.</span><span class="sxs-lookup"><span data-stu-id="2600f-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="2600f-217">los valores de Hello entre comillas Hola son necesarios toocreate Hola conexión en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="2600f-218">Copie estos editor de texto tooa de valores, como el Bloc de notas, para que pueda pegarlos fácilmente al crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="2600f-219">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2600f-219">Example output:</span></span>

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

  <span data-ttu-id="2600f-220">Copiar valores de hello después **"id":** entre comillas Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="2600f-221">Obtener Hola Id. de recurso de VNet4GW y copie Hola valores tooa editor de texto.</span><span class="sxs-lookup"><span data-stu-id="2600f-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="2600f-222">Crear hello TestVNet1 tooTestVNet4 conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="2600f-223">En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2600f-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="2600f-224">No hay una clave compartida que se hace referencia en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="2600f-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="2600f-225">Puede utilizar sus propios valores de clave compartida de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="2600f-226">Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones.</span><span class="sxs-lookup"><span data-stu-id="2600f-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="2600f-227">Crear una conexión, toma un valor bajo al toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2600f-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="2600f-228">Crear hello TestVNet4 tooTestVNet1 conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="2600f-229">Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="2600f-230">Asegúrese de que coincide con las claves de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="2600f-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="2600f-231">Tarda unos minutos en conexión de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="2600f-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="2600f-232">Compruebe las conexiones.</span><span class="sxs-lookup"><span data-stu-id="2600f-232">Verify your connections.</span></span> <span data-ttu-id="2600f-233">Consulte [Comprobación de las conexiones](#verify).</span><span class="sxs-lookup"><span data-stu-id="2600f-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="2600f-234"><a name="samerg"></a>tooconnect redes virtuales que residen en hello mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2600f-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="2600f-235">Crear hello TestVNet1 tooTestVNet4 conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="2600f-236">En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2600f-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="2600f-237">Grupos de recursos de Hola de aviso se Hola igual en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="2600f-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="2600f-238">También verá una clave compartida que se hace referencia en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="2600f-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="2600f-239">Puede utilizar sus propios valores de clave compartida de hello, sin embargo, debe coincidir con una clave compartida hello para ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="2600f-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="2600f-240">Crear una conexión, toma un valor bajo al toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2600f-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="2600f-241">Crear hello TestVNet4 tooTestVNet1 conexión.</span><span class="sxs-lookup"><span data-stu-id="2600f-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="2600f-242">Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="2600f-243">Asegúrese de que coincide con las claves de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="2600f-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="2600f-244">Tarda unos minutos en conexión de hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="2600f-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="2600f-245">Compruebe las conexiones.</span><span class="sxs-lookup"><span data-stu-id="2600f-245">Verify your connections.</span></span> <span data-ttu-id="2600f-246">Consulte [Comprobación de las conexiones](#verify).</span><span class="sxs-lookup"><span data-stu-id="2600f-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="2600f-247"><a name="difsub"></a>Conexión de redes virtuales que están en suscripciones diferentes</span><span class="sxs-lookup"><span data-stu-id="2600f-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![diagrama de v2v](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="2600f-249">En este escenario, conectaremos TestVNet1 y TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2600f-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="2600f-250">Hola redes virtuales residen distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="2600f-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="2600f-251">las suscripciones de Hello no es necesario toobe asociado con hello mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2600f-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="2600f-252">pasos de Hola para esta configuración de agregan una conexión de red virtual a red virtual adicional en orden tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2600f-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="2600f-253"><a name="TestVNet1diff"></a>Paso 5: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2600f-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="2600f-254">Seguir estas instrucciones de los pasos de hello en secciones anteriores de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="2600f-255">Debe completar [paso 1](#Connect) y [paso 2](#TestVNet1) toocreate TestVNet1 y configurar hello puerta de enlace VPN para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="2600f-256">Para esta configuración, no es necesario toocreate TestVNet4 desde la sección anterior de hello, aunque si lo creó, no estará en conflicto con estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2600f-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="2600f-257">Cuando haya completado el paso 1 y el 2, continúe con el paso 6 (a continuación).</span><span class="sxs-lookup"><span data-stu-id="2600f-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="2600f-258"><a name="verifyranges"></a>Paso 6: comprobar los intervalos de direcciones IP de Hola</span><span class="sxs-lookup"><span data-stu-id="2600f-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="2600f-259">Al crear conexiones adicionales, es importante tooverify que espacio de direcciones IP de saludo de la nueva red virtual de hello no se superponga con ninguno de los otros intervalos de VNet o intervalos de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="2600f-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="2600f-260">Para este ejercicio, puede usar Hola después de valores de hello TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="2600f-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="2600f-261">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="2600f-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="2600f-262">Nombre de red virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="2600f-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="2600f-263">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="2600f-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="2600f-264">Ubicación: Japón Oriental</span><span class="sxs-lookup"><span data-stu-id="2600f-264">Location: Japan East</span></span>
* <span data-ttu-id="2600f-265">TestVNet5: 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2600f-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="2600f-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="2600f-267">Backend: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2600f-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="2600f-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="2600f-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="2600f-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="2600f-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="2600f-270">Dirección IP pública: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="2600f-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="2600f-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2600f-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="2600f-272">Conexión: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="2600f-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="2600f-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2600f-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="2600f-274"><a name="TestVNet5"></a>Paso 7: Creación y configuración de TestVNet5</span><span class="sxs-lookup"><span data-stu-id="2600f-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="2600f-275">Este paso debe realizarse en el contexto de Hola de nueva suscripción hello, 5 de suscripción.</span><span class="sxs-lookup"><span data-stu-id="2600f-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="2600f-276">Administrador de hello en otra organización que posee la suscripción de hello puede realizar esta parte.</span><span class="sxs-lookup"><span data-stu-id="2600f-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="2600f-277">tooswitch entre el uso de suscripciones ' lista de cuentas de az--todos los ' toolist Hola cuenta tooyour disponibles de las suscripciones y luego use ' az cuenta conjunto--suscripción <subscriptionID>' tooswitch toohello suscripción que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="2600f-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="2600f-278">Asegúrese de que está conectado tooSubscription 5 y luego crea un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2600f-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="2600f-279">Cree TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2600f-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="2600f-280">Agregue subredes.</span><span class="sxs-lookup"><span data-stu-id="2600f-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="2600f-281">Agregar subred de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="2600f-282">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2600f-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="2600f-283">Crear puerta de enlace de hello TestVNet5</span><span class="sxs-lookup"><span data-stu-id="2600f-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="2600f-284"><a name="connections5"></a>Paso 8: crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="2600f-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="2600f-285">Dividiremos este paso en dos sesiones CLI marcados como **[1 suscripción]**, y **[suscripción 5]** porque son puertas de enlace de hello en distintas suscripciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="2600f-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="2600f-286">tooswitch entre el uso de suscripciones ' lista de cuentas de az--todos los ' toolist Hola cuenta tooyour disponibles de las suscripciones y luego use ' az cuenta conjunto--suscripción <subscriptionID>' tooswitch toohello suscripción que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="2600f-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="2600f-287">**[Suscripción 1]**  Iniciar sesión y conectarse tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="2600f-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="2600f-288">Siguiente ejecución Hola de comandos de nombre de hello tooget y el identificador del programa Hola a puerta de enlace de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="2600f-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="2600f-289">Copiar el resultado de hello para "Id.:".</span><span class="sxs-lookup"><span data-stu-id="2600f-289">Copy hello output for "id:".</span></span> <span data-ttu-id="2600f-290">Enviar identificador de Hola y el nombre de Hola de hello red virtual (VNet1GW) de la puerta de enlace toohello Administrador de 5 de la suscripción a través de correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="2600f-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="2600f-291">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2600f-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="2600f-292">**[Suscripción 5]**  Iniciar sesión y conectarse tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="2600f-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="2600f-293">Siguiente ejecución Hola de comandos de nombre de hello tooget y el identificador del programa Hola a puerta de enlace de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="2600f-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="2600f-294">Copiar el resultado de hello para "Id.:".</span><span class="sxs-lookup"><span data-stu-id="2600f-294">Copy hello output for "id:".</span></span> <span data-ttu-id="2600f-295">Enviar identificador de Hola y el nombre de Hola de hello red virtual (VNet5GW) de la puerta de enlace toohello Administrador de suscripción: 1 a través de correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="2600f-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="2600f-296">**[Suscripción 1]**  En este paso, crear conexión Hola de TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2600f-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="2600f-297">Puede utilizar sus propios valores de clave compartida de hello, sin embargo, debe coincidir con una clave compartida hello para ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="2600f-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="2600f-298">Crear una conexión puede tardar un poco al toocomplete.</span><span class="sxs-lookup"><span data-stu-id="2600f-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="2600f-299">Asegúrese de que se conecta tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="2600f-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="2600f-300">**[Suscripción 5]**  Este paso es toohello similar uno anterior, excepto que va a crear la conexión Hola de TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2600f-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="2600f-301">Asegúrese de que ese Hola compartidos coincidencia de claves y se conecta tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="2600f-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="2600f-302"><a name="verify"></a>Compruebe las conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="2600f-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="2600f-303"><a name="faq"></a>P+F sobre conexiones de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="2600f-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2600f-304">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2600f-304">Next steps</span></span>

* <span data-ttu-id="2600f-305">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="2600f-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="2600f-306">Para obtener más información, vea hello [documentación de máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="2600f-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="2600f-307">Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2600f-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
