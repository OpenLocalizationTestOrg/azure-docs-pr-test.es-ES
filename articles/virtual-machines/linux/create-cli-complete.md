---
title: aaaCreate un entorno de Linux con hello 2.0 de CLI de Azure | Documentos de Microsoft
description: "Crear almacenamiento, una VM de Linux, una red virtual y subred, un equilibrador de carga, una NIC, una dirección IP pública y un grupo de seguridad de red, todo ello desde Hola descárguese de corriente mediante el uso de hello 2.0 de CLI de Azure."
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
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="2511a-103">Crear una máquina virtual de Linux completa con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="2511a-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="2511a-104">tooquickly crear una máquina virtual (VM) en Azure, puede usar un solo comando de CLI de Azure que usa de forma predeterminada valores toocreate cualquier requiere compatibilidad con recursos.</span><span class="sxs-lookup"><span data-stu-id="2511a-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="2511a-105">Los recursos como una red virtual, una dirección IP pública y reglas de grupo de seguridad de red se crean automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2511a-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="2511a-106">Para tener más control de su entorno de producción usar, puede crear estos recursos antes de tiempo y, a continuación, agregue el toothem de las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2511a-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="2511a-107">En este artículo le guiará en el proceso de cómo toocreate una máquina virtual y cada uno de Hola recursos de soporte uno por uno.</span><span class="sxs-lookup"><span data-stu-id="2511a-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="2511a-108">Asegúrese de que ha instalado hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) y tooan inició Azure cuenta con [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="2511a-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="2511a-109">En hello en los ejemplos siguientes, reemplace los nombres de parámetros de ejemplo con sus propios valores.</span><span class="sxs-lookup"><span data-stu-id="2511a-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2511a-110">Los nombres de parámetro de ejemplo incluyen *myResourceGroup*, *myVnet* y *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2511a-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="2511a-111">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2511a-111">Create resource group</span></span>
<span data-ttu-id="2511a-112">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="2511a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="2511a-113">Se debe crear un grupo de recursos antes que una máquina virtual y los recursos de red virtual de apoyo.</span><span class="sxs-lookup"><span data-stu-id="2511a-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="2511a-114">Crear grupo de recursos de hello con [crear grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="2511a-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="2511a-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="2511a-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2511a-116">De forma predeterminada, la salida de hello de comandos de CLI de Azure está en JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="2511a-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="2511a-117">toochange Hola predeterminado salida tooa lista o tabla, por ejemplo, utilice [az configurar--salida](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="2511a-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="2511a-118">También puede agregar `--output` cambiar tooany comando para una sola vez en formato de salida.</span><span class="sxs-lookup"><span data-stu-id="2511a-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="2511a-119">Hello en el ejemplo siguiente se muestra resultado JSON Hola Hola `az group create` comando:</span><span class="sxs-lookup"><span data-stu-id="2511a-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="2511a-120">Creación de una red virtual y una subred</span><span class="sxs-lookup"><span data-stu-id="2511a-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="2511a-121">A continuación, crear una red virtual en Azure y una subred de toowhich puede crear las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2511a-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="2511a-122">Use [crear red virtual de red az](/cli/azure/network/vnet#create) toocreate una red virtual denominada *myVnet* con hello *192.168.0.0/16* prefijo de dirección.</span><span class="sxs-lookup"><span data-stu-id="2511a-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="2511a-123">También agregar una subred denominada *mySubnet* con prefijo de dirección de hello *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="2511a-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="2511a-124">salida de Hello muestra subred Hola que lógicamente se crea dentro de la red virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="2511a-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="2511a-125">Crear una dirección IP pública</span><span class="sxs-lookup"><span data-stu-id="2511a-125">Create a public IP address</span></span>
<span data-ttu-id="2511a-126">Ahora cree una dirección IP pública con [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="2511a-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="2511a-127">Esta dirección IP pública permite tooconnect tooyour máquinas virtuales de hello Internet.</span><span class="sxs-lookup"><span data-stu-id="2511a-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="2511a-128">Debido a la dirección predeterminada hello es dinámica, también creamos una entrada DNS con nombre con hello `--domain-name-label` opción.</span><span class="sxs-lookup"><span data-stu-id="2511a-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="2511a-129">Hello en el ejemplo siguiente se crea una IP pública denominada *myPublicIP* con el nombre DNS de Hola de *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="2511a-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="2511a-130">Como nombre DNS de hello debe ser único, proporcionar su propio nombre DNS único:</span><span class="sxs-lookup"><span data-stu-id="2511a-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="2511a-131">Salida:</span><span class="sxs-lookup"><span data-stu-id="2511a-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="2511a-132">Crear un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="2511a-132">Create a network security group</span></span>
<span data-ttu-id="2511a-133">flujo de hello toocontrol de tráfico dentro y fuera de las máquinas virtuales, cree un grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="2511a-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="2511a-134">Un grupo de seguridad de red puede ser aplicada tooa NIC o subred.</span><span class="sxs-lookup"><span data-stu-id="2511a-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="2511a-135">Hello siguiente ejemplo se utiliza [crear az red nsg](/cli/azure/network/nsg#create) toocreate un grupo de seguridad de red denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2511a-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="2511a-136">Definir reglas que permitan o denieguen el tráfico específico de Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="2511a-137">tooallow las conexiones entrantes en el puerto 22 (SSH de toosupport), cree una regla de entrada para el grupo de seguridad de red de hello con [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="2511a-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="2511a-138">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="2511a-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="2511a-139">tooallow las conexiones entrantes en el puerto 80 (tráfico de web toosupport), agregue otra regla de grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="2511a-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="2511a-140">Hello en el ejemplo siguiente se crea una regla denominada *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="2511a-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="2511a-141">Examinar el grupo de seguridad de red de Hola y las reglas con [show de nsg de red az](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="2511a-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="2511a-142">Salida:</span><span class="sxs-lookup"><span data-stu-id="2511a-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs tooInternet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="2511a-143">Crear un adaptador de red virtual</span><span class="sxs-lookup"><span data-stu-id="2511a-143">Create a virtual NIC</span></span>
<span data-ttu-id="2511a-144">Tarjetas de interfaz de red virtual (NIC) están disponibles mediante programación porque puede aplicar reglas tootheir uso.</span><span class="sxs-lookup"><span data-stu-id="2511a-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="2511a-145">También puede tener más de una.</span><span class="sxs-lookup"><span data-stu-id="2511a-145">You can also have more than one.</span></span> <span data-ttu-id="2511a-146">Siguiente hello [crear nic de red az](/cli/azure/network/nic#create) comando, cree una NIC denominada *myNic* y asocie al grupo de seguridad de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="2511a-147">dirección IP pública de Hola *myPublicIP* también está asociado a la NIC virtual Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="2511a-148">Salida:</span><span class="sxs-lookup"><span data-stu-id="2511a-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="2511a-149">Crear un conjunto de disponibilidad</span><span class="sxs-lookup"><span data-stu-id="2511a-149">Create an availability set</span></span>
<span data-ttu-id="2511a-150">Los conjuntos de disponibilidad ayudan a propagar las máquinas virtuales a los dominios de error y de actualización.</span><span class="sxs-lookup"><span data-stu-id="2511a-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="2511a-151">Aunque solo crear ahora una máquina virtual, es mejor práctica toouse disponibilidad conjuntos toomake sea más fácil tooexpand Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="2511a-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="2511a-152">Los dominios de error definen un grupo de máquinas virtuales que comparten una fuente de alimentación común y un conmutador de red.</span><span class="sxs-lookup"><span data-stu-id="2511a-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="2511a-153">De forma predeterminada, máquinas virtuales de Hola que estén configuradas en el conjunto de disponibilidad están separadas a través de dominios de error toothree.</span><span class="sxs-lookup"><span data-stu-id="2511a-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="2511a-154">Un problema de hardware en uno de estos dominios de error no afecta a todas las máquinas virtuales que ejecutan la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2511a-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="2511a-155">Dominios de actualización indican los grupos de máquinas virtuales y el hardware físico subyacente que puede reiniciarse en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="2511a-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="2511a-156">Durante el mantenimiento planeado, orden de hello en los de actualización de dominios se reinician no sea secuencial, pero solo una actualización de dominio se reinicia cada vez.</span><span class="sxs-lookup"><span data-stu-id="2511a-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="2511a-157">Azure distribuye automáticamente las máquinas virtuales entre dominios de error y actualización de hello cuando se coloquen en un conjunto de disponibilidad.</span><span class="sxs-lookup"><span data-stu-id="2511a-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="2511a-158">Para obtener más información, consulte [administrar la disponibilidad de Hola de máquinas virtuales](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="2511a-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="2511a-159">Cree un conjunto de disponibilidad para las máquinas virtuales con [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="2511a-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="2511a-160">Hello en el ejemplo siguiente se crea un conjunto con nombre de disponibilidad *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="2511a-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="2511a-161">dominios de error de notas de la salida de Hello y dominios de actualización:</span><span class="sxs-lookup"><span data-stu-id="2511a-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="2511a-162">Crear máquinas virtuales de Linux de Hola</span><span class="sxs-lookup"><span data-stu-id="2511a-162">Create hello Linux VMs</span></span>
<span data-ttu-id="2511a-163">Ha creado toosupport de recursos de red de hello VM accesibles desde Internet.</span><span class="sxs-lookup"><span data-stu-id="2511a-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="2511a-164">Ahora cree una máquina virtual y protéjala con una clave SSH.</span><span class="sxs-lookup"><span data-stu-id="2511a-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="2511a-165">En este caso, vamos toocreate una VM Ubuntu según hello LTS más reciente.</span><span class="sxs-lookup"><span data-stu-id="2511a-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="2511a-166">Puede encontrar imágenes adicionales con [az vm image list](/cli/azure/vm/image#list), como se explica en [Finding Azure VM images (Búsqueda de imágenes de máquina virtual de Azure)](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="2511a-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="2511a-167">También especificamos un toouse clave SSH para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="2511a-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="2511a-168">Si no tiene un par de claves públicas de SSH, puede [crearlos](mac-create-ssh-keys.md) o usar hello `--generate-ssh-keys` toocreate parámetro usarlas para usted.</span><span class="sxs-lookup"><span data-stu-id="2511a-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="2511a-169">Si ya tiene un par de claves, este parámetro usa las claves existentes en `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="2511a-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="2511a-170">Crear Hola VM si se ponen todos nuestros recursos e información junto con hello [crear vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="2511a-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="2511a-171">Hello en el ejemplo siguiente se crea una máquina virtual denominada *myVM*:</span><span class="sxs-lookup"><span data-stu-id="2511a-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="2511a-172">SSH tooyour VM con hello entrada DNS que proporcionó al crear la dirección IP pública Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="2511a-173">Esto `fqdn` se muestra en la salida de hello a medida que cree la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="2511a-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="2511a-174">Salida:</span><span class="sxs-lookup"><span data-stu-id="2511a-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="2511a-175">Puede instalar NGINX y vea toohello de flujo de tráfico de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2511a-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="2511a-176">Instale NGINX como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2511a-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="2511a-177">sitio NGINX toosee Hola predeterminado en acción, abra el explorador web y escriba su FQDN:</span><span class="sxs-lookup"><span data-stu-id="2511a-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Sitio NGINX predeterminado en la máquina virtual](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="2511a-179">Exportar como plantilla</span><span class="sxs-lookup"><span data-stu-id="2511a-179">Export as a template</span></span>
<span data-ttu-id="2511a-180">¿Qué ocurre si ahora desea toocreate un entorno de desarrollo adicional con hello mismos parámetros o un entorno de producción que coincida con él?</span><span class="sxs-lookup"><span data-stu-id="2511a-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="2511a-181">Administrador de recursos usa plantillas JSON que definen todos los parámetros de Hola para su entorno.</span><span class="sxs-lookup"><span data-stu-id="2511a-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="2511a-182">Puede crear entornos enteros haciendo referencia a esta plantilla JSON.</span><span class="sxs-lookup"><span data-stu-id="2511a-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="2511a-183">También puede [generar plantillas JSON de forma manual](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o exportar una plantilla JSON de entorno toocreate Hola existente para usted.</span><span class="sxs-lookup"><span data-stu-id="2511a-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="2511a-184">Use [exportación de grupo az](/cli/azure/group#export) tooexport el recurso de grupo como sigue:</span><span class="sxs-lookup"><span data-stu-id="2511a-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="2511a-185">Este comando crea hello `myResourceGroup.json` archivo en el directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="2511a-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="2511a-186">Cuando se crea un entorno de esta plantilla, le pediremos todos los nombres de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="2511a-187">Puede rellenar estos nombres en el archivo de plantilla mediante la adición de hello `--include-parameter-default-value` toohello parámetro `az group export` comando.</span><span class="sxs-lookup"><span data-stu-id="2511a-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="2511a-188">Editar los nombres de recursos JSON plantilla toospecify hello, o [crear un archivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica los nombres de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2511a-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="2511a-189">un entorno a partir de la plantilla, utilice toocreate [Crear implementación de grupo az](/cli/azure/group/deployment#create) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="2511a-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="2511a-190">Es recomendable tooread [más información acerca de cómo toodeploy de plantillas de](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2511a-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2511a-191">Obtenga información acerca de cómo usar el archivo de parámetros de hello tooincrementally entornos de actualización y tener acceso a plantillas desde una sola ubicación de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="2511a-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2511a-192">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2511a-192">Next steps</span></span>
<span data-ttu-id="2511a-193">Ahora está listo toobegin trabajar con varios componentes de red y máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="2511a-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="2511a-194">Puede usar este toobuild de entorno de ejemplo horizontalmente la aplicación con los componentes principales de hello introducidos aquí.</span><span class="sxs-lookup"><span data-stu-id="2511a-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
