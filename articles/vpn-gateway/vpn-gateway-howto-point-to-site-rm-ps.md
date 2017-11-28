---
title: "Conectar una red virtual de Azure con Point-to-Site tooan de equipo y la autenticación de certificados: PowerShell | Documentos de Microsoft"
description: "Conectarse de forma segura una red virtual de tooyour de equipo mediante la creación de una conexión de puerta de enlace de Point-to-Site VPN mediante la autenticación de certificado. En este artículo se aplica el modelo de implementación del Administrador de recursos de toohello y usa PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a><span data-ttu-id="bb204-104">Configurar una tooa de conexión de punto a sitio red virtual mediante la autenticación de certificado: PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb204-104">Configure a Point-to-Site connection tooa VNet using certificate authentication: PowerShell</span></span>

<span data-ttu-id="bb204-105">Este artículo muestra cómo toocreate una red virtual con una conexión de punto a sitio en la implementación del Administrador de recursos de hello modelar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb204-105">This article shows you how toocreate a VNet with a Point-to-Site connection in hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="bb204-106">Esta configuración utiliza Hola de tooauthenticate certificados conecta el cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-106">This configuration uses certificates tooauthenticate hello connecting client.</span></span> <span data-ttu-id="bb204-107">También puede crear esta configuración con una herramienta de implementación diferentes o un modelo de implementación seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb204-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb204-108">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bb204-108">Azure portal</span></span>](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="bb204-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb204-109">PowerShell</span></span>](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [<span data-ttu-id="bb204-110">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="bb204-110">Azure portal (classic)</span></span>](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

<span data-ttu-id="bb204-111">Una puerta de enlace VPN de punto a sitio (P2S) le permite crear una red virtual de tooyour de conexión segura desde un equipo cliente individual.</span><span class="sxs-lookup"><span data-stu-id="bb204-111">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="bb204-112">Las conexiones de VPN de sitio a punto son útiles cuando se desea tooconnect tooyour red virtual desde una ubicación remota, como cuando trabajan a distancia desde casa o una conferencia.</span><span class="sxs-lookup"><span data-stu-id="bb204-112">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="bb204-113">Una VPN P2S también es un toouse solución útil en lugar de una VPN de sitio a sitio cuando hay solo unos clientes que necesitan tooconnect tooa red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-113">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span>

<span data-ttu-id="bb204-114">Usa P2S Hola Secure Socket de protocolo de túnel (SSTP), que es un protocolo VPN basada en SSL.</span><span class="sxs-lookup"><span data-stu-id="bb204-114">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="bb204-115">Se establece una conexión VPN P2S, empiece por equipo de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-115">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Conectar una red virtual de Azure - diagrama de sitio de punto de conexión de equipo tooan](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

<span data-ttu-id="bb204-117">Las conexiones de autenticación de certificado de punto a sitio requieren siguientes de hello:</span><span class="sxs-lookup"><span data-stu-id="bb204-117">Point-to-Site certificate authentication connections require hello following:</span></span>

* <span data-ttu-id="bb204-118">Una puerta de enlace de VPN RouteBased.</span><span class="sxs-lookup"><span data-stu-id="bb204-118">A RouteBased VPN gateway.</span></span>
* <span data-ttu-id="bb204-119">Hola clave pública (archivo .cer) para un certificado raíz, que es cargado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb204-119">hello public key (.cer file) for a root certificate, which is uploaded tooAzure.</span></span> <span data-ttu-id="bb204-120">Una vez cargado el certificado de hello, se considera un certificado de confianza y se utiliza para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="bb204-120">Once hello certificate is uploaded, it is considered a trusted certificate and is used for authentication.</span></span>
* <span data-ttu-id="bb204-121">Un certificado de cliente que se genera a partir de certificado de raíz de Hola e instalado en cada equipo cliente que se conectará toohello red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-121">A client certificate that is generated from hello root certificate and installed on each client computer that will connect toohello VNet.</span></span> <span data-ttu-id="bb204-122">Este certificado se usa para la autenticación de cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-122">This certificate is used for client authentication.</span></span>
* <span data-ttu-id="bb204-123">Un paquete de configuración de cliente de VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-123">A VPN client configuration package.</span></span> <span data-ttu-id="bb204-124">paquete de configuración de cliente VPN de Hello contiene información necesaria de Hola para hello cliente tooconnect toohello red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-124">hello VPN client configuration package contains hello necessary information for hello client tooconnect toohello VNet.</span></span> <span data-ttu-id="bb204-125">paquete de Hello configura el cliente VPN existente hello es nativo toohello sistema operativo Windows.</span><span class="sxs-lookup"><span data-stu-id="bb204-125">hello package configures hello existing VPN client that is native toohello Windows operating system.</span></span> <span data-ttu-id="bb204-126">Cada cliente que se conecta debe configurarse mediante el paquete de configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-126">Each client that connects must be configured using hello configuration package.</span></span>

<span data-ttu-id="bb204-127">Las conexiones de punto a sitio no requieren un dispositivo VPN ni una dirección IP de acceso público local.</span><span class="sxs-lookup"><span data-stu-id="bb204-127">Point-to-Site connections do not require a VPN device or an on-premises public-facing IP address.</span></span> <span data-ttu-id="bb204-128">Hola conexión VPN se crea a través de SSTP (Protocolo de túnel de sockets de seguros).</span><span class="sxs-lookup"><span data-stu-id="bb204-128">hello VPN connection is created over SSTP (Secure Socket Tunneling Protocol).</span></span> <span data-ttu-id="bb204-129">En el lado del servidor hello, se admiten las versiones 1.0, 1.1 y 1.2 de SSTP.</span><span class="sxs-lookup"><span data-stu-id="bb204-129">On hello server side, we support SSTP versions 1.0, 1.1, and 1.2.</span></span> <span data-ttu-id="bb204-130">cliente de Hello decide qué toouse de versión.</span><span class="sxs-lookup"><span data-stu-id="bb204-130">hello client decides which version toouse.</span></span> <span data-ttu-id="bb204-131">Para Windows 8.1 y versiones posteriores, SSTP usa 1.2 de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="bb204-131">For Windows 8.1 and above, SSTP uses 1.2 by default.</span></span> 

<span data-ttu-id="bb204-132">Para obtener más información acerca de las conexiones punto a sitio, vea hello [Point-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bb204-132">For more information about Point-to-Site connections, see hello [Point-to-Site FAQ](#faq) at hello end of this article.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="bb204-133">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="bb204-133">Before beginning</span></span>

* <span data-ttu-id="bb204-134">Compruebe que tiene una suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-134">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="bb204-135">Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) o registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="bb204-135">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="bb204-136">Instalar versión más reciente de Hola de hello cmdlets de PowerShell del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-136">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="bb204-137">Para obtener más información acerca de cómo instalar los cmdlets de PowerShell, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bb204-137">For more information about installing PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="bb204-138"><a name="example"></a>Valores del ejemplo</span><span class="sxs-lookup"><span data-stu-id="bb204-138"><a name="example"></a>Example values</span></span>

<span data-ttu-id="bb204-139">Puede usar toocreate de valores de ejemplo de Hola un entorno de prueba, o hacer referencia a valores de toothese toobetter comprender los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="bb204-139">You can use hello example values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article.</span></span> <span data-ttu-id="bb204-140">Variables de Hola se establece en la sección [1](#declare) de artículo Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-140">We set hello variables in section [1](#declare) of hello article.</span></span> <span data-ttu-id="bb204-141">Puede utilizar pasos Hola como un ejemplo paso a paso y usar valores de hello sin modificarlas o cambiarlos tooreflect su entorno.</span><span class="sxs-lookup"><span data-stu-id="bb204-141">You can either use hello steps as a walk-through and use hello values without changing them, or change them tooreflect your environment.</span></span> 

* <span data-ttu-id="bb204-142">**Nombre: VNet1**</span><span class="sxs-lookup"><span data-stu-id="bb204-142">**Name: VNet1**</span></span>
* <span data-ttu-id="bb204-143">**Espacio de direcciones: 192.168.0.0/16** y **10.254.0.0/16**</span><span class="sxs-lookup"><span data-stu-id="bb204-143">**Address space: 192.168.0.0/16** and **10.254.0.0/16**</span></span><br><span data-ttu-id="bb204-144">En este ejemplo, se usa más de un tooillustrate de espacio de dirección que esta configuración funciona con varios espacios de direcciones.</span><span class="sxs-lookup"><span data-stu-id="bb204-144">For this example, we use more than one address space tooillustrate that this configuration works with multiple address spaces.</span></span> <span data-ttu-id="bb204-145">Sin embargo, para esta configuración no se necesitan varios espacios de direcciones.</span><span class="sxs-lookup"><span data-stu-id="bb204-145">However, multiple address spaces are not required for this configuration.</span></span>
* <span data-ttu-id="bb204-146">**Nombre de subred: FrontEnd**</span><span class="sxs-lookup"><span data-stu-id="bb204-146">**Subnet name: FrontEnd**</span></span>
  * <span data-ttu-id="bb204-147">**Intervalo de direcciones de subred: 192.168.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="bb204-147">**Subnet address range: 192.168.1.0/24**</span></span>
* <span data-ttu-id="bb204-148">**Nombre de subred: BackEnd**</span><span class="sxs-lookup"><span data-stu-id="bb204-148">**Subnet name: BackEnd**</span></span>
  * <span data-ttu-id="bb204-149">**Intervalo de direcciones de subred: 10.254.1.0/24**</span><span class="sxs-lookup"><span data-stu-id="bb204-149">**Subnet address range: 10.254.1.0/24**</span></span>
* <span data-ttu-id="bb204-150">**Nombre de subred: GatewaySubnet**</span><span class="sxs-lookup"><span data-stu-id="bb204-150">**Subnet name: GatewaySubnet**</span></span><br><span data-ttu-id="bb204-151">nombre de la subred de Hello *GatewaySubnet* es obligatorio para toowork de puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-151">hello Subnet name *GatewaySubnet* is mandatory for hello VPN gateway toowork.</span></span>
  * <span data-ttu-id="bb204-152">**Intervalo de direcciones de GatewaySubnet: 192.168.200.0/24**</span><span class="sxs-lookup"><span data-stu-id="bb204-152">**GatewaySubnet address range: 192.168.200.0/24**</span></span> 
* <span data-ttu-id="bb204-153">**Grupo de direcciones de clientes de VPN: 172.16.201.0/24**</span><span class="sxs-lookup"><span data-stu-id="bb204-153">**VPN client address pool: 172.16.201.0/24**</span></span><br><span data-ttu-id="bb204-154">Los clientes VPN que se conectan toohello red virtual con esta conexión de punto a sitio reciban una dirección IP de hello grupo de direcciones de cliente VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-154">VPN clients that connect toohello VNet using this Point-to-Site connection receive an IP address from hello VPN client address pool.</span></span>
* <span data-ttu-id="bb204-155">**Suscripción:** si tiene más de una suscripción, compruebe que está usando Hola correcto.</span><span class="sxs-lookup"><span data-stu-id="bb204-155">**Subscription:** If you have more than one subscription, verify that you are using hello correct one.</span></span>
* <span data-ttu-id="bb204-156">**Grupo de recursos: TestRG**</span><span class="sxs-lookup"><span data-stu-id="bb204-156">**Resource Group: TestRG**</span></span>
* <span data-ttu-id="bb204-157">**Ubicación: este de EE. UU.**</span><span class="sxs-lookup"><span data-stu-id="bb204-157">**Location: East US**</span></span>
* <span data-ttu-id="bb204-158">**Servidor DNS: Dirección IP** del servidor DNS de Hola que quiere toouse de resolución de nombres.</span><span class="sxs-lookup"><span data-stu-id="bb204-158">**DNS Server: IP address** of hello DNS server that you want toouse for name resolution.</span></span>
* <span data-ttu-id="bb204-159">**Nombre de puerta de enlace: Vnet1GW**</span><span class="sxs-lookup"><span data-stu-id="bb204-159">**GW Name: Vnet1GW**</span></span>
* <span data-ttu-id="bb204-160">**Nombre IP pública: VNet1GWPIP**</span><span class="sxs-lookup"><span data-stu-id="bb204-160">**Public IP name: VNet1GWPIP**</span></span>
* <span data-ttu-id="bb204-161">**VPNType: RouteBased**</span><span class="sxs-lookup"><span data-stu-id="bb204-161">**VpnType: RouteBased**</span></span> 

## <span data-ttu-id="bb204-162"><a name="declare"></a>1. Inicio de sesión y establecimiento de variables</span><span class="sxs-lookup"><span data-stu-id="bb204-162"><a name="declare"></a>1. Log in and set variables</span></span>

<span data-ttu-id="bb204-163">En esta sección, inicie sesión y declarar los valores de hello utilizados para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="bb204-163">In this section, you log in and declare hello values used for this configuration.</span></span> <span data-ttu-id="bb204-164">Hola declara valores se utilizan en las secuencias de comandos de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-164">hello declared values are used in hello sample scripts.</span></span> <span data-ttu-id="bb204-165">Cambiar tooreflect de valores de hello en su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="bb204-165">Change hello values tooreflect your own environment.</span></span> <span data-ttu-id="bb204-166">O bien, puede usar hello declarado valores y seguir los pasos de Hola como un ejercicio.</span><span class="sxs-lookup"><span data-stu-id="bb204-166">Or, you can use hello declared values and go through hello steps as an exercise.</span></span>

1. <span data-ttu-id="bb204-167">Abra la consola de PowerShell con privilegios elevados e inicie sesión tooyour cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-167">Open your PowerShell console with elevated privileges, and log in tooyour Azure account.</span></span> <span data-ttu-id="bb204-168">Este cmdlet le pide las credenciales de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-168">This cmdlet prompts you for hello login credentials.</span></span> <span data-ttu-id="bb204-169">Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bb204-169">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
2. <span data-ttu-id="bb204-170">Obtenga una lista de las suscripciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-170">Get a list of your Azure subscriptions.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
3. <span data-ttu-id="bb204-171">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-171">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. <span data-ttu-id="bb204-172">Declare las variables de Hola que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="bb204-172">Declare hello variables that you want toouse.</span></span> <span data-ttu-id="bb204-173">Usar hello según muestra, sustituyendo los valores de hello para su propio cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="bb204-173">Use hello following sample, substituting hello values for your own when necessary.</span></span>

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <span data-ttu-id="bb204-174"><a name="ConfigureVNet"></a>2. Configuración de una red virtual</span><span class="sxs-lookup"><span data-stu-id="bb204-174"><a name="ConfigureVNet"></a>2. Configure a VNet</span></span>

1. <span data-ttu-id="bb204-175">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bb204-175">Create a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. <span data-ttu-id="bb204-176">Crear configuraciones de subred para la red virtual de hello, asignarles de hello *front-end*, *back-end*, y *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="bb204-176">Create hello subnet configurations for hello virtual network, naming them *FrontEnd*, *BackEnd*, and *GatewaySubnet*.</span></span> <span data-ttu-id="bb204-177">Estos prefijos deben formar parte del programa Hola espacio de direcciones de red virtual que declara.</span><span class="sxs-lookup"><span data-stu-id="bb204-177">These prefixes must be part of hello VNet address space that you declared.</span></span>

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. <span data-ttu-id="bb204-178">Crear red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-178">Create hello virtual network.</span></span>

  <span data-ttu-id="bb204-179">En este ejemplo, el servidor DNS de hello es opcional.</span><span class="sxs-lookup"><span data-stu-id="bb204-179">In this example, hello DNS server is optional.</span></span> <span data-ttu-id="bb204-180">La especificación de un valor no crea un servidor DNS nuevo.</span><span class="sxs-lookup"><span data-stu-id="bb204-180">Specifying a value does not create a new DNS server.</span></span> <span data-ttu-id="bb204-181">Hello dirección IP del servidor DNS que especifique debe ser un servidor DNS que pueda resolver nombres de Hola para los recursos de saludo a que se está conectando.</span><span class="sxs-lookup"><span data-stu-id="bb204-181">hello DNS server IP address that you specify should be a DNS server that can resolve hello names for hello resources you are connecting to.</span></span> <span data-ttu-id="bb204-182">En este ejemplo, se usa una dirección IP privada, pero es probable que esto no es Hola dirección IP del servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="bb204-182">For this example, we used a private IP address, but it is likely that this is not hello IP address of your DNS server.</span></span> <span data-ttu-id="bb204-183">Ser seguro toouse sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="bb204-183">Be sure toouse your own values.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. <span data-ttu-id="bb204-184">Especificar las variables de hello para la red virtual de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="bb204-184">Specify hello variables for hello virtual network you created.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. <span data-ttu-id="bb204-185">Una puerta de enlace VPN debe tener una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="bb204-185">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="bb204-186">Solicitar el recurso de dirección IP hello y, a continuación, hacer referencia tooit al crear la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-186">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="bb204-187">dirección IP de Hola se asigna dinámicamente toohello recursos cuando se crea la puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-187">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="bb204-188">Actualmente, VPN Gateway solo admite la asignación de direcciones IP públicas *dinámicas*.</span><span class="sxs-lookup"><span data-stu-id="bb204-188">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="bb204-189">No se puede solicitar una asignación de direcciones IP públicas estáticas.</span><span class="sxs-lookup"><span data-stu-id="bb204-189">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="bb204-190">Sin embargo, no significa que se cambia la dirección IP de hello después de que se le ha asignado tooyour puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-190">However, it doesn't mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="bb204-191">cambios en la dirección IP pública hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="bb204-191">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="bb204-192">No cambia cuando se cambia el tamaño, se restablece o se realizan actualizaciones u otras operaciones de mantenimiento interno de una puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-192">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

  <span data-ttu-id="bb204-193">Solicite una dirección IP pública asignada de forma dinámica.</span><span class="sxs-lookup"><span data-stu-id="bb204-193">Request a dynamically assigned public IP address.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <span data-ttu-id="bb204-194"><a name="creategateway"></a>3. Crear puerta de enlace VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="bb204-194"><a name="creategateway"></a>3. Create hello VPN gateway</span></span>

<span data-ttu-id="bb204-195">Configurar y crear la puerta de enlace de red virtual de hello para la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-195">Configure and create hello virtual network gateway for your VNet.</span></span>

* <span data-ttu-id="bb204-196">Hola *- el GatewayType* debe ser **Vpn** hello y *- VpnType* debe ser **RouteBased**.</span><span class="sxs-lookup"><span data-stu-id="bb204-196">hello *-GatewayType* must be **Vpn** and hello *-VpnType* must be **RouteBased**.</span></span>
* <span data-ttu-id="bb204-197">Una puerta de enlace VPN puede tardar hasta too45 toocomplete de minutos, dependiendo de hello [sku de puerta de enlace](vpn-gateway-about-vpn-gateway-settings.md) seleccione.</span><span class="sxs-lookup"><span data-stu-id="bb204-197">A VPN gateway can take up too45 minutes toocomplete, depending on hello [gateway sku](vpn-gateway-about-vpn-gateway-settings.md) you select.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <span data-ttu-id="bb204-198"><a name="addresspool"></a>4. Agregar grupo de direcciones de cliente VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="bb204-198"><a name="addresspool"></a>4. Add hello VPN client address pool</span></span>

<span data-ttu-id="bb204-199">Una vez finaliza la creación de puerta de enlace VPN de hello, puede agregar grupo de direcciones de cliente VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-199">After hello VPN gateway finishes creating, you can add hello VPN client address pool.</span></span> <span data-ttu-id="bb204-200">Hola grupo de direcciones de cliente VPN es intervalo Hola desde el cual los clientes VPN de Hola reciban una dirección IP al conectarse.</span><span class="sxs-lookup"><span data-stu-id="bb204-200">hello VPN client address pool is hello range from which hello VPN clients receive an IP address when connecting.</span></span> <span data-ttu-id="bb204-201">Usar un intervalo de direcciones IP privadas que no se superponen con ubicación local de Hola que se conectan desde, o con hello red virtual que desea tooconnect a.</span><span class="sxs-lookup"><span data-stu-id="bb204-201">Use a private IP address range that does not overlap with hello on-premises location that you connect from, or with hello VNet that you want tooconnect to.</span></span> <span data-ttu-id="bb204-202">En este ejemplo, hello grupo de direcciones de cliente VPN se declara como un [variable](#declare) en el paso 1.</span><span class="sxs-lookup"><span data-stu-id="bb204-202">In this example, hello VPN client address pool is declared as a [variable](#declare) in Step 1.</span></span>

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <span data-ttu-id="bb204-203"><a name="Certificates"></a>5. Generación de certificados</span><span class="sxs-lookup"><span data-stu-id="bb204-203"><a name="Certificates"></a>5. Generate certificates</span></span>

<span data-ttu-id="bb204-204">Los clientes VPN tooauthenticate Azure usan certificados para Point-to-Site VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-204">Certificates are used by Azure tooauthenticate VPN clients for Point-to-Site VPNs.</span></span> <span data-ttu-id="bb204-205">Cargar información de clave pública de Hola de tooAzure de certificado de raíz de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-205">You upload hello public key information of hello root certificate tooAzure.</span></span> <span data-ttu-id="bb204-206">clave pública de Hello, a continuación, se considera "confianza".</span><span class="sxs-lookup"><span data-stu-id="bb204-206">hello public key is then considered 'trusted'.</span></span> <span data-ttu-id="bb204-207">Los certificados de cliente deben ser generados a partir de certificado de raíz de confianza de hello y, a continuación, se instala en cada equipo cliente en el almacén de certificados de usuario o Personal de certificados actual Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-207">Client certificates must be generated from hello trusted root certificate, and then installed on each client computer in hello Certificates-Current User/Personal certificate store.</span></span> <span data-ttu-id="bb204-208">certificado de Hello es cliente de Hola de tooauthenticate usado cuando inicia una red virtual toohello de conexión.</span><span class="sxs-lookup"><span data-stu-id="bb204-208">hello certificate is used tooauthenticate hello client when it initiates a connection toohello VNet.</span></span> 

<span data-ttu-id="bb204-209">Si usa certificados autofirmados, se deben crear con parámetros específicos.</span><span class="sxs-lookup"><span data-stu-id="bb204-209">If you use self-signed certificates, they must be created using specific parameters.</span></span> <span data-ttu-id="bb204-210">Puede crear un certificado autofirmado mediante instrucciones de Hola para [PowerShell y Windows 10](vpn-gateway-certificates-point-to-site.md), o bien, si no tiene Windows 10, puede usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span><span class="sxs-lookup"><span data-stu-id="bb204-210">You can create a self-signed certificate using hello instructions for [PowerShell and Windows 10](vpn-gateway-certificates-point-to-site.md), or, if you don't have Windows 10, you can use [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md).</span></span> <span data-ttu-id="bb204-211">Es importante que siga los pasos de hello en instrucciones de hello al generar certificados raíz autofirmados y certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-211">It's important that you follow hello steps in hello instructions when generating self-signed root certificates and client certificates.</span></span> <span data-ttu-id="bb204-212">En caso contrario, no serán compatibles con conexiones de P2S certificados Hola que generar y recibirá un error de conexión.</span><span class="sxs-lookup"><span data-stu-id="bb204-212">Otherwise, hello certificates you generate will not be compatible with P2S connections and you will receive a connection error.</span></span>

### <span data-ttu-id="bb204-213"><a name="cer"></a>1. Obtener el archivo .cer de hello para el certificado de raíz de Hola</span><span class="sxs-lookup"><span data-stu-id="bb204-213"><a name="cer"></a>1. Obtain hello .cer file for hello root certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <span data-ttu-id="bb204-214"><a name="generate"></a>2. Generación de un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="bb204-214"><a name="generate"></a>2. Generate a client certificate</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <span data-ttu-id="bb204-215"><a name="upload"></a>6. Cargar información de clave pública de hello raíz certificado</span><span class="sxs-lookup"><span data-stu-id="bb204-215"><a name="upload"></a>6. Upload hello root certificate public key information</span></span>

<span data-ttu-id="bb204-216">Compruebe que ha terminado de crear la puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="bb204-216">Verify that your VPN gateway has finished creating.</span></span> <span data-ttu-id="bb204-217">Una vez que se ha completado, puede cargar Hola CER (que contiene información de clave pública de hello) para un tooAzure de certificado raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="bb204-217">Once it has completed, you can upload hello .cer file (which contains hello public key information) for a trusted root certificate tooAzure.</span></span> <span data-ttu-id="bb204-218">Una vez cargado el archivo a.cer, Azure puede usar a los clientes de tooauthenticate que han instalado un certificado de cliente generado a partir de certificado de raíz de confianza de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-218">Once a.cer file is uploaded, Azure can use it tooauthenticate clients that have installed a client certificate generated from hello trusted root certificate.</span></span> <span data-ttu-id="bb204-219">Puede cargar los archivos de certificado raíz de confianza adicionales - tooa total de 20, más adelante, si es necesario.</span><span class="sxs-lookup"><span data-stu-id="bb204-219">You can upload additional trusted root certificate files - up tooa total of 20 - later, if needed.</span></span>

1. <span data-ttu-id="bb204-220">Declarar la variable de hello para el nombre del certificado, reemplazando el valor de Hola por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="bb204-220">Declare hello variable for your certificate name, replacing hello value with your own.</span></span>

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. <span data-ttu-id="bb204-221">Reemplace la ruta de acceso de archivo de hello con sus propios y, a continuación, ejecutar los cmdlets de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-221">Replace hello file path with your own, and then run hello cmdlets.</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. <span data-ttu-id="bb204-222">Cargar hello tooAzure de información de clave pública.</span><span class="sxs-lookup"><span data-stu-id="bb204-222">Upload hello public key information tooAzure.</span></span> <span data-ttu-id="bb204-223">Una vez que se carga la información del certificado hello, Azure tiene en cuenta este toobe un certificado raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="bb204-223">Once hello certificate information is uploaded, Azure considers this toobe a trusted root certificate.</span></span>

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <span data-ttu-id="bb204-224"><a name="clientconfig"></a>7. Descargar paquete de configuración de cliente VPN de Hola</span><span class="sxs-lookup"><span data-stu-id="bb204-224"><a name="clientconfig"></a>7. Download hello VPN client configuration package</span></span>

<span data-ttu-id="bb204-225">tooconnect tooa red virtual con una VPN de sitio a punto, cada cliente debe instalar un paquete de configuración de cliente que se configura el cliente VPN nativo que Hola con los valores de hello y archivos de red virtual de toohello tooconnect necesarios.</span><span class="sxs-lookup"><span data-stu-id="bb204-225">tooconnect tooa VNet using a Point-to-Site VPN, each client must install a client configuration package that configures hello native VPN client with hello settings and files that are necessary tooconnect toohello virtual network.</span></span> <span data-ttu-id="bb204-226">paquete de configuración de cliente VPN de Hello configura el cliente de VPN de Windows nativo hello, pero no instala un cliente VPN de nuevo o diferente.</span><span class="sxs-lookup"><span data-stu-id="bb204-226">hello VPN client configuration package configures hello native Windows VPN client, it doesn't install a new or different VPN client.</span></span> 

<span data-ttu-id="bb204-227">Puede usar Hola misma configuración de cliente VPN del paquete en cada equipo cliente, como versión de Hola coincida con la arquitectura de hello para el cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-227">You can use hello same VPN client configuration package on each client computer, as long as hello version matches hello architecture for hello client.</span></span> <span data-ttu-id="bb204-228">Para hello obtener lista de sistemas operativos cliente que son compatibles, vea hello [conexionesPoint-to-Site preguntas más frecuentes sobre](#faq) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="bb204-228">For hello list of client operating systems that are supported, see hello [Point-to-Site connections FAQ](#faq) at hello end of this article.</span></span>

1. <span data-ttu-id="bb204-229">Una vez creada la puerta de enlace de hello, puede generar y descargar el paquete de configuración de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-229">After hello gateway has been created, you can generate and download hello client configuration package.</span></span> <span data-ttu-id="bb204-230">En este ejemplo, se descarga el paquete de Hola para los clientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="bb204-230">This example downloads hello package for 64-bit clients.</span></span> <span data-ttu-id="bb204-231">Si desea que el cliente de 32 bits de hello toodownload, reemplace 'Amd64' con 'x86'.</span><span class="sxs-lookup"><span data-stu-id="bb204-231">If you want toodownload hello 32-bit client, replace 'Amd64' with 'x86'.</span></span> <span data-ttu-id="bb204-232">También puede descargar el cliente VPN de hello mediante el uso de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-232">You can also download hello VPN client by using hello Azure portal.</span></span>

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. <span data-ttu-id="bb204-233">Copie y pegue el vínculo de Hola que se devuelve tooa explorador toodownload Hola paquete web, teniendo cuidado de las comillas de hello tooremove que rodea el vínculo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-233">Copy and paste hello link that is returned tooa web browser toodownload hello package, taking care tooremove hello quotes surrounding hello link.</span></span> 
3. <span data-ttu-id="bb204-234">Descargue e instale el paquete de hello en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-234">Download and install hello package on hello client computer.</span></span> <span data-ttu-id="bb204-235">Si ve una ventana emergente de SmartScreen, haga clic en **Más información** y en **Ejecutar de todas formas**.</span><span class="sxs-lookup"><span data-stu-id="bb204-235">If you see a SmartScreen popup, click **More info**, then **Run anyway**.</span></span> <span data-ttu-id="bb204-236">También puede guardar Hola paquete tooinstall en otros equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-236">You can also save hello package tooinstall on other client computers.</span></span>
4. <span data-ttu-id="bb204-237">En el equipo de cliente hello, vaya demasiado**configuración de red** y haga clic en **VPN**.</span><span class="sxs-lookup"><span data-stu-id="bb204-237">On hello client computer, navigate too**Network Settings** and click **VPN**.</span></span> <span data-ttu-id="bb204-238">Hola conexión VPN muestra nombre Hola de red virtual de Hola que se conecta a.</span><span class="sxs-lookup"><span data-stu-id="bb204-238">hello VPN connection shows hello name of hello virtual network that it connects to.</span></span>

## <span data-ttu-id="bb204-239"><a name="clientcertificate"></a>8. Instalación de un certificado de cliente exportado</span><span class="sxs-lookup"><span data-stu-id="bb204-239"><a name="clientcertificate"></a>8. Install an exported client certificate</span></span>

<span data-ttu-id="bb204-240">Si desea toocreate una P2S conexión desde un equipo cliente que no sea de Hola que utiliza certificados de cliente hello toogenerate, deberá tooinstall un certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-240">If you want toocreate a P2S connection from a client computer other than hello one you used toogenerate hello client certificates, you need tooinstall a client certificate.</span></span> <span data-ttu-id="bb204-241">Al instalar un certificado de cliente, necesita contraseña Hola que se creó cuando se exporta el certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-241">When installing a client certificate, you need hello password that was created when hello client certificate was exported.</span></span> <span data-ttu-id="bb204-242">Normalmente, es simplemente cuestión de doble clic en el certificado de hello e instalarla.</span><span class="sxs-lookup"><span data-stu-id="bb204-242">Typically, it is just a matter of double-clicking hello certificate and installing it.</span></span>

<span data-ttu-id="bb204-243">Asegúrese de que se exportó el certificado de cliente de Hola como un .pfx junto con la cadena de certificados completa de hello (que es el valor predeterminado de hello).</span><span class="sxs-lookup"><span data-stu-id="bb204-243">Make sure hello client certificate was exported as a .pfx along with hello entire certificate chain (which is hello default).</span></span> <span data-ttu-id="bb204-244">En caso contrario, no está presente en el equipo de cliente hello información del certificado de raíz de Hola y cliente hello no será capaz de tooauthenticate correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb204-244">Otherwise, hello root certificate information isn't present on hello client computer and hello client won't be able tooauthenticate properly.</span></span> <span data-ttu-id="bb204-245">Para más información, consulte [Instalación de un certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).</span><span class="sxs-lookup"><span data-stu-id="bb204-245">For more information, see [Install an exported client certificate](vpn-gateway-certificates-point-to-site.md#install).</span></span> 

## <span data-ttu-id="bb204-246"><a name="connect"></a>9. Conectar tooAzure</span><span class="sxs-lookup"><span data-stu-id="bb204-246"><a name="connect"></a>9. Connect tooAzure</span></span>

1. <span data-ttu-id="bb204-247">tooconnect tooyour de red virtual, en el equipo de cliente hello, navegar por las conexiones de tooVPN y encontrar la conexión de VPN de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="bb204-247">tooconnect tooyour VNet, on hello client computer, navigate tooVPN connections and locate hello VPN connection that you created.</span></span> <span data-ttu-id="bb204-248">Se denomina hello mismo nombre como la red virtual.</span><span class="sxs-lookup"><span data-stu-id="bb204-248">It is named hello same name as your virtual network.</span></span> <span data-ttu-id="bb204-249">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="bb204-249">Click **Connect**.</span></span> <span data-ttu-id="bb204-250">Puede aparecer un mensaje emergente que hace referencia el certificado de hello toousing.</span><span class="sxs-lookup"><span data-stu-id="bb204-250">A pop-up message may appear that refers toousing hello certificate.</span></span> <span data-ttu-id="bb204-251">Haga clic en **continuar** toouse privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="bb204-251">Click **Continue** toouse elevated privileges.</span></span> 
2. <span data-ttu-id="bb204-252">En hello **conexión** página de estado, haga clic en **conectar** conexión de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="bb204-252">On hello **Connection** status page, click **Connect** toostart hello connection.</span></span> <span data-ttu-id="bb204-253">Si ve un **Seleccionar certificado** pantalla, compruebe que Hola cliente certificado que se muestra es Hola uno que desea toouse tooconnect.</span><span class="sxs-lookup"><span data-stu-id="bb204-253">If you see a **Select Certificate** screen, verify that hello client certificate showing is hello one that you want toouse tooconnect.</span></span> <span data-ttu-id="bb204-254">Si no es así, utilice certificado correcto de hello flecha de lista desplegable tooselect hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bb204-254">If it is not, use hello drop-down arrow tooselect hello correct certificate, and then click **OK**.</span></span>

  ![TooAzure conecta el cliente VPN](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. <span data-ttu-id="bb204-256">Se ha establecido la conexión.</span><span class="sxs-lookup"><span data-stu-id="bb204-256">Your connection is established.</span></span>

  ![Conexión establecida](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a><span data-ttu-id="bb204-258">Solución de problemas de conexiones P2S</span><span class="sxs-lookup"><span data-stu-id="bb204-258">Troubleshooting P2S connections</span></span>

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <span data-ttu-id="bb204-259"><a name="verify"></a>10. Comprobación de la conexión</span><span class="sxs-lookup"><span data-stu-id="bb204-259"><a name="verify"></a>10. Verify your connection</span></span>

1. <span data-ttu-id="bb204-260">tooverify que la conexión VPN esté activa, abra un símbolo del sistema con privilegios elevados y ejecute *ipconfig/all*.</span><span class="sxs-lookup"><span data-stu-id="bb204-260">tooverify that your VPN connection is active, open an elevated command prompt, and run *ipconfig/all*.</span></span>
2. <span data-ttu-id="bb204-261">Ver los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-261">View hello results.</span></span> <span data-ttu-id="bb204-262">Tenga en cuenta que la dirección IP de hello recibió es una de las direcciones de hello en el grupo de direcciones de cliente VPN de hello Point-to-Site que especificó en la configuración.</span><span class="sxs-lookup"><span data-stu-id="bb204-262">Notice that hello IP address you received is one of hello addresses within hello Point-to-Site VPN Client Address Pool that you specified in your configuration.</span></span> <span data-ttu-id="bb204-263">resultados de Hello son similares de toothis de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="bb204-263">hello results are similar toothis example:</span></span>

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <span data-ttu-id="bb204-264"><a name="connectVM"></a>Conectar máquina virtual de tooa</span><span class="sxs-lookup"><span data-stu-id="bb204-264"><a name="connectVM"></a>Connect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <span data-ttu-id="bb204-265"><a name="addremovecert"></a>Adición o eliminación de un certificado raíz</span><span class="sxs-lookup"><span data-stu-id="bb204-265"><a name="addremovecert"></a>Add or remove a root certificate</span></span>

<span data-ttu-id="bb204-266">Puede agregar y quitar certificados raíz de confianza de Azure.</span><span class="sxs-lookup"><span data-stu-id="bb204-266">You can add and remove trusted root certificates from Azure.</span></span> <span data-ttu-id="bb204-267">Cuando se quita un certificado raíz, los clientes que tienen un certificado generado a partir de certificado de raíz de hello no se pueden autenticar y no será capaz de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="bb204-267">When you remove a root certificate, clients that have a certificate generated from hello root certificate can't authenticate and won't be able tooconnect.</span></span> <span data-ttu-id="bb204-268">Si desea que un cliente tooauthenticate y conectarse, debe tooinstall genera un nuevo certificado de cliente de un certificado raíz de confianza tooAzure (cargado).</span><span class="sxs-lookup"><span data-stu-id="bb204-268">If you want a client tooauthenticate and connect, you need tooinstall a new client certificate generated from a root certificate that is trusted (uploaded) tooAzure.</span></span>

### <span data-ttu-id="bb204-269"><a name="addtrustedroot"></a>tooadd un certificado raíz de confianza</span><span class="sxs-lookup"><span data-stu-id="bb204-269"><a name="addtrustedroot"></a>tooadd a trusted root certificate</span></span>

<span data-ttu-id="bb204-270">Puede sumar too20 raíz certificado .cer archivos tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb204-270">You can add up too20 root certificate .cer files tooAzure.</span></span> <span data-ttu-id="bb204-271">Hola siguientes pasos le indican ayudan a agregar un certificado raíz:</span><span class="sxs-lookup"><span data-stu-id="bb204-271">hello following steps help you add a root certificate:</span></span>

#### <span data-ttu-id="bb204-272"><a name="certmethod1"></a>Método 1</span><span class="sxs-lookup"><span data-stu-id="bb204-272"><a name="certmethod1"></a>Method 1</span></span>

<span data-ttu-id="bb204-273">Se trata de tooupload de método más eficaz de hello un certificado raíz.</span><span class="sxs-lookup"><span data-stu-id="bb204-273">This is hello most efficient method tooupload a root certificate.</span></span>

1. <span data-ttu-id="bb204-274">Preparar tooupload de archivo .cer hello:</span><span class="sxs-lookup"><span data-stu-id="bb204-274">Prepare hello .cer file tooupload:</span></span>

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. <span data-ttu-id="bb204-275">Cargar archivo hello.</span><span class="sxs-lookup"><span data-stu-id="bb204-275">Upload hello file.</span></span> <span data-ttu-id="bb204-276">Solo puede cargar un archivo a la vez.</span><span class="sxs-lookup"><span data-stu-id="bb204-276">You can only upload one file at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. <span data-ttu-id="bb204-277">tooverify que Hola cargado el archivo de certificado:</span><span class="sxs-lookup"><span data-stu-id="bb204-277">tooverify that hello certificate file uploaded:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <span data-ttu-id="bb204-278"><a name="certmethod2"></a>Método 2</span><span class="sxs-lookup"><span data-stu-id="bb204-278"><a name="certmethod2"></a>Method 2</span></span>

<span data-ttu-id="bb204-279">Este método es tiene pasos más que el método 1, pero tiene Hola el mismo resultado.</span><span class="sxs-lookup"><span data-stu-id="bb204-279">This method is has more steps than Method 1, but has hello same result.</span></span> <span data-ttu-id="bb204-280">Se incluye por si tuviera datos del certificado tooview Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-280">It is included in case you need tooview hello certificate data.</span></span>

1. <span data-ttu-id="bb204-281">Crear y preparar Hola nueva raíz certificado tooadd tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bb204-281">Create and prepare hello new root certificate tooadd tooAzure.</span></span> <span data-ttu-id="bb204-282">Exportar la clave pública de hello como Base64 codificado X.509 (. (CER) y ábralo con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="bb204-282">Export hello public key as a Base-64 encoded X.509 (.CER) and open it with a text editor.</span></span> <span data-ttu-id="bb204-283">Copiar valores de hello, como se muestra en el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb204-283">Copy hello values, as shown in hello following example:</span></span>

  ![certificado](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > <span data-ttu-id="bb204-285">Cuando se copian datos de certificado de hello, asegúrese de que copia texto hello como una línea continua sin retornos de carro o avances de línea.</span><span class="sxs-lookup"><span data-stu-id="bb204-285">When copying hello certificate data, make sure that you copy hello text as one continuous line without carriage returns or line feeds.</span></span> <span data-ttu-id="bb204-286">Deberá toomodify la vista mediante too'Show de editor de texto hello símbolos/mostrar toosee Hola de carro todos los caracteres devuelve y saltos de línea.</span><span class="sxs-lookup"><span data-stu-id="bb204-286">You may need toomodify your view in hello text editor too'Show Symbol/Show all characters' toosee hello carriage returns and line feeds.</span></span>
  >
  >

2. <span data-ttu-id="bb204-287">Especificar el nombre del certificado de Hola y la información clave como una variable.</span><span class="sxs-lookup"><span data-stu-id="bb204-287">Specify hello certificate name and key information as a variable.</span></span> <span data-ttu-id="bb204-288">Reemplace Hola información con su cuenta, como se muestra en hello ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="bb204-288">Replace hello information with your own, as shown in hello following example:</span></span>

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. <span data-ttu-id="bb204-289">Agregar nuevo certificado de raíz Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-289">Add hello new root certificate.</span></span> <span data-ttu-id="bb204-290">Solo puede agregar un certificado raíz a la vez.</span><span class="sxs-lookup"><span data-stu-id="bb204-290">You can only add one certificate at a time.</span></span>

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. <span data-ttu-id="bb204-291">Puede comprobar el que certificado nuevo Hola se agregó correctamente utilizando el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="bb204-291">You can verify that hello new certificate was added correctly by using hello following example:</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <span data-ttu-id="bb204-292"><a name="removerootcert"></a>tooremove un certificado raíz</span><span class="sxs-lookup"><span data-stu-id="bb204-292"><a name="removerootcert"></a>tooremove a root certificate</span></span>

1. <span data-ttu-id="bb204-293">Declare las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-293">Declare hello variables.</span></span>

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. <span data-ttu-id="bb204-294">Quitar certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-294">Remove hello certificate.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. <span data-ttu-id="bb204-295">Hola de uso después de tooverify de ejemplo que Hola certificado se eliminó correctamente.</span><span class="sxs-lookup"><span data-stu-id="bb204-295">Use hello following example tooverify that hello certificate was removed successfully.</span></span>

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <span data-ttu-id="bb204-296"><a name="revoke"></a>Revocación de un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="bb204-296"><a name="revoke"></a>Revoke a client certificate</span></span>

<span data-ttu-id="bb204-297">Puede revocar certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="bb204-297">You can revoke client certificates.</span></span> <span data-ttu-id="bb204-298">podrá tooselectively lista de revocación de certificados de Hello denegar conectividad de punto a sitio basada en certificados de cliente individuales.</span><span class="sxs-lookup"><span data-stu-id="bb204-298">hello certificate revocation list allows you tooselectively deny Point-to-Site connectivity based on individual client certificates.</span></span> <span data-ttu-id="bb204-299">Esto difiere de la forma en que se quita un certificado raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="bb204-299">This is different than removing a trusted root certificate.</span></span> <span data-ttu-id="bb204-300">Si quita un .cer del certificado raíz de confianza de Azure, revoca el acceso de Hola para todos los certificados de cliente generado y firmado por certificado de raíz revocados Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-300">If you remove a trusted root certificate .cer from Azure, it revokes hello access for all client certificates generated/signed by hello revoked root certificate.</span></span> <span data-ttu-id="bb204-301">Revocar un certificado de cliente, en lugar de certificado de raíz de hello, permite Hola otros certificados que se generaron desde el certificado de raíz de hello toocontinue toobe utilizado para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="bb204-301">Revoking a client certificate, rather than hello root certificate, allows hello other certificates that were generated from hello root certificate toocontinue toobe used for authentication.</span></span>

<span data-ttu-id="bb204-302">una práctica habitual Hello es toouse Hola certificado toomanage acceso a la raíz en los niveles de equipo u organización, durante el uso de certificados de cliente revocados para el control de acceso específica para los usuarios individuales.</span><span class="sxs-lookup"><span data-stu-id="bb204-302">hello common practice is toouse hello root certificate toomanage access at team or organization levels, while using revoked client certificates for fine-grained access control on individual users.</span></span>

### <span data-ttu-id="bb204-303"><a name="revokeclientcert"></a>toorevoke un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="bb204-303"><a name="revokeclientcert"></a>toorevoke a client certificate</span></span>

1. <span data-ttu-id="bb204-304">Recuperar la huella digital del certificado de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-304">Retrieve hello client certificate thumbprint.</span></span> <span data-ttu-id="bb204-305">Para obtener más información, consulte [cómo tooretrieve Hola huella digital de un certificado](https://msdn.microsoft.com/library/ms734695.aspx).</span><span class="sxs-lookup"><span data-stu-id="bb204-305">For more information, see [How tooretrieve hello Thumbprint of a Certificate](https://msdn.microsoft.com/library/ms734695.aspx).</span></span>
2. <span data-ttu-id="bb204-306">Copiar información hello tooa, editor de texto y quite todos los espacios para que sea una sola cadena continua.</span><span class="sxs-lookup"><span data-stu-id="bb204-306">Copy hello information tooa text editor and remove all spaces so that it is a continuous string.</span></span> <span data-ttu-id="bb204-307">Esta cadena se declara como una variable en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="bb204-307">This string is declared as a variable in hello next step.</span></span>
3. <span data-ttu-id="bb204-308">Declare las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-308">Declare hello variables.</span></span> <span data-ttu-id="bb204-309">Asegúrese de que ha recuperado la huella digital Hola de toodeclare seguro en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-309">Make sure toodeclare hello thumbprint you retrieved in hello previous step.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. <span data-ttu-id="bb204-310">Agregue Hola huella digital toohello lista de certificados revocados.</span><span class="sxs-lookup"><span data-stu-id="bb204-310">Add hello thumbprint toohello list of revoked certificates.</span></span> <span data-ttu-id="bb204-311">Vea "Correcto" cuando se ha agregado la huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-311">You see "Succeeded" when hello thumbprint has been added.</span></span>

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. <span data-ttu-id="bb204-312">Comprobar que huella digital Hola se agregó toohello lista de revocación de certificados.</span><span class="sxs-lookup"><span data-stu-id="bb204-312">Verify that hello thumbprint was added toohello certificate revocation list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. <span data-ttu-id="bb204-313">Una vez agregada la huella digital de hello, certificado de hello ya no puede ser tooconnect usado.</span><span class="sxs-lookup"><span data-stu-id="bb204-313">After hello thumbprint has been added, hello certificate can no longer be used tooconnect.</span></span> <span data-ttu-id="bb204-314">Los clientes que intentan tooconnect con este certificado, aparece un mensaje que indica que dicho certificado Hola ya no es válido.</span><span class="sxs-lookup"><span data-stu-id="bb204-314">Clients that try tooconnect using this certificate receive a message saying that hello certificate is no longer valid.</span></span>

### <span data-ttu-id="bb204-315"><a name="reinstateclientcert"></a>tooreinstate un certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="bb204-315"><a name="reinstateclientcert"></a>tooreinstate a client certificate</span></span>

<span data-ttu-id="bb204-316">Puede volver a aplicar un certificado de cliente mediante la eliminación de huella digital de hello en lista de Hola de certificados de cliente revocados.</span><span class="sxs-lookup"><span data-stu-id="bb204-316">You can reinstate a client certificate by removing hello thumbprint from hello list of revoked client certificates.</span></span>

1. <span data-ttu-id="bb204-317">Declare las variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-317">Declare hello variables.</span></span> <span data-ttu-id="bb204-318">Asegúrese de que se declare Hola correcto la huella digital de certificado de Hola que quiere que tooreinstate.</span><span class="sxs-lookup"><span data-stu-id="bb204-318">Make sure you declare hello correct thumbprint for hello certificate that you want tooreinstate.</span></span>

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. <span data-ttu-id="bb204-319">Quitar huella digital del certificado Hola de lista de revocación de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="bb204-319">Remove hello certificate thumbprint from hello certificate revocation list.</span></span>

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. <span data-ttu-id="bb204-320">Compruebe si la huella digital de Hola se quita de hello revocado lista.</span><span class="sxs-lookup"><span data-stu-id="bb204-320">Check if hello thumbprint is removed from hello revoked list.</span></span>

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <span data-ttu-id="bb204-321"><a name="faq"></a>Preguntas más frecuentes sobre la conexión de punto a sitio</span><span class="sxs-lookup"><span data-stu-id="bb204-321"><a name="faq"></a>Point-to-Site FAQ</span></span>

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bb204-322">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bb204-322">Next steps</span></span>
<span data-ttu-id="bb204-323">Una vez completada la conexión, puede agregar redes virtuales de máquinas virtuales tooyour.</span><span class="sxs-lookup"><span data-stu-id="bb204-323">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="bb204-324">Consulte [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) para más información.</span><span class="sxs-lookup"><span data-stu-id="bb204-324">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span> <span data-ttu-id="bb204-325">toounderstand más información acerca de las redes y máquinas virtuales, consulte [información general de red de Azure y VM de Linux](../virtual-machines/linux/azure-vm-network-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb204-325">toounderstand more about networking and virtual machines, see [Azure and Linux VM network overview](../virtual-machines/linux/azure-vm-network-overview.md).</span></span>
