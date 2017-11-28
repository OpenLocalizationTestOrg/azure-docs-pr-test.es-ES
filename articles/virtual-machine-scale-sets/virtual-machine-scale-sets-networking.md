---
title: "aaaNetworking para conjuntos de escalas de máquina virtual de Azure | Documentos de Microsoft"
description: "Propiedades de configuración de red para el conjunto de escalado de máquinas virtuales de Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="ecf26-103">Redes para conjuntos de escalado de máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="ecf26-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="ecf26-104">Cuando se implementación un conjunto a través del portal de Hola de escalas de máquina virtual de Azure, algunas propiedades de red se establecen de forma predeterminadas, por ejemplo un equilibrador de carga de Azure con las reglas NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="ecf26-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="ecf26-105">Este artículo describe cómo se establece toouse algunos hello más funciones avanzadas de red que se pueden configurar con una escala.</span><span class="sxs-lookup"><span data-stu-id="ecf26-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="ecf26-106">Puede configurar todas las características de hello tratadas en este artículo usando plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="ecf26-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="ecf26-107">También se incluyen ejemplos de la CLI de Azure y PowerShell para las características seleccionadas.</span><span class="sxs-lookup"><span data-stu-id="ecf26-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="ecf26-108">Use CLI 2.10 y PowerShell 4.2.0 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="ecf26-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="ecf26-109">Redes aceleradas</span><span class="sxs-lookup"><span data-stu-id="ecf26-109">Accelerated Networking</span></span>
<span data-ttu-id="ecf26-110">Azure [Accelerated redes](../virtual-network/virtual-network-create-vm-accelerated-networking.md) mejora el rendimiento de la red habilitando la máquina virtual de E/S de raíz única (SR-IOV) de virtualización tooa.</span><span class="sxs-lookup"><span data-stu-id="ecf26-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="ecf26-111">toouse accelerated redes con conjuntos de escalas, establezca enableAcceleratedNetworking demasiado**true** en la configuración de networkInterfaceConfigurations de su conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="ecf26-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="ecf26-112">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="ecf26-113">Creación de un conjunto de escalado que hace referencia a una instancia de Azure Load Balancer existente</span><span class="sxs-lookup"><span data-stu-id="ecf26-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="ecf26-114">Cuando se crea un conjunto de escala con hello portal de Azure, se crea un nuevo equilibrador de carga para la mayoría de opciones de configuración.</span><span class="sxs-lookup"><span data-stu-id="ecf26-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="ecf26-115">Si crea un conjunto de escala, que debe tooreference un equilibrador de carga existente, puede hacerlo mediante la CLI.</span><span class="sxs-lookup"><span data-stu-id="ecf26-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="ecf26-116">Hola siguiente secuencia de comandos de ejemplo crea un equilibrador de carga y, a continuación, crea un conjunto de escala, que hace referencia a él:</span><span class="sxs-lookup"><span data-stu-id="ecf26-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="ecf26-117">Valores de DNS configurables</span><span class="sxs-lookup"><span data-stu-id="ecf26-117">Configurable DNS Settings</span></span>
<span data-ttu-id="ecf26-118">Conjuntos de escalas de adopta de forma predeterminada, en configuración de DNS específico de Hola de hello red virtual y subred que se crearon.</span><span class="sxs-lookup"><span data-stu-id="ecf26-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="ecf26-119">Obstante, puede configurar el DNS de Hola para una escala establecer directamente.</span><span class="sxs-lookup"><span data-stu-id="ecf26-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="ecf26-120">Creación de un conjunto de escalado con servidores DNS configurables</span><span class="sxs-lookup"><span data-stu-id="ecf26-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="ecf26-121">toocreate una escala configurada con una configuración de DNS personalizada mediante 2.0 de CLI, agregue hello **servidores dns--** argumento toohello **vmss crear** separados de comando, seguido por el espacio de direcciones ip del servidor.</span><span class="sxs-lookup"><span data-stu-id="ecf26-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="ecf26-122">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="ecf26-123">tooconfigure los servidores DNS personalizados en una plantilla de Azure, agregue una escala de toohello de propiedad de clase dnsSettings la sección networkInterfaceConfigurations del conjunto.</span><span class="sxs-lookup"><span data-stu-id="ecf26-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="ecf26-124">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="ecf26-125">Creación de un conjunto de escalado con nombres de dominio de máquinas virtuales configurables</span><span class="sxs-lookup"><span data-stu-id="ecf26-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="ecf26-126">toocreate establece una escala con un nombre DNS personalizado para máquinas virtuales mediante la CLI 2.0, agregar hello **--vm nombre de dominio** argumento toohello **vmss crear** comando, seguido de una cadena que representa el nombre de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="ecf26-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="ecf26-127">nombre de dominio de hello tooset en una plantilla de Azure, agregue un **dnsSettings** conjunto de escalas de propiedad toohello **networkInterfaceConfigurations** sección.</span><span class="sxs-lookup"><span data-stu-id="ecf26-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="ecf26-128">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="ecf26-129">salida de Hello, para un nombre de dns de la máquina virtual individual sería Hola siguiente forma:</span><span class="sxs-lookup"><span data-stu-id="ecf26-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="ecf26-130">Dirección IPv4 pública por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ecf26-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="ecf26-131">En general, las máquinas virtuales del conjunto de escalado de Azure no requieren direcciones IP públicas propias.</span><span class="sxs-lookup"><span data-stu-id="ecf26-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="ecf26-132">Para la mayoría de los casos, resulta más económico y segura tooassociate un pública IP dirección tooa carga equilibrador o tooan máquina virtual individual (también conocido como un jumpbox), que, a continuación, enruta entrantes conexiones tooscale conjunto de las máquinas virtuales según sea necesario (por ejemplo, mediante reglas NAT de entrada).</span><span class="sxs-lookup"><span data-stu-id="ecf26-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="ecf26-133">Sin embargo, algunos escenarios requieren conjunto de escalado de máquinas virtuales toohave su propia dirección IP pública direcciones.</span><span class="sxs-lookup"><span data-stu-id="ecf26-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="ecf26-134">Un ejemplo es juegos, donde una consola necesita toomake una conexión directa tooa nube máquina virtual en que está realizando el procesamiento de juego física.</span><span class="sxs-lookup"><span data-stu-id="ecf26-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="ecf26-135">Otro ejemplo es donde máquinas virtuales deben toomake conexiones externas tooone otro a lo largo de las regiones en una base de datos distribuida.</span><span class="sxs-lookup"><span data-stu-id="ecf26-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="ecf26-136">Creación de un conjunto de escalado con una dirección IP pública por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ecf26-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="ecf26-137">toocreate un conjunto de escala que asigna una máquina de virtual pública de tooeach dirección IP 2.0 de CLI, agregue hello **--public-ip por vm** parámetro toohello **vmss crear** comando.</span><span class="sxs-lookup"><span data-stu-id="ecf26-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="ecf26-138">toocreate una escala que se establecen a través de una plantilla de Azure, asegúrese de versión de Hola API de hello Microsoft.Compute/virtualMachineScaleSets recurso es al menos **2017-03-30**y agregue un **publicIpAddressConfiguration**IpConfigurations sección del conjunto de escala de toohello de propiedad JSON.</span><span class="sxs-lookup"><span data-stu-id="ecf26-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="ecf26-139">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="ecf26-140">Ejemplo de plantilla: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="ecf26-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="ecf26-141">Al consultar la dirección IP pública de Hola el conjunto de direcciones de máquinas virtuales de hello en una escala</span><span class="sxs-lookup"><span data-stu-id="ecf26-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="ecf26-142">asignar las direcciones IP públicas de toolist hello tooscale conjunto de máquinas virtuales con CLI 2.0, use hello **vmss az-instancia de lista-IP pública** comando.</span><span class="sxs-lookup"><span data-stu-id="ecf26-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="ecf26-143">conjunto de escalado de toolist de direcciones IP públicas con PowerShell, use hello _Get AzureRmPublicIpAddress_ comando.</span><span class="sxs-lookup"><span data-stu-id="ecf26-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="ecf26-144">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="ecf26-145">También puede direcciones IP públicas de consulta Hola haciendo referencia directamente a los Id. de recurso de Hola de configuración de dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="ecf26-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="ecf26-146">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="ecf26-147">asignar las direcciones IP públicas de tooquery hello tooscale conjunto de máquinas virtuales con hello [Explorador de recursos de Azure](https://resources.azure.com), u Hola API de REST de Azure con la versión **2017-03-30** o superior.</span><span class="sxs-lookup"><span data-stu-id="ecf26-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="ecf26-148">tooview de direcciones IP públicas para una escala que se establecen a través de hello Explorador de recursos, mire hello **las publicipaddresses a las** sección en su conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="ecf26-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="ecf26-149">Por ejemplo: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="ecf26-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="ecf26-150">Salida de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="ecf26-151">Varias direcciones IP por NIC</span><span class="sxs-lookup"><span data-stu-id="ecf26-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="ecf26-152">Cada NIC conectada tooa que máquina virtual en un conjunto de escala puede tener una o varias configuraciones de IP asociadas con él.</span><span class="sxs-lookup"><span data-stu-id="ecf26-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="ecf26-153">Se asigna a cada configuración una dirección IP privada.</span><span class="sxs-lookup"><span data-stu-id="ecf26-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="ecf26-154">Cada configuración también puede tener un recurso de dirección IP pública asociado con ella.</span><span class="sxs-lookup"><span data-stu-id="ecf26-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="ecf26-155">toounderstand cuántas direcciones IP pueden asignarse tooa NIC, y cuántas direcciones IP públicas que puede usar en una suscripción de Azure, consulte demasiado[el límite de Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="ecf26-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="ecf26-156">Varias NIC por máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ecf26-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="ecf26-157">Puede tener hasta too8 NIC por máquina virtual, según el tamaño de la máquina.</span><span class="sxs-lookup"><span data-stu-id="ecf26-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="ecf26-158">número máximo de Hola de NIC por máquina está disponible en hello [artículo de tamaño de máquina virtual](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="ecf26-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="ecf26-159">Hello en el ejemplo siguiente se es que una escala de conjunto de perfil de red que muestra varias entradas NIC y varias direcciones IP públicas por máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="ecf26-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="ecf26-160">NSG por conjunto de escalado</span><span class="sxs-lookup"><span data-stu-id="ecf26-160">NSG per scale set</span></span>
<span data-ttu-id="ecf26-161">Grupos de seguridad de red se pueden aplicar directamente tooa escala, mediante la adición de una sección de configuración de interfaz de referencia toohello red de escala de hello establece propiedades de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ecf26-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="ecf26-162">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ecf26-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="ecf26-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ecf26-163">Next steps</span></span>
<span data-ttu-id="ecf26-164">Para obtener más información sobre redes virtuales de Azure, consulte demasiado[esta documentación](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecf26-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
