---
title: "aaaCreate Docker se hospeda en Azure con Docker máquina | Documentos de Microsoft"
description: "Describe el uso de los hosts de máquina Docker toocreate docker en Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="976ca-103">Creación de hosts de Docker en Azure con docker-machine</span><span class="sxs-lookup"><span data-stu-id="976ca-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="976ca-104">Ejecuta [Docker](https://www.docker.com/) contenedores requiere un demonio de docker host VM ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="976ca-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="976ca-105">Este tema se describe cómo hello toouse [máquina docker](https://docs.docker.com/machine/) comando toocreate nuevas máquinas virtuales de Linux, configurada con hello demonio de Docker, se está ejecutando en Azure.</span><span class="sxs-lookup"><span data-stu-id="976ca-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="976ca-106">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="976ca-106">**Note:**</span></span> 

* <span data-ttu-id="976ca-107">*Este artículo depende de la versión 0.9.0-rc2 de docker-machine, o de una versión superior*</span><span class="sxs-lookup"><span data-stu-id="976ca-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="976ca-108">*Se admitirán los contenedores de Windows a través de la máquina de docker en hello futuro próximo*</span><span class="sxs-lookup"><span data-stu-id="976ca-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="976ca-109">Creación de VM con la máquina de Docker</span><span class="sxs-lookup"><span data-stu-id="976ca-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="976ca-110">Crear máquinas virtuales del host docker en Azure con hello `docker-machine create` comando con hello `azure` controlador.</span><span class="sxs-lookup"><span data-stu-id="976ca-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="976ca-111">Hola controlador Azure requiere el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="976ca-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="976ca-112">Puede usar hello [CLI de Azure](cli-install-nodejs.md) o hello [Portal de Azure](https://portal.azure.com) tooretrieve su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="976ca-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="976ca-113">**Uso de hello Portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="976ca-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="976ca-114">Seleccione **suscripciones** de hello izquierdo página y copiar Hola Id. de suscripción.</span><span class="sxs-lookup"><span data-stu-id="976ca-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="976ca-115">**Uso de hello CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="976ca-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="976ca-116">Tipo ```azure account list``` y el Id. de suscripción de Hola de copia.</span><span class="sxs-lookup"><span data-stu-id="976ca-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="976ca-117">Tipo `docker-machine create --driver azure` toosee Hola opciones y sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="976ca-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="976ca-118">También puede ver hello [documentación del controlador de Azure Docker](https://docs.docker.com/machine/drivers/azure/) para obtener más información.</span><span class="sxs-lookup"><span data-stu-id="976ca-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="976ca-119">Hello siguiente ejemplo se basa en hello [valores predeterminados](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), pero si lo desea establecer estos valores:</span><span class="sxs-lookup"><span data-stu-id="976ca-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="976ca-120">dns de Azure para nombre de hello asociado con la dirección IP pública de Hola y certificados generados.</span><span class="sxs-lookup"><span data-stu-id="976ca-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="976ca-121">Este es el nombre DNS de saludo de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="976ca-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="976ca-122">Hola VM puede, a continuación, con seguridad detener, versión IP dinámicas de Hola y proporcionar Hola capacidad tooreconnect después Hola vm se inicia de nuevo con una dirección IP nueva.</span><span class="sxs-lookup"><span data-stu-id="976ca-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="976ca-123">prefijo del nombre de Hello debe ser único para esa región UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="976ca-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="976ca-124">abrir el puerto 80 en hello VM para el acceso a internet saliente</span><span class="sxs-lookup"><span data-stu-id="976ca-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="976ca-125">tamaño de almacenamiento de máquina virtual tooutilize más rápido premium hello</span><span class="sxs-lookup"><span data-stu-id="976ca-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="976ca-126">almacenamiento Premium usarse como disco de máquina virtual de Hola</span><span class="sxs-lookup"><span data-stu-id="976ca-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="976ca-127">Elección de un host de Docker con una docker-machine</span><span class="sxs-lookup"><span data-stu-id="976ca-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="976ca-128">Una vez que tenga una entrada en la máquina de docker para el host, puede establecer el host predeterminado de hello cuando ejecuta comandos de docker.</span><span class="sxs-lookup"><span data-stu-id="976ca-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="976ca-129">Con PowerShell</span><span class="sxs-lookup"><span data-stu-id="976ca-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="976ca-130">Con Bash</span><span class="sxs-lookup"><span data-stu-id="976ca-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="976ca-131">Ahora puede ejecutar comandos de docker en host especificado Hola</span><span class="sxs-lookup"><span data-stu-id="976ca-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="976ca-132">Ejecución de un contenedor</span><span class="sxs-lookup"><span data-stu-id="976ca-132">Run a container</span></span>
<span data-ttu-id="976ca-133">Con un host configurado, ahora puede ejecutar un tootest de servidor web simple si el host se configuró correctamente.</span><span class="sxs-lookup"><span data-stu-id="976ca-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="976ca-134">Aquí se usa una imagen de nginx estándar, especifique que debe escuchar en el puerto 80, y que si se reinicia la máquina virtual del host de hello, contenedor Hola reiniciarán también (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="976ca-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="976ca-135">salida de Hello debe tener un aspecto similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="976ca-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="976ca-136">Contenedor de prueba Hola</span><span class="sxs-lookup"><span data-stu-id="976ca-136">Test hello container</span></span>
<span data-ttu-id="976ca-137">Examine los contenedores en ejecución mediante `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="976ca-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="976ca-138">Toosee hello y ejecución de contenedor, tipo `docker-machine ip <VM name>` tooenter de dirección IP toofind hello en el Explorador de hello:</span><span class="sxs-lookup"><span data-stu-id="976ca-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Ejecución del contenedor ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="976ca-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="976ca-140">Summary</span></span>
<span data-ttu-id="976ca-141">Con docker-machine se pueden aprovisionar fácilmente hosts de Docker en Azure para las validaciones de host de Docker individuales.</span><span class="sxs-lookup"><span data-stu-id="976ca-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="976ca-142">Para la producción de hospedaje de contenedores, vea hello [servicio de contenedor de Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="976ca-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="976ca-143">toodevelop .NET Core aplicaciones con Visual Studio, vea [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="976ca-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

