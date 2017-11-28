---
title: "aaaManage Kubernetes de Azure de clúster con la interfaz de usuario web | Documentos de Microsoft"
description: Con hello Kubernetes web interfaz de usuario en el servicio de contenedor de Azure
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
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="8fdca-103">Con hello Kubernetes web interfaz de usuario con el servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="8fdca-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fdca-104">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8fdca-104">Prerequisites</span></span>
<span data-ttu-id="8fdca-105">En este tutorial se da por supuesto que ha [creado un clúster de Kubernetes con Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8fdca-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="8fdca-106">También se supone que dispone de hello Azure CLI 2.0 y `kubectl` herramientas instaladas.</span><span class="sxs-lookup"><span data-stu-id="8fdca-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="8fdca-107">Puede probar si tiene hello `az` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="8fdca-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="8fdca-108">Si no tienes hello `az` herramienta instalada, se ofrecen instrucciones [aquí](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="8fdca-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="8fdca-109">Puede probar si tiene hello `kubectl` instalada mediante la ejecución de la herramienta:</span><span class="sxs-lookup"><span data-stu-id="8fdca-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="8fdca-110">Si no tiene la herramienta `kubectl` instalada, puede ejecutar:</span><span class="sxs-lookup"><span data-stu-id="8fdca-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="8fdca-111">Información general</span><span class="sxs-lookup"><span data-stu-id="8fdca-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="8fdca-112">Conecte la interfaz de usuario de web toohello</span><span class="sxs-lookup"><span data-stu-id="8fdca-112">Connect toohello web UI</span></span>
<span data-ttu-id="8fdca-113">Para iniciar la interfaz de usuario de web de hello Kubernetes ejecutando:</span><span class="sxs-lookup"><span data-stu-id="8fdca-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="8fdca-114">Se debería abrir un web explorador configurado tootalk tooa segura proxy que se conecta la interfaz de usuario de la web de Kubernetes toohello de equipo local.</span><span class="sxs-lookup"><span data-stu-id="8fdca-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="8fdca-115">Creación y exposición de un servicio</span><span class="sxs-lookup"><span data-stu-id="8fdca-115">Create and expose a service</span></span>
1. <span data-ttu-id="8fdca-116">En la interfaz de usuario del web Kubernetes hello, haga clic en **crear** botón en hello superior derecho de la ventana.</span><span class="sxs-lookup"><span data-stu-id="8fdca-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Interfaz de usuario de creación de Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="8fdca-118">Se debería abrir un cuadro de diálogo en el que puede comenzar a crear la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8fdca-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="8fdca-119">Asígnele el nombre hello `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="8fdca-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="8fdca-120">Hola de uso [ `nginx` contenedor de Docker](https://hub.docker.com/_/nginx/) e implementar tres réplicas de este servicio web.</span><span class="sxs-lookup"><span data-stu-id="8fdca-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Cuadro de diálogo de creación de pod de Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="8fdca-122">En **Service** (Servicio), seleccione **External** (Externo) y escriba el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="8fdca-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="8fdca-123">Esta configuración equilibra la carga toohello tres réplicas de tráfico.</span><span class="sxs-lookup"><span data-stu-id="8fdca-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Cuadro de diálogo de creación del servicio de Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="8fdca-125">Haga clic en **implementar** toodeploy estos contenedores y los servicios.</span><span class="sxs-lookup"><span data-stu-id="8fdca-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="8fdca-127">Visualización de los contenedores</span><span class="sxs-lookup"><span data-stu-id="8fdca-127">View your containers</span></span>
<span data-ttu-id="8fdca-128">Tras hacer clic en **implementar**, Hola interfaz de usuario muestra una vista de su servicio tal y como se implementa:</span><span class="sxs-lookup"><span data-stu-id="8fdca-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Estado de Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="8fdca-130">Puede ver estado de Hola de cada objeto Kubernetes en círculo hello en el lado izquierdo de saludo de la interfaz de usuario, en **pod**.</span><span class="sxs-lookup"><span data-stu-id="8fdca-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="8fdca-131">Si es un círculo parcialmente completo, objeto de hello todavía está implementando.</span><span class="sxs-lookup"><span data-stu-id="8fdca-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="8fdca-132">Cuando un objeto está totalmente implementado, muestra una marca de verificación verde:</span><span class="sxs-lookup"><span data-stu-id="8fdca-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Implementación de Kubernetes](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="8fdca-134">Una vez que todo funciona, haga clic en uno de los detalles de toosee pod sobre Hola ejecutando el servicio web.</span><span class="sxs-lookup"><span data-stu-id="8fdca-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Pod de Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="8fdca-136">Hola **pod** vista, puede ver información acerca de los contenedores de hello en pod hello, así como recursos de CPU y memoria de hello usados por los contenedores:</span><span class="sxs-lookup"><span data-stu-id="8fdca-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Recursos de Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="8fdca-138">Si no ve los recursos de hello, puede necesitar toowait unos minutos para hello toopropagate de datos de supervisión.</span><span class="sxs-lookup"><span data-stu-id="8fdca-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="8fdca-139">registros de hello toosee para el contenedor, haga clic en **ver registros**.</span><span class="sxs-lookup"><span data-stu-id="8fdca-139">toosee hello logs for your container, click **View logs**.</span></span>

![Registros de Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="8fdca-141">Visualización del servicio</span><span class="sxs-lookup"><span data-stu-id="8fdca-141">Viewing your service</span></span>
<span data-ttu-id="8fdca-142">En suma toorunning los contenedores, hello Kubernetes UI ha creado una referencia externa `Service` que proporciona un contenedor de toohello carga equilibrador toobring tráfico en el clúster.</span><span class="sxs-lookup"><span data-stu-id="8fdca-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="8fdca-143">En el panel de navegación izquierdo de hello, haga clic en **servicios** tooview todos los servicios (debería haber sólo uno).</span><span class="sxs-lookup"><span data-stu-id="8fdca-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Servicios de Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="8fdca-145">En la vista, debería ver un extremo externo (dirección IP) que se ha asignado el servicio tooyour.</span><span class="sxs-lookup"><span data-stu-id="8fdca-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="8fdca-146">Si hace clic en esa dirección IP, debería ver el contenedor de Nginx que se ejecuta detrás del equilibrador de carga.</span><span class="sxs-lookup"><span data-stu-id="8fdca-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![vista de nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="8fdca-148">Cambio del tamaño del servicio</span><span class="sxs-lookup"><span data-stu-id="8fdca-148">Resizing your service</span></span>
<span data-ttu-id="8fdca-149">En suma tooviewing los objetos en Hola interfaz de usuario, puede editar y actualizar objetos de la API de Kubernetes Hola.</span><span class="sxs-lookup"><span data-stu-id="8fdca-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="8fdca-150">En primer lugar, haga clic en **implementaciones** Hola dejado la implementación de Hola de toosee de panel de navegación para el servicio.</span><span class="sxs-lookup"><span data-stu-id="8fdca-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="8fdca-151">Una vez que esté en esa vista, haga clic en el conjunto de réplicas de hello y, a continuación, haga clic en **editar** en la barra de navegación superior de hello:</span><span class="sxs-lookup"><span data-stu-id="8fdca-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Edición de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="8fdca-153">Editar hello `spec.replicas` campo toobe `2`y haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="8fdca-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="8fdca-154">Esto hace que número Hola de réplicas toodrop tootwo mediante la eliminación de uno de los conjuntos de pod.</span><span class="sxs-lookup"><span data-stu-id="8fdca-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

