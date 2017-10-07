---
title: 'aaaCreate un equilibrador de carga interno: portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de cómo toocreate un interno equilibrador de carga de recursos Manager mediante Hola portal de Azure"
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
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="ef988-103">Crear un equilibrador de carga interno en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ef988-103">Create an Internal load balancer in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ef988-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ef988-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="ef988-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef988-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="ef988-106">CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="ef988-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="ef988-107">Plantilla</span><span class="sxs-lookup"><span data-stu-id="ef988-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ef988-108">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ef988-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="ef988-109">Este artículo incluye el uso de modelo de implementación de administrador de recursos de hello, que Microsoft recomienda para la mayoría de las nueva implementaciones en lugar de hello [modelo de implementación clásica](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ef988-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a><span data-ttu-id="ef988-110">Primeros pasos en la creación de un equilibrador de carga interno mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="ef988-110">Get started creating an Internal load balancer using Azure portal</span></span>

<span data-ttu-id="ef988-111">Usar hello siguiendo los pasos toocreate un equilibrador de carga interno de hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef988-111">Use hello following steps toocreate an internal load balancer from hello Azure Portal.</span></span>

1. <span data-ttu-id="ef988-112">Abra un explorador, vaya toohello [portal de Azure](http://portal.azure.com)e inicie sesión con su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef988-112">Open a browser, navigate toohello [Azure portal](http://portal.azure.com), and sign in with your Azure account.</span></span>
2. <span data-ttu-id="ef988-113">En hello superior izquierda de la pantalla de bienvenida, haga clic en **New** > **red** > **equilibrador de carga**.</span><span class="sxs-lookup"><span data-stu-id="ef988-113">In hello upper left hand side of hello screen, click **New** > **Networking** > **Load balancer**.</span></span>
3. <span data-ttu-id="ef988-114">Hola **equilibrador de carga de crear** hoja, escriba una **nombre** para el equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="ef988-114">In hello **Create load balancer** blade, enter a **Name** for your load balancer.</span></span>
4. <span data-ttu-id="ef988-115">En **Esquema**, haga clic en **Interno**.</span><span class="sxs-lookup"><span data-stu-id="ef988-115">Under **Scheme**, click **Internal**.</span></span>
5. <span data-ttu-id="ef988-116">Haga clic en **red Virtual**, y, a continuación, seleccione Hola donde desea que el equilibrador de carga de hello toocreate de red virtual.</span><span class="sxs-lookup"><span data-stu-id="ef988-116">Click **Virtual network**, and then select hello virtual network where you want toocreate hello load balancer.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef988-117">Si no ve la red virtual de Hola que desea toouse, compruebe hello **ubicación** se está usando para el equilibrador de carga de Hola y cambia en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="ef988-117">If you do not see hello virtual network you want toouse, check hello **Location** you are using for hello load balancer, and change it accordingly.</span></span>

6. <span data-ttu-id="ef988-118">Haga clic en **subred**y, a continuación, seleccione subred Hola donde desea que el equilibrador de carga de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-118">Click **Subnet**, and then select hello subnet where you want toocreate hello load balancer.</span></span>
7. <span data-ttu-id="ef988-119">En **asignación de direcciones IP**, haga clic en **dinámica** o **estático**, dependiendo de si desea dirección IP de Hola para hello carga equilibrador toobe fijo (estático) o no.</span><span class="sxs-lookup"><span data-stu-id="ef988-119">Under **IP address assignment**, click either **Dynamic** or **Static**, depending on whether you want hello IP address for hello load balancer toobe fixed (static) or not.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ef988-120">Si selecciona toouse una dirección IP estática, tendrá que tooprovide es una dirección de equilibrador de carga de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-120">If you select toouse a static IP address, you will have tooprovide an address for hello load balancer.</span></span>

8. <span data-ttu-id="ef988-121">En **grupo de recursos** especifique Hola nombre de un nuevo grupo de recursos para el equilibrador de carga de hello, o haga clic en **seleccione existente** y seleccione un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="ef988-121">Under **Resource group** either specify hello name of a new resource group for hello load balancer, or click **select existing** and select an existing resource group.</span></span>
9. <span data-ttu-id="ef988-122">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="ef988-122">Click **Create**.</span></span>

## <a name="configure-load-balancing-rules"></a><span data-ttu-id="ef988-123">Configuración de las reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="ef988-123">Configure load balancing rules</span></span>

<span data-ttu-id="ef988-124">Después de hello creación de equilibrador de carga, vaya tooconfigure de recurso de equilibrador de carga de toohello lo.</span><span class="sxs-lookup"><span data-stu-id="ef988-124">After hello load balancer creation, navigate toohello load balancer resource tooconfigure it.</span></span>
<span data-ttu-id="ef988-125">Necesita tooconfigure primero un grupo de direcciones de back-end y un sondeo antes de configurar una regla de equilibrio de carga.</span><span class="sxs-lookup"><span data-stu-id="ef988-125">You need tooconfigure first a back-end address pool and a probe before configuring a load balancing rule.</span></span>

### <a name="step-1-configure-a-back-end-pool"></a><span data-ttu-id="ef988-126">Paso 1: Configuración de un grupo back-end</span><span class="sxs-lookup"><span data-stu-id="ef988-126">Step 1: Configure a back-end pool</span></span>

1. <span data-ttu-id="ef988-127">Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ef988-127">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="ef988-128">Hola **configuración** hoja, haga clic en **grupos back-end**.</span><span class="sxs-lookup"><span data-stu-id="ef988-128">In hello **Settings** blade, click **Backend pools**.</span></span>
3. <span data-ttu-id="ef988-129">Hola **grupos de direcciones de back-end** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="ef988-129">In hello **Backend address pools** blade, click **Add**.</span></span>
4. <span data-ttu-id="ef988-130">Hola **Agregar grupo back-end** hoja, escriba una **nombre** para el grupo de back-end de hello y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ef988-130">In hello **Add backend pool** blade, enter a **Name** for hello backend pool, and then click **OK**.</span></span>

### <a name="step-2-configure-a-probe"></a><span data-ttu-id="ef988-131">Paso 2: Configuración de un sondeo</span><span class="sxs-lookup"><span data-stu-id="ef988-131">Step 2: Configure a probe</span></span>

1. <span data-ttu-id="ef988-132">Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ef988-132">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="ef988-133">Hola **configuración** hoja, haga clic en **sondeos**.</span><span class="sxs-lookup"><span data-stu-id="ef988-133">In hello **Settings** blade, click **Probes**.</span></span>
3. <span data-ttu-id="ef988-134">Hola **sondeos** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="ef988-134">In hello **Probes**  blade, click **Add**.</span></span>
4. <span data-ttu-id="ef988-135">Hola **agregar sondeo** hoja, escriba una **nombre** para la sonda de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-135">In hello **Add probe** blade, enter a **Name** for hello probe.</span></span>
5. <span data-ttu-id="ef988-136">En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).</span><span class="sxs-lookup"><span data-stu-id="ef988-136">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="ef988-137">En **puerto**, especifique Hola puerto toouse al acceder a sondeo Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-137">Under **Port**, specify hello port toouse when accessing hello probe.</span></span>
7. <span data-ttu-id="ef988-138">En **ruta de acceso** (para HTTP sondeos solo), especifique hello toouse de ruta de acceso como un sondeo.</span><span class="sxs-lookup"><span data-stu-id="ef988-138">Under **Path** (for HTTP probes only), specify hello path toouse as a probe.</span></span>
8. <span data-ttu-id="ef988-139">En **intervalo** especificar con qué frecuencia tooprobe Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="ef988-139">Under **Interval** specify how frequently tooprobe hello application.</span></span>
9. <span data-ttu-id="ef988-140">En **umbral incorrecto**, especifique cuántos intentos deben generar un error antes de máquina virtual de back-end de hello está marcado como incorrecto.</span><span class="sxs-lookup"><span data-stu-id="ef988-140">Under **Unhealthy threshold**, specify how many attempts should fail before hello backend virtual machine is marked as unhealthy.</span></span>
10. <span data-ttu-id="ef988-141">Haga clic en **Aceptar** toocreate sondeo.</span><span class="sxs-lookup"><span data-stu-id="ef988-141">Click **OK** toocreate probe.</span></span>

### <a name="step-3-configure-load-balancing-rules"></a><span data-ttu-id="ef988-142">Paso 3: Configuración de las reglas de equilibrio de carga</span><span class="sxs-lookup"><span data-stu-id="ef988-142">Step 3: Configure load balancing rules</span></span>

1. <span data-ttu-id="ef988-143">Hola portal de Azure, haga clic en **examinar** > **equilibradores de carga**y, a continuación, haga clic en el equilibrador de carga de Hola que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ef988-143">In hello Azure portal, click **Browse** > **Load balancers**, and then click hello load balancer you created above.</span></span>
2. <span data-ttu-id="ef988-144">Hola **configuración** hoja, haga clic en **reglas de equilibrio de carga**.</span><span class="sxs-lookup"><span data-stu-id="ef988-144">In hello **Settings** blade, click **Load balancing rules**.</span></span>
3. <span data-ttu-id="ef988-145">Hola **reglas de equilibrio de carga** hoja, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="ef988-145">In hello **Load balancing rules** blade, click **Add**.</span></span>
4. <span data-ttu-id="ef988-146">Hola **regla de equilibrio de carga de agregar** hoja, escriba una **nombre** de regla de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-146">In hello **Add load balancing rule** blade, enter a **Name** for hello rule.</span></span>
5. <span data-ttu-id="ef988-147">En **Protocolo**, seleccione **HTTP** (para sitios web) o **TCP** (para otras aplicaciones basadas en TCP).</span><span class="sxs-lookup"><span data-stu-id="ef988-147">Under **Protocol**, select **HTTP** (for web sites) or **TCP** (for other TCP based applications).</span></span>
6. <span data-ttu-id="ef988-148">En **puerto**, especificar los clientes de puerto de hello conecten equilibrador de carga de hello tooin.</span><span class="sxs-lookup"><span data-stu-id="ef988-148">Under **Port**, specify hello port clients connect tooin hello load balancer.</span></span>
7. <span data-ttu-id="ef988-149">En **puerto back-end**, especifique Hola puerto toobe usa en el bloque de back-end de hello (normalmente, el puerto de equilibrador de carga de Hola y el puerto de back-end de Hola se Hola mismo).</span><span class="sxs-lookup"><span data-stu-id="ef988-149">Under **Backend port**, specify hello port toobe used in hello backend pool (usually, hello load balancer port and hello backend port are hello same).</span></span>
8. <span data-ttu-id="ef988-150">En **grupo back-end**, seleccione Hola back-end del grupo que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ef988-150">Under **Backend pool**, select hello backend pool you created above.</span></span>
9. <span data-ttu-id="ef988-151">En **persistencia de la sesión**, seleccione cómo desea que las sesiones toopersist.</span><span class="sxs-lookup"><span data-stu-id="ef988-151">Under **Session persistence**, select how you want sessions toopersist.</span></span>
10. <span data-ttu-id="ef988-152">En **tiempo de espera de inactividad (minutos)**, especifique el tiempo de espera de inactividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="ef988-152">Under **Idle timeout (minutes)**, specify hello idle timeout.</span></span>
11. <span data-ttu-id="ef988-153">En **IP flotante (Direct Server Return)**, haga clic en **Deshabilitado** o **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="ef988-153">Under **Floating IP (direct server return)**, click **Disabled** or **Enabled**.</span></span>
12. <span data-ttu-id="ef988-154">Haga clic en **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef988-154">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef988-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ef988-155">Next steps</span></span>

[<span data-ttu-id="ef988-156">Configuración de un modo de distribución del equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="ef988-156">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ef988-157">Configuración de opciones de tiempo de espera de inactividad de TCP para el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="ef988-157">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

