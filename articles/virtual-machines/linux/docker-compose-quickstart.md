---
title: aaaUse Docker Compose en una VM de Linux en Azure | Documentos de Microsoft
description: "Cómo toouse Docker y Redactar en máquinas virtuales de Linux con Hola CLI de Azure"
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
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="c550f-103">Obtener partió toodefine Docker y crear y ejecutar una aplicación de contenedor de varios en Azure</span><span class="sxs-lookup"><span data-stu-id="c550f-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="c550f-104">Con [redactar](http://github.com/docker/compose), use un toodefine del archivo de texto simple de una aplicación que consta de varios contenedores de Docker.</span><span class="sxs-lookup"><span data-stu-id="c550f-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="c550f-105">, A continuación, haga clic en la aplicación en un único comando que hace todo lo que toodeploy el entorno definido.</span><span class="sxs-lookup"><span data-stu-id="c550f-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="c550f-106">Por ejemplo, este artículo muestra cómo tooquickly configurado un blog de WordPress con un back-end de base de datos MariaDB SQL en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c550f-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="c550f-107">También puede utilizar tooset de redacción de seguridad de aplicaciones más complejas.</span><span class="sxs-lookup"><span data-stu-id="c550f-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="c550f-108">Configuración de una máquina virtual Linux como host de Docker</span><span class="sxs-lookup"><span data-stu-id="c550f-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="c550f-109">Puede usar diversos procedimientos de Azure y las imágenes disponibles o plantillas de administrador de recursos en Azure Marketplace de hello toocreate una VM de Linux y se configura como un host Docker.</span><span class="sxs-lookup"><span data-stu-id="c550f-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="c550f-110">Por ejemplo, vea [con hello extensión de máquina virtual Docker toodeploy su entorno](dockerextension.md) tooquickly crear una VM Ubuntu con hello extensión de máquina virtual de Azure Docker mediante un [plantilla de inicio rápido](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c550f-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c550f-111">Cuando se utiliza la extensión de máquina virtual Docker de hello, la máquina virtual se configura automáticamente como un host Docker y redactar ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="c550f-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="c550f-112">Creación de un host de Docker con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c550f-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="c550f-113">Hola de instalación más reciente [CLI de Azure 2.0](/cli/azure/install-az-cli2) e inicie sesión con cuenta de Azure de tooan [inicio de sesión de az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c550f-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c550f-114">En primer lugar, cree un grupo de recursos para su entorno de Docker con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c550f-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c550f-115">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *oesteee. UU.* ubicación:</span><span class="sxs-lookup"><span data-stu-id="c550f-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c550f-116">A continuación, implementar una máquina virtual con [Crear implementación de grupo az](/cli/azure/group/deployment#create) que incluye la extensión de máquina virtual de Azure Docker Hola de [esta plantilla de administrador de recursos de Azure en GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c550f-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c550f-117">Proporcione sus propios valores para *newStorageAccountName*, *adminUsername*, *adminPassword* y *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="c550f-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c550f-118">Se tarda unos minutos para hello toofinish de implementación.</span><span class="sxs-lookup"><span data-stu-id="c550f-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c550f-119">Una vez finalizada la implementación de hello, [mover paso toonext](#verify-that-compose-is-installed) tooSSH tooyour máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c550f-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="c550f-120">Opcionalmente, el símbolo del sistema de tooinstead control devuelto toohello e implementación de hello permiten continúan en segundo plano de hello, agregue hello `--no-wait` marca toohello anterior comando.</span><span class="sxs-lookup"><span data-stu-id="c550f-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="c550f-121">Este proceso le permite tooperform otro trabajo en hello CLI mientras continúa la implementación de Hola durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c550f-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="c550f-122">A continuación, puede ver detalles sobre el estado de host de hello Docker con [mostrar de la máquina virtual de az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c550f-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c550f-123">Hello en el ejemplo siguiente se comprueba estado Hola de máquina virtual denominada hello *myDockerVM* (Hola nombre predeterminado de la plantilla de hello: no cambie este nombre) en grupo de recursos de hello llamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c550f-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c550f-124">Cuando vuelve este comando *correcto*, ha terminado la implementación de Hola y puede SSH toohello VM Hola siguiendo el paso.</span><span class="sxs-lookup"><span data-stu-id="c550f-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="c550f-125">Comprobación de que se ha instalado Compose</span><span class="sxs-lookup"><span data-stu-id="c550f-125">Verify that Compose is installed</span></span>
<span data-ttu-id="c550f-126">Una vez finalizada la implementación de hello, SSH tooyour nuevo host Docker utilizando el nombre DNS de Hola que proporcionó durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="c550f-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="c550f-127">Puede usar `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview detalles de la máquina virtual, incluido el nombre DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="c550f-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c550f-128">toocheck que componen se instala en Hola de máquina virtual, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="c550f-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="c550f-129">Obtiene un resultado similar demasiado*docker-redactar 1.6.2, compilación 4D 72027*.</span><span class="sxs-lookup"><span data-stu-id="c550f-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="c550f-130">Si usa otro método toocreate un host Docker y necesita tooinstall crear usted mismo, consulte hello [redactar documentación](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c550f-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="c550f-131">Creación de un archivo de configuración docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="c550f-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="c550f-132">A continuación creará un `docker-compose.yml` archivo, que es simplemente un archivo de configuración de texto, toorun de contenedores de Docker toodefine hello en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c550f-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="c550f-133">archivo Hello especifica Hola imagen toorun en cada contenedor (o bien, podría deberse a una compilación de un archivo Dockerfile), variables de entorno necesarias y las dependencias, puertos y vínculos de hello entre contenedores.</span><span class="sxs-lookup"><span data-stu-id="c550f-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="c550f-134">Para más información sobre la sintaxis del archivo YML, consulte la [referencia del archivo de Compose](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="c550f-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="c550f-135">Crear hello *docker compose.yml* como sigue:</span><span class="sxs-lookup"><span data-stu-id="c550f-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="c550f-136">Utilice la tooadd del editor de texto que prefiera algunos archivos de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="c550f-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="c550f-137">Hello en el ejemplo siguiente se usa hello *vi* editor:</span><span class="sxs-lookup"><span data-stu-id="c550f-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="c550f-138">Pegue Hola siguiente ejemplo en el archivo de texto.</span><span class="sxs-lookup"><span data-stu-id="c550f-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="c550f-139">Esta configuración usa las imágenes de hello [DockerHub registro](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (sistema de administración contenido y creación de blogs de código abierto Hola) y un servidor vinculado MariaDB SQL de base de datos.</span><span class="sxs-lookup"><span data-stu-id="c550f-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="c550f-140">Escriba su propio *MYSQL_ROOT_PASSWORD* como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="c550f-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="c550f-141">Contenedores de Hola de inicio con redactar</span><span class="sxs-lookup"><span data-stu-id="c550f-141">Start hello containers with Compose</span></span>
<span data-ttu-id="c550f-142">En Hola mismo directorio como su *docker compose.yml* archivo, ejecute el siguiente comando de hello (dependiendo de su entorno, deberá toorun `docker-compose` con `sudo`):</span><span class="sxs-lookup"><span data-stu-id="c550f-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c550f-143">Este comando inicia contenedores de Docker Hola especificados en *docker compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="c550f-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="c550f-144">Tarda un minuto o dos para este paso toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c550f-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="c550f-145">Vea toohello similar de salida siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c550f-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="c550f-146">Estar seguro de hello toouse **-d** opción Inicio para que los contenedores de Hola se ejecutan en segundo plano de hello continuamente.</span><span class="sxs-lookup"><span data-stu-id="c550f-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="c550f-147">tooverify que son contenedores de hello, tipo `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="c550f-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="c550f-148">Debería ver algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c550f-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="c550f-149">Ahora puede conectarse tooWordPress directamente en hello VM en el puerto 80.</span><span class="sxs-lookup"><span data-stu-id="c550f-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="c550f-150">Abra un explorador web y escriba el nombre DNS de saludo de la máquina virtual (como `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="c550f-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="c550f-151">Ahora debería ver Hola que WordPress iniciar pantalla, donde puede completar la instalación de Hola y empezar a trabajar con la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="c550f-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Pantalla de inicio de WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="c550f-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c550f-153">Next steps</span></span>
* <span data-ttu-id="c550f-154">Vaya toohello [Guía de usuario de extensión de máquina virtual Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) para obtener más opciones tooconfigure Docker y Redactar en la máquina virtual Docker.</span><span class="sxs-lookup"><span data-stu-id="c550f-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="c550f-155">Por ejemplo, una opción es tooput redactar yml archivo hello (tooJSON convertido) directamente en la configuración de Hola de hello extensión de máquina virtual de Docker.</span><span class="sxs-lookup"><span data-stu-id="c550f-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="c550f-156">Extraer del repositorio hello [crear la referencia de línea de comandos](http://docs.docker.com/compose/reference/) y [Guía de usuario](http://docs.docker.com/compose/) para obtener más ejemplos de crear e implementar aplicaciones de contenedor de varios.</span><span class="sxs-lookup"><span data-stu-id="c550f-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="c550f-157">Usar una plantilla de Azure Resource Manager, ya sea su propio o uno proceden de Hola [Comunidad](https://azure.microsoft.com/documentation/templates/), toodeploy una VM de Azure con Docker y una aplicación prepararle redactar.</span><span class="sxs-lookup"><span data-stu-id="c550f-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="c550f-158">Por ejemplo, hello [implementar un blog de WordPress con Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) plantilla utiliza Docker y redactar tooquickly implementar WordPress con un back-end de MySQL en una VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c550f-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="c550f-159">Pruebe a integrar Docker Compose con un clúster de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c550f-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="c550f-160">Consulte [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) (Uso de Compose con Swarm) para conocer distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="c550f-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
