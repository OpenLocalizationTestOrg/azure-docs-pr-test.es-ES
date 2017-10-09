---
title: aaaCreate de red de grupos de seguridad - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar grupos de seguridad de red mediante Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="e2abc-103">Crear grupos de seguridad mediante Azure CLI 2.0 Hola de red</span><span class="sxs-lookup"><span data-stu-id="e2abc-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e2abc-104">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="e2abc-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="e2abc-105">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="e2abc-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="e2abc-106">[Azure 1.0 de CLI](virtual-networks-create-nsg-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="e2abc-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="e2abc-107">[Azure 2.0 CLI](#Create-the-nsg-for-the-front-end-subnet) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="e2abc-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="e2abc-108">ejemplo de Hola a Azure CLI 2.0 comandos siguiente espera un entorno simple ya creado basándose en el escenario de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="e2abc-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="e2abc-109">Crear hello NSG para hello `FrontEnd` subred</span><span class="sxs-lookup"><span data-stu-id="e2abc-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="e2abc-110">toocreate un NSG denominado *NSG-front-end* según Hola escenario anterior, siga el siguiente de pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="e2abc-111">Si aún no lo ha aún, instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e2abc-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="e2abc-112">Crear un NSG con hello [crear az red nsg](/cli/azure/network/nsg#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="e2abc-113">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="e2abc-113">Parameters:</span></span>
   
   * <span data-ttu-id="e2abc-114">`--resource-group`: Nombre del grupo de recursos de Hola donde se crea hello NSG.</span><span class="sxs-lookup"><span data-stu-id="e2abc-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="e2abc-115">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="e2abc-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="e2abc-116">`--location`: Región azure donde hello nuevo NSG se crea.</span><span class="sxs-lookup"><span data-stu-id="e2abc-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="e2abc-117">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="e2abc-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="e2abc-118">`--name`: Nombre Hola nuevo NSG.</span><span class="sxs-lookup"><span data-stu-id="e2abc-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="e2abc-119">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="e2abc-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="e2abc-120">Hola espera el resultado es un poco de información, incluida una lista de todas las reglas predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="e2abc-121">Hello en el ejemplo siguiente se muestra las reglas predeterminadas de hello con un filtro de consulta JMESPATH hello `table` formato de salida:</span><span class="sxs-lookup"><span data-stu-id="e2abc-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="e2abc-122">Salida:</span><span class="sxs-lookup"><span data-stu-id="e2abc-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="e2abc-123">Crear una regla que permita acceso tooport 3389 (RDP) de hello Internet con hello [crear regla de nsg de red az](/cli/azure/network/nsg/rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="e2abc-124">Función que usa el shell de hello, podría necesitar hello toomodify `*` caracteres en argumentos de hello después de modo que no tooexpand Hola argumento antes de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="e2abc-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="e2abc-125">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="e2abc-126">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="e2abc-126">Parameters:</span></span>

    * <span data-ttu-id="e2abc-127">`--resource-group testrg`: Hola toouse de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2abc-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="e2abc-128">Tenga en cuenta que distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e2abc-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="e2abc-129">`--nsg-name NSG-FrontEnd`: Nombre del NSG de hello en qué Hola se crea la regla.</span><span class="sxs-lookup"><span data-stu-id="e2abc-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="e2abc-130">`--name rdp-rule`: Nombre de nueva regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="e2abc-131">`--access Allow`: Nivel de acceso para reglas de hello (denegar o permitir).</span><span class="sxs-lookup"><span data-stu-id="e2abc-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="e2abc-132">`--protocol Tcp`: protocolo (TCP, UDP o *).</span><span class="sxs-lookup"><span data-stu-id="e2abc-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="e2abc-133">`--direction Inbound`: Dirección de conexión de hello (entrante o saliente).</span><span class="sxs-lookup"><span data-stu-id="e2abc-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="e2abc-134">`--priority 100`: Prioridad de regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="e2abc-135">`--source-address-prefix Internet`: prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e2abc-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="e2abc-136">`--source-port-range "*"`: puerto de origen o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="e2abc-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="e2abc-137">Puerto que abre la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="e2abc-138">`--destination-address-prefix "*"`: prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e2abc-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="e2abc-139">`--destination-port-range 3389`: puerto de destino o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="e2abc-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="e2abc-140">Puerto que recibe la solicitud de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="e2abc-141">Crear una regla que permita acceso tooport 80 (HTTP) de hello Internet **crear regla de nsg de red az** comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="e2abc-142">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="e2abc-143">Enlazar hello NSG toohello **front-end** subred con hello [actualización de subred de red virtual de red az](/cli/azure/network/vnet/subnet#update) comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="e2abc-144">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="e2abc-145">Crear hello NSG para hello `BackEnd` subred</span><span class="sxs-lookup"><span data-stu-id="e2abc-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="e2abc-146">toocreate un NSG denominado *back-end de NSG* en función en escenario de hello anterior, siga los siguientes pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2abc-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="e2abc-147">Crear hello `NSG-BackEnd` NSG con **crear az red nsg**.</span><span class="sxs-lookup"><span data-stu-id="e2abc-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="e2abc-148">Como en el paso 2, anterior, Hola espera salida es bastante grande, incluidas las reglas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="e2abc-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="e2abc-149">Crear una regla que permita acceso tooport 1433 (SQL) de hello `FrontEnd` subred con hello **crear regla de nsg de red az** comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="e2abc-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="e2abc-151">Crear una regla que deniegue el acceso a toohello Internet mediante hello **crear regla de nsg de red az** comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="e2abc-152">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="e2abc-153">Enlazar hello NSG toohello `BackEnd` subred usando hello **conjunto de subredes de red virtual de red az** comando.</span><span class="sxs-lookup"><span data-stu-id="e2abc-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="e2abc-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="e2abc-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
