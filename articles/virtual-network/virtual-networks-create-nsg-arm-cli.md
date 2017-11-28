---
title: "Creación de grupos de seguridad de red: CLI de Azure 2.0 | Microsoft Docs"
description: Aprenda a crear e implementar grupos de seguridad de red mediante la CLI de Azure 2.0.
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
ms.openlocfilehash: 8efb3ab66d07875b51f723fed5594bcb477ed025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-20"></a><span data-ttu-id="693ff-103">Creación de grupos de seguridad de red con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="693ff-103">Create network security groups using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="693ff-104">Versiones de la CLI para completar la tarea</span><span class="sxs-lookup"><span data-stu-id="693ff-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="693ff-105">Puede completar la tarea mediante una de las siguientes versiones de la CLI:</span><span class="sxs-lookup"><span data-stu-id="693ff-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="693ff-106">[CLI de Azure 1.0](virtual-networks-create-nsg-cli-nodejs.md): la CLI para los modelos de implementación clásico y de Resource Manager</span><span class="sxs-lookup"><span data-stu-id="693ff-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="693ff-107">[CLI de Azure 2.0](#Create-the-nsg-for-the-front-end-subnet): la CLI de última generación para el modelo de implementación de administración de recursos (este artículo).</span><span class="sxs-lookup"><span data-stu-id="693ff-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="693ff-108">En los siguientes comandos de CLI de Azure 2.0 de ejemplo se presupone que ya se ha creado un entorno simple según el escenario anterior.</span><span class="sxs-lookup"><span data-stu-id="693ff-108">The sample Azure CLI 2.0 commands following expect a simple environment already created based on the scenario preceding.</span></span> 

## <a name="create-the-nsg-for-the-frontend-subnet"></a><span data-ttu-id="693ff-109">Creación del grupo de seguridad de red para la subred `FrontEnd`</span><span class="sxs-lookup"><span data-stu-id="693ff-109">Create the NSG for the `FrontEnd` subnet</span></span>

<span data-ttu-id="693ff-110">Para crear un grupo de seguridad de red denominado *NSG-FrontEnd* según el escenario anterior, siga los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="693ff-110">To create an NSG named *NSG-FrontEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="693ff-111">Si todavía no lo ha hecho, instale y configure la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="693ff-111">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="693ff-112">Cree un grupo de seguridad de red con el comando [azure network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="693ff-112">Create an NSG using the [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="693ff-113">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="693ff-113">Parameters:</span></span>
   
   * <span data-ttu-id="693ff-114">`--resource-group`: nombre del grupo de recursos donde se crea el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="693ff-114">`--resource-group`: Name of the resource group where the NSG is created.</span></span> <span data-ttu-id="693ff-115">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="693ff-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="693ff-116">`--location`: región de Azure donde se crea el grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="693ff-116">`--location`: Azure region where the new NSG is created.</span></span> <span data-ttu-id="693ff-117">En este escenario, *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="693ff-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="693ff-118">`--name`: nombre del nuevo grupo de seguridad de red.</span><span class="sxs-lookup"><span data-stu-id="693ff-118">`--name`: Name for the new NSG.</span></span> <span data-ttu-id="693ff-119">En este escenario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="693ff-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="693ff-120">La salida esperada es una gran cantidad de información, incluida una lista de todas las reglas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="693ff-120">The expected output is quite a bit of information including a list of all the default rules.</span></span> <span data-ttu-id="693ff-121">En el ejemplo siguiente se muestran las reglas predeterminadas mediante un filtro de consulta JMESPATH con el formato de salida `table`:</span><span class="sxs-lookup"><span data-stu-id="693ff-121">The following example shows the default rules using a JMESPATH query filter with the `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="693ff-122">Salida:</span><span class="sxs-lookup"><span data-stu-id="693ff-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs to all VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs to Internet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="693ff-123">Cree una regla que permita el acceso al puerto 3389 (RDP) desde Internet con el comando [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="693ff-123">Create a rule that allows access to port 3389 (RDP) from the Internet with the [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="693ff-124">Según el shell que esté usando, tendrá que modificar el carácter `*` en los argumentos siguientes para que no se expanda el argumento antes de la ejecución.</span><span class="sxs-lookup"><span data-stu-id="693ff-124">Depending on the shell you are using, you might need to modify the `*` character in the arguments following so as not to expand the argument before execution.</span></span>
   
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
   
    <span data-ttu-id="693ff-125">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-125">Expected output:</span></span>
   
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

    <span data-ttu-id="693ff-126">Parámetros:</span><span class="sxs-lookup"><span data-stu-id="693ff-126">Parameters:</span></span>

    * <span data-ttu-id="693ff-127">`--resource-group testrg`: el grupo de recursos que se va a usar.</span><span class="sxs-lookup"><span data-stu-id="693ff-127">`--resource-group testrg`: The resource group to use.</span></span> <span data-ttu-id="693ff-128">Tenga en cuenta que distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="693ff-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="693ff-129">`--nsg-name NSG-FrontEnd`: nombre del grupo de seguridad de red en el que se crea la regla.</span><span class="sxs-lookup"><span data-stu-id="693ff-129">`--nsg-name NSG-FrontEnd`: Name of the NSG in which the rule is created.</span></span>
    * <span data-ttu-id="693ff-130">`--name rdp-rule`: nombre de la nueva regla.</span><span class="sxs-lookup"><span data-stu-id="693ff-130">`--name rdp-rule`: Name for the new rule.</span></span>
    * <span data-ttu-id="693ff-131">`--access Allow`: nivel de acceso de la regla (Denegar o Permitir).</span><span class="sxs-lookup"><span data-stu-id="693ff-131">`--access Allow`: Access level for the rule (Deny or Allow).</span></span>
    * <span data-ttu-id="693ff-132">`--protocol Tcp`: protocolo (TCP, UDP o *).</span><span class="sxs-lookup"><span data-stu-id="693ff-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="693ff-133">`--direction Inbound`: dirección de conexión (Entrante o Saliente).</span><span class="sxs-lookup"><span data-stu-id="693ff-133">`--direction Inbound`: Direction of the connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="693ff-134">`--priority 100`: prioridad de la regla.</span><span class="sxs-lookup"><span data-stu-id="693ff-134">`--priority 100`: Priority for the rule.</span></span>
    * <span data-ttu-id="693ff-135">`--source-address-prefix Internet`: prefijo de dirección de origen en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="693ff-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="693ff-136">`--source-port-range "*"`: puerto de origen o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="693ff-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="693ff-137">Puerto que ha abierto la conexión.</span><span class="sxs-lookup"><span data-stu-id="693ff-137">Port that opened the connection.</span></span>
    * <span data-ttu-id="693ff-138">`--destination-address-prefix "*"`: prefijo de dirección de destino en CIDR o con las etiquetas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="693ff-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="693ff-139">`--destination-port-range 3389`: puerto de destino o intervalo de puertos.</span><span class="sxs-lookup"><span data-stu-id="693ff-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="693ff-140">Puerto que recibe la solicitud de conexión.</span><span class="sxs-lookup"><span data-stu-id="693ff-140">Port that receives the connection request.</span></span>



4. <span data-ttu-id="693ff-141">Cree una regla que permita el acceso al puerto 80 (HTTP) desde Internet con el comando **az network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="693ff-141">Create a rule that allows access to port 80 (HTTP) from the Internet **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="693ff-142">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-142">Expected putput:</span></span>
   
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

5. <span data-ttu-id="693ff-143">Enlace el grupo de seguridad de red a la subred **FrontEnd** con el comando [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span><span class="sxs-lookup"><span data-stu-id="693ff-143">Bind the NSG to the **FrontEnd** subnet with the [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="693ff-144">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-144">Expected output:</span></span>
   
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

## <a name="create-the-nsg-for-the-backend-subnet"></a><span data-ttu-id="693ff-145">Creación del grupo de seguridad de red para la subred `BackEnd`</span><span class="sxs-lookup"><span data-stu-id="693ff-145">Create the NSG for the `BackEnd` subnet</span></span>
<span data-ttu-id="693ff-146">Para crear un grupo de seguridad de red denominado *NSG-BackEnd* según el escenario anterior, siga los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="693ff-146">To create an NSG named *NSG-BackEnd* based on the scenario preceding, follow the steps following.</span></span>

1. <span data-ttu-id="693ff-147">Cree el grupo de seguridad de red `NSG-BackEnd` con el comando **az network nsg create**.</span><span class="sxs-lookup"><span data-stu-id="693ff-147">Create the `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="693ff-148">Como en el paso 2 anterior, la salida esperada es bastante grande, incluidas las reglas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="693ff-148">As in step 2, preceding, the expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="693ff-149">Cree una regla que permita el acceso al puerto 1433 (SQL) desde la subred `FrontEnd` con el comando **az network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="693ff-149">Create a rule that allows access to port 1433 (SQL) from the `FrontEnd` subnet with the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="693ff-150">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-150">Expected output:</span></span>

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

3. <span data-ttu-id="693ff-151">Cree una regla que deniegue el acceso a Internet mediante el comando **az network nsg rule create**.</span><span class="sxs-lookup"><span data-stu-id="693ff-151">Create a rule that denies access to the Internet using the **az network nsg rule create** command.</span></span>
   
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
   
    <span data-ttu-id="693ff-152">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-152">Expected putput:</span></span>
   
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

4. <span data-ttu-id="693ff-153">Vincule el grupo de seguridad de red a la subred `BackEnd` mediante el comando **az network vnet subnet update**.</span><span class="sxs-lookup"><span data-stu-id="693ff-153">Bind the NSG to the `BackEnd` subnet using the **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="693ff-154">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="693ff-154">Expected output:</span></span>
   
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
