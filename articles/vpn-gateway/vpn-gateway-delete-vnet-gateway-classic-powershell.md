---
title: "Eliminación de una puerta de enlace de red virtual: PowerShell: Azure clásico | Microsoft Docs"
description: "Elimine una puerta de enlace de red virtual mediante PowerShell en el modelo de implementación clásica."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="c1303-103">Eliminación de una puerta de enlace de red virtual mediante PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="c1303-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c1303-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c1303-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="c1303-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1303-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="c1303-106">Clásico: PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1303-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="c1303-107">Este artículo le ayuda a eliminar una puerta de enlace de VPN en el modelo de implementación clásica mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1303-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="c1303-108">Una vez que elimina la puerta de enlace de red virtual, modifique el archivo de configuración de red para quitar los elementos que ya no usa.</span><span class="sxs-lookup"><span data-stu-id="c1303-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="c1303-109"><a name="connect"></a>Paso 1: Conexión con Azure</span><span class="sxs-lookup"><span data-stu-id="c1303-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="c1303-110">1. Instale los cmdlets más recientes de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1303-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="c1303-111">Descargue e instale la versión más reciente de los cmdlets de PowerShell para Azure Service Management (SM).</span><span class="sxs-lookup"><span data-stu-id="c1303-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="c1303-112">Para más información, vea [Instalación y configuración de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c1303-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="c1303-113">2. Conéctese a su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c1303-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="c1303-114">Abra la consola de PowerShell con privilegios elevados y conéctese a su cuenta.</span><span class="sxs-lookup"><span data-stu-id="c1303-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="c1303-115">Use el siguiente ejemplo para conectarse:</span><span class="sxs-lookup"><span data-stu-id="c1303-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="c1303-116"><a name="export"></a>Paso 2: Exportación y visualización del archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="c1303-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="c1303-117">Cree un directorio en el equipo y, a continuación, exporte el archivo de configuración de red al directorio.</span><span class="sxs-lookup"><span data-stu-id="c1303-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="c1303-118">Use este archivo para ver la información de la configuración actual y también para modificar la configuración de red.</span><span class="sxs-lookup"><span data-stu-id="c1303-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="c1303-119">En este ejemplo, se exporta el archivo de configuración de red a C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="c1303-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="c1303-120">Abra el archivo con un editor de texto y consulte el nombre de la red virtual clásica.</span><span class="sxs-lookup"><span data-stu-id="c1303-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="c1303-121">Cuando crea una red virtual en Azure Portal, el nombre completo que Azure usa no aparece en el portal.</span><span class="sxs-lookup"><span data-stu-id="c1303-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="c1303-122">Por ejemplo, una red virtual que parece llamarse "ClassicVNet1" en Azure Portal puede que tenga un nombre mucho más largo en el archivo de configuración de la red.</span><span class="sxs-lookup"><span data-stu-id="c1303-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="c1303-123">El nombre podría ser similar al siguiente: "Group ClassicRG1 ClassicVNet1".</span><span class="sxs-lookup"><span data-stu-id="c1303-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="c1303-124">Los nombres de las redes virtuales aparecen como **"VirtualNetworkSite name ="**.</span><span class="sxs-lookup"><span data-stu-id="c1303-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="c1303-125">Use los nombres que aparecen en el archivo de configuración de red cuando ejecute los cmdlets de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1303-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="c1303-126"><a name="delete"></a>Paso 3: Eliminación de la puerta de enlace de red virtual</span><span class="sxs-lookup"><span data-stu-id="c1303-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="c1303-127">Cuando elimina una puerta de enlace de red virtual, se desconectan todas las conexiones a la red virtual a través de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c1303-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="c1303-128">Si tiene clientes de P2S conectados a la red virtual, se desconectarán sin advertencia.</span><span class="sxs-lookup"><span data-stu-id="c1303-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="c1303-129">Este ejemplo elimina la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c1303-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="c1303-130">Asegúrese de usar el nombre completo de la red virtual como aparece en el archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="c1303-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="c1303-131">Si es correcto, el resultado mostrará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c1303-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="c1303-132"><a name="modify"></a>Paso 4: Modificación del archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="c1303-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="c1303-133">Cuando elimina una puerta de enlace de red virtual, el cmdlet no modifica el archivo de configuración de red.</span><span class="sxs-lookup"><span data-stu-id="c1303-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="c1303-134">Debe modificar el archivo para quitar los elementos que ya no se usan.</span><span class="sxs-lookup"><span data-stu-id="c1303-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="c1303-135">Las secciones siguientes lo ayudan a modificar el archivo de configuración de red que descargó.</span><span class="sxs-lookup"><span data-stu-id="c1303-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="c1303-136"><a name="lnsref"></a>Referencias de sitio de red local</span><span class="sxs-lookup"><span data-stu-id="c1303-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="c1303-137">Cuando quite la información de referencia del sitio, haga cambios en la configuración en **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="c1303-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="c1303-138">Quitar una referencia a sitio local hace que Azure elimine un túnel.</span><span class="sxs-lookup"><span data-stu-id="c1303-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="c1303-139">Según la configuración que creó, puede que no aparezca **LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="c1303-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="c1303-140">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1303-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="c1303-141"><a name="lns"></a>Sitios de red local</span><span class="sxs-lookup"><span data-stu-id="c1303-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="c1303-142">Quite los sitios locales que ya no usa.</span><span class="sxs-lookup"><span data-stu-id="c1303-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="c1303-143">Según la configuración que haya creado, es posible que no aparezca el elemento **LocalNetworkSite** en la lista.</span><span class="sxs-lookup"><span data-stu-id="c1303-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="c1303-144">En este ejemplo, solo quitamos Site3.</span><span class="sxs-lookup"><span data-stu-id="c1303-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="c1303-145"><a name="clientaddresss"></a>Grupo de direcciones de cliente</span><span class="sxs-lookup"><span data-stu-id="c1303-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="c1303-146">Si tuviera una conexión P2S a la red virtual, tendría un elemento **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="c1303-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="c1303-147">Quite los grupos de direcciones de cliente que correspondan a la puerta de enlace de red virtual que eliminó.</span><span class="sxs-lookup"><span data-stu-id="c1303-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="c1303-148">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1303-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="c1303-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="c1303-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="c1303-150">Elimine el elemento **GatewaySubnet** que corresponde a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="c1303-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="c1303-151">Ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1303-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="c1303-152"><a name="upload"></a>Paso 5: Carga del archivo de configuración de red</span><span class="sxs-lookup"><span data-stu-id="c1303-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="c1303-153">Guarde los cambios y cargue el archivo de configuración de red en Azure.</span><span class="sxs-lookup"><span data-stu-id="c1303-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="c1303-154">Asegúrese de cambiar la ruta de acceso según sea necesario para su entorno.</span><span class="sxs-lookup"><span data-stu-id="c1303-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="c1303-155">Si lo hace correctamente, el resultado será similar a este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c1303-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded