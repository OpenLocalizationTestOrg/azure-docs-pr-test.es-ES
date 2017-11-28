---
title: "Conectar redes virtuales clásicas tooAzure VNets el Administrador de recursos: PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión VPN entre clásico redes virtuales y VNets el Administrador de recursos con puerta de enlace VPN y PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="8f7f8-103">Conexión de redes virtuales a partir de diferentes modelos de implementación con PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7f8-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="8f7f8-104">Este artículo muestra cómo tooconnect clásico redes virtuales tooResource Manager VNets tooallow Hola recursos ubicados en hello toocommunicate de modelos de implementación independiente entre sí.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="8f7f8-105">pasos de Hello en este artículo usan PowerShell, pero también puede crear esta configuración con hello portal de Azure, seleccione artículo hello en esta lista.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8f7f8-106">Portal</span><span class="sxs-lookup"><span data-stu-id="8f7f8-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="8f7f8-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7f8-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="8f7f8-108">Conectar un tooa de red virtual clásica VNet el Administrador de recursos es similar tooconnecting una ubicación de sitio de red virtual tooan local.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="8f7f8-109">Ambos tipos de conectividad usan un tooprovide de puerta de enlace VPN un túnel seguro mediante IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="8f7f8-110">Puede crear una conexión entre redes virtuales que estén en diferentes suscripciones y en diferentes regiones.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="8f7f8-111">También puede conectar redes virtuales que ya tengan redes locales tooon de conexiones, siempre que sea de puerta de enlace de Hola que les ha configurado dinámica o basadas en enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="8f7f8-112">Para obtener más información acerca de las conexiones de red virtual a red virtual, vea hello [P+F de red virtual a red virtual](#faq) final Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="8f7f8-113">Si sus redes virtuales están en hello misma región, puede que desee tooinstead considerar realizar la conexión con el intercambio de tráfico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="8f7f8-114">El emparejamiento de VNET no usa VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="8f7f8-115">Para más información, consulte [Emparejamiento de VNET](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f7f8-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="8f7f8-116">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="8f7f8-116">Before beginning</span></span>

<span data-ttu-id="8f7f8-117">Hola pasos siguientes le ofrezca Hola configuración necesario tooconfigure una puerta de enlace dinámico o de ruta para cada red virtual y crear una conexión VPN entre puertas de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="8f7f8-118">Esta configuración no admite puertas de enlace estáticas o basadas en directivas.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8f7f8-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8f7f8-119">Prerequisites</span></span>

* <span data-ttu-id="8f7f8-120">Se han creado ambas redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="8f7f8-121">intervalos de direcciones de Hola para hello redes virtuales no se superponen entre sí, ni se superponen con ninguno de los intervalos de Hola para otras conexiones que se pueden conectar las puertas de enlace de Hola a.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="8f7f8-122">Se ha instalado cmdlets de PowerShell de hello más recientes.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="8f7f8-123">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="8f7f8-124">Asegúrese de que instalar Service Management (SM) de Hola y Hola cmdlets del Administrador de recursos (RM).</span><span class="sxs-lookup"><span data-stu-id="8f7f8-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="8f7f8-125"><a name="exampleref"></a>Configuración de ejemplo</span><span class="sxs-lookup"><span data-stu-id="8f7f8-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="8f7f8-126">Puede usar estos toocreate valores un entorno de prueba, o consulte toothem toobetter comprender los ejemplos de hello en este artículo.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="8f7f8-127">**Configuración de redes virtuales clásicas**</span><span class="sxs-lookup"><span data-stu-id="8f7f8-127">**Classic VNet settings**</span></span>

<span data-ttu-id="8f7f8-128">Nombre de la red virtual = RedVClásica</span><span class="sxs-lookup"><span data-stu-id="8f7f8-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="8f7f8-129">Ubicación = Oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-129">Location = West US</span></span> <br>
<span data-ttu-id="8f7f8-130">Espacios de direcciones de red virtual = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="8f7f8-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="8f7f8-131">Subred-1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="8f7f8-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="8f7f8-132">Subred de la puerta de enlace= 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="8f7f8-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="8f7f8-133">Nombre de la red local = RedLocalRMV</span><span class="sxs-lookup"><span data-stu-id="8f7f8-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="8f7f8-134">Tipo de puerta de enlace = EnrutamientoDinámico</span><span class="sxs-lookup"><span data-stu-id="8f7f8-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="8f7f8-135">**Configuración de redes virtuales de Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="8f7f8-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="8f7f8-136">Nombre de red virtual = RedRMV</span><span class="sxs-lookup"><span data-stu-id="8f7f8-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="8f7f8-137">Grupo de recursos = GR1</span><span class="sxs-lookup"><span data-stu-id="8f7f8-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="8f7f8-138">Espacios de direcciones IP de red virtual = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="8f7f8-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="8f7f8-139">Subred-1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="8f7f8-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="8f7f8-140">Subred de la puerta de enlace = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="8f7f8-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="8f7f8-141">Ubicación = Este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-141">Location = East US</span></span> <br>
<span data-ttu-id="8f7f8-142">Nombre IP público de puerta de enlace = pepip</span><span class="sxs-lookup"><span data-stu-id="8f7f8-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="8f7f8-143">Puerta de enlace de red local = LocalRedVClásica</span><span class="sxs-lookup"><span data-stu-id="8f7f8-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="8f7f8-144">Nombre de la puerta de enlace de red virtual = PuertaDeEnlaceRM</span><span class="sxs-lookup"><span data-stu-id="8f7f8-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="8f7f8-145">Configuración de direccionamiento IP de puerta de enlace = configpeip</span><span class="sxs-lookup"><span data-stu-id="8f7f8-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="8f7f8-146"><a name="createsmgw"></a>Sección 1: configurar red virtual clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="8f7f8-147">Parte 1: exportación del archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="8f7f8-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="8f7f8-148">Inicie sesión en tooyour cuenta de Azure en la consola de PowerShell de hello con derechos elevados.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="8f7f8-149">Hello siguiente cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="8f7f8-150">Después de iniciar sesión, descarga la configuración de la cuenta para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="8f7f8-151">Utilice hello toocomplete de cmdlets de PowerShell de SM esta parte de la configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="8f7f8-152">Exportar el archivo de configuración de red de Azure ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="8f7f8-153">Puede cambiar la ubicación Hola Hola tooexport tooa diferentes de ubicación de archivos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="8f7f8-154">Archivo .xml de hello abierto que descargó tooedit lo.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="8f7f8-155">Para obtener un ejemplo de archivo de configuración de red de hello, vea hello [esquema de configuración de red](https://msdn.microsoft.com/library/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="8f7f8-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="8f7f8-156">Parte 2 - Compruebe la subred de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="8f7f8-157">Hola **VirtualNetworkSites** elemento, agregue un tooyour de subred de puerta de enlace red virtual si aún no ha creado ninguno.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="8f7f8-158">Cuando se trabaja con el archivo de configuración de red de hello, subred de puerta de enlace de hello debe denominarse "GatewaySubnet" o Azure no puede reconocer y utilizarlo como una subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="8f7f8-159">**Ejemplo:**</span><span class="sxs-lookup"><span data-stu-id="8f7f8-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="8f7f8-160">Parte 3: agregar sitio de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="8f7f8-161">sitio de red local de Hello que agregará representa hello toowhich de red virtual de RM que desee tooconnect.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="8f7f8-162">Agregar un **LocalNetworkSites** elemento toohello file si no existe.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="8f7f8-163">En este momento en configuración de hello, Hola valor de VPNGatewayAddress puede ser cualquier dirección IP pública válida porque aún no hemos creado la puerta de enlace de Hola para hello VNet el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="8f7f8-164">Una vez que se crea la puerta de enlace de hello, reemplazamos esta dirección IP de marcador de posición con hello correcto dirección IP pública que se ha asignado la puerta de enlace de toohello RM.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="8f7f8-165">Parte 4: asocie Hola red virtual con el sitio de red local de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="8f7f8-166">En esta sección, se especifica el sitio de red local de Hola que desea tooconnect Hola VNet a.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="8f7f8-167">En este caso, es hello VNet el Administrador de recursos que hace referencia anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="8f7f8-168">Que los nombres de Hola que coincidan con.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-168">Make sure hello names match.</span></span> <span data-ttu-id="8f7f8-169">En este paso no se crea una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-169">This step does not create a gateway.</span></span> <span data-ttu-id="8f7f8-170">Especifica la red local de Hola que Hola puerta de enlace se conectará al.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="8f7f8-171">Parte 5: guardar el archivo hello y cargar</span><span class="sxs-lookup"><span data-stu-id="8f7f8-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="8f7f8-172">Guardar archivo hello, a continuación, importarlo tooAzure ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="8f7f8-173">Asegúrese de que se cambie la ruta de acceso Hola según sea necesario para su entorno.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="8f7f8-174">Verá un resultado similar que muestra que la importación de Hola se realizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="8f7f8-175">Parte 6: crear puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="8f7f8-176">Antes de ejecutar este ejemplo, consulte toohello toosee espera que el archivo de configuración de red que ha descargado para nombres de hello exacto que Azure.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="8f7f8-177">archivo de configuración de red de Hello contiene valores de hello para las redes virtuales clásicas.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="8f7f8-178">A veces los nombres de Hola para clásico en que redes virtuales se cambian en el archivo de configuración de red de hello al crear la configuración de red virtual clásica Hola portal de Azure debido a diferencias de toohello en los modelos de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="8f7f8-179">Por ejemplo, si ha usado hello Azure portal toocreate una red virtual clásica denominado 'VNet clásico' y creado en un grupo de recursos con el nombre 'ClassicRG', nombre de Hola que se encuentra en el archivo de configuración de red de hello es convertido too'Group red virtual clásica de ClassicRG'.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="8f7f8-180">Al especificar el nombre de Hola de una red virtual que contiene espacios, use comillas en el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="8f7f8-181">Usar hello después toocreate una puerta de enlace de enrutamiento dinámico de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="8f7f8-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="8f7f8-182">Puede comprobar estado de Hola de puerta de enlace de hello mediante hello **Get-AzureVNetGateway** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="8f7f8-183"><a name="creatermgw"></a>Sección 2: Configurar Hola puerta de enlace de red virtual de RM</span><span class="sxs-lookup"><span data-stu-id="8f7f8-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="8f7f8-184">toocreate una puerta de enlace VPN para hello RM red virtual, siga Hola siguiendo las instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="8f7f8-185">No inicie pasos Hola hasta después de que se haya recuperado la dirección IP pública de Hola para puerta de enlace de hello clásico la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="8f7f8-186">Inicie sesión en tooyour cuenta de Azure en la consola de PowerShell de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="8f7f8-187">Hello siguiente cmdlet le pide las credenciales de inicio de sesión de Hola para su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="8f7f8-188">Después de iniciar sesión, la configuración de su cuenta se descarga para que estén disponible tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="8f7f8-189">Si tiene más de una suscripción de Azure, obtenga una lista de todas ellas.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="8f7f8-190">Especifique que desea toouse de suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="8f7f8-191">Cree una puerta de enlace de red local.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-191">Create a local network gateway.</span></span> <span data-ttu-id="8f7f8-192">En una red virtual, puerta de enlace de red local de hello suele hacer referencia tooyour ubicación.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="8f7f8-193">En este caso, puerta de enlace de red local de hello hace referencia tooyour clásico de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="8f7f8-194">Asígnele un nombre por el que Azure puede hacer referencia tooit y también especificar el prefijo de espacio de dirección de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="8f7f8-195">Azure utiliza el prefijo de dirección IP de hello especificar tooidentify qué tooyour toosend de tráfico ubicación local.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="8f7f8-196">Si necesita información de hello tooadjust aquí una versión posterior, antes de crear la puerta de enlace, puede modificar el ejemplo de Hola ejecución y valores de hello.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="8f7f8-197">**-Nombre** es nombre hello desee puerta de enlace de tooassign toorefer toohello red local.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="8f7f8-198">
   **-AddressPrefix** es hello espacio de direcciones de la red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="8f7f8-199">
**-GatewayIpAddress** es la dirección IP pública de Hola de puerta de enlace de hello clásico la red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="8f7f8-200">Asegúrese de ejemplo siguiente de hello toochange se tooreflect Hola dirección IP.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="8f7f8-201">Solicitar pública IP dirección toobe toohello asignado red virtual puerta de enlace de hello VNet el Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="8f7f8-202">No se puede especificar la dirección IP de Hola que desee toouse.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="8f7f8-203">dirección IP de Hola se asigna dinámicamente toohello puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="8f7f8-204">Sin embargo, esto implica cambios en la dirección IP Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="8f7f8-205">cambios de dirección IP de puerta de enlace de red virtual de hello cuando se Hola puerta de enlace de única vez de Hola se elimina y vuelve a crear.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="8f7f8-206">No cambia en el cambio de tamaño, restablecer o en otras actualizaciones y mantenimiento internos de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="8f7f8-207">En este paso, también se establece una variable que se utilizará en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="8f7f8-208">Compruebe que la red virtual tenga una subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="8f7f8-209">Si no existe ninguna subred de puerta de enlace, agregue una.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="8f7f8-210">Asegúrese de que se denomina subred de puerta de enlace de hello *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="8f7f8-211">Recuperar la subred de hello usada para la puerta de enlace de hello ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="8f7f8-212">En este paso, también se establece una variable toobe usado en el paso siguiente de saludo.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="8f7f8-213">**-Nombre** es Hola nombre de la VNet del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="8f7f8-214">
   **-ResourceGroupName** es grupo de recursos de Hola que hello red virtual está asociado.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="8f7f8-215">subred de puerta de enlace de Hello ya debe existir para esta red virtual y debe denominarse *GatewaySubnet* toowork correctamente.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="8f7f8-216">Crear configuración de direcciones IP de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="8f7f8-217">configuración de puerta de enlace de Hello define la subred de Hola y Hola toouse de dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="8f7f8-218">Use Hola ejemplo siguiente se toocreate la configuración de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="8f7f8-219">En este paso, Hola **- SubnetId** y **- PublicIpAddressId** parámetros deben pasarse propiedad de Id. de Hola de subred de Hola y objetos de dirección IP, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="8f7f8-220">No puede usar una cadena sencilla.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-220">You can't use a simple string.</span></span> <span data-ttu-id="8f7f8-221">Estas variables se establecen en hello paso toorequest una IP pública y Hola paso tooretrieve Hola subred.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="8f7f8-222">Crear puerta de enlace de red virtual de administrador de recursos de hello ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="8f7f8-223">Hola `-VpnType` debe ser *RouteBased*.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="8f7f8-224">Puede tardar 45 minutos o más en hello toocreate de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="8f7f8-225">Copie la dirección IP pública Hola una vez creada la puerta de enlace VPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="8f7f8-226">Se usa cuando configure los parámetros de la red virtual clásica Hola red local.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="8f7f8-227">Puede usar Hola siguiente cmdlet tooretrieve Hola la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="8f7f8-228">Hello dirección IP pública aparece en hello devuelto como *IpAddress*.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="8f7f8-229">Sección 3: Modificar la configuración del sitio local de red virtual clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="8f7f8-230">En esta sección, se trabaja con hello clásico red virtual.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="8f7f8-231">Reemplace la dirección IP de marcador de posición de Hola que usó al especificar la configuración de sitio local de Hola que será usado tooconnect toohello puerta de enlace de VNet Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="8f7f8-232">Exportar archivo de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="8f7f8-233">Con un editor de texto, modifique el valor de hello para el valor de VPNGatewayAddress.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="8f7f8-234">Reemplace la dirección IP de marcador de posición de hello con dirección IP pública de Hola de puerta de enlace de administrador de recursos de hello y, a continuación, guarde los cambios de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="8f7f8-235">Hola de importación modificado tooAzure de archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="8f7f8-236"><a name="connect"></a>Sección 4: Crear una conexión entre las puertas de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="8f7f8-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="8f7f8-237">Crear una conexión entre las puertas de enlace de hello requiere PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="8f7f8-238">Puede que necesite tooadd la versión clásica de cuenta de Azure toouse Hola Hola de cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="8f7f8-239">por lo tanto, use toodo **Add-AzureAccount**.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="8f7f8-240">En la consola de PowerShell de hello, establezca la clave compartida.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="8f7f8-241">Antes de ejecutar los cmdlets de hello, consulte toohello toosee espera que el archivo de configuración de red que ha descargado para nombres de hello exacto que Azure.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="8f7f8-242">Al especificar el nombre de Hola de una red virtual que contiene espacios, use comillas simples en el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="8f7f8-243">En el ejemplo siguiente, **- VNetName** es nombre Hola de hello VNet clásico y **- LocalNetworkSiteName** es nombre hello que especificó para el sitio de red local de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="8f7f8-244">Hola **- SharedKey** es un valor que se generan y se especifica.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="8f7f8-245">En el ejemplo de Hola, hemos usado "abc123", pero puede generar y utilizar algo más complejo.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="8f7f8-246">Hola importante que es ese valor de Hola que especifique aquí debe ser Hola que mismo valor que especifique en el paso siguiente de hello al crear la conexión.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="8f7f8-247">Hola devuelto debería mostrar **estado: correcto**.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="8f7f8-248">Crear la conexión de VPN de hello ejecutando Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="8f7f8-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="8f7f8-249">Establecer variables de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="8f7f8-250">Crear conexiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-250">Create hello connection.</span></span> <span data-ttu-id="8f7f8-251">Tenga en cuenta que hello **- ConnectionType** es IPsec, no Vnet2Vnet.</span><span class="sxs-lookup"><span data-stu-id="8f7f8-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="8f7f8-252">Sección 5: comprobación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="8f7f8-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="8f7f8-253">conexión de hello tooverify desde su tooyour clásico de red virtual VNet el Administrador de recursos</span><span class="sxs-lookup"><span data-stu-id="8f7f8-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="8f7f8-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7f8-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="8f7f8-255">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8f7f8-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="8f7f8-256">conexión de hello tooverify desde el Administrador de recursos VNet tooyour red virtual clásica</span><span class="sxs-lookup"><span data-stu-id="8f7f8-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="8f7f8-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f7f8-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="8f7f8-258">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8f7f8-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="8f7f8-259"><a name="faq"></a>P+F sobre conexiones de red virtual a red virtual</span><span class="sxs-lookup"><span data-stu-id="8f7f8-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

