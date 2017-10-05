---
title: "Creación de un equilibrador de carga interno: Azure Portal | Microsoft Docs"
description: "Obtenga información sobre cómo crear un equilibrador de carga interno en Resource Manager mediante el Portal de Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 8fbe9d5d04d745de51e0e41516d6c12683c98637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a><span data-ttu-id="c2287-103">Creación de un equilibrador de carga interno en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c2287-103">Create an Internal load balancer in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2287-104">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c2287-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="c2287-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2287-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="c2287-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c2287-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="c2287-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="c2287-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="c2287-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c2287-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c2287-109">En este artículo se describe el uso del modelo de implementación de Resource Manager, recomendado por Microsoft para la mayoría de las nuevas implementaciones en lugar del [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c2287-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="c2287-110">Primeros pasos en la creación de un equilibrador de carga interno mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="c2287-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="c2287-111">Para crear un equilibrador de carga interno desde Azure Portal, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c2287-111">Use the following steps to create an internal load balancer from the Azure Portal.</span></span>

1. <span data-ttu-id="c2287-112">Abra un explorador, navegue a [Azure Portal](http://portal.azure.com) e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c2287-112">Open a browser, navigate to the [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="c2287-113">En la parte superior izquierda de la pantalla, haga clic en **Nuevo** > **Redes** > **Equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="c2287-113">In the upper left hand side of the screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="c2287-114">En la hoja **Crear equilibrador de carga**, escriba el **nombre** del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-114">In the **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="c2287-115">En **Esquema**, haga clic en **Interno**.</span><span class="sxs-lookup"><span data-stu-id="c2287-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="c2287-116">Haga clic en **Red Virtual**y, a continuación, seleccione la red virtual donde desee crear el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-116">Click **Virtual network**, and then select the virtual network where you want to create the load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c2287-117">Si no ve la red virtual que desea utilizar, compruebe la **ubicación** que utiliza para el equilibrador de carga y cámbiela según corresponda.</span><span class="sxs-lookup"><span data-stu-id="c2287-117">If you do not see the virtual network you want to use, check the **Location** you are using for the load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="c2287-118">Haga clic en **Subred**y, a continuación, seleccione la subred en la que desee crear el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-118">Click **Subnet**, and then select the subnet where you want to create the load balancer.</span></span>
7. <span data-ttu-id="c2287-119">En **Asignación de dirección IP**, haga clic en **Dinámica** o **Estática**, en función de si desea que la dirección IP del equilibrador de carga sea fija (estática) o no.</span><span class="sxs-lookup"><span data-stu-id="c2287-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want the IP address for the load balancer to be fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c2287-120">Si selecciona usar una dirección IP estática, tendrá que proporcionar una dirección para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-120">If you select to use a static IP address, you will have to provide an address for the load balancer.</span></span>

8. <span data-ttu-id="c2287-121">En **Grupo de recursos**, especifique el nombre de un grupo de recursos nuevo para el equilibrador de carga, o haga clic en **Seleccionar existente** y seleccione un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="c2287-121">Under **Resource group** either specify the name of a new resource group for the load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="c2287-122">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="c2287-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="c2287-123">Configuración de las reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="c2287-123">Configure load balancing rules</span></span>

<span data-ttu-id="c2287-124">Después de la creación del equilibrador de carga, vaya al recurso del equilibrador de carga para configurarlo.</span><span class="sxs-lookup"><span data-stu-id="c2287-124">After the load balancer creation, navigate to the load balancer resource to configure it.</span></span>
<span data-ttu-id="c2287-125">Tiene que configurar primero un grupo de direcciones back-end y un sondeo antes de configurar una regla de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-125">You need to configure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="c2287-126">Paso 1: Configuración de un grupo back-end</span><span class="sxs-lookup"><span data-stu-id="c2287-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="c2287-127">En Azure Portal, haga clic en **Examinar** > **Equilibradores de carga** y, después, haga clic en el equilibrador de carga que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2287-127">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="c2287-128">En la hoja **Configuración**, haga clic en **Grupos back-end**.</span><span class="sxs-lookup"><span data-stu-id="c2287-128">In the **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="c2287-129">En la hoja **Grupos de direcciones de back-end**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c2287-129">In the **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="c2287-130">En la hoja **Agregar grupo de back-end**, escriba el **nombre** del grupo de back-end y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c2287-130">In the **Add backend pool** blade, enter a **Name** for the backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="c2287-131">Paso 2: Configuración de un sondeo</span><span class="sxs-lookup"><span data-stu-id="c2287-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="c2287-132">En Azure Portal, haga clic en **Examinar** > **Equilibradores de carga** y, después, haga clic en el equilibrador de carga que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2287-132">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="c2287-133">En la hoja **Configuración**, haga clic en **Sondeos**.</span><span class="sxs-lookup"><span data-stu-id="c2287-133">In the **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="c2287-134">En la hoja **Sondeos**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c2287-134">In the **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="c2287-135">En la hoja **Agregar sondeo**, escriba el **nombre** del sondeo.</span><span class="sxs-lookup"><span data-stu-id="c2287-135">In the **Add probe** blade, enter a **Name** for the probe.</span></span>
5. <span data-ttu-id="c2287-136">En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).</span><span class="sxs-lookup"><span data-stu-id="c2287-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="c2287-137">En **Puerto**, especifique el puerto que se utilizará al obtener acceso el sondeo.</span><span class="sxs-lookup"><span data-stu-id="c2287-137">Under **Port**, specify the port to use when accessing the probe.</span></span>
7. <span data-ttu-id="c2287-138">En **Ruta** (solo para sondeos HTTP), especifique la ruta de acceso que usar como un sondeo.</span><span class="sxs-lookup"><span data-stu-id="c2287-138">Under **Path** (for HTTP probes only), specify the path to use as a probe.</span></span>
8. <span data-ttu-id="c2287-139">En **Intervalo** , especifique la frecuencia de sondeo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="c2287-139">Under **Interval** specify how frequently to probe the application.</span></span>
9. <span data-ttu-id="c2287-140">En **Umbral incorrecto**, especifique en cuántos intentos debe producirse un error para que la máquina virtual de back-end se marque como incorrecta.</span><span class="sxs-lookup"><span data-stu-id="c2287-140">Under **Unhealthy threshold**, specify how many attempts should fail before the backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="c2287-141">Haga clic en **Aceptar** para crear el sondeo.</span><span class="sxs-lookup"><span data-stu-id="c2287-141">Click **OK** to create probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="c2287-142">Paso 3: Configuración de las reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="c2287-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="c2287-143">En Azure Portal, haga clic en **Examinar** > **Equilibradores de carga** y, después, haga clic en el equilibrador de carga que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2287-143">In the Azure portal, click **Browse** > **Load balancers**, and then click the load balancer you created above.</span></span>
2. <span data-ttu-id="c2287-144">En la hoja **Configuración**, haga clic en **Reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="c2287-144">In the **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="c2287-145">En la hoja **Reglas de equilibrio de carga**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="c2287-145">In the **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="c2287-146">En la hoja **Agregar regla de equilibrio de carga**, escriba el **nombre** de la regla.</span><span class="sxs-lookup"><span data-stu-id="c2287-146">In the **Add load balancing rule** blade, enter a **Name** for the rule.</span></span>
5. <span data-ttu-id="c2287-147">En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).</span><span class="sxs-lookup"><span data-stu-id="c2287-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="c2287-148">En **Puerto**, especifique los puertos a los que se conectan los clientes en el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="c2287-148">Under **Port**, specify the port clients connect to in the load balancer.</span></span>
7. <span data-ttu-id="c2287-149">En **Puerto back-end**, especifique el puerto que se utilizará para el grupo back-end (normalmente, el puerto del equilibrador de carga y el puerto back-end son iguales).</span><span class="sxs-lookup"><span data-stu-id="c2287-149">Under **Backend port**, specify the port to be used in the backend pool (usually, the load balancer port and the backend port are the same).</span></span>
8. <span data-ttu-id="c2287-150">En **Grupo back-end**, seleccione el grupo back-end que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c2287-150">Under **Backend pool**, select the backend pool you created above.</span></span>
9. <span data-ttu-id="c2287-151">En **Persistencia de la sesión**, seleccione cómo desea que se conserven las sesiones.</span><span class="sxs-lookup"><span data-stu-id="c2287-151">Under **Session persistence**, select how you want sessions to persist.</span></span>
10. <span data-ttu-id="c2287-152">En **Tiempo de espera de inactividad (minutos)**, especifique el tiempo de espera de inactividad.</span><span class="sxs-lookup"><span data-stu-id="c2287-152">Under **Idle timeout (minutes)**, specify the idle timeout.</span></span>
11. <span data-ttu-id="c2287-153">En **IP flotante (Direct Server Return)**, haga clic en **Deshabilitado** o **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="c2287-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="c2287-154">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="c2287-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2287-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2287-155">Next steps</span></span>

[<span data-ttu-id="c2287-156">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="c2287-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c2287-157">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="c2287-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

