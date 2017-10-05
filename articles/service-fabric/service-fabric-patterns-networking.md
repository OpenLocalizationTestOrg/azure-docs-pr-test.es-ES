---
title: Patrones de redes para Azure Service Fabric | Microsoft Docs
description: "En este artículo se describen los patrones de redes comunes de Service Fabric y cómo crear un clúster con las características de red de Azure."
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
ms.openlocfilehash: 126637002b24391058fb702227a570aa0b58c1d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="9d638-103">Patrones de redes de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d638-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="9d638-104">Puede integrar el clúster de Azure Service Fabric con otras características de red de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d638-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="9d638-105">En este artículo se muestra cómo crear clústeres que usan las siguientes características:</span><span class="sxs-lookup"><span data-stu-id="9d638-105">In this article, we show you how to create clusters that use the following features:</span></span>

- [<span data-ttu-id="9d638-106">Subred y red virtual existentes</span><span class="sxs-lookup"><span data-stu-id="9d638-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="9d638-107">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="9d638-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="9d638-108">Equilibrador de carga solo interno</span><span class="sxs-lookup"><span data-stu-id="9d638-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="9d638-109">Equilibrador de carga interno y externo</span><span class="sxs-lookup"><span data-stu-id="9d638-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="9d638-110">Service Fabric se ejecuta en un conjunto de escalado de máquinas virtuales estándar.</span><span class="sxs-lookup"><span data-stu-id="9d638-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="9d638-111">Cualquier funcionalidad que pueda usar en un conjunto de escalado de máquinas virtuales, puede usarse con un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d638-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="9d638-112">Las secciones de red de las plantillas de Azure Resource Manager para los conjuntos de escalado de máquinas virtuales y Service Fabric son idénticas.</span><span class="sxs-lookup"><span data-stu-id="9d638-112">The networking sections of the Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="9d638-113">Después de implementar en una red virtual existente, es fácil incorporar otras características de red como Azure ExpressRoute, Azure VPN Gateway, un grupo de seguridad de red y emparejamiento de redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="9d638-113">After you deploy to an existing virtual network, it's easy to incorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="9d638-114">Service Fabric es único en relación con otras características de red en un aspecto.</span><span class="sxs-lookup"><span data-stu-id="9d638-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="9d638-115">[Azure Portal](https://portal.azure.com) usa internamente el proveedor de recursos de Service Fabric para llamar a un clúster con el fin de obtener información de los nodos y las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9d638-115">The [Azure portal](https://portal.azure.com) internally uses the Service Fabric resource provider to call to a cluster to get information about nodes and applications.</span></span> <span data-ttu-id="9d638-116">El proveedor de recursos de Service Fabric requiere acceso de entrada público al puerto de la puerta de enlace HTTP (puerto 19080 de forma predeterminada) en el punto de conexión de administración.</span><span class="sxs-lookup"><span data-stu-id="9d638-116">The Service Fabric resource provider requires publicly accessible inbound access to the HTTP gateway port (port 19080, by default) on the management endpoint.</span></span> <span data-ttu-id="9d638-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) utiliza el punto de conexión de administración para administrar el clúster.</span><span class="sxs-lookup"><span data-stu-id="9d638-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses the management endpoint to manage your cluster.</span></span> <span data-ttu-id="9d638-118">Este puerto también lo emplea el proveedor de recursos de Service Fabric para consultar información sobre el clúster con el fin de que se muestre en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9d638-118">The Service Fabric resource provider also uses this port to query information about your cluster, to display in the Azure portal.</span></span> 

<span data-ttu-id="9d638-119">Si el puerto 19080 no es accesible desde el proveedor de recursos de Service Fabric, aparecerá un mensaje del tipo *No se encontraron los nodos* en el portal, y la lista de nodos y aplicaciones aparecerá vacía.</span><span class="sxs-lookup"><span data-stu-id="9d638-119">If port 19080 is not accessible from the Service Fabric resource provider, a message like *Nodes Not Found* appears in the portal, and your node and application list appears empty.</span></span> <span data-ttu-id="9d638-120">Si desea ver el clúster en Azure Portal, el equilibrador de carga debe exponer una dirección IP pública y el grupo de seguridad de red debe permitir el tráfico entrante en el puerto 19080.</span><span class="sxs-lookup"><span data-stu-id="9d638-120">If you want to see your cluster in the Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="9d638-121">Si no se cumplen estos requisitos de configuración, Azure Portal no mostrará el estado del clúster.</span><span class="sxs-lookup"><span data-stu-id="9d638-121">If your setup does not meet these requirements, the Azure portal does not display the status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="9d638-122">Plantillas</span><span class="sxs-lookup"><span data-stu-id="9d638-122">Templates</span></span>

<span data-ttu-id="9d638-123">Todas las plantillas de Service Fabric están en [un archivo de descarga](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="9d638-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="9d638-124">Debe poder implementar las plantillas tal como están con los siguientes comandos de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9d638-124">You should be able to deploy the templates as-is by using the following PowerShell commands.</span></span> <span data-ttu-id="9d638-125">Si va a implementar la plantilla existente de Azure Virtual Network o la de dirección IP pública estática, lea primero la sección [Configuración inicial](#initialsetup) de este artículo.</span><span class="sxs-lookup"><span data-stu-id="9d638-125">If you are deploying the existing Azure Virtual Network template or the static public IP template, first read the [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="9d638-126">Configuración inicial</span><span class="sxs-lookup"><span data-stu-id="9d638-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="9d638-127">Red virtual existente</span><span class="sxs-lookup"><span data-stu-id="9d638-127">Existing virtual network</span></span>

<span data-ttu-id="9d638-128">En el ejemplo siguiente, vamos a empezar con una red virtual existente denominada "ExistingRG-vnet" en el grupo de recursos **ExistingRG**.</span><span class="sxs-lookup"><span data-stu-id="9d638-128">In the following example, we start with an existing virtual network named ExistingRG-vnet, in the **ExistingRG** resource group.</span></span> <span data-ttu-id="9d638-129">La subred recibe un nombre predeterminado.</span><span class="sxs-lookup"><span data-stu-id="9d638-129">The subnet is named default.</span></span> <span data-ttu-id="9d638-130">Estos recursos predeterminados son los que se crearon al usar Azure Portal para crear una máquina virtual estándar.</span><span class="sxs-lookup"><span data-stu-id="9d638-130">These default resources are created when you use the Azure portal to create a standard virtual machine (VM).</span></span> <span data-ttu-id="9d638-131">Se podría crear la red y subred virtual sin necesidad de crear la máquina virtual, pero el objetivo principal de agregar un clúster a una red virtual existente es proporcionar conectividad de red a otras máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9d638-131">You could create the virtual network and subnet without creating the VM, but the main goal of adding a cluster to an existing virtual network is to provide network connectivity to other VMs.</span></span> <span data-ttu-id="9d638-132">La creación de la máquina virtual proporciona un buen ejemplo de cómo se usa normalmente una red virtual existente.</span><span class="sxs-lookup"><span data-stu-id="9d638-132">Creating the VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="9d638-133">Si el clúster de Service Fabric solo usa un equilibrador de carga interno, sin una dirección IP pública, podrá usar la máquina virtual con su dirección IP pública como *equipo de inicio de sesión seguro*.</span><span class="sxs-lookup"><span data-stu-id="9d638-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use the VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="9d638-134">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="9d638-134">Static public IP address</span></span>

<span data-ttu-id="9d638-135">Una dirección IP pública estática es normalmente un recurso dedicado que se administra de forma independiente de las máquinas virtuales a las que está asignada.</span><span class="sxs-lookup"><span data-stu-id="9d638-135">A static public IP address generally is a dedicated resource that's managed separately from the VM or VMs it's assigned to.</span></span> <span data-ttu-id="9d638-136">Se aprovisiona en un grupo de recursos de red dedicado (en contraposición al aprovisionamiento en el grupo de recursos del clúster de Service Fabric en sí).</span><span class="sxs-lookup"><span data-stu-id="9d638-136">It's provisioned in a dedicated networking resource group (as opposed to in the Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="9d638-137">Cree una dirección IP pública estática con el nombre "staticIP1" en el mismo grupo de recursos ExistingRG, ya sea a través de Azure Portal o mediante PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9d638-137">Create a static public IP address named staticIP1 in the same ExistingRG resource group, either in the Azure portal or by using PowerShell:</span></span>

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

### <a name="service-fabric-template"></a><span data-ttu-id="9d638-138">Plantilla de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d638-138">Service Fabric template</span></span>

<span data-ttu-id="9d638-139">En los ejemplos de este artículo, usamos el archivo template.json de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d638-139">In the examples in this article, we use the Service Fabric template.json.</span></span> <span data-ttu-id="9d638-140">Puede usar el asistente estándar del portal para descargar la plantilla desde el portal antes de crear un clúster.</span><span class="sxs-lookup"><span data-stu-id="9d638-140">You can use the standard portal wizard to download the template from the portal before you create a cluster.</span></span> <span data-ttu-id="9d638-141">También puede emplear una de las plantillas de la [galería de plantillas](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), como la del [clúster de cinco nodos de Service Fabric](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="9d638-141">You also can use one of the templates in the [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like the [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="9d638-142">Subred y red virtual existentes</span><span class="sxs-lookup"><span data-stu-id="9d638-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="9d638-143">Cambie el parámetro de subred al nombre de la subred existente y agregue dos nuevos parámetros para hacer referencia a la red virtual existente:</span><span class="sxs-lookup"><span data-stu-id="9d638-143">Change the subnet parameter to the name of the existing subnet, and then add two new parameters to reference the existing virtual network:</span></span>

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


2. <span data-ttu-id="9d638-144">Cambie la variable `vnetID` para que apunte a la red virtual existente:</span><span class="sxs-lookup"><span data-stu-id="9d638-144">Change the `vnetID` variable to point to the existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="9d638-145">Quite `Microsoft.Network/virtualNetworks` de los recursos, para que Azure no cree una nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="9d638-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

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

4. <span data-ttu-id="9d638-146">Comente la red virtual del atributo `dependsOn` de `Microsoft.Compute/virtualMachineScaleSets`, para que no dependa de crear una nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="9d638-146">Comment out the virtual network from the `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

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

5. <span data-ttu-id="9d638-147">Implemente la plantilla:</span><span class="sxs-lookup"><span data-stu-id="9d638-147">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="9d638-148">Después de la implementación, la red virtual debe incluir las nuevas máquinas virtuales del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="9d638-148">After deployment, your virtual network should include the new scale set VMs.</span></span> <span data-ttu-id="9d638-149">El tipo de nodo del conjunto de escalado de máquinas virtuales debe mostrar la red virtual y la subred existentes.</span><span class="sxs-lookup"><span data-stu-id="9d638-149">The virtual machine scale set node type should show the existing virtual network and subnet.</span></span> <span data-ttu-id="9d638-150">También puede usar el protocolo de escritorio remoto (RDP) para tener acceso a la máquina virtual que se encontraba ya en la red virtual y hacer ping en las nuevas máquinas virtuales del conjunto de escalado:</span><span class="sxs-lookup"><span data-stu-id="9d638-150">You also can use Remote Desktop Protocol (RDP) to access the VM that was already in the virtual network, and to ping the new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="9d638-151">Para obtener otro ejemplo, consulte [uno que no es específico de Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="9d638-151">For another example, see [one that is not specific to Service Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="9d638-152">Dirección IP pública estática</span><span class="sxs-lookup"><span data-stu-id="9d638-152">Static public IP address</span></span>

1. <span data-ttu-id="9d638-153">Agregue parámetros para el nombre del grupo de recursos de direcciones IP estáticas existente, el nombre y el nombre de dominio completo (FQDN):</span><span class="sxs-lookup"><span data-stu-id="9d638-153">Add parameters for the name of the existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

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

2. <span data-ttu-id="9d638-154">Elimine el parámetro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="9d638-154">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="9d638-155">(La dirección IP estática ya tiene uno).</span><span class="sxs-lookup"><span data-stu-id="9d638-155">(The static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="9d638-156">Agregue una variable para hacer referencia a la dirección IP estática existente:</span><span class="sxs-lookup"><span data-stu-id="9d638-156">Add a variable to reference the existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="9d638-157">Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="9d638-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

5. <span data-ttu-id="9d638-158">Comente la dirección IP del atributo `dependsOn` de `Microsoft.Network/loadBalancers`, para que no dependa de crear una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="9d638-158">Comment out the IP address from the `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

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

6. <span data-ttu-id="9d638-159">En el recurso `Microsoft.Network/loadBalancers`, cambie el elemento `publicIPAddress` de `frontendIPConfigurations` para que haga referencia a la dirección IP estática existente en lugar de a una recién creada:</span><span class="sxs-lookup"><span data-stu-id="9d638-159">In the `Microsoft.Network/loadBalancers` resource, change the `publicIPAddress` element of `frontendIPConfigurations` to reference the existing static IP address instead of a newly created one:</span></span>

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

7. <span data-ttu-id="9d638-160">En el recurso `Microsoft.ServiceFabric/clusters`, cambie `managementEndpoint` al FQDN de DNS de la dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="9d638-160">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to the DNS FQDN of the static IP address.</span></span> <span data-ttu-id="9d638-161">Si está usando un clúster seguro, asegúrese de cambiar *http://* a *https://*.</span><span class="sxs-lookup"><span data-stu-id="9d638-161">If you are using a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="9d638-162">(Tenga en cuenta que este paso se aplica solo a los clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d638-162">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="9d638-163">Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).</span><span class="sxs-lookup"><span data-stu-id="9d638-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="9d638-164">Implemente la plantilla:</span><span class="sxs-lookup"><span data-stu-id="9d638-164">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="9d638-165">Después de la implementación, puede ver que el equilibrador de carga está enlazado a la dirección IP estática pública del otro grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d638-165">After deployment, you can see that your load balancer is bound to the public static IP address from the other resource group.</span></span> <span data-ttu-id="9d638-166">El punto de conexión del cliente de Service Fabric y [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) apuntan al FQDN de DNS de la dirección IP estática.</span><span class="sxs-lookup"><span data-stu-id="9d638-166">The Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point to the DNS FQDN of the static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="9d638-167">Equilibrador de carga solo interno</span><span class="sxs-lookup"><span data-stu-id="9d638-167">Internal-only load balancer</span></span>

<span data-ttu-id="9d638-168">Este escenario reemplaza el equilibrador de carga externo en la plantilla predeterminada de Service Fabric por un equilibrador de carga solo interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-168">This scenario replaces the external load balancer in the default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="9d638-169">Para conocer las implicaciones en Azure Portal y en el proveedor de recursos de Service Fabric, consulte la sección anterior.</span><span class="sxs-lookup"><span data-stu-id="9d638-169">For implications for the Azure portal and for the Service Fabric resource provider, see the preceding section.</span></span>

1. <span data-ttu-id="9d638-170">Elimine el parámetro `dnsName`.</span><span class="sxs-lookup"><span data-stu-id="9d638-170">Remove the `dnsName` parameter.</span></span> <span data-ttu-id="9d638-171">(No es necesario).</span><span class="sxs-lookup"><span data-stu-id="9d638-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="9d638-172">Si lo desea, puede agregar un parámetro de dirección IP estática, si usa el método de asignación estático.</span><span class="sxs-lookup"><span data-stu-id="9d638-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="9d638-173">Si usa un método de asignación dinámico, no es necesario realizar este paso.</span><span class="sxs-lookup"><span data-stu-id="9d638-173">If you use a dynamic allocation method, you do not need to do this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="9d638-174">Quite `Microsoft.Network/publicIPAddresses` de los recursos, para que Azure no cree una nueva dirección IP:</span><span class="sxs-lookup"><span data-stu-id="9d638-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

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

4. <span data-ttu-id="9d638-175">Elimine la dirección IP del atributo `dependsOn` de `Microsoft.Network/loadBalancers`, para que no dependa de crear una nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="9d638-175">Remove the IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="9d638-176">Agregue el atributo `dependsOn` de la red virtual porque el equilibrador de carga ahora depende de la subred de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="9d638-176">Add the virtual network `dependsOn` attribute because the load balancer now depends on the subnet from the virtual network:</span></span>

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

5. <span data-ttu-id="9d638-177">Cambie la configuración `frontendIPConfigurations` del equilibrador de carga para que pase de usar un `publicIPAddress` a usar una subred y `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="9d638-177">Change the load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, to using a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="9d638-178">`privateIPAddress` usa una dirección IP interna estática predefinida.</span><span class="sxs-lookup"><span data-stu-id="9d638-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="9d638-179">Para utilizar una dirección IP dinámica, quite el elemento `privateIPAddress` y, a continuación, cambie `privateIPAllocationMethod` a **Dinámico**.</span><span class="sxs-lookup"><span data-stu-id="9d638-179">To use a dynamic IP address, remove the `privateIPAddress` element, and then change `privateIPAllocationMethod` to **Dynamic**.</span></span>

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

6. <span data-ttu-id="9d638-180">En el recurso `Microsoft.ServiceFabric/clusters`, cambie `managementEndpoint` para que apunte a la dirección del equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-180">In the `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` to point to the internal load balancer address.</span></span> <span data-ttu-id="9d638-181">Si usa un clúster seguro, asegúrese de cambiar *http://* a *https://*.</span><span class="sxs-lookup"><span data-stu-id="9d638-181">If you use a secure cluster, make sure you change *http://* to *https://*.</span></span> <span data-ttu-id="9d638-182">(Tenga en cuenta que este paso se aplica solo a los clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d638-182">(Note that this step applies only to Service Fabric clusters.</span></span> <span data-ttu-id="9d638-183">Si está empleando un conjunto de escalado de máquinas virtuales, omita este paso).</span><span class="sxs-lookup"><span data-stu-id="9d638-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="9d638-184">Implemente la plantilla:</span><span class="sxs-lookup"><span data-stu-id="9d638-184">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="9d638-185">Después de la implementación, el equilibrador de carga usará la dirección IP privada estática 10.0.0.250.</span><span class="sxs-lookup"><span data-stu-id="9d638-185">After deployment, your load balancer uses the private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="9d638-186">Si tiene otra máquina en esa misma red virtual puede ir al punto de conexión interno de [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9d638-186">If you have another machine in that same virtual network, you can go to the internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="9d638-187">Tenga en cuenta que se conecta a uno de los nodos detrás del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9d638-187">Note that it connects to one of the nodes behind the load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="9d638-188">Equilibrador de carga interno y externo</span><span class="sxs-lookup"><span data-stu-id="9d638-188">Internal and external load balancer</span></span>

<span data-ttu-id="9d638-189">En este escenario, comienza por el equilibrador de carga externo de un solo tipo de nodo y se agrega un equilibrador de carga interno adicional al mismo tipo de nodo.</span><span class="sxs-lookup"><span data-stu-id="9d638-189">In this scenario, you start with the existing single-node type external load balancer, and add an internal load balancer for the same node type.</span></span> <span data-ttu-id="9d638-190">Un puerto de back-end conectado a un grupo de direcciones de back-end solo se puede asignar a un único equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="9d638-190">A back-end port attached to a back-end address pool can be assigned only to a single load balancer.</span></span> <span data-ttu-id="9d638-191">Elija qué equilibrador de carga tendrá los puertos de la aplicación y cuál tendrá los puntos de conexión de administración (puertos 19000 y 19080).</span><span class="sxs-lookup"><span data-stu-id="9d638-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="9d638-192">Si pone los puntos de conexión de administración en el equilibrador de carga interno, tenga en cuenta las restricciones del proveedor de recursos de Service Fabric descritas anteriormente en este artículo.</span><span class="sxs-lookup"><span data-stu-id="9d638-192">If you put the management endpoints on the internal load balancer, keep in mind the Service Fabric resource provider restrictions discussed earlier in the article.</span></span> <span data-ttu-id="9d638-193">En el ejemplo que estamos utilizando, los puntos de conexión de administración permanecen en el equilibrador de carga externo.</span><span class="sxs-lookup"><span data-stu-id="9d638-193">In the example we use, the management endpoints remain on the external load balancer.</span></span> <span data-ttu-id="9d638-194">También puede agregar un puerto de aplicación 80 y colocarlo en el equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-194">You also add a port 80 application port, and place it on the internal load balancer.</span></span>

<span data-ttu-id="9d638-195">En un clúster de dos tipos de nodo, un tipo de nodo está en el equilibrador de carga externo.</span><span class="sxs-lookup"><span data-stu-id="9d638-195">In a two-node-type cluster, one node type is on the external load balancer.</span></span> <span data-ttu-id="9d638-196">El otro estará en el equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-196">The other node type is on the internal load balancer.</span></span> <span data-ttu-id="9d638-197">Para usar un clúster de dos tipos de nodo, en la plantilla de dos tipos de nodo creada en el portal (que incluye dos equilibradores de carga), cambie el segundo equilibrador de carga a un equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-197">To use a two-node-type cluster, in the portal-created two-node-type template (which comes with two load balancers), switch the second load balancer to an internal load balancer.</span></span> <span data-ttu-id="9d638-198">Para más información, consulte la sección [Equilibrador de carga solo interno](#internallb).</span><span class="sxs-lookup"><span data-stu-id="9d638-198">For more information, see the [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="9d638-199">Agregue el parámetro de dirección IP del equilibrador de carga interno estático.</span><span class="sxs-lookup"><span data-stu-id="9d638-199">Add the static internal load balancer IP address parameter.</span></span> <span data-ttu-id="9d638-200">(Para ver las notas relativas al uso de una dirección IP dinámica, consulte las secciones anteriores de este artículo).</span><span class="sxs-lookup"><span data-stu-id="9d638-200">(For notes related to using a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="9d638-201">Agregue un parámetro de puerto 80 de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d638-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="9d638-202">Para agregar las versiones internas de las variables de red existentes, cópielas y péguelas y agregue "-Int" al nombre:</span><span class="sxs-lookup"><span data-stu-id="9d638-202">To add internal versions of the existing networking variables, copy and paste them, and add "-Int" to the name:</span></span>

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

4. <span data-ttu-id="9d638-203">Si ha empezado con la plantilla generada mediante el portal que usa un puerto 80 de aplicación, la plantilla del portal predeterminada agrega AppPort1 (puerto 80) en el equilibrador de carga externo.</span><span class="sxs-lookup"><span data-stu-id="9d638-203">If you start with the portal-generated template that uses application port 80, the default portal template adds AppPort1 (port 80) on the external load balancer.</span></span> <span data-ttu-id="9d638-204">En este caso, elimine AppPort1 de los sondeos y del elemento `loadBalancingRules` del equilibrador de carga externo para que pueda agregarlo al equilibrador de carga interno:</span><span class="sxs-lookup"><span data-stu-id="9d638-204">In this case, remove AppPort1 from the external load balancer `loadBalancingRules` and probes, so you can add it to the internal load balancer:</span></span>

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
        } /* Remove AppPort1 from the external load balancer.
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
        } /* Remove AppPort1 from the external load balancer.
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

5. <span data-ttu-id="9d638-205">Agregue un segundo recurso `Microsoft.Network/loadBalancers`.</span><span class="sxs-lookup"><span data-stu-id="9d638-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="9d638-206">Se parece al equilibrador de carga interno creado en la sección [Equilibrador de carga solo interno](#internallb), pero usa las variables "-Int" del equilibrador de carga e implementa únicamente el puerto 80 de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d638-206">It looks similar to the internal load balancer created in the [Internal-only load balancer](#internallb) section, but it uses the "-Int" load balancer variables, and implements only the application port 80.</span></span> <span data-ttu-id="9d638-207">Este procedimiento quita también `inboundNatPools`, para conservar los puntos de conexión RDP en el equilibrador de carga público.</span><span class="sxs-lookup"><span data-stu-id="9d638-207">This also removes `inboundNatPools`, to keep RDP endpoints on the public load balancer.</span></span> <span data-ttu-id="9d638-208">Si desea acceder mediante RDP en el equilibrador de carga interno, mueva `inboundNatPools` del equilibrador de carga externo a este interno:</span><span class="sxs-lookup"><span data-stu-id="9d638-208">If you want RDP on the internal load balancer, move `inboundNatPools` from the external load balancer to this internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and the "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" to the name. */
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
                                /* Switch from Public to Private IP address
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
                        /* Add the AppPort rule. Be sure to reference the "-Int" versions of backendAddressPool, frontendIPConfiguration, and the probe variables. */
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
                    /* Add the probe for the app port. */
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

6. <span data-ttu-id="9d638-209">En `networkProfile` para el recurso `Microsoft.Compute/virtualMachineScaleSets`, agregue el grupo de direcciones de back-end interno:</span><span class="sxs-lookup"><span data-stu-id="9d638-209">In `networkProfile` for the `Microsoft.Compute/virtualMachineScaleSets` resource, add the internal back-end address pool:</span></span>

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

7. <span data-ttu-id="9d638-210">Implemente la plantilla:</span><span class="sxs-lookup"><span data-stu-id="9d638-210">Deploy the template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="9d638-211">Después de la implementación, puede ver dos de equilibradores de carga en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="9d638-211">After deployment, you can see two load balancers in the resource group.</span></span> <span data-ttu-id="9d638-212">Si examina los equilibradores de carga, puede ver la dirección IP pública y los puntos de conexión de administración (puertos 19000 y 19080) asignados a la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="9d638-212">If you browse the load balancers, you can see the public IP address and management endpoints (ports 19000 and 19080) assigned to the public IP address.</span></span> <span data-ttu-id="9d638-213">También puede ver la dirección IP interna estática y el punto de conexión de la aplicación (puerto 80) asignados al equilibrador de carga interno.</span><span class="sxs-lookup"><span data-stu-id="9d638-213">You also can see the static internal IP address and application endpoint (port 80) assigned to the internal load balancer.</span></span> <span data-ttu-id="9d638-214">Ambos equilibradores de carga usan el mismo grupo de back-end de conjunto de escalado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9d638-214">Both load balancers use the same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d638-215">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d638-215">Next steps</span></span>
[<span data-ttu-id="9d638-216">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="9d638-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
