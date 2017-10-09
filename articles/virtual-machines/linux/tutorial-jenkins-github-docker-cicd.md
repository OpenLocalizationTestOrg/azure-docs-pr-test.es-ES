---
title: "una canalización de desarrollo en Azure con Jenkins aaaCreate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate un Jenkins virtual automático en Azure que extrae desde GitHub en cada código de confirmación y crea a una nuevo Docker contenedor toorun la aplicación"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c079e3c9186c9da0a3e51e1823215779c565e0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-development-infrastructure-on-a-linux-vm-in-azure-with-jenkins-github-and-docker"></a><span data-ttu-id="eaaff-103">¿Cómo toocreate una infraestructura de desarrollo en una VM de Linux en Azure con Jenkins, GitHub y Docker</span><span class="sxs-lookup"><span data-stu-id="eaaff-103">How toocreate a development infrastructure on a Linux VM in Azure with Jenkins, GitHub, and Docker</span></span>
<span data-ttu-id="eaaff-104">tooautomate Hola compilación y prueba la fase de desarrollo de aplicaciones, puede usar una integración continua y la canalización de implementación (CI/CD).</span><span class="sxs-lookup"><span data-stu-id="eaaff-104">tooautomate hello build and test phase of application development, you can use a continuous integration and deployment (CI/CD) pipeline.</span></span> <span data-ttu-id="eaaff-105">En este tutorial, creará una canalización de CI/CD en una máquina virtual de Azure, y aprenderá los siguientes temas:</span><span class="sxs-lookup"><span data-stu-id="eaaff-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaaff-106">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="eaaff-107">Instalar y configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-107">Install and configure Jenkins</span></span>
> * <span data-ttu-id="eaaff-108">Crear la integración de webhook entre GitHub y Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-108">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="eaaff-109">Crear y desencadenar trabajos de compilación de Jenkins desde confirmaciones de GitHub</span><span class="sxs-lookup"><span data-stu-id="eaaff-109">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="eaaff-110">Crear una imagen de Docker para la aplicación</span><span class="sxs-lookup"><span data-stu-id="eaaff-110">Create a Docker image for your app</span></span>
> * <span data-ttu-id="eaaff-111">Comprobar que GitHub confirma la imagen de Docker de nueva compilación y actualiza la aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="eaaff-111">Verify GitHub commits build new Docker image and updates running app</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eaaff-112">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="eaaff-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eaaff-113">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eaaff-114">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eaaff-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-jenkins-instance"></a><span data-ttu-id="eaaff-115">Creación de la instancia de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-115">Create Jenkins instance</span></span>
<span data-ttu-id="eaaff-116">En un tutorial anterior en [cómo toocustomize una máquina virtual de Linux en el primer arranque](tutorial-automate-vm-deployment.md), también habrá aprendido cómo tooautomate personalización de máquina virtual con init de la nube.</span><span class="sxs-lookup"><span data-stu-id="eaaff-116">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="eaaff-117">Este tutorial utiliza una nube init archivo tooinstall Jenkins y Docker en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="eaaff-117">This tutorial uses a cloud-init file tooinstall Jenkins and Docker on a VM.</span></span> 

<span data-ttu-id="eaaff-118">En el shell actual, cree un archivo denominado *init.txt nube* y pegar Hola siguiente configuración.</span><span class="sxs-lookup"><span data-stu-id="eaaff-118">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="eaaff-119">Por ejemplo, crear archivo hello en hello Shell en la nube, no en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="eaaff-119">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="eaaff-120">Escriba `sensible-editor cloud-init-jenkins.txt` toocreate Hola archivo y ver una lista de editores disponibles.</span><span class="sxs-lookup"><span data-stu-id="eaaff-120">Enter `sensible-editor cloud-init-jenkins.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="eaaff-121">Asegúrese de que ese archivo de nube-init todo Hola se copia correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="eaaff-121">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
write_files:
  - path: /etc/systemd/system/docker.service.d/docker.conf
    content: |
      [Service]
        ExecStart=
        ExecStart=/usr/bin/dockerd
  - path: /etc/docker/daemon.json
    content: |
      {
        "hosts": ["fd://","tcp://127.0.0.1:2375"]
      }
runcmd:
  - wget -q -O - https://jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add -
  - sh -c 'echo deb http://pkg.jenkins-ci.org/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  - apt-get update && apt-get install jenkins -y
  - curl -sSL https://get.docker.com/ | sh
  - usermod -aG docker azureuser
  - usermod -aG docker jenkins
  - service jenkins restart
```

<span data-ttu-id="eaaff-122">Antes de poder crear una máquina virtual, cree un grupo de recursos con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="eaaff-122">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="eaaff-123">Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroupJenkins* en hello *eastus* ubicación:</span><span class="sxs-lookup"><span data-stu-id="eaaff-123">hello following example creates a resource group named *myResourceGroupJenkins* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupJenkins --location eastus
```

<span data-ttu-id="eaaff-124">Ahora cree una máquina virtual con el comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="eaaff-124">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="eaaff-125">Hola de uso `--custom-data` toopass de parámetro en el archivo de configuración de nube init.</span><span class="sxs-lookup"><span data-stu-id="eaaff-125">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="eaaff-126">Proporcione la ruta de acceso completa de hello demasiado*nube-init-jenkins.txt* si guarda el archivo hello fuera de su directorio de trabajo actual.</span><span class="sxs-lookup"><span data-stu-id="eaaff-126">Provide hello full path too*cloud-init-jenkins.txt* if you saved hello file outside of your present working directory.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroupJenkins \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-jenkins.txt
```

<span data-ttu-id="eaaff-127">Se tarda unos minutos para hello toobe de máquina virtual creada y configurada.</span><span class="sxs-lookup"><span data-stu-id="eaaff-127">It takes a few minutes for hello VM toobe created and configured.</span></span>

<span data-ttu-id="eaaff-128">tooallow web tooreach de tráfico de la máquina virtual, use [az de vm abrir puerto](/cli/azure/vm#open-port) tooopen puerto *8080* para tráfico Jenkins y el puerto *1337* para aplicación de Node.js de hello es toorun usa una aplicación de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="eaaff-128">tooallow web traffic tooreach your VM, use [az vm open-port](/cli/azure/vm#open-port) tooopen port *8080* for Jenkins traffic and port *1337* for hello Node.js app that is used toorun a sample app:</span></span>

```azurecli-interactive 
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 8080 --priority 1001
az vm open-port --resource-group myResourceGroupJenkins --name myVM --port 1337 --priority 1002
```


## <a name="configure-jenkins"></a><span data-ttu-id="eaaff-129">Configuración de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-129">Configure Jenkins</span></span>
<span data-ttu-id="eaaff-130">tooaccess su Jenkins la instancia, obtener dirección IP pública de saludo de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="eaaff-130">tooaccess your Jenkins instance, obtain hello public IP address of your VM:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="eaaff-131">Por motivos de seguridad, se necesita contraseña de administrador inicial de hello tooenter que se almacena en un archivo de texto en el saludo de toostart VM que Jenkins instalar.</span><span class="sxs-lookup"><span data-stu-id="eaaff-131">For security purposes, you need tooenter hello initial admin password that is stored in a text file on your VM toostart hello Jenkins install.</span></span> <span data-ttu-id="eaaff-132">Usar dirección IP pública Hola obtenida en hello anterior paso tooSSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="eaaff-132">Use hello public IP address obtained in hello previous step tooSSH tooyour VM:</span></span>

```bash
ssh azureuser@<publicIps>
```

<span data-ttu-id="eaaff-133">Hola de vista `initialAdminPassword` para instalar sus Jenkins y se copia:</span><span class="sxs-lookup"><span data-stu-id="eaaff-133">View hello `initialAdminPassword` for your Jenkins install and copy it:</span></span>

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<span data-ttu-id="eaaff-134">Si el archivo hello aún no está disponible, espere unos minutos más en la nube init toocomplete Hola Jenkins e instalación de Docker.</span><span class="sxs-lookup"><span data-stu-id="eaaff-134">If hello file isn't available yet, wait a couple more minutes for cloud-init toocomplete hello Jenkins and Docker install.</span></span>

<span data-ttu-id="eaaff-135">Ahora, abra un explorador web y vaya demasiado`http://<publicIps>:8080`.</span><span class="sxs-lookup"><span data-stu-id="eaaff-135">Now open a web browser and go too`http://<publicIps>:8080`.</span></span> <span data-ttu-id="eaaff-136">Complete el saludo inicial Jenkins el programa de instalación como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="eaaff-136">Complete hello initial Jenkins setup as follows:</span></span>

- <span data-ttu-id="eaaff-137">Escriba hello *initialAdminPassword* obtenido de hello VM en el paso anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-137">Enter hello *initialAdminPassword* obtained from hello VM in hello previous step.</span></span>
- <span data-ttu-id="eaaff-138">Haga clic en **seleccione complementos tooinstall**</span><span class="sxs-lookup"><span data-stu-id="eaaff-138">Click **Select plugins tooinstall**</span></span>
- <span data-ttu-id="eaaff-139">Busque *GitHub* en el cuadro de texto de Hola a través de la parte superior de hello, seleccione hello *complemento de GitHub*, a continuación, haga clic en **instalar**</span><span class="sxs-lookup"><span data-stu-id="eaaff-139">Search for *GitHub* in hello text box across hello top, select hello *GitHub plugin*, then click **Install**</span></span>
- <span data-ttu-id="eaaff-140">toocreate una cuenta de usuario Jenkins, rellenar el formulario de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="eaaff-140">toocreate a Jenkins user account, fill out hello form as desired.</span></span> <span data-ttu-id="eaaff-141">Desde la perspectiva de seguridad, debe crear este primer usuario Jenkins en lugar de continuar como cuenta de administrador predeterminada de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-141">From a security perspective, you should create this first Jenkins user rather than continuing as hello default admin account.</span></span>
- <span data-ttu-id="eaaff-142">Cuando termine, haga clic en **Start using Jenkins** (Empezar a usar Jenkins).</span><span class="sxs-lookup"><span data-stu-id="eaaff-142">When finished, click **Start using Jenkins**</span></span>


## <a name="create-github-webhook"></a><span data-ttu-id="eaaff-143">Creación de un webhook de GitHub</span><span class="sxs-lookup"><span data-stu-id="eaaff-143">Create GitHub webhook</span></span>
<span data-ttu-id="eaaff-144">integración de hello tooconfigure con GitHub, abra hello [aplicación de ejemplo de Hola a todos Node.js](https://github.com/Azure-Samples/nodejs-docs-hello-world) desde el repositorio de ejemplos de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-144">tooconfigure hello integration with GitHub, open hello [Node.js Hello World sample app](https://github.com/Azure-Samples/nodejs-docs-hello-world) from hello Azure samples repo.</span></span> <span data-ttu-id="eaaff-145">toofork Hola repositorio tooyour posee la cuenta de GitHub, haga clic en hello **bifurcar** botón en la esquina superior derecha de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-145">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

<span data-ttu-id="eaaff-146">Crear un webhook dentro de bifurcación de Hola que creó:</span><span class="sxs-lookup"><span data-stu-id="eaaff-146">Create a webhook inside hello fork you created:</span></span>

- <span data-ttu-id="eaaff-147">Haga clic en **configuración**, a continuación, seleccione **integraciones & servicios** en el lado izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-147">Click **Settings**, then select **Integrations & services** on hello left-hand side.</span></span>
- <span data-ttu-id="eaaff-148">Haga clic en **Agregar servicio** y, luego, escriba *Jenkins* en el cuadro de filtro.</span><span class="sxs-lookup"><span data-stu-id="eaaff-148">Click **Add service**, then enter *Jenkins* in filter box.</span></span>
- <span data-ttu-id="eaaff-149">Seleccione *Jenkins (GitHub plugin)* Jenkins (complemento de GitHub).</span><span class="sxs-lookup"><span data-stu-id="eaaff-149">Select *Jenkins (GitHub plugin)*</span></span>
- <span data-ttu-id="eaaff-150">Para hello **Jenkins enlazar la dirección URL**, escriba `http://<publicIps>:8080/github-webhook/`.</span><span class="sxs-lookup"><span data-stu-id="eaaff-150">For hello **Jenkins hook URL**, enter `http://<publicIps>:8080/github-webhook/`.</span></span> <span data-ttu-id="eaaff-151">Asegúrese de incluir finales Hola /</span><span class="sxs-lookup"><span data-stu-id="eaaff-151">Make sure you include hello trailing /</span></span>
- <span data-ttu-id="eaaff-152">Haga clic en **Add service** (Agregar servicio).</span><span class="sxs-lookup"><span data-stu-id="eaaff-152">Click **Add service**</span></span>

![Agregar repositorio de GitHub webhook tooyour bifurcado](media/tutorial-jenkins-github-docker-cicd/github_webhook.png)


## <a name="create-jenkins-job"></a><span data-ttu-id="eaaff-154">Creación de trabajos de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-154">Create Jenkins job</span></span>
<span data-ttu-id="eaaff-155">toohave Jenkins responden tooan evento en GitHub como Confirmar código, cree un trabajo de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="eaaff-155">toohave Jenkins respond tooan event in GitHub such as committing code, create a Jenkins job.</span></span> 

<span data-ttu-id="eaaff-156">En el sitio Web Jenkins, haga clic en **crear trabajos nuevos** desde la página principal de hello:</span><span class="sxs-lookup"><span data-stu-id="eaaff-156">In your Jenkins website, click **Create new jobs** from hello home page:</span></span>

- <span data-ttu-id="eaaff-157">Escriba *HelloWorld* como nombre del trabajo.</span><span class="sxs-lookup"><span data-stu-id="eaaff-157">Enter *HelloWorld* as job name.</span></span> <span data-ttu-id="eaaff-158">Seleccione **Freestyle project** (Proyecto de estilo libre) y elija **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="eaaff-158">Choose **Freestyle project**, then select **OK**.</span></span>
- <span data-ttu-id="eaaff-159">En hello **General** sección, seleccione **GitHub** proyecto y escriba la dirección URL de repositorio bifurcada, como por ejemplo *https://github.com/iainfoulds/nodejs-docs-hello-world*</span><span class="sxs-lookup"><span data-stu-id="eaaff-159">Under hello **General** section, select **GitHub** project and enter your forked repo URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world*</span></span>
- <span data-ttu-id="eaaff-160">En hello **del origen de la administración de código** sección, seleccione **Git**, escriba su repositorio bifurcada *.git* de dirección URL, como *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span><span class="sxs-lookup"><span data-stu-id="eaaff-160">Under hello **Source code management** section, select **Git**, enter your forked repo *.git* URL, such as *https://github.com/iainfoulds/nodejs-docs-hello-world.git*</span></span>
- <span data-ttu-id="eaaff-161">En hello **crear desencadenadores** sección, seleccione **GitHub desencadenador de enlace para el sondeo de GITscm**.</span><span class="sxs-lookup"><span data-stu-id="eaaff-161">Under hello **Build Triggers** section, select **GitHub hook trigger for GITscm polling**.</span></span>
- <span data-ttu-id="eaaff-162">En hello **generar** sección, elija **agregar el paso de compilación**.</span><span class="sxs-lookup"><span data-stu-id="eaaff-162">Under hello **Build** section, choose **Add build step**.</span></span> <span data-ttu-id="eaaff-163">Seleccione **ejecutar shell**, a continuación, escriba `echo "Testing"` en la ventana de toocommand.</span><span class="sxs-lookup"><span data-stu-id="eaaff-163">Select **Execute shell**, then enter `echo "Testing"` in toocommand window.</span></span>
- <span data-ttu-id="eaaff-164">Haga clic en **guardar** final Hola de ventana de trabajos de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-164">Click **Save** at hello bottom of hello jobs window.</span></span>


## <a name="test-github-integration"></a><span data-ttu-id="eaaff-165">Prueba de la integración de GitHub</span><span class="sxs-lookup"><span data-stu-id="eaaff-165">Test GitHub integration</span></span>
<span data-ttu-id="eaaff-166">Hola tootest GitHub integración con Jenkins, confirmar un cambio en la bifurcación.</span><span class="sxs-lookup"><span data-stu-id="eaaff-166">tootest hello GitHub integration with Jenkins, commit a change in your fork.</span></span> 

<span data-ttu-id="eaaff-167">En GitHub de interfaz de usuario web, seleccione el repositorio bifurcada y, a continuación, haga clic en hello **index.js** archivo.</span><span class="sxs-lookup"><span data-stu-id="eaaff-167">Back in GitHub web UI, select your forked repo, and then click hello **index.js** file.</span></span> <span data-ttu-id="eaaff-168">Haga clic en tooedit de icono de lápiz Hola este archivo para que lea la línea 6:</span><span class="sxs-lookup"><span data-stu-id="eaaff-168">Click hello pencil icon tooedit this file so line 6 reads:</span></span>

```nodejs
response.end("Hello World!");
```

<span data-ttu-id="eaaff-169">toocommit los cambios, haga clic en hello **Confirmar cambios** situado en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-169">toocommit your changes, click hello **Commit changes** button at hello bottom.</span></span>

<span data-ttu-id="eaaff-170">En Jenkins, se inicia una nueva compilación en hello **generar historial** sección de esquina Hola inferior izquierda de la página de trabajo.</span><span class="sxs-lookup"><span data-stu-id="eaaff-170">In Jenkins, a new build starts under hello **Build history** section of hello bottom left-hand corner of your job page.</span></span> <span data-ttu-id="eaaff-171">Haga clic en el vínculo de número de compilación de Hola y seleccione **consola salida** en tamaño izquierdo Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-171">Click hello build number link and select **Console output** on hello left-hand size.</span></span> <span data-ttu-id="eaaff-172">Puede ver los pasos de hello Jenkins tarda más que el código se haya extraído de hello y GitHub compilación acción salidas mensaje hello `Testing` toohello consola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-172">You can view hello steps Jenkins takes as your code is pulled from GitHub and hello build action outputs hello message `Testing` toohello console.</span></span> <span data-ttu-id="eaaff-173">Cada vez que se realiza una confirmación en GitHub, hello webhook llega tooJenkins y desencadenan una nueva compilación de este modo.</span><span class="sxs-lookup"><span data-stu-id="eaaff-173">Each time a commit is made in GitHub, hello webhook reaches out tooJenkins and trigger a new build in this way.</span></span>


## <a name="define-docker-build-image"></a><span data-ttu-id="eaaff-174">Definición de la imagen de la compilación de Docker</span><span class="sxs-lookup"><span data-stu-id="eaaff-174">Define Docker build image</span></span>
<span data-ttu-id="eaaff-175">aplicación de Node.js de hello toosee ejecutando basándose en las confirmaciones de GitHub, permite generar una Docker aplicación hello de imagen toorun.</span><span class="sxs-lookup"><span data-stu-id="eaaff-175">toosee hello Node.js app running based on your GitHub commits, lets build a Docker image toorun hello app.</span></span> <span data-ttu-id="eaaff-176">imagen de Hola se crea a partir de un archivo Dockerfile que define cómo tooconfigure Hola contenedor que se ejecuta la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eaaff-176">hello image is built from a Dockerfile that defines how tooconfigure hello container that runs hello app.</span></span> 

<span data-ttu-id="eaaff-177">Desde Hola SSH conexión tooyour VM, cambie el directorio de área de trabajo de Jenkins de toohello con el nombre de trabajo de Hola que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="eaaff-177">From hello SSH connection tooyour VM, change toohello Jenkins workspace directory named after hello job you created in a previous step.</span></span> <span data-ttu-id="eaaff-178">En nuestro ejemplo, se llama "*HelloWorld*".</span><span class="sxs-lookup"><span data-stu-id="eaaff-178">In our example, that was named *HelloWorld*.</span></span>

```bash
cd /var/lib/jenkins/workspace/HelloWorld
```

<span data-ttu-id="eaaff-179">Cree un archivo con en este directorio de área de trabajo con `sudo sensible-editor Dockerfile` y pegar Hola siguiendo el contenido.</span><span class="sxs-lookup"><span data-stu-id="eaaff-179">Create a file with in this workspace directory with `sudo sensible-editor Dockerfile` and paste hello following contents.</span></span> <span data-ttu-id="eaaff-180">Asegúrese de que ese hello que dockerfile todo es copiado correctamente, especialmente Hola primera línea:</span><span class="sxs-lookup"><span data-stu-id="eaaff-180">Make sure that hello whole Dockerfile is copied correctly, especially hello first line:</span></span>

```yaml
FROM node:alpine

EXPOSE 1337

WORKDIR /var/www
COPY package.json /var/www/
RUN npm install
COPY index.js /var/www/
```

<span data-ttu-id="eaaff-181">Este Dockerfile usa Hola base Node.js imagen con Linux Alpine, puerto expone 1337 Hola aplicación Hola a todos, a continuación, se ejecuta, copia los archivos de aplicación Hola y la inicializa.</span><span class="sxs-lookup"><span data-stu-id="eaaff-181">This Dockerfile uses hello base Node.js image using Alpine Linux, exposes port 1337 that hello Hello World app runs on, then copies hello app files and initializes it.</span></span>


## <a name="create-jenkins-build-rules"></a><span data-ttu-id="eaaff-182">Creación de reglas de generación de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-182">Create Jenkins build rules</span></span>
<span data-ttu-id="eaaff-183">En un paso anterior, creó una regla de compilación Jenkins básica que den como resultado una consola de toohello de mensaje.</span><span class="sxs-lookup"><span data-stu-id="eaaff-183">In a previous step, you created a basic Jenkins build rule that output a message toohello console.</span></span> <span data-ttu-id="eaaff-184">Permite crear toouse de paso de compilación de hello nuestro Dockerfile y ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="eaaff-184">Lets create hello build step toouse our Dockerfile and run hello app.</span></span>

<span data-ttu-id="eaaff-185">En la instancia Jenkins, seleccione el trabajo de Hola que creó en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="eaaff-185">Back in your Jenkins instance, select hello job you created in a previous step.</span></span> <span data-ttu-id="eaaff-186">Haga clic en **configurar** en el lado izquierdo de Hola y desplácese hacia abajo toohello **generar** sección:</span><span class="sxs-lookup"><span data-stu-id="eaaff-186">Click **Configure** on hello left-hand side and scroll down toohello **Build** section:</span></span>

- <span data-ttu-id="eaaff-187">Quite el paso de compilación `echo "Test"`.</span><span class="sxs-lookup"><span data-stu-id="eaaff-187">Remove your existing `echo "Test"` build step.</span></span> <span data-ttu-id="eaaff-188">Haga clic en rojo cruzado en hello parte superior derecha del cuadro del paso de compilación existente de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-188">Click hello red cross on hello top right-hand corner of hello existing build step box.</span></span>
- <span data-ttu-id="eaaff-189">Haga clic en **Add build step** (Agregar paso de compilación) y seleccione **Execute shell** (Ejecutar shell).</span><span class="sxs-lookup"><span data-stu-id="eaaff-189">Click **Add build step**, then select **Execute shell**</span></span>
- <span data-ttu-id="eaaff-190">Hola **comando** cuadro, escriba Hola siga los comandos de Docker y luego seleccione **guardar**:</span><span class="sxs-lookup"><span data-stu-id="eaaff-190">In hello **Command** box, enter hello following Docker commands, then select **Save**:</span></span>

  ```bash
  docker build --tag helloworld:$BUILD_NUMBER .
  docker stop helloworld && docker rm helloworld
  docker run --name helloworld -p 1337:1337 helloworld:$BUILD_NUMBER node /var/www/index.js &
  ```

<span data-ttu-id="eaaff-191">pasos de compilación de Docker de Hello crean una imagen y etiqueta con hello Jenkins número de compilación de modo que pueda mantener un historial de imágenes.</span><span class="sxs-lookup"><span data-stu-id="eaaff-191">hello Docker build steps create an image and tag it with hello Jenkins build number so you can maintain a history of images.</span></span> <span data-ttu-id="eaaff-192">Los contenedores existentes que ejecuta la aplicación hello se detendrá y, a continuación, se quitará.</span><span class="sxs-lookup"><span data-stu-id="eaaff-192">Any existing containers running hello app are stopped and then removed.</span></span> <span data-ttu-id="eaaff-193">Un nuevo contenedor es iniciado con imagen hello y se ejecuta la aplicación Node.js en función de confirmaciones más recientes de hello en GitHub.</span><span class="sxs-lookup"><span data-stu-id="eaaff-193">A new container is then started using hello image and runs your Node.js app based on hello latest commits in GitHub.</span></span>


## <a name="test-your-pipeline"></a><span data-ttu-id="eaaff-194">Prueba de la canalización</span><span class="sxs-lookup"><span data-stu-id="eaaff-194">Test your pipeline</span></span>
<span data-ttu-id="eaaff-195">canalización completa de hello toosee en acción, editar hello *index.js* un archivo en el repositorio de GitHub bifurcado nuevo y haga clic en **Confirmar cambio**.</span><span class="sxs-lookup"><span data-stu-id="eaaff-195">toosee hello whole pipeline in action, edit hello *index.js* file in your forked GitHub repo again and click **Commit change**.</span></span> <span data-ttu-id="eaaff-196">Un nuevo trabajo se inicia en Jenkins según hello webhook para GitHub.</span><span class="sxs-lookup"><span data-stu-id="eaaff-196">A new job starts in Jenkins based on hello webhook for GitHub.</span></span> <span data-ttu-id="eaaff-197">Se tarda unos segundos en imagen de Docker de toocreate hello e iniciar la aplicación en un nuevo contenedor.</span><span class="sxs-lookup"><span data-stu-id="eaaff-197">It takes a few seconds toocreate hello Docker image and start your app in a new container.</span></span>

<span data-ttu-id="eaaff-198">Si es necesario, volver a obtener la dirección IP pública de saludo de la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="eaaff-198">If needed, obtain hello public IP address of your VM again:</span></span>

```azurecli-interactive 
az vm show --resource-group myResourceGroupJenkins --name myVM -d --query [publicIps] --o tsv
```

<span data-ttu-id="eaaff-199">Abra un explorador web y escriba `http://<publicIps>:1337`.</span><span class="sxs-lookup"><span data-stu-id="eaaff-199">Open a web browser and enter `http://<publicIps>:1337`.</span></span> <span data-ttu-id="eaaff-200">La aplicación Node.js se muestra y refleja confirmaciones más recientes de hello en la bifurcación GitHub como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="eaaff-200">Your Node.js app is displayed and reflects hello latest commits in your GitHub fork as follows:</span></span>

![Ejecución de la aplicación Node.js](media/tutorial-jenkins-github-docker-cicd/running_nodejs_app.png)

<span data-ttu-id="eaaff-202">Ahora, realizar otro toohello editar *index.js* archivo en GitHub y Confirmar cambio de Hola.</span><span class="sxs-lookup"><span data-stu-id="eaaff-202">Now make another edit toohello *index.js* file in GitHub and commit hello change.</span></span> <span data-ttu-id="eaaff-203">Espere unos segundos para toocomplete de trabajo de hello en Jenkins, a continuación, actualizar la versión de Hola actualizado de toosee de explorador web de la aplicación que se ejecuta en un nuevo contenedor, como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="eaaff-203">Wait a few seconds for hello job toocomplete in Jenkins, then refresh your web browser toosee hello updated version of your app running in a new container as follows:</span></span>

![Aplicación de Node.js en ejecución después de otra confirmación de GitHub](media/tutorial-jenkins-github-docker-cicd/another_running_nodejs_app.png)


## <a name="next-steps"></a><span data-ttu-id="eaaff-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="eaaff-205">Next steps</span></span>
<span data-ttu-id="eaaff-206">En este tutorial, configurado GitHub toorun un trabajo de compilación Jenkins en cada confirmación de código y, a continuación, implementar un tootest del contenedor de Docker de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="eaaff-206">In this tutorial, you configured GitHub toorun a Jenkins build job on each code commit and then deploy a Docker container tootest your app.</span></span> <span data-ttu-id="eaaff-207">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="eaaff-207">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eaaff-208">Crear una máquina virtual de Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-208">Create a Jenkins VM</span></span>
> * <span data-ttu-id="eaaff-209">Instalar y configurar Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-209">Install and configure Jenkins</span></span>
> * <span data-ttu-id="eaaff-210">Crear la integración de webhook entre GitHub y Jenkins</span><span class="sxs-lookup"><span data-stu-id="eaaff-210">Create webhook integration between GitHub and Jenkins</span></span>
> * <span data-ttu-id="eaaff-211">Crear y desencadenar trabajos de compilación de Jenkins desde confirmaciones de GitHub</span><span class="sxs-lookup"><span data-stu-id="eaaff-211">Create and trigger Jenkins build jobs from GitHub commits</span></span>
> * <span data-ttu-id="eaaff-212">Crear una imagen de Docker para la aplicación</span><span class="sxs-lookup"><span data-stu-id="eaaff-212">Create a Docker image for your app</span></span>
> * <span data-ttu-id="eaaff-213">Comprobar que GitHub confirma la imagen de Docker de nueva compilación y actualiza la aplicación en ejecución</span><span class="sxs-lookup"><span data-stu-id="eaaff-213">Verify GitHub commits build new Docker image and updates running app</span></span>

<span data-ttu-id="eaaff-214">Avanzar toohello siguiente tutorial toolearn más información acerca de cómo toointegrate Jenkins con Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="eaaff-214">Advance toohello next tutorial toolearn more about how toointegrate Jenkins with Visual Studio Team Services.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eaaff-215">Implementación de aplicaciones con Jenkins y Team Services</span><span class="sxs-lookup"><span data-stu-id="eaaff-215">Deploy apps with Jenkins and Team Services</span></span>](tutorial-build-deploy-jenkins.md)