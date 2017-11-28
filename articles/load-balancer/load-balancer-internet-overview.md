---
title: "Información general sobre el equilibrador de carga accesible desde Internet | Microsoft Docs"
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
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="a7119-104">Información general sobre el equilibrador de carga accesible desde Internet</span><span class="sxs-lookup"><span data-stu-id="a7119-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="a7119-105">El Equilibrador de carga de Azure asigna la dirección IP y el número de puerto públicos del tráfico entrante a la dirección IP y el número de puerto privados de la máquina virtual, y viceversa, para el tráfico de respuesta desde la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7119-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="a7119-106">Las reglas de equilibrio de carga permiten distribuir tipos específicos de tráfico entre varias máquinas virtuales o servicios.</span><span class="sxs-lookup"><span data-stu-id="a7119-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="a7119-107">Por ejemplo, puede extender la carga del tráfico de solicitudes web entre varios servidores web o roles web.</span><span class="sxs-lookup"><span data-stu-id="a7119-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="a7119-108">Para los servicios en la nube que contienen instancias de roles web o de roles de trabajo, puede definir un punto de conexión público en la definición de servicio (.csdef).</span><span class="sxs-lookup"><span data-stu-id="a7119-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="a7119-109">El archivo *servicedefinition.csdef* contiene la configuración del punto de conexión y, cuando tenga varias instancias de rol para una implementación de rol web o de trabajo, el equilibrador de carga se configurará para ello.</span><span class="sxs-lookup"><span data-stu-id="a7119-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="a7119-110">La forma de agregar instancias a su implementación en la nube está cambiando el recuento de instancias en el archivo de configuración de servicio (.csfg).</span><span class="sxs-lookup"><span data-stu-id="a7119-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="a7119-111">En la siguiente ilustración, se muestra un punto de conexión de carga equilibrada para el tráfico web que se comparte entre tres máquinas virtuales en el puerto TCP público y privado de 80.</span><span class="sxs-lookup"><span data-stu-id="a7119-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="a7119-112">Estas tres máquinas virtuales se encuentran en un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="a7119-112">These three virtual machines are in a load-balanced set.</span></span>

![ejemplo de equilibrador de carga público](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="a7119-114">Figura 1: punto de conexión de carga equilibrada para tráfico web</span><span class="sxs-lookup"><span data-stu-id="a7119-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="a7119-115">Cuando los clientes de Internet envían solicitudes de página web a la dirección IP pública del servicio en la nube en el puerto TCP 80, Azure Load Balancer distribuye las solicitudes entre las tres máquinas virtuales del conjunto de carga equilibrada.</span><span class="sxs-lookup"><span data-stu-id="a7119-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="a7119-116">Para más información sobre algoritmos del equilibrador de carga, consulte la [página de información general del equilibrador de carga](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="a7119-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="a7119-117">De forma predeterminada, Azure Load Balancer distribuye el tráfico de red equitativamente entre varias instancias de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a7119-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="a7119-118">También puede configurar la afinidad de la sesión. Para más información, consulte el [modo de distribución del equilibrador de carga](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="a7119-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7119-119">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a7119-119">Next steps</span></span>

<span data-ttu-id="a7119-120">Obtenga más información sobre el [equilibrador de carga interno](load-balancer-internal-overview.md) para saber qué equilibrador de carga se adapta mejor a su implementación en la nube.</span><span class="sxs-lookup"><span data-stu-id="a7119-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="a7119-121">También puede [empezar a crear un equilibrador de carga accesible desde Internet](load-balancer-get-started-internet-arm-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento especifico del tráfico de red del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="a7119-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="a7119-122">Si la aplicación necesita mantener conexiones activas para servidores detrás de un equilibrador de carga, puede obtener más información acerca de la [configuración de tiempo de espera de inactividad de TCP para el equilibrador de carga](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="a7119-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="a7119-123">Le ayudará a conocer el comportamiento de conexión del tiempo de inactividad cuando se usa el Equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="a7119-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
