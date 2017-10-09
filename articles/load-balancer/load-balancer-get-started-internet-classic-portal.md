---
title: "equilibrador de carga de aaaCreate una conexión a Internet: portal de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un equilibrador de carga con conexión a Internet en el modelo de implementación clásica utilizando Hola portal de Azure clásico"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a><span data-ttu-id="5c95a-103">Empezar a crear un equilibrador de carga (clásica) en el portal de Azure clásico Hola de Internet</span><span class="sxs-lookup"><span data-stu-id="5c95a-103">Get started creating an Internet facing load balancer (classic) in hello Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c95a-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="5c95a-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="5c95a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c95a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="5c95a-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="5c95a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="5c95a-107">Servicios en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="5c95a-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5c95a-108">Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico.</span><span class="sxs-lookup"><span data-stu-id="5c95a-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="5c95a-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c95a-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="5c95a-110">Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="5c95a-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="5c95a-111">Este artículo trata el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5c95a-112">También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5c95a-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="5c95a-113">Configuración de un equilibrador de carga accesible desde Internet para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="5c95a-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="5c95a-114">Tráfico de red de orden tooload saldo de hello Internet todas las máquinas virtuales de Hola de un servicio de nube, debe crear un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="5c95a-114">In order tooload balance network traffic from hello Internet across hello virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="5c95a-115">Este procedimiento se supone que ya ha creado máquinas virtuales de Hola y que están todas en hello mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="5c95a-115">This procedure assumes that you have already created hello virtual machines and that they are all within hello same cloud service.</span></span>

<span data-ttu-id="5c95a-116">**tooconfigure un conjunto con equilibrio de carga para las máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="5c95a-116">**tooconfigure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="5c95a-117">Hola portal de Azure clásico, haga clic en **máquinas virtuales**y, a continuación, haga clic en nombre de Hola de una máquina virtual en el conjunto de equilibrio de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-117">In hello Azure classic portal, click **Virtual Machines**, and then click hello name of a virtual machine in hello load-balanced set.</span></span>
2. <span data-ttu-id="5c95a-118">Haga clic en **Puntos de conexión** y luego en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5c95a-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="5c95a-119">En hello **agregar una máquina virtual de tooa de punto de conexión** página, haga clic en la flecha derecha Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-119">On hello **Add an endpoint tooa virtual machine** page, click hello right arrow.</span></span>
4. <span data-ttu-id="5c95a-120">En hello **especificar detalles de Hola de punto de conexión de hello** página:</span><span class="sxs-lookup"><span data-stu-id="5c95a-120">On hello **Specify hello details of hello endpoint** page:</span></span>

   * <span data-ttu-id="5c95a-121">En **nombre**, escriba un nombre para el punto de conexión de Hola o seleccione el nombre de hello en lista de Hola de extremos predefinidos para protocolos comunes.</span><span class="sxs-lookup"><span data-stu-id="5c95a-121">In **Name**, type a name for hello endpoint or select hello name from hello list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="5c95a-122">En **protocolo**, seleccione Protocolo de hello requeridos por tipo hello del extremo, TCP o UDP, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5c95a-122">In **Protocol**, select hello protocol required by hello type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="5c95a-123">En **puerto público y puerto privado**, escriba los números de puerto de Hola que desee Hola toouse de máquina virtual, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5c95a-123">In **Public Port and Private Port**, type hello port numbers that you want hello virtual machine toouse, as needed.</span></span> <span data-ttu-id="5c95a-124">Puede usar el puerto privado de Hola y reglas de firewall en tráfico de tooredirect Hola máquinas virtuales de una manera que sea adecuada para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="5c95a-124">You can use hello private port and firewall rules on hello virtual machine tooredirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="5c95a-125">puerto privado Hola puede ser Hola igual que el puerto público de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-125">hello private port can be hello same as hello public port.</span></span> <span data-ttu-id="5c95a-126">Por ejemplo, para un extremo para el tráfico web (HTTP), podría asignar puerto 80 tooboth Hola públicas y privadas port.</span><span class="sxs-lookup"><span data-stu-id="5c95a-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 tooboth hello public and private port.</span></span>

5. <span data-ttu-id="5c95a-127">Seleccione **crear un conjunto con equilibrio de carga**y, a continuación, haga clic en la flecha derecha Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-127">Select **Create a load-balanced set**, and then click hello right arrow.</span></span>
6. <span data-ttu-id="5c95a-128">En hello **configurar el conjunto de equilibrio de carga de hello** página, escriba un nombre para el conjunto de equilibrio de carga de hello y, a continuación, asignar valores de hello para sondear el comportamiento de hello equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="5c95a-128">On hello **Configure hello load-balanced set** page, type a name for hello load-balanced set, and then assign hello values for probe behavior of hello Azure Load Balancer.</span></span> <span data-ttu-id="5c95a-129">Hola equilibrador de carga utiliza sondeos toodetermine si hay máquinas virtuales de hello en el conjunto de equilibrio de carga de hello tooreceive disponible el tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="5c95a-129">hello Load Balancer uses probes toodetermine if hello virtual machines in hello load-balanced set are available tooreceive incoming traffic.</span></span>
7. <span data-ttu-id="5c95a-130">Haga clic en el extremo de carga equilibrada de hello marca de verificación toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-130">Click hello check mark toocreate hello load-balanced endpoint.</span></span> <span data-ttu-id="5c95a-131">Verá **Sí** en hello **nombre de conjunto de carga equilibrada** columna de hello **extremos** página para la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-131">You will see **Yes** in hello **Load-balanced set name** column of hello **Endpoints** page for hello virtual machine.</span></span>
8. <span data-ttu-id="5c95a-132">En el portal de hello, haga clic en **máquinas virtuales**, haga clic en nombre de Hola de una máquina virtual adicional en el conjunto de equilibrio de carga de hello, haga clic en **extremos**y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5c95a-132">In hello portal, click **Virtual Machines**, click hello name of an additional virtual machine in hello load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="5c95a-133">En hello **agregar una máquina virtual en extremo tooa** página, haga clic en **Agregar conjunto de carga equilibrada existente de punto de conexión tooan**, seleccione Hola nombre de conjunto de equilibrio de carga de hello y, a continuación, haga clic en la flecha derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-133">On hello **Add an endpoint tooa virtual machine** page, click **Add endpoint tooan existing load-balanced set**, select hello name of hello load-balanced set, and then click hello right arrow.</span></span>
10. <span data-ttu-id="5c95a-134">En hello **especificar detalles de Hola de punto de conexión de hello** página, escriba un nombre para el extremo de hello y, a continuación, haga clic en la casilla de verificación Hola.</span><span class="sxs-lookup"><span data-stu-id="5c95a-134">On hello **Specify hello details of hello endpoint** page, type a name for hello endpoint, and then click hello check mark.</span></span>

<span data-ttu-id="5c95a-135">Para las máquinas virtuales adicionales de hello en el conjunto de equilibrio de carga de hello, repita los pasos 8-10.</span><span class="sxs-lookup"><span data-stu-id="5c95a-135">For hello additional virtual machines in hello load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c95a-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5c95a-136">Next steps</span></span>

[<span data-ttu-id="5c95a-137">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="5c95a-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="5c95a-138">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="5c95a-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="5c95a-139">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="5c95a-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
