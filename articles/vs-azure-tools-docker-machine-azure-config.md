---
title: "Creación de hosts de Docker en Azure con Docker Machine | Microsoft Docs"
description: "Describe el uso de la máquina de Docker para crear hosts de docker en Azure."
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
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="45014-103">Creación de hosts de Docker en Azure con docker-machine</span><span class="sxs-lookup"><span data-stu-id="45014-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="45014-104">La ejecución de contenedores de [Docker](https://www.docker.com/) requiere una máquina virtual host que ejecute el demonio de Docker.</span><span class="sxs-lookup"><span data-stu-id="45014-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="45014-105">En este tema, se describe cómo usar el comando [docker-machine](https://docs.docker.com/machine/) para crear máquinas virtuales Linux, configuradas con el demonio de Docker, que se ejecuten en Azure.</span><span class="sxs-lookup"><span data-stu-id="45014-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="45014-106">**Nota:**</span><span class="sxs-lookup"><span data-stu-id="45014-106">**Note:**</span></span> 

* <span data-ttu-id="45014-107">*Este artículo depende de la versión 0.9.0-rc2 de docker-machine, o de una versión superior*</span><span class="sxs-lookup"><span data-stu-id="45014-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="45014-108">*Muy pronto será posible usar contenedores de Windows a través del comando docker-machine*</span><span class="sxs-lookup"><span data-stu-id="45014-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="45014-109">Creación de VM con la máquina de Docker</span><span class="sxs-lookup"><span data-stu-id="45014-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="45014-110">Cree máquinas virtuales host de Docker en Azure con el comando `docker-machine create` mediante el controlador `azure`.</span><span class="sxs-lookup"><span data-stu-id="45014-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="45014-111">El controlador de Azure necesita su identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="45014-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="45014-112">Para recuperar su suscripción de Azure, puede usar la [CLI de Azure](cli-install-nodejs.md) o [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="45014-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="45014-113">**Uso del portal de Azure**</span><span class="sxs-lookup"><span data-stu-id="45014-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="45014-114">Seleccione **Suscripciones** de la página de navegación izquierda y copie el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="45014-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="45014-115">**Uso de la CLI de Azure**</span><span class="sxs-lookup"><span data-stu-id="45014-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="45014-116">Escriba ```azure account list``` y copie el identificador de suscripción.</span><span class="sxs-lookup"><span data-stu-id="45014-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="45014-117">Escriba `docker-machine create --driver azure` para ver las opciones y sus valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="45014-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="45014-118">Para más información, también puede consultar la [documentación del controlador de Azure de Docker](https://docs.docker.com/machine/drivers/azure/) .</span><span class="sxs-lookup"><span data-stu-id="45014-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="45014-119">En el siguiente ejemplo se usan los [valores predeterminados](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), pero se configuran opcionalmente estos valores:</span><span class="sxs-lookup"><span data-stu-id="45014-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="45014-120">azure-dns para el nombre asociado a la dirección IP pública y los certificados generados.</span><span class="sxs-lookup"><span data-stu-id="45014-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="45014-121">Este es el nombre DNS de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="45014-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="45014-122">La máquina virtual puede así detenerse sin ningún riesgo, liberar la dirección IP dinámica y ofrecer la posibilidad de volver a conectarse una vez que la máquina virtual se inicia de nuevo con una dirección IP nueva.</span><span class="sxs-lookup"><span data-stu-id="45014-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="45014-123">El prefijo del nombre debe ser único para esa región UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="45014-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="45014-124">abrir el puerto 80 en la máquina virtual para el acceso a internet saliente</span><span class="sxs-lookup"><span data-stu-id="45014-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="45014-125">tamaño de la máquina virtual para usar Premium Storage más rápido</span><span class="sxs-lookup"><span data-stu-id="45014-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="45014-126">Premium Storage utilizado para el disco de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="45014-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="45014-127">Elección de un host de Docker con una docker-machine</span><span class="sxs-lookup"><span data-stu-id="45014-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="45014-128">Una vez que tenga una entrada en docker-machine para su host, puede establecer el host predeterminado al ejecutar comandos de Docker.</span><span class="sxs-lookup"><span data-stu-id="45014-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="45014-129">Con PowerShell</span><span class="sxs-lookup"><span data-stu-id="45014-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="45014-130">Con Bash</span><span class="sxs-lookup"><span data-stu-id="45014-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="45014-131">Ya se pueden ejecutar comandos de Docker en el host especificado</span><span class="sxs-lookup"><span data-stu-id="45014-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="45014-132">Ejecución de un contenedor</span><span class="sxs-lookup"><span data-stu-id="45014-132">Run a container</span></span>
<span data-ttu-id="45014-133">Con un host configurado, ya se puede ejecutar un servidor web simple para probar si dicho host se ha configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="45014-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="45014-134">Aquí se usará una imagen de nginx estándar, se especifica que debe escuchar el puerto 80 y que si la máquina virtual host se reinicia, el contenedor también se reiniciará (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="45014-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="45014-135">La salida debe tener un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="45014-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="45014-136">Prueba del contenedor</span><span class="sxs-lookup"><span data-stu-id="45014-136">Test the container</span></span>
<span data-ttu-id="45014-137">Examine los contenedores en ejecución mediante `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="45014-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="45014-138">Y para comprobar el contenedor en ejecución, escriba `docker-machine ip <VM name>` para buscar la dirección IP que debe especificar en el explorador:</span><span class="sxs-lookup"><span data-stu-id="45014-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Ejecución del contenedor ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="45014-140">Resumen</span><span class="sxs-lookup"><span data-stu-id="45014-140">Summary</span></span>
<span data-ttu-id="45014-141">Con docker-machine se pueden aprovisionar fácilmente hosts de Docker en Azure para las validaciones de host de Docker individuales.</span><span class="sxs-lookup"><span data-stu-id="45014-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="45014-142">Para la creación de hospedaje de contenedores, consulte el [Servicio de contenedores de Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="45014-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="45014-143">Para desarrollar aplicaciones de .NET Core con Visual Studio, consulte [Docker Tools para Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="45014-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

