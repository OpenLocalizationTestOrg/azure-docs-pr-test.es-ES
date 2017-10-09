---
title: aaaCreate una red virtual con Hola 1.0 de CLI de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate una red virtual con Hola 1.0 de CLI de Azure | Administrador de recursos."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="cc10b-103">Crear una red virtual con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="cc10b-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="cc10b-104">Azure cuenta con dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="cc10b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="cc10b-105">Microsoft recomienda crear recursos a través del modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc10b-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="cc10b-106">Obtenga más información sobre toolearn Hola diferencias entre Hola dos modelos, leer hello [modelos de implementación de Azure comprender](../azure-resource-manager/resource-manager-deployment-model.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="cc10b-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cc10b-107">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="cc10b-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="cc10b-108">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="cc10b-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="cc10b-109">[Azure 2.0 CLI](virtual-networks-create-vnet-arm-cli.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="cc10b-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="cc10b-110">[Azure 1.0 de CLI](#create-a-virtual-network) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="cc10b-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="cc10b-111">Crear una red virtual</span><span class="sxs-lookup"><span data-stu-id="cc10b-111">Create a virtual network</span></span>

<span data-ttu-id="cc10b-112">toocreate una red virtual con Hola CLI de Azure, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="cc10b-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="cc10b-113">Instalar y configurar Hola CLI de Azure por hello siguiente pasos en hello [instalar y configurar hello Azure CLI](../cli-install-nodejs.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="cc10b-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="cc10b-114">Creación de una red virtual y una subred:</span><span class="sxs-lookup"><span data-stu-id="cc10b-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="cc10b-115">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="cc10b-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="cc10b-116">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="cc10b-116">Parameters used:</span></span>

   * <span data-ttu-id="cc10b-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-117">**--vnet**.</span></span> <span data-ttu-id="cc10b-118">Nombre de hello toobe de red virtual creado.</span><span class="sxs-lookup"><span data-stu-id="cc10b-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="cc10b-119">En este escenario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="cc10b-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="cc10b-120">**-e (o --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="cc10b-121">Espacio de direcciones de red virtual.</span><span class="sxs-lookup"><span data-stu-id="cc10b-121">VNet address space.</span></span> <span data-ttu-id="cc10b-122">En este escenario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="cc10b-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="cc10b-123">**-i (o -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="cc10b-124">Máscara de red en formato CIDR.</span><span class="sxs-lookup"><span data-stu-id="cc10b-124">Network mask in CIDR format.</span></span> <span data-ttu-id="cc10b-125">En este escenario, *16*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="cc10b-126">**-n (o --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="cc10b-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="cc10b-127">Nombre de la primera subred de Hola.</span><span class="sxs-lookup"><span data-stu-id="cc10b-127">Name of hello first subnet.</span></span> <span data-ttu-id="cc10b-128">En este escenario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="cc10b-129">**-p (or --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="cc10b-130">Dirección IP inicial de la subred o el espacio de direcciones de la subred.</span><span class="sxs-lookup"><span data-stu-id="cc10b-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="cc10b-131">En este escenario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="cc10b-132">**-r (o --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="cc10b-133">Máscara de red en formato CIDR para subred.</span><span class="sxs-lookup"><span data-stu-id="cc10b-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="cc10b-134">En este escenario, *24*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="cc10b-135">**-l (o --location)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-135">**-l (or --location)**.</span></span> <span data-ttu-id="cc10b-136">Región de Azure donde se crea Hola red virtual.</span><span class="sxs-lookup"><span data-stu-id="cc10b-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="cc10b-137">En este escenario, *Central US*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="cc10b-138">Creación de una subred:</span><span class="sxs-lookup"><span data-stu-id="cc10b-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="cc10b-139">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="cc10b-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="cc10b-140">Parámetros usados:</span><span class="sxs-lookup"><span data-stu-id="cc10b-140">Parameters used:</span></span>

   * <span data-ttu-id="cc10b-141">**-t (o --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="cc10b-142">Nombre de red virtual donde se creará la subred de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="cc10b-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="cc10b-143">En este escenario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="cc10b-144">**-n (o --name)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-144">**-n (or --name)**.</span></span> <span data-ttu-id="cc10b-145">Nombre de subred nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="cc10b-145">Name of hello new subnet.</span></span> <span data-ttu-id="cc10b-146">En este escenario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="cc10b-147">**-a (or --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="cc10b-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="cc10b-148">Bloque CIDR de subred.</span><span class="sxs-lookup"><span data-stu-id="cc10b-148">Subnet CIDR block.</span></span> <span data-ttu-id="cc10b-149">En este escenario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="cc10b-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="cc10b-150">propiedades de hello tooview de Hola nueva red virtual:</span><span class="sxs-lookup"><span data-stu-id="cc10b-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="cc10b-151">Resultado esperado:</span><span class="sxs-lookup"><span data-stu-id="cc10b-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="cc10b-152">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc10b-152">Next steps</span></span>

<span data-ttu-id="cc10b-153">Obtenga información acerca de cómo tooconnect:</span><span class="sxs-lookup"><span data-stu-id="cc10b-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="cc10b-154">Una red virtual de máquina virtual (VM) tooa leyendo hello [crear una VM Linux](../virtual-machines/linux/quick-create-cli.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="cc10b-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="cc10b-155">En lugar de crear una red virtual y la subred en los pasos de Hola de artículos de hello, puede seleccionar una red virtual existente y la subred tooconnect una máquina virtual a.</span><span class="sxs-lookup"><span data-stu-id="cc10b-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="cc10b-156">Hola redes virtuales de red virtual tooother leyendo hello [conectar redes virtuales](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="cc10b-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="cc10b-157">Hola tooan de red virtual local de la red mediante una red privada virtual (VPN) de sitio a sitio o el circuito de ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="cc10b-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="cc10b-158">Obtenga información acerca de cómo leyendo hello [conectar una red de red virtual tooan local mediante una VPN de sitio a sitio](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) y [vincular un circuito de ExpressRoute de red virtual tooan](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cc10b-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
