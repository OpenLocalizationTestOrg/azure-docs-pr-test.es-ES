---
title: Requisitos de ExpressRoute aaaQoS | Documentos de Microsoft
description: "En esta página se proporcionan requisitos detallados para configurar y administrar QoS para circuitos ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: db1c1447-0283-4a09-907b-ae481adc40c7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: cherylmc
ms.openlocfilehash: 46cc81bd38ff50dd9e7a1bfdd0faa457ff7b2fa1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-qos-requirements"></a><span data-ttu-id="25bc9-103">Requisitos de QoS ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25bc9-103">ExpressRoute QoS requirements</span></span>
<span data-ttu-id="25bc9-104">Skype Empresarial tiene varias cargas de trabajo que requieren tratamiento diferenciado de QoS.</span><span class="sxs-lookup"><span data-stu-id="25bc9-104">Skype for Business has various workloads that require differentiated QoS treatment.</span></span> <span data-ttu-id="25bc9-105">Si tiene previsto tooconsume de servicios de voz a través de ExpressRoute, debe cumplir los requisitos de toohello descritos a continuación.</span><span class="sxs-lookup"><span data-stu-id="25bc9-105">If you plan tooconsume voice services through ExpressRoute, you should adhere toohello requirements described below.</span></span>

![](./media/expressroute-qos/expressroute-qos.png)

> [!NOTE]
> <span data-ttu-id="25bc9-106">Requisitos de QoS aplican solo al emparejamiento de Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="25bc9-106">QoS requirements apply toohello Microsoft peering only.</span></span> <span data-ttu-id="25bc9-107">Restablecer too0 serán los valores DSCP de Hello en el tráfico de red recibido en pares públicos de Azure y Azure intercambio de tráfico privado.</span><span class="sxs-lookup"><span data-stu-id="25bc9-107">hello DSCP values in your network traffic received on Azure public peering and Azure private peering will be reset too0.</span></span> 
> 
> 

<span data-ttu-id="25bc9-108">Hello tabla siguiente proporciona una lista de marcado de DSCP usado Skype para la empresa.</span><span class="sxs-lookup"><span data-stu-id="25bc9-108">hello following table provides a list of DSCP markings used by Skype for Business.</span></span> <span data-ttu-id="25bc9-109">Consulte demasiado[administración de QoS para Skype empresarial](https://technet.microsoft.com/library/gg405409.aspx) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="25bc9-109">Refer too[Managing QoS for Skype for Business](https://technet.microsoft.com/library/gg405409.aspx) for more information.</span></span>

| <span data-ttu-id="25bc9-110">**Clase de tráfico**</span><span class="sxs-lookup"><span data-stu-id="25bc9-110">**Traffic Class**</span></span> | <span data-ttu-id="25bc9-111">**Tratamiento (marcado de DSCP)**</span><span class="sxs-lookup"><span data-stu-id="25bc9-111">**Treatment (DSCP Marking)**</span></span> | <span data-ttu-id="25bc9-112">**Cargas de trabajo de Skype Empresarial**</span><span class="sxs-lookup"><span data-stu-id="25bc9-112">**Skype for Business Workloads**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="25bc9-113">**Voz**</span><span class="sxs-lookup"><span data-stu-id="25bc9-113">**Voice**</span></span> |<span data-ttu-id="25bc9-114">EF (46)</span><span class="sxs-lookup"><span data-stu-id="25bc9-114">EF (46)</span></span> |<span data-ttu-id="25bc9-115">Voz de Skype o Lync</span><span class="sxs-lookup"><span data-stu-id="25bc9-115">Skype / Lync voice</span></span> |
| <span data-ttu-id="25bc9-116">**Interactivo**</span><span class="sxs-lookup"><span data-stu-id="25bc9-116">**Interactive**</span></span> |<span data-ttu-id="25bc9-117">AF41 (34)</span><span class="sxs-lookup"><span data-stu-id="25bc9-117">AF41 (34)</span></span> |<span data-ttu-id="25bc9-118">Video, VBSS</span><span class="sxs-lookup"><span data-stu-id="25bc9-118">Video, VBSS</span></span> |
| <span data-ttu-id="25bc9-119">AF21 (18)</span><span class="sxs-lookup"><span data-stu-id="25bc9-119">AF21 (18)</span></span> |<span data-ttu-id="25bc9-120">Uso compartido de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="25bc9-120">App sharing</span></span> | |
| <span data-ttu-id="25bc9-121">**Valor predeterminado**</span><span class="sxs-lookup"><span data-stu-id="25bc9-121">**Default**</span></span> |<span data-ttu-id="25bc9-122">AF11 (10)</span><span class="sxs-lookup"><span data-stu-id="25bc9-122">AF11 (10)</span></span> |<span data-ttu-id="25bc9-123">Transferencia de archivos</span><span class="sxs-lookup"><span data-stu-id="25bc9-123">File transfer</span></span> |
| <span data-ttu-id="25bc9-124">CS0 (0)</span><span class="sxs-lookup"><span data-stu-id="25bc9-124">CS0 (0)</span></span> |<span data-ttu-id="25bc9-125">Nada más</span><span class="sxs-lookup"><span data-stu-id="25bc9-125">Anything else</span></span> | |

* <span data-ttu-id="25bc9-126">Debe clasificar las cargas de trabajo de Hola y marcar valores DSCP de hello correctos.</span><span class="sxs-lookup"><span data-stu-id="25bc9-126">You should classify hello workloads and mark hello right DSCP values.</span></span> <span data-ttu-id="25bc9-127">Siga las instrucciones de hello indicadas [aquí](https://technet.microsoft.com/library/gg405409.aspx) acerca de cómo tooset marcas de DSCP de la red.</span><span class="sxs-lookup"><span data-stu-id="25bc9-127">Follow hello guidance provided [here](https://technet.microsoft.com/library/gg405409.aspx) on how tooset DSCP markings in your network.</span></span>
* <span data-ttu-id="25bc9-128">Debe configurar y admitir varias colas de QoS dentro de la red.</span><span class="sxs-lookup"><span data-stu-id="25bc9-128">You should configure and support multiple QoS queues within your network.</span></span> <span data-ttu-id="25bc9-129">Debe ser una clase independiente de voz y reciben un tratamiento EF Hola especificado en RFC 3246.</span><span class="sxs-lookup"><span data-stu-id="25bc9-129">Voice must be a standalone class and receive hello EF treatment specified in RFC 3246.</span></span> 
* <span data-ttu-id="25bc9-130">Puede decidir Hola Queue mecanismo, la directiva de detección de congestión y asignación de ancho de banda por clase de tráfico.</span><span class="sxs-lookup"><span data-stu-id="25bc9-130">You can decide hello queuing mechanism, congestion detection policy, and bandwidth allocation per traffic class.</span></span> <span data-ttu-id="25bc9-131">Sin embargo, hello DSCP marcar de Skype para cargas de trabajo de negocios debe conservarse.</span><span class="sxs-lookup"><span data-stu-id="25bc9-131">But, hello DSCP marking for Skype for Business workloads must be preserved.</span></span> <span data-ttu-id="25bc9-132">Si usas marcas DSCP no indicados anteriormente, p. ej. AF31 (26), debe volver a escribir este too0 del valor DSCP antes de enviar tooMicrosoft de paquetes de saludo.</span><span class="sxs-lookup"><span data-stu-id="25bc9-132">If you are using DSCP markings not listed above, e.g. AF31 (26), you must rewrite this DSCP value too0 before sending hello packet tooMicrosoft.</span></span> <span data-ttu-id="25bc9-133">Microsoft sólo envía paquetes marcados con hello el valor de DSCP se muestra en hello por encima de la tabla.</span><span class="sxs-lookup"><span data-stu-id="25bc9-133">Microsoft only sends packets marked with hello DSCP value shown in hello above table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="25bc9-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25bc9-134">Next steps</span></span>
* <span data-ttu-id="25bc9-135">Consulte los requisitos de toohello para [enrutamiento](expressroute-routing.md) y [NAT](expressroute-nat.md).</span><span class="sxs-lookup"><span data-stu-id="25bc9-135">Refer toohello requirements for [Routing](expressroute-routing.md) and [NAT](expressroute-nat.md).</span></span>
* <span data-ttu-id="25bc9-136">Vea la siguiente Hola vincula tooconfigure la conexión ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="25bc9-136">See hello following links tooconfigure your ExpressRoute connection.</span></span>
  
  * [<span data-ttu-id="25bc9-137">Creación de un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="25bc9-137">Create an ExpressRoute circuit</span></span>](expressroute-howto-circuit-classic.md)
  * [<span data-ttu-id="25bc9-138">Configuración del enrutamiento</span><span class="sxs-lookup"><span data-stu-id="25bc9-138">Configure routing</span></span>](expressroute-howto-routing-classic.md)
  * [<span data-ttu-id="25bc9-139">Vincular un circuito de ExpressRoute de tooan de red virtual</span><span class="sxs-lookup"><span data-stu-id="25bc9-139">Link a VNet tooan ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-classic.md)

