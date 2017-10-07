---
title: "clúster de Azure Kubernetes aaaMonitor - administración de operaciones | Documentos de Microsoft"
description: "Supervisión de un clúster de Kubernetes en Azure Container Service utilizando Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="73dde-103">Supervisión de un clúster de Azure Container Service con Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="73dde-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73dde-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="73dde-104">Prerequisites</span></span>
<span data-ttu-id="73dde-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="73dde-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="73dde-106">También se supone que dispone de hello `az` cli de Azure y `kubectl` herramientas instaladas.</span><span class="sxs-lookup"><span data-stu-id="73dde-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="73dde-107">Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="73dde-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="73dde-108">Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="73dde-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="73dde-109">Como alternativa, puede usar [Shell en la nube de Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tiene hello `az` cli de Azure y `kubectl` herramientas ya instaladas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="73dde-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="73dde-110">Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="73dde-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="73dde-111">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="73dde-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="73dde-112">tootest si tiene claves kubernetes instaladas en la herramienta kubectl puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="73dde-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="73dde-113">Si hello por encima de los errores de comando out, necesita claves de clúster de tooinstall kubernetes en la herramienta kubectl.</span><span class="sxs-lookup"><span data-stu-id="73dde-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="73dde-114">Puede hacerlo con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="73dde-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="73dde-115">Supervisión de contenedores con Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="73dde-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="73dde-116">Microsoft Operations Management (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local.</span><span class="sxs-lookup"><span data-stu-id="73dde-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="73dde-117">Solución de contenedor es una solución de análisis de registros de OMS, que le ayuda a ver el inventario de contenedor de hello, rendimiento y los registros en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="73dde-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="73dde-118">Puede auditar, solucionar los contenedores viendo Hola registros en una ubicación centralizada y encontrar con ruido consumiendo exceso contenedor en un host.</span><span class="sxs-lookup"><span data-stu-id="73dde-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="73dde-119">Para obtener más información acerca de la solución de contenedor, consulte toothe [análisis de registros de solución de contenedor](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="73dde-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="73dde-120">Instalación de OMS en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="73dde-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="73dde-121">Obtención de la clave y el identificador de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="73dde-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="73dde-122">Para el servicio OMS agente tootalk toohello Hola debe toobe configurado con un identificador de área de trabajo y una clave de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="73dde-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="73dde-123">cuenta de Id. de área de trabajo de hello tooget y clave necesita toocreate un OMS <https://mms.microsoft.com>. Siga Hola pasos toocreate una cuenta.</span><span class="sxs-lookup"><span data-stu-id="73dde-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="73dde-124">Una vez que haya terminado de crear cuenta de hello, necesita tooobtain el identificador y la clave haciendo clic en **configuración**, a continuación, **orígenes conectados**y, a continuación, **servidores Linux**, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="73dde-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="73dde-125">Instalar a agente OMS de hello mediante un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="73dde-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="73dde-126">DaemonSets usan Kubernetes toorun una sola instancia de un contenedor en cada host de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="73dde-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="73dde-127">Son perfectos para ejecutar agentes de supervisión.</span><span class="sxs-lookup"><span data-stu-id="73dde-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="73dde-128">Aquí es hello [archivo DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="73dde-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="73dde-129">Guárdelo con el nombre archivo tooa `oms-daemonset.yaml` y reemplazar los valores de marcador de posición de Hola para `WSID` y `KEY` con el Id. de área de trabajo y la clave en el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="73dde-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="73dde-130">Cuando haya agregado su Id. de área de trabajo y la configuración de DaemonSet toohello clave, puede instalar agente OMS de hello en el clúster con hello `kubectl` herramienta de línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="73dde-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="73dde-131">Instalar agente OMS Hola usar un secreto Kubernetes</span><span class="sxs-lookup"><span data-stu-id="73dde-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="73dde-132">tooprotect el Id. de área de trabajo OMS y la clave que se puede usar Kubernetes secreto como parte del archivo DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="73dde-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="73dde-133">Copiar script de Hola, archivo de plantilla secreto y Hola archivo DaemonSet YAML (de [repositorio](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) y asegúrese de que se encuentren en hello mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="73dde-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="73dde-134">Script de generación de secretos: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="73dde-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="73dde-135">Plantilla de secretos: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="73dde-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="73dde-136">Archivo DaemonSet YAML: omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="73dde-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="73dde-137">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="73dde-137">Run hello script.</span></span> <span data-ttu-id="73dde-138">script de Hola le pedirá Hola Id. de área de trabajo de OMS y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="73dde-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="73dde-139">Por favor, inserte y script de Hola creará un archivo yaml secreto para que pueda ejecutar.</span><span class="sxs-lookup"><span data-stu-id="73dde-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="73dde-140">Crear pod de secretos de hello ejecutando Hola siguiente:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="73dde-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="73dde-141">toocheck, ejecute hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="73dde-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="73dde-142">Ejecute ``` kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent</span><span class="sxs-lookup"><span data-stu-id="73dde-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="73dde-143">Conclusión</span><span class="sxs-lookup"><span data-stu-id="73dde-143">Conclusion</span></span>
<span data-ttu-id="73dde-144">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="73dde-144">That's it!</span></span> <span data-ttu-id="73dde-145">Después de unos minutos, debe tener datos toosee pueda fluir tooyour panel de OMS.</span><span class="sxs-lookup"><span data-stu-id="73dde-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
