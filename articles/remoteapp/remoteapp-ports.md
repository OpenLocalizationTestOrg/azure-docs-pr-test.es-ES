---
title: Lista de puertos y direcciones URL que se deben incluir en la lista blanca de Azure RemoteApp implementada en la red virtual de cliente | Microsoft Docs
description: "Obtenga información sobre qué puertos y direcciones URL tendrá que configurar para la comunicación a través de Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="f9cdc-103">Lista de puertos y direcciones URL para permitir el acceso a Azure RemoteApp implementada en el cliente de red virtual</span><span class="sxs-lookup"><span data-stu-id="f9cdc-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f9cdc-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f9cdc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f9cdc-105">Para obtener más información, lea el [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="f9cdc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f9cdc-106">Si va a implementar una nube de Azure RemoteApp o una colección híbrida en una red virtual (VNET), consulte la siguiente información sobre puertos.</span><span class="sxs-lookup"><span data-stu-id="f9cdc-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="f9cdc-107">Para obtener más información sobre las redes virtuales, consulte la [información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9cdc-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="f9cdc-108">Si creó un grupo de seguridad de red (NSG) que restringe el tráfico dirigido a los recursos de red virtual de su colección, asegúrese de que los siguientes puertos sean accesibles y estén permitidos en las directivas de seguridad de la red virtual.</span><span class="sxs-lookup"><span data-stu-id="f9cdc-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="f9cdc-109">Para obtener más información sobre los grupos de seguridad de red, consulte el artículo sobre [qué es un grupo de seguridad de red. (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f9cdc-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="f9cdc-110">La subred de Azure RemoteApp necesita acceso a estos puntos de conexión y direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="f9cdc-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="f9cdc-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9cdc-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="f9cdc-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="f9cdc-112">*.servicebus.net</span></span>
* <span data-ttu-id="f9cdc-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f9cdc-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="f9cdc-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f9cdc-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9cdc-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="f9cdc-117">Saliente: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="f9cdc-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="f9cdc-118">Opcional. UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="f9cdc-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="f9cdc-119">Los clientes Azure RemoteApp necesitan acceso a estos puntos de conexión y direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="f9cdc-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="f9cdc-120">Por clientes, me refiero a los escritorios, dispositivos etc. que los usuarios usan para conectarse a las aplicaciones implementadas en la colección de Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="f9cdc-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="f9cdc-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f9cdc-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span><span class="sxs-lookup"><span data-stu-id="f9cdc-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="f9cdc-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9cdc-123">https://login.windows.net</span></span>  
* <span data-ttu-id="f9cdc-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="f9cdc-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f9cdc-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="f9cdc-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f9cdc-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="f9cdc-127">Saliente: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="f9cdc-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="f9cdc-128">Opcional: UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="f9cdc-128">Optional - UDP: 3391</span></span> 

