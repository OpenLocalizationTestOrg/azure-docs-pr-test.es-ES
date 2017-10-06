---
title: patrones de aaaNetworking para Azure Service Fabric | Documentos de Microsoft
description: "Describe los patrones comunes de redes de Service Fabric y cómo toocreate un clúster mediante el uso de características de red de Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="1c095-103">Patrones de redes de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1c095-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="1c095-104">Puede integrar el clúster de Azure Service Fabric con otras características de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c095-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="1c095-105">En este artículo, le mostraremos cómo toocreate clústeres ese Hola de uso siguientes características:</span><span class="sxs-lookup"><span data-stu-id="1c095-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="1c095-106">Subred y red virtual existentes</span><span class="sxs-lookup"><span data-stu-id="1c095-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="1c095-107">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="1c095-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="1c095-108">Equilibrador de carga solo interno</span><span class="sxs-lookup"><span data-stu-id="1c095-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="1c095-109">Equilibrador de carga interno y externo</span><span class="sxs-lookup"><span data-stu-id="1c095-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="1c095-110">Service Fabric se ejecuta en un conjunto de escalado de máquinas virtuales estándar.</span><span class="sxs-lookup"><span data-stu-id="1c095-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="1c095-111">Cualquier funcionalidad que pueda usar en un conjunto de escalado de máquinas virtuales, puede usarse con un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1c095-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="1c095-112">Hola red secciones de plantillas de Azure Resource Manager Hola para conjuntos de escalas de máquina virtual y el tejido de servicio son idénticas.</span><span class="sxs-lookup"><span data-stu-id="1c095-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="1c095-113">Después de implementar tooan existente de la red virtual, es fácil tooincorporate otra características, como ExpressRoute de Azure, la puerta de enlace de VPN de Azure, un grupo de seguridad de red e intercambio de tráfico de red virtual de red.</span><span class="sxs-lookup"><span data-stu-id="1c095-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="1c095-114">Service Fabric es único en relación con otras características de red en un aspecto.</span><span class="sxs-lookup"><span data-stu-id="1c095-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="1c095-115">Hola [portal de Azure](https://portal.azure.com) internamente utiliza Hola Service Fabric proveedor toocall tooa clúster tooget información sobre recursos nodos y aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1c095-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="1c095-116">proveedor de recursos de Service Fabric Hola requiere acceso de entrada es accesible públicamente toohello HTTP puerta de enlace (puerto 19080, de forma predeterminada) en el extremo de administración de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="1c095-117">[Explorador de Service Fabric](service-fabric-visualizing-your-cluster.md) usa Hola toomanage de punto de conexión de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="1c095-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="1c095-118">proveedor de recursos de Service Fabric Hello también usa esta información de tooquery de puerto relativa al clúster, toodisplay Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="1c095-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="1c095-119">Si el puerto 19080 no es accesible desde el proveedor de recursos de Service Fabric hello, al igual que un mensaje *nodos no se encontró* aparece en el portal de hello, y la lista de nodo y la aplicación aparece vacía.</span><span class="sxs-lookup"><span data-stu-id="1c095-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="1c095-120">Si desea toosee el clúster en hello portal de Azure, el equilibrador de carga debe exponer una dirección IP pública y el grupo de seguridad de red debe permitir el tráfico de puerto 19080 entrante.</span><span class="sxs-lookup"><span data-stu-id="1c095-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="1c095-121">Si el programa de instalación no cumple estos requisitos, Hola portal de Azure no mostrar estado de hello del clúster.</span><span class="sxs-lookup"><span data-stu-id="1c095-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="1c095-122">Plantillas</span><span class="sxs-lookup"><span data-stu-id="1c095-122">Templates</span></span>

<span data-ttu-id="1c095-123">Todas las plantillas de Service Fabric están en [un archivo de descarga](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="1c095-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="1c095-124">Debe ser capaz de toodeploy plantillas de hello como-consiste en usar Hola siga los comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1c095-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="1c095-125">Si va a implementar Hola plantilla de red Virtual de Azure existente u Hola plantilla de IP pública estática, lea primero hello [Initial setup](#initialsetup) sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="1c095-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="1c095-126">Configuración inicial</span><span class="sxs-lookup"><span data-stu-id="1c095-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="1c095-127">Red virtual existente</span><span class="sxs-lookup"><span data-stu-id="1c095-127">Existing virtual network</span></span>

<span data-ttu-id="1c095-128">En el siguiente ejemplo de Hola, empezaremos con una red virtual existente con el nombre de red virtual ExistingRG, Hola **ExistingRG** grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1c095-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="1c095-129">subred de Hola se denomina de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="1c095-129">hello subnet is named default.</span></span> <span data-ttu-id="1c095-130">Estos recursos de forma predeterminada se crean cuando se usa hello toocreate portal Azure una máquina virtual estándar (VM).</span><span class="sxs-lookup"><span data-stu-id="1c095-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="1c095-131">Puede crear red virtual de Hola y subred sin necesidad de crear Hola VM, pero objetivo principal de Hola de agregar una red virtual de clúster tooan existente es tooother de conectividad de red de tooprovide las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1c095-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="1c095-132">Hola crear VM proporciona un buen ejemplo de cómo una red virtual existente por lo general se usa la.</span><span class="sxs-lookup"><span data-stu-id="1c095-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="1c095-133">Si su clúster de Service Fabric usa solo un equilibrador de carga interno, sin una dirección IP pública, puede usar Hola VM y su dirección IP pública como una ubicación segura *saltar cuadro*.</span><span class="sxs-lookup"><span data-stu-id="1c095-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="1c095-134">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="1c095-134">Static public IP address</span></span>

<span data-ttu-id="1c095-135">Por lo general, una dirección IP pública estática es un recurso dedicado que se administra independientemente del Hola VM o máquinas virtuales que se asigna a.</span><span class="sxs-lookup"><span data-stu-id="1c095-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="1c095-136">Se aprovisiona en un grupo de recursos de red dedicado (como tooin opuestos Hola Service Fabric grupo de recursos de sí misma).</span><span class="sxs-lookup"><span data-stu-id="1c095-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="1c095-137">Crear una dirección IP pública estática denominada staticIP1 Hola mismo grupo de recursos de ExistingRG, Hola portal de Azure o mediante el uso de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1c095-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="1c095-138">Plantilla de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1c095-138">Service Fabric template</span></span>

<span data-ttu-id="1c095-139">En los ejemplos de hello en este artículo, usamos Hola Service Fabric template.json.</span><span class="sxs-lookup"><span data-stu-id="1c095-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="1c095-140">Puede utilizar la plantilla de Hola de toodownload de asistente estándar del portal de Hola desde el portal de hello antes de crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="1c095-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="1c095-141">También puede utilizar una de las plantillas de Hola Hola [Galería de plantillas de](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), como hello [clúster de cinco nodos Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="1c095-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="1c095-142">Subred y red virtual existentes</span><span class="sxs-lookup"><span data-stu-id="1c095-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="1c095-143">Cambiar nombre de toohello del parámetro hello subred de red existente de hello y, a continuación, agregue dos nuevos parámetros tooreference Hola red virtual existente:</span><span class="sxs-lookup"><span data-stu-id="1c095-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="1c095-144">Hola de cambio `vnetID` variable toopoint toohello red virtual:</span><span class="sxs-lookup"><span data-stu-id="1c095-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="1c095-145">Quite `Microsoft.Network/virtualNetworks` de los recursos, para que Azure no cree una nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="1c095-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="1c095-146">Comenta la red virtual de Hola de hello `dependsOn` atributo de `Microsoft.Compute/virtualMachineScaleSets`, por lo que no depende de crear una nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="1c095-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="1c095-147">Implementar la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="1c095-148">Después de la implementación, debe incluir la red virtual nueva escala de hello establece las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="1c095-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="1c095-149">tipo de nodo de conjunto de escala de máquina virtual de Hello debe mostrar subred y red virtual existente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="1c095-150">También puede usar protocolo de escritorio remoto (RDP) tooaccess Hola VM que se encontraba en la red virtual de Hola y conjunto de tooping Hola nueva escala de máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="1c095-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="1c095-151">Para obtener otro ejemplo, vea [uno que no sea específico tooService tejido](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="1c095-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="1c095-152">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="1c095-152">Static public IP address</span></span>

1. <span data-ttu-id="1c095-153">Agregar parámetros para el nombre de Hola de hello existente de grupo de recursos IP estática, el nombre y el nombre de dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="1c095-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="1c095-154">Quitar hello `dnsName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="1c095-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="1c095-155">(dirección IP estática de hello ya tiene uno).</span><span class="sxs-lookup"><span data-stu-id="1c095-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="1c095-156">Agregue una variable tooreference Hola dirección IP estática existente:</span><span class="sxs-lookup"><span data-stu-id="1c095-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="1c095-157">Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="1c095-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="1c095-158">Comenta la dirección IP de Hola de hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, por lo que no depende de crear una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="1c095-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="1c095-159">Hola `Microsoft.Network/loadBalancers` recurso, cambio hello `publicIPAddress` elemento de `frontendIPConfigurations` tooreference Hola existente dirección IP estática en lugar de uno recién creada:</span><span class="sxs-lookup"><span data-stu-id="1c095-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="1c095-160">Hola `Microsoft.ServiceFabric/clusters` recurso, cambio `managementEndpoint` toohello FQDN de DNS de la dirección IP estática de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="1c095-161">Si está usando un clúster seguro, asegúrese de cambiar *http://* demasiado*https://*.</span><span class="sxs-lookup"><span data-stu-id="1c095-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="1c095-162">(Tenga en cuenta que este paso se aplica solo los clústeres de tejido de tooService.</span><span class="sxs-lookup"><span data-stu-id="1c095-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="1c095-163">Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).</span><span class="sxs-lookup"><span data-stu-id="1c095-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="1c095-164">Implementar la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="1c095-165">Después de la implementación, puede ver que el equilibrador de carga es la dirección IP estática pública del toohello enlazado de hello otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1c095-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="1c095-166">Hola de extremo de conexión de cliente de Service Fabric y [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello de punto de punto de conexión de dirección IP estática de hello las DNS FQDN.</span><span class="sxs-lookup"><span data-stu-id="1c095-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="1c095-167">Equilibrador de carga solo interno</span><span class="sxs-lookup"><span data-stu-id="1c095-167">Internal-only load balancer</span></span>

<span data-ttu-id="1c095-168">Este escenario reemplaza el equilibrador de carga externo de hello en plantilla de Service Fabric Hola predeterminada con un equilibrador de carga solo para uso interno.</span><span class="sxs-lookup"><span data-stu-id="1c095-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="1c095-169">Para implicaciones de hello portal de Azure y de proveedor de recursos de Service Fabric hello, vea Hola sección anterior.</span><span class="sxs-lookup"><span data-stu-id="1c095-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="1c095-170">Quitar hello `dnsName` parámetro.</span><span class="sxs-lookup"><span data-stu-id="1c095-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="1c095-171">(No es necesario).</span><span class="sxs-lookup"><span data-stu-id="1c095-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="1c095-172">Si lo desea, puede agregar un parámetro de dirección IP estática, si usa el método de asignación estático.</span><span class="sxs-lookup"><span data-stu-id="1c095-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="1c095-173">Si usa un método de asignación dinámica, no es necesario toodo este paso.</span><span class="sxs-lookup"><span data-stu-id="1c095-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="1c095-174">Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="1c095-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="1c095-175">Quite la dirección IP de hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, por lo que no depende de crear una nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="1c095-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="1c095-176">Agregar la red virtual de hello `dependsOn` atributo porque equilibrador de carga de hello ahora depende de subred de Hola de red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="1c095-177">Cambiar del equilibrador de carga de hello `frontendIPConfigurations` configuración del uso de un `publicIPAddress`, toousing una subred y `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="1c095-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="1c095-178">`privateIPAddress` usa una dirección IP interna estática predefinida.</span><span class="sxs-lookup"><span data-stu-id="1c095-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="1c095-179">toouse una dirección IP dinámica, quitar hello `privateIPAddress` elemento y, a continuación, cambie `privateIPAllocationMethod` demasiado**dinámica**.</span><span class="sxs-lookup"><span data-stu-id="1c095-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="1c095-180">Hola `Microsoft.ServiceFabric/clusters` recurso, cambio `managementEndpoint` dirección de equilibrador de carga interno de toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="1c095-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="1c095-181">Si utiliza un clúster segura, asegúrese de cambiar *http://* demasiado*https://*.</span><span class="sxs-lookup"><span data-stu-id="1c095-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="1c095-182">(Tenga en cuenta que este paso se aplica solo los clústeres de tejido de tooService.</span><span class="sxs-lookup"><span data-stu-id="1c095-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="1c095-183">Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).</span><span class="sxs-lookup"><span data-stu-id="1c095-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="1c095-184">Implementar la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="1c095-185">Después de la implementación, el equilibrador de carga utiliza la dirección IP de hello 10.0.0.250 estático privado.</span><span class="sxs-lookup"><span data-stu-id="1c095-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="1c095-186">Si tiene otro equipo en esa misma red virtual, puede ir toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="1c095-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="1c095-187">Tenga en cuenta que se conecta tooone de nodos de hello detrás de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="1c095-188">Equilibrador de carga interno y externo</span><span class="sxs-lookup"><span data-stu-id="1c095-188">Internal and external load balancer</span></span>

<span data-ttu-id="1c095-189">En este escenario, comience con el equilibrador de carga externo de tipo de nodo único existente de Hola y agregar un equilibrador de carga interno para hello mismo tipo de nodo.</span><span class="sxs-lookup"><span data-stu-id="1c095-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="1c095-190">Puede asignarse a un grupo de direcciones de back-end de tooa de puerto de back-end que se adjunta solo tooa equilibrador de carga única.</span><span class="sxs-lookup"><span data-stu-id="1c095-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="1c095-191">Elija qué equilibrador de carga tendrá los puertos de la aplicación y cuál tendrá los puntos de conexión de administración (puertos 19000 y 19080).</span><span class="sxs-lookup"><span data-stu-id="1c095-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="1c095-192">Si coloca los puntos de conexión de administración de hello en el equilibrador de carga interno de Hola, tenga en hello cuenta recursos de Service Fabric restricciones de proveedor descritas anteriormente en el artículo de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="1c095-193">En el ejemplo de Hola que usamos, extremos de administración de hello permanecen en equilibrador de carga externo Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="1c095-194">También agregue un puerto de aplicación 80 y colocarlo en el equilibrador de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="1c095-195">En un clúster de dos tipo de nodo, un tipo de nodo está en el equilibrador de carga externo Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="1c095-196">Hello otro tipo de nodo está en el equilibrador de carga interno de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="1c095-197">toouse un clúster de dos tipo de nodo, en hello portal plantilla creada por el tipo de nodo de dos (que viene con dos de los equilibradores de carga), cambie el equilibrador de carga interno para tooan el segundo equilibrador de carga Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="1c095-198">Para obtener más información, vea hello [equilibrador de carga interno solo](#internallb) sección.</span><span class="sxs-lookup"><span data-stu-id="1c095-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="1c095-199">Agregue el parámetro de dirección IP de equilibrador de carga interno estático de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="1c095-200">(Para notas relacionada toousing una dirección IP dinámica, consulte las secciones anteriores de este artículo).</span><span class="sxs-lookup"><span data-stu-id="1c095-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="1c095-201">Agregue un parámetro de puerto 80 de aplicación.</span><span class="sxs-lookup"><span data-stu-id="1c095-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="1c095-202">tooadd versiones interno de hello las redes variables, copie y pegue ellos y agregue "-Int" toohello nombre:</span><span class="sxs-lookup"><span data-stu-id="1c095-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="1c095-203">Si empieza con plantilla generados por el portal de Hola que usa el puerto 80 de aplicación, plantilla del portal de Hola predeterminado agrega AppPort1 (puerto 80) en el equilibrador de carga externo Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="1c095-204">En este caso, quite AppPort1 de equilibrador de carga externo hello `loadBalancingRules` y sondeos, para que pueda agregar equilibrador de carga interno de toohello:</span><span class="sxs-lookup"><span data-stu-id="1c095-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="1c095-205">Agregue un segundo recurso `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="1c095-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="1c095-206">Parece que el equilibrador de carga interno toohello similar creado en hello [equilibrador de carga interno solo](#internallb) sección, pero usa Hola "-Int" cargar equilibrador variables e implementa sólo Hola aplicación el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="1c095-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="1c095-207">Este procedimiento quita también `inboundNatPools`, tookeep puntos de conexión RDP en el equilibrador de carga públicos Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="1c095-208">Si desea RDP en el equilibrador de carga interno de hello, mueva `inboundNatPools` de toothis de equilibrador de carga externo Hola interno equilibrador de carga:</span><span class="sxs-lookup"><span data-stu-id="1c095-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="1c095-209">En `networkProfile` para hello `Microsoft.Compute/virtualMachineScaleSets` recursos, Agregar grupo de direcciones de back-end interno de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="1c095-210">Implementar la plantilla de hello:</span><span class="sxs-lookup"><span data-stu-id="1c095-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="1c095-211">Después de la implementación, puede ver dos equilibradores de carga en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1c095-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="1c095-212">Si examina los equilibradores de carga de hello, puede ver la dirección IP pública hello y dirección IP pública de toohello de puntos de conexión (puertos 19000 y 19080) asignados de administración.</span><span class="sxs-lookup"><span data-stu-id="1c095-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="1c095-213">También puede ver Hola estático interno IP dirección y aplicación de punto de conexión (puerto 80) asignado toohello interno equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="1c095-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="1c095-214">Uso de equilibradores de carga mismo escalas de máquina virtual hello Establecer grupo back-end.</span><span class="sxs-lookup"><span data-stu-id="1c095-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c095-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1c095-215">Next steps</span></span>
[<span data-ttu-id="1c095-216">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="1c095-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
