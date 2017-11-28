---
title: "Eliminación de una puerta de enlace de red virtual: Azure Portal y Azure Resource Manager | Microsoft Docs"
description: "Elimine una puerta de enlace de red virtual mediante Azure Portal en el modelo de implementación de Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 1d289c09465cb8d5e4bfa569441dffcbf562b3bf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="c9f35-103">Eliminación de una puerta de enlace de red virtual mediante el portal</span><span class="sxs-lookup"><span data-stu-id="c9f35-103">Delete a virtual network gateway using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9f35-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c9f35-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="c9f35-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c9f35-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="c9f35-106">PowerShell (clásico)</span><span class="sxs-lookup"><span data-stu-id="c9f35-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)

<span data-ttu-id="c9f35-107">Hay un par de enfoques que puede adoptar cuando desee eliminar una puerta de enlace de red virtual correspondiente a una configuración de puerta de enlace VPN.</span><span class="sxs-lookup"><span data-stu-id="c9f35-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="c9f35-108">Si quiere eliminar todo el contenido y volver a empezar, como en el caso de un entorno de prueba, puede eliminar el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9f35-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="c9f35-109">Cuando se elimina un grupo de recursos, se quitan todos los recursos de él.</span><span class="sxs-lookup"><span data-stu-id="c9f35-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="c9f35-110">Este método solo se recomienda si no desea conservar los recursos del grupo en cuestión.</span><span class="sxs-lookup"><span data-stu-id="c9f35-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="c9f35-111">Con este enfoque no podrá eliminar de forma selectiva solo unos pocos recursos.</span><span class="sxs-lookup"><span data-stu-id="c9f35-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="c9f35-112">Si desea mantener algunos de los recursos en el grupo de recursos, será algo más complicado eliminar una puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c9f35-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="c9f35-113">Antes de poder eliminar la puerta de enlace de red virtual, primero debe quitar todos los recursos que dependen de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c9f35-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="c9f35-114">Los pasos que seguirá dependerán del tipo de conexiones que creó y de los recursos dependientes de cada conexión.</span><span class="sxs-lookup"><span data-stu-id="c9f35-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="delete-a-vpn-gateway"></a><span data-ttu-id="c9f35-115">Eliminación de una instancia de VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="c9f35-115">Delete a VPN gateway</span></span>

<span data-ttu-id="c9f35-116">Para eliminar una puerta de enlace de red virtual, primero debe eliminar cada recurso que pertenece a la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c9f35-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="c9f35-117">Los recursos deben eliminarse en un orden determinado debido a las dependencias.</span><span class="sxs-lookup"><span data-stu-id="c9f35-117">Resources must be deleted in a certain order due to dependencies.</span></span>

[!INCLUDE [delete gateway](../../includes/vpn-gateway-delete-vnet-gateway-portal-include.md)]

<span data-ttu-id="c9f35-118">En este punto, se elimina la puerta de enlace de red virtual.</span><span class="sxs-lookup"><span data-stu-id="c9f35-118">At this point, the virtual network gateway is deleted.</span></span> <span data-ttu-id="c9f35-119">Los pasos siguientes ayudan a eliminar todos los recursos que ya no se usan.</span><span class="sxs-lookup"><span data-stu-id="c9f35-119">The next steps help you delete any resources that are no longer being used.</span></span>

### <a name="to-delete-the-local-network-gateway"></a><span data-ttu-id="c9f35-120">Para eliminar la puerta de enlace de red local</span><span class="sxs-lookup"><span data-stu-id="c9f35-120">To delete the local network gateway</span></span>

1. <span data-ttu-id="c9f35-121">En **Todos los recursos**, busque las puertas de enlace de red local asociadas a cada conexión.</span><span class="sxs-lookup"><span data-stu-id="c9f35-121">In **All resources**, locate the local network gateways that were associated with each connection.</span></span>
2. <span data-ttu-id="c9f35-122">En la hoja **Información general** de la puerta de enlace de red local, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c9f35-122">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

### <a name="to-delete-the-public-ip-address-resource-for-the-gateway"></a><span data-ttu-id="c9f35-123">Para eliminar el recurso de dirección IP pública para la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="c9f35-123">To delete the Public IP address resource for the gateway</span></span>

1. <span data-ttu-id="c9f35-124">En **Todos los recursos**, busque el recurso de dirección IP pública que se asoció a la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c9f35-124">In **All resources**, locate the Public IP address resource that was associated to the gateway.</span></span> <span data-ttu-id="c9f35-125">Si la puerta de enlace de red virtual era activa-activa, verá dos direcciones IP públicas.</span><span class="sxs-lookup"><span data-stu-id="c9f35-125">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> 
2. <span data-ttu-id="c9f35-126">En la página **Introducción general** de la dirección IP pública, haga clic en **Eliminar** y después en **Sí** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="c9f35-126">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

### <a name="to-delete-the-gateway-subnet"></a><span data-ttu-id="c9f35-127">Para eliminar la subred de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="c9f35-127">To delete the gateway subnet</span></span>

1. <span data-ttu-id="c9f35-128">En **Todos los recursos**, busque la red virtual.</span><span class="sxs-lookup"><span data-stu-id="c9f35-128">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="c9f35-129">En la hoja **Subredes**, haga clic en el elemento **GatewaySubnet** y después en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c9f35-129">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="c9f35-130">Haga clic en **Sí** para confirmar que desea eliminar la subred de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="c9f35-130">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

## <span data-ttu-id="c9f35-131"><a name="deleterg"></a>Eliminación de una puerta de enlace VPN mediante la eliminación del grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c9f35-131"><a name="deleterg"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="c9f35-132">Si no desea mantener ninguno de los recursos del grupo, sino que desea empezar de nuevo, puede eliminar dicho grupo al completo.</span><span class="sxs-lookup"><span data-stu-id="c9f35-132">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="c9f35-133">Se trata de una forma rápida de quitarlos todos.</span><span class="sxs-lookup"><span data-stu-id="c9f35-133">This is a quick way to remove everything.</span></span> <span data-ttu-id="c9f35-134">Los siguientes pasos se aplican solo al modelo de implementación de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9f35-134">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="c9f35-135">En **Todos los recursos**, busque el grupo de recursos y haga clic para abrir la hoja.</span><span class="sxs-lookup"><span data-stu-id="c9f35-135">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="c9f35-136">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c9f35-136">Click **Delete**.</span></span> <span data-ttu-id="c9f35-137">En la hoja Eliminar, revise los recursos afectados.</span><span class="sxs-lookup"><span data-stu-id="c9f35-137">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="c9f35-138">Asegúrese de que desea eliminar todos estos recursos.</span><span class="sxs-lookup"><span data-stu-id="c9f35-138">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="c9f35-139">Si no es así, siga los pasos de [Eliminación de una puerta de enlace VPN](#deletegw) en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c9f35-139">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="c9f35-140">Para continuar, escriba el nombre del grupo de recursos que quiere eliminar y, después, haga clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="c9f35-140">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>