---
title: "Creación de un equilibrador de carga con conexión a Internet: Portal de Azure clásico | Microsoft Docs"
description: "Aprenda a crear un equilibrador de carga accesible desde Internet en el modelo de implementación clásica mediante el Portal de Azure clásico"
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
ms.openlocfilehash: a022154f5eca6de2d2dbfc1b9aa30d2ea0a7d650
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-the-azure-classic-portal"></a><span data-ttu-id="414e0-103">Introducción a la creación de un equilibrador de carga accesible desde Internet (clásico) en el Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="414e0-103">Get started creating an Internet facing load balancer (classic) in the Azure classic portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="414e0-104">Portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="414e0-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="414e0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="414e0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="414e0-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="414e0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="414e0-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="414e0-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="414e0-108">Antes de trabajar con recursos de Azure, es importante comprender que Azure tiene actualmente dos modelos de implementación: Azure Resource Manager y el clásico.</span><span class="sxs-lookup"><span data-stu-id="414e0-108">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="414e0-109">Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="414e0-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="414e0-110">Puede ver la documentación de las distintas herramientas haciendo clic en las fichas en la parte superior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="414e0-110">You can view the documentation for different tools by clicking the tabs at the top of this article.</span></span> <span data-ttu-id="414e0-111">Este artículo trata sobre el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="414e0-111">This article covers the classic deployment model.</span></span> <span data-ttu-id="414e0-112">También puede [obtener información sobre cómo crear un equilibrador de carga orientado a Internet con el Administrador de recursos de Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="414e0-112">You can also [Learn how to create an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a><span data-ttu-id="414e0-113">Configuración de un equilibrador de carga accesible desde Internet para máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="414e0-113">Set up an Internet-facing load balancer for virtual machines</span></span>

<span data-ttu-id="414e0-114">Para equilibrar la carga del tráfico de red de Internet entre las máquinas virtuales de un servicio en la nube, debe crear un conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="414e0-114">In order to load balance network traffic from the Internet across the virtual machines of a cloud service, you must create a load-balanced set.</span></span> <span data-ttu-id="414e0-115">En este procedimiento se supone que ya ha creado las máquinas virtuales y que están toda dentro del mismo servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="414e0-115">This procedure assumes that you have already created the virtual machines and that they are all within the same cloud service.</span></span>

<span data-ttu-id="414e0-116">**Para configurar un equilibrio de carga establecido para máquinas virtuales**</span><span class="sxs-lookup"><span data-stu-id="414e0-116">**To configure a load-balanced set for virtual machines**</span></span>

1. <span data-ttu-id="414e0-117">En el Portal de Azure  clásico, haga clic en **Máquinas virtuales**y luego en el nombre de una máquina virtual del conjunto con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="414e0-117">In the Azure classic portal, click **Virtual Machines**, and then click the name of a virtual machine in the load-balanced set.</span></span>
2. <span data-ttu-id="414e0-118">Haga clic en **Puntos de conexión** y luego en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="414e0-118">Click **Endpoints**, and then click **Add**.</span></span>
3. <span data-ttu-id="414e0-119">En la página **Agregar un extremo a una máquina virtual** , haga clic en la flecha derecha.</span><span class="sxs-lookup"><span data-stu-id="414e0-119">On the **Add an endpoint to a virtual machine** page, click the right arrow.</span></span>
4. <span data-ttu-id="414e0-120">En la página **Specify the details of the endpoint** :</span><span class="sxs-lookup"><span data-stu-id="414e0-120">On the **Specify the details of the endpoint** page:</span></span>

   * <span data-ttu-id="414e0-121">En **Name**, escriba un nombre para el extremo o seleccione uno de la lista de extremos predefinidos para protocolos comunes.</span><span class="sxs-lookup"><span data-stu-id="414e0-121">In **Name**, type a name for the endpoint or select the name from the list of predefined endpoints for common protocols.</span></span>
   * <span data-ttu-id="414e0-122">En **Protocol**, seleccione el protocolo que requiere el tipo de extremo, TCP o UDP, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="414e0-122">In **Protocol**, select the protocol required by the type of endpoint, either TCP or UDP, as needed.</span></span>
   * <span data-ttu-id="414e0-123">En **Public Port y Private Port**, escriba los números de puerto que desee que utilice la máquina virtual, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="414e0-123">In **Public Port and Private Port**, type the port numbers that you want the virtual machine to use, as needed.</span></span> <span data-ttu-id="414e0-124">Puede utilizar el puerto privado y las reglas de firewall en la máquina virtual para redirigir el tráfico de la manera más adecuada para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="414e0-124">You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.</span></span> <span data-ttu-id="414e0-125">El puerto privado puede ser el mismo que el puerto público.</span><span class="sxs-lookup"><span data-stu-id="414e0-125">The private port can be the same as the public port.</span></span> <span data-ttu-id="414e0-126">Por ejemplo, para un extremo para tráfico web (HTTP), puede asignar el puerto 80 al puerto público y el privado.</span><span class="sxs-lookup"><span data-stu-id="414e0-126">For example, for an endpoint for web (HTTP) traffic, you could assign port 80 to both the public and private port.</span></span>

5. <span data-ttu-id="414e0-127">Haga clic en **Create a load-balanced set**y, a continuación, en la flecha derecha.</span><span class="sxs-lookup"><span data-stu-id="414e0-127">Select **Create a load-balanced set**, and then click the right arrow.</span></span>
6. <span data-ttu-id="414e0-128">En la página **Configure the load-balanced set** , especifique un nombre para el conjunto con equilibrio de carga y, a continuación, asigne los valores para probar el comportamiento del equilibrador de carga de Azure.</span><span class="sxs-lookup"><span data-stu-id="414e0-128">On the **Configure the load-balanced set** page, type a name for the load-balanced set, and then assign the values for probe behavior of the Azure Load Balancer.</span></span> <span data-ttu-id="414e0-129">El equilibrador de carga utiliza pruebas para determinar si las máquinas virtuales del conjunto con equilibrio de carga están disponibles para recibir tráfico entrante.</span><span class="sxs-lookup"><span data-stu-id="414e0-129">The Load Balancer uses probes to determine if the virtual machines in the load-balanced set are available to receive incoming traffic.</span></span>
7. <span data-ttu-id="414e0-130">Haga clic en la marca de verificación para crear el extremo con equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="414e0-130">Click the check mark to create the load-balanced endpoint.</span></span> <span data-ttu-id="414e0-131">Verá **Sí** en la columna **Nombre de conjunto de carga equilibrada** de la página **Puntos de conexión** de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="414e0-131">You will see **Yes** in the **Load-balanced set name** column of the **Endpoints** page for the virtual machine.</span></span>
8. <span data-ttu-id="414e0-132">En el portal, haga clic en **Máquinas virtuales**, en el nombre de otra máquina virtual del conjunto con equilibrio de carga, en **Puntos de conexión** y, finalmente, en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="414e0-132">In the portal, click **Virtual Machines**, click the name of an additional virtual machine in the load-balanced set, click **Endpoints**, and then click **Add**.</span></span>
9. <span data-ttu-id="414e0-133">En la página **Agregar un extremo a una máquina virtual**, haga clic en **Add endpoint to an existing load-balanced set** (Agregar punto de conexión a un conjunto de carga equilibrada existente), seleccione el nombre del conjunto con equilibrio de carga y haga clic en la flecha derecha.</span><span class="sxs-lookup"><span data-stu-id="414e0-133">On the **Add an endpoint to a virtual machine** page, click **Add endpoint to an existing load-balanced set**, select the name of the load-balanced set, and then click the right arrow.</span></span>
10. <span data-ttu-id="414e0-134">En la página **Specify the details of the endpoint** , escriba un nombre para el extremo y, a continuación, haga clic en la marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="414e0-134">On the **Specify the details of the endpoint** page, type a name for the endpoint, and then click the check mark.</span></span>

<span data-ttu-id="414e0-135">Para las máquinas virtuales adicionales del conjunto con equilibrio de carga, repita los pasos del 8 al 10.</span><span class="sxs-lookup"><span data-stu-id="414e0-135">For the additional virtual machines in the load-balanced set, repeat steps 8-10.</span></span>

## <a name="next-steps"></a><span data-ttu-id="414e0-136">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="414e0-136">Next steps</span></span>

[<span data-ttu-id="414e0-137">Introducción a la configuración de un equilibrador de carga interno</span><span class="sxs-lookup"><span data-stu-id="414e0-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="414e0-138">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="414e0-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="414e0-139">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="414e0-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
