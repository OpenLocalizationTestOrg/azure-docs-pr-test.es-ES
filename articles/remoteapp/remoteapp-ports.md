---
title: aaaList de toowhitelist de puertos y las direcciones URL para Azure RemoteApp implementado en la red virtual de cliente | Documentos de Microsoft
description: "Obtenga información acerca de qué puertos y direcciones URL que necesitará tooconfigure para la comunicación a través de Azure RemoteApp."
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
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="f4427-103">Lista de puertos y direcciones URL de acceso de toopermit para Azure RemoteApp implementado en el cliente de red Virtual</span><span class="sxs-lookup"><span data-stu-id="f4427-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f4427-104">Azure RemoteApp dejará de estar disponible el 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="f4427-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f4427-105">Hola de lectura [anuncio](https://go.microsoft.com/fwlink/?linkid=821148) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="f4427-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f4427-106">Si va a implementar una colección de nube o híbridas de Azure RemoteApp en una red virtual (VNET), revise Hola siguiendo la información de puerto.</span><span class="sxs-lookup"><span data-stu-id="f4427-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="f4427-107">Para obtener más información sobre las redes virtuales, consulte la [información general sobre redes virtuales](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f4427-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="f4427-108">Si ha creado un grupo de seguridad de red (NSG) restringir los recursos de red virtual de tráfico toohello en la colección, asegúrese de que Hola después puertos sean accesibles y permitida a través de directivas de seguridad de hello en red virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4427-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="f4427-109">Para obtener más información sobre los grupos de seguridad de red, consulte el artículo sobre [qué es un grupo de seguridad de red. (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="f4427-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="f4427-110">Subred de Azure RemoteApp necesita acceso toothese extremos y direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="f4427-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="f4427-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="f4427-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="f4427-112">*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="f4427-112">*.servicebus.net</span></span>
* <span data-ttu-id="f4427-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f4427-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f4427-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f4427-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="f4427-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f4427-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f4427-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f4427-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="f4427-117">Saliente: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="f4427-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="f4427-118">Opcional. UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="f4427-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="f4427-119">Clientes de Azure RemoteApp necesitan tener acceso a los puntos de conexión de toothese y las direcciones URL:</span><span class="sxs-lookup"><span data-stu-id="f4427-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="f4427-120">Los clientes que quiero decir Hola escritorios, dispositivos, etc. que las personas uso tooconnect toohello aplicaciones implementan en hello colección RemoteApp de Azure.</span><span class="sxs-lookup"><span data-stu-id="f4427-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="f4427-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f4427-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="f4427-122">https://*.RemoteApp.windowsazure.com (puertos UDP opcionales de hello son para esta dirección)</span><span class="sxs-lookup"><span data-stu-id="f4427-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="f4427-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="f4427-123">https://login.windows.net</span></span>  
* <span data-ttu-id="f4427-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="f4427-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="f4427-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="f4427-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="f4427-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f4427-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="f4427-127">Saliente: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="f4427-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="f4427-128">Opcional: UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="f4427-128">Optional - UDP: 3391</span></span> 

