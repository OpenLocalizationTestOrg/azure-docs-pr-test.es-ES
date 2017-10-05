---
title: "Tutorial de Azure Container Service: supervisión de Kubernetes | Microsoft Docs"
description: "Tutorial de Azure Container Service: supervisión de Kubernetes con Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Microservicios, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="e4ba2-104">Supervisión de un clúster de Kubernetes con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="e4ba2-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="e4ba2-105">La supervisión de su clúster de Kubernetes y de los contenedores es fundamental, sobre todo al administrar un clúster de producción a escala con varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="e4ba2-106">Puede sacar provecho de varias soluciones de supervisión de Kubernetes, tanto de Microsoft como de otros proveedores.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="e4ba2-107">En este tutorial, se supervisa un clúster de Kubernetes mediante la solución Containers de [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), la solución de administración de TI en la nube de Microsoft</span><span class="sxs-lookup"><span data-stu-id="e4ba2-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="e4ba2-108">(la solución Containers de OMS está en versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="e4ba2-109">Este tutorial, la séptima parte de siete, trata las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="e4ba2-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4ba2-110">Obtener la configuración del área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="e4ba2-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="e4ba2-111">Configurar agentes OMS en los nodos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e4ba2-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="e4ba2-112">Acceder a la información de supervisión en el Portal de OMS o en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4ba2-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e4ba2-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="e4ba2-113">Before you begin</span></span>

<span data-ttu-id="e4ba2-114">En los tutoriales anteriores se empaquetaba una aplicación en imágenes de contenedor, se cargaban estas imágenes en Azure Container Registry y se creó un clúster de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="e4ba2-115">Si no ha realizado estos pasos, pero desea continuar, vuelva al tutorial [Create container images to be used with Azure Container Service](./container-service-tutorial-kubernetes-prepare-app.md) (Creación de las imágenes de contenedor que se usan con Azure Container Service).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="e4ba2-116">Como mínimo, este tutorial requiere un clúster de Kubernetes con nodos de agente de Linux y una cuenta de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="e4ba2-117">Si es necesario, regístrese para disfrutar de una [versión de evaluación gratuita de OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="e4ba2-118">Obtener la configuración del área de trabajo</span><span class="sxs-lookup"><span data-stu-id="e4ba2-118">Get Workspace settings</span></span>

<span data-ttu-id="e4ba2-119">Cuando pueda acceder al [Portal de OMS](https://mms.microsoft.com), vaya a **Configuración** > **Orígenes conectados** > **Servidores Linux**.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="e4ba2-120">Ahí puede encontrar el *identificador del área de trabajo* y una *clave del área de trabajo* principal o secundaria.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="e4ba2-121">Anote de estos valores, ya que se necesitan para configurar agentes de OMS en el clúster.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="e4ba2-122">Configuración de agentes de OMS</span><span class="sxs-lookup"><span data-stu-id="e4ba2-122">Set up OMS agents</span></span>

<span data-ttu-id="e4ba2-123">Este es un archivo YAML para configurar agentes de OMS en los nodos de clúster de Linux.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="e4ba2-124">Crea un recurso [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) de Kubernetes, que ejecuta un solo pod idéntico en cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="e4ba2-125">El recurso DaemonSet es ideal para implementar a un agente de supervisión.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="e4ba2-126">Guarde el siguiente texto en un archivo denominado `oms-daemonset.yaml` y reemplace los valores de marcador de posición de *myWorkspaceID* y *myWorkspaceKey* con la clave y el identificador del área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="e4ba2-127">(en producción, estos valores se pueden codificar como secretos).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="e4ba2-128">Cree el recurso DaemonSet con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e4ba2-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="e4ba2-129">Para ver que se ha creado, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e4ba2-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="e4ba2-130">La salida es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e4ba2-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="e4ba2-131">Una vez que se ejecutan los agentes, OMS tarda varios minutos en ingerir y procesar los datos.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="e4ba2-132">Acceso a los datos de supervisión</span><span class="sxs-lookup"><span data-stu-id="e4ba2-132">Access monitoring data</span></span>

<span data-ttu-id="e4ba2-133">Vea y analice los datos de supervisión del contenedor de OMS con la [solución Containers](../../log-analytics/log-analytics-containers.md) en el Portal de OMS o en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="e4ba2-134">Para instalar dicha solución desde el [Portal de OMS](https://mms.microsoft.com), vaya a **Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="e4ba2-135">A continuación, agregue **Solución de contenedor**.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-135">Then add **Container Solution**.</span></span> <span data-ttu-id="e4ba2-136">Como alternativa, agregue la solución Containers de [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="e4ba2-137">En el portal de OMS, busque un icono de resumen de **Containers** en el panel de OMS.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="e4ba2-138">Haga clic en el icono para obtener la siguiente información: eventos de contenedor, errores, estado, inventario de la imagen y uso de la CPU y la memoria.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="e4ba2-139">Para obtener información más detallada, haga clic en una fila de cualquier icono o realice una [búsqueda de registros](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="e4ba2-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Panel de contenedores en el Portal de OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="e4ba2-141">En Azure Portal, vaya a **Log Analytics** y seleccione el nombre de su área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="e4ba2-142">Para ver el icono de resumen de **Containers**, haga clic en **Soluciones** > **Containers**.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="e4ba2-143">Para ver los detalles, haga clic en el icono.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-143">To see details, click the tile.</span></span>

<span data-ttu-id="e4ba2-144">Consulte la [documentación de Azure Log Analytics](../../log-analytics/index.md) para obtener una guía detallada para consultar y analizar los datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4ba2-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e4ba2-145">Next steps</span></span>

<span data-ttu-id="e4ba2-146">En este tutorial, se ha supervisado el clúster de Kubernetes con OMS.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="e4ba2-147">Estas son las tareas que se han tratado:</span><span class="sxs-lookup"><span data-stu-id="e4ba2-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4ba2-148">Obtener la configuración del área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="e4ba2-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="e4ba2-149">Configurar agentes OMS en los nodos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e4ba2-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="e4ba2-150">Acceder a la información de supervisión en el Portal de OMS o en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e4ba2-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="e4ba2-151">Siga este vínculo para ver ejemplos de scripts del servicio Container creados previamente.</span><span class="sxs-lookup"><span data-stu-id="e4ba2-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4ba2-152">Ejemplos de scripts de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e4ba2-152">Azure Container Service script samples</span></span>](cli-samples.md)
