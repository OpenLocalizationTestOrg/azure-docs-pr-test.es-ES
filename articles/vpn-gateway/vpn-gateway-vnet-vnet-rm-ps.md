---
title: "Conexión de una red virtual de Azure a otra red virtual: PowerShell | Microsoft Docs"
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
ms.openlocfilehash: 8c42c0046ccaa98c572134042fbbb7e883ef93c3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="2f5b2-103">Configuración de una conexión de VPN Gateway de red virtual a red virtual mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f5b2-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="2f5b2-104">En este artículo se explica cómo crear una conexión de VPN Gateway entre redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="2f5b2-105">Las redes virtuales pueden estar en la misma región o en distintas, así como pertenecer a una única suscripción o a varias.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="2f5b2-106">Al conectar redes virtuales de distintas suscripciones, estas no necesitan estar asociadas con el mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="2f5b2-107">Los pasos descritos en este artículo se aplican al modelo de implementación de Resource Manager y utilizan PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-107">The steps in this article apply to the Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="2f5b2-108">También se puede crear esta configuración con una herramienta o modelo de implementación distintos, mediante la selección de una opción diferente en la lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2f5b2-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2f5b2-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="2f5b2-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f5b2-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="2f5b2-111">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2f5b2-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="2f5b2-112">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="2f5b2-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="2f5b2-113">Conexión de diferentes modelos de implementación - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2f5b2-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="2f5b2-114">Conexión de diferentes modelos de implementación - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f5b2-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="2f5b2-115">La conexión de una red virtual a otra es muy parecida a la conexión de una red virtual a una ubicación de un sitio local.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="2f5b2-116">Ambos tipos de conectividad usan una puerta de enlace de VPN para proporcionar un túnel seguro con IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="2f5b2-117">Si las redes virtuales están en la misma región, podría pensar en conectarlas mediante emparejamiento de VNET.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="2f5b2-118">El emparejamiento de VNET no usa VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="2f5b2-119">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="2f5b2-120">Se puede combinar la comunicación entre redes virtuales con configuraciones de varios sitios.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="2f5b2-121">Esto permite establecer topologías de red que combinan la conectividad entre entornos locales con la conectividad entre redes virtuales, como se muestra en el diagrama siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Acerca de las conexiones](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="2f5b2-123">¿Por qué debería conectarse a redes virtuales?</span><span class="sxs-lookup"><span data-stu-id="2f5b2-123">Why connect virtual networks?</span></span>

<span data-ttu-id="2f5b2-124">Puede que desee conectar redes virtuales por las siguientes razones:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="2f5b2-125">**Presencia geográfica y redundancia geográfica entre regiones**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="2f5b2-126">Puede configurar su propia replicación geográfica o sincronización con conectividad segura sin recurrir a los puntos de conexión a Internet.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="2f5b2-127">Con el Equilibrador de carga y el Administrador de tráfico de Azure, puede configurar cargas de trabajo de alta disponibilidad con redundancia geográfica en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="2f5b2-128">Por ejemplo, puede configurar AlwaysOn de SQL con grupos de disponibilidad distribuidos en varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="2f5b2-129">**Aplicaciones regionales de niveles múltiples con aislamiento o un límite administrativo**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="2f5b2-130">Dentro de la misma región, se pueden configurar aplicaciones de niveles múltiples con varias redes virtuales conectadas entre sí para cumplir requisitos administrativos o de aislamiento.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="2f5b2-131">Para más información acerca de las conexiones de red virtual a red virtual, consulte [P+F sobre conexiones de red virtual a red virtual](#faq) al final de este artículo.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="2f5b2-132">¿Qué serie de pasos debo seguir?</span><span class="sxs-lookup"><span data-stu-id="2f5b2-132">Which set of steps should I use?</span></span>

<span data-ttu-id="2f5b2-133">En este artículo, verá dos conjuntos de pasos diferentes.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="2f5b2-134">Un conjunto de pasos para [redes virtuales que residen en la misma suscripción](#samesub) y otro para [redes virtuales que residen en suscripciones diferentes](#difsub).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="2f5b2-135">La diferencia clave entre ambos conjuntos es si se pueden crear y configurar todos los recursos de red virtual y puerta de enlace en la misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-135">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="2f5b2-136">Los pasos de este artículo utilizan variables que se declaran al principio de cada sección.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-136">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="2f5b2-137">Si ya trabaja con redes virtuales existentes, modifique las variables para reflejar la configuración de su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-137">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> <span data-ttu-id="2f5b2-138">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="2f5b2-139"><a name="samesub"></a>Conexión de redes virtuales que están en la misma suscripción</span><span class="sxs-lookup"><span data-stu-id="2f5b2-139"><a name="samesub"></a>How to connect VNets that are in the same subscription</span></span>

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="2f5b2-141">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="2f5b2-141">Before you begin</span></span>

<span data-ttu-id="2f5b2-142">Antes de comenzar, tiene que instalar la versión más reciente de los cmdlets de PowerShell de Azure Resource Manager, como mínimo 4.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-142">Before beginning, you need to install the latest version of the Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="2f5b2-143">Consulte [Instalación y configuración de Azure PowerShell](/powershell/azure/overview) para más información sobre cómo instalar los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-143">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="2f5b2-144"><a name="Step1"></a>Paso 1: Planeamiento de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="2f5b2-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="2f5b2-145">En los pasos siguientes, se crearán dos redes virtuales junto con sus subredes de puerta de enlace y configuraciones correspondientes.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-145">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="2f5b2-146">A continuación crearemos una conexión VPN entre las dos redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-146">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="2f5b2-147">Es importante planear los intervalos de direcciones IP para la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-147">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="2f5b2-148">Tenga en cuenta que hay que asegurarse de que ninguno de los intervalos de VNet o intervalos de red local se solapen.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="2f5b2-149">En estos ejemplos, no se incluye ningún servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="2f5b2-150">Si desea disponer de resolución de nombres en las redes virtuales, consulte [Resolución de nombres](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="2f5b2-151">En los ejemplos usamos los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-151">We use the following values in the examples:</span></span>

<span data-ttu-id="2f5b2-152">**Valores para TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="2f5b2-153">Nombre de red virtual: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="2f5b2-154">Grupo de recursos: TestRG1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="2f5b2-155">Ubicación: Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-155">Location: East US</span></span>
* <span data-ttu-id="2f5b2-156">TestVNet1: 10.11.0.0/16 y 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2f5b2-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="2f5b2-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="2f5b2-158">Backend: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="2f5b2-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="2f5b2-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="2f5b2-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="2f5b2-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="2f5b2-161">Dirección IP pública: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="2f5b2-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="2f5b2-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2f5b2-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="2f5b2-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="2f5b2-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="2f5b2-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="2f5b2-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="2f5b2-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2f5b2-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="2f5b2-166">**Valores para TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="2f5b2-167">Nombre de red virtual: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2f5b2-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="2f5b2-168">TestVNet2: 10.41.0.0/16 y 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2f5b2-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="2f5b2-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="2f5b2-170">Backend: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="2f5b2-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="2f5b2-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="2f5b2-172">Grupo de recursos: TestRG4</span><span class="sxs-lookup"><span data-stu-id="2f5b2-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="2f5b2-173">Ubicación: Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-173">Location: West US</span></span>
* <span data-ttu-id="2f5b2-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="2f5b2-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="2f5b2-175">Dirección IP pública: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="2f5b2-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="2f5b2-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2f5b2-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="2f5b2-177">Conexión: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="2f5b2-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2f5b2-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="2f5b2-179"><a name="Step2"></a>Paso 2: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="2f5b2-180">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-180">Declare your variables.</span></span> <span data-ttu-id="2f5b2-181">En este ejemplo se declaran las variables con los valores para este ejercicio.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-181">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="2f5b2-182">En la mayoría de los casos, deberá reemplazar los valores por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-182">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="2f5b2-183">No obstante, puede usar estas variables si está practicando los pasos para familiarizarse con este tipo de configuración.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-183">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="2f5b2-184">Si es necesario, modifique las variables y después cópielas y péguelas en la consola de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-184">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

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

2. <span data-ttu-id="2f5b2-185">Conéctese a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-185">Connect to your account.</span></span> <span data-ttu-id="2f5b2-186">Use el siguiente ejemplo para conectarse:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-186">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="2f5b2-187">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-187">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="2f5b2-188">Especifique la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-188">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="2f5b2-189">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="2f5b2-190">Cree las configuraciones de subred para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-190">Create the subnet configurations for TestVNet1.</span></span> <span data-ttu-id="2f5b2-191">En este ejemplo se crea una red virtual denominada TestVNet1 y tres subredes llamadas: GatewaySubnet, FrontEnd y Backend.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="2f5b2-192">Al reemplazar valores, es importante que siempre asigne el nombre GatewaySubnet a la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="2f5b2-193">Si usa otro, se produce un error al crear la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="2f5b2-194">El siguiente ejemplo usa las variables que estableció anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-194">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="2f5b2-195">En este ejemplo, la subred de la puerta de enlace está usando un /27.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-195">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="2f5b2-196">Aunque es posible crear una subred de puerta de enlace tan pequeña como /29, se recomienda que cree una subred mayor que incluya más direcciones seleccionando al menos /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-196">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="2f5b2-197">Esto permitirá suficientes direcciones para dar cabida a posibles configuraciones adicionales que desee en el futuro.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-197">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="2f5b2-198">Cree TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="2f5b2-199">Solicite que se asigne una dirección IP pública a la puerta de enlace que creará para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-199">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="2f5b2-200">Observe que AllocationMethod es dinámico.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-200">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="2f5b2-201">No puede especificar la dirección IP que desea usar.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-201">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="2f5b2-202">Se asigna dinámicamente a la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-202">It's dynamically allocated to your gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="2f5b2-203">Establezca la configuración de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-203">Create the gateway configuration.</span></span> <span data-ttu-id="2f5b2-204">La configuración de puerta de enlace define la subred y la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-204">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="2f5b2-205">Use el ejemplo para crear la configuración de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-205">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="2f5b2-206">Cree la puerta de enlace para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-206">Create the gateway for TestVNet1.</span></span> <span data-ttu-id="2f5b2-207">En este paso, creará la puerta de enlace de red virtual para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-207">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="2f5b2-208">Las configuraciones VNet a VNet requieren un VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="2f5b2-209">La creación de una puerta de enlace suele tardar 45 minutos o más, según la SKU de la puerta de enlace seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-209">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="2f5b2-210">Paso 3: Creación y configuración de TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2f5b2-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="2f5b2-211">Una vez que haya configurado TestVNet1, cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="2f5b2-212">Siga los pasos a continuación y reemplace los valores por los suyos propios cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-212">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="2f5b2-213">Este paso puede realizarse en la misma sesión de PowerShell porque está en la misma suscripción.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-213">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="2f5b2-214">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-214">Declare your variables.</span></span> <span data-ttu-id="2f5b2-215">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="2f5b2-216">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="2f5b2-217">Cree las configuraciones de subred para TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-217">Create the subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="2f5b2-218">Cree TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="2f5b2-219">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="2f5b2-220">Establezca la configuración de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-220">Create the gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="2f5b2-221">Creación de la puerta de enlace de TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-221">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="2f5b2-222">La creación de una puerta de enlace suele tardar 45 minutos o más, según la SKU de la puerta de enlace seleccionada.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-222">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-the-connections"></a><span data-ttu-id="2f5b2-223">Paso 4: Creación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="2f5b2-223">Step 4 - Create the connections</span></span>

1. <span data-ttu-id="2f5b2-224">Obtenga ambas puertas de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-224">Get both virtual network gateways.</span></span> <span data-ttu-id="2f5b2-225">Si ambas están en la misma suscripción, como en el ejemplo, puede completar este paso en la misma sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-225">If both of the gateways are in the same subscription, as they are in the example, you can complete this step in the same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="2f5b2-226">Cree la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-226">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="2f5b2-227">En este paso, creará la conexión de TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-227">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="2f5b2-228">Verá una clave compartida a la que se hace referencia en los ejemplos.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-228">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="2f5b2-229">Puede utilizar sus propios valores para la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-229">You can use your own values for the shared key.</span></span> <span data-ttu-id="2f5b2-230">Lo importante es que la clave compartida coincida en ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-230">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="2f5b2-231">Se tardará unos momentos en terminar de crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-231">Creating a connection can take a short while to complete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="2f5b2-232">Cree la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-232">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="2f5b2-233">Este paso es similar al anterior, salvo en que se crea la conexión de TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-233">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="2f5b2-234">Asegúrese de que coincidan las claves compartidas.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-234">Make sure the shared keys match.</span></span> <span data-ttu-id="2f5b2-235">Después de unos minutos, se habrá establecido la conexión.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-235">The connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="2f5b2-236">Compruebe la conexión.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-236">Verify your connection.</span></span> <span data-ttu-id="2f5b2-237">Consulte la sección [Comprobación de la conexión](#verify).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-237">See the section [How to verify your connection](#verify).</span></span>

## <span data-ttu-id="2f5b2-238"><a name="difsub"></a>Conexión de redes virtuales que están en suscripciones diferentes</span><span class="sxs-lookup"><span data-stu-id="2f5b2-238"><a name="difsub"></a>How to connect VNets that are in different subscriptions</span></span>

![diagrama de v2v](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="2f5b2-240">En este escenario, conectaremos TestVNet1 y TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="2f5b2-241">TestVNet1 y TestVNet5 residen en suscripciones diferentes.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="2f5b2-242">Las suscripciones no necesitan estar asociadas con el mismo inquilino de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-242">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="2f5b2-243">La diferencia entre estos pasos y el conjunto anterior es que parte de los pasos de configuración se deben realizar en una sesión de PowerShell distinta en el contexto de la segunda suscripción.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-243">The difference between these steps and the previous set is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="2f5b2-244">Especialmente cuando las dos suscripciones pertenecen a distintas organizaciones.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-244">Especially when the two subscriptions belong to different organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="2f5b2-245">Paso 5: Creación y configuración de TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="2f5b2-246">Tiene que completar el [paso 1](#Step1) y el [paso 2](#Step2) de la sección anterior para crear y configurar TestVNet1 y la puerta de enlace de VPN para TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from the previous section to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="2f5b2-247">Para esta configuración, no se necesita crear TestVNet4 de la sección anterior, aunque, si la creó, no entrará en conflicto con estos pasos.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-247">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="2f5b2-248">Cuando haya completado el paso 1 y el 2, continúe con el paso 6 para crear TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-248">Once you complete Step 1 and Step 2, continue with Step 6 to create TestVNet5.</span></span> 

### <a name="step-6---verify-the-ip-address-ranges"></a><span data-ttu-id="2f5b2-249">Paso 6: Comprobación de los intervalos de direcciones IP</span><span class="sxs-lookup"><span data-stu-id="2f5b2-249">Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="2f5b2-250">Es importante asegurarse de que el espacio de direcciones IP de la red virtual nueva, TestVNet5, no se solape con ninguno de los intervalos de red virtual o de puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-250">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="2f5b2-251">En este ejemplo, las redes virtuales pueden pertenecer a distintas organizaciones.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-251">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="2f5b2-252">En este ejercicio, use los siguientes valores para TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-252">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="2f5b2-253">**Valores para TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="2f5b2-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="2f5b2-254">Nombre de red virtual: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="2f5b2-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="2f5b2-255">Grupo de recursos: TestRG5</span><span class="sxs-lookup"><span data-stu-id="2f5b2-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="2f5b2-256">Ubicación: Japón Oriental</span><span class="sxs-lookup"><span data-stu-id="2f5b2-256">Location: Japan East</span></span>
* <span data-ttu-id="2f5b2-257">TestVNet5: 10.51.0.0/16 y 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="2f5b2-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="2f5b2-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="2f5b2-259">Backend: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="2f5b2-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="2f5b2-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="2f5b2-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="2f5b2-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="2f5b2-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="2f5b2-262">Dirección IP pública: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="2f5b2-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="2f5b2-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="2f5b2-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="2f5b2-264">Conexión: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="2f5b2-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="2f5b2-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="2f5b2-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="2f5b2-266">Paso 7: Creación y configuración de TestVNet5</span><span class="sxs-lookup"><span data-stu-id="2f5b2-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="2f5b2-267">Este paso debe realizarse en el contexto de la nueva suscripción.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-267">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="2f5b2-268">Es posible que esta parte la realice el administrador de otra organización que posea la suscripción.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-268">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="2f5b2-269">Declare las variables.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-269">Declare your variables.</span></span> <span data-ttu-id="2f5b2-270">Asegúrese de reemplazar los valores por los que desea usar para su configuración.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-270">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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
2. <span data-ttu-id="2f5b2-271">Conéctese con la suscripción 5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-271">Connect to subscription 5.</span></span> <span data-ttu-id="2f5b2-272">Abre la consola de PowerShell y conéctate a tu cuenta.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-272">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="2f5b2-273">Use el siguiente ejemplo para ayudarle a conectarse:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-273">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="2f5b2-274">Compruebe las suscripciones para la cuenta.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-274">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="2f5b2-275">Especifique la suscripción que desea usar.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-275">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="2f5b2-276">Cree un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="2f5b2-277">Cree las configuraciones de subred para TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-277">Create the subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="2f5b2-278">Cree TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="2f5b2-279">Pida una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="2f5b2-280">Establezca la configuración de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-280">Create the gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="2f5b2-281">Cree la puerta de enlace de TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-281">Create the TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-the-connections"></a><span data-ttu-id="2f5b2-282">Paso 8: Creación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="2f5b2-282">Step 8 - Create the connections</span></span>

<span data-ttu-id="2f5b2-283">En este ejemplo, como las puertas de enlace están en suscripciones diferentes, hemos dividido el paso en dos sesiones de PowerShell marcadas como [Suscripción 1] y [Suscripción 5].</span><span class="sxs-lookup"><span data-stu-id="2f5b2-283">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="2f5b2-284">**[Suscripción 1]** Obtenga la puerta de enlace de red virtual para la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-284">**[Subscription 1]** Get the virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="2f5b2-285">Inicie sesión y conéctese a Suscripción 1 antes de ejecutar el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-285">Log in and connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="2f5b2-286">Copie la salida de los siguientes elementos y envíesela al administrador de la suscripción 5 por correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-286">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="2f5b2-287">Estos dos elementos tendrán valores similares a la salida de ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-287">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="2f5b2-288">**[Suscripción 5]** Obtenga la puerta de enlace de red virtual para la suscripción 5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-288">**[Subscription 5]** Get the virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="2f5b2-289">Inicie sesión y conéctese a Suscripción 5 antes de ejecutar el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-289">Log in and connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="2f5b2-290">Copie la salida de los siguientes elementos y envíesela al administrador de la suscripción 1 por correo electrónico u otro método.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-290">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="2f5b2-291">Estos dos elementos tendrán valores similares a la salida de ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-291">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="2f5b2-292">**[Suscripción 1]** Cree la conexión entre TestVNet1 y TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-292">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection.</span></span> <span data-ttu-id="2f5b2-293">En este paso, creará la conexión de TestVNet1 a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-293">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="2f5b2-294">La diferencia en este caso es que no se puede obtener $vnet5gw directamente porque está en una suscripción diferente.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-294">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="2f5b2-295">Debe crear un nuevo objeto de PowerShell con los valores que se le hayan proporcionado para la suscripción 1 en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-295">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="2f5b2-296">Use el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-296">Use the example below.</span></span> <span data-ttu-id="2f5b2-297">Reemplace el nombre (Name), el identificador (Id) y la clave compartida por sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-297">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="2f5b2-298">Lo importante es que la clave compartida coincida en ambas conexiones.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-298">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="2f5b2-299">Se tardará unos momentos en terminar de crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-299">Creating a connection can take a short while to complete.</span></span>

  <span data-ttu-id="2f5b2-300">Conéctese a Suscripción 1 antes de ejecutar el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-300">Connect to Subscription 1 before running the following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="2f5b2-301">**[Suscripción 5]** Cree la conexión entre TestVNet5 y TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-301">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection.</span></span> <span data-ttu-id="2f5b2-302">Este paso es similar al anterior, salvo en que se crea la conexión de TestVNet5 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-302">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="2f5b2-303">Aquí también se aplica el mismo proceso de creación de un objeto de PowerShell basándose en los valores obtenidos de la suscripción 1.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-303">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="2f5b2-304">En este paso, asegúrese de que las claves compartidas coincidan.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-304">In this step, be sure that the shared keys match.</span></span>

  <span data-ttu-id="2f5b2-305">Conéctese a Suscripción 5 antes de ejecutar el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2f5b2-305">Connect to Subscription 5 before running the following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="2f5b2-306"><a name="verify"></a>Comprobación de una conexión</span><span class="sxs-lookup"><span data-stu-id="2f5b2-306"><a name="verify"></a>How to verify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="2f5b2-307"><a name="faq"></a>P+F sobre conexiones de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="2f5b2-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="2f5b2-308">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2f5b2-308">Next steps</span></span>

* <span data-ttu-id="2f5b2-309">Una vez completada la conexión, puede agregar máquinas virtuales a las redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-309">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="2f5b2-310">Consulte la [documentación sobre máquinas virtuales](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.</span><span class="sxs-lookup"><span data-stu-id="2f5b2-310">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="2f5b2-311">Para más información acerca de BGP, consulte [Información general de BGP](vpn-gateway-bgp-overview.md) y [Configuración de BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b2-311">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>