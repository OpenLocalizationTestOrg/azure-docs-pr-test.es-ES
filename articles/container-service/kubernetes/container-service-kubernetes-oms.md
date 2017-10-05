---
title: "Supervisión de un clúster de Azure Kubernetes - Operations Management | Microsoft Docs"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="a069f-103">Supervisión de un clúster de Azure Container Service con Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="a069f-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a069f-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="a069f-104">Prerequisites</span></span>
<span data-ttu-id="a069f-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a069f-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="a069f-106">También se da por supuesto que tiene la CLI de Azure `az` y las herramientas de `kubectl` instaladas.</span><span class="sxs-lookup"><span data-stu-id="a069f-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="a069f-107">Puede probar si tiene la herramienta `az` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="a069f-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="a069f-108">Si no tiene la herramienta `az` instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="a069f-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="a069f-109">Como alternativa, puede usar [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tiene la `az` CLI de Azure y `kubectl` herramientas ya instaladas.</span><span class="sxs-lookup"><span data-stu-id="a069f-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="a069f-110">Puede probar si tiene la herramienta `kubectl` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="a069f-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="a069f-111">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="a069f-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="a069f-112">Para probar si tiene claves de kubernetes instaladas en la herramienta de kubectl, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="a069f-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="a069f-113">Si aparecen los errores anteriores de comando, debe instalar las claves de clúster de kubernetes en la herramienta de kubectl.</span><span class="sxs-lookup"><span data-stu-id="a069f-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="a069f-114">Para ello, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="a069f-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="a069f-115">Supervisión de contenedores con Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="a069f-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="a069f-116">Microsoft Operations Management (OMS) es la solución de administración de TI basada en la nube de Microsoft que le ayuda a administrar y proteger su infraestructura en la nube y local.</span><span class="sxs-lookup"><span data-stu-id="a069f-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="a069f-117">La solución de contenedor es una solución de Log Analytics de OMS, que le permite ver el inventario de contenedor, el rendimiento y los registros en una sola ubicación.</span><span class="sxs-lookup"><span data-stu-id="a069f-117">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="a069f-118">Puede auditar contenedores y solucionar problemas de los mismos mediante la visualización de los registros en una ubicación centralizada, así como encontrar contenedores ruidosos con un consumo excesivo.</span><span class="sxs-lookup"><span data-stu-id="a069f-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="a069f-119">Para más información sobre la solución de contenedor, consulte [Solución Containers (versión preliminar) en Log Analytics](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="a069f-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="a069f-120">Instalación de OMS en Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a069f-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="a069f-121">Obtención de la clave y el identificador de área de trabajo</span><span class="sxs-lookup"><span data-stu-id="a069f-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="a069f-122">Para que el agente OMS se comunique con el servicio tiene que configurarse con un identificador de área de trabajo y una clave de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="a069f-122">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="a069f-123">Para obtener ambos tiene que crear una cuenta OMS en <https://mms.microsoft.com>. Siga los pasos para crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="a069f-123">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="a069f-124">Una vez que haya terminado de crear la cuenta, tendrá que obtener su identificador y su clave haciendo clic en **Configuración**, luego en **Connected Sources** (Orígenes conectados) y, por último, en **Servidores Linux**, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a069f-124">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="a069f-125">Instalación del agente OMS con un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="a069f-125">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="a069f-126">Kubernetes utiliza DaemonSets para ejecutar una única instancia de un contenedor en cada host del clúster.</span><span class="sxs-lookup"><span data-stu-id="a069f-126">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="a069f-127">Son perfectos para ejecutar agentes de supervisión.</span><span class="sxs-lookup"><span data-stu-id="a069f-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="a069f-128">Este es el [archivo DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="a069f-128">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="a069f-129">Guárdelo en un archivo denominado `oms-daemonset.yaml` y reemplace los valores de marcador de posición de `WSID` y `KEY` con el identificador y la clave del área de trabajo en el archivo.</span><span class="sxs-lookup"><span data-stu-id="a069f-129">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="a069f-130">Cuando haya agregado la clave y el identificador de área de trabajo a la configuración de DaemonSet, puede instalar el agente de OMS en el clúster con la herramienta de línea de comandos `kubectl`:</span><span class="sxs-lookup"><span data-stu-id="a069f-130">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="a069f-131">Instalación del agente de OMS con un Secreto de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a069f-131">Installing the OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="a069f-132">Para proteger el identificador del área de trabajo de OMS y la clave, se puede usar un Secreto de Kubernetes como parte del archivo DaemonSet YAML.</span><span class="sxs-lookup"><span data-stu-id="a069f-132">To protect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="a069f-133">Copie el script, el archivo de plantilla secreto y el archivo DaemonSet YAML (desde el [repositorio](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) y asegúrese de que estén en el mismo directorio.</span><span class="sxs-lookup"><span data-stu-id="a069f-133">Copy the script, secret template file and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span> 
      - <span data-ttu-id="a069f-134">Script de generación de secretos: secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="a069f-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="a069f-135">Plantilla de secretos: secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="a069f-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="a069f-136">Archivo DaemonSet YAML: omsagent-ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="a069f-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="a069f-137">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="a069f-137">Run the script.</span></span> <span data-ttu-id="a069f-138">El script le pedirá el identificador del área de trabajo de OMS y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="a069f-138">The script will ask for the OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="a069f-139">Inserte esos datos y el script creará un archivo yaml secreto para que pueda ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="a069f-139">Please insert that and the script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="a069f-140">Ejecute lo siguiente para crear el pod de secretos: ``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="a069f-140">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="a069f-141">Para comprobarlo, ejecute lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a069f-141">To check, run the following:</span></span> 

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
 
  - <span data-ttu-id="a069f-142">Ejecute ``` kubectl create -f omsagent-ds-secrets.yaml ``` para crear el daemon-set de omsagent</span><span class="sxs-lookup"><span data-stu-id="a069f-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="a069f-143">Conclusión</span><span class="sxs-lookup"><span data-stu-id="a069f-143">Conclusion</span></span>
<span data-ttu-id="a069f-144">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="a069f-144">That's it!</span></span> <span data-ttu-id="a069f-145">Pasados unos minutos, debería ver los datos que fluyen en el panel OMS.</span><span class="sxs-lookup"><span data-stu-id="a069f-145">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>
