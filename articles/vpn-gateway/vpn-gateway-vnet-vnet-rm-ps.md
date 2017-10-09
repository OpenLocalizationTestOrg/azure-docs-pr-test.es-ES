---
title: 'Conectar una red virtual de red virtual de Azure tooanother: PowerShell | Documentos de Microsoft'
description: "Este artículo le guiará para conectar redes virtuales entre sí por medio de PowerShell y el Administrador de recursos de Azure."
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
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="4fc42-103">Configuración de una conexión de VPN Gateway de red virtual a red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fc42-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="4fc42-104">Este artículo muestra cómo toocreate una conexión de puerta de enlace VPN entre redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4fc42-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="4fc42-105">Hello redes virtuales pueden estar en Hola mismo o en distintas regiones y de Hola iguales o distintas suscripciones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="4fc42-106">Al conectar redes virtuales de distintas suscripciones, las suscripciones de hello no es necesario toobe asociada Hola a mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fc42-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="4fc42-107">pasos de Hello en este artículo aplican el modelo de implementación del Administrador de recursos de toohello y usan PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fc42-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="4fc42-108">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="4fc42-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4fc42-109">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="4fc42-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="4fc42-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fc42-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="4fc42-111">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="4fc42-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="4fc42-112">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="4fc42-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="4fc42-113">Conexión de diferentes modelos de implementación - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4fc42-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="4fc42-114">Conexión de diferentes modelos de implementación - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fc42-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="4fc42-115">Conectar una red virtual (VNet a VNet) tooanother de red virtual es similar tooconnecting una ubicación de sitio de red virtual tooan local.</span><span class="sxs-lookup"><span data-stu-id="4fc42-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="4fc42-116">Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="4fc42-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="4fc42-117">Si sus redes virtuales están en hello misma región, puede que desee tooconsider conectándolos mediante el intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc42-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="4fc42-118">El emparejamiento de VNET no usa VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="4fc42-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="4fc42-119">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4fc42-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="4fc42-120">Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="4fc42-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="4fc42-121">Esto le permite establecer topologías de red que combinen la conectividad entre entornos con conectividad entre redes virtuales, como se muestra en hello siguiente diagrama:</span><span class="sxs-lookup"><span data-stu-id="4fc42-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Acerca de las conexiones](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="4fc42-123">¿Por qué debería conectarse a redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="4fc42-123">Why connect virtual networks?</span></span>

<span data-ttu-id="4fc42-124">Puede que desee tooconnect las redes virtuales para hello siguientes motivos:</span><span class="sxs-lookup"><span data-stu-id="4fc42-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="4fc42-125">**Presencia geográfica y redundancia geográfica entre regiones**</span><span class="sxs-lookup"><span data-stu-id="4fc42-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="4fc42-126">Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="4fc42-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="4fc42-127">Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc42-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="4fc42-128">Por ejemplo, puede tooset seguridad SQL Always On con grupos de disponibilidad a través de varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc42-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="4fc42-129">**Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**</span><span class="sxs-lookup"><span data-stu-id="4fc42-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="4fc42-130">Hola dentro mismo región, puede configurar aplicaciones de varios niveles con varias redes virtuales conectadas entre sí debido tooisolation o requisitos administrativos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="4fc42-131">Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="4fc42-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="4fc42-132">¿Qué serie de pasos debo seguir?</span><span class="sxs-lookup"><span data-stu-id="4fc42-132">Which set of steps should I use?</span></span>

<span data-ttu-id="4fc42-133">En este artículo, verá dos conjuntos de pasos diferentes.</span><span class="sxs-lookup"><span data-stu-id="4fc42-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="4fc42-134">Un conjunto de pasos para [redes virtuales que residen en Hola misma suscripción](#samesub)y otro para [redes virtuales que residen en distintas suscripciones](#difsub).</span><span class="sxs-lookup"><span data-stu-id="4fc42-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="4fc42-135">Hello diferencia clave entre conjuntos de hello es si puede crear y configurar todos los recursos de red y puerta de enlace virtuales dentro de hello misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fc42-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="4fc42-136">Hello pasos de este artículo utilizan variables que se declaran en principio Hola de cada sección.</span><span class="sxs-lookup"><span data-stu-id="4fc42-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="4fc42-137">Si ya está trabajando con redes virtuales existentes, modificar la configuración de Hola de hello variables tooreflect en su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="4fc42-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="4fc42-138">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4fc42-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="4fc42-139"><a name="samesub"></a>¿Cómo tooconnect redes virtuales que están en hello misma suscripción</span><span class="sxs-lookup"><span data-stu-id="4fc42-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="4fc42-141">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="4fc42-141">Before you begin</span></span>

<span data-ttu-id="4fc42-142">Antes de comenzar, necesita la versión más reciente de tooinstall Hola Hola Azure Resource Manager de cmdlets de PowerShell, por lo menos 4.0 o posteriores.</span><span class="sxs-lookup"><span data-stu-id="4fc42-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="4fc42-143">Para obtener más información acerca de cómo instalar los cmdlets de PowerShell de hello, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4fc42-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="4fc42-144"><a name="Step1"></a>Paso 1: Planeamiento de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="4fc42-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="4fc42-145">Hola pasos, se crea dos redes virtuales junto con sus subredes correspondientes de la puerta de enlace y las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="4fc42-146">Creamos, a continuación, una conexión VPN entre Hola dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="4fc42-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="4fc42-147">Es importante tooplan intervalos de direcciones IP de hello para la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="4fc42-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="4fc42-148">Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen.</span><span class="sxs-lookup"><span data-stu-id="4fc42-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="4fc42-149">En estos ejemplos, no se incluye ningún servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="4fc42-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="4fc42-150">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="4fc42-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="4fc42-151">Utilizamos Hola después los valores en los ejemplos de hello:</span><span class="sxs-lookup"><span data-stu-id="4fc42-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="4fc42-152">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="4fc42-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="4fc42-153">Nombre de red virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fc42-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="4fc42-154">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="4fc42-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="4fc42-155">Ubicación: Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="4fc42-155">Location: East US</span></span>
* <span data-ttu-id="4fc42-156">TestVNet1: 10.11.0.0/16 y 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fc42-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="4fc42-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="4fc42-158">Backend: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="4fc42-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4fc42-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="4fc42-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="4fc42-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="4fc42-161">Dirección IP pública: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="4fc42-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="4fc42-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fc42-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fc42-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="4fc42-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="4fc42-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="4fc42-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="4fc42-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fc42-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="4fc42-166">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="4fc42-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="4fc42-167">Nombre de red virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4fc42-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="4fc42-168">TestVNet2: 10.41.0.0/16 y 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fc42-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="4fc42-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="4fc42-170">Backend: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="4fc42-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="4fc42-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="4fc42-172">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="4fc42-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="4fc42-173">Ubicación: Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="4fc42-173">Location: West US</span></span>
* <span data-ttu-id="4fc42-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="4fc42-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="4fc42-175">Dirección IP pública: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="4fc42-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="4fc42-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fc42-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fc42-177">Conexión: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="4fc42-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="4fc42-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fc42-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="4fc42-179"><a name="Step2"></a>Paso 2: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fc42-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="4fc42-180">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="4fc42-180">Declare your variables.</span></span> <span data-ttu-id="4fc42-181">Este ejemplo declara las variables de hello con valores de hello para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="4fc42-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="4fc42-182">En la mayoría de los casos, debe reemplazar los valores de hello por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="4fc42-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="4fc42-183">Sin embargo, puede utilizar estas variables si está ejecutando a través de hello pasos toobecome familiarizado con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="4fc42-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="4fc42-184">Modificar variables de hello si es necesario, a continuación, copie y péguelos en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fc42-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="4fc42-185">Conectarse a tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="4fc42-185">Connect tooyour account.</span></span> <span data-ttu-id="4fc42-186">Usar hello después toohelp de ejemplo que se conecta:</span><span class="sxs-lookup"><span data-stu-id="4fc42-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4fc42-187">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="4fc42-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4fc42-188">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="4fc42-189">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="4fc42-190">Crear configuraciones de subred para TestVNet1 de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="4fc42-191">En este ejemplo se crea una red virtual denominada TestVNet1 y tres subredes llamadas: GatewaySubnet, FrontEnd y Backend.</span><span class="sxs-lookup"><span data-stu-id="4fc42-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="4fc42-192">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4fc42-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="4fc42-193">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="4fc42-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="4fc42-194">Hello en el ejemplo siguiente se usa variables de hello establecidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4fc42-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="4fc42-195">En este ejemplo, la subred de puerta de enlace de hello está usando un /27.</span><span class="sxs-lookup"><span data-stu-id="4fc42-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="4fc42-196">Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluye direcciones más si se selecciona al menos /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="4fc42-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="4fc42-197">Esto le permitirá suficientes direcciones tooaccommodate posibles configuraciones adicionales que puede querer en hello futuras.</span><span class="sxs-lookup"><span data-stu-id="4fc42-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="4fc42-198">Cree TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="4fc42-199">Solicitar una pública dirección toobe toohello asignado puerta de enlace IP que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc42-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="4fc42-200">Tenga en cuenta que hello AllocationMethod es dinámico.</span><span class="sxs-lookup"><span data-stu-id="4fc42-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="4fc42-201">No se puede especificar la dirección IP de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="4fc42-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="4fc42-202">Es puerta de enlace de tooyour asignada dinámicamente.</span><span class="sxs-lookup"><span data-stu-id="4fc42-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4fc42-203">Crear configuración de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-203">Create hello gateway configuration.</span></span> <span data-ttu-id="4fc42-204">configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="4fc42-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="4fc42-205">Use la configuración de puerta de enlace de toocreate de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="4fc42-206">Crear puerta de enlace de Hola para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="4fc42-207">En este paso, creará la puerta de enlace de red virtual de Hola para su TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="4fc42-208">Las configuraciones VNet a VNet requieren un VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="4fc42-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="4fc42-209">Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU.</span><span class="sxs-lookup"><span data-stu-id="4fc42-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="4fc42-210">Paso 3: Creación y configuración de TestVNet4</span><span class="sxs-lookup"><span data-stu-id="4fc42-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="4fc42-211">Una vez que haya configurado TestVNet1, cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fc42-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="4fc42-212">Siga los pasos de hello siguiente, reemplazando los valores de hello con su propio cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="4fc42-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="4fc42-213">Este paso puede realizarse en hello misma sesión de PowerShell porque está en Hola misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="4fc42-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="4fc42-214">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="4fc42-214">Declare your variables.</span></span> <span data-ttu-id="4fc42-215">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="4fc42-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="4fc42-216">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="4fc42-217">Crear configuraciones de subred para TestVNet4 de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="4fc42-218">Cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fc42-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="4fc42-219">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="4fc42-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="4fc42-220">Crear configuración de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="4fc42-221">Crear puerta de enlace de hello TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fc42-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="4fc42-222">Crear una puerta de enlace a menudo puede tardar 45 minutos o más, en función de puerta de enlace de hello seleccionado SKU.</span><span class="sxs-lookup"><span data-stu-id="4fc42-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="4fc42-223">Paso 4: crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="4fc42-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="4fc42-224">Obtenga ambas puertas de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="4fc42-224">Get both virtual network gateways.</span></span> <span data-ttu-id="4fc42-225">Si ambos de puertas de enlace de hello están en hello misma suscripción, tal como están en el ejemplo de Hola, puede completar este paso en hello misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4fc42-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="4fc42-226">Crear hello TestVNet1 tooTestVNet4 conexión.</span><span class="sxs-lookup"><span data-stu-id="4fc42-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="4fc42-227">En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="4fc42-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="4fc42-228">Verá una clave compartida que se hace referencia en los ejemplos de hello.</span><span class="sxs-lookup"><span data-stu-id="4fc42-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="4fc42-229">Puede utilizar sus propios valores de clave compartida de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="4fc42-230">Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="4fc42-231">Crear una conexión puede tardar un poco al toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4fc42-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="4fc42-232">Crear hello TestVNet4 tooTestVNet1 conexión.</span><span class="sxs-lookup"><span data-stu-id="4fc42-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="4fc42-233">Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="4fc42-234">Asegúrese de que coincide con las claves de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="4fc42-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="4fc42-235">se establecerá la conexión de Hello después de unos minutos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4fc42-236">Compruebe la conexión.</span><span class="sxs-lookup"><span data-stu-id="4fc42-236">Verify your connection.</span></span> <span data-ttu-id="4fc42-237">Consulte la sección de hello [cómo tooverify la conexión](#verify).</span><span class="sxs-lookup"><span data-stu-id="4fc42-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="4fc42-238"><a name="difsub"></a>¿Cómo tooconnect redes virtuales que se encuentran en distintas suscripciones</span><span class="sxs-lookup"><span data-stu-id="4fc42-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="4fc42-240">En este escenario, conectaremos TestVNet1 y TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="4fc42-241">TestVNet1 y TestVNet5 residen en suscripciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="4fc42-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="4fc42-242">las suscripciones de Hello no es necesario toobe asociado con hello mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fc42-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="4fc42-243">diferencia de Hello entre estos pasos y el conjunto anterior de hello es que algunos de los pasos de configuración de Hola necesitan toobe realizada en una sesión de PowerShell independiente en el contexto de Hola de suscripción segundo Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="4fc42-244">Sobre todo cuando las suscripciones de hello dos pertenecen toodifferent organizaciones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="4fc42-245">Paso 5: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="4fc42-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="4fc42-246">Debe completar [paso 1](#Step1) y [paso 2](#Step2) de hello anterior sección toocreate y configurar TestVNet1 Hola puerta de enlace VPN para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="4fc42-247">Para esta configuración, no es necesario toocreate TestVNet4 desde la sección anterior de hello, aunque si lo creó, no estará en conflicto con estos pasos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="4fc42-248">Cuando haya completado los pasos 1 y 2 de paso, continúe con el paso 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="4fc42-249">Paso 6: comprobar los intervalos de direcciones IP de Hola</span><span class="sxs-lookup"><span data-stu-id="4fc42-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="4fc42-250">Es importante toomake seguro de que el espacio de direcciones IP de Hola de hello nueva red virtual, TestVNet5, no se superponen con ninguno de los intervalos de VNet o intervalos de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="4fc42-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="4fc42-251">En este ejemplo, las redes virtuales Hola pueden pertenecer toodifferent organizaciones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="4fc42-252">Para este ejercicio, puede usar Hola después de valores de hello TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="4fc42-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="4fc42-253">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="4fc42-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="4fc42-254">Nombre de red virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4fc42-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="4fc42-255">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="4fc42-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="4fc42-256">Ubicación: Japón Oriental</span><span class="sxs-lookup"><span data-stu-id="4fc42-256">Location: Japan East</span></span>
* <span data-ttu-id="4fc42-257">TestVNet5: 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="4fc42-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="4fc42-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="4fc42-259">Backend: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="4fc42-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="4fc42-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="4fc42-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="4fc42-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="4fc42-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="4fc42-262">Dirección IP pública: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="4fc42-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="4fc42-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="4fc42-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="4fc42-264">Conexión: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="4fc42-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="4fc42-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="4fc42-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="4fc42-266">Paso 7: Creación y configuración de TestVNet5</span><span class="sxs-lookup"><span data-stu-id="4fc42-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="4fc42-267">Este paso debe realizarse en el contexto de Hola de suscripción nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="4fc42-268">Administrador de hello en otra organización que posee la suscripción de hello puede realizar esta parte.</span><span class="sxs-lookup"><span data-stu-id="4fc42-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="4fc42-269">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="4fc42-269">Declare your variables.</span></span> <span data-ttu-id="4fc42-270">Ser seguro tooreplace valores de hello con hello las que desea que toouse para la configuración.</span><span class="sxs-lookup"><span data-stu-id="4fc42-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="4fc42-271">Conectar toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-271">Connect toosubscription 5.</span></span> <span data-ttu-id="4fc42-272">Abra la consola de PowerShell y conectar con tooyour cuenta.</span><span class="sxs-lookup"><span data-stu-id="4fc42-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="4fc42-273">Usar hello después toohelp de ejemplo que conectarse:</span><span class="sxs-lookup"><span data-stu-id="4fc42-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="4fc42-274">Compruebe las suscripciones de hello para la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="4fc42-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="4fc42-275">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="4fc42-276">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4fc42-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="4fc42-277">Crear configuraciones de subred para TestVNet5 de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="4fc42-278">Cree TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="4fc42-279">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="4fc42-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="4fc42-280">Crear configuración de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="4fc42-281">Crear puerta de enlace de hello TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="4fc42-282">Paso 8: crear conexiones de Hola</span><span class="sxs-lookup"><span data-stu-id="4fc42-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="4fc42-283">En este ejemplo, dado que las puertas de enlace de hello están en distintas suscripciones hello, hemos dividiremos este paso en dos sesiones de PowerShell marcadas como [suscripción 1] y [suscripción 5].</span><span class="sxs-lookup"><span data-stu-id="4fc42-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="4fc42-284">**[Suscripción 1]**  Obtener puerta de enlace de red virtual de hello para la suscripción: 1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="4fc42-285">Inicie sesión y conectar tooSubscription 1 antes de ejecutar el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4fc42-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="4fc42-286">Copiar el resultado de hello de hello siguientes elementos y enviar estos administrador toohello de 5 de la suscripción a través de correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="4fc42-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="4fc42-287">Estos dos elementos tendrán valores toohello similar después de la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4fc42-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="4fc42-288">**[Suscripción 5]**  Obtener puerta de enlace de red virtual de Hola para 5 de suscripción.</span><span class="sxs-lookup"><span data-stu-id="4fc42-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="4fc42-289">Inicie sesión y conectar tooSubscription 5 antes de ejecutar el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4fc42-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="4fc42-290">Copiar el resultado de hello de hello siguientes elementos y enviar estos administrador toohello de suscripción: 1 a través de correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="4fc42-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="4fc42-291">Estos dos elementos tendrán valores toohello similar después de la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4fc42-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="4fc42-292">**[Suscripción 1]**  Crear conexión hello TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="4fc42-293">En este paso, se crea la conexión de Hola de TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="4fc42-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="4fc42-294">Hola diferencia es que vnet5gw $ no se puede obtener directamente porque está en una suscripción diferente.</span><span class="sxs-lookup"><span data-stu-id="4fc42-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="4fc42-295">Deberá toocreate un nuevo objeto de PowerShell con valores de hello comunicado entre el 1 de suscripción en hello los pasos descritos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4fc42-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="4fc42-296">Utilice el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4fc42-296">Use hello example below.</span></span> <span data-ttu-id="4fc42-297">Reemplace Hola nombre, identificador y una clave compartida con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="4fc42-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="4fc42-298">Hola importante que es esa clave compartida de hello debe coincidir en las dos conexiones.</span><span class="sxs-lookup"><span data-stu-id="4fc42-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="4fc42-299">Crear una conexión puede tardar un poco al toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4fc42-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="4fc42-300">Conectar tooSubscription 1 antes de ejecutar el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4fc42-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="4fc42-301">**[Suscripción 5]**  Crear conexión hello TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="4fc42-302">Este paso es similar toohello uno anterior, salvo que va a crear la conexión Hola de TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="4fc42-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="4fc42-303">Hola mismo proceso de creación de un objeto de PowerShell basado en valores de hello obtenidos en el 1 de la suscripción es válida aquí también.</span><span class="sxs-lookup"><span data-stu-id="4fc42-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="4fc42-304">En este paso, asegúrese de que coinciden con las claves de hello compartido.</span><span class="sxs-lookup"><span data-stu-id="4fc42-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="4fc42-305">Conectar tooSubscription 5 antes de ejecutar el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="4fc42-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="4fc42-306"><a name="verify"></a>¿Cómo tooverify una conexión</span><span class="sxs-lookup"><span data-stu-id="4fc42-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="4fc42-307"><a name="faq"></a>P+F sobre conexiones de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="4fc42-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4fc42-308">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4fc42-308">Next steps</span></span>

* <span data-ttu-id="4fc42-309">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="4fc42-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="4fc42-310">Vea hello [documentación de máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="4fc42-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="4fc42-311">Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4fc42-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
