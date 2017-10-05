---
title: "Implementación de contenedores con Helm en Azure Kubernetes | Microsoft Docs"
description: "Uso de la herramienta de empaquetado de Helm para implementar contenedores en un clúster de Kubernetes en Azure Container Service"
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="c2642-103">Uso de Helm para implementar contenedores en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c2642-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="c2642-104">[Helm](https://github.com/kubernetes/helm/) es una herramienta de empaquetado de código abierto que ayuda a instalar y administrar el ciclo de vida de las aplicaciones de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c2642-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="c2642-105">Helm, que funciona de forma similar a los administradores de paquetes de Linux como get Apt y Yum, se utiliza para administrar los gráficos de Kubernetes, que son paquetes de recursos de Kubernetes preconfigurados.</span><span class="sxs-lookup"><span data-stu-id="c2642-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="c2642-106">Este artículo muestra cómo trabajar con Helm en un clúster de Kubernetes implementado en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="c2642-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="c2642-107">Helm tiene dos componentes:</span><span class="sxs-lookup"><span data-stu-id="c2642-107">Helm has two components:</span></span> 
* <span data-ttu-id="c2642-108">La **CLI de Helm** es un cliente que se ejecuta en el equipo local o en la nube</span><span class="sxs-lookup"><span data-stu-id="c2642-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="c2642-109">**Tiller** es un servidor que se ejecuta en el clúster de Kubernetes y administra el ciclo de vida de las aplicaciones de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="c2642-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="c2642-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c2642-110">Prerequisites</span></span>

* <span data-ttu-id="c2642-111">[Creación de un clúster de Kubernetes](container-service-kubernetes-walkthrough.md) en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c2642-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="c2642-112">[Instalación y configuración `kubectl` ](../container-service-connect.md) en un equipo local</span><span class="sxs-lookup"><span data-stu-id="c2642-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="c2642-113">[Instalación de Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) en un equipo local</span><span class="sxs-lookup"><span data-stu-id="c2642-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="c2642-114">Aspectos básicos de Helm</span><span class="sxs-lookup"><span data-stu-id="c2642-114">Helm basics</span></span> 

<span data-ttu-id="c2642-115">Para ver información sobre el clúster de Kubernetes en el que está instalando Tiller e implementando las aplicaciones, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2642-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="c2642-117">Después de haber instalado Helm, instale Tiller en el clúster de Kubernetes escribiendo el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2642-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="c2642-118">Una vez completado correctamente, verá el siguiente resultado:</span><span class="sxs-lookup"><span data-stu-id="c2642-118">When it completes successfully, you see output like the following:</span></span>

![Instalación de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="c2642-120">Para ver todos los gráficos de Helm disponibles en el repositorio, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2642-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="c2642-121">El resultado debe ser parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="c2642-121">You see output like the following:</span></span>

![Búsqueda de Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="c2642-123">Para actualizar los gráficos para obtener las versiones más recientes, escriba:</span><span class="sxs-lookup"><span data-stu-id="c2642-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="c2642-124">Implementación de un gráfico de controlador de entrada de Nginx</span><span class="sxs-lookup"><span data-stu-id="c2642-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="c2642-125">Para implementar un gráfico de controlador de entrada de Nginx, escriba un comando único:</span><span class="sxs-lookup"><span data-stu-id="c2642-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Implementación del controlador de entrada](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="c2642-127">Si escribe `kubectl get svc` para ver todos los servicios que se ejecutan en el clúster, verá que se asigna una dirección IP al controlador de entrada.</span><span class="sxs-lookup"><span data-stu-id="c2642-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="c2642-128">(Mientras que la asignación está en curso, verá `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="c2642-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="c2642-129">Tarda unos minutos en completarse).</span><span class="sxs-lookup"><span data-stu-id="c2642-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="c2642-130">Después de que se asigne la dirección IP, vaya hasta el valor de la dirección IP externa para ver la ejecución de back-end de Nginx.</span><span class="sxs-lookup"><span data-stu-id="c2642-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Dirección IP de entrada](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="c2642-132">Para ver una lista de gráficos instalados en el clúster, escriba:</span><span class="sxs-lookup"><span data-stu-id="c2642-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="c2642-133">Puede abreviar el comando en `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="c2642-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="c2642-134">Implementación de un cliente y un gráfico de MariaDB</span><span class="sxs-lookup"><span data-stu-id="c2642-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="c2642-135">Ahora implemente un gráfico y un cliente de MariaDB para conectarse a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="c2642-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="c2642-136">Para implementar el gráfico de MariaDB, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c2642-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="c2642-137">donde `--name` es una etiqueta que se usa para las versiones.</span><span class="sxs-lookup"><span data-stu-id="c2642-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="c2642-138">Si se produce un error en la implementación, ejecute `helm repo update` e inténtelo de nuevo.</span><span class="sxs-lookup"><span data-stu-id="c2642-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="c2642-139">Para ver todos los gráficos implementados en el clúster, escriba:</span><span class="sxs-lookup"><span data-stu-id="c2642-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="c2642-140">Para ver todas las implementaciones que se ejecutan en el clúster, escriba:</span><span class="sxs-lookup"><span data-stu-id="c2642-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="c2642-141">Por último, para ejecutar un pod para tener acceso al cliente, escriba:</span><span class="sxs-lookup"><span data-stu-id="c2642-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="c2642-142">Para conectar con el cliente, escriba el siguiente comando, reemplazando `v1-mariadb` por el nombre de la implementación:</span><span class="sxs-lookup"><span data-stu-id="c2642-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="c2642-143">Ahora puede usar los comandos SQL estándar para crear bases de datos, tablas, etc. Por ejemplo, `Create DATABASE testdb1;` crea una base de datos vacía.</span><span class="sxs-lookup"><span data-stu-id="c2642-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="c2642-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c2642-144">Next steps</span></span>

* <span data-ttu-id="c2642-145">Para más información sobre cómo administrar gráficos de Kubernetes, vea la [Documentación de Helm](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="c2642-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

