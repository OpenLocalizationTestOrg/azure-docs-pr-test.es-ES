---
title: Uso de Docker Compose en una VM Linux en Azure | Microsoft Docs
description: "Uso de Docker y Compose en máquinas virtuales con Linux mediante la CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="cea36-103">Introducción a Docker y Compose para definir y ejecutar una aplicación de contenedores múltiples en Azure</span><span class="sxs-lookup"><span data-stu-id="cea36-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="cea36-104">Con [Compose](http://github.com/docker/compose), usará un archivo de texto simple para definir una aplicación compuesta de varios contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="cea36-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="cea36-105">Después, puede poner en marcha la aplicación con un solo comando que realiza todos los pasos para implementarla en el entorno definido.</span><span class="sxs-lookup"><span data-stu-id="cea36-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="cea36-106">Como ejemplo, en este artículo se muestra cómo configurar rápidamente un blog de WordPress con una base de datos SQL MariaDB de back-end en una máquina virtual Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="cea36-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="cea36-107">También puede utilizar Compose para configurar aplicaciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="cea36-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="cea36-108">Configuración de una máquina virtual Linux como host de Docker</span><span class="sxs-lookup"><span data-stu-id="cea36-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="cea36-109">Puede emplear diversos procedimientos de Azure, así como las imágenes y plantillas de Azure Resource Manager disponibles en Azure Marketplace, para crear una máquina virtual Linux y configurarla como host de Docker.</span><span class="sxs-lookup"><span data-stu-id="cea36-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="cea36-110">Por ejemplo, consulte [Uso de la extensión de VM de Docker para implementar el entorno](dockerextension.md) para crear rápidamente una máquina virtual Ubuntu con la extensión de máquina virtual de Azure Docker mediante el uso de una [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="cea36-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="cea36-111">Cuando utilice la extensión de máquina virtual de Docker, la máquina virtual se configurará automáticamente como un host de Docker.</span><span class="sxs-lookup"><span data-stu-id="cea36-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="cea36-112">Creación de un host de Docker con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="cea36-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="cea36-113">Instale la última versión de la [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión en una cuenta de Azure con [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="cea36-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="cea36-114">En primer lugar, cree un grupo de recursos para su entorno de Docker con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="cea36-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="cea36-115">En el ejemplo siguiente, se crea un grupo de recursos denominado *myResourceGroup* en la ubicación *westus*:</span><span class="sxs-lookup"><span data-stu-id="cea36-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="cea36-116">A continuación, implemente una VM con [az group deployment create](/cli/azure/group/deployment#create), que incluye la extensión de VM de Docker para Azure de [esta plantilla de Azure Resource Manager en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="cea36-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="cea36-117">Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="cea36-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="cea36-118">La implementación tarda unos minutos en finalizar.</span><span class="sxs-lookup"><span data-stu-id="cea36-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="cea36-119">Una vez finalizada la implementación, [vaya al paso siguiente](#verify-that-compose-is-installed) para SSH en la VM.</span><span class="sxs-lookup"><span data-stu-id="cea36-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="cea36-120">Opcionalmente, en lugar de devolver el control al símbolo del sistema y permitir que la implementación continúe en segundo plano, agregue la marca `--no-wait` al comando anterior.</span><span class="sxs-lookup"><span data-stu-id="cea36-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="cea36-121">Este proceso permite realizar otro trabajo en la CLI mientras continúa la implementación durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="cea36-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="cea36-122">Puede ver detalles sobre el estado del host de Docker con [az vm show](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="cea36-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="cea36-123">En el ejemplo siguiente, se comprueba el estado de la máquina virtual denominada *myDockerVM* (se trata del nombre predeterminado de la plantilla; no lo cambie) del grupo de recursos denominado *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="cea36-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="cea36-124">Cuando este comando devuelve un estado *correcto*, ha terminado la implementación y puede implementar SSH en la máquina virtual en el paso siguiente.</span><span class="sxs-lookup"><span data-stu-id="cea36-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="cea36-125">Comprobación de que se ha instalado Compose</span><span class="sxs-lookup"><span data-stu-id="cea36-125">Verify that Compose is installed</span></span>
<span data-ttu-id="cea36-126">Una vez que haya terminado la implementación, aplique SSH a su nuevo host de Docker mediante el nombre DNS que proporcionó durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="cea36-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="cea36-127">Puede usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` para ver los detalles de la máquina virtual, incluido el nombre DNS.</span><span class="sxs-lookup"><span data-stu-id="cea36-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="cea36-128">Para comprobar que Compose esté instalado en la máquina virtual, ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="cea36-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="cea36-129">Verá una salida similar a *docker-compose 1.6.2, build 4d72027*.</span><span class="sxs-lookup"><span data-stu-id="cea36-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="cea36-130">Si utiliza otro método para crear un host de Docker y necesita instalar Compose de forma manual, consulte la [documentación de esta herramienta](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="cea36-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="cea36-131">Creación de un archivo de configuración docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="cea36-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="cea36-132">A continuación, debe crear un archivo `docker-compose.yml` , que es simplemente un archivo de configuración para definir los contenedores de Docker para ejecutar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cea36-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="cea36-133">El archivo especifica la imagen que se ejecutará en cada contenedor (o podría ser una compilación de un Dockerfile), variables de entorno y dependencias necesarias, puertos y vínculos entre contenedores.</span><span class="sxs-lookup"><span data-stu-id="cea36-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="cea36-134">Para más información sobre la sintaxis del archivo YML, consulte la [referencia del archivo de Compose](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="cea36-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="cea36-135">Cree el archivo *docker-compose.yml* de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="cea36-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="cea36-136">Use el editor de texto que prefiera para agregar algunos datos al archivo.</span><span class="sxs-lookup"><span data-stu-id="cea36-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="cea36-137">En el ejemplo siguiente se usa el editor *vi*:</span><span class="sxs-lookup"><span data-stu-id="cea36-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="cea36-138">Pegue el siguiente ejemplo en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="cea36-138">Paste the following example into your text file.</span></span> <span data-ttu-id="cea36-139">Esta configuración usa imágenes del [Registro de DockerHub](https://registry.hub.docker.com/_/wordpress/) para instalar WordPress (el sistema de administración de contenido y blogs de código abierto) y una base de datos SQL MariaDB de back-end vinculada.</span><span class="sxs-lookup"><span data-stu-id="cea36-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="cea36-140">Escriba su propio *MYSQL_ROOT_PASSWORD* como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="cea36-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="cea36-141">inicio de los contenedores con Compose</span><span class="sxs-lookup"><span data-stu-id="cea36-141">Start the containers with Compose</span></span>
<span data-ttu-id="cea36-142">En el mismo directorio que el archivo *docker-compose.yml*, ejecute el comando siguiente (dependiendo de su entorno, quizás tenga que ejecutar `docker-compose` mediante `sudo`):</span><span class="sxs-lookup"><span data-stu-id="cea36-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="cea36-143">Este comando inicia los contenedores de Docker especificados en *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="cea36-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="cea36-144">Este paso tarda uno o dos minutos en completarse.</span><span class="sxs-lookup"><span data-stu-id="cea36-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="cea36-145">Verá un resultado similar al del siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cea36-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="cea36-146">Asegúrese de utilizar la opción **-d** al iniciar para que los contenedores se ejecuten continuamente en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="cea36-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="cea36-147">Para comprobar que los contenedores están activos, escriba `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="cea36-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="cea36-148">Debería ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="cea36-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="cea36-149">Ahora puede conectarse a WordPress directamente en la máquina virtual a través del puerto 80.</span><span class="sxs-lookup"><span data-stu-id="cea36-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="cea36-150">Abra un explorador web y escriba el nombre DNS de la máquina virtual (por ejemplo, `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="cea36-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="cea36-151">Ahora debería ver la pantalla de inicio de WordPress, donde se puede completar la instalación e iniciar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="cea36-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![Pantalla de inicio de WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="cea36-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cea36-153">Next steps</span></span>
* <span data-ttu-id="cea36-154">Consulte el [manual del usuario de extensión de máquina virtual de Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obtener más opciones de configuración de Docker y Compose en su máquina virtual de Docker.</span><span class="sxs-lookup"><span data-stu-id="cea36-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="cea36-155">Por ejemplo, una de ellas consiste en colocar el archivo YML de Compose (convertido a JSON) directamente en la configuración de la extensión de máquina virtual de Docker.</span><span class="sxs-lookup"><span data-stu-id="cea36-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="cea36-156">Consulte la [referencia de línea de comandos de Compose](http://docs.docker.com/compose/reference/) y el [manual del usuario](http://docs.docker.com/compose/) para obtener más ejemplos de compilación e implementación de aplicaciones con varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="cea36-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="cea36-157">Use una plantilla del Administrador de recursos de Azure, o bien una propia o una proporcionada por la [comunidad](https://azure.microsoft.com/documentation/templates/), para implementar una VM de Azure con Docker y una aplicación configurada con Compose.</span><span class="sxs-lookup"><span data-stu-id="cea36-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="cea36-158">Por ejemplo, la plantilla [Implementación de un blog de WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) usa Docker y Compose para implementar rápidamente WordPress con un back-end de MySQL en una máquina virtual de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="cea36-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="cea36-159">Pruebe a integrar Docker Compose con un clúster de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="cea36-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="cea36-160">Consulte [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso de Compose con Swarm) para conocer distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="cea36-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
