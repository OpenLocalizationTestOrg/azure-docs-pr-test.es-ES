---
title: "aaaMultiple las direcciones IP para máquinas virtuales de Azure - PowerShell | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooassign varias direcciones IP de máquina virtual de tooa mediante PowerShell | Administrador de recursos."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="a88f7-103">Asignar varias direcciones IP máquinas toovirtual con PowerShell</span><span class="sxs-lookup"><span data-stu-id="a88f7-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="a88f7-104">Este artículo explica cómo toocreate una máquina virtual (VM) a través de la implementación de Azure Resource Manager Hola modelar con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a88f7-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="a88f7-105">No se puede asignar tooresources que se creó mediante el modelo de implementación clásica de Hola a varias direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="a88f7-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="a88f7-106">más información acerca de los modelos de implementación de Azure, lea hello toolearn [comprender los modelos de implementación](../resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="a88f7-107"><a name = "create"></a>Creación de una máquina virtual con varias direcciones IP</span><span class="sxs-lookup"><span data-stu-id="a88f7-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="a88f7-108">pasos de Hola que siguen explican cómo toocreate aborda un máquina virtual con varias IP de ejemplo, tal y como se describe en el escenario de Hola.</span><span class="sxs-lookup"><span data-stu-id="a88f7-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="a88f7-109">Cambie los valores de variable según sea necesario para la implementación.</span><span class="sxs-lookup"><span data-stu-id="a88f7-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="a88f7-110">Abra un símbolo del sistema de PowerShell y Hola completa restante pasos de esta sección dentro de una sola sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a88f7-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="a88f7-111">Si aún no tiene PowerShell instalado y configurado, Hola completa los pasos de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a88f7-112">Cuenta de inicio de sesión tooyour con hello `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="a88f7-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="a88f7-113">Reemplace *myResourceGroup* y *westus* por un nombre y una ubicación de su elección.</span><span class="sxs-lookup"><span data-stu-id="a88f7-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="a88f7-114">Cree un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a88f7-114">Create a resource group.</span></span> <span data-ttu-id="a88f7-115">Un grupo de recursos es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a88f7-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="a88f7-116">Crear una red virtual (VNet) y la subred en hello misma ubicación que el grupo de recursos de hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="a88f7-117">Cree un grupo de seguridad de red (NSG) y una regla.</span><span class="sxs-lookup"><span data-stu-id="a88f7-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="a88f7-118">Hola NSG protege Hola VM mediante reglas entrantes y salientes.</span><span class="sxs-lookup"><span data-stu-id="a88f7-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="a88f7-119">En este caso, se crea una regla de entrada para el puerto 3389, que permite las conexiones entrantes al Escritorio remoto.</span><span class="sxs-lookup"><span data-stu-id="a88f7-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="a88f7-120">Definir configuración IP primaria de Hola para hello NIC.</span><span class="sxs-lookup"><span data-stu-id="a88f7-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="a88f7-121">Cambio 10.0.0.4 tooa dirección válida en la subred de Hola que ha creado, si no utiliza valor Hola definido previamente.</span><span class="sxs-lookup"><span data-stu-id="a88f7-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="a88f7-122">Antes de asignar una dirección IP estática, se recomienda que primero confirme que no está en uso.</span><span class="sxs-lookup"><span data-stu-id="a88f7-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="a88f7-123">Escriba el comando hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="a88f7-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="a88f7-124">Si está disponible la dirección de hello, Hola output devuelve *True*.</span><span class="sxs-lookup"><span data-stu-id="a88f7-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="a88f7-125">Si no está disponible, Hola salida devuelve *False* y una lista de direcciones que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="a88f7-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="a88f7-126">Hola, siga los comandos, **reemplace < reemplazar-con-your-único-name > por hello toouse de nombre DNS único.**</span><span class="sxs-lookup"><span data-stu-id="a88f7-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="a88f7-127">nombre de Hello debe ser único en todas las direcciones IP públicas dentro de una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="a88f7-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="a88f7-128">Se trata de un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="a88f7-128">This is an optional parameter.</span></span> <span data-ttu-id="a88f7-129">Se puede quitar si sólo desea tooconnect toohello máquina virtual con la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="a88f7-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="a88f7-130">Cuando asigna varias IP configuraciones tooa NIC, se debe asignar una configuración como hello *-principal*.</span><span class="sxs-lookup"><span data-stu-id="a88f7-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a88f7-131">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="a88f7-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a88f7-132">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="a88f7-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a88f7-133">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="a88f7-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a88f7-134">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="a88f7-135">Definir configuraciones de IP secundarias Hola para hello NIC.</span><span class="sxs-lookup"><span data-stu-id="a88f7-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="a88f7-136">Puede agregar o quitar las configuraciones que sean necesarias.</span><span class="sxs-lookup"><span data-stu-id="a88f7-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="a88f7-137">Cada configuración de dirección IP debe tener asignada una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="a88f7-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="a88f7-138">Cada configuración puede tener asignada opcionalmente una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="a88f7-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="a88f7-139">Crear hello NIC y asociar Hola tres IP configuraciones tooit:</span><span class="sxs-lookup"><span data-stu-id="a88f7-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="a88f7-140">Aunque todas las configuraciones se asignan tooone NIC en este artículo, puede asignar varios tooevery NIC conectada toohello VM configuraciones de IP.</span><span class="sxs-lookup"><span data-stu-id="a88f7-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="a88f7-141">toolearn cómo leer toocreate una máquina virtual con varias NIC hello [crear una máquina virtual con varias NIC](virtual-network-deploy-multinic-arm-ps.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="a88f7-142">Crear Hola VM escribiendo Hola siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="a88f7-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="a88f7-143">Sistema operativo de la VM de toohello las direcciones IP privada de agregar Hola siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="a88f7-144">No agregue el sistema de operativo para toohello el público direcciones IP Hola.</span><span class="sxs-lookup"><span data-stu-id="a88f7-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="a88f7-145"><a name="add"></a>Agregar tooa de direcciones IP virtual</span><span class="sxs-lookup"><span data-stu-id="a88f7-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="a88f7-146">Puede agregar pública y privada tooa de direcciones IP NIC siguiendo los pasos de Hola que siguen.</span><span class="sxs-lookup"><span data-stu-id="a88f7-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="a88f7-147">Hello en los ejemplos de hello las secciones siguientes se suponen que ya tiene una máquina virtual con configuraciones de IP de hello tres descritas en hello [escenario](#Scenario) en este artículo, pero no es necesario que lo haga.</span><span class="sxs-lookup"><span data-stu-id="a88f7-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="a88f7-148">Abra un símbolo del sistema de PowerShell y Hola completa restante pasos de esta sección dentro de una sola sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a88f7-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="a88f7-149">Si aún no tiene PowerShell instalado y configurado, Hola completa los pasos de hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a88f7-150">Cambiar los valores"hello" de hello después $Variables toohello nombre de hello NIC que desee tooadd IP dirección tooand Hola recursos grupo y ubicación Hola en que NIC existe:</span><span class="sxs-lookup"><span data-stu-id="a88f7-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="a88f7-151">Si no conoce el nombre de Hola de hello NIC que desee toochange, escriba Hola siga los comandos, a continuación, cambiar los valores de hello de variables anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="a88f7-152">Cree una variable y establézcalo toohello existente NIC escribiendo el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="a88f7-153">Hola después de comandos, cambiar *MyVNet* y *MySubnet* toohello nombres de Hola Hola de red virtual y subred NIC está conectada a.</span><span class="sxs-lookup"><span data-stu-id="a88f7-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="a88f7-154">Escriba Hola comandos tooretrieve Hola red virtual y subred objetos Hola A que NIC está conectada:</span><span class="sxs-lookup"><span data-stu-id="a88f7-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="a88f7-155">Si no sabe Hola red virtual o la subred nombre Hola A que NIC está conectada, escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a88f7-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="a88f7-156">En la salida de hello, buscar texto toohello similar después de la salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a88f7-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="a88f7-157">En esta salida, *MyVnet* es hello red virtual y *MySubnet* es Hola subred hello NIC está conectada a.</span><span class="sxs-lookup"><span data-stu-id="a88f7-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="a88f7-158">Complete los pasos de hello en una de las siguientes secciones, según sus requisitos de hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="a88f7-159">**Incorporación de una dirección IP privada**</span><span class="sxs-lookup"><span data-stu-id="a88f7-159">**Add a private IP address**</span></span>

    <span data-ttu-id="a88f7-160">tooadd una tooa de dirección IP privada NIC, debe crear una configuración de IP.</span><span class="sxs-lookup"><span data-stu-id="a88f7-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="a88f7-161">Hello siguiente comando crea una configuración con una dirección IP estática de 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="a88f7-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="a88f7-162">Al especificar una dirección IP estática, debe ser una dirección no utilizada para la subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="a88f7-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="a88f7-163">Se recomienda que primero pruebe Hola dirección tooensure está disponible mediante la especificación de hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando.</span><span class="sxs-lookup"><span data-stu-id="a88f7-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="a88f7-164">Si está disponible la dirección IP de hello, Hola output devuelve *True*.</span><span class="sxs-lookup"><span data-stu-id="a88f7-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="a88f7-165">Si no está disponible, Hola salida devuelve *False*y una lista de direcciones que están disponibles.</span><span class="sxs-lookup"><span data-stu-id="a88f7-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="a88f7-166">Cree tantas configuraciones como sea necesario mediante nombres de configuración únicos y direcciones IP privadas (para las configuraciones con direcciones IP estáticas).</span><span class="sxs-lookup"><span data-stu-id="a88f7-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="a88f7-167">Agregar: sistema operativo de la VM de hello privado IP dirección toohello siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="a88f7-168">**Incorporación de una dirección IP pública**</span><span class="sxs-lookup"><span data-stu-id="a88f7-168">**Add a public IP address**</span></span>

    <span data-ttu-id="a88f7-169">Se agrega una dirección IP pública asociando un tooeither de recurso de dirección IP pública de una nueva configuración de IP o una configuración de IP existente.</span><span class="sxs-lookup"><span data-stu-id="a88f7-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="a88f7-170">Complete los pasos de hello en una de las secciones de Hola que siguen, como sea necesario.</span><span class="sxs-lookup"><span data-stu-id="a88f7-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a88f7-171">Las direcciones IP públicas tienen un precio simbólico.</span><span class="sxs-lookup"><span data-stu-id="a88f7-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="a88f7-172">toolearn más información acerca de la IP direcciones sobre los precios, leer hello [precios de dirección IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="a88f7-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="a88f7-173">Hay un toohello limitar el número de direcciones IP públicas que puede usarse en una suscripción.</span><span class="sxs-lookup"><span data-stu-id="a88f7-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="a88f7-174">toolearn más acerca de los límites de hello, leer hello [Azure tiene una limitación](../azure-subscription-service-limits.md#networking-limits) artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="a88f7-175">**Asociar Hola pública recursos tooa nueva IP configuración de dirección IP**</span><span class="sxs-lookup"><span data-stu-id="a88f7-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="a88f7-176">Siempre que agregue una dirección IP pública en una nueva configuración de IP, también debe agregar una dirección IP privada, porque todas las configuraciones de IP deben tener una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="a88f7-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="a88f7-177">Puede agregar un recurso de dirección IP pública existente o crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="a88f7-178">toocreate uno nuevo, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="a88f7-179">toocreate una nueva configuración de IP con una dirección IP privada estática y Hola asociados *myPublicIp3* IP pública recurso Dirección, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="a88f7-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="a88f7-180">**Asociar Hola pública recursos tooan existente IP configuración de dirección IP**</span><span class="sxs-lookup"><span data-stu-id="a88f7-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="a88f7-181">Configuración de IP de tooan asociado que ya no tiene asociado sólo puede ser un recurso de dirección IP público.</span><span class="sxs-lookup"><span data-stu-id="a88f7-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="a88f7-182">Puede determinar si una configuración de IP tiene una dirección IP pública asociada mediante la especificación de hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a88f7-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="a88f7-183">Se ve resultados similares toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="a88f7-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="a88f7-184">Desde hello **PublicIpAddress** columna para *IpConfig-3* está en blanco, ningún recurso de dirección IP pública está asociada actualmente tooit.</span><span class="sxs-lookup"><span data-stu-id="a88f7-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="a88f7-185">Puede agregar una existente pública IP dirección recursos tooIpConfig-3, o escriba Hola después toocreate comando uno:</span><span class="sxs-lookup"><span data-stu-id="a88f7-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="a88f7-186">Escriba el siguiente comando con el nombre por la configuración de IP existente de recursos toohello de dirección IP pública de tooassociate Hola de hello *IpConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="a88f7-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="a88f7-187">Establecer Hola NIC con una nueva configuración de IP Hola escribiendo Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a88f7-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="a88f7-188">Ver direcciones IP privadas de Hola y Hola pública IP dirección recursos asignado toohello NIC escribiendo Hola el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a88f7-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="a88f7-189">Agregar: sistema operativo de la VM de hello privado IP dirección toohello siguiendo los pasos de hello para el sistema operativo en hello [sistema operativo de la VM de tooa las direcciones IP agregar](#os-config) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a88f7-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="a88f7-190">No agregue el sistema de operativo para toohello el público dirección IP Hola.</span><span class="sxs-lookup"><span data-stu-id="a88f7-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
