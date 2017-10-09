---
title: "Hola aaaUse extensión de máquina virtual de Azure Docker | Documentos de Microsoft"
description: "Obtenga información acerca cómo toouse Hola tooquickly de extensión de máquina virtual Docker y segura implementar un entorno de Docker en Azure con plantillas de administrador de recursos y Hola 2.0 de CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="42f7e-103">Crear un entorno de Docker en Azure con la extensión de máquina virtual Docker Hola</span><span class="sxs-lookup"><span data-stu-id="42f7e-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="42f7e-104">Docker es una plataforma de creación de imágenes que le permite trabajar de tooquickly con contenedores en Linux y administración de contenedor populares.</span><span class="sxs-lookup"><span data-stu-id="42f7e-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="42f7e-105">En Azure, existen varias maneras puede implementar según las necesidades de tooyour de Docker.</span><span class="sxs-lookup"><span data-stu-id="42f7e-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="42f7e-106">En este artículo se centra en utilizar la extensión de máquina virtual Docker de Hola y plantillas del Administrador de recursos de Azure con hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="42f7e-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="42f7e-107">También puede realizar estos pasos con hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="42f7e-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="42f7e-108">Introducción a la extensión de máquina virtual de Docker para Azure</span><span class="sxs-lookup"><span data-stu-id="42f7e-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="42f7e-109">Hola extensión de máquina virtual de Azure Docker instala y configura el demonio de Docker Hola, cliente de Docker y Docker Compose en la máquina virtual (VM) de Linux.</span><span class="sxs-lookup"><span data-stu-id="42f7e-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="42f7e-110">Mediante el uso de extensión de máquina virtual de Azure Docker hello, tiene más control y características que simplemente se usa máquina Docker o creación de host de Docker Hola usted mismo.</span><span class="sxs-lookup"><span data-stu-id="42f7e-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="42f7e-111">Estos más características, como [Docker Compose](https://docs.docker.com/compose/overview/), asegúrese de extensión de máquina virtual de Azure Docker Hola adecuado para entornos de producción o desarrollador más sólidos.</span><span class="sxs-lookup"><span data-stu-id="42f7e-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="42f7e-112">Para obtener más información acerca de los métodos de implementación diferentes de hello, incluido el uso de la máquina de Docker y servicios de contenedor de Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="42f7e-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="42f7e-113">prototipo de tooquickly una aplicación, puede crear un único host de Docker con [Docker máquina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="42f7e-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="42f7e-114">toobuild para entornos de producción entornos escalables que proporcionan herramientas de programación y administración adicionales, puede implementar un [Docker Swarm clúster en los servicios de contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="42f7e-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="42f7e-115">Implementar una plantilla con hello extensión de máquina virtual de Azure Docker</span><span class="sxs-lookup"><span data-stu-id="42f7e-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="42f7e-116">Vamos a usar una existente toocreate de plantilla de inicio rápido un Ubuntu VM que use tooinstall de extensión de máquina virtual de Azure Docker hello y configurar host de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="42f7e-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="42f7e-117">Puede ver la plantilla de hello aquí: [implementación Simple de una VM de Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="42f7e-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="42f7e-118">Necesita hello más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) instalado y registrado en tooan cuenta de Azure mediante [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="42f7e-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="42f7e-119">En primer lugar, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="42f7e-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="42f7e-120">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación:</span><span class="sxs-lookup"><span data-stu-id="42f7e-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="42f7e-121">A continuación, implementar una máquina virtual con [Crear implementación de grupo az](/cli/azure/group/deployment#create) que incluye la extensión de máquina virtual de Azure Docker Hola de [esta plantilla de administrador de recursos de Azure en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="42f7e-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="42f7e-122">Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP* de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="42f7e-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="42f7e-123">Se tarda unos minutos para hello toofinish de implementación.</span><span class="sxs-lookup"><span data-stu-id="42f7e-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="42f7e-124">Una vez finalizada la implementación de hello, [mover paso toonext](#deploy-your-first-nginx-container) tooSSH tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="42f7e-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="42f7e-125">Opcionalmente, el símbolo del sistema de tooinstead control devuelto toohello e implementación de hello permiten continúan en segundo plano de hello, agregue hello `--no-wait` marca toohello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="42f7e-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="42f7e-126">Este proceso le permite tooperform otro trabajo en hello CLI mientras continúa la implementación de Hola durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="42f7e-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="42f7e-127">A continuación, puede ver detalles sobre el estado de host de hello Docker con [mostrar de la máquina virtual de az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="42f7e-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="42f7e-128">Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="42f7e-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="42f7e-129">Cuando vuelve este comando *correcto*, ha terminado la implementación de Hola y puede SSH toohello VM Hola siguiendo el paso.</span><span class="sxs-lookup"><span data-stu-id="42f7e-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="42f7e-130">Implementación del primer contenedor nginx</span><span class="sxs-lookup"><span data-stu-id="42f7e-130">Deploy your first nginx container</span></span>
<span data-ttu-id="42f7e-131">usar tooview detalles de la máquina virtual, incluyendo nombre DNS de hello, `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="42f7e-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="42f7e-132">SSH tooyour nuevas Docker de host desde el equipo local como sigue:</span><span class="sxs-lookup"><span data-stu-id="42f7e-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="42f7e-133">Una vez iniciada la sesión toohello host Docker, vamos a ejecutar un contenedor de nginx:</span><span class="sxs-lookup"><span data-stu-id="42f7e-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="42f7e-134">salida de Hello es similar toohello siguiente ejemplo como hello nginx imagen se descarga y un contenedor inicia:</span><span class="sxs-lookup"><span data-stu-id="42f7e-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="42f7e-135">Comprobar el estado de Hola de contenedores de Hola que se ejecutan en el host Docker como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="42f7e-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="42f7e-136">salida de Hello es similar toohello ejemplo siguiente, que muestra que el contenedor de hello nginx se está ejecutando y los puertos TCP 80 y 443 y reenvían:</span><span class="sxs-lookup"><span data-stu-id="42f7e-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="42f7e-137">toosee el contenedor en acción, abra una copia de seguridad un explorador web y escriba el nombre DNS de hello del host Docker:</span><span class="sxs-lookup"><span data-stu-id="42f7e-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Ejecución del contenedor ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="42f7e-139">Referencia sobre la plantilla de la extensión de máquina virtual de Docker para Azure</span><span class="sxs-lookup"><span data-stu-id="42f7e-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="42f7e-140">ejemplo de Hola anterior usa una plantilla existente de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="42f7e-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="42f7e-141">También puede implementar la extensión de máquina virtual de Azure Docker Hola con sus propias plantillas de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="42f7e-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="42f7e-142">toodo por lo tanto, agregar Hola después tooyour plantillas de administrador de recursos, la definición de hello `vmName` de la máquina virtual correctamente:</span><span class="sxs-lookup"><span data-stu-id="42f7e-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="42f7e-143">Puede encontrar un tutorial más detallado sobre el uso de plantillas de Resource Manager en [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42f7e-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42f7e-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="42f7e-144">Next steps</span></span>
<span data-ttu-id="42f7e-145">Puede ser conveniente demasiado[configurar el puerto TCP de hello Docker daemon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprender [seguridad Docker](https://docs.docker.com/engine/security/security/), o implementar contenedores con [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="42f7e-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="42f7e-146">Para obtener más información sobre Hola extensión de máquina virtual de Azure Docker propio, vea hello [GitHub proyecto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="42f7e-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="42f7e-147">Leer más información acerca de las opciones de implementación de Docker adicionales de hello en Azure:</span><span class="sxs-lookup"><span data-stu-id="42f7e-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="42f7e-148">Usar el equipo de Docker con hello Azure controlador</span><span class="sxs-lookup"><span data-stu-id="42f7e-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="42f7e-149">[Introducción a Docker y redactar toodefine y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="42f7e-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="42f7e-150">Implementación de un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="42f7e-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

