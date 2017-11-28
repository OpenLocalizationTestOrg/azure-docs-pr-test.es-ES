---
title: tutorial de servicio de contenedor de aaaAzure - Monitor Kubernetes | Documentos de Microsoft
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="25d76-104">Supervisión de un clúster de Kubernetes con Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="25d76-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="25d76-105">La supervisión de su clúster de Kubernetes y de los contenedores es fundamental, sobre todo al administrar un clúster de producción a escala con varias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="25d76-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="25d76-106">Puede sacar provecho de varias soluciones de supervisión de Kubernetes, tanto de Microsoft como de otros proveedores.</span><span class="sxs-lookup"><span data-stu-id="25d76-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="25d76-107">En este tutorial, supervisar el clúster Kubernetes mediante el uso de la solución de contenedores de hello en [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solución de administración de TI en la nube de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="25d76-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="25d76-108">(Hola solución de contenedores de OMS está en vista previa).</span><span class="sxs-lookup"><span data-stu-id="25d76-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="25d76-109">Este tutorial, parte siete de siete, trata Hola siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="25d76-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="25d76-110">Obtener la configuración del área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="25d76-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="25d76-111">Configurar agentes OMS en nodos de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="25d76-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="25d76-112">Obtener acceso a información de supervisión en el portal de OMS de Hola o portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25d76-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="25d76-113">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="25d76-113">Before you begin</span></span>

<span data-ttu-id="25d76-114">En los tutoriales anteriores, una aplicación se empaqueta en imágenes del contenedor, estas imágenes cargan tooAzure del registro de contenedor y un clúster de Kubernetes creado.</span><span class="sxs-lookup"><span data-stu-id="25d76-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="25d76-115">Si aún no ha hecho estos pasos y desearía toofollow a lo largo, devolver demasiado[Tutorial 1: crear imágenes del contenedor](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="25d76-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="25d76-116">Como mínimo, este tutorial requiere un clúster de Kubernetes con nodos de agente de Linux y una cuenta de Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="25d76-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="25d76-117">Si es necesario, regístrese para disfrutar de una [versión de evaluación gratuita de OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="25d76-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="25d76-118">Obtener la configuración del área de trabajo</span><span class="sxs-lookup"><span data-stu-id="25d76-118">Get Workspace settings</span></span>

<span data-ttu-id="25d76-119">Al acceder a hello [portal de OMS](https://mms.microsoft.com), vaya demasiado**configuración** > **orígenes conectados** > **servidores Linux**.</span><span class="sxs-lookup"><span data-stu-id="25d76-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="25d76-120">Allí, puede encontrar Hola *Id. de área de trabajo* y un principal o secundario *clave de área de trabajo*.</span><span class="sxs-lookup"><span data-stu-id="25d76-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="25d76-121">Tome nota de estos valores, que necesita tooset los agentes OMS en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="25d76-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="25d76-122">Configuración de agentes de OMS</span><span class="sxs-lookup"><span data-stu-id="25d76-122">Set up OMS agents</span></span>

<span data-ttu-id="25d76-123">Este es un tooset de archivo YAML los agentes OMS en nodos de clúster de Linux Hola.</span><span class="sxs-lookup"><span data-stu-id="25d76-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="25d76-124">Crea un recurso [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) de Kubernetes, que ejecuta un solo pod idéntico en cada nodo del clúster.</span><span class="sxs-lookup"><span data-stu-id="25d76-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="25d76-125">Hola DaemonSet recursos es ideal para implementar a un agente de supervisión.</span><span class="sxs-lookup"><span data-stu-id="25d76-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="25d76-126">Guardar Hola siguiente con el nombre el archivo de texto tooa `oms-daemonset.yaml`y reemplace los valores de marcador de posición de Hola para *myWorkspaceID* y *myWorkspaceKey* con la clave y el identificador de área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="25d76-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="25d76-127">(en producción, estos valores se pueden codificar como secretos).</span><span class="sxs-lookup"><span data-stu-id="25d76-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="25d76-128">Crear hello DaemonSet con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="25d76-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="25d76-129">toosee ese hello DaemonSet se crea, ejecute:</span><span class="sxs-lookup"><span data-stu-id="25d76-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="25d76-130">Salida es la siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="25d76-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="25d76-131">Después de que se ejecutan los agentes de hello, tarda varios minutos para los datos de hello tooingest y proceso OMS.</span><span class="sxs-lookup"><span data-stu-id="25d76-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="25d76-132">Acceso a los datos de supervisión</span><span class="sxs-lookup"><span data-stu-id="25d76-132">Access monitoring data</span></span>

<span data-ttu-id="25d76-133">Ver y analizar datos con hello de supervisión de contenedores OMS de hello [soluciones de contenedor](../../log-analytics/log-analytics-containers.md) en el portal de OMS de Hola u Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="25d76-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="25d76-134">solución de contenedor de hello tooinstall mediante hello [portal de OMS](https://mms.microsoft.com), vaya demasiado**Galería de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="25d76-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="25d76-135">A continuación, agregue **Solución de contenedor**.</span><span class="sxs-lookup"><span data-stu-id="25d76-135">Then add **Container Solution**.</span></span> <span data-ttu-id="25d76-136">O bien, agregar soluciones de contenedores de Hola de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="25d76-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="25d76-137">En el portal de OMS de hello, busque un **contenedores** mosaico de resumen en el panel de OMS Hola.</span><span class="sxs-lookup"><span data-stu-id="25d76-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="25d76-138">Haga clic en el icono de Hola para obtener detalles como: eventos de contenedor, errores, estado, inventario de la imagen y uso de CPU y memoria.</span><span class="sxs-lookup"><span data-stu-id="25d76-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="25d76-139">Para obtener información más detallada, haga clic en una fila de cualquier icono o realice una [búsqueda de registros](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="25d76-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Panel de contenedores en el Portal de OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="25d76-141">De forma similar, en hello portal de Azure, vaya demasiado**análisis de registros** y seleccione el nombre del área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="25d76-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="25d76-142">Hola toosee **contenedores** mosaico de resumen, haga clic en **soluciones** > **contenedores**.</span><span class="sxs-lookup"><span data-stu-id="25d76-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="25d76-143">toosee detalles, haga clic en el icono de Hola.</span><span class="sxs-lookup"><span data-stu-id="25d76-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="25d76-144">Vea hello [documentación de Azure Log Analytics](../../log-analytics/index.md) para obtener instrucciones detalladas para consultar y analizar los datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="25d76-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25d76-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25d76-145">Next steps</span></span>

<span data-ttu-id="25d76-146">En este tutorial, se ha supervisado el clúster de Kubernetes con OMS.</span><span class="sxs-lookup"><span data-stu-id="25d76-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="25d76-147">Estas son las tareas que se han tratado:</span><span class="sxs-lookup"><span data-stu-id="25d76-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="25d76-148">Obtener la configuración del área de trabajo de OMS</span><span class="sxs-lookup"><span data-stu-id="25d76-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="25d76-149">Configurar agentes OMS en nodos de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="25d76-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="25d76-150">Obtener acceso a información de supervisión en el portal de OMS de Hola o portal de Azure</span><span class="sxs-lookup"><span data-stu-id="25d76-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="25d76-151">Siga este toosee vínculo pregeneradas ejemplos de script para el servicio de contenedor.</span><span class="sxs-lookup"><span data-stu-id="25d76-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25d76-152">Ejemplos de scripts de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="25d76-152">Azure Container Service script samples</span></span>](cli-samples.md)
