---
title: "contenedores de aaaDeploy con timón en Azure Kubernetes | Documentos de Microsoft"
description: "Utilizar contenedores de toodeploy de herramienta de hello timón empaquetado en un clúster de Kubernetes en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="6877c-103">Utilizar contenedores de toodeploy de timón en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6877c-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="6877c-104">[Timón](https://github.com/kubernetes/helm/) es una herramienta de empaquetado de código abierto que le ayuda a instalar y administrar el ciclo de vida de Hola de Kubernetes aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6877c-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="6877c-105">Administradores de paquetes tooLinux similar como Apt get y Yum, timón es toomanage usado Kubernetes gráficos, que son paquetes de recursos de Kubernetes preconfigurados.</span><span class="sxs-lookup"><span data-stu-id="6877c-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="6877c-106">Este artículo muestra cómo implementa toowork con timón en un clúster de Kubernetes en el servicio de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="6877c-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="6877c-107">Helm tiene dos componentes:</span><span class="sxs-lookup"><span data-stu-id="6877c-107">Helm has two components:</span></span> 
* <span data-ttu-id="6877c-108">Hola **timón CLI** es un cliente que se ejecuta en el equipo local o en la nube de Hola</span><span class="sxs-lookup"><span data-stu-id="6877c-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="6877c-109">**Caña** es un servidor que se ejecuta en hello Kubernetes clúster y administra Hola del ciclo de vida de las aplicaciones Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6877c-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="6877c-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="6877c-110">Prerequisites</span></span>

* <span data-ttu-id="6877c-111">[Creación de un clúster de Kubernetes](container-service-kubernetes-walkthrough.md) en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6877c-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="6877c-112">[Instalación y configuración `kubectl`](../container-service-connect.md) en un equipo local</span><span class="sxs-lookup"><span data-stu-id="6877c-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="6877c-113">[Instalación de Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) en un equipo local</span><span class="sxs-lookup"><span data-stu-id="6877c-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="6877c-114">Aspectos básicos de Helm</span><span class="sxs-lookup"><span data-stu-id="6877c-114">Helm basics</span></span> 

<span data-ttu-id="6877c-115">tooview información sobre hello Kubernetes clúster que está instalando caña y la implementación de las aplicaciones, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="6877c-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="6877c-117">Después de haber instalado timón, instalar caña en el clúster Kubernetes escribiendo el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="6877c-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="6877c-118">Cuando se complete correctamente, verá resultados similares a Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6877c-118">When it completes successfully, you see output like hello following:</span></span>

![Instalación de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="6877c-120">tooview de comandos de todos los Hola timón gráficos disponibles en el repositorio de hello, Hola de tipo siguientes:</span><span class="sxs-lookup"><span data-stu-id="6877c-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="6877c-121">Verá resultados similares a Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="6877c-121">You see output like hello following:</span></span>

![Búsqueda de Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="6877c-123">tooupdate Hola gráficos tooget Hola versiones más recientes, escriba:</span><span class="sxs-lookup"><span data-stu-id="6877c-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="6877c-124">Implementación de un gráfico de controlador de entrada de Nginx</span><span class="sxs-lookup"><span data-stu-id="6877c-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="6877c-125">toodeploy un gráfico de controlador de entrada de Nginx, escriba un comando único:</span><span class="sxs-lookup"><span data-stu-id="6877c-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Implementación del controlador de entrada](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="6877c-127">Si escribe `kubectl get svc` tooview todos los servicios que se ejecutan en el clúster de hello, verá que se asigna una dirección IP toohello controlador de entrada.</span><span class="sxs-lookup"><span data-stu-id="6877c-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="6877c-128">(Mientras asignación Hola está en curso, vea `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="6877c-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="6877c-129">Toma un par de minutos toocomplete).</span><span class="sxs-lookup"><span data-stu-id="6877c-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="6877c-130">Una vez se asigna la dirección IP de hello, navegue toohello valo Hola externo IP dirección toosee hello Nginx back-end ejecuta.</span><span class="sxs-lookup"><span data-stu-id="6877c-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Dirección IP de entrada](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="6877c-132">toosee una lista de gráficos instalado en el clúster, tipo:</span><span class="sxs-lookup"><span data-stu-id="6877c-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="6877c-133">Se puede abreviar como comando hello demasiado`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="6877c-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="6877c-134">Implementación de un cliente y un gráfico de MariaDB</span><span class="sxs-lookup"><span data-stu-id="6877c-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="6877c-135">Implementar ahora un gráfico de MariaDB y una base de datos de MariaDB cliente tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="6877c-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="6877c-136">gráfico de toodeploy hello MariaDB, Hola de tipo siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6877c-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="6877c-137">donde `--name` es una etiqueta que se usa para las versiones.</span><span class="sxs-lookup"><span data-stu-id="6877c-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="6877c-138">Si se produce un error en la implementación de hello, ejecute `helm repo update` y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="6877c-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="6877c-139">tooview todos los gráficos de hello implementan en el clúster, tipo:</span><span class="sxs-lookup"><span data-stu-id="6877c-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="6877c-140">tooview todas las implementaciones que se ejecutan en el clúster, escriba:</span><span class="sxs-lookup"><span data-stu-id="6877c-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="6877c-141">Por último, toorun un cliente de hello pod tooaccess, escriba:</span><span class="sxs-lookup"><span data-stu-id="6877c-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="6877c-142">tooconnect toohello cliente, Hola de tipo siguiente comando, reemplazando `v1-mariadb` con nombre hello de la implementación:</span><span class="sxs-lookup"><span data-stu-id="6877c-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="6877c-143">Ahora puede usar el estándares SQL comandos toocreate las bases de datos, tablas, etcetera. Por ejemplo, `Create DATABASE testdb1;` crea una base de datos vacía.</span><span class="sxs-lookup"><span data-stu-id="6877c-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="6877c-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6877c-144">Next steps</span></span>

* <span data-ttu-id="6877c-145">Para obtener más información acerca de cómo administrar Kubernetes gráficos, vea hello [timón documentación](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="6877c-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

