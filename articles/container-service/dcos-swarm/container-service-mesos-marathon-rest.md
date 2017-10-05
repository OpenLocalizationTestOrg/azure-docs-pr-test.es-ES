---
title: "Administración de un clúster DC/OS de Azure con la API de REST de Marathon | Microsoft Docs"
description: "Implemente contenedores en un clúster de DC/OS de Azure Container Service mediante la API de REST de Marathon."
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
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="08cab-104">Administración de contenedores de DC/OS a través de la API de REST de Marathon</span><span class="sxs-lookup"><span data-stu-id="08cab-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="08cab-105">DC/OS proporciona un entorno para implementar y escalar cargas de trabajo agrupadas, al tiempo que reduce el hardware subyacente.</span><span class="sxs-lookup"><span data-stu-id="08cab-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="08cab-106">Por encima de DC/OS hay un marco que administra la programación y ejecución de cargas de trabajo de proceso.</span><span class="sxs-lookup"><span data-stu-id="08cab-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="08cab-107">Aunque hay marcos de trabajo disponibles para muchas cargas de trabajo conocidas, este documento es una introducción a la creación y el escalado de implementaciones de contenedor con la API de REST de Marathon.</span><span class="sxs-lookup"><span data-stu-id="08cab-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="08cab-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="08cab-108">Prerequisites</span></span>

<span data-ttu-id="08cab-109">Antes de trabajar con estos ejemplos, necesita un clúster de DC/OS configurado en el servicio Contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="08cab-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="08cab-110">También debe tener conectividad remota con este clúster.</span><span class="sxs-lookup"><span data-stu-id="08cab-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="08cab-111">Para más información sobre estos aspectos, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="08cab-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="08cab-112">Implementación de un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="08cab-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="08cab-113">Conexión a un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="08cab-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="08cab-114">Acceso a las API de DC/OS</span><span class="sxs-lookup"><span data-stu-id="08cab-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="08cab-115">Una vez conectado al clúster de Azure Container Service, podrá acceder a DC/OS y a las API de REST relacionadas a través de http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="08cab-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="08cab-116">Los ejemplos de este documento suponen que está realizando la tunelización en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="08cab-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="08cab-117">Por ejemplo, a los puntos de conexión de Marathon se puede acceder en los identificadores URI que comienzan por `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="08cab-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="08cab-118">Para más información sobre las diferentes API, consulte la documentación de Mesosphere sobre [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) y [Chronos API](https://mesos.github.io/chronos/docs/api.html), así como la documentación de Apache sobre [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="08cab-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="08cab-119">Recopilación de información de DC/OS y Marathon</span><span class="sxs-lookup"><span data-stu-id="08cab-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="08cab-120">Antes de implementar contenedores en el clúster de DC/OS, recopile información sobre él, como los nombres y el estado de los agentes de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="08cab-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="08cab-121">Para ello, consulte el punto de conexión `master/slaves` de la API de REST de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="08cab-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="08cab-122">Si todo va bien, la consulta devuelve una lista de agentes de DC/OS y varias propiedades de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="08cab-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="08cab-123">Ahora, utilice el punto de conexión `/apps` de Marathon para buscar las implementaciones actuales de aplicaciones en el clúster de DC/OS.</span><span class="sxs-lookup"><span data-stu-id="08cab-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="08cab-124">Si se trata de un nuevo clúster, verá una matriz vacía para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="08cab-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="08cab-125">Implementación de un contenedor con formato Docker</span><span class="sxs-lookup"><span data-stu-id="08cab-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="08cab-126">Los contenedores con formato Docker se implementan a través de la API de REST de Marathon mediante un archivo JSON que describe la implementación deseada.</span><span class="sxs-lookup"><span data-stu-id="08cab-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="08cab-127">El ejemplo siguiente implementa un contenedor de Nginx en un agente privado del clúster.</span><span class="sxs-lookup"><span data-stu-id="08cab-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

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

<span data-ttu-id="08cab-128">Para implementar un contenedor con formato Docker, almacene el archivo JSON en una ubicación a la que se pueda accesible.</span><span class="sxs-lookup"><span data-stu-id="08cab-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="08cab-129">A continuación, ejecute el siguiente comando para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="08cab-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="08cab-130">Especifique el nombre del archivo JSON (`marathon.json` en este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="08cab-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="08cab-131">La salida será similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="08cab-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="08cab-132">Ahora, si consulta Marathon sobre las aplicaciones, esta nueva aplicación se muestra en el resultado.</span><span class="sxs-lookup"><span data-stu-id="08cab-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="08cab-133">Cobertura del contenedor</span><span class="sxs-lookup"><span data-stu-id="08cab-133">Reach the container</span></span>

<span data-ttu-id="08cab-134">Puede comprobar que Nginx se ejecuta en un contenedor de uno de los agentes privados del clúster.</span><span class="sxs-lookup"><span data-stu-id="08cab-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="08cab-135">Para buscar el host y el puerto donde se ejecuta el contenedor, consulte estas tareas de ejecución en Marathon:</span><span class="sxs-lookup"><span data-stu-id="08cab-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="08cab-136">Busque el valor de `host` en el resultado (una dirección IP similar a `10.32.0.x`) y el valor de `ports`.</span><span class="sxs-lookup"><span data-stu-id="08cab-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="08cab-137">Ahora puede realizar una conexión de terminal de SSH (no una conexión de túnel) en el FQDN de administración del clúster.</span><span class="sxs-lookup"><span data-stu-id="08cab-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="08cab-138">Una vez conectado, sustituya los valores correctos de `host` y `ports`, y realice esta solicitud:</span><span class="sxs-lookup"><span data-stu-id="08cab-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="08cab-139">La salida del servidor de Nginx es similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="08cab-139">The Nginx server output is similar to the following:</span></span>

![Nginx desde el contenedor](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="08cab-141">Escalado de los contenedores</span><span class="sxs-lookup"><span data-stu-id="08cab-141">Scale your containers</span></span>
<span data-ttu-id="08cab-142">La API de Marathon se puede utilizar para escalar horizontalmente implementaciones de aplicaciones o reducirlas horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="08cab-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="08cab-143">En el ejemplo anterior, ha implementado una instancia de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="08cab-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="08cab-144">Vamos a escalarla horizontalmente a tres instancias de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="08cab-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="08cab-145">Para ello, cree un archivo JSON mediante el siguiente texto JSON y almacénelo en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="08cab-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="08cab-146">Desde la conexión de túnel, ejecute el comando siguiente para escalar la aplicación horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="08cab-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="08cab-147">El identificador URI es http://localhost/marathon/v2/apps/, seguido del identificador de la aplicación que se va a escalar.</span><span class="sxs-lookup"><span data-stu-id="08cab-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="08cab-148">Si utiliza el ejemplo de Nginx que se incluye aquí, el identificador URI sería http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="08cab-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="08cab-149">Por último, consulte el punto de conexión de Marathon para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="08cab-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="08cab-150">Verá que ahora hay tres contenedores de Nginx.</span><span class="sxs-lookup"><span data-stu-id="08cab-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="08cab-151">Comandos de PowerShell equivalentes</span><span class="sxs-lookup"><span data-stu-id="08cab-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="08cab-152">Puede realizar las mismas acciones mediante comandos de PowerShell en un sistema Windows.</span><span class="sxs-lookup"><span data-stu-id="08cab-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="08cab-153">Para recopilar información sobre el clúster de DC/OS, como los nombres y los estados de los agentes, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="08cab-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="08cab-154">Los contenedores con formato Docker se implementan a través de Marathon mediante un archivo JSON que describe la implementación deseada.</span><span class="sxs-lookup"><span data-stu-id="08cab-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="08cab-155">En el ejemplo siguiente, se implementa el contenedor Nginx y se enlaza el puerto 80 del agente de DC/OS al puerto 80 del contenedor.</span><span class="sxs-lookup"><span data-stu-id="08cab-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

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

<span data-ttu-id="08cab-156">Para implementar un contenedor con formato Docker, almacene el archivo JSON en una ubicación a la que se pueda accesible.</span><span class="sxs-lookup"><span data-stu-id="08cab-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="08cab-157">A continuación, ejecute el siguiente comando para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="08cab-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="08cab-158">Especifique la ruta del archivo JSON (`marathon.json` de este ejemplo).</span><span class="sxs-lookup"><span data-stu-id="08cab-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="08cab-159">La API de Marathon también se puede utilizar para escalar horizontalmente implementaciones de aplicaciones o reducirlas horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="08cab-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="08cab-160">En el ejemplo anterior, ha implementado una instancia de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="08cab-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="08cab-161">Vamos a escalarla horizontalmente a tres instancias de una aplicación.</span><span class="sxs-lookup"><span data-stu-id="08cab-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="08cab-162">Para ello, cree un archivo JSON mediante el siguiente texto JSON y almacénelo en una ubicación accesible.</span><span class="sxs-lookup"><span data-stu-id="08cab-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="08cab-163">Ejecute el comando siguiente para escalar la aplicación horizontalmente:</span><span class="sxs-lookup"><span data-stu-id="08cab-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="08cab-164">El identificador URI es http://localhost/marathon/v2/apps/, seguido del identificador de la aplicación que se va a escalar.</span><span class="sxs-lookup"><span data-stu-id="08cab-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="08cab-165">Si utiliza el ejemplo de Nginx que se incluye aquí, el identificador URI sería http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="08cab-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="08cab-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="08cab-166">Next steps</span></span>
* [<span data-ttu-id="08cab-167">Más información acerca de los puntos de conexión HTTP de Mesos</span><span class="sxs-lookup"><span data-stu-id="08cab-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="08cab-168">Más información acerca de la API de REST de Marathon</span><span class="sxs-lookup"><span data-stu-id="08cab-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

