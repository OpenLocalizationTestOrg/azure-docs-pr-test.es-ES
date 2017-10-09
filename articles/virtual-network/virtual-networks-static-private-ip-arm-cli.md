---
title: "aaaConfigure de direcciones IP privadas para las máquinas virtuales - 2.0 de CLI de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure de direcciones IP privadas de máquinas virtuales mediante hello Azure interfaz de línea de comandos (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="34eec-103">Configurar las direcciones IP privadas para una máquina virtual mediante Hola 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="34eec-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="34eec-104">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="34eec-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="34eec-105">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="34eec-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="34eec-106">[Azure 1.0 de CLI](virtual-networks-static-private-ip-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="34eec-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="34eec-107">[Azure 2.0 CLI](#specify-a-static-private-ip-address-when-creating-a-vm) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="34eec-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="34eec-108">Este artículo trata el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="34eec-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="34eec-109">También puede [administrar dirección IP privada estática en el modelo de implementación clásica de hello](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="34eec-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="34eec-110">comandos de CLI de Azure 2.0 de ejemplo de Hola a continuación esperan un entorno simple ya creado.</span><span class="sxs-lookup"><span data-stu-id="34eec-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="34eec-111">Si desea toorun comandos de hello, que se muestran en este documento, en primer lugar crear entorno de prueba de Hola se describe en [crear una red virtual](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="34eec-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="34eec-112">Especificación de una dirección IP privada estática al crear una VM</span><span class="sxs-lookup"><span data-stu-id="34eec-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="34eec-113">una máquina virtual denominada toocreate *DNS01* en hello *front-end* subred de una red virtual denominada *TestVNet* con una dirección IP estática privada de *192.168.1.101*, Siga los pasos de hello siguientes:</span><span class="sxs-lookup"><span data-stu-id="34eec-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="34eec-114">Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="34eec-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="34eec-115">Crear una dirección IP pública para hello VM con hello [crear az red public-ip](/cli/azure/network/public-ip#create) comando.</span><span class="sxs-lookup"><span data-stu-id="34eec-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="34eec-116">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="34eec-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="34eec-117">Puede quiere o necesita toouse valores diferentes para los argumentos de esta y pasos siguientes, dependiendo de su entorno.</span><span class="sxs-lookup"><span data-stu-id="34eec-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="34eec-118">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="34eec-119">`--resource-group`: Nombre del grupo de recursos de hello en qué dirección IP pública de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="34eec-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="34eec-120">`--name`: Nombre de la dirección IP pública de Hola.</span><span class="sxs-lookup"><span data-stu-id="34eec-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="34eec-121">`--location`: Región azure en qué dirección IP pública de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="34eec-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="34eec-122">Ejecute hello [crear nic de red az](/cli/azure/network/nic#create) comando toocreate una NIC con una dirección IP estática privada.</span><span class="sxs-lookup"><span data-stu-id="34eec-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="34eec-123">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="34eec-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="34eec-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="34eec-125">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="34eec-125">Parameters:</span></span>

    * <span data-ttu-id="34eec-126">`--private-ip-address`: Dirección IP privada estática para hello NIC.</span><span class="sxs-lookup"><span data-stu-id="34eec-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="34eec-127">`--vnet-name`: Nombre de red virtual de hello en qué toocreate Hola NIC.</span><span class="sxs-lookup"><span data-stu-id="34eec-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="34eec-128">`--subnet`: Nombre de subred de hello en qué hello toocreate NIC.</span><span class="sxs-lookup"><span data-stu-id="34eec-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="34eec-129">Ejecute hello [crear la máquina virtual de azure](/cli/azure/vm/nic#create) comando toocreate hello máquina virtual con la dirección IP pública de Hola y formación creada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="34eec-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="34eec-130">lista de Hola que se muestra después de la salida de hello explica parámetros Hola utilizados.</span><span class="sxs-lookup"><span data-stu-id="34eec-130">hello list shown after hello output explains hello parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="34eec-131">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="34eec-132">Parámetros que no sean de hello básico [crear vm az](/cli/azure/vm#create) parámetros.</span><span class="sxs-lookup"><span data-stu-id="34eec-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="34eec-133">`--nics`: Nombre del programa Hola toowhich a Hola NIC virtual está conectado.</span><span class="sxs-lookup"><span data-stu-id="34eec-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="34eec-134">Recuperación de la información de la dirección IP privada estática para una VM</span><span class="sxs-lookup"><span data-stu-id="34eec-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="34eec-135">tooview Hola privada dirección IP estática que ha creado, ejecute hello siguiente comando de CLI de Azure y observar los valores de hello para *IP privada alloc (método)* y *dirección IP privada*:</span><span class="sxs-lookup"><span data-stu-id="34eec-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="34eec-136">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="34eec-137">toodisplay Hola información específica de IP de hello NIC para esa máquina virtual, Hola consulta NIC específicamente:</span><span class="sxs-lookup"><span data-stu-id="34eec-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="34eec-138">salida de Hello es similar:</span><span class="sxs-lookup"><span data-stu-id="34eec-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="34eec-139">Eliminación de una dirección IP privada estática de una VM</span><span class="sxs-lookup"><span data-stu-id="34eec-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="34eec-140">No se puede eliminar una dirección IP privada estática de una NIC en la CLI de Azure para implementaciones de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="34eec-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="34eec-141">Debe:</span><span class="sxs-lookup"><span data-stu-id="34eec-141">You must:</span></span>
- <span data-ttu-id="34eec-142">Crear una nueva NIC que use una dirección IP dinámica.</span><span class="sxs-lookup"><span data-stu-id="34eec-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="34eec-143">Establecer Hola NIC en Hola Hola VM recién creado NIC.</span><span class="sxs-lookup"><span data-stu-id="34eec-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="34eec-144">Hola toochange NIC para hello máquina virtual que se utiliza en los comandos de hello anteriores, siga los pasos de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="34eec-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="34eec-145">Ejecute hello **crear nic de red de azure** comando toocreate una NIC nuevo mediante la asignación de IP dinámica con una nueva dirección IP.</span><span class="sxs-lookup"><span data-stu-id="34eec-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="34eec-146">Tenga en cuenta que dado que no se especifica ninguna dirección IP, método de asignación de hello **dinámica**.</span><span class="sxs-lookup"><span data-stu-id="34eec-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="34eec-147">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="34eec-148">Ejecute hello **conjunto de máquina virtual de azure** comando toochange hello NIC que se utiliza por hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="34eec-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="34eec-149">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="34eec-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="34eec-150">Si Hola VM es lo suficientemente grande como toohave más de una NIC, ejecute hello **nic de red de azure eliminar** comando toodelete Hola antigua NIC</span><span class="sxs-lookup"><span data-stu-id="34eec-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="34eec-151">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="34eec-151">Next steps</span></span>
* <span data-ttu-id="34eec-152">Obtenga más información acerca de las [direcciones IP públicas reservadas](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="34eec-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="34eec-153">Obtenga información sobre las [direcciones IP públicas a nivel de instancia (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="34eec-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="34eec-154">Consulte hello [API de REST para IP reservadas](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="34eec-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

