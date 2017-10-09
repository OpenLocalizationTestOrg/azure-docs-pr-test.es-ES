---
title: "clúster de Azure DC/OS aaaManage con la API de REST de maratón | Documentos de Microsoft"
description: "Implementar el clúster de servicio de contenedor de Azure DC/OS tooan de contenedores mediante Hola API de REST de maratón."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, contenedores, microservicios, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="d50aa-104">Administración de contenedores de DC/OS a través de la API de REST de maratón Hola</span><span class="sxs-lookup"><span data-stu-id="d50aa-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="d50aa-105">Controlador de dominio/OS proporciona un entorno para implementar y ampliar las cargas de trabajo en clúster, mientras la abstracción de hardware subyacente Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="d50aa-106">Por encima de DC/OS hay un marco que administra la programación y ejecución de cargas de trabajo de proceso.</span><span class="sxs-lookup"><span data-stu-id="d50aa-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="d50aa-107">Aunque los marcos están disponibles para muchas cargas de trabajo populares, este documento ofrece una introducción crear y ajustar la escala de las implementaciones de contenedor mediante el uso de API de REST de maratón Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d50aa-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="d50aa-108">Prerequisites</span></span>

<span data-ttu-id="d50aa-109">Antes de trabajar con estos ejemplos, necesita un clúster de DC/OS configurado en el servicio Contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="d50aa-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="d50aa-110">También necesita clúster de toothis de conectividad remota de toohave.</span><span class="sxs-lookup"><span data-stu-id="d50aa-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="d50aa-111">Para obtener más información sobre estos elementos, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="d50aa-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="d50aa-112">Implementación de un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="d50aa-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="d50aa-113">Conexión de clúster del servicio de contenedor de Azure tooan</span><span class="sxs-lookup"><span data-stu-id="d50aa-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="d50aa-114">Hola de acceso a las API del controlador de dominio/OS</span><span class="sxs-lookup"><span data-stu-id="d50aa-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="d50aa-115">Cuando se haya conectado toohello clúster de servicio de contenedor de Azure, puede tener acceso a través del puerto http://localhost:local Hola DC/OS y las API de REST relacionadas.</span><span class="sxs-lookup"><span data-stu-id="d50aa-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="d50aa-116">ejemplos de Hello en este documento se supone que está realizando un túnel en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="d50aa-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="d50aa-117">Por ejemplo, se pueden alcanzar los puntos de conexión de maratón hello en URI a partir de `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="d50aa-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="d50aa-118">Para obtener más información sobre Hola varias API, consulte la documentación de Mesosphere de Hola de hello [API maratón](https://mesosphere.github.io/marathon/docs/rest-api.html) y [Chronos API](https://mesos.github.io/chronos/docs/api.html)y la documentación de Apache de hello [Mesos API del programador ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="d50aa-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="d50aa-119">Recopilación de información de DC/OS y Marathon</span><span class="sxs-lookup"><span data-stu-id="d50aa-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="d50aa-120">Antes de implementar el clúster de contenedores toohello DC/OS, recopilar información sobre clústeres de DC/OS hello, como nombres de Hola y el estado de los agentes de Hola DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d50aa-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="d50aa-121">toodo por lo tanto, consultar hello `master/slaves` punto de conexión de hello API de REST de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d50aa-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="d50aa-122">Si todo va bien, consulta Hola devuelve una lista de agentes de DC/OS y varias propiedades para cada uno.</span><span class="sxs-lookup"><span data-stu-id="d50aa-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="d50aa-123">Ahora, utilice Hola maratón `/apps` toocheck de punto de conexión de clúster de DC/OS de toohello de las implementaciones de aplicación actual.</span><span class="sxs-lookup"><span data-stu-id="d50aa-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="d50aa-124">Si se trata de un nuevo clúster, verá una matriz vacía para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d50aa-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="d50aa-125">Implementación de un contenedor con formato Docker</span><span class="sxs-lookup"><span data-stu-id="d50aa-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="d50aa-126">Implementar contenedores con Docker formato a través de la API de REST de maratón hello mediante un archivo JSON que describe la implementación de hello prevista.</span><span class="sxs-lookup"><span data-stu-id="d50aa-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="d50aa-127">Hello en el ejemplo siguiente implementa a un agente Nginx contenedor tooa privado en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="d50aa-128">toodeploy un contenedor con formato Docker, almacene el archivo JSON de hello en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="d50aa-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="d50aa-129">Contenedor siguiente, de hello toodeploy, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="d50aa-130">Especificar nombre de hello del archivo JSON de hello (`marathon.json` en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="d50aa-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="d50aa-131">salida de Hello es siguiente de toohello similar:</span><span class="sxs-lookup"><span data-stu-id="d50aa-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="d50aa-132">Ahora, si consulta maratón para las aplicaciones, esta nueva aplicación aparece en la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="d50aa-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="d50aa-133">Alcanzar contenedor Hola</span><span class="sxs-lookup"><span data-stu-id="d50aa-133">Reach hello container</span></span>

<span data-ttu-id="d50aa-134">Puede comprobar que hello que nginx se ejecuta en un contenedor en uno de los agentes privados de hello en clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="d50aa-135">host de hello toofind y el puerto donde se está ejecutando el contenedor de hello, consultar maratón hello las tareas en ejecución:</span><span class="sxs-lookup"><span data-stu-id="d50aa-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="d50aa-136">Busca el valor de Hola de `host` en la salida de hello (una dirección IP similar demasiado`10.32.0.x`) y el valor de Hola de `ports`.</span><span class="sxs-lookup"><span data-stu-id="d50aa-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="d50aa-137">Ahora, realizar una administración de toohello de conexión de terminal (no una conexión de túnel) SSH FQDN de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="d50aa-138">Una vez conectado, asegúrese de hello después de la solicitud, sustituyendo los valores correctos de Hola de `host` y `ports`:</span><span class="sxs-lookup"><span data-stu-id="d50aa-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="d50aa-139">Hola Nginx salida de servidor es similar a continuación toohello:</span><span class="sxs-lookup"><span data-stu-id="d50aa-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx desde el contenedor](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="d50aa-141">Escalado de los contenedores</span><span class="sxs-lookup"><span data-stu-id="d50aa-141">Scale your containers</span></span>
<span data-ttu-id="d50aa-142">Puede usar Hola maratón API tooscale out o escala en las implementaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d50aa-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="d50aa-143">En el ejemplo anterior de hello, ha implementado una instancia de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d50aa-144">Vamos a ajustar el tamaño toothree instancias de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="d50aa-145">toodo por lo tanto, crear un archivo JSON mediante Hola después de texto JSON y almacenarla en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="d50aa-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d50aa-146">Desde la conexión de túnel, ejecute hello después tooscale comando aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="d50aa-147">Hola URI es http://localhost/marathon/v2/apps/ seguido por Id. de Hola de hello tooscale de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="d50aa-148">Si utilizas muestra de Hola a Nginx que se proporciona aquí, Hola URI sería http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="d50aa-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="d50aa-149">Por último, consultar punto de conexión de hello maratón para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d50aa-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="d50aa-150">Verá que ahora hay tres contenedores de Nginx.</span><span class="sxs-lookup"><span data-stu-id="d50aa-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="d50aa-151">Comandos de PowerShell equivalentes</span><span class="sxs-lookup"><span data-stu-id="d50aa-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="d50aa-152">Puede realizar las mismas acciones mediante comandos de PowerShell en un sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="d50aa-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="d50aa-153">toogather información sobre clústeres de DC/OS hello, como nombres de agente y el estado del agente, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="d50aa-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="d50aa-154">Implementar contenedores con Docker formato a través de maratón mediante un archivo JSON que describe la implementación de hello prevista.</span><span class="sxs-lookup"><span data-stu-id="d50aa-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="d50aa-155">Hello en el ejemplo siguiente implementa contenedor Nginx de hello, enlazar el puerto 80 de Hola DC/OS agente tooport 80 del contenedor de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="d50aa-156">toodeploy un contenedor con formato Docker, almacene el archivo JSON de hello en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="d50aa-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="d50aa-157">Contenedor siguiente, de hello toodeploy, ejecute el siguiente comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="d50aa-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="d50aa-158">Especificar archivo JSON de toohello de ruta de acceso de hello (`marathon.json` en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="d50aa-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="d50aa-159">También puede utilizar Hola maratón API tooscale out o escala en las implementaciones de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d50aa-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="d50aa-160">En el ejemplo anterior de hello, ha implementado una instancia de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="d50aa-161">Vamos a ajustar el tamaño toothree instancias de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="d50aa-162">toodo por lo tanto, crear un archivo JSON mediante Hola después de texto JSON y almacenarla en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="d50aa-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="d50aa-163">Siguiente ejecución Hola comando tooscale aplicación Hola:</span><span class="sxs-lookup"><span data-stu-id="d50aa-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="d50aa-164">Hola URI es http://localhost/marathon/v2/apps/ seguido por Id. de Hola de hello tooscale de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d50aa-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="d50aa-165">Si utilizas ejemplo de Hola Nginx proporcionado aquí, Hola URI sería http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="d50aa-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="d50aa-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d50aa-166">Next steps</span></span>
* [<span data-ttu-id="d50aa-167">Obtenga más información acerca de los puntos de conexión de hello Mesos HTTP</span><span class="sxs-lookup"><span data-stu-id="d50aa-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="d50aa-168">Obtenga más información acerca de la API de REST de maratón Hola</span><span class="sxs-lookup"><span data-stu-id="d50aa-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

