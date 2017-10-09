---
title: "Conectarse a un sitio de sitios de red virtual toomultiple con puerta de enlace VPN y PowerShell: clásico | Documentos de Microsoft"
description: "En este artículo le guiará a través de conectar varias instalaciones locales sitios tooa red virtual con una puerta de enlace de VPN para el modelo de implementación clásica de Hola."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="e74cf-103">Agregar una tooa de conexión de sitio a sitio red virtual con una conexión de puerta de enlace VPN existente (clásica)</span><span class="sxs-lookup"><span data-stu-id="e74cf-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e74cf-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e74cf-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="e74cf-105">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="e74cf-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="e74cf-106">Este artículo le guiará a través mediante PowerShell tooadd sitio a sitio (S2S) conexiones tooa puerta de enlace VPN que tiene una conexión existente.</span><span class="sxs-lookup"><span data-stu-id="e74cf-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="e74cf-107">Este tipo de conexión es a menudo tooas que se hace referencia una configuración de "varios sitio".</span><span class="sxs-lookup"><span data-stu-id="e74cf-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="e74cf-108">Hello pasos descritos en este artículo aplican redes toovirtual creadas mediante el modelo de implementación clásica de hello (también conocido como administración de servicios).</span><span class="sxs-lookup"><span data-stu-id="e74cf-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="e74cf-109">Estos pasos no aplican las configuraciones de conexión coexistentes tooExpressRoute/sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="e74cf-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="e74cf-110">Modelos de implementación y métodos</span><span class="sxs-lookup"><span data-stu-id="e74cf-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="e74cf-111">Esta tabla se actualiza cada vez que hay nuevos artículos y nuevas herramientas disponibles para esta configuración.</span><span class="sxs-lookup"><span data-stu-id="e74cf-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="e74cf-112">Cuando un artículo está disponible, vinculamos directamente tooit de esta tabla.</span><span class="sxs-lookup"><span data-stu-id="e74cf-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="e74cf-113">Acerca de la conexión</span><span class="sxs-lookup"><span data-stu-id="e74cf-113">About connecting</span></span>

<span data-ttu-id="e74cf-114">Puede conectar varios sitios tooa único virtual red local.</span><span class="sxs-lookup"><span data-stu-id="e74cf-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="e74cf-115">Esto resulta especialmente atractivo para crear soluciones híbridas en la nube.</span><span class="sxs-lookup"><span data-stu-id="e74cf-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="e74cf-116">Crear una puerta de enlace de red virtual de Azure de conexión de varios sitios tooyour es toocreating similar otras conexiones de sitio a sitio.</span><span class="sxs-lookup"><span data-stu-id="e74cf-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="e74cf-117">De hecho, puede usar una puerta de enlace de VPN de Azure existente, como puerta de enlace de hello es dinámico (basado en ruta).</span><span class="sxs-lookup"><span data-stu-id="e74cf-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="e74cf-118">Si ya tiene una red virtual de puerta de enlace estática tooyour conectado, puede cambiar toodynamic de tipo de puerta de enlace de hello sin necesidad de red virtual de toorebuild hello en varios sitios de orden tooaccommodate.</span><span class="sxs-lookup"><span data-stu-id="e74cf-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="e74cf-119">Antes de cambiar el tipo de enrutamiento de hello, asegúrese de que la puerta de enlace VPN local admite configuraciones de VPN basadas en enrutamiento.</span><span class="sxs-lookup"><span data-stu-id="e74cf-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="e74cf-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span><span class="sxs-lookup"><span data-stu-id="e74cf-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="e74cf-121">Puntos tooconsider</span><span class="sxs-lookup"><span data-stu-id="e74cf-121">Points tooconsider</span></span>

<span data-ttu-id="e74cf-122">**No será la red virtual de toouse capaz de hello toomake portal cambios toothis.**</span><span class="sxs-lookup"><span data-stu-id="e74cf-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="e74cf-123">Necesita el archivo de configuración de red toomake cambios toohello en lugar de usar el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="e74cf-124">Si realiza cambios en el portal de hello, sobrescribirán la configuración de referencia de varios sitios para esta red virtual.</span><span class="sxs-lookup"><span data-stu-id="e74cf-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="e74cf-125">Deben sentirse cómodos utilizando el archivo de configuración de red de Hola por tiempo Hola ha completado procedimiento de varios sitios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="e74cf-126">Sin embargo, si hay varias personas trabajando en la configuración de red, necesitará toomake seguro de que todas conocen esta limitación.</span><span class="sxs-lookup"><span data-stu-id="e74cf-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="e74cf-127">Esto no significa que no puede usar el portal de hello en absoluto.</span><span class="sxs-lookup"><span data-stu-id="e74cf-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="e74cf-128">Puede utilizarlo para todo lo demás, excepto que realiza la red virtual concreto de toothis de cambios configuración.</span><span class="sxs-lookup"><span data-stu-id="e74cf-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e74cf-129">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e74cf-129">Before you begin</span></span>

<span data-ttu-id="e74cf-130">Antes de comenzar, compruebe que dispone de los siguientes hello:</span><span class="sxs-lookup"><span data-stu-id="e74cf-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="e74cf-131">Hardware VPN compatible para cada ubicación local.</span><span class="sxs-lookup"><span data-stu-id="e74cf-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="e74cf-132">Comprobar [acerca de los dispositivos VPN para la conectividad de red Virtual](vpn-gateway-about-vpn-devices.md) tooverify si el dispositivo de Hola que desea toouse es algo que se conoce toobe compatible.</span><span class="sxs-lookup"><span data-stu-id="e74cf-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="e74cf-133">Una dirección IP IPv4 pública orientada externamente para cada dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="e74cf-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="e74cf-134">dirección IP de Hello no puede estar situado detrás de un dispositivo NAT.</span><span class="sxs-lookup"><span data-stu-id="e74cf-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="e74cf-135">Esto es un requisito.</span><span class="sxs-lookup"><span data-stu-id="e74cf-135">This is requirement.</span></span>
* <span data-ttu-id="e74cf-136">Necesitará la versión más reciente de hello tooinstall de hello cmdlets de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="e74cf-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="e74cf-137">Asegúrese de que instalar versión de Service Management (SM) de hello en la versión de administrador de recursos de toohello de adición.</span><span class="sxs-lookup"><span data-stu-id="e74cf-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="e74cf-138">Vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="e74cf-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="e74cf-139">Alguna persona con experiencia en configuración de hardware de VPN</span><span class="sxs-lookup"><span data-stu-id="e74cf-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="e74cf-140">Tendrá toohave una comprensión segura del cómo tooconfigure su dispositivo VPN o trabajar con alguien que lo tiene.</span><span class="sxs-lookup"><span data-stu-id="e74cf-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="e74cf-141">intervalos de direcciones IP de Hola que quiere toouse de la red virtual (si ya no ha creado una).</span><span class="sxs-lookup"><span data-stu-id="e74cf-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="e74cf-142">intervalos de direcciones IP de Hola para cada uno de los sitios de red local de Hola que se va a conectar.</span><span class="sxs-lookup"><span data-stu-id="e74cf-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="e74cf-143">Necesitará toomake seguro de que intervalos de direcciones IP de Hola para cada uno de los sitios de red local de Hola que desea tooconnect toodo no se superponen.</span><span class="sxs-lookup"><span data-stu-id="e74cf-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="e74cf-144">En caso contrario, el portal de Hola o hello API de REST rechazará configuración Hola que se va a cargar.</span><span class="sxs-lookup"><span data-stu-id="e74cf-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="e74cf-145">Por ejemplo, si tiene dos sitios de red local que ambos contienen Hola IP dirección intervalo 10.2.3.0/24 y tiene un paquete con una dirección de destino 10.2.3.3, Azure no sabría qué sitio va intervalos de direcciones de toosend Hola paquete toobecause Hola son que se superponen.</span><span class="sxs-lookup"><span data-stu-id="e74cf-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="e74cf-146">problemas de enrutamiento tooprevent, Azure no permite tooupload un archivo de configuración que tiene intervalos solapados.</span><span class="sxs-lookup"><span data-stu-id="e74cf-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="e74cf-147">1. Crear una VPN de sitio a sitio</span><span class="sxs-lookup"><span data-stu-id="e74cf-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="e74cf-148">Si ya tiene una VPN de sitio a sitio con una puerta de enlace de enrutamiento dinámico, perfecto.</span><span class="sxs-lookup"><span data-stu-id="e74cf-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="e74cf-149">Puede continuar demasiado[exportar opciones de configuración de red virtual de hello](#export).</span><span class="sxs-lookup"><span data-stu-id="e74cf-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="e74cf-150">Si no es así, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e74cf-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="e74cf-151">Si ya dispone de una red virtual de sitio a sitio, pero con una puerta de enlace de enrutamiento estático (basada en directivas):</span><span class="sxs-lookup"><span data-stu-id="e74cf-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="e74cf-152">Cambiar el enrutamiento de toodynamic de tipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e74cf-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="e74cf-153">Una VPN de varios sitios requiere una puerta de enlace de enrutamiento dinámico (también denominada basada en ruta).</span><span class="sxs-lookup"><span data-stu-id="e74cf-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="e74cf-154">tipo de la puerta de enlace de toochange, es necesita puerta de enlace de toofirst delete Hola existente y crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="e74cf-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="e74cf-155">Para obtener instrucciones, consulte [cómo toochange Hola tipo de enrutamiento de VPN para la puerta de enlace](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e74cf-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="e74cf-156">Configure la nueva puerta de enlace y cree un túnel de VPN.</span><span class="sxs-lookup"><span data-stu-id="e74cf-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="e74cf-157">Para obtener instrucciones, consulte [configurar una puerta de enlace de VPN en el Portal de Azure clásico hello](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e74cf-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="e74cf-158">En primer lugar, cambie la ruta de toodynamic de tipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e74cf-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="e74cf-159">Si no dispone de una red virtual de sitio a sitio:</span><span class="sxs-lookup"><span data-stu-id="e74cf-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="e74cf-160">Crear la red virtual de sitio a sitio usando estas instrucciones: [crear una red Virtual con una conexión de VPN de sitio a sitio en el Portal de Azure clásico hello](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="e74cf-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="e74cf-161">Configure una puerta de enlace de enrutamiento dinámico con estas instrucciones: [Configuración de una VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="e74cf-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="e74cf-162">Ser seguro tooselect **enrutamiento dinámico** para el tipo de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="e74cf-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="e74cf-163"><a name="export"></a>2. Exportar archivo de configuración de red de Hola</span><span class="sxs-lookup"><span data-stu-id="e74cf-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="e74cf-164">Exportar el archivo de configuración de red de Azure ejecutando el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="e74cf-165">Puede cambiar la ubicación Hola Hola tooexport tooa diferentes de ubicación de archivos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="e74cf-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="e74cf-166">3. Archivo de configuración de red de hello abierto</span><span class="sxs-lookup"><span data-stu-id="e74cf-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="e74cf-167">Abra el archivo de configuración de red de Hola que descargó en el último paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="e74cf-168">Use el editor xml que desee.</span><span class="sxs-lookup"><span data-stu-id="e74cf-168">Use any xml editor that you like.</span></span> <span data-ttu-id="e74cf-169">archivo de Hello debería ser similar siguiente toohello:</span><span class="sxs-lookup"><span data-stu-id="e74cf-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="e74cf-170">4. Agregar referencias de varios sitios</span><span class="sxs-lookup"><span data-stu-id="e74cf-170">4. Add multiple site references</span></span>
<span data-ttu-id="e74cf-171">Al agregar o quitar información de referencia de sitio, podrá realizar cambios de configuración toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="e74cf-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="e74cf-172">Agregando una nueva referencia de sitio local desencadena un nuevo túnel toocreate de Azure.</span><span class="sxs-lookup"><span data-stu-id="e74cf-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="e74cf-173">En el siguiente ejemplo de Hola, configuración de red de hello es para una conexión de sitio único.</span><span class="sxs-lookup"><span data-stu-id="e74cf-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="e74cf-174">Guardar archivo hello cuando haya terminado de realizar los cambios.</span><span class="sxs-lookup"><span data-stu-id="e74cf-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="e74cf-175">tooadd referencias a sitios adicionales (crear una configuración de varios sitio), basta con agregar líneas de "LocalNetworkSiteRef" adicionales, como se muestra en el ejemplo de Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e74cf-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="e74cf-176">5. Importar archivo de configuración de red de Hola</span><span class="sxs-lookup"><span data-stu-id="e74cf-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="e74cf-177">Importar archivo de configuración de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-177">Import hello network configuration file.</span></span> <span data-ttu-id="e74cf-178">Al importar este archivo con cambios de hello, se agregarán nuevos túneles de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="e74cf-179">túneles de Hello usará Hola puerta de enlace dinámico que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e74cf-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="e74cf-180">Puede usar portal clásico de Hola o archivo de hello tooimport de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e74cf-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="e74cf-181">6. Descargar las claves</span><span class="sxs-lookup"><span data-stu-id="e74cf-181">6. Download keys</span></span>
<span data-ttu-id="e74cf-182">Una vez que se han agregado los túneles nuevos, use Hola PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget Hola claves IPsec/IKE compartidas previamente para cada túnel.</span><span class="sxs-lookup"><span data-stu-id="e74cf-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="e74cf-183">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e74cf-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="e74cf-184">Si lo prefiere, también puede usar hello *Get Virtual Network Gateway Shared Key* tooget de API de REST Hola claves previamente compartidas.</span><span class="sxs-lookup"><span data-stu-id="e74cf-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="e74cf-185">7. Comprobación de las conexiones</span><span class="sxs-lookup"><span data-stu-id="e74cf-185">7. Verify your connections</span></span>
<span data-ttu-id="e74cf-186">Comprobar estado de túnel de varios sitios de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="e74cf-187">Después de descargar las claves de Hola para cada túnel, le interesará tooverify conexiones.</span><span class="sxs-lookup"><span data-stu-id="e74cf-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="e74cf-188">Utilice tooget 'Get-AzureVnetConnection' túnel de una lista de red virtual, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="e74cf-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="e74cf-189">VNet1 es nombre Hola de hello red virtual.</span><span class="sxs-lookup"><span data-stu-id="e74cf-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="e74cf-190">Valor devuelto del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="e74cf-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="e74cf-191">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e74cf-191">Next steps</span></span>

<span data-ttu-id="e74cf-192">toolearn más información acerca de las puertas de enlace de VPN, consulte [acerca de puertas de enlace VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="e74cf-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
