---
title: "aaaInternet orientada hacia la información general del equilibrador de carga | Documentos de Microsoft"
description: "Información general sobre el equilibrador de carga accesible desde Internet y sus características. Cómo funciona un Equilibrador de carga de Azure mediante máquinas virtuales y servicios en la nube."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="6e8ec-104">Información general sobre el equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="6e8ec-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="6e8ec-105">Equilibrador de carga Azure asigna Hola público IP dirección y número de puerto entrante tráfico toohello privada dirección IP y puerto número de máquina virtual de Hola y viceversa para el tráfico de respuesta de saludo de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="6e8ec-106">Reglas de equilibrio de carga permiten a toodistribute determinados tipos de tráfico entre varias máquinas virtuales o servicios.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="6e8ec-107">Por ejemplo, se puede propagar carga Hola de tráfico de solicitudes web en varios servidores web o roles web.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="6e8ec-108">Para un servicio de nube que contiene instancias de roles web o roles de trabajo, puede definir un extremo público en el archivo de definición (.csdef) del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="6e8ec-109">Hola *servicedefinition.csdef* archivo contiene la configuración de punto de conexión de Hola y cuando haya varias instancias de rol para una implementación de rol web o de trabajo, equilibrador de carga de Hola se configurará para él.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="6e8ec-110">implementación de nube de Hello forma tooadd instancias tooyour está cambiando el número de instancias de hello en el archivo de configuración de servicio de hello (. csfg).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="6e8ec-111">Hello en la ilustración siguiente se muestra un extremo con equilibrio de carga para tráfico web que se comparte entre tres máquinas virtuales para hello pública y privada puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="6e8ec-112">Estas tres máquinas virtuales se encuentran en un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-112">These three virtual machines are in a load-balanced set.</span></span>

![ejemplo de equilibrador de carga público](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="6e8ec-114">Figura 1: punto de conexión de carga equilibrada para tráfico web</span><span class="sxs-lookup"><span data-stu-id="6e8ec-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="6e8ec-115">Cuando los clientes de Internet envían solicitudes de páginas web toohello de dirección IP pública del servicio de nube de hello en el puerto TCP 80, Hola equilibrador de carga de Azure distribuye las solicitudes de hello entre Hola tres máquinas virtuales en el conjunto de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="6e8ec-116">Para obtener más información acerca de los algoritmos de equilibrador de carga, vea hello [página de información general del equilibrador de carga](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="6e8ec-117">De forma predeterminada, Azure Load Balancer distribuye el tráfico de red equitativamente entre varias instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="6e8ec-118">También puede configurar la afinidad de la sesión. Para más información, consulte el [modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e8ec-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e8ec-119">Next steps</span></span>

<span data-ttu-id="6e8ec-120">Obtenga información acerca de [equilibrador de carga interno](load-balancer-internal-overview.md) toobetter comprender qué equilibrador de carga es mejor para su implementación en la nube.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="6e8ec-121">También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="6e8ec-122">Si su aplicación necesita que las conexiones de tookeep activo de servidores detrás de un equilibrador de carga, puede conocer más acerca de [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="6e8ec-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="6e8ec-123">Cuando se usa el equilibrador de carga de Azure le servirá de ayuda toolearn acerca del comportamiento de conexión inactiva.</span><span class="sxs-lookup"><span data-stu-id="6e8ec-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
