---
title: aaaTroubleshoot grupos de seguridad de red - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot grupos de seguridad de red en la implementación de Azure Resource Manager Hola modelar con Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="628ab-103">Solución de problemas de los grupos de seguridad de red utilizando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="628ab-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="628ab-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="628ab-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="628ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="628ab-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="628ab-106">Si configura los grupos de seguridad de red (NSG) en la máquina virtual (VM) y están experimentando problemas de conectividad de la máquina virtual, este artículo proporciona información general sobre las capacidades de diagnóstico para los NSG toohelp seguir solucionando el problema.</span><span class="sxs-lookup"><span data-stu-id="628ab-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="628ab-107">Los NSG permiten tipos de hello toocontrol de tráfico que fluyen dentro y fuera de sus máquinas virtuales (VM).</span><span class="sxs-lookup"><span data-stu-id="628ab-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="628ab-108">Los NSG pueden toosubnets aplicados en una red Virtual de Azure (VNet), interfaces de red (NIC) o ambos.</span><span class="sxs-lookup"><span data-stu-id="628ab-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="628ab-109">Hola efectivo reglas que se aplican tooa NIC son una agregación de reglas de Hola que existan en hello NSG aplicadas tooa hello y formación subred está conectado a.</span><span class="sxs-lookup"><span data-stu-id="628ab-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="628ab-110">Las reglas en estos NSG a veces pueden entrar en conflicto entre sí y afectar la conectividad de red de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="628ab-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="628ab-111">Puede ver todas las reglas de seguridad eficaz Hola desde sus NSG, tal como se aplica en NIC de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="628ab-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="628ab-112">Este artículo muestra cómo los problemas de conectividad VM tootroubleshoot utilizando estas reglas en Hola modelo de implementación de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="628ab-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="628ab-113">Si no está familiarizado con conceptos de red virtual y NSG, leer hello [red Virtual](virtual-networks-overview.md) y [grupos de seguridad de red](virtual-networks-nsg.md) artículos de información general.</span><span class="sxs-lookup"><span data-stu-id="628ab-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="628ab-114">Utilizando el flujo de tráfico de las reglas de seguridad efectivo tootroubleshoot VM</span><span class="sxs-lookup"><span data-stu-id="628ab-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="628ab-115">escenario de Hola que sigue es un ejemplo de un problema de conexión comunes:</span><span class="sxs-lookup"><span data-stu-id="628ab-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="628ab-116">Una máquina virtual denominada *VM1* forma parte de una subred *Subnet1* dentro de una red virtual denominada *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="628ab-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="628ab-117">Un toohello de tooconnect de intento de máquinas virtuales mediante RDP a través del puerto TCP 3389 se produce un error.</span><span class="sxs-lookup"><span data-stu-id="628ab-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="628ab-118">Los NSG se aplican en ambos Hola NIC *VM1 NIC1* y Hola subred *subred1*.</span><span class="sxs-lookup"><span data-stu-id="628ab-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="628ab-119">Se permite tráfico tooTCP puerto 3389 en hello NSG asociado a la interfaz de red de hello *VM1 NIC1*; sin embargo, produce un error de tooVM1 puerto 3389 de ping de TCP.</span><span class="sxs-lookup"><span data-stu-id="628ab-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="628ab-120">Aunque este ejemplo utiliza el puerto TCP 3389, Hola lo siguiente puede ser usado toodetermine errores de conexión entrantes y salientes a través de cualquier puerto.</span><span class="sxs-lookup"><span data-stu-id="628ab-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="628ab-121">Pasos de la solución de problemas detallada</span><span class="sxs-lookup"><span data-stu-id="628ab-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="628ab-122">Completar Hola siguiendo los pasos tootroubleshoot NSG para una máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="628ab-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="628ab-123">Inicie un tooAzure de sesión y de inicio de sesión de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="628ab-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="628ab-124">Si no está familiarizado con el uso de PowerShell de Azure, lea hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="628ab-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="628ab-125">Escriba Hola siguiente comando tooreturn tooa NIC con el nombre de aplicar todas las reglas NSG *VM1 NIC1* en grupo de recursos de hello *RG1*:</span><span class="sxs-lookup"><span data-stu-id="628ab-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="628ab-126">Si no conoce el nombre de Hola de una NIC, escriba Hola siguiendo los nombres de comando tooretrieve Hola de todas las NIC en un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="628ab-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="628ab-127">Hello texto siguiente es un ejemplo de Hola reglas efectivo salida que se devuelve para hello *VM1 NIC1* NIC:</span><span class="sxs-lookup"><span data-stu-id="628ab-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="628ab-128">Tenga en cuenta Hola siguiendo la información de salida de hello:</span><span class="sxs-lookup"><span data-stu-id="628ab-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="628ab-129">Hay dos secciones **NetworkSecurityGroup**: una está asociada a una subred (*Subnet1*) y otra está asociada a una NIC (*VM1- NIC1*).</span><span class="sxs-lookup"><span data-stu-id="628ab-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="628ab-130">En este ejemplo, un NSG ha sido tooeach aplicada.</span><span class="sxs-lookup"><span data-stu-id="628ab-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="628ab-131">**Asociación** se muestran los recursos de hello (subred o NIC) está asociado a un NSG determinado.</span><span class="sxs-lookup"><span data-stu-id="628ab-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="628ab-132">Si Hola recursos NSG es mover o eliminar la asociación inmediatamente antes de ejecutar este comando, puede necesitar toowait unos segundos para hello tooreflect de cambio en la salida del comando Hola.</span><span class="sxs-lookup"><span data-stu-id="628ab-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="628ab-133">Hola nombres de las reglas que se prologa con *defaultSecurityRules*: se crea cuando un NSG, varias reglas de seguridad de forma predeterminada se crean dentro de él.</span><span class="sxs-lookup"><span data-stu-id="628ab-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="628ab-134">Las reglas predeterminadas no se pueden quitar, pero pueden reemplazarse con reglas de prioridad más alta.</span><span class="sxs-lookup"><span data-stu-id="628ab-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="628ab-135">Hola de lectura [información general NSG](virtual-networks-nsg.md#default-rules) toolearn artículo más información acerca de NSG predeterminado de las reglas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="628ab-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="628ab-136">**ExpandedAddressPrefix** se expande prefijos de direcciones de Hola para las etiquetas predeterminadas NSG.</span><span class="sxs-lookup"><span data-stu-id="628ab-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="628ab-137">Las etiquetas representan varios prefijos de direcciones.</span><span class="sxs-lookup"><span data-stu-id="628ab-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="628ab-138">Expansión de etiquetas de hello puede ser útil al solucionar problemas de conectividad de la máquina virtual de prefijos de dirección específica.</span><span class="sxs-lookup"><span data-stu-id="628ab-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="628ab-139">Por ejemplo, con el intercambio de tráfico de red virtual, etiqueta VIRTUAL_NETWORK expande tooshow emparejar los prefijos de red virtual en la salida anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="628ab-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="628ab-140">Hola comando solo muestran efectivo reglas si un NSG está asociado a una subred, una NIC o ambos.</span><span class="sxs-lookup"><span data-stu-id="628ab-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="628ab-141">Una máquina virtual puede tener varias NIC con diferentes NSG aplicados.</span><span class="sxs-lookup"><span data-stu-id="628ab-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="628ab-142">Para solucionar el problema, ejecute el comando de Hola para cada NIC.</span><span class="sxs-lookup"><span data-stu-id="628ab-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="628ab-143">tooease filtrado a través de un número mayor de reglas NSG, escriba Hola después más tootroubleshoot de comandos:</span><span class="sxs-lookup"><span data-stu-id="628ab-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="628ab-144">Un filtro para el tráfico RDP (puerto TCP 3389) es aplicar toohello vista de cuadrícula, como se muestra en hello después de imagen:</span><span class="sxs-lookup"><span data-stu-id="628ab-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Lista de reglas](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="628ab-146">Como puede ver en la vista de cuadrícula de hello, hay dos permiten y denegación las reglas para RDP.</span><span class="sxs-lookup"><span data-stu-id="628ab-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="628ab-147">resultado del paso 2 Hello muestra ese hello *DenyRDP* regla se encuentra en hello NSG aplica toohello subred.</span><span class="sxs-lookup"><span data-stu-id="628ab-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="628ab-148">Para las reglas de entrada, los NSG aplicados toohello subred se procesa en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="628ab-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="628ab-149">Si se encuentra una coincidencia, no se procesa la interfaz de red de hello NSG aplica toohello.</span><span class="sxs-lookup"><span data-stu-id="628ab-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="628ab-150">En este caso, Hola *DenyRDP* regla de subred de hello bloquea RDP toohello VM (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="628ab-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="628ab-151">Una máquina virtual puede tener varios tooit adjunto de NIC.</span><span class="sxs-lookup"><span data-stu-id="628ab-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="628ab-152">Cada uno de ellos puede ser tooa conectado otra subred.</span><span class="sxs-lookup"><span data-stu-id="628ab-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="628ab-153">Puesto que los comandos de hello en los pasos anteriores de Hola se ejecutan en una NIC, es importante tooensure que especifique Hola NIC tiene error de conectividad de Hola a.</span><span class="sxs-lookup"><span data-stu-id="628ab-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="628ab-154">Si no está seguro, siempre puede ejecutar comandos de hello en cada máquina virtual de toohello NIC conectada.</span><span class="sxs-lookup"><span data-stu-id="628ab-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="628ab-155">tooRDP en VM1, cambio hello *denegar RDP (3389)* regla demasiado*permitir RDP(3389)* en hello **NSG subred1** NSG.</span><span class="sxs-lookup"><span data-stu-id="628ab-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="628ab-156">Confirme que el puerto TCP 3389 está abierto abriendo una toohello de conexión RDP VM o utilizando la herramienta de PsPing Hola.</span><span class="sxs-lookup"><span data-stu-id="628ab-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="628ab-157">Se puede obtener más información acerca de PsPing por leer hello [página de descarga de PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="628ab-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="628ab-158">Puede o quitar reglas de un NSG con información de hello en la salida de hello de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="628ab-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="628ab-159">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="628ab-159">Considerations</span></span>
<span data-ttu-id="628ab-160">Considere la posibilidad de hello siguientes puntos al solucionar problemas de conectividad:</span><span class="sxs-lookup"><span data-stu-id="628ab-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="628ab-161">Reglas NSG predeterminadas bloqueará el acceso entrante de hello tráfico entrante de internet y sólo permitir red virtual.</span><span class="sxs-lookup"><span data-stu-id="628ab-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="628ab-162">Las reglas deben agregarse explícitamente tooallow acceso de entrada desde Internet, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="628ab-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="628ab-163">Si no hay ninguna regla de seguridad NSG causa toofail de conectividad de red de la máquina virtual, el problema de hello causa puede ser:</span><span class="sxs-lookup"><span data-stu-id="628ab-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="628ab-164">Software de firewall que se ejecuta en el sistema operativo de la máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="628ab-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="628ab-165">Rutas configuradas para dispositivos virtuales o para el tráfico local.</span><span class="sxs-lookup"><span data-stu-id="628ab-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="628ab-166">Tráfico de Internet puede ser redirigido tooon local a través de tunelización forzada.</span><span class="sxs-lookup"><span data-stu-id="628ab-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="628ab-167">Una conexión RDP/SSH de hello Internet tooyour VM no funcionen con esta configuración, dependiendo de cómo administra el hardware de red local de hello este tráfico.</span><span class="sxs-lookup"><span data-stu-id="628ab-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="628ab-168">Hola de lectura [solución de problemas de rutas](virtual-network-routes-troubleshoot-powershell.md) artículo toolearn cómo toodiagnose dirigir los problemas que pueden ser y se impide Hola flujo de tráfico dentro y fuera de Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="628ab-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="628ab-169">Si ha emparejar las redes virtuales, de forma predeterminada, Hola etiqueta VIRTUAL_NETWORK expandirá automáticamente tooinclude prefijos para emparejar redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="628ab-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="628ab-170">Puede ver estos prefijos en hello **ExpandedAddressPrefix** enumerar, tootroubleshoot cualquier tooVNet relacionados problemas emparejamiento conectividad.</span><span class="sxs-lookup"><span data-stu-id="628ab-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="628ab-171">Las reglas de seguridad eficaz solo se muestran si hay que un NSG asociada a la máquina virtual de hello NIC y o subred.</span><span class="sxs-lookup"><span data-stu-id="628ab-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="628ab-172">Si no hay ningún NSG asociados con hello NIC o subred y tiene una dirección IP pública asignada tooyour VM, todos los puertos se abrirán para el acceso entrante y saliente.</span><span class="sxs-lookup"><span data-stu-id="628ab-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="628ab-173">Si Hola máquina virtual tiene una dirección IP pública, aplicar los NSG toohello NIC o la subred se recomienda.</span><span class="sxs-lookup"><span data-stu-id="628ab-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

