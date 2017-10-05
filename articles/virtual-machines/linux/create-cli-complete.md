---
title: "Creación de un entorno de Linux con la CLI de Azure 2.0 | Microsoft Docs"
description: "Cree almacenamiento, una máquina virtual Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública, un grupo de seguridad de red, todo desde el principio mediante la CLI de Azure 2.0."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="c9be0-103">Creación de una máquina virtual completa de Linux con la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c9be0-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="c9be0-104">Para crear rápidamente una máquina virtual en Azure, puede usar un solo comando de la CLI de Azure que use valores predeterminados para crear los recursos de apoyo necesarios.</span><span class="sxs-lookup"><span data-stu-id="c9be0-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="c9be0-105">Los recursos como una red virtual, una dirección IP pública y reglas de grupo de seguridad de red se crean automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c9be0-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="c9be0-106">Para tener más control del entorno en uso de producción, puede crear estos recursos antes de tiempo y luego agregarles las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c9be0-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="c9be0-107">Este artículo lo guía a lo largo del proceso de creación de una máquina virtual y de cada uno de los recursos de apoyo.</span><span class="sxs-lookup"><span data-stu-id="c9be0-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="c9be0-108">Asegúrese de que ha instalado la versión más reciente de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e iniciado sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c9be0-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c9be0-109">En los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo por los suyos propios.</span><span class="sxs-lookup"><span data-stu-id="c9be0-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c9be0-110">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c9be0-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="c9be0-111">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c9be0-111">Create resource group</span></span>
<span data-ttu-id="c9be0-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9be0-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c9be0-113">Se debe crear un grupo de recursos antes que una máquina virtual y los recursos de red virtual de apoyo.</span><span class="sxs-lookup"><span data-stu-id="c9be0-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="c9be0-114">Cree el grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c9be0-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c9be0-115">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *eastus*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c9be0-116">De forma predeterminada, la salida de los comandos de la CLI de Azure está en JSON (notación de objetos JavaScript).</span><span class="sxs-lookup"><span data-stu-id="c9be0-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="c9be0-117">Para cambiar la salida predeterminada a una lista o tabla, por ejemplo, use [az configure --output](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="c9be0-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="c9be0-118">También puede agregar `--output` a cualquier comando para un cambio específico del formato de salida.</span><span class="sxs-lookup"><span data-stu-id="c9be0-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="c9be0-119">En el ejemplo siguiente se muestra la salida JSON desde el comando `az group create`:</span><span class="sxs-lookup"><span data-stu-id="c9be0-119">The following example shows the JSON output from the `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="c9be0-120">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="c9be0-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="c9be0-121">Después el usuario crea una red virtual en Azure y una subred en la que pueda crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c9be0-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="c9be0-122">Use [az network vnet create](/cli/azure/network/vnet#create) para crear una red virtual denominada *myVnet* con el prefijo de dirección *192.168.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="c9be0-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="c9be0-123">Agregue también una subred denominada *mySubnet* con el prefijo de dirección *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="c9be0-124">La salida muestra la subred como creada lógicamente dentro de la red virtual:</span><span class="sxs-lookup"><span data-stu-id="c9be0-124">The output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="c9be0-125">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="c9be0-125">Create a public IP address</span></span>
<span data-ttu-id="c9be0-126">Ahora cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="c9be0-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="c9be0-127">Esta dirección IP pública le permite conectarse a las máquinas virtuales desde Internet.</span><span class="sxs-lookup"><span data-stu-id="c9be0-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="c9be0-128">Dado que la dirección predeterminada es dinámica, también se crea una entrada DNS con nombre con la opción `--domain-name-label`.</span><span class="sxs-lookup"><span data-stu-id="c9be0-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="c9be0-129">En el ejemplo siguiente se crea una IP pública denominada "*myPublicIP*" con el nombre DNS *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="c9be0-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="c9be0-130">Como el nombre DNS debe ser único, especifique su propio nombre DNS único:</span><span class="sxs-lookup"><span data-stu-id="c9be0-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="c9be0-131">Salida:</span><span class="sxs-lookup"><span data-stu-id="c9be0-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="c9be0-132">Crear un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="c9be0-132">Create a network security group</span></span>
<span data-ttu-id="c9be0-133">Para controlar el flujo de tráfico de entrada y salida de las máquinas virtuales, cree un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c9be0-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="c9be0-134">Un grupo de seguridad de red puede aplicarse a una tarjeta de interfaz de red o a una subred.</span><span class="sxs-lookup"><span data-stu-id="c9be0-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="c9be0-135">En el ejemplo siguiente se usa [az network nsg create](/cli/azure/network/nsg#create) para crear un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="c9be0-136">Defina las reglas que permiten o deniegan el tráfico específico.</span><span class="sxs-lookup"><span data-stu-id="c9be0-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="c9be0-137">Para permitir las conexiones entrantes en el puerto 22 (para admitir SSH), cree una regla de entrada para el grupo de seguridad de red con [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="c9be0-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="c9be0-138">En el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="c9be0-139">Para permitir las conexiones entrantes en el puerto 80 (para admitir el tráfico web), agregue otra regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c9be0-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="c9be0-140">En el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="c9be0-141">Examine el grupo de seguridad de red y las reglas con [az network nsg create](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="c9be0-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="c9be0-142">Salida:</span><span class="sxs-lookup"><span data-stu-id="c9be0-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="c9be0-143">Crear un adaptador de red virtual</span><span class="sxs-lookup"><span data-stu-id="c9be0-143">Create a virtual NIC</span></span>
<span data-ttu-id="c9be0-144">Los adaptadores de red (NIC) virtuales están disponibles mediante programación porque se pueden aplicar reglas a su uso.</span><span class="sxs-lookup"><span data-stu-id="c9be0-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="c9be0-145">También puede tener más de una.</span><span class="sxs-lookup"><span data-stu-id="c9be0-145">You can also have more than one.</span></span> <span data-ttu-id="c9be0-146">En el siguiente comando [az network nic create](/cli/azure/network/nic#create), cree un NIC denominado *myNic* y asócielo al grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="c9be0-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="c9be0-147">La dirección IP pública *myPublicIP* también se asocia al NIC virtual.</span><span class="sxs-lookup"><span data-stu-id="c9be0-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="c9be0-148">Salida:</span><span class="sxs-lookup"><span data-stu-id="c9be0-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="c9be0-149">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="c9be0-149">Create an availability set</span></span>
<span data-ttu-id="c9be0-150">Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y de actualización.</span><span class="sxs-lookup"><span data-stu-id="c9be0-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="c9be0-151">Aunque ahora solo cree una máquina virtual, es recomendable usar conjuntos de disponibilidad para facilitar la propagación en el futuro.</span><span class="sxs-lookup"><span data-stu-id="c9be0-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="c9be0-152">Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="c9be0-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="c9be0-153">De manera predeterminada, las máquinas virtuales configuradas dentro de su conjunto de disponibilidad se separan en hasta tres dominios de error.</span><span class="sxs-lookup"><span data-stu-id="c9be0-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="c9be0-154">Un problema de hardware en uno de estos dominios de error no afecta a todas las máquinas virtuales que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c9be0-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="c9be0-155">Los dominios de actualización indican grupos de máquinas virtuales y hardware físico subyacente que se pueden reiniciar al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="c9be0-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="c9be0-156">Durante el mantenimiento planeado, es posible que el orden de reinicio de los dominios de actualización no sea secuencial, sino que solo se reinicie un dominio de actualización cada vez.</span><span class="sxs-lookup"><span data-stu-id="c9be0-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="c9be0-157">Azure distribuye automáticamente las máquinas virtuales en los dominios de error y actualización al colocarlas en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="c9be0-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="c9be0-158">Para más información, vea [Administración de la disponibilidad de las máquinas virtuales](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="c9be0-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="c9be0-159">Cree un conjunto de disponibilidad para las máquinas virtuales con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="c9be0-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="c9be0-160">En el ejemplo siguiente se crea un conjunto de disponibilidad denominado *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="c9be0-161">La salida anota los dominios de error y de actualización:</span><span class="sxs-lookup"><span data-stu-id="c9be0-161">The output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-the-linux-vms"></a><span data-ttu-id="c9be0-162">Creación de las máquinas virtuales Linux</span><span class="sxs-lookup"><span data-stu-id="c9be0-162">Create the Linux VMs</span></span>
<span data-ttu-id="c9be0-163">Ha creado los recursos de red para dar soporte a VM con acceso a Internet.</span><span class="sxs-lookup"><span data-stu-id="c9be0-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="c9be0-164">Ahora cree una máquina virtual y protéjala con una clave SSH.</span><span class="sxs-lookup"><span data-stu-id="c9be0-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="c9be0-165">En este caso, vamos a crear una máquina virtual con Ubuntu basada en la LTM más reciente.</span><span class="sxs-lookup"><span data-stu-id="c9be0-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="c9be0-166">Puede encontrar imágenes adicionales con [az vm image list](/cli/azure/vm/image#list), como se explica en [Finding Azure VM images (Búsqueda de imágenes de máquina virtual de Azure)](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="c9be0-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="c9be0-167">También especificamos una clave SSH para usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="c9be0-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="c9be0-168">Si no tiene un par de claves públicas de SSH, puede [crearlas](mac-create-ssh-keys.md) o usar el parámetro `--generate-ssh-keys` para crearlas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c9be0-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="c9be0-169">Si ya tiene un par de claves, este parámetro usa las claves existentes en `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="c9be0-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="c9be0-170">Cree la máquina virtual al recopilar toda la información y los recursos con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c9be0-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="c9be0-171">En el ejemplo siguiente se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c9be0-171">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="c9be0-172">Inicie sesión mediante SSH en la máquina virtual con la entrada DNS que proporcionó al crear la dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="c9be0-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="c9be0-173">Este `fqdn` se muestra en la salida al crear la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="c9be0-173">This `fqdn` is shown in the output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="c9be0-174">Salida:</span><span class="sxs-lookup"><span data-stu-id="c9be0-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="c9be0-175">Puede instalar NGINX y ver el flujo de tráfico a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c9be0-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="c9be0-176">Instale NGINX como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c9be0-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="c9be0-177">Para ver el sitio NGINX predeterminado en acción, abra el explorador web y escriba el FQDN:</span><span class="sxs-lookup"><span data-stu-id="c9be0-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Sitio NGINX predeterminado en la máquina virtual](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="c9be0-179">Exportar como plantilla</span><span class="sxs-lookup"><span data-stu-id="c9be0-179">Export as a template</span></span>
<span data-ttu-id="c9be0-180">¿Y si ahora quiere crear un entorno de desarrollo adicional con los mismos parámetros o un entorno de producción correspondiente?</span><span class="sxs-lookup"><span data-stu-id="c9be0-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="c9be0-181">Resource Manager usa plantillas JSON que definen todos los parámetros de su entorno.</span><span class="sxs-lookup"><span data-stu-id="c9be0-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="c9be0-182">Puede crear entornos enteros haciendo referencia a esta plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="c9be0-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="c9be0-183">Puede [compilar plantillas JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar un entorno existente para que la plantilla JSON se cree automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c9be0-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="c9be0-184">Use [az group export](/cli/azure/group#export) para exportar su grupo de recursos de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c9be0-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="c9be0-185">Este comando crea el archivo `myResourceGroup.json` en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="c9be0-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="c9be0-186">Al crear un entorno a partir de esta plantilla, se le piden todos los nombres de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9be0-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="c9be0-187">Puede rellenar estos nombres en el archivo de plantilla si agrega el parámetro `--include-parameter-default-value` al comando `az group export`.</span><span class="sxs-lookup"><span data-stu-id="c9be0-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="c9be0-188">Edite su plantilla JSON para especificar los nombres de recursos o [cree un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifique los nombres de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9be0-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="c9be0-189">Para crear un entorno desde su plantilla, use [az group deployment create](/cli/azure/group/deployment#create) de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c9be0-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="c9be0-190">Es posible que quiera leer [más sobre cómo realizar implementaciones desde plantillas](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9be0-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c9be0-191">Obtenga información sobre cómo actualizar los entornos de manera incremental, usar el archivo de parámetros y tener acceso a las plantillas desde una única ubicación de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="c9be0-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9be0-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c9be0-192">Next steps</span></span>
<span data-ttu-id="c9be0-193">Ya está listo para empezar a trabajar con varios componentes de red y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="c9be0-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="c9be0-194">Puede usar este entorno de ejemplo para crear la aplicación con los componentes principales aquí presentados.</span><span class="sxs-lookup"><span data-stu-id="c9be0-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
