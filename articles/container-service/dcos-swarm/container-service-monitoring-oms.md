---
title: "clúster de Azure DC/OS aaaMonitor - administración de operaciones | Documentos de Microsoft"
description: "Uso de Microsoft Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="0e003-103">Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="0e003-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="0e003-104">Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="0e003-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="0e003-105">Solución de contenedor es una solución de análisis de registros de OMS, que le ayuda a ver el inventario de contenedor de hello, rendimiento y los registros en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="0e003-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="0e003-106">Puede auditar, solucionar los contenedores viendo Hola registros en una ubicación centralizada y encontrar con ruido consumiendo exceso contenedor en un host.</span><span class="sxs-lookup"><span data-stu-id="0e003-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="0e003-107">Para obtener más información acerca de la solución de contenedor, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="0e003-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="0e003-108">Configuración de OMS desde el universo de Hola DC/OS</span><span class="sxs-lookup"><span data-stu-id="0e003-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="0e003-109">Este artículo se supone que ha configurado un controlador de dominio/OS y ha implementado aplicaciones de contenedor de web simple en el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e003-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="0e003-110">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="0e003-110">Pre-requisite</span></span>
- <span data-ttu-id="0e003-111">[Suscripción de Microsoft Azure](https://azure.microsoft.com/free/) (se puede obtener de gratis).</span><span class="sxs-lookup"><span data-stu-id="0e003-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="0e003-112">Configuración de área de trabajo de Microsoft OMS (consulte el "paso 3" a continuación)</span><span class="sxs-lookup"><span data-stu-id="0e003-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="0e003-113">[CLI de DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) instalada.</span><span class="sxs-lookup"><span data-stu-id="0e003-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="0e003-114">En el panel de DC/OS hello, haga clic en el universo de y busque 'OMS' tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0e003-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="0e003-115">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="0e003-115">Click **Install**.</span></span> <span data-ttu-id="0e003-116">Aparecerá un pop con información de versión OMS de Hola y un **Instalar paquete** o **instalación avanzada** botón.</span><span class="sxs-lookup"><span data-stu-id="0e003-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="0e003-117">Al hacer clic en **instalación avanzada**, lo que provoca toohello **propiedades de configuración específicas de OMS** página.</span><span class="sxs-lookup"><span data-stu-id="0e003-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="0e003-118">En este caso, se le pedirá hello tooenter `wsid` (Hola Id. de área de trabajo OMS) y `wskey` (Hola OMS clave principal para el Id. de área de trabajo de hello).</span><span class="sxs-lookup"><span data-stu-id="0e003-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="0e003-119">tooget ambos `wsid` y `wskey` necesita una cuenta OMS en toocreate <https://mms.microsoft.com>. Siga Hola pasos toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="0e003-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="0e003-120">Una vez haya terminado de crear cuenta de hello, tendrá que tooobtain su `wsid` y `wskey` haciendo clic en **configuración**, a continuación, **orígenes conectados**y, a continuación, **servidores Linux** , tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="0e003-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="0e003-121">Seleccionar Hola número OMS instancias que desee y haga clic en botón de hello 'Revisar e instalar'.</span><span class="sxs-lookup"><span data-stu-id="0e003-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="0e003-122">Por lo general, le interesará toohave Hola número de OMS instancias toohello igual de la máquina virtual tiene en el clúster de agente.</span><span class="sxs-lookup"><span data-stu-id="0e003-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="0e003-123">Agente de OMS para Linux es instala como contenedores individuales en cada máquina virtual que desea toocollect información de supervisión y la información del registro.</span><span class="sxs-lookup"><span data-stu-id="0e003-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="0e003-124">Configuración de un panel de OMS</span><span class="sxs-lookup"><span data-stu-id="0e003-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="0e003-125">Una vez que ha instalado Hola agente de OMS para Linux en máquinas virtuales de hello, el siguiente paso es tooset de panel de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="0e003-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="0e003-126">Hay dos toodo formas esto: Portal de OMS o Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="0e003-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="0e003-127">Portal de OMS</span><span class="sxs-lookup"><span data-stu-id="0e003-127">OMS Portal</span></span> 

<span data-ttu-id="0e003-128">Inicie sesión en el portal de OMS toohello (<https://mms.microsoft.com>) y vaya toohello **Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="0e003-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="0e003-129">Una vez que esté en hello **Galería de soluciones**, seleccione **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="0e003-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="0e003-130">Una vez que haya seleccionado Hola soluciones de contenedor, verá de mosaico en la página del panel de información general de OMS Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="0e003-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="0e003-131">Una vez que se indizan los datos del contenedor de hello ingestión, verá icono Hola rellenado con información sobre los iconos de vista de la solución.</span><span class="sxs-lookup"><span data-stu-id="0e003-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="0e003-132">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="0e003-132">Azure Portal</span></span> 

<span data-ttu-id="0e003-133">Portal de inicio de sesión tooAzure en <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="0e003-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="0e003-134">Vaya a **Marketplace**, seleccione **Supervisión y administración** y haga clic en **See All** (Ver todo).</span><span class="sxs-lookup"><span data-stu-id="0e003-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="0e003-135">A continuación, escriba `containers` en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0e003-135">Then Type `containers` in search.</span></span> <span data-ttu-id="0e003-136">Verá "contenedores" en los resultados de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="0e003-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="0e003-137">Seleccione **Contenedores** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e003-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="0e003-138">Cuando haga clic en **Crear**, le preguntará por el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0e003-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="0e003-139">Seleccione el área de trabajo o si no tiene uno, cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="0e003-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="0e003-140">Una vez que haya seleccionado el área de trabajo, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="0e003-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="0e003-141">Para obtener más información acerca de hello soluciones de contenedor de OMS, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="0e003-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="0e003-142">¿Cómo tooscale agente de OMS con ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="0e003-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="0e003-143">En caso de que necesita toohave instalado el agente de OMS en el número de nodos real de Hola o se escalado VMSS mediante la adición de más máquinas virtuales, puede hacerlo mediante el escalado hello `msoms` servicio.</span><span class="sxs-lookup"><span data-stu-id="0e003-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="0e003-144">Puede ir tooMarathon o hello pestaña servicios de interfaz de usuario de controlador de dominio/OS y escalar verticalmente el número de nodos.</span><span class="sxs-lookup"><span data-stu-id="0e003-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="0e003-145">Esta acción implementará nodos tooother que aún no ha implementado a agente de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="0e003-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="0e003-146">Desinstalación de MS OMS</span><span class="sxs-lookup"><span data-stu-id="0e003-146">Uninstall MS OMS</span></span>

<span data-ttu-id="0e003-147">toouninstall MS OMS escriba Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="0e003-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="0e003-148">¡Queremos saber!</span><span class="sxs-lookup"><span data-stu-id="0e003-148">Let us know!!!</span></span>
<span data-ttu-id="0e003-149">¿Qué funciona?</span><span class="sxs-lookup"><span data-stu-id="0e003-149">What works?</span></span> <span data-ttu-id="0e003-150">¿Qué falta?</span><span class="sxs-lookup"><span data-stu-id="0e003-150">What is missing?</span></span> <span data-ttu-id="0e003-151">¿Qué más ¿necesita para este toobe útil para usted?</span><span class="sxs-lookup"><span data-stu-id="0e003-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="0e003-152">Háganos saber en <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="0e003-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e003-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0e003-153">Next steps</span></span>

 <span data-ttu-id="0e003-154">Ahora que ha configurado OMS toomonitor los contenedores,[ver el panel de contenedor](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="0e003-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
