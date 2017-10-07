---
title: aaaCreate una red virtual - 2.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red virtual con Hola 2.0 de CLI de Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="f4f89-103">Crear una red virtual con hello 2.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="f4f89-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="f4f89-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="f4f89-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f4f89-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f89-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f4f89-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f4f89-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f4f89-107">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="f4f89-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f4f89-108">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="f4f89-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f4f89-109">[Azure 1.0 de CLI](virtual-networks-create-vnet-cli-nodejs.md) – nuestro CLI para modelos de implementación de administración de recursos y clásico Hola</span><span class="sxs-lookup"><span data-stu-id="f4f89-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="f4f89-110">[Azure 2.0 CLI](#create-a-virtual-network) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de hello (en este artículo)'</span><span class="sxs-lookup"><span data-stu-id="f4f89-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="f4f89-111">También puede crear una red virtual mediante el Administrador de recursos con otras herramientas o crear una red virtual a través del modelo de implementación clásica de hello seleccionando una opción diferente de hello lista siguiente:</span><span class="sxs-lookup"><span data-stu-id="f4f89-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4f89-112">Portal</span><span class="sxs-lookup"><span data-stu-id="f4f89-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="f4f89-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4f89-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="f4f89-114">CLI</span><span class="sxs-lookup"><span data-stu-id="f4f89-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="f4f89-115">Plantilla</span><span class="sxs-lookup"><span data-stu-id="f4f89-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="f4f89-116">Portal (clásico)</span><span class="sxs-lookup"><span data-stu-id="f4f89-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="f4f89-117">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="f4f89-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="f4f89-118">CLI (clásico)</span><span class="sxs-lookup"><span data-stu-id="f4f89-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="f4f89-119">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="f4f89-119">Create a virtual network</span></span>

<span data-ttu-id="f4f89-120">toocreate una red virtual con Hola CLI de Azure 2.0, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="f4f89-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="f4f89-121">Instalar y configurar hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f4f89-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="f4f89-122">Crear un grupo de recursos para una red virtual con hello [crear grupo az](/cli/azure/group#create) comando con hello `--name` y `--location` argumentos:</span><span class="sxs-lookup"><span data-stu-id="f4f89-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="f4f89-123">Creación de una red virtual y una subred:</span><span class="sxs-lookup"><span data-stu-id="f4f89-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="f4f89-124">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f4f89-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="f4f89-125">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="f4f89-125">Parameters used:</span></span>

    - <span data-ttu-id="f4f89-126">`--name TestVNet`: Nombre de hello toobe de red virtual creado.</span><span class="sxs-lookup"><span data-stu-id="f4f89-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="f4f89-127">`--resource-group TestRG`: nombre de grupo de recursos de Hola de # que controla el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f89-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="f4f89-128">`--location centralus`: Hola ubicación en que toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f4f89-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="f4f89-129">`--address-prefix 192.168.0.0/16`: Hola prefijo de dirección y el bloque.</span><span class="sxs-lookup"><span data-stu-id="f4f89-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="f4f89-130">`--subnet-name FrontEnd`: nombre de Hola de subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f89-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="f4f89-131">`--subnet-prefix 192.168.1.0/24`: Hola prefijo de dirección y el bloque.</span><span class="sxs-lookup"><span data-stu-id="f4f89-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="f4f89-132">toolist toouse de información básica de Hola Hola comando a continuación, puede realizar consultas Hola red virtual con un [filtro de consulta](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="f4f89-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="f4f89-133">Lo que produce Hola después de salida:</span><span class="sxs-lookup"><span data-stu-id="f4f89-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="f4f89-134">Creación de una subred:</span><span class="sxs-lookup"><span data-stu-id="f4f89-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="f4f89-135">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f4f89-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="f4f89-136">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="f4f89-136">Parameters used:</span></span>

    - <span data-ttu-id="f4f89-137">`--address-prefix 192.168.2.0/24`: el bloque CIDR de subred.</span><span class="sxs-lookup"><span data-stu-id="f4f89-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="f4f89-138">`--name BackEnd`: Nombre de subred nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f89-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="f4f89-139">`--resource-group TestRG`: grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4f89-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="f4f89-140">`--vnet-name TestVNet`: nombre de Hola de hello propietaria de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f4f89-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="f4f89-141">Propiedades de Hola de consulta de Hola nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="f4f89-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="f4f89-142">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f4f89-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="f4f89-143">Consultar propiedades de Hola de subredes de hello:</span><span class="sxs-lookup"><span data-stu-id="f4f89-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="f4f89-144">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="f4f89-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="f4f89-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4f89-145">Next steps</span></span>

<span data-ttu-id="f4f89-146">Obtenga información acerca de cómo tooconnect:</span><span class="sxs-lookup"><span data-stu-id="f4f89-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="f4f89-147">Una red virtual de máquina virtual (VM) tooa leyendo hello [crear una VM Linux](../virtual-machines/linux/quick-create-cli.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f4f89-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="f4f89-148">En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.</span><span class="sxs-lookup"><span data-stu-id="f4f89-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="f4f89-149">Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="f4f89-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="f4f89-150">Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f4f89-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="f4f89-151">Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f4f89-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
