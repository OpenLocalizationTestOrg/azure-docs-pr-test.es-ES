---
title: comprobar el flujo de tooIP aaaIntroduction en Monitor de red de Azure | Documentos de Microsoft
description: "Esta página proporciona una visión general de hello IP de Monitor de red flujo comprobar la capacidad"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="8a0ff-103">Comprobar el flujo de introducción tooIP en Monitor de red de Azure</span><span class="sxs-lookup"><span data-stu-id="8a0ff-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="8a0ff-104">Flujo IP Compruebe comprueba si un paquete se permite o deniega tooor desde una máquina virtual basada en la información de tupla de 5.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="8a0ff-105">Esta información está formada por la dirección, el protocolo, la dirección IP local, la dirección IP remota, el puerto local y el puerto remoto.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="8a0ff-106">Si el paquete de saludo ha sido denegado por un grupo de seguridad, se devuelve el nombre de Hola de regla de Hola que deniega el paquete de saludo.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="8a0ff-107">Aunque puede elegir cualquier dirección IP de origen o destino, esta característica ayuda a los administradores diagnosticar rápidamente problemas de conectividad de o toohello internet y desde o entorno local de toohello.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="8a0ff-108">La comprobación de flujo de IP tiene como destino una interfaz de red de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="8a0ff-109">Flujo de tráfico, a continuación, se comprueba en función de hello configurado tooor de configuración de esa interfaz de red.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="8a0ff-110">Esta capacidad es útil para confirmar si una regla en un grupo de seguridad de red está bloqueando tooor de tráfico de entrada o salida de una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="8a0ff-111">Comprobar una instancia del Monitor de red necesidades toobe creado en todas las regiones que planea toorun flujo IP.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="8a0ff-112">Monitor de red es un servicio regional y solo se ejecutó con los recursos en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="8a0ff-113">Esto no afecta a Hola comprobar resultados de flujo IP como ruta de hello asociada Hola que NIC todavía se devolverá.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="8a0ff-115">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8a0ff-115">Next steps</span></span>

<span data-ttu-id="8a0ff-116">Visite Hola después toolearn artículo si un paquete se permite o deniega para una máquina virtual específica a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="8a0ff-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="8a0ff-117">Compruebe si se permite el tráfico en una máquina virtual con IP flujo Compruebe mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="8a0ff-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












