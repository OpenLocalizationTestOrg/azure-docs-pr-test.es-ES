---
title: "Administración de un clúster de Azure Kubernetes con una interfaz de usuario web | Microsoft Docs"
description: Uso de la interfaz de usuario web de Kubernetes en Azure Container Service
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e31f90d61fc61f17582372fe9f491a1e21f628b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="941fd-103">Uso de la interfaz de usuario web de Kubernetes con Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="941fd-103">Using the Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="941fd-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="941fd-104">Prerequisites</span></span>
<span data-ttu-id="941fd-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="941fd-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="941fd-106">También se da por supuesto que tiene la CLI de Azure 2.0 y las herramientas de `kubectl` instaladas.</span><span class="sxs-lookup"><span data-stu-id="941fd-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="941fd-107">Puede probar si tiene la herramienta `az` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="941fd-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="941fd-108">Si no tiene la herramienta `az` instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="941fd-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="941fd-109">Puede probar si tiene la herramienta `kubectl` instalada mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="941fd-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="941fd-110">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="941fd-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="941fd-111">Información general</span><span class="sxs-lookup"><span data-stu-id="941fd-111">Overview</span></span>

### <a name="connect-to-the-web-ui"></a><span data-ttu-id="941fd-112">Conexión a la interfaz de usuario web</span><span class="sxs-lookup"><span data-stu-id="941fd-112">Connect to the web UI</span></span>
<span data-ttu-id="941fd-113">Puede iniciar la interfaz de usuario web de Kubernetes ejecutando lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="941fd-113">You can launch the Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="941fd-114">Debería abrirse un explorador web configurado para comunicarse con un proxy seguro que conecta la máquina local con la interfaz de usuario web de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="941fd-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="941fd-115">Creación y exposición de un servicio</span><span class="sxs-lookup"><span data-stu-id="941fd-115">Create and expose a service</span></span>
1. <span data-ttu-id="941fd-116">En la interfaz de usuario web de Kubernetes, haga clic en el botón **Create** (Crear) de la ventana derecha superior.</span><span class="sxs-lookup"><span data-stu-id="941fd-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span></span>

    ![Interfaz de usuario de creación de Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="941fd-118">Se debería abrir un cuadro de diálogo en el que puede comenzar a crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="941fd-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="941fd-119">Utilice el nombre `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="941fd-119">Give it the name `hello-nginx`.</span></span> <span data-ttu-id="941fd-120">Use el contenedor [ `nginx` de Docker](https://hub.docker.com/_/nginx/) e implemente las tres réplicas de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="941fd-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Cuadro de diálogo de creación de pod de Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="941fd-122">En **Service** (Servicio), seleccione **External** (Externo) y escriba el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="941fd-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="941fd-123">Esta configuración equilibra la carga de tráfico a las tres réplicas.</span><span class="sxs-lookup"><span data-stu-id="941fd-123">This setting load-balances traffic to the three replicas.</span></span>

    ![Cuadro de diálogo de creación del servicio de Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="941fd-125">Haga clic en **Deploy** (Implementar) para implementar estos contenedores y servicios.</span><span class="sxs-lookup"><span data-stu-id="941fd-125">Click **Deploy** to deploy these containers and services.</span></span>

    ![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="941fd-127">Visualización de los contenedores</span><span class="sxs-lookup"><span data-stu-id="941fd-127">View your containers</span></span>
<span data-ttu-id="941fd-128">Después de hacer clic en **Deploy** (Implementar), la interfaz de usuario muestra una vista de su servicio tal y como se implementa:</span><span class="sxs-lookup"><span data-stu-id="941fd-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span></span>

![Estado de Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="941fd-130">Puede ver el estado de cada objeto de Kubernetes en el círculo en el lado izquierdo de la interfaz de usuario, bajo **Pods** (Pods).</span><span class="sxs-lookup"><span data-stu-id="941fd-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="941fd-131">Si es un círculo parcialmente completo, el objeto se sigue implementando.</span><span class="sxs-lookup"><span data-stu-id="941fd-131">If it is a partially full circle, then the object is still deploying.</span></span> <span data-ttu-id="941fd-132">Cuando un objeto está totalmente implementado, muestra una marca de verificación verde:</span><span class="sxs-lookup"><span data-stu-id="941fd-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="941fd-134">Cuando todo funcione, puede hacer clic en uno de los pod para ver detalles sobre el servicio web que se esté ejecutando.</span><span class="sxs-lookup"><span data-stu-id="941fd-134">Once everything is running, click one of your pods to see details about the running web service.</span></span>

![Pod de Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="941fd-136">En la vista específica **Pods**, puede ver información sobre los contenedores del pod, así como los recursos de CPU y memoria utilizados por los contenedores:</span><span class="sxs-lookup"><span data-stu-id="941fd-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span></span>

![Recursos de Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="941fd-138">Si no ve los recursos, es posible que tenga que esperar unos minutos para que los datos de supervisión de propaguen.</span><span class="sxs-lookup"><span data-stu-id="941fd-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span></span>

<span data-ttu-id="941fd-139">Para ver los registros para el contenedor, haga clic en **View logs** (Ver registros).</span><span class="sxs-lookup"><span data-stu-id="941fd-139">To see the logs for your container, click **View logs**.</span></span>

![Registros de Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="941fd-141">Visualización del servicio</span><span class="sxs-lookup"><span data-stu-id="941fd-141">Viewing your service</span></span>
<span data-ttu-id="941fd-142">Además de ejecutar los contenedores, la interfaz de usuario de Kubernetes ha creado una referencia externa `Service` que aprovisiona un equilibrador de carga para proporcionar tráfico a los contenedores en el clúster.</span><span class="sxs-lookup"><span data-stu-id="941fd-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span></span>

<span data-ttu-id="941fd-143">En el panel de navegación izquierdo, haga clic en **Services** (Servicios) para ver todos los servicios (debería haber solo uno).</span><span class="sxs-lookup"><span data-stu-id="941fd-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span></span>

![Servicios de Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="941fd-145">En esa vista debe ver un punto de conexión externo (dirección IP) asignado a su servicio.</span><span class="sxs-lookup"><span data-stu-id="941fd-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span></span>
<span data-ttu-id="941fd-146">Si hace clic en esa dirección IP, debería ver el contenedor de Nginx que se ejecuta detrás del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="941fd-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![vista de nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="941fd-148">Cambio del tamaño del servicio</span><span class="sxs-lookup"><span data-stu-id="941fd-148">Resizing your service</span></span>
<span data-ttu-id="941fd-149">Además de ver los objetos en la interfaz de usuario, también puede editar y actualizar los objetos de la API de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="941fd-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span></span>

<span data-ttu-id="941fd-150">En primer lugar, vaya a **Deployments** (Implentaciones) del panel de navegación izquierdo para ver la implementación de su servicio.</span><span class="sxs-lookup"><span data-stu-id="941fd-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span></span>

<span data-ttu-id="941fd-151">Cuando esté en esa vista, haga clic en el conjunto de réplicas y, luego, haga clic en **Edit** (Editar) en la barra de navegación superior:</span><span class="sxs-lookup"><span data-stu-id="941fd-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span></span>

![Edición de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="941fd-153">Edite el campo `spec.replicas` para establecerlo en `2`y haga clic en **Update** (Actualizar).</span><span class="sxs-lookup"><span data-stu-id="941fd-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span></span>

<span data-ttu-id="941fd-154">Esto hará que el número de réplicas descienda a dos mediante la eliminación de uno de los pod.</span><span class="sxs-lookup"><span data-stu-id="941fd-154">This causes the number of replicas to drop to two by deleting one of your pods.</span></span>

 

