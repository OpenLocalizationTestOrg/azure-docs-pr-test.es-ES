---
title: "Conexión de Azure Stack a Azure mediante ExpressRoute"
description: "Cómo conectar redes virtuales en Azure Stack a redes virtuales en Azure mediante ExpressRoute."
services: azure-stack
documentationcenter: 
author: victorar
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 9/25/2017
ms.author: victorh
ms.openlocfilehash: aa6973939c6cfe0688f5781fdcea5d39670249df
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="connect-azure-stack-to-azure-using-expressroute"></a><span data-ttu-id="6f5fd-103">Conexión de Azure Stack a Azure mediante ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6f5fd-103">Connect Azure Stack to Azure using ExpressRoute</span></span>

<span data-ttu-id="6f5fd-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="6f5fd-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="6f5fd-105">Hay dos métodos admitidos para conectar redes virtuales de Azure Stack a redes virtuales de Azure:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-105">There are two supported methods to connect virtual networks in Azure Stack to virtual networks in Azure:</span></span>
   * <span data-ttu-id="6f5fd-106">**De sitio a sitio**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-106">**Site-to-Site**</span></span>

     <span data-ttu-id="6f5fd-107">Una conexión VPN sobre IPsec (IKE v1 e IKE v2).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-107">A VPN connection over IPsec (IKE v1 and IKE v2).</span></span> <span data-ttu-id="6f5fd-108">Este tipo de conexión requiere un dispositivo VPN o RRAS.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-108">This type of connection requires a VPN device or RRAS.</span></span> <span data-ttu-id="6f5fd-109">Para obtener más información, consulte [Conectar Azure Stack a Azure mediante VPN](azure-stack-connect-vpn.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-109">For more information, see [Connect Azure Stack to Azure using VPN](azure-stack-connect-vpn.md).</span></span>
   * <span data-ttu-id="6f5fd-110">**ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-110">**ExpressRoute**</span></span>

     <span data-ttu-id="6f5fd-111">Una conexión directa a Azure desde la implementación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-111">A direct connection to Azure from your Azure Stack deployment.</span></span> <span data-ttu-id="6f5fd-112">ExpressRoute **no** es una conexión VPN por la red pública de Internet.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-112">ExpressRoute is **not** a VPN connection over the public Internet.</span></span> <span data-ttu-id="6f5fd-113">Para obtener más información sobre Azure ExpressRoute, consulte [Información general sobre ExpressRoute](../expressroute/expressroute-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-113">For more information about Azure ExpressRoute, see [ExpressRoute overview](../expressroute/expressroute-introduction.md).</span></span>

<span data-ttu-id="6f5fd-114">En este artículo se muestra un ejemplo del uso de ExpressRoute para conectar Azure Stack a Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-114">This article shows an example using ExpressRoute to connect Azure Stack to Azure.</span></span>
## <a name="requirements"></a><span data-ttu-id="6f5fd-115">Requisitos</span><span class="sxs-lookup"><span data-stu-id="6f5fd-115">Requirements</span></span>
<span data-ttu-id="6f5fd-116">Los siguientes son requisitos específicos para conectar Azure Stack y Azure mediante ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-116">The following are specific requirements to connect Azure Stack and Azure using ExpressRoute:</span></span>
* <span data-ttu-id="6f5fd-117">Una suscripción a Azure para crear un circuito ExpressRoute y VNet en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-117">An Azure subscription to create an ExpressRoute circuit and VNets in Azure.</span></span>
* <span data-ttu-id="6f5fd-118">Un circuito ExpressRoute aprovisionado a través de un [proveedor de conectividad](../expressroute/expressroute-locations.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-118">A provisioned ExpressRoute circuit through a [connectivity provider](../expressroute/expressroute-locations.md).</span></span>
* <span data-ttu-id="6f5fd-119">Un enrutador que tenga el circuito ExpressRoute conectado a sus puertos WAN.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-119">A router that has the ExpressRoute circuit connected to its WAN ports.</span></span>
* <span data-ttu-id="6f5fd-120">El lado de LAN del enrutador está vinculado a la puerta de enlace multiinquilino de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-120">The LAN side of the router is linked to the Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="6f5fd-121">El enrutador debe admitir las conexiones VPN de sitio a sitio entre su interfaz LAN y la puerta de enlace multiinquilino de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-121">The router must support Site-to-Site VPN connections between its LAN interface and Azure Stack Multitenant Gateway.</span></span>
* <span data-ttu-id="6f5fd-122">Si se agrega más de un inquilino a la implementación de Azure Stack, el enrutador debe ser capaz de crear múltiples VRF (enrutamiento virtual y reenvío).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-122">If more than one tenant is added in your Azure Stack deployment, the router must be able to create multiple VRFs (Virtual Routing and Forwarding).</span></span>

<span data-ttu-id="6f5fd-123">En el siguiente diagrama se muestra una vista conceptual de red después de completar la configuración:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-123">The following diagram shows a conceptual networking view after you complete the configuration:</span></span>

![Diagrama conceptual](media/azure-stack-connect-expressroute/Conceptual.png)

<span data-ttu-id="6f5fd-125">**Diagrama 1**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-125">**Diagram 1**</span></span>

<span data-ttu-id="6f5fd-126">En el siguiente diagrama de arquitectura se muestra cómo varios inquilinos se conectan desde la infraestructura de Azure Stack a través del enrutador de ExpressRoute a Azure en Microsoft Edge:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-126">The following architecture diagram shows how multiple tenants connect from the Azure Stack infrastructure through the ExpressRoute router to Azure at the Microsoft edge:</span></span>

![Diagrama de la arquitectura](media/azure-stack-connect-expressroute/Architecture.png)

<span data-ttu-id="6f5fd-128">**Diagrama 2**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-128">**Diagram 2**</span></span>

<span data-ttu-id="6f5fd-129">En el ejemplo mostrado en este artículo se usa la misma arquitectura para conectarse a Azure a través de emparejamiento privado de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-129">The example shown in this article uses the same architecture to connect to Azure via ExpressRoute private peering.</span></span> <span data-ttu-id="6f5fd-130">Esto se realiza mediante una conexión VPN de sitio a sitio desde la puerta de enlace de red virtual en Azure Stack a un enrutador de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-130">It is done using a Site-to-Site VPN connection from the virtual network gateway in Azure Stack to an ExpressRoute router.</span></span> <span data-ttu-id="6f5fd-131">Los pasos siguientes en este artículo muestran cómo crear una conexión de extremo a extremo entre dos VNet de dos inquilinos distintos en Azure Stack a sus VNet correspondientes en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-131">The following steps in this article show how to create an end-to-end connection between two VNets from two different tenants in Azure Stack to their respective VNets in Azure.</span></span> <span data-ttu-id="6f5fd-132">Puede elegir agregar tantas VNet de inquilino y replicar los pasos para cada inquilino, o utilizar este ejemplo para implementar una única VNet de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-132">You can choose to add as many tenant VNets and replicate the steps for each tenant or use this example to deploy just a single tenant VNet.</span></span>

## <a name="configure-azure-stack"></a><span data-ttu-id="6f5fd-133">Configurar Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6f5fd-133">Configure Azure Stack</span></span>
<span data-ttu-id="6f5fd-134">Ahora creará los recursos que necesita para configurar el entorno de Azure Stack como inquilino.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-134">Now you create the resources you need to set up your Azure Stack environment as a tenant.</span></span> <span data-ttu-id="6f5fd-135">Los siguientes pasos muestran lo que tiene que hacer.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-135">The following steps illustrate what you need to do.</span></span> <span data-ttu-id="6f5fd-136">Estas instrucciones muestran cómo crear recursos mediante el portal de Azure Stack, pero también puede usar PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-136">These instructions show how to create resources using the Azure Stack portal, but you can also use PowerShell.</span></span>

![Pasos para recursos de red](media/azure-stack-connect-expressroute/image2.png)
### <a name="before-you-begin"></a><span data-ttu-id="6f5fd-138">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6f5fd-138">Before you begin</span></span>
<span data-ttu-id="6f5fd-139">Antes de empezar la configuración, necesita:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-139">Before you start the configuration, you need:</span></span>
* <span data-ttu-id="6f5fd-140">Una implementación de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-140">An Azure Stack deployment.</span></span>

   <span data-ttu-id="6f5fd-141">Para obtener información sobre cómo implementar Azure Stack Development Kit, consulte [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md) (Inicio rápido de implementación de Azure Stack Development Kit).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-141">For information about deploying Azure Stack Development Kit, see [Azure Stack Development Kit deployment quickstart](azure-stack-deploy-overview.md).</span></span>
* <span data-ttu-id="6f5fd-142">Una oferta de Azure Stack a la que el usuario pueda suscribirse.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-142">An offer on Azure Stack that your user can subscribe to.</span></span>

  <span data-ttu-id="6f5fd-143">Para obtener instrucciones, consulte [Máquinas virtuales disponibles para los usuarios de Azure Stack](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-143">For instructions, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

### <a name="create-network-resources-in-azure-stack"></a><span data-ttu-id="6f5fd-144">Creación de recursos de red en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6f5fd-144">Create network resources in Azure Stack</span></span>

<span data-ttu-id="6f5fd-145">Utilice los procedimientos siguientes para crear los recursos de red necesarios en Azure Stack para cada inquilino:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-145">Use the following procedures to create the required network resources in Azure Stack for each tenant:</span></span>

#### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="6f5fd-146">Creación de la red virtual y la subred de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-146">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="6f5fd-147">Inicie sesión en el portal de usuario con una cuenta de usuario (inquilino).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-147">Sign in the user portal with a user (tenant) account.</span></span>

2. <span data-ttu-id="6f5fd-148">En el portal, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-148">In the portal, click **New**.</span></span>

   ![](media/azure-stack-connect-expressroute/MAS-new.png)

3. <span data-ttu-id="6f5fd-149">Seleccione **Redes** en el menú de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-149">Select **Networking** from the Marketplace menu.</span></span>

4. <span data-ttu-id="6f5fd-150">Haga clic en **Red virtual** en el menú.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-150">Click **Virtual network** on the menu.</span></span>

5. <span data-ttu-id="6f5fd-151">Escriba los valores en los campos correspondientes usando la siguiente tabla:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-151">Type the values into the appropriate fields using the following table:</span></span>

   |<span data-ttu-id="6f5fd-152">Campo</span><span class="sxs-lookup"><span data-stu-id="6f5fd-152">Field</span></span>  |<span data-ttu-id="6f5fd-153">Valor</span><span class="sxs-lookup"><span data-stu-id="6f5fd-153">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="6f5fd-154">Nombre</span><span class="sxs-lookup"><span data-stu-id="6f5fd-154">Name</span></span>     |<span data-ttu-id="6f5fd-155">Tenant1VNet1</span><span class="sxs-lookup"><span data-stu-id="6f5fd-155">Tenant1VNet1</span></span>         |
   |<span data-ttu-id="6f5fd-156">Espacio de direcciones</span><span class="sxs-lookup"><span data-stu-id="6f5fd-156">Address space</span></span>     |<span data-ttu-id="6f5fd-157">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="6f5fd-157">10.1.0.0/16</span></span>|
   |<span data-ttu-id="6f5fd-158">Nombre de subred</span><span class="sxs-lookup"><span data-stu-id="6f5fd-158">Subnet name</span></span>     |<span data-ttu-id="6f5fd-159">Tenant1-Sub1</span><span class="sxs-lookup"><span data-stu-id="6f5fd-159">Tenant1-Sub1</span></span>|
   |<span data-ttu-id="6f5fd-160">Intervalo de direcciones de subred</span><span class="sxs-lookup"><span data-stu-id="6f5fd-160">Subnet address range</span></span>     |<span data-ttu-id="6f5fd-161">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="6f5fd-161">10.1.1.0/24</span></span>|

6. <span data-ttu-id="6f5fd-162">Debería ver la suscripción que creó anteriormente rellena en el campo **Suscripción**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-162">You should see the Subscription you created earlier populated in the **Subscription** field.</span></span>

    <span data-ttu-id="6f5fd-163">a.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-163">a.</span></span> <span data-ttu-id="6f5fd-164">Para Grupo de recursos, puede crear un grupo de recursos o, si ya tiene uno, seleccione **Usar existente**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-164">For Resource Group, you can either create a Resource Group or if you already have one, select **Use existing**.</span></span>

    <span data-ttu-id="6f5fd-165">b.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-165">b.</span></span> <span data-ttu-id="6f5fd-166">Compruebe la ubicación predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-166">Verify the default location.</span></span>

    <span data-ttu-id="6f5fd-167">c.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-167">c.</span></span> <span data-ttu-id="6f5fd-168">Haga clic en **Anclar al panel**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-168">Click **Pin to dashboard**.</span></span>

    <span data-ttu-id="6f5fd-169">d.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-169">d.</span></span> <span data-ttu-id="6f5fd-170">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-170">Click **Create**.</span></span>



#### <a name="create-the-gateway-subnet"></a><span data-ttu-id="6f5fd-171">Creación de la subred de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="6f5fd-171">Create the gateway subnet</span></span>
1. <span data-ttu-id="6f5fd-172">Abra el recurso Red virtual que acaba de crear (Tenant1VNet1) desde el panel.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-172">Open the Virtual Network resource you created (Tenant1VNet1) from the dashboard.</span></span>
2. <span data-ttu-id="6f5fd-173">En la sección Configuración, seleccione **Subredes**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-173">On the Settings section, select **Subnets**.</span></span>
3. <span data-ttu-id="6f5fd-174">Haga clic en **Subred de puerta de enlace** para agregar una subred de puerta de enlace a la red virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-174">Click **Gateway Subnet** to add a gateway subnet to the virtual network.</span></span>
   
    ![](media/azure-stack-connect-expressroute/gatewaysubnet.png)
4. <span data-ttu-id="6f5fd-175">El nombre de la subred se establece como **GatewaySubnet** de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-175">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="6f5fd-176">Las subredes de puerta de enlace son especiales y tienen que tener este nombre específico para funcionar correctamente.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-176">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="6f5fd-177">En el campo **Intervalo de direcciones**, compruebe que la dirección sea **10.1.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-177">In the **Address range** field, verify the address is **10.1.0.0/24**.</span></span>
6. <span data-ttu-id="6f5fd-178">Haga clic en **Aceptar** para crear la subred de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-178">Click **OK** to create the gateway subnet.</span></span>

#### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="6f5fd-179">Creación de la puerta de enlace de red virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-179">Create the virtual network gateway</span></span>
1. <span data-ttu-id="6f5fd-180">En el portal de usuario de Azure Stack, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-180">In the Azure Stack user portal, click **New**.</span></span>
   
2. <span data-ttu-id="6f5fd-181">Seleccione **Redes** en el menú de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-181">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="6f5fd-182">Seleccione **Puerta de enlace de red virtual** en la lista de recursos de red.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-182">Select **Virtual network gateway** from the list of network resources.</span></span>
4. <span data-ttu-id="6f5fd-183">En el campo **Nombre** escriba **GW1**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-183">In the **Name** field type **GW1**.</span></span>
5. <span data-ttu-id="6f5fd-184">Haga clic en el elemento **Red virtual** para seleccionar una red virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-184">Click the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="6f5fd-185">Seleccione **Tenant1VNet1** en la lista.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-185">Select **Tenant1VNet1** from the list.</span></span>
6. <span data-ttu-id="6f5fd-186">Haga clic el elemento de menú **Dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-186">Click the **Public IP address** menu item.</span></span> <span data-ttu-id="6f5fd-187">Cuando se abra la sección **Elegir dirección IP pública**, haga clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-187">When the **Choose public IP address** section opens click **Create new**.</span></span>
7. <span data-ttu-id="6f5fd-188">En el campo **Nombre**, escriba **GW1 PiP** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-188">In the **Name** field, type **GW1-PiP** and click **OK**.</span></span>
8. <span data-ttu-id="6f5fd-189">El **Tipo de VPN** debe tener seleccionada la opción **Route-based** (Basada en enrutamiento) de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-189">The **VPN type** should have **Route-based** selected by default.</span></span>
    <span data-ttu-id="6f5fd-190">Mantenga este ajuste.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-190">Keep this setting.</span></span>
9. <span data-ttu-id="6f5fd-191">Compruebe que la **Suscripción** y la **Ubicación** son correctas.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-191">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="6f5fd-192">Si lo desea, puede anclar el recurso al panel.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-192">You can pin the resource to the Dashboard if you want.</span></span> <span data-ttu-id="6f5fd-193">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-193">Click **Create**.</span></span>

#### <a name="create-the-local-network-gateway"></a><span data-ttu-id="6f5fd-194">Creación de la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="6f5fd-194">Create the local network gateway</span></span>

<span data-ttu-id="6f5fd-195">El propósito del recurso de la puerta de enlace de red Local es indicar la puerta de enlace remota en el otro extremo de la conexión VPN.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-195">The purpose of the Local network gateway resource is to indicate the remote gateway at the other end of the VPN connection.</span></span> <span data-ttu-id="6f5fd-196">En este ejemplo, el lado remoto es la subinterfaz LAN del enrutador de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-196">For this example, the remote side is the LAN subinterface of the ExpressRoute router.</span></span> <span data-ttu-id="6f5fd-197">Para Tenant 1 en este ejemplo, la dirección remota es 10.60.3.255, tal como se muestra en el diagrama 2.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-197">For Tenant 1 in this example, the remote address is 10.60.3.255 as shown in Diagram 2.</span></span>

1. <span data-ttu-id="6f5fd-198">Inicie sesión en la máquina física de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-198">Log in to the Azure Stack physical machine.</span></span>
2. <span data-ttu-id="6f5fd-199">Inicie sesión en el portal de usuario con su cuenta de usuario y haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-199">Sign in to the user portal with your user account and click **New**.</span></span>
3. <span data-ttu-id="6f5fd-200">Seleccione **Redes** en el menú de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-200">Select **Networking** from the Marketplace menu.</span></span>
4. <span data-ttu-id="6f5fd-201">Seleccione **local network gateway** (puerta de enlace de red local) en la lista de recursos de red.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-201">Select **local network gateway** from the list of resources.</span></span>
5. <span data-ttu-id="6f5fd-202">En el campo **Nombre**, escriba **ER-Router-GW**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-202">In the **Name** field type **ER-Router-GW**.</span></span>
6. <span data-ttu-id="6f5fd-203">Para el campo **Dirección IP**, consulte el diagrama 2.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-203">For the **IP address** field, refer to Diagram 2.</span></span> <span data-ttu-id="6f5fd-204">La dirección IP de la subinterfaz LAN del enrutador de ExpressRoute para Tenant 1 es 10.60.3.255.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-204">The IP address of the ExpressRoute router's LAN subinterface for Tenant 1 is 10.60.3.255.</span></span> <span data-ttu-id="6f5fd-205">Para su propio entorno, escriba la dirección IP de la interfaz correspondiente a su enrutador.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-205">For your own environment, type the IP address of your router's corresponding interface.</span></span>
7. <span data-ttu-id="6f5fd-206">En el campo **Espacio de direcciones**, escriba el espacio de direcciones de las VNet que van a conectarse con Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-206">In the **Address Space** field, type the address space of the VNets that you want to connect to in Azure.</span></span> <span data-ttu-id="6f5fd-207">Para este ejemplo, consulte el diagrama 2.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-207">For this example, refer to Diagram 2.</span></span> <span data-ttu-id="6f5fd-208">Para Tenant 1, tenga en cuenta que las subredes necesarias son **192.168.2.0/24** (esta es la VNet de hub en Azure) y **10.100.0.0/16** (esta es la VNet de spoke en Azure).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-208">For Tenant 1, notice that the required subnets are **192.168.2.0/24** (this is the Hub Vnet in Azure) and **10.100.0.0/16** (this is the Spoke VNet in Azure).</span></span> <span data-ttu-id="6f5fd-209">Escriba las subredes correspondientes para su propio entorno.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-209">Type the corresponding subnets for your own environment.</span></span>
   > [!IMPORTANT]
   > <span data-ttu-id="6f5fd-210">En este ejemplo se da por supuesto que usa rutas estáticas para la conexión VPN de sitio a sitio entre la puerta de enlace de Azure Stack y el enrutador de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-210">This example assumes you are using static routes for the Site-to-Site VPN connection between the Azure Stack gateway and the ExpressRoute router.</span></span>

8. <span data-ttu-id="6f5fd-211">Compruebe que **Suscripción**, **Grupo de recursos** y **Ubicación** sean correctos y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-211">Verify that your **Subscription**, **Resource Group**, and **Location** are all correct and click **Create**.</span></span>

#### <a name="create-the-connection"></a><span data-ttu-id="6f5fd-212">Creación de la conexión</span><span class="sxs-lookup"><span data-stu-id="6f5fd-212">Create the connection</span></span>
1. <span data-ttu-id="6f5fd-213">En el portal de usuario de Azure Stack, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-213">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="6f5fd-214">Seleccione **Redes** en el menú de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-214">Select **Networking** from the Marketplace menu.</span></span>
3. <span data-ttu-id="6f5fd-215">Seleccione **Conexión** en la lista de recursos.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-215">Select **Connection** from the list of resources.</span></span>
4. <span data-ttu-id="6f5fd-216">En la sección **Conceptos básicos**, elija **De sitio a sitio (IPsec)** como el **Tipo de conexión**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-216">In the **Basics** settings section, choose **Site-to-site (IPSec)** as the **Connection type**.</span></span>
5. <span data-ttu-id="6f5fd-217">Seleccione **Suscripción**, **Grupo de recursos** y **Ubicación** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-217">Select the **Subscription**, **Resource Group**, and **Location** and click **OK**.</span></span>
6. <span data-ttu-id="6f5fd-218">En la sección **Configuración**, haga clic en **Puerta de enlace de red virtual** y haga clic en **GW1**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-218">In the **Settings** section,  click **Virtual network gateway** click **GW1**.</span></span>
7. <span data-ttu-id="6f5fd-219">Haga clic en **Puerta de enlace de red local**y haga clic en **ER Router GW**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-219">Click **Local network gateway**, and click **ER Router GW**.</span></span>
8. <span data-ttu-id="6f5fd-220">En el campo **Nombre de la conexión**, escriba **ConnectToAzure**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-220">In the **Connection Name** field, type **ConnectToAzure**.</span></span>
9. <span data-ttu-id="6f5fd-221">En el campo **Clave compartida (PSK)**, escriba **abc123** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-221">In the **Shared key (PSK)** field, type **abc123** and click **OK**.</span></span>
10. <span data-ttu-id="6f5fd-222">En la sección **Resumen**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-222">On the **Summary** section, click **OK**.</span></span>

    <span data-ttu-id="6f5fd-223">Una vez que se haya creado la conexión, puede ver la dirección IP pública que utiliza la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-223">After the connection is created, you can see the public IP address used by the virtual network gateway.</span></span> <span data-ttu-id="6f5fd-224">Para buscar la dirección en el portal de Azure Stack, vaya a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-224">To find the address in the Azure Stack portal, browse to your Virtual network gateway.</span></span> <span data-ttu-id="6f5fd-225">En **Información general**, busque la **Dirección IP pública**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-225">In **Overview**, find the **Public IP address**.</span></span> <span data-ttu-id="6f5fd-226">Anote esta dirección; se usará como *Dirección IP interna* en la sección siguiente (si corresponde su implementación).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-226">Note this address; you will use it as the *Internal IP address* in the next section (if applicable for your deployment).</span></span>

    ![](media/azure-stack-connect-expressroute/GWPublicIP.png)

#### <a name="create-a-virtual-machine"></a><span data-ttu-id="6f5fd-227">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-227">Create a virtual machine</span></span>
<span data-ttu-id="6f5fd-228">Para validar los datos que se desplazan a través de la conexión VPN, es necesario que las máquinas virtuales envíen y reciban datos en cada VNet de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-228">To validate data traveling through the VPN Connection, you need virtual machines to send and receive data in the Azure Stack Vnet.</span></span> <span data-ttu-id="6f5fd-229">Ahora, cree una máquina virtual y colóquela en la subred de máquina virtual en la red virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-229">Create a virtual machine now and put it in your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="6f5fd-230">En el portal de usuario de Azure Stack, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-230">In the Azure Stack user portal, click **New**.</span></span>
2. <span data-ttu-id="6f5fd-231">Seleccione **Máquinas virtuales** en el menú de Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-231">Select **Virtual Machines** from the Marketplace menu.</span></span>
3. <span data-ttu-id="6f5fd-232">En la lista de imágenes de máquinas virtuales, seleccione la imagen **Windows Server 2016 Datacenter Eval** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-232">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image and click **Create**.</span></span>
4. <span data-ttu-id="6f5fd-233">En la sección **Conceptos básicos**, en el campo **Nombre** escriba **VM01**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-233">On the **Basics** section, in the **Name** field type **VM01**.</span></span>
5. <span data-ttu-id="6f5fd-234">Escriba un nombre de usuario y una contraseña válidos.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-234">Type a valid user name and password.</span></span> <span data-ttu-id="6f5fd-235">Usará esta cuenta para iniciar sesión en la máquina virtual una vez creada.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-235">You’ll use this account to log in to the VM after it has been created.</span></span>
6. <span data-ttu-id="6f5fd-236">Proporcione **Suscripción**, **Grupo de recursos** y **Ubicación** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-236">Provide a **Subscription**, **Resource Group**, and **Location** and then click **OK**.</span></span>
7. <span data-ttu-id="6f5fd-237">En la sección **Tamaño**, haga clic en un tamaño de máquina virtual para esta instancia y luego haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-237">On the **Size** section, click a virtual machine size for this instance and then click **Select**.</span></span>
8. <span data-ttu-id="6f5fd-238">En la sección **Configuración**, acepte los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-238">On the **Settings** section, you can accept the defaults.</span></span> <span data-ttu-id="6f5fd-239">Pero asegúrese de que la red virtual seleccionada sea **Tenant1VNet1** y la subred esté establecida en **10.1.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-239">But ensure the virtual network selected is **Tenant1VNet1** and the subnet is set to **10.1.1.0/24**.</span></span> <span data-ttu-id="6f5fd-240">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-240">Click **OK**.</span></span>
9. <span data-ttu-id="6f5fd-241">Revise la configuración en la sección **Resumen** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-241">Review the settings on the **Summary** section and click **OK**.</span></span>

<span data-ttu-id="6f5fd-242">Para cada VNet de inquilino a la que desee conectarse, repita los pasos anteriores de la sección **Creación de la red virtual y la subred de máquina virtual** a la **Creación de una máquina virtual**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-242">For each tenant VNet you want to connect, repeat the previous steps from **Create the virtual network and VM subnet** through **Create a virtual machine** sections.</span></span>

### <a name="configure-the-nat-virtual-machine-for-gateway-traversal"></a><span data-ttu-id="6f5fd-243">Configuración de la máquina virtual de NAT para cada recorrido de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="6f5fd-243">Configure the NAT virtual machine for gateway traversal</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6f5fd-244">Esta sección está dirigida únicamente a implementaciones de Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-244">This section is for Azure Stack Development Kit deployments only.</span></span> <span data-ttu-id="6f5fd-245">La NAT no es necesaria para las implementaciones de varios nodos.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-245">The NAT is not needed for multi-node deployments.</span></span>

<span data-ttu-id="6f5fd-246">El Azure Stack Development Kit está autocontenido y aislado de la red en el que se implementa el host físico.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-246">The Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed.</span></span> <span data-ttu-id="6f5fd-247">Por lo tanto, la red de VIP “externa” a la que están conectadas las puertas de enlace no es externa, sino que, está oculta detrás de un enrutador que realiza la traducción de direcciones de red (NAT).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-247">So, the “External” VIP network that the gateways are connected to is not external, but instead is hidden behind a router doing Network Address Translation (NAT).</span></span>
 
<span data-ttu-id="6f5fd-248">El enrutador es una máquina virtual Windows Server (**AzS-BGPNAT01**) que ejecuta el rol de Servicios de enrutamiento y acceso remoto (RRAS) en la infraestructura de Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-248">The router is a Windows Server virtual machine (**AzS-BGPNAT01**) running the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="6f5fd-249">Tiene que configurar NAT en la máquina virtual AzS-BGPNAT01 para permitir la conexión VPN de sitio a sitio en ambos extremos.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-249">You must configure NAT on the AzS-BGPNAT01 virtual machine to allow the Site-to-Site VPN Connection to connect on both ends.</span></span>

#### <a name="configure-the-nat"></a><span data-ttu-id="6f5fd-250">Configuración de la NAT</span><span class="sxs-lookup"><span data-stu-id="6f5fd-250">Configure the NAT</span></span>

1. <span data-ttu-id="6f5fd-251">Inicie sesión en el equipo físico de Azure Stack con su cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-251">Log in to the Azure Stack physical machine with your administrator account.</span></span>
2. <span data-ttu-id="6f5fd-252">Copie y edite el siguiente script de PowerShell y ejecútelo en un Windows PowerShell ISE con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-252">Copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="6f5fd-253">Reemplace la contraseña de administrador.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-253">Replace your administrator password.</span></span> <span data-ttu-id="6f5fd-254">La dirección devuelta es la *Dirección de BGPNAT externo*.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-254">The address returned is your *External BGPNAT address*.</span></span>

   ```
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "azs-bgpnat01" `
    -Password $Password
   ```
4. <span data-ttu-id="6f5fd-255">Para configurar la NAT, copie y edite el siguiente script de PowerShell y ejecútelo en un Windows PowerShell ISE con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-255">To configure the NAT, copy and edit the following PowerShell script and run in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="6f5fd-256">Edite el script para reemplazar la *Dirección de BGPNAT externo* y la *Dirección IP interna* (que anotó anteriormente en la sección **Creación de la conexión**).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-256">Edit the script to replace the *External BGPNAT address* and *Internal IP address* (which you noted previously in the **Create the Connection** section).</span></span>

   <span data-ttu-id="6f5fd-257">En los diagramas de ejemplo, la *Dirección de BGPNAT externo* es 10.10.0.62 y la *Dirección IP interna* es 192.168.102.1.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-257">In the example diagrams, the *External BGPNAT address* is 10.10.0.62 and the *Internal IP address* is 192.168.102.1.</span></span>

   ```
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName azs-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

## <a name="configure-azure"></a><span data-ttu-id="6f5fd-258">Configuración de Azure</span><span class="sxs-lookup"><span data-stu-id="6f5fd-258">Configure Azure</span></span>
<span data-ttu-id="6f5fd-259">Ahora que ha completado la configuración de Azure Stack, puede implementar algunos recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-259">Now that you have completed the Azure Stack configuration, you can deploy some Azure resources.</span></span> <span data-ttu-id="6f5fd-260">El siguiente diagrama muestra una red virtual de inquilino de ejemplo en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-260">The following diagram shows a sample tenant virtual network in Azure.</span></span> <span data-ttu-id="6f5fd-261">Puede usar cualquier esquema de nombres y de direccionamiento para VNet en Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-261">You can use any name and addressing scheme for your VNet in Azure.</span></span> <span data-ttu-id="6f5fd-262">Sin embargo, el intervalo de direcciones de las VNet en Azure y Azure Stack debe ser único y no superponerse.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-262">However, the address range of the VNets in Azure and Azure Stack must be unique and not overlap.</span></span>

![VNet de Azure](media/azure-stack-connect-expressroute/AzureArchitecture.png)

<span data-ttu-id="6f5fd-264">**Diagrama 3**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-264">**Diagram 3**</span></span>

<span data-ttu-id="6f5fd-265">Los recursos que se implementan en Azure son similares a los recursos que se implementar en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-265">The resources you deploy in Azure are similar to the resources you deployed in Azure Stack.</span></span> <span data-ttu-id="6f5fd-266">De forma similar, se implementan:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-266">Similarly, you deploy:</span></span>
* <span data-ttu-id="6f5fd-267">Redes virtuales y subredes</span><span class="sxs-lookup"><span data-stu-id="6f5fd-267">Virtual networks and subnets</span></span>
* <span data-ttu-id="6f5fd-268">Una subred de puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="6f5fd-268">A gateway subnet</span></span>
* <span data-ttu-id="6f5fd-269">Una puerta de enlace de red virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-269">A virtual network gateway</span></span>
* <span data-ttu-id="6f5fd-270">Una conexión</span><span class="sxs-lookup"><span data-stu-id="6f5fd-270">A connection</span></span>
* <span data-ttu-id="6f5fd-271">Un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6f5fd-271">An ExpressRoute circuit</span></span>

<span data-ttu-id="6f5fd-272">La infraestructura de red de Azure de ejemplo está configurada de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-272">The example Azure network infrastructure is configured in the following way:</span></span>
* <span data-ttu-id="6f5fd-273">Se utiliza un modelo estándar de VNet de hub (192.168.2.0/24) y spoke (10.100.0.0./16).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-273">A standard hub (192.168.2.0/24) and spoke (10.100.0.0./16) VNet model is used.</span></span>
* <span data-ttu-id="6f5fd-274">Las cargas de trabajo se implementan en la VNet de spoke y el circuito ExpressRoute se conecta a la VNet de hub.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-274">The workloads are deployed in the spoke Vnet and the ExpressRoute circuit is connected to the hub VNet.</span></span>
* <span data-ttu-id="6f5fd-275">Las dos VNet están vinculadas mediante la característica de emparejamiento de VNET.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-275">The two VNets are linked using the VNet peering feature.</span></span>

### <a name="configure-vnets"></a><span data-ttu-id="6f5fd-276">Configuración de VNet</span><span class="sxs-lookup"><span data-stu-id="6f5fd-276">Configure Vnets</span></span>
1. <span data-ttu-id="6f5fd-277">Inicie sesión en Azure Portal con las credenciales de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-277">Sign in to the Azure portal with your Azure credentials.</span></span>
2. <span data-ttu-id="6f5fd-278">Cree la VNet de hub con el espacio de direcciones 192.168.2.0/24.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-278">Create the hub VNet using the 192.168.2.0/24 address space.</span></span> <span data-ttu-id="6f5fd-279">Cree una subred con el intervalo de direcciones 192.168.2.0/25 y agregue una subred de puerta de enlace con el intervalo de direcciones 192.168.2.128/27.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-279">Create a subnet using the 192.168.2.0/25 address range, and add a gateway subnet using the 192.168.2.128/27 address range.</span></span>
3. <span data-ttu-id="6f5fd-280">Cree la VNet de spoke con el intervalo de direcciones 10.100.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-280">Create the spoke VNet and subnet using the 10.100.0.0/16 address range.</span></span>


<span data-ttu-id="6f5fd-281">Para obtener más información sobre cómo crear redes virtuales en Azure, consulte [Creación de una red virtual con varias subredes](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-281">For more information about creating virtual networks in Azure, see [Create a virtual network with multiple subnets](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

### <a name="configure-an-expressroute-circuit"></a><span data-ttu-id="6f5fd-282">Configuración de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6f5fd-282">Configure an ExpressRoute circuit</span></span>

1. <span data-ttu-id="6f5fd-283">Revise los requisitos previos de ExpressRoute en [Requisitos previos y lista de comprobación de ExpressRoute](../expressroute/expressroute-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-283">Review the ExpressRoute prerequisites in [ExpressRoute prerequisites & checklist](../expressroute/expressroute-prerequisites.md).</span></span>
2. <span data-ttu-id="6f5fd-284">Siga los pasos de [Creación y modificación de un circuito ExpressRoute](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) para crear un circuito ExpressRoute con su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-284">Follow the steps in [Create and modify an ExpressRoute circuit](../expressroute/expressroute-howto-circuit-portal-resource-manager.md) to create an ExpressRoute circuit using your Azure subscription.</span></span>
3. <span data-ttu-id="6f5fd-285">Comparta la clave de servicio del paso anterior con su anfitrión o proveedor para aprovisionar el circuito ExpressRoute en su extremo.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-285">Share the service key from the previous step with your hoster/provider to provision your ExpressRoute circuit at their end.</span></span>
4. <span data-ttu-id="6f5fd-286">Siga los pasos de [Creación y modificación del emparejamiento de un circuito ExpressRoute](../expressroute/expressroute-howto-routing-portal-resource-manager.md) para configurar el emparejamiento privado en el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-286">Follow the steps in [Create and modify peering for an ExpressRoute circuit](../expressroute/expressroute-howto-routing-portal-resource-manager.md) to configure private peering on the ExpressRoute circuit.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="6f5fd-287">Creación de la puerta de enlace de red virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-287">Create the virtual network gateway</span></span>

* <span data-ttu-id="6f5fd-288">Siga los pasos de [Configuración de una puerta de enlace de red virtual para ExpressRoute con PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) para crear una puerta de enlace de red virtual para ExpressRoute en la VNet de hub.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-288">Follow the steps in [Configure a virtual network gateway for ExpressRoute using PowerShell](../expressroute/expressroute-howto-add-gateway-resource-manager.md) to create a virtual network gateway for ExpressRoute in the hub VNet.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="6f5fd-289">Creación de la conexión</span><span class="sxs-lookup"><span data-stu-id="6f5fd-289">Create the connection</span></span>

* <span data-ttu-id="6f5fd-290">Para vincular el circuito ExpressRoute con la VNet de hub, siga los pasos de [Conexión de una red virtual a un circuito ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-290">To link the ExpressRoute circuit to the hub VNet, follow the steps in [Connect a virtual network to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>

### <a name="peer-the-vnets"></a><span data-ttu-id="6f5fd-291">Empareje las VNet</span><span class="sxs-lookup"><span data-stu-id="6f5fd-291">Peer the Vnets</span></span>

* <span data-ttu-id="6f5fd-292">Empareje las VNet de hub y spoke según los pasos de [Creación de un emparejamiento de redes virtuales con Azure Portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6f5fd-292">Peer the Hub and Spoke VNets using the steps in [Create a virtual network peering using the Azure portal](../virtual-network/virtual-networks-create-vnetpeering-arm-portal.md).</span></span> <span data-ttu-id="6f5fd-293">Al configurar el emparejamiento de VNet, asegúrese de seleccionar las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-293">When configuring VNet peering, ensure you select the following options:</span></span>
   * <span data-ttu-id="6f5fd-294">De hub a spoke: **Permitir tránsito de puerta de enlace**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-294">From hub to spoke: **Allow gateway transit**</span></span>
   * <span data-ttu-id="6f5fd-295">De spoke a hub: **Usar puerta de enlace remota**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-295">From spoke to hub: **Use remote gateway**</span></span>

### <a name="create-a-virtual-machine"></a><span data-ttu-id="6f5fd-296">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="6f5fd-296">Create a virtual machine</span></span>

* <span data-ttu-id="6f5fd-297">Implemente las máquinas virtuales de carga de trabajo en la VNet de spoke.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-297">Deploy your workload virtual machines into the spoke VNet.</span></span>

<span data-ttu-id="6f5fd-298">Repita estos pasos para cualquier VNet de inquilino adicional que desee conectar en Azure a través de sus circuitos ExpressRoute correspondientes.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-298">Repeat these steps for any additional tenant VNets you want to connect in Azure through their respective ExpressRoute circuits.</span></span>

## <a name="configure-the-router"></a><span data-ttu-id="6f5fd-299">Configuración del enrutador</span><span class="sxs-lookup"><span data-stu-id="6f5fd-299">Configure the router</span></span>

<span data-ttu-id="6f5fd-300">Puede usar el siguiente diagrama de infraestructura de un extremo a otro para guiar la configuración del enrutador ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-300">You can use the following end-to-end infrastructure diagram to guide the configuration of your ExpressRoute Router.</span></span> <span data-ttu-id="6f5fd-301">Este diagrama muestra dos inquilinos (Tenant 1 y Tenant 2) con sus circuitos ExpressRoute correspondientes.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-301">This diagram shows two tenants (Tenant 1 and Tenant 2) with their respective Express Route circuits.</span></span> <span data-ttu-id="6f5fd-302">Cada uno está vinculado a su propio VRF (enrutamiento virtual y reenvío) en el lado LAN y WAN del enrutador ExpressRoute para garantizar el aislamiento de extremo a extremo entre los dos inquilinos.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-302">Each is linked to their own VRF (Virtual Routing and Forwarding) in the LAN and WAN side of the ExpressRoute router to ensure end-to-end isolation between the two tenants.</span></span> <span data-ttu-id="6f5fd-303">Anote las direcciones IP usadas en las interfaces del enrutador a medida que siga la configuración del ejemplo.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-303">Note the IP addresses used in the router interfaces as you follow the sample configuration.</span></span>

![Diagrama de un extremo a otro](media/azure-stack-connect-expressroute/EndToEnd.png)

<span data-ttu-id="6f5fd-305">**Diagrama 4**</span><span class="sxs-lookup"><span data-stu-id="6f5fd-305">**Diagram 4**</span></span>

<span data-ttu-id="6f5fd-306">Puede usar cualquier enrutador que admita VPN de IKEv2 y BGP para finalizar la conexión VPN de sitio a sitio desde Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-306">You can use any router that supports IKEv2 VPN and BGP to terminate the Site-to-Site VPN connection from Azure Stack.</span></span> <span data-ttu-id="6f5fd-307">El mismo enrutador se utiliza para conectarse a Azure con un circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-307">The same router is used to connect to Azure using an ExpressRoute circuit.</span></span> 

<span data-ttu-id="6f5fd-308">Este es un ejemplo de configuración de Cisco ASR 1000 que admite la infraestructura de red que se muestra en el Diagrama 4:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-308">Here is a sample configuration from a Cisco ASR 1000 that supports the network infrastructure shown in Diagram 4:</span></span>

```
ip vrf Tenant 1
 description Routing Domain for PRIVATE peering to Azure for Tenant 1
 rd 1:1
!
ip vrf Tenant 2
 description Routing Domain for PRIVATE peering to Azure for Tenant 2
 rd 1:5
!
crypto ikev2 proposal V2-PROPOSAL2 
description IKEv2 proposal for Tenant 1 
encryption aes-cbc-256
 integrity sha256
 group 2
crypto ikev2 proposal V4-PROPOSAL2 
description IKEv2 proposal for Tenant 2 
encryption aes-cbc-256
 integrity sha256
 group 2
!
crypto ikev2 policy V2-POLICY2 
description IKEv2 Policy for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 proposal V2-PROPOSAL2
description IKEv2 Policy for Tenant 2
crypto ikev2 policy V4-POLICY2 
 match fvrf Tenant 2
 match address local 10.60.3.251
 proposal V4-PROPOSAL2
!
crypto ikev2 profile V2-PROFILE
description IKEv2 profile for Tenant 1 
match fvrf Tenant 1
 match address local 10.60.3.255
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 1
!
crypto ikev2 profile V4-PROFILE
description IKEv2 profile for Tenant 2
 match fvrf Tenant 2
 match address local 10.60.3.251
 match identity remote any
 authentication remote pre-share key abc123
 authentication local pre-share key abc123
 ivrf Tenant 2
!
crypto ipsec transform-set V2-TRANSFORM2 esp-gcm 256 
 mode tunnel
crypto ipsec transform-set V4-TRANSFORM2 esp-gcm 256 
 mode tunnel
!
crypto ipsec profile V2-PROFILE
 set transform-set V2-TRANSFORM2 
 set ikev2-profile V2-PROFILE
!
crypto ipsec profile V4-PROFILE
 set transform-set V4-TRANSFORM2 
 set ikev2-profile V4-PROFILE
!
interface Tunnel10
description S2S VPN Tunnel for Tenant 1
 ip vrf forwarding Tenant 1
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.211
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf Tenant 1
 tunnel protection ipsec profile V2-PROFILE
!
interface Tunnel20
description S2S VPN Tunnel for Tenant 2
 ip vrf forwarding Tenant 2
 ip address 11.0.0.2 255.255.255.252
 ip tcp adjust-mss 1350
 tunnel source TenGigabitEthernet0/1/0.213
 tunnel mode ipsec ipv4
 tunnel destination 10.10.0.62
 tunnel vrf VNET3
 tunnel protection ipsec profile V4-PROFILE
!
interface GigabitEthernet0/0/1
 description PRIMARY Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/1.100
description Primary WAN interface of Tenant 1
 description PRIMARY ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.1 255.255.255.252
!
interface GigabitEthernet0/0/1.102
description Primary WAN interface of Tenant 2
 description PRIMARY ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.17 255.255.255.252
!
interface GigabitEthernet0/0/2
 description BACKUP Express Route Link to AZURE over Equinix
 no ip address
 negotiation auto
!
interface GigabitEthernet0/0/2.100
description Secondary WAN interface of Tenant 1
 description BACKUP ER link supporting Tenant 1 to Azure
 encapsulation dot1Q 101
 ip vrf forwarding Tenant 1
 ip address 192.168.1.5 255.255.255.252
!
interface GigabitEthernet0/0/2.102
description Secondary WAN interface of Tenant 2 
description BACKUP ER link supporting Tenant 2 to Azure
 encapsulation dot1Q 102
 ip vrf forwarding Tenant 2
 ip address 192.168.1.21 255.255.255.252
!
interface TenGigabitEthernet0/1/0
 description Downlink to ---Port 1/47
 no ip address
!
interface TenGigabitEthernet0/1/0.211
 description LAN interface of Tenant 1
description Downlink to --- Port 1/47.211
 encapsulation dot1Q 211
 ip vrf forwarding Tenant 1
 ip address 10.60.3.255 255.255.255.254
!
interface TenGigabitEthernet0/1/0.213
description LAN interface of Tenant 2
 description Downlink to --- Port 1/47.213
 encapsulation dot1Q 213
 ip vrf forwarding Tenant 2
 ip address 10.60.3.251 255.255.255.254
!
router bgp 65530
 bgp router-id <removed>
 bgp log-neighbor-changes
 description BGP neighbor config and route advertisement for Tenant 1 VRF 
 address-family ipv4 vrf Tenant 1
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.254 mask 255.255.255.254
  network 192.168.1.0 mask 255.255.255.252
  network 192.168.1.4 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65100
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 1
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.254 remote-as 4232570301
  neighbor 10.60.3.254 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.254 activate
  neighbor 10.60.3.254 route-map BLOCK-ALL out
  neighbor 192.168.1.2 remote-as 12076
  neighbor 192.168.1.2 description PRIMARY ER peer for Tenant 1 to Azure
  neighbor 192.168.1.2 ebgp-multihop 5
  neighbor 192.168.1.2 activate
  neighbor 192.168.1.2 soft-reconfiguration inbound
  neighbor 192.168.1.2 route-map Tenant 1-ONLY out
  neighbor 192.168.1.6 remote-as 12076
  neighbor 192.168.1.6 description BACKUP ER peer for Tenant 1 to Azure
  neighbor 192.168.1.6 ebgp-multihop 5
  neighbor 192.168.1.6 activate
  neighbor 192.168.1.6 soft-reconfiguration inbound
  neighbor 192.168.1.6 route-map Tenant 1-ONLY out
  maximum-paths 8
 exit-address-family
 !
description BGP neighbor config and route advertisement for Tenant 2 VRF 
address-family ipv4 vrf Tenant 2
  network 10.1.0.0 mask 255.255.0.0
  network 10.60.3.250 mask 255.255.255.254
  network 192.168.1.16 mask 255.255.255.252
  network 192.168.1.20 mask 255.255.255.252
  neighbor 10.10.0.62 remote-as 65300
  neighbor 10.10.0.62 description VPN-BGP-PEER-for-Tenant 2
  neighbor 10.10.0.62 ebgp-multihop 5
  neighbor 10.10.0.62 activate
  neighbor 10.60.3.250 remote-as 4232570301
  neighbor 10.60.3.250 description LAN peer for CPEC:INET:2112 VRF
  neighbor 10.60.3.250 activate
  neighbor 10.60.3.250 route-map BLOCK-ALL out
  neighbor 192.168.1.18 remote-as 12076
  neighbor 192.168.1.18 description PRIMARY ER peer for Tenant 2 to Azure
  neighbor 192.168.1.18 ebgp-multihop 5
  neighbor 192.168.1.18 activate
  neighbor 192.168.1.18 soft-reconfiguration inbound
  neighbor 192.168.1.18 route-map VNET-ONLY out
  neighbor 192.168.1.22 remote-as 12076
  neighbor 192.168.1.22 description BACKUP ER peer for Tenant 2 to Azure
  neighbor 192.168.1.22 ebgp-multihop 5
  neighbor 192.168.1.22 activate
  neighbor 192.168.1.22 soft-reconfiguration inbound
  neighbor 192.168.1.22 route-map VNET-ONLY out
  maximum-paths 8
 exit-address-family
!
ip forward-protocol nd
!
ip as-path access-list 1 permit ^$
ip route vrf Tenant 1 10.1.0.0 255.255.0.0 Tunnel10
ip route vrf Tenant 2 10.1.0.0 255.255.0.0 Tunnel20
!
ip prefix-list BLOCK-ALL seq 5 deny 0.0.0.0/0 le 32
!
route-map BLOCK-ALL permit 10
 match ip address prefix-list BLOCK-ALL
!
route-map VNET-ONLY permit 10
 match as-path 1
!
```

## <a name="test-the-connection"></a><span data-ttu-id="6f5fd-309">Comprobación de la conexión</span><span class="sxs-lookup"><span data-stu-id="6f5fd-309">Test the connection</span></span>

<span data-ttu-id="6f5fd-310">Pruebe la conexión después de establecer la conexión de sitio a sitio y el circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-310">Test your connection after establishing the Site-to-Site connection and the ExpressRoute circuit.</span></span> <span data-ttu-id="6f5fd-311">Esta tarea es sencilla.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-311">This task is simple.</span></span>  <span data-ttu-id="6f5fd-312">Inicie sesión en una de las máquinas virtuales creadas en la VNet de Azure y haga ping a la máquina virtual que creó en el entorno de Azure Stack o viceversa.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-312">Log on to one of the virtual machines you created in your Azure VNet and ping the virtual machine you created in the Azure Stack environment, or vice versa.</span></span> 

<span data-ttu-id="6f5fd-313">Para asegurarse de enviar el tráfico a través de conexiones de sitio a sitio y ExpressRoute, debe hacer ping a la dirección IP dedicada (DIP) de la máquina virtual en ambos extremos y no a la dirección VIP de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-313">To ensure you are sending the traffic through the Site-to-Site and ExpressRoute connections, you must ping the dedicated IP (DIP) address of the virtual machine at both ends and not the VIP address of the virtual machine.</span></span> <span data-ttu-id="6f5fd-314">Para ello, tiene que encontrar y anotar la dirección en el otro extremo de la conexión.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-314">So, you must find and note the address on the other end of the connection.</span></span>

### <a name="allow-icmp-in-through-the-firewall"></a><span data-ttu-id="6f5fd-315">Permitir que ICMP pase por el firewall</span><span class="sxs-lookup"><span data-stu-id="6f5fd-315">Allow ICMP in through the firewall</span></span>
<span data-ttu-id="6f5fd-316">De manera predeterminada, Windows Server 2016 no permite que los paquetes ICMP pasen por el firewall.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-316">By default, Windows Server 2016 does not allow ICMP packets in through the firewall.</span></span> <span data-ttu-id="6f5fd-317">Por lo tanto, para cada máquina virtual que use en la prueba, ejecute el siguiente cmdlet en una ventana de PowerShell con privilegios elevados:</span><span class="sxs-lookup"><span data-stu-id="6f5fd-317">So, for every virtual machine you use in the test, run the following cmdlet in an elevated PowerShell window:</span></span>


   ```
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="ping-the-azure-stack-virtual-machine"></a><span data-ttu-id="6f5fd-318">Hacer ping a la máquina virtual de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6f5fd-318">Ping the Azure Stack virtual machine</span></span>

1. <span data-ttu-id="6f5fd-319">Inicie sesión en el portal de usuarios de Azure Stack con una cuenta de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-319">Sign in to the Azure Stack user portal using a tenant account.</span></span>
2. <span data-ttu-id="6f5fd-320">En la barra de navegación de la izquierda, haga clic en **Máquinas virtuales**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-320">Click **Virtual Machines** in the left navigation bar.</span></span>
3. <span data-ttu-id="6f5fd-321">Busque la máquina virtual que creó anteriormente y haga clic en ella.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-321">Find the virtual machine that you previously created and click it.</span></span>
4. <span data-ttu-id="6f5fd-322">En la sección de la máquina virtual, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-322">On the section for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="6f5fd-323">Abra una ventana de PowerShell con privilegios elevados y escriba **ipconfig/all**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-323">Open an elevated PowerShell window, and type **ipconfig /all**.</span></span>
6. <span data-ttu-id="6f5fd-324">Encuentre la dirección IPv4 en la salida y anótela.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-324">Find the IPv4 Address in the output and note it.</span></span> <span data-ttu-id="6f5fd-325">Haga ping a esta dirección desde la máquina virtual en la VNet de Azure.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-325">Ping this address from the virtual machine in the Azure VNet.</span></span> <span data-ttu-id="6f5fd-326">En el entorno de ejemplo, la dirección proviene de la subred 10.1.1.x/24.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-326">In the example environment, the address is from the 10.1.1.x/24 subnet.</span></span> <span data-ttu-id="6f5fd-327">En su entorno, la dirección puede variar.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-327">In your environment, the address might be different.</span></span> <span data-ttu-id="6f5fd-328">Sin embargo, debe estar dentro de la subred que creó para la subred de VNet de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-328">However, it should be within the subnet you created for the Tenant VNet subnet.</span></span>


### <a name="view-data-transfer-statistics"></a><span data-ttu-id="6f5fd-329">Visualización de estadísticas de transferencia de datos</span><span class="sxs-lookup"><span data-stu-id="6f5fd-329">View data transfer statistics</span></span>

<span data-ttu-id="6f5fd-330">Si desea saber la cantidad de tráfico que está pasando por la conexión, puede encontrar esta información en la sección Conexión en el portal de usuario de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-330">If you want to know how much traffic is passing through your connection, you can find this information on the Connection section in the Azure Stack user portal.</span></span> <span data-ttu-id="6f5fd-331">Esta información también es otra buena forma de comprobar que el ping que acaba de enviar haya pasado por las conexiones VPN y ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-331">This information is also another good way to verify that the ping you just sent actually went through the VPN and ExpressRoute connections.</span></span>

1. <span data-ttu-id="6f5fd-332">Inicie sesión en el portal de usuarios de Microsoft Azure Stack con la cuenta de inquilino.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-332">Sign in to the Microsoft Azure Stack user portal using your tenant account.</span></span>
2. <span data-ttu-id="6f5fd-333">Vaya al grupo de recursos donde se creó la puerta de enlace de VPN y seleccione el tipo de objeto **Conexiones**.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-333">Navigate to the resource group where your VPN Gateway was created and select the **Connections** object type.</span></span>
3. <span data-ttu-id="6f5fd-334">Haga clic en la conexión **ConnectToAzure** en la lista.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-334">Click the **ConnectToAzure** connection in the list.</span></span>
4. <span data-ttu-id="6f5fd-335">En la sección **Conexión**, puede ver las estadísticas de **Datos de entrada** y **Datos de salida**. Debería ver algunos valores distintos de cero.</span><span class="sxs-lookup"><span data-stu-id="6f5fd-335">On the **Connection** section, you can see statistics for **Data in** and **Data out**. You should see some non-zero values there.</span></span>

   ![Datos de entrada y salida](media/azure-stack-connect-expressroute/DataInDataOut.png)

## <a name="next-steps"></a><span data-ttu-id="6f5fd-337">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6f5fd-337">Next steps</span></span>
[<span data-ttu-id="6f5fd-338">Implementar aplicaciones en Azure y Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6f5fd-338">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)