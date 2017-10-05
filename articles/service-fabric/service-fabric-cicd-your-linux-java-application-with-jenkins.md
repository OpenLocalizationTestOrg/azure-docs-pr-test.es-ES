---
title: "Compilación e integración continua de la aplicación de Java para Linux de Azure Service Fabric mediante Jenkins | Microsoft Docs"
description: "Compilación e integración continua de la aplicación de Java para Linux de Azure Service Fabric mediante Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: d9372407540d903acca5b1639a2d9ceb0bf3c571
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="use-jenkins-to-build-and-deploy-your-linux-java-application"></a><span data-ttu-id="fdc73-103">Uso de Jenkins para compilar e implementar una aplicación de Java para Linux</span><span class="sxs-lookup"><span data-stu-id="fdc73-103">Use Jenkins to build and deploy your Linux Java application</span></span>
<span data-ttu-id="fdc73-104">Jenkins es una herramienta popular para la integración e implementación continuas de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fdc73-104">Jenkins is a popular tool for continuous integration and deployment of your apps.</span></span> <span data-ttu-id="fdc73-105">Así es como se compila e implementa una aplicación de Azure Service Fabric mediante Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-105">Here's how to build and deploy your Azure Service Fabric application by using Jenkins.</span></span>

## <a name="general-prerequisites"></a><span data-ttu-id="fdc73-106">Requisitos previos generales</span><span class="sxs-lookup"><span data-stu-id="fdc73-106">General prerequisites</span></span>
- <span data-ttu-id="fdc73-107">Git debe estar instalado localmente.</span><span class="sxs-lookup"><span data-stu-id="fdc73-107">Have Git installed locally.</span></span> <span data-ttu-id="fdc73-108">La versión adecuada de Git se puede instalar desde [la página de descargas de la Git](https://git-scm.com/downloads), en función de su sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fdc73-108">You can install the appropriate Git version from [the Git downloads page](https://git-scm.com/downloads), based on your operating system.</span></span> <span data-ttu-id="fdc73-109">Si no conoce Git, encontrará más información al respecto en la [documentación de Git](https://git-scm.com/docs).</span><span class="sxs-lookup"><span data-stu-id="fdc73-109">If you are new to Git, learn more about it from the [Git documentation](https://git-scm.com/docs).</span></span>
- <span data-ttu-id="fdc73-110">Tener a mano el complemento de Jenkins para Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fdc73-110">Have the Service Fabric Jenkins plug-in handy.</span></span> <span data-ttu-id="fdc73-111">Puede descargarlo de las [descargas de Service Fabric](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span><span class="sxs-lookup"><span data-stu-id="fdc73-111">You can download it from [Service Fabric downloads](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).</span></span>

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a><span data-ttu-id="fdc73-112">Configuración de Jenkins en un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fdc73-112">Set up Jenkins inside a Service Fabric cluster</span></span>

<span data-ttu-id="fdc73-113">Jenkins se puede configurar dentro o fuera de un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fdc73-113">You can set up Jenkins either inside or outside a Service Fabric cluster.</span></span> <span data-ttu-id="fdc73-114">En las secciones siguientes se muestra cómo configurarlo dentro de un clúster mientras se usa una cuenta de Azure Storage para guardar el estado de la instancia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="fdc73-114">The following sections show how to set it up inside a cluster while using an Azure storage account to save the state of the container instance.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fdc73-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fdc73-115">Prerequisites</span></span>
1. <span data-ttu-id="fdc73-116">Tenga preparado un clúster Linux de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fdc73-116">Have a Service Fabric Linux cluster ready.</span></span> <span data-ttu-id="fdc73-117">En los clústeres de Service Fabric creados desde Azure Portal ya está Docker instalado.</span><span class="sxs-lookup"><span data-stu-id="fdc73-117">A Service Fabric cluster created from the Azure portal already has Docker installed.</span></span> <span data-ttu-id="fdc73-118">Si el clúster se ejecuta localmente, para comprobar si Docker está instalado, use el comando ``docker info``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-118">If you are running the cluster locally, check if Docker is installed by using the command ``docker info``.</span></span> <span data-ttu-id="fdc73-119">Si no está instalado, instálelo con los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="fdc73-119">If it is not installed, install it accordingly by using the following commands:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. <span data-ttu-id="fdc73-120">Implemente la aplicación de contenedor de Service Fabric en el clúster, para lo que debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fdc73-120">Have the Service Fabric container application deployed on the cluster, by using the following steps:</span></span>

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. <span data-ttu-id="fdc73-121">Necesita los detalles de la opción de conexión del recurso compartido de archivos de Azure Storage donde quiere guardar el estado de la instancia del contenedor Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-121">You need the connect option details of the Azure storage file-share, where you want to persist the state of the Jenkins container instance.</span></span> <span data-ttu-id="fdc73-122">Si está usando Microsoft Azure Portal para lo mismo, siga los pasos de Crear una cuenta de almacenamiento de Azure, por ejemplo ``sfjenkinsstorage1``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-122">If you are using the Microsoft Azure portal for the same, please follow the steps - Create an Azure storage account, say ``sfjenkinsstorage1``.</span></span> <span data-ttu-id="fdc73-123">Cree un **recurso compartido de archivos** en esa cuenta de almacenamiento, por ejemplo ``sfjenkins``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-123">Create a **File Share** under that storage account, say ``sfjenkins``.</span></span> <span data-ttu-id="fdc73-124">Haga clic en **Conectar** para el recurso compartido de archivos y anote los valores que se muestran bajo **Conectando desde Linux**, que por ejemplo tendría el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="fdc73-124">Click on **Connect** for the file-share and note the values it displays under **Connecting from Linux**, say this would look like as follows -</span></span>
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. <span data-ttu-id="fdc73-125">Actualice los valores de marcador de posición en el script ```setupentrypoint.sh``` con los detalles de almacenamiento de Azure correspondientes.</span><span class="sxs-lookup"><span data-stu-id="fdc73-125">Update the placeholder values in the ```setupentrypoint.sh``` script with corresponding azure-storage details.</span></span>
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
<span data-ttu-id="fdc73-126">Reemplace ``[REMOTE_FILE_SHARE_LOCATION]`` con el valor ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` de la salida de la conexión en el punto 3 anterior.</span><span class="sxs-lookup"><span data-stu-id="fdc73-126">Replace ``[REMOTE_FILE_SHARE_LOCATION]`` with the value ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` from the output of the connect in point 3 above.</span></span>
<span data-ttu-id="fdc73-127">Reemplace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` con el valor ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` del punto 3 anterior.</span><span class="sxs-lookup"><span data-stu-id="fdc73-127">Replace ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` with the value ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` from point 3 above.</span></span>

5. <span data-ttu-id="fdc73-128">Conéctese al clúster e instale la aplicación contenedora.</span><span class="sxs-lookup"><span data-stu-id="fdc73-128">Connect to the cluster and install the container application.</span></span>
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
<span data-ttu-id="fdc73-129">Así se instala un contenedor de Jenkins en el clúster y se puede supervisar mediante Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="fdc73-129">This installs a Jenkins container on the cluster, and can be monitored by using the Service Fabric Explorer.</span></span>

### <a name="steps"></a><span data-ttu-id="fdc73-130">Pasos</span><span class="sxs-lookup"><span data-stu-id="fdc73-130">Steps</span></span>
1. <span data-ttu-id="fdc73-131">En el explorador, vaya a ``http://PublicIPorFQDN:8081``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-131">From your browser, go to ``http://PublicIPorFQDN:8081``.</span></span> <span data-ttu-id="fdc73-132">Se proporciona la ruta de acceso de la contraseña de administrador inicial necesaria para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="fdc73-132">It provides the path of the initial admin password required to sign in.</span></span> <span data-ttu-id="fdc73-133">Puede seguir usando Jenkins como usuario administrador.</span><span class="sxs-lookup"><span data-stu-id="fdc73-133">You can continue to use Jenkins as an admin user.</span></span> <span data-ttu-id="fdc73-134">O bien puede crear y cambiar el usuario una vez que inicie sesión con la cuenta de administrador inicial.</span><span class="sxs-lookup"><span data-stu-id="fdc73-134">Or you can create and change the user, after you sign in with the initial admin account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fdc73-135">Asegúrese de que el puerto 8081 se especifica como puerto de punto de conexión de la aplicación al crear el clúster.</span><span class="sxs-lookup"><span data-stu-id="fdc73-135">Ensure that the 8081 port is specified as the application endpoint port while you are creating the cluster.</span></span>
   >

2. <span data-ttu-id="fdc73-136">Obtenga el identificador de la instancia del contenedor mediante ``docker ps -a``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-136">Get the container instance ID by using ``docker ps -a``.</span></span>
3. <span data-ttu-id="fdc73-137">Inicie una sesión de Secure Shell (SSH) en el contenedor y pegue la ruta de acceso que se mostró en el portal de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-137">Secure Shell (SSH) sign in to the container, and paste the path you were shown on the Jenkins portal.</span></span> <span data-ttu-id="fdc73-138">Por ejemplo, si en el portal se muestra la ruta `PATH_TO_INITIAL_ADMIN_PASSWORD`, ejecute la siguiente línea:</span><span class="sxs-lookup"><span data-stu-id="fdc73-138">For example, if in the portal it shows the path `PATH_TO_INITIAL_ADMIN_PASSWORD`, run the following:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. <span data-ttu-id="fdc73-139">Configure GitHub para que funcione con Jenkins, para lo que debe seguir los pasos que se indican en [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (Generación de una clave SSH nueva y su adición al agente de SSH).</span><span class="sxs-lookup"><span data-stu-id="fdc73-139">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
    * <span data-ttu-id="fdc73-140">Use las instrucciones que proporciona GitHub para generar la clave SSH y agregar la clave SSH a la cuenta de GitHub que hospeda el repositorio.</span><span class="sxs-lookup"><span data-stu-id="fdc73-140">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting your repository.</span></span>
    * <span data-ttu-id="fdc73-141">Ejecute los comandos que se mencionan en el vínculo anterior en el shell de Docker para Jenkins (no en el host).</span><span class="sxs-lookup"><span data-stu-id="fdc73-141">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
    * <span data-ttu-id="fdc73-142">Para iniciar sesión en el shell de Jenkins desde un host, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="fdc73-142">To sign in to the Jenkins shell from your host, use the following command:</span></span>

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a><span data-ttu-id="fdc73-143">Configuración de Jenkins fuera de un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fdc73-143">Set up Jenkins outside a Service Fabric cluster</span></span>

<span data-ttu-id="fdc73-144">Jenkins se puede configurar dentro o fuera de un clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fdc73-144">You can set up Jenkins either inside or outside of a Service Fabric cluster.</span></span> <span data-ttu-id="fdc73-145">En las secciones siguientes se muestra cómo se configura fuera de un clúster.</span><span class="sxs-lookup"><span data-stu-id="fdc73-145">The following sections show how to set it up outside a cluster.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fdc73-146">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fdc73-146">Prerequisites</span></span>
<span data-ttu-id="fdc73-147">Debe tener instalado Docker.</span><span class="sxs-lookup"><span data-stu-id="fdc73-147">You need to have Docker installed.</span></span> <span data-ttu-id="fdc73-148">Los siguientes comandos se pueden usar para instalar Docker desde el terminal:</span><span class="sxs-lookup"><span data-stu-id="fdc73-148">The following commands can be used to install Docker from the terminal:</span></span>

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

<span data-ttu-id="fdc73-149">Ahora, cuando ejecute ``docker info`` en el terminal, verá en la salida que el servicio Docker se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="fdc73-149">Now when you run ``docker info`` in the terminal, you should see in the output that the Docker service is running.</span></span>

### <a name="steps"></a><span data-ttu-id="fdc73-150">Pasos</span><span class="sxs-lookup"><span data-stu-id="fdc73-150">Steps</span></span>
  1. <span data-ttu-id="fdc73-151">Extraiga la imagen del contenedor de Jenkins de Service Fabric: ``docker pull raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="fdc73-151">Pull the Service Fabric Jenkins container image: ``docker pull raunakpandya/jenkins:v1``</span></span>
  2. <span data-ttu-id="fdc73-152">Ejecute la imagen del contenedor: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span><span class="sxs-lookup"><span data-stu-id="fdc73-152">Run the container image: ``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``</span></span>
  3. <span data-ttu-id="fdc73-153">Obtenga el identificador de la instancia de la imagen de contenedor.</span><span class="sxs-lookup"><span data-stu-id="fdc73-153">Get the ID of the container image instance.</span></span> <span data-ttu-id="fdc73-154">Puede enumerar todos los contenedores de Docker con el comando ``docker ps –a``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-154">You can list all the Docker containers with the command ``docker ps –a``</span></span>
  4. <span data-ttu-id="fdc73-155">Inicie sesión en el portal de Jenkins, para lo que debe seguir estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fdc73-155">Sign in to the Jenkins portal by using the following steps:</span></span>

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    <span data-ttu-id="fdc73-156">Si el identificador del contenedor es 2d24a73b5964, use 2d24.</span><span class="sxs-lookup"><span data-stu-id="fdc73-156">If container ID is 2d24a73b5964, use 2d24.</span></span>
    * <span data-ttu-id="fdc73-157">Esta contraseña es necesaria para iniciar sesión en el panel de Jenkins desde el portal, que es ``http://<HOST-IP>:8080``</span><span class="sxs-lookup"><span data-stu-id="fdc73-157">This password is required for signing in to the Jenkins dashboard from portal, which is ``http://<HOST-IP>:8080``</span></span>
    * <span data-ttu-id="fdc73-158">La primera vez que inicie sesión puede crear su propia cuenta de usuario y usarla en el futuro, o bien puede seguir usando la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="fdc73-158">After you sign in for the first time, you can create your own user account and use that for future purposes, or you can continue to use the administrator account.</span></span> <span data-ttu-id="fdc73-159">Después de que cree un usuario, debe continuar con él.</span><span class="sxs-lookup"><span data-stu-id="fdc73-159">After you create a user, you need to continue with that.</span></span>
  5. <span data-ttu-id="fdc73-160">Configure GitHub para que funcione con Jenkins, para lo que debe seguir los pasos que se indican en [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/) (Generación de una clave SSH nueva y su adición al agente de SSH).</span><span class="sxs-lookup"><span data-stu-id="fdc73-160">Set up GitHub to work with Jenkins, by using the steps mentioned in [Generating a new SSH key and adding it to the SSH agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).</span></span>
        * <span data-ttu-id="fdc73-161">Use las instrucciones que proporciona GitHub para generar la clave SSH y agregar la clave SSH a la cuenta de GitHub que hospeda el repositorio.</span><span class="sxs-lookup"><span data-stu-id="fdc73-161">Use the instructions provided by GitHub to generate the SSH key, and to add the SSH key to the GitHub account that is hosting the repository.</span></span>
        * <span data-ttu-id="fdc73-162">Ejecute los comandos que se mencionan en el vínculo anterior en el shell de Docker para Jenkins (no en el host).</span><span class="sxs-lookup"><span data-stu-id="fdc73-162">Run the commands mentioned in the preceding link in the Jenkins Docker shell (and not on your host).</span></span>
      * <span data-ttu-id="fdc73-163">Para iniciar sesión en el shell de Jenkins desde un host, use los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="fdc73-163">To sign in to the Jenkins shell from your host, use the following commands:</span></span>

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

<span data-ttu-id="fdc73-164">Asegúrese de que el clúster o el equipo donde se hospeda la imagen del contenedor de Jenkins o tienen una dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="fdc73-164">Ensure that the cluster or machine where the Jenkins container image is hosted has a public-facing IP.</span></span> <span data-ttu-id="fdc73-165">Esto permite a la instancia de Jenkins recibir notificaciones de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdc73-165">This enables the Jenkins instance to receive notifications from GitHub.</span></span>

## <a name="install-the-service-fabric-jenkins-plug-in-from-the-portal"></a><span data-ttu-id="fdc73-166">Instalación del complemento de Jenkins para Service Fabric desde el portal</span><span class="sxs-lookup"><span data-stu-id="fdc73-166">Install the Service Fabric Jenkins plug-in from the portal</span></span>

1. <span data-ttu-id="fdc73-167">Vaya a ``http://PublicIPorFQDN:8081``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-167">Go to ``http://PublicIPorFQDN:8081``</span></span>
2. <span data-ttu-id="fdc73-168">En el panel de Jenkins, seleccione **Manage Jenkins** >  (Administrar Jenkins) **Manage Plugins** >  (Administrar complementos) **Advanced** (Configuración avanzada).</span><span class="sxs-lookup"><span data-stu-id="fdc73-168">From the Jenkins dashboard, select **Manage Jenkins** > **Manage Plugins** > **Advanced**.</span></span>
<span data-ttu-id="fdc73-169">Aquí puede cargar un complemento.</span><span class="sxs-lookup"><span data-stu-id="fdc73-169">Here, you can upload a plug-in.</span></span> <span data-ttu-id="fdc73-170">Seleccione **Choose file** (Elegir archivo) y luego seleccione el archivo **serviceFabric.hpi**, que descargó en los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="fdc73-170">Select **Choose file**, and then select the **serviceFabric.hpi** file, which you downloaded under prerequisites.</span></span> <span data-ttu-id="fdc73-171">Al seleccionar **Upload** (Cargar), Jenkins instala automáticamente el complemento.</span><span class="sxs-lookup"><span data-stu-id="fdc73-171">When you select **Upload**, Jenkins automatically installs the plug-in.</span></span> <span data-ttu-id="fdc73-172">Permita un reinicio si se solicita.</span><span class="sxs-lookup"><span data-stu-id="fdc73-172">Allow a restart if requested.</span></span>

## <a name="create-and-configure-a-jenkins-job"></a><span data-ttu-id="fdc73-173">Creación y configuración de trabajos de Jenkins</span><span class="sxs-lookup"><span data-stu-id="fdc73-173">Create and configure a Jenkins job</span></span>

1. <span data-ttu-id="fdc73-174">Cree un **nuevo elemento** desde el panel.</span><span class="sxs-lookup"><span data-stu-id="fdc73-174">Create a **new item** from dashboard.</span></span>
2. <span data-ttu-id="fdc73-175">Escriba un nombre para dicho elemento (por ejemplo, **MyJob**).</span><span class="sxs-lookup"><span data-stu-id="fdc73-175">Enter an item name (for example, **MyJob**).</span></span> <span data-ttu-id="fdc73-176">Seleccione **free-style project** (proyecto de estilo libre) y haga clic en **OK** (Aceptar).</span><span class="sxs-lookup"><span data-stu-id="fdc73-176">Select **free-style project**, and click **OK**.</span></span>
3. <span data-ttu-id="fdc73-177">Vaya a la página del trabajo y haga clic en **Configure** (Configurar).</span><span class="sxs-lookup"><span data-stu-id="fdc73-177">Go the job page, and click **Configure**.</span></span>

   <span data-ttu-id="fdc73-178">a.</span><span class="sxs-lookup"><span data-stu-id="fdc73-178">a.</span></span> <span data-ttu-id="fdc73-179">En la sección general, en **GitHub project** (proyecto de GitHub), especifique la dirección URL del proyecto de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdc73-179">In the general section, under **GitHub project**, specify your GitHub project URL.</span></span> <span data-ttu-id="fdc73-180">Dicha URL hospeda la aplicación de Java para Service Fabric que desea integrar con el flujo de integración continua e implementación continua (CI/CD) de Jenkins (por ejemplo, ``https://github.com/sayantancs/SFJenkins``).</span><span class="sxs-lookup"><span data-stu-id="fdc73-180">This URL hosts the Service Fabric Java application that you want to integrate with the Jenkins continuous integration, continuous deployment (CI/CD) flow (for example, ``https://github.com/sayantancs/SFJenkins``).</span></span>

   <span data-ttu-id="fdc73-181">b.</span><span class="sxs-lookup"><span data-stu-id="fdc73-181">b.</span></span> <span data-ttu-id="fdc73-182">En la sección **Source Code Management** (Administración del código fuente), seleccione **Git**.</span><span class="sxs-lookup"><span data-stu-id="fdc73-182">Under the **Source Code Management** section, select **Git**.</span></span> <span data-ttu-id="fdc73-183">Especifique la dirección URL del repositorio que hospeda la aplicación de Java para Service Fabric que desea integrar con el flujo de CI/CD de Jenkins (por ejemplo, ``https://github.com/sayantancs/SFJenkins.git``).</span><span class="sxs-lookup"><span data-stu-id="fdc73-183">Specify the repository URL that hosts the Service Fabric Java application that you want to integrate with the Jenkins CI/CD flow (for example, ``https://github.com/sayantancs/SFJenkins.git``).</span></span> <span data-ttu-id="fdc73-184">También puede especificar la rama que se va a compilar (por ejemplo, **/master**).</span><span class="sxs-lookup"><span data-stu-id="fdc73-184">Also, you can specify here which branch to build (for example, **/master**).</span></span>
4. <span data-ttu-id="fdc73-185">Configure su instancia de *GitHub* (la que hospeda el repositorio) para que pueda comunicarse con Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-185">Configure your *GitHub* (which is hosting the repository) so that it is able to talk to Jenkins.</span></span> <span data-ttu-id="fdc73-186">Para ello, siga los pasos que se describen a continuación:</span><span class="sxs-lookup"><span data-stu-id="fdc73-186">Use the following steps:</span></span>

   <span data-ttu-id="fdc73-187">a.</span><span class="sxs-lookup"><span data-stu-id="fdc73-187">a.</span></span> <span data-ttu-id="fdc73-188">Vaya a la página del repositorio de GitHub.</span><span class="sxs-lookup"><span data-stu-id="fdc73-188">Go to your GitHub repository page.</span></span> <span data-ttu-id="fdc73-189">Vaya a **Settings** >  (Configuración) **Integrations and Services** (Integraciones y servicios).</span><span class="sxs-lookup"><span data-stu-id="fdc73-189">Go to **Settings** > **Integrations and Services**.</span></span>

   <span data-ttu-id="fdc73-190">b.</span><span class="sxs-lookup"><span data-stu-id="fdc73-190">b.</span></span> <span data-ttu-id="fdc73-191">Seleccione **Add Service** (Agregar servicio), escriba **Jenkins** y seleccione el **complemento Jenkins-GitHub**.</span><span class="sxs-lookup"><span data-stu-id="fdc73-191">Select **Add Service**, type **Jenkins**, and select the **Jenkins-GitHub plugin**.</span></span>

   <span data-ttu-id="fdc73-192">c.</span><span class="sxs-lookup"><span data-stu-id="fdc73-192">c.</span></span> <span data-ttu-id="fdc73-193">Escriba la dirección URL del webhook de Jenkins (de forma predeterminada, será ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span><span class="sxs-lookup"><span data-stu-id="fdc73-193">Enter your Jenkins webhook URL (by default, it should be ``http://<PublicIPorFQDN>:8081/github-webhook/``).</span></span> <span data-ttu-id="fdc73-194">Haga clic en **Add/Update Service** (Agregar o actualizar servicio).</span><span class="sxs-lookup"><span data-stu-id="fdc73-194">Click **add/update service**.</span></span>

   <span data-ttu-id="fdc73-195">d.</span><span class="sxs-lookup"><span data-stu-id="fdc73-195">d.</span></span> <span data-ttu-id="fdc73-196">Se enviará un evento de prueba a la instancia de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-196">A test event is sent to your Jenkins instance.</span></span> <span data-ttu-id="fdc73-197">Debería ver una marca de verificación verde junto al webhook en GitHub y el proyecto se compilará.</span><span class="sxs-lookup"><span data-stu-id="fdc73-197">You should see a green check by the webhook in GitHub, and your project will build.</span></span>

   <span data-ttu-id="fdc73-198">e.</span><span class="sxs-lookup"><span data-stu-id="fdc73-198">e.</span></span> <span data-ttu-id="fdc73-199">En la sección **Build Triggers** (Compilar desencadenadores), seleccione la opción de compilación que desea.</span><span class="sxs-lookup"><span data-stu-id="fdc73-199">Under the **Build Triggers** section, select which build option you want.</span></span> <span data-ttu-id="fdc73-200">Para este ejemplo, desea desencadenar una compilación cada vez que se produzca alguna inserción en el repositorio.</span><span class="sxs-lookup"><span data-stu-id="fdc73-200">For this example, you want to trigger a build whenever some push to the repository happens.</span></span> <span data-ttu-id="fdc73-201">Por tanto, selecciona **GitHub hook trigger for GITScm polling** (Desencadenador de enlace de GitHub para el sondeo de GITScm).</span><span class="sxs-lookup"><span data-stu-id="fdc73-201">So you select **GitHub hook trigger for GITScm polling**.</span></span> <span data-ttu-id="fdc73-202">[antes, esta opción se denominaba **Build when a change is pushed to GitHub** (Compilar cuando se inserta un cambio en GitHub)].</span><span class="sxs-lookup"><span data-stu-id="fdc73-202">(Previously, this option was called **Build when a change is pushed to GitHub**.)</span></span>

   <span data-ttu-id="fdc73-203">f.</span><span class="sxs-lookup"><span data-stu-id="fdc73-203">f.</span></span> <span data-ttu-id="fdc73-204">En la **sección de compilación**, en la lista desplegable **Add build step** (Agregar paso de compilación), seleccione la opción **Invoke Gradle Script** (Invocar script de Gradle).</span><span class="sxs-lookup"><span data-stu-id="fdc73-204">Under the **Build section**, from the drop-down **Add build step**, select the option **Invoke Gradle Script**.</span></span> <span data-ttu-id="fdc73-205">En el widget que aparece, especifique la ruta de acceso a **Root build script** (Script de compilación raíz) para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fdc73-205">In the widget that comes, specify the path to **Root build script** for your application.</span></span> <span data-ttu-id="fdc73-206">Toma el archivo build.gradle de la ruta de acceso especificada y funciona en consecuencia.</span><span class="sxs-lookup"><span data-stu-id="fdc73-206">It picks up build.gradle from the path specified, and works accordingly.</span></span> <span data-ttu-id="fdc73-207">Si crea un proyecto llamado ``MyActor`` (mediante el complemento de Eclipse o el generador de Yeoman), el script de compilación raíz debe contener ``${WORKSPACE}/MyActor``.</span><span class="sxs-lookup"><span data-stu-id="fdc73-207">If you create a project named ``MyActor`` (using the Eclipse plug-in or Yeoman generator), the root build script should contain ``${WORKSPACE}/MyActor``.</span></span> <span data-ttu-id="fdc73-208">La siguiente captura de pantalla es un ejemplo de su aspecto:</span><span class="sxs-lookup"><span data-stu-id="fdc73-208">See the following screenshot for an example of what this looks like:</span></span>

    ![Acción de compilación de Jenkins en Service Fabric][build-step]

   <span data-ttu-id="fdc73-210">g.</span><span class="sxs-lookup"><span data-stu-id="fdc73-210">g.</span></span> <span data-ttu-id="fdc73-211">En la lista desplegable **Post-Build Actions** (Acciones posteriores a la compilación), seleccione **Deploy Service Fabric Project** (Implementar proyecto de Service Fabric).</span><span class="sxs-lookup"><span data-stu-id="fdc73-211">From the **Post-Build Actions** drop-down, select **Deploy Service Fabric Project**.</span></span> <span data-ttu-id="fdc73-212">Aquí es preciso proporcionar los detalles del clúster donde se implementará la aplicación de Service Fabric compilada por Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-212">Here you need to provide cluster details where the Jenkins compiled Service Fabric application would be deployed.</span></span> <span data-ttu-id="fdc73-213">También se puede especificar más detalles de la aplicación usados para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="fdc73-213">You can also provide additional application details used to deploy the application.</span></span> <span data-ttu-id="fdc73-214">La siguiente captura de pantalla es un ejemplo de su aspecto:</span><span class="sxs-lookup"><span data-stu-id="fdc73-214">See the following screenshot for an example of what this looks like:</span></span>

    ![Acción de compilación de Jenkins en Service Fabric][post-build-step]

   > [!NOTE]
   > <span data-ttu-id="fdc73-216">Este clúster puede ser el mismo que el que hospeda la aplicación del contenedor de Jenkins, en caso de que se vaya a usar Service Fabric para implementar la imagen del contenedor de Jenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-216">The cluster here could be same as the one hosting the Jenkins container application, in case you are using Service Fabric to deploy the Jenkins container image.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="fdc73-217">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fdc73-217">Next steps</span></span>
<span data-ttu-id="fdc73-218">GitHub y Jenkins ya están configurados.</span><span class="sxs-lookup"><span data-stu-id="fdc73-218">GitHub and Jenkins are now configured.</span></span> <span data-ttu-id="fdc73-219">Considere la posibilidad de realizar algún cambio ejemplo de cambio en el proyecto ``MyActor`` del ejemplo de repositorio, https://github.com/sayantancs/SFJenkins.</span><span class="sxs-lookup"><span data-stu-id="fdc73-219">Consider making some sample change in your ``MyActor`` project in the repository example, https://github.com/sayantancs/SFJenkins.</span></span> <span data-ttu-id="fdc73-220">Inserte los cambios en una rama ``master`` remota (o en cualquier rama que ha configurado para trabajar con ella).</span><span class="sxs-lookup"><span data-stu-id="fdc73-220">Push your changes to a remote ``master`` branch (or any branch that you have configured to work with).</span></span> <span data-ttu-id="fdc73-221">Esto desencadena el trabajo de Jenkins, ``MyJob``, que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="fdc73-221">This triggers the Jenkins job, ``MyJob``, that you configured.</span></span> <span data-ttu-id="fdc73-222">Captura los cambios de GitHub, los compila e implementa la aplicación en el punto de conexión del clúster que especificó en las acciones posteriores a la compilación.</span><span class="sxs-lookup"><span data-stu-id="fdc73-222">It fetches the changes from GitHub, builds them, and deploys the application to the cluster endpoint you specified in post-build actions.</span></span>  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png