---
title: 'Conectar su tooan de red local red virtual de Azure: VPN de sitio a sitio: CLI | Documentos de Microsoft'
description: "Una conexión de IPsec desde el entorno local de red tooan red virtual de Azure a través de toocreate de pasos Hola Internet pública. Estos pasos le ayudarán a crear una conexión de VPN Gateway de sitio a sitio entre locales mediante la CLI."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="c2d2f-104">Creación de una red virtual con una conexión VPN de sitio a sitio mediante la CLI</span><span class="sxs-lookup"><span data-stu-id="c2d2f-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="c2d2f-105">Este artículo muestra cómo toouse hello Azure CLI toocreate una conexión de puerta de enlace VPN de sitio a sitio desde su toohello de red local red virtual.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="c2d2f-106">pasos de Hello en este artículo aplican toohello modelo de implementación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c2d2f-107">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2d2f-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c2d2f-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c2d2f-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2d2f-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c2d2f-110">CLI</span><span class="sxs-lookup"><span data-stu-id="c2d2f-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c2d2f-111">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="c2d2f-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagrama de la conexión entre locales de VPN Gateway de sitio a sitio](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="c2d2f-113">Una conexión de puerta de enlace VPN de sitio a sitio es tooconnect utilizado en sus instalaciones de red tooan red virtual de Azure a través de un túnel VPN de IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c2d2f-114">Este tipo de conexión requiere una VPN dispositivo situado en local que tiene un tooit de dirección asignada de IP pública con orientación externa.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="c2d2f-115">Para más información acerca de las puertas de enlace VPN, consulte [Acerca de VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c2d2f-116">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="c2d2f-116">Before you begin</span></span>

<span data-ttu-id="c2d2f-117">Compruebe que se ha cumplido hello siguiendo criterios antes de comenzar la configuración:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="c2d2f-118">Asegúrese de que tiene un dispositivo VPN compatible y alguna persona tooconfigure capaz de él.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c2d2f-119">Para más información acerca de los dispositivos VPN compatibles y su configuración, consulte [Acerca de los dispositivos VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c2d2f-120">Compruebe que tiene una dirección IPv4 pública externa para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c2d2f-121">Esta dirección IP no puede estar detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c2d2f-122">Si no está familiarizado con intervalos de direcciones IP de hello ubicados en configuración de red local, deberá toocoordinate con alguien que pueda proporcionarle estos detalles para usted.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c2d2f-123">Al crear esta configuración, debe especificar prefijos para intervalo de direcciones IP con hello que Azure enrutará la ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="c2d2f-124">Ninguna de las subredes de saludo de la red local puede enumerar sobre el regazo con subredes de red virtual de Hola que desee tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="c2d2f-125">Compruebe que ha instalado una versión más reciente de los comandos de CLI de hello (2.0 o posteriores).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="c2d2f-126">Para obtener información acerca de cómo instalar los comandos de CLI de hello, consulte [instalar Azure CLI 2.0](/cli/azure/install-azure-cli) y [empezar a trabajar con Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="c2d2f-127"><a name="example"></a>Valores del ejemplo</span><span class="sxs-lookup"><span data-stu-id="c2d2f-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c2d2f-128">Puede usar hello después valores toocreate un entorno de prueba, o consultar valores toothese toobetter comprender los ejemplos de hello en este artículo:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="c2d2f-129"><a name="Login"></a>1. Conectar tooyour suscripción</span><span class="sxs-lookup"><span data-stu-id="c2d2f-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="c2d2f-130"><a name="rg"></a>2. Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c2d2f-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="c2d2f-131">Hello en el ejemplo siguiente se crea un grupo de recursos con el nombre 'TestRG1' en la ubicación de hello 'eastus'.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="c2d2f-132">Si ya tiene un grupo de recursos en la región de Hola que deseas toocreate la red virtual, puede usar en su lugar que uno.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="c2d2f-133"><a name="VNet"></a>3. Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="c2d2f-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="c2d2f-134">Si ya no tiene una red virtual, cree uno mediante hello [crear red virtual de red az](/cli/azure/network/vnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="c2d2f-135">Al crear una red virtual, asegúrese de que los espacios de direcciones de hello especificados no superponen con cualquiera de los espacios de direcciones de Hola que existen en la red local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="c2d2f-136">Hello en el ejemplo siguiente se crea una red virtual con el nombre de una subred, 'Subred1' y 'TestVNet1'.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="c2d2f-137">4. <a name="gwsub"></a>Crear una subred de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="c2d2f-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="c2d2f-138">Para esta configuración, también es necesaria una subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="c2d2f-139">puerta de enlace de red virtual de Hello usa una subred de puerta de enlace que contiene direcciones IP de Hola que usan servicios de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="c2d2f-140">Cuando se crea una subred de la puerta de enlace, debe tener el nombre 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="c2d2f-141">Si le asigna otro nombre, crea una subred, pero Azure no la tratará como subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="c2d2f-142">tamaño de Hola de subred de puerta de enlace de Hola que especifique depende en configuración de puerta de enlace VPN de Hola que desea toocreate.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="c2d2f-143">Aunque es posible toocreate una subred de puerta de enlace tan pequeña como /29, le recomendamos que cree una subred mayor que incluya más direcciones seleccionando /27 o /28.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="c2d2f-144">Mediante una subred de puerta de enlace mayor permite suficiente IP direcciones tooaccommodate futuras configuraciones posibles.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="c2d2f-145">Hola de uso [crear subredes de red virtual de red az](/cli/azure/network/vnet/subnet#create) subred de puerta de enlace de comando toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="c2d2f-146"><a name="localnet"></a>5. Crear puerta de enlace de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="c2d2f-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="c2d2f-147">puerta de enlace de red local de Hello suele hacer referencia a ubicación de tooyour local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="c2d2f-148">Se asigne un nombre mediante el cual Azure puede consulte tooit y luego especifique la dirección IP de Hola a sitio Hola de hello local VPN dispositivo toowhich creará una conexión.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="c2d2f-149">También especificar prefijos de direcciones IP de Hola que se enrutará a través del dispositivo VPN de toohello de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="c2d2f-150">Especifique los prefijos de direcciones Hola son prefijos de hello ubicados en la red local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="c2d2f-151">Si cambia su red local, puede actualizar fácilmente los prefijos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="c2d2f-152">Usar hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-152">Use hello following values:</span></span>

* <span data-ttu-id="c2d2f-153">Hola *--dirección de ip de puerta de enlace* es la dirección IP de hello de dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c2d2f-154">El dispositivo VPN no se encuentra detrás de un NAT.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c2d2f-155">Hola *--prefijos de direcciones local* son espacios de direcciones de sus instalaciones.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="c2d2f-156">Hola de uso [crear az red local puerta de enlace](/cli/azure/network/local-gateway#create) comando tooadd una puerta de enlace de red local con varios prefijos de direcciones:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="c2d2f-157"><a name="PublicIP"></a>6. Solicite una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="c2d2f-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="c2d2f-158">Una puerta de enlace VPN debe tener una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c2d2f-159">Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="c2d2f-160">dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="c2d2f-161">Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c2d2f-162">No se puede solicitar una asignación de direcciones IP públicas estáticas.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c2d2f-163">Sin embargo, esto no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="c2d2f-164">cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="c2d2f-165">No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c2d2f-166">Hola de uso [crear az red public-ip](/cli/azure/network/public-ip#create) comando toorequest una dirección IP pública dinámica.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="c2d2f-167"><a name="CreateGateway"></a>7. Crear puerta de enlace VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="c2d2f-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="c2d2f-168">Crear puerta de enlace VPN de red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="c2d2f-169">Crear una puerta de enlace VPN puede tardar hasta too45 minutos o más toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="c2d2f-170">Usar hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-170">Use hello following values:</span></span>

* <span data-ttu-id="c2d2f-171">Hola *: tipo de puerta de enlace* para un sitio a sitio es configuración *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c2d2f-172">tipo de puerta de enlace de Hello siempre es configuración toohello específico que va a implementar.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="c2d2f-173">Para más información, consulte [Tipos de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="c2d2f-174">Hola *--vpn-type* puede ser *RouteBased* (llamada tooas una puerta de enlace dinámico en algunos documentos), o *PolicyBased* (denominada tooas una puerta de enlace estática en algunos documentación).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="c2d2f-175">saludo es toorequirements específico del dispositivo de Hola que se va a conectar.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="c2d2f-176">Para más información sobre los tipos de puertas de enlace de VPN, consulte [Acerca de la información de VPN Gateway](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="c2d2f-177">Seleccione Hola SKU de puerta de enlace que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="c2d2f-178">Hay limitaciones de configuración para determinadas SKU.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c2d2f-179">Consulte [SKU de puertas de enlace](vpn-gateway-about-vpn-gateway-settings.md#gwsku) para más información.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="c2d2f-180">Crear puerta de enlace VPN de hello con hello [crear enlace de red virtual de red az](/cli/azure/network/vnet-gateway#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="c2d2f-181">Si ejecuta este comando usando hello '--sin - wait' parámetro, no ve los comentarios o la salida.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="c2d2f-182">Este parámetro permite toocreate de puerta de enlace de hello en segundo plano de Hola.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="c2d2f-183">Tardará aproximadamente 45 minutos toocreate una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="c2d2f-184"><a name="VPNDevice"></a>8. Configurar el dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="c2d2f-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="c2d2f-185">Red local de las conexiones de sitio a sitio tooan requieren un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="c2d2f-186">En este paso, se configura el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c2d2f-187">Al configurar el dispositivo VPN, necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2d2f-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="c2d2f-188">Una clave compartida.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-188">A shared key.</span></span> <span data-ttu-id="c2d2f-189">Esto es Hola mismo compartido clave que se especifique al crear la conexión VPN de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c2d2f-190">En estos ejemplos se utiliza una clave compartida básica.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c2d2f-191">Se recomienda que generar un toouse clave más compleja.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="c2d2f-192">Hola dirección IP pública de la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c2d2f-193">Puede ver la dirección IP pública hello mediante Hola portal de Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c2d2f-194">dirección IP toofind Hola pública de la puerta de enlace de red virtual, use hello [lista de ip pública de red az](/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="c2d2f-195">Para facilitar la lectura, la salida de hello es toodisplay con formato de lista de Hola de direcciones IP públicas en formato de tabla.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c2d2f-196"><a name="CreateConnection"></a>9. Crear la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="c2d2f-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="c2d2f-197">Crear la conexión de VPN de sitio a sitio Hola entre la puerta de enlace de red virtual y el dispositivo VPN local.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="c2d2f-198">Preste especial atención toohello compartido valor de clave, que debe coincidir con hello configurado comparte el valor de clave para el dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="c2d2f-199">Crear conexión de hello mediante hello [crear conexión de vpn de red az](/cli/azure/network/vpn-connection#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="c2d2f-200">Después de un valor bajo al Hola se establecerá la conexión.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="c2d2f-201"><a name="toverify"></a>10. Compruebe la conexión de VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="c2d2f-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="c2d2f-202">Si desea toouse tooverify de otro método la conexión, consulte [comprobar una conexión de puerta de enlace VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="c2d2f-203"><a name="connectVM"></a>máquina virtual de tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="c2d2f-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="c2d2f-204"><a name="tasks"></a>Tareas comunes</span><span class="sxs-lookup"><span data-stu-id="c2d2f-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="c2d2f-205">Esta sección contiene comandos comunes que son útiles al trabajar con configuraciones de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="c2d2f-206">Para hello lista completa de los comandos de red de CLI, consulte [CLI de Azure - red](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c2d2f-207">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2d2f-207">Next steps</span></span>

* <span data-ttu-id="c2d2f-208">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c2d2f-209">Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.</span><span class="sxs-lookup"><span data-stu-id="c2d2f-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c2d2f-210">Para obtener información sobre BGP, consulte hello [información general de BGP](vpn-gateway-bgp-overview.md) y [cómo tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="c2d2f-211">Para más información acerca de la tunelización forzada, consulte la [información acerca de la tunelización forzada](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="c2d2f-212">Para obtener información acerca de las conexiones activo/activo de alta disponibilidad, consulte [Conectividad de alta disponibilidad entre locales y de red virtual a red virtual](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="c2d2f-213">Para obtener una lista de comandos de red de la CLI de Azure, consulte [Networking - az network](https://docs.microsoft.com/cli/azure/network) (Redes: az network).</span><span class="sxs-lookup"><span data-stu-id="c2d2f-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>