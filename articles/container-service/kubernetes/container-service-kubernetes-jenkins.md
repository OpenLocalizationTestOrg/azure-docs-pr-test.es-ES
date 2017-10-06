---
title: aaaJenkins CI/CD con Kubernetes en el servicio de contenedor de Azure | Documentos de Microsoft
description: "Cómo procesar tooautomate un CD de integración continua con Jenkins toodeploy y actualiza una aplicación en contenedores en Kubernetes en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: Docker, contenedores, Kubernetes, Azure, Jenkins
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a><span data-ttu-id="031c5-104">Integración de Jenkins con Azure Container Service y Kubernetes</span><span class="sxs-lookup"><span data-stu-id="031c5-104">Jenkins integration with Azure Container Service and Kubernetes</span></span> 
<span data-ttu-id="031c5-105">En este tutorial, recorreremos Hola proceso tooset la integración continua de una aplicación de contenedor múltiples en Kubernetes de servicio de contenedor de Azure con la plataforma de Jenkins Hola.</span><span class="sxs-lookup"><span data-stu-id="031c5-105">In this tutorial, we walk through hello process tooset up continuous integration of a multi-container application into Azure Container Service Kubernetes using hello Jenkins platform.</span></span> <span data-ttu-id="031c5-106">flujo de trabajo de Hello imagen de contenedor de hello en Docker Hub de actualizaciones pod de hello Kubernetes mediante una ejecución de la implementación.</span><span class="sxs-lookup"><span data-stu-id="031c5-106">hello workflow updates hello container image in Docker Hub and upgrades hello Kubernetes pods using a deployment rollout.</span></span> 

## <a name="high-level-process"></a><span data-ttu-id="031c5-107">Proceso de alto nivel</span><span class="sxs-lookup"><span data-stu-id="031c5-107">High level process</span></span>
<span data-ttu-id="031c5-108">Hola pasos básicos descritos en este artículo son:</span><span class="sxs-lookup"><span data-stu-id="031c5-108">hello basic steps detailed in this article are:</span></span> 
- <span data-ttu-id="031c5-109">Instalación de un clúster de Kubernetes en Container Service</span><span class="sxs-lookup"><span data-stu-id="031c5-109">Install a Kubernetes cluster in Container Service</span></span>
- <span data-ttu-id="031c5-110">Configurar Jenkins y acceso tooContainer servicio</span><span class="sxs-lookup"><span data-stu-id="031c5-110">Set up Jenkins and configure access tooContainer Service</span></span>
- <span data-ttu-id="031c5-111">Creación de un flujo de trabajo de Jenkins</span><span class="sxs-lookup"><span data-stu-id="031c5-111">Create a Jenkins workflow</span></span>
- <span data-ttu-id="031c5-112">Probar el proceso final tooend de hello CI/CD</span><span class="sxs-lookup"><span data-stu-id="031c5-112">Test hello CI/CD process end tooend</span></span>

## <a name="install-a-kubernetes-cluster"></a><span data-ttu-id="031c5-113">Instalación de un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="031c5-113">Install a Kubernetes cluster</span></span>
    
<span data-ttu-id="031c5-114">Implementar el clúster de Kubernetes de hello en el servicio de contenedor de Azure con hello pasos.</span><span class="sxs-lookup"><span data-stu-id="031c5-114">Deploy hello Kubernetes cluster in Azure Container Service using hello following steps.</span></span> <span data-ttu-id="031c5-115">La documentación completa se encuentra [aquí](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="031c5-115">Full documentation is located [here](container-service-kubernetes-walkthrough.md).</span></span>

### <a name="step-1-create-a-resource-group"></a><span data-ttu-id="031c5-116">Paso 1: Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="031c5-116">Step 1: Create a resource group</span></span>
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a><span data-ttu-id="031c5-117">Paso 2: Implementar el clúster de Hola</span><span class="sxs-lookup"><span data-stu-id="031c5-117">Step 2: Deploy hello cluster</span></span>
> [!NOTE]
> <span data-ttu-id="031c5-118">Hello estos pasos requieren una clave pública local de SSH almacenada en la carpeta de ~/.ssh Hola.</span><span class="sxs-lookup"><span data-stu-id="031c5-118">hello following steps require a local SSH public key stored in hello ~/.ssh folder.</span></span>
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a><span data-ttu-id="031c5-119">Configurar Jenkins y acceso tooContainer servicio</span><span class="sxs-lookup"><span data-stu-id="031c5-119">Set up Jenkins and configure access tooContainer Service</span></span>

### <a name="step-1-install-jenkins"></a><span data-ttu-id="031c5-120">Paso 1: Instalación de Jenkins</span><span class="sxs-lookup"><span data-stu-id="031c5-120">Step 1: Install Jenkins</span></span>
1. <span data-ttu-id="031c5-121">Cree una máquina virtual de Azure con Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="031c5-121">Create an Azure VM with Ubuntu 16.04 LTS.</span></span>  <span data-ttu-id="031c5-122">Puesto que más adelante en hello los pasos se necesita tooconnect toothis VM con bash en el equipo local, la clave pública de conjunto hello 'Tipo de autenticación' too'SSH' y pegar Hola clave pública SSH que se almacena localmente en la carpeta ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="031c5-122">Since later in hello steps you will need tooconnect toothis VM using bash on your local machine, set hello 'Authentication type' too'SSH public key' and paste hello SSH public key that is stored locally in your ~/.ssh folder.</span></span>  <span data-ttu-id="031c5-123">Además, tome nota de hello 'Nombre de usuario' que se especifican como este nombre de usuario estará panel de tooview necesario Hola Jenkins y para la conexión toohello Jenkins VM en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="031c5-123">Also, take note of hello 'User name' that you specify since this user name will be needed tooview hello Jenkins dashboard and for connecting toohello Jenkins VM in later steps.</span></span>
2. <span data-ttu-id="031c5-124">Instale Jenkins mediante estas [instrucciones](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span><span class="sxs-lookup"><span data-stu-id="031c5-124">Install Jenkins via these [instructions](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu).</span></span> <span data-ttu-id="031c5-125">Se puede encontrar un tutorial más detallado en [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span><span class="sxs-lookup"><span data-stu-id="031c5-125">A more detailed tutorial is at [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).</span></span>
3. <span data-ttu-id="031c5-126">tooview Hola Jenkins panel en el equipo local, actualizar el puerto de tooallow 8080 para el grupo de seguridad de red de Azure hello mediante la adición de una regla de entrada que permite acceso tooport 8080.</span><span class="sxs-lookup"><span data-stu-id="031c5-126">tooview hello Jenkins dashboard on your local machine, update hello Azure network security group tooallow port 8080 by adding an inbound rule that allows access tooport 8080.</span></span>  <span data-ttu-id="031c5-127">Además, puede configurar el desvío del puerto mediante la ejecución de este comando: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span><span class="sxs-lookup"><span data-stu-id="031c5-127">Alternatively, you may setup port forwarding by running this command: `ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`</span></span>
4. <span data-ttu-id="031c5-128">Conecte tooyour Jenkins servidor mediante el Explorador de hello desplazándose IP pública de toohello (http:// < your_jenkins_public_ip >: 8080) y desbloquear el panel de Jenkins Hola para hello primera vez con la contraseña de administrador inicial de Hola.</span><span class="sxs-lookup"><span data-stu-id="031c5-128">Connect tooyour Jenkins server using hello browser by navigating toohello public IP (http://<your_jenkins_public_ip>:8080) and unlock hello Jenkins dashboard for hello first time with hello initial admin password.</span></span>  <span data-ttu-id="031c5-129">contraseña de administrador de Hola se almacena en /var/lib/jenkins/secrets/initialAdminPassword en hello Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="031c5-129">hello admin password is stored at /var/lib/jenkins/secrets/initialAdminPassword on hello Jenkins VM.</span></span>  <span data-ttu-id="031c5-130">Un tooget fácilmente esta contraseña es tooSSH en Hola Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="031c5-130">An easy way tooget this password is tooSSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="031c5-131">A continuación, ejecute: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span><span class="sxs-lookup"><span data-stu-id="031c5-131">Next, run: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.</span></span>
5. <span data-ttu-id="031c5-132">Instalación de Docker en la máquina de hello Jenkins a través de estos [instrucciones](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span><span class="sxs-lookup"><span data-stu-id="031c5-132">Install Docker on hello Jenkins machine via these [instructions](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts).</span></span> <span data-ttu-id="031c5-133">Esto permite toobe de comandos de Docker ejecutar trabajos Jenkins.</span><span class="sxs-lookup"><span data-stu-id="031c5-133">This allows for Docker commands toobe run in Jenkins jobs.</span></span>
6. <span data-ttu-id="031c5-134">Configurar Docker permisos tooallow Jenkins tooaccess hello Docker extremo.</span><span class="sxs-lookup"><span data-stu-id="031c5-134">Configure Docker permissions tooallow Jenkins tooaccess hello Docker endpoint.</span></span>

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. <span data-ttu-id="031c5-135">Instale la CLI de `kubectl` en Jenkins.</span><span class="sxs-lookup"><span data-stu-id="031c5-135">Install `kubectl` CLI on Jenkins.</span></span> <span data-ttu-id="031c5-136">Se pueden encontrar más detalles en [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/) (Instalación y configuración de kubectl).</span><span class="sxs-lookup"><span data-stu-id="031c5-136">More details are at [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>  <span data-ttu-id="031c5-137">Trabajos de Jenkins usará 'kubectl' toomanage e implementar toohello Kubernetes clúster.</span><span class="sxs-lookup"><span data-stu-id="031c5-137">Jenkins jobs will use 'kubectl' toomanage and deploy toohello Kubernetes cluster.</span></span>

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a><span data-ttu-id="031c5-138">Paso 2: Configurar el clúster de acceso toohello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="031c5-138">Step 2: Set up access toohello Kubernetes cluster</span></span>

> [!NOTE]
> <span data-ttu-id="031c5-139">Hay varios Hola de tooaccomplishing enfoques pasos.</span><span class="sxs-lookup"><span data-stu-id="031c5-139">There are multiple approaches tooaccomplishing hello following steps.</span></span> <span data-ttu-id="031c5-140">Usar el enfoque de Hola que sea más fácil para usted.</span><span class="sxs-lookup"><span data-stu-id="031c5-140">Use hello approach that is easiest for you.</span></span>
>

1. <span data-ttu-id="031c5-141">Hola copia `kubectl` toohello del archivo de configuración Jenkins automático para que los trabajos Jenkins tengan clúster de acceso toohello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="031c5-141">Copy hello `kubectl` config file toohello Jenkins machine so that Jenkins jobs have access toohello Kubernetes cluster.</span></span> <span data-ttu-id="031c5-142">Estas instrucciones se supone que está usando intensiva de errores desde un equipo diferente de Hola Jenkins VM y que una clave pública de SSH local se almacena en la carpeta de la máquina de hello ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="031c5-142">These instructions assume that you are using bash from a different machine than hello Jenkins VM and that a local SSH public key is stored in hello machine's ~/.ssh folder.</span></span>

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. <span data-ttu-id="031c5-143">Validar from Jenkins ese hello Kubernetes clúster es accesible.</span><span class="sxs-lookup"><span data-stu-id="031c5-143">Validate from Jenkins that hello Kubernetes cluster is accessible.</span></span>  <span data-ttu-id="031c5-144">toodo, SSH en hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span><span class="sxs-lookup"><span data-stu-id="031c5-144">toodo this, SSH into hello Jenkins VM: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.</span></span>  <span data-ttu-id="031c5-145">A continuación, compruebe Jenkins puede conectarse correctamente clúster tooyour: `kubectl cluster-info`.</span><span class="sxs-lookup"><span data-stu-id="031c5-145">Next, verify Jenkins can successfully connect tooyour cluster: `kubectl cluster-info`.</span></span>
    

## <a name="create-a-jenkins-workflow"></a><span data-ttu-id="031c5-146">Creación de un flujo de trabajo de Jenkins</span><span class="sxs-lookup"><span data-stu-id="031c5-146">Create a Jenkins workflow</span></span>

### <a name="prerequisites"></a><span data-ttu-id="031c5-147">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="031c5-147">Prerequisites</span></span>

- <span data-ttu-id="031c5-148">Cuenta de GitHub para el repositorio de código.</span><span class="sxs-lookup"><span data-stu-id="031c5-148">GitHub account for code repo.</span></span>
- <span data-ttu-id="031c5-149">Concentrador cuenta toostore y actualizar imágenes de docker.</span><span class="sxs-lookup"><span data-stu-id="031c5-149">Docker Hub account toostore and update images.</span></span>
- <span data-ttu-id="031c5-150">Aplicación en contenedor que se puede volver a compilar y actualizar.</span><span class="sxs-lookup"><span data-stu-id="031c5-150">Containerized application that can be rebuilt and updated.</span></span> <span data-ttu-id="031c5-151">Puede usar esta aplicación de contenedor de ejemplo escrita en Golang: https://github.com/chzbrgr71/go-web.</span><span class="sxs-lookup"><span data-stu-id="031c5-151">You can use this sample container app written in Golang: https://github.com/chzbrgr71/go-web</span></span> 

> [!NOTE]
> <span data-ttu-id="031c5-152">Hello estos pasos se deben realizar en su propia cuenta de GitHub.</span><span class="sxs-lookup"><span data-stu-id="031c5-152">hello following steps must be performed in your own GitHub account.</span></span> <span data-ttu-id="031c5-153">Cree hello tooclone libre por encima del repositorio, pero debe utilizar sus propio webhooks de hello tooconfigure de cuenta y tener acceso Jenkins.</span><span class="sxs-lookup"><span data-stu-id="031c5-153">Feel free tooclone hello above repo, but you must use your own account tooconfigure hello webhooks and Jenkins access.</span></span>
>

### <a name="step-1-deploy-initial-v1-of-application"></a><span data-ttu-id="031c5-154">Paso 1: Implementación de la v1 inicial de la aplicación</span><span class="sxs-lookup"><span data-stu-id="031c5-154">Step 1: Deploy initial v1 of application</span></span>
1. <span data-ttu-id="031c5-155">Crear aplicación hello de máquina del desarrollador de hello con hello siga los comandos.</span><span class="sxs-lookup"><span data-stu-id="031c5-155">Build hello app from hello developer machine with hello following commands.</span></span> <span data-ttu-id="031c5-156">Reemplace `myrepo` por el suyo propio.</span><span class="sxs-lookup"><span data-stu-id="031c5-156">Replace `myrepo` with your own.</span></span>
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. <span data-ttu-id="031c5-157">Insertar imagen tooDocker concentrador.</span><span class="sxs-lookup"><span data-stu-id="031c5-157">Push image tooDocker Hub.</span></span>

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. <span data-ttu-id="031c5-158">Implementar toohello Kubernetes clúster.</span><span class="sxs-lookup"><span data-stu-id="031c5-158">Deploy toohello Kubernetes cluster.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="031c5-159">Editar hello `go-web.yaml` archivo tooupdate su imagen de contenedor y el repositorio.</span><span class="sxs-lookup"><span data-stu-id="031c5-159">Edit hello `go-web.yaml` file tooupdate your container image and repo.</span></span>
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a><span data-ttu-id="031c5-160">Paso 2: Configuración del sistema Jenkins</span><span class="sxs-lookup"><span data-stu-id="031c5-160">Step 2: Configure Jenkins system</span></span>
1. <span data-ttu-id="031c5-161">Haga clic en **Manage Jenkins** >  (Administrar Jenkins) **Configure System** (Configurar el sistema).</span><span class="sxs-lookup"><span data-stu-id="031c5-161">Click **Manage Jenkins** > **Configure System**.</span></span>
2. <span data-ttu-id="031c5-162">En **GitHub**, seleccione **Add GitHub Server** (Agregar servidor de GitHub).</span><span class="sxs-lookup"><span data-stu-id="031c5-162">Under **GitHub**, select **Add GitHub Server**.</span></span>
3. <span data-ttu-id="031c5-163">Deje **API URL** (Dirección URL de API) como valor predeterminado.</span><span class="sxs-lookup"><span data-stu-id="031c5-163">Leave **API URL** as default.</span></span>
4. <span data-ttu-id="031c5-164">En **Credentials** (Credenciales), agregue una credencial de Jenkins mediante **texto secreto**.</span><span class="sxs-lookup"><span data-stu-id="031c5-164">Under **Credentials**, add a Jenkins credential using **Secret text**.</span></span> <span data-ttu-id="031c5-165">Se recomienda usar tokens de acceso personal de GitHub, que se configuran en la configuración de su cuenta de usuario de GitHub.</span><span class="sxs-lookup"><span data-stu-id="031c5-165">We recommend using GitHub personal access tokens, which are configured in your GitHub user account settings.</span></span> <span data-ttu-id="031c5-166">Puede encontrar más detalles al respecto [aquí.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span><span class="sxs-lookup"><span data-stu-id="031c5-166">More details on this [here.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)</span></span>
5. <span data-ttu-id="031c5-167">Haga clic en **Probar conexión** tooensure esto está configurado correctamente.</span><span class="sxs-lookup"><span data-stu-id="031c5-167">Click **Test connection** tooensure this is configured correctly.</span></span>
6. <span data-ttu-id="031c5-168">En **Global Properties** (Propiedades globales), agregue una variable de entorno `DOCKER_HUB` y proporcione su contraseña de Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="031c5-168">Under **Global Properties**, add an environment variable `DOCKER_HUB` and provide your Docker Hub password.</span></span> <span data-ttu-id="031c5-169">(Esto es útil en esta demostración, pero en un escenario de producción sería necesario un enfoque más seguro).</span><span class="sxs-lookup"><span data-stu-id="031c5-169">(This is useful in this demo, but a production scenario would require a more secure approach.)</span></span>
7. <span data-ttu-id="031c5-170">Haga clic en Save (Guardar).</span><span class="sxs-lookup"><span data-stu-id="031c5-170">Save.</span></span>

![Acceso a GitHub de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a><span data-ttu-id="031c5-172">Paso 3: Crear el flujo de trabajo de hello Jenkins</span><span class="sxs-lookup"><span data-stu-id="031c5-172">Step 3: Create hello Jenkins workflow</span></span>
1. <span data-ttu-id="031c5-173">Cree un elemento de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="031c5-173">Create a Jenkins item.</span></span>
2. <span data-ttu-id="031c5-174">Proporcione un nombre (por ejemplo, "go-web") y seleccione **Freestyle Project** (Proyecto de estilo libre).</span><span class="sxs-lookup"><span data-stu-id="031c5-174">Provide a name (for example, "go-web") and select **Freestyle Project**.</span></span> 
3. <span data-ttu-id="031c5-175">Comprobar **GitHub proyecto** y proporcione el repositorio de GitHub de tooyour de dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="031c5-175">Check **GitHub project** and provide hello URL tooyour GitHub repo.</span></span>
4. <span data-ttu-id="031c5-176">En **administración de código fuente**, proporcione la dirección URL de repositorio de GitHub de Hola y las credenciales.</span><span class="sxs-lookup"><span data-stu-id="031c5-176">In **Source Code Management**, provide hello GitHub repo URL and credentials.</span></span> 
5. <span data-ttu-id="031c5-177">Agregar un **paso de compilación** de tipo **ejecutar shell** y use Hola siguiendo texto:</span><span class="sxs-lookup"><span data-stu-id="031c5-177">Add a **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. <span data-ttu-id="031c5-178">Agregue otro **paso de compilación** de tipo **ejecutar shell** y use Hola siguiendo texto:</span><span class="sxs-lookup"><span data-stu-id="031c5-178">Add another **Build Step** of type **Execute shell** and use hello following text:</span></span>

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Pasos de compilación de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. <span data-ttu-id="031c5-180">Guardar elemento de hello Jenkins y probar con **generar ahora**.</span><span class="sxs-lookup"><span data-stu-id="031c5-180">Save hello Jenkins item and test with **Build Now**.</span></span>

### <a name="step-4-connect-github-webhook"></a><span data-ttu-id="031c5-181">Paso 4: Conexión del webhook de GitHub</span><span class="sxs-lookup"><span data-stu-id="031c5-181">Step 4: Connect GitHub webhook</span></span>
1. <span data-ttu-id="031c5-182">En el elemento de Jenkins Hola que creó, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="031c5-182">In hello Jenkins item you created, click **Configure**.</span></span>
2. <span data-ttu-id="031c5-183">En **Build Triggers** (Compila desencadenadores), seleccione **GitHub hook trigger for GITScm polling** (Desencadenador de enlace de GitHub para sondeo de GITScm) y haga clic en **Save** (Guardar).</span><span class="sxs-lookup"><span data-stu-id="031c5-183">Under **Build Triggers**, select **GitHub hook trigger for GITScm polling** and **Save**.</span></span> <span data-ttu-id="031c5-184">Esto configura automáticamente hello GitHub webhook.</span><span class="sxs-lookup"><span data-stu-id="031c5-184">This automatically configures hello GitHub webhook.</span></span>
3. <span data-ttu-id="031c5-185">En el repositorio de GitHub para go-web, haga clic en **Settings > Webhooks** (Configuración > Webhooks).</span><span class="sxs-lookup"><span data-stu-id="031c5-185">In your GitHub repo for go-web, click **Settings > Webhooks**.</span></span>
4. <span data-ttu-id="031c5-186">Compruebe que hello webhook Jenkins dirección URL se agregó correctamente.</span><span class="sxs-lookup"><span data-stu-id="031c5-186">Verify that hello Jenkins webhook URL was added successfully.</span></span> <span data-ttu-id="031c5-187">dirección URL de Hello debe finalizar en "github webhook".</span><span class="sxs-lookup"><span data-stu-id="031c5-187">hello URL should end in "github-webhook".</span></span>

![Configuración del webhook de Jenkins](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a><span data-ttu-id="031c5-189">Probar el proceso final tooend de hello CI/CD</span><span class="sxs-lookup"><span data-stu-id="031c5-189">Test hello CI/CD process end tooend</span></span>

1. <span data-ttu-id="031c5-190">Actualizar código para el repositorio de Hola e inserción/sincronización con el repositorio de GitHub de Hola.</span><span class="sxs-lookup"><span data-stu-id="031c5-190">Update code for hello repo and push/synch with hello GitHub repository.</span></span>
2. <span data-ttu-id="031c5-191">Desde la consola de Jenkins hello, active hello **generar historial** y validar ese Hola trabajo se ha ejecutado.</span><span class="sxs-lookup"><span data-stu-id="031c5-191">From hello Jenkins console, check hello **Build History** and validate that hello job has run.</span></span> <span data-ttu-id="031c5-192">Ver detalles de toosee de salida de consola.</span><span class="sxs-lookup"><span data-stu-id="031c5-192">View console output toosee details.</span></span>
3. <span data-ttu-id="031c5-193">Desde Kubernetes, ver detalles de hello actualizan implementación:</span><span class="sxs-lookup"><span data-stu-id="031c5-193">From Kubernetes, view details of hello upgraded deployment:</span></span>

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a><span data-ttu-id="031c5-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="031c5-194">Next steps</span></span>

- <span data-ttu-id="031c5-195">Implemente Azure Container Registry y almacene las imágenes en un repositorio seguro.</span><span class="sxs-lookup"><span data-stu-id="031c5-195">Deploy Azure Container Registry and store images in a secure repository.</span></span> <span data-ttu-id="031c5-196">Consulte [Documentación de Azure Container Registry](https://docs.microsoft.com/azure/container-registry).</span><span class="sxs-lookup"><span data-stu-id="031c5-196">See [Azure Container Registry docs](https://docs.microsoft.com/azure/container-registry).</span></span>
- <span data-ttu-id="031c5-197">Cree un flujo de trabajo más complejo que incluya la implementación en paralelo y pruebas automatizadas de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="031c5-197">Build a more complex workflow that includes side-by-side deployment and automated tests in Jenkins.</span></span>
- <span data-ttu-id="031c5-198">Para obtener más información acerca de elementos de configuración/CD con Jenkins y Kubernetes, vea hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span><span class="sxs-lookup"><span data-stu-id="031c5-198">For more information about CI/CD with Jenkins and Kubernetes, see hello [Jenkins blog](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).</span></span>
