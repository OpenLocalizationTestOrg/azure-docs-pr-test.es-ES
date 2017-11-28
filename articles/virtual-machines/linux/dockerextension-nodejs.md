---
title: "Hola aaaUse extensión de máquina virtual de Azure Docker con hello 1.0 de CLI de Azure | Documentos de Microsoft"
description: "Conozca cómo toouse Hola tooquickly de extensión de máquina virtual Docker e implementar de forma segura un entorno de Docker en Azure con plantillas de administrador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="33eea-103">Crear un entorno de Docker en Azure con extensión de máquina virtual Docker Hola Hola 1.0 de CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="33eea-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="33eea-104">Docker es una plataforma de creación de imágenes que le permite trabajar de tooquickly con contenedores en Linux (y también de Windows) y la administración de contenedor populares.</span><span class="sxs-lookup"><span data-stu-id="33eea-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="33eea-105">En Azure, existen varias maneras puede implementar según las necesidades de tooyour de Docker.</span><span class="sxs-lookup"><span data-stu-id="33eea-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="33eea-106">En este artículo se centra sobre el uso de la extensión de máquina virtual Docker de Hola y plantillas del Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="33eea-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="33eea-107">Para obtener más información acerca de los métodos de implementación diferentes de hello, incluido el uso de la máquina de Docker y servicios de contenedor de Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="33eea-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="33eea-108">prototipo de tooquickly una aplicación, puede crear un único host de Docker con [Docker máquina](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="33eea-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="33eea-109">En entornos grandes y más estables, puede usar la extensión de máquina virtual de Azure Docker hello, que también es compatible con [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate implementaciones de contenedor coherente.</span><span class="sxs-lookup"><span data-stu-id="33eea-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="33eea-110">Este artículo se detallan mediante la extensión de máquina virtual de Azure Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="33eea-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="33eea-111">toobuild para entornos de producción entornos escalables que proporcionan herramientas de programación y administración adicionales, puede implementar un [Docker Swarm clúster en los servicios de contenedor de Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="33eea-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="33eea-112">Tarea CLI versiones toocomplete hello</span><span class="sxs-lookup"><span data-stu-id="33eea-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="33eea-113">Puede completar la tarea hello mediante uno de hello después de las versiones CLI:</span><span class="sxs-lookup"><span data-stu-id="33eea-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="33eea-114">[Azure 1.0 de CLI](#azure-docker-vm-extension-overview) – nuestro CLI para hello clásico y recursos administración modelos de implementación (en este artículo)</span><span class="sxs-lookup"><span data-stu-id="33eea-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="33eea-115">[Azure 2.0 CLI](dockerextension.md) -nuestro CLI de próxima generación para el modelo de implementación de administración de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="33eea-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="33eea-116">Introducción a la extensión de máquina virtual de Docker para Azure</span><span class="sxs-lookup"><span data-stu-id="33eea-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="33eea-117">Hola extensión de máquina virtual de Azure Docker instala y configura el demonio de Docker Hola, cliente de Docker y Docker Compose en la máquina virtual (VM) de Linux.</span><span class="sxs-lookup"><span data-stu-id="33eea-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="33eea-118">Mediante el uso de extensión de máquina virtual de Azure Docker hello, tiene más control y características que simplemente se usa máquina Docker o creación de host de Docker Hola usted mismo.</span><span class="sxs-lookup"><span data-stu-id="33eea-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="33eea-119">Estos más características, como [Docker Compose](https://docs.docker.com/compose/overview/), asegúrese de extensión de máquina virtual de Azure Docker Hola adecuado para entornos de producción o desarrollador más sólidos.</span><span class="sxs-lookup"><span data-stu-id="33eea-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="33eea-120">Las plantillas de administrador de recursos Azure definen estructura completa de Hola de su entorno.</span><span class="sxs-lookup"><span data-stu-id="33eea-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="33eea-121">Las plantillas permiten toocreate y configurar recursos tales como host de Docker de hello las máquinas virtuales, almacenamiento, controles de acceso basado en roles (RBAC) y diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="33eea-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="33eea-122">Puede volver a usar estas implementaciones adicionales de toocreate de plantillas de una manera coherente.</span><span class="sxs-lookup"><span data-stu-id="33eea-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="33eea-123">Para más información sobre Azure Resource Manager, consulte [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33eea-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="33eea-124">Implementar una plantilla con hello extensión de máquina virtual de Azure Docker</span><span class="sxs-lookup"><span data-stu-id="33eea-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="33eea-125">Vamos a usar una existente toocreate de plantilla de inicio rápido un Ubuntu VM que use tooinstall de extensión de máquina virtual de Azure Docker hello y configurar host de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="33eea-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="33eea-126">Puede ver la plantilla de hello aquí: [implementación Simple de una VM de Ubuntu con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="33eea-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="33eea-127">Necesita hello [CLI de Azure más reciente](../../cli-install-nodejs.md) instalado e inició sesión mediante el modo de administrador de recursos de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="33eea-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="33eea-128">Implementar la plantilla de hello mediante Hola CLI de Azure, especifique Hola plantilla URI.</span><span class="sxs-lookup"><span data-stu-id="33eea-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="33eea-129">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación.</span><span class="sxs-lookup"><span data-stu-id="33eea-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="33eea-130">Use el nombre y la ubicación de su grupo de recursos como sigue:</span><span class="sxs-lookup"><span data-stu-id="33eea-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="33eea-131">Responder Hola indicaciones tooname su cuenta de almacenamiento, proporcione un nombre de usuario y una contraseña y proporcione un nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="33eea-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="33eea-132">Hola de salida es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33eea-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="33eea-133">Hola CLI de Azure devuelve toohello símbolo del sistema después de unos pocos segundos, pero el host Docker todavía se está creando y configurado por hello extensión de máquina virtual de Azure Docker.</span><span class="sxs-lookup"><span data-stu-id="33eea-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="33eea-134">Se tarda unos minutos para hello toofinish de implementación.</span><span class="sxs-lookup"><span data-stu-id="33eea-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="33eea-135">Puede ver detalles sobre el estado de host de Docker Hola con hello `azure vm show` comando.</span><span class="sxs-lookup"><span data-stu-id="33eea-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="33eea-136">Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="33eea-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="33eea-137">Escriba el nombre de Hola Hola del grupo de recursos que creó en hello anterior paso:</span><span class="sxs-lookup"><span data-stu-id="33eea-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="33eea-138">Hola salida de hello `azure vm show` comando es similar toohello siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="33eea-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="33eea-139">Cerca de la parte superior de Hola de salida de hello, vea hello **ProvisioningState** de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33eea-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="33eea-140">Cuando se muestra *correcto*, ha terminado la implementación de Hola y puede SSH toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="33eea-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="33eea-141">Final de hello de la salida de hello, *FQDN* muestra el nombre de dominio completo de hello del host Docker.</span><span class="sxs-lookup"><span data-stu-id="33eea-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="33eea-142">Este FQDN es lo que usa host de Docker de tooSSH tooyour Hola restantes pasos.</span><span class="sxs-lookup"><span data-stu-id="33eea-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="33eea-143">Implementación del primer contenedor nginx</span><span class="sxs-lookup"><span data-stu-id="33eea-143">Deploy your first nginx container</span></span>
<span data-ttu-id="33eea-144">Una vez haya terminado implementación hello, SSH tooyour nuevo host de Docker desde el equipo local.</span><span class="sxs-lookup"><span data-stu-id="33eea-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="33eea-145">Escriba su nombre de usuario y el FQDN como sigue:</span><span class="sxs-lookup"><span data-stu-id="33eea-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="33eea-146">Una vez iniciada la sesión toohello host Docker, vamos a ejecutar un contenedor de nginx:</span><span class="sxs-lookup"><span data-stu-id="33eea-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="33eea-147">salida de Hello es similar toohello siguiente ejemplo como hello nginx imagen se descarga y un contenedor inicia:</span><span class="sxs-lookup"><span data-stu-id="33eea-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="33eea-148">Comprobar el estado de Hola de contenedores de Hola que se ejecutan en el host Docker como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="33eea-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="33eea-149">salida de Hello es similar toohello ejemplo siguiente, que muestra que el contenedor de hello nginx se está ejecutando y los puertos TCP 80 y 443 y reenvían:</span><span class="sxs-lookup"><span data-stu-id="33eea-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="33eea-150">toosee el contenedor en acción, abra una copia de seguridad un explorador web y escriba el nombre FQDN de hello del host Docker:</span><span class="sxs-lookup"><span data-stu-id="33eea-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Ejecución del contenedor ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="33eea-152">Referencia sobre la plantilla de la extensión de máquina virtual de Docker para Azure</span><span class="sxs-lookup"><span data-stu-id="33eea-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="33eea-153">ejemplo de Hola anterior usa una plantilla existente de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="33eea-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="33eea-154">También puede implementar la extensión de máquina virtual de Azure Docker Hola con sus propias plantillas de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="33eea-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="33eea-155">toodo por lo tanto, agregar Hola después tooyour plantillas de administrador de recursos, la definición de hello *vmName* de la máquina virtual correctamente:</span><span class="sxs-lookup"><span data-stu-id="33eea-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="33eea-156">Puede encontrar un tutorial más detallado sobre el uso de plantillas de Resource Manager en [Información general de Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33eea-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="33eea-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="33eea-157">Next steps</span></span>
<span data-ttu-id="33eea-158">Puede ser conveniente demasiado[configurar el puerto TCP de hello Docker daemon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprender [seguridad Docker](https://docs.docker.com/engine/security/security/), o implementar contenedores con [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="33eea-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="33eea-159">Para obtener más información sobre Hola extensión de máquina virtual de Azure Docker propio, vea hello [GitHub proyecto](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="33eea-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="33eea-160">Leer más información acerca de las opciones de implementación de Docker adicionales de hello en Azure:</span><span class="sxs-lookup"><span data-stu-id="33eea-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="33eea-161">Usar el equipo de Docker con hello Azure controlador</span><span class="sxs-lookup"><span data-stu-id="33eea-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="33eea-162">[Introducción a Docker y redactar toodefine y ejecutar una aplicación de contenedor múltiples en una máquina virtual de Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="33eea-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="33eea-163">Implementación de un clúster del servicio Contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="33eea-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

