---
title: "Supervisión de un clúster de Azure DC/OS - Operations Management | Microsoft Docs"
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
ms.openlocfilehash: 9b8f96b34b53982c469273a3df9751ceb7930d60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="b4411-103">Uso de Operations Management Suite para supervisar un clúster DC/OS de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="b4411-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="b4411-104">Microsoft Operations Management Suite (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura local y en la nube.</span><span class="sxs-lookup"><span data-stu-id="b4411-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="b4411-105">La solución de contenedor es una solución de Log Analytics de OMS, que le permite ver el inventario de contenedor, el rendimiento y los registros en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="b4411-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="b4411-106">Puede auditar contenedores y solucionar problemas de los mismos mediante la visualización de los registros en una ubicación centralizada, así como encontrar contenedores ruidosos con un consumo excesivo.</span><span class="sxs-lookup"><span data-stu-id="b4411-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="b4411-107">Para más información sobre la solución de contenedor, consulte [Solución Containers (versión preliminar) en Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="b4411-108">Configuración de OMS desde el universo de DC/OS</span><span class="sxs-lookup"><span data-stu-id="b4411-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="b4411-109">En este artículo se supone que ha configurado un DC/OS y ha implementado aplicaciones de contenedor web simples en el clúster.</span><span class="sxs-lookup"><span data-stu-id="b4411-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="b4411-110">Requisito previo</span><span class="sxs-lookup"><span data-stu-id="b4411-110">Pre-requisite</span></span>
- <span data-ttu-id="b4411-111">[Suscripción de Microsoft Azure](https://azure.microsoft.com/free/) (se puede obtener de gratis).</span><span class="sxs-lookup"><span data-stu-id="b4411-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="b4411-112">Configuración de área de trabajo de Microsoft OMS (consulte el "paso 3" a continuación)</span><span class="sxs-lookup"><span data-stu-id="b4411-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="b4411-113">[CLI de DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) instalada.</span><span class="sxs-lookup"><span data-stu-id="b4411-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="b4411-114">En el panel de DC/OS, haga clic en Universo y busque ‘OMS’ tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b4411-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="b4411-115">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="b4411-115">Click **Install**.</span></span> <span data-ttu-id="b4411-116">Verá un mensaje emergente con la información de versión OMS y un botón **Instalar paquete** o **Advanced Installation** (Instalación avanzada).</span><span class="sxs-lookup"><span data-stu-id="b4411-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="b4411-117">Al hacer clic en **Instalación avanzada**, se abre la página **OMS specific configuration properties** (Propiedades de configuración específicas de OMS).</span><span class="sxs-lookup"><span data-stu-id="b4411-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="b4411-118">Aquí se le pedirá que escriba `wsid` (el identificador del área de trabajo de OMS) y `wskey` (la clave principal de OMS para el identificador del área de trabajo).</span><span class="sxs-lookup"><span data-stu-id="b4411-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="b4411-119">Para obtener ambos `wsid` y `wskey` debe crear una cuenta OMS en <https://mms.microsoft.com>. Siga los pasos para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="b4411-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="b4411-120">Una vez que haya terminado de crear la cuenta, deberá obtener su `wsid` y `wskey` haciendo clic en **Configuración**, luego en **Orígenes conectados** y, por último, en **Servidores Linux**, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="b4411-120">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="b4411-121">Seleccione el número de instancias de OMS que desee y haga clic en el botón 'Revisar e instalar'.</span><span class="sxs-lookup"><span data-stu-id="b4411-121">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="b4411-122">Por lo general, querrá tener el mismo número de instancias de OMS que VM hay en el clúster de agente.</span><span class="sxs-lookup"><span data-stu-id="b4411-122">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="b4411-123">El agente de OMS para Linux se instala como contenedores individuales en cada VM que quiere para recopilar información de supervisión e inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="b4411-123">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="b4411-124">Configuración de un panel de OMS</span><span class="sxs-lookup"><span data-stu-id="b4411-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="b4411-125">Una vez que instalado al agente de OMS para Linux en las VM, el siguiente paso es configurar el panel de OMS.</span><span class="sxs-lookup"><span data-stu-id="b4411-125">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="b4411-126">Hay dos maneras de hacerlo: mediante el portal de OMS o mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b4411-126">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="b4411-127">Portal de OMS</span><span class="sxs-lookup"><span data-stu-id="b4411-127">OMS Portal</span></span> 

<span data-ttu-id="b4411-128">Inicie sesión en el portal de OMS (<https://mms.microsoft.com>) y vaya a la **Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="b4411-128">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="b4411-129">Cuando se encuentre en la **Galería de soluciones**, seleccione **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="b4411-129">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="b4411-130">Una vez que haya seleccionado la solución de contenedor, verá el icono en la página OMS Overview Dashboard (Panel de información general de OMS).</span><span class="sxs-lookup"><span data-stu-id="b4411-130">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="b4411-131">Una vez indizador los datos de contenedor ingeridos, verá el icono rellenado con información sobre los iconos de vista de la solución.</span><span class="sxs-lookup"><span data-stu-id="b4411-131">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="b4411-132">Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b4411-132">Azure Portal</span></span> 

<span data-ttu-id="b4411-133">Inicie sesión en Azure Portal en <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="b4411-133">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="b4411-134">Vaya a **Marketplace**, seleccione **Supervisión y administración** y haga clic en **See All** (Ver todo).</span><span class="sxs-lookup"><span data-stu-id="b4411-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="b4411-135">A continuación, escriba `containers` en la búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b4411-135">Then Type `containers` in search.</span></span> <span data-ttu-id="b4411-136">Verá "contenedores" en los resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="b4411-136">You will see "containers" in the search results.</span></span> <span data-ttu-id="b4411-137">Seleccione **Contenedores** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b4411-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="b4411-138">Cuando haga clic en **Crear**, le preguntará por el área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b4411-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="b4411-139">Seleccione el área de trabajo o si no tiene uno, cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="b4411-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="b4411-140">Una vez que haya seleccionado el área de trabajo, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="b4411-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="b4411-141">Para más información sobre la solución de contenedor de OMS, consulte [Solución Containers (versión preliminar) en Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-141">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="b4411-142">Escalado del agente de OMS con ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="b4411-142">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="b4411-143">En caso de que se necesite tener instalado el agente de OMS o esté escalando verticalmente VMSS mediante la incorporación de más VM, puede hacerlo mediante el escalado del servicio `msoms`.</span><span class="sxs-lookup"><span data-stu-id="b4411-143">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="b4411-144">Puede ir a Marathon o la pestaña de servicios de IU de DC/OS y escalar verticalmente el número de nodos.</span><span class="sxs-lookup"><span data-stu-id="b4411-144">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="b4411-145">Esto se implementará en otros nodos que aún no han implementado el agente de OMS.</span><span class="sxs-lookup"><span data-stu-id="b4411-145">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="b4411-146">Desinstalación de MS OMS</span><span class="sxs-lookup"><span data-stu-id="b4411-146">Uninstall MS OMS</span></span>

<span data-ttu-id="b4411-147">Para desinstalar MS OMS escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="b4411-147">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="b4411-148">¡Queremos saber!</span><span class="sxs-lookup"><span data-stu-id="b4411-148">Let us know!!!</span></span>
<span data-ttu-id="b4411-149">¿Qué funciona?</span><span class="sxs-lookup"><span data-stu-id="b4411-149">What works?</span></span> <span data-ttu-id="b4411-150">¿Qué falta?</span><span class="sxs-lookup"><span data-stu-id="b4411-150">What is missing?</span></span> <span data-ttu-id="b4411-151">¿Qué más necesita para esto para que sea útil para usted?</span><span class="sxs-lookup"><span data-stu-id="b4411-151">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="b4411-152">Háganos saber en <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="b4411-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4411-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4411-153">Next steps</span></span>

 <span data-ttu-id="b4411-154">Ahora que ha configurado OMS para supervisar los contenedores,[vea el panel de contenedor](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b4411-154">Now that you have set up OMS to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
