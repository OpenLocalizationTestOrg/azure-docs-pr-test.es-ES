---
title: "aaaDeploy una aplicación de arranque del muelle en Kubernetes en el servicio de contenedor de Azure | Documentos de Microsoft"
description: "Este tutorial le guiará aunque Hola pasos toodeploy una aplicación de arranque del muelle en un clúster de Kubernetes en Microsoft Azure."
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="550a0-103">Implementar una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="550a0-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="550a0-104">Hola  **[Spring Framework]**  es un marco de código abierto popular que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web.</span><span class="sxs-lookup"><span data-stu-id="550a0-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="550a0-105">Este tutorial utiliza una aplicación de ejemplo creada con [arranque primavera], un enfoque basado en la convención para el uso de primavera tooget a trabajar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="550a0-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="550a0-106">**[Kubernetes]**  y  **[cliente de Docker]**  son soluciones de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, el ajuste de escala y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="550a0-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="550a0-107">Este tutorial guía aunque combinar estos toodevelop dos tecnologías populares, código abierto e implementar un tooMicrosoft de aplicación de arranque de primavera Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="550a0-108">Más específicamente, use  *[arranque primavera]*  para el desarrollo de aplicaciones,  *[Kubernetes]*  para la implementación de contenedor y Hola [Contenedor Service (ACS) de azure] toohost la aplicación.</span><span class="sxs-lookup"><span data-stu-id="550a0-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="550a0-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="550a0-109">Prerequisites</span></span>

* <span data-ttu-id="550a0-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="550a0-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="550a0-111">Hola [interfaz de línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="550a0-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="550a0-112">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="550a0-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="550a0-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="550a0-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="550a0-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="550a0-114">A [Git] client.</span></span>
* <span data-ttu-id="550a0-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="550a0-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="550a0-116">Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="550a0-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="550a0-117">Crear Hola Spring arranque en la aplicación web de introducción a Docker</span><span class="sxs-lookup"><span data-stu-id="550a0-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="550a0-118">Hola pasos le guían por creando una aplicación web de arranque de primavera y las pruebas de forma local.</span><span class="sxs-lookup"><span data-stu-id="550a0-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="550a0-119">Abra un símbolo y crear un directorio local toohold la aplicación y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="550a0-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="550a0-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="550a0-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="550a0-121">Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="550a0-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="550a0-122">Cambiar directorio toohello completado proyecto.</span><span class="sxs-lookup"><span data-stu-id="550a0-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="550a0-123">Utilice toobuild de Maven y aplicaciones de ejemplo de Hola de ejecución.</span><span class="sxs-lookup"><span data-stu-id="550a0-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="550a0-124">Aplicación de prueba hello web examinando toohttp://localhost:8080 o con siguiente hello `curl` comando:</span><span class="sxs-lookup"><span data-stu-id="550a0-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="550a0-125">Debería ver el siguiente mensaje de Hola: **Docker Hola a todos**</span><span class="sxs-lookup"><span data-stu-id="550a0-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="550a0-127">Crear un registro de contenedor de Azure mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="550a0-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="550a0-128">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="550a0-128">Open a command prompt.</span></span>

1. <span data-ttu-id="550a0-129">Inicie sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="550a0-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="550a0-130">Crear un grupo de recursos para hello recursos de Azure usados en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="550a0-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="550a0-131">Crear un registro de contenedor de Azure privada en el grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="550a0-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="550a0-132">tutorial de Hello inserta la aplicación de ejemplo de Hola como un registro de toothis de imágenes de Docker en pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="550a0-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="550a0-133">Reemplace `wingtiptoysregistry` por un nombre único para el registro.</span><span class="sxs-lookup"><span data-stu-id="550a0-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="550a0-134">Error en el registro de aplicación toohello contenedor de inserción</span><span class="sxs-lookup"><span data-stu-id="550a0-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="550a0-135">Navegue toohello el directorio de configuración para la instalación de Maven (~/.m2/ predeterminado o C:\Users\username\.m2) abierto hello y *settings.xml* archivo con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="550a0-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="550a0-136">Recuperar la contraseña de hello para el registro de contenedor de hello CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="550a0-137">Agregue los tooa del registro de contenedor de Azure de identificador y la contraseña nueva `<server>` colección Hola *settings.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="550a0-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="550a0-138">Hola `id` y `username` son Hola nombre del registro de hello.</span><span class="sxs-lookup"><span data-stu-id="550a0-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="550a0-139">Hola de uso `password` valor del comando anterior de hello (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="550a0-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="550a0-140">Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completa*"), abra hello y *pom.xml* archivo con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="550a0-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="550a0-141">Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="550a0-142">Hola de actualización `<plugins>` colección Hola *pom.xml* de archivos para que Hola `<plugin>` contiene Hola inicio de sesión del registro y la dirección del nombre del servidor para el registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="550a0-143">Navegue toohello completado el directorio del proyecto para la aplicación de arranque de primavera y ejecute hello después comando toobuild hello Docker contenedor e inserte Hola imagen toohello del registro:</span><span class="sxs-lookup"><span data-stu-id="550a0-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="550a0-144">Puede recibir un mensaje de error es tooone similar de siguientes hello cuando Maven inserta Hola imagen tooAzure:</span><span class="sxs-lookup"><span data-stu-id="550a0-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="550a0-145">Si recibe este error, inicie sesión en tooAzure de línea de comandos de Docker Hola.</span><span class="sxs-lookup"><span data-stu-id="550a0-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="550a0-146">Después, inserte el contenedor:</span><span class="sxs-lookup"><span data-stu-id="550a0-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="550a0-147">Cree un Kubernetes clúster en ACS con hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="550a0-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="550a0-148">Cree un clúster de Kubernetes en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="550a0-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="550a0-149">Hello siguiente comando crea un *kubernetes* clúster Hola *wingtiptoys kubernetes* recursos grupo con *wingtiptoys-objeto containerservice* como clúster de Hola nombre, y *wingtiptoys kubernetes* como prefijo DNS de hello:</span><span class="sxs-lookup"><span data-stu-id="550a0-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="550a0-150">Este comando puede tardar un rato toocomplete.</span><span class="sxs-lookup"><span data-stu-id="550a0-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="550a0-151">Instalar `kubectl` utilizando Hola CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="550a0-152">Los usuarios de Linux pueden tener tooprefix este comando con `sudo` desde que se implementa hello Kubernetes CLI demasiado`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="550a0-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="550a0-153">Descargar la información de configuración de clúster de Hola para que pueda administrar el clúster desde la interfaz web de hello Kubernetes y `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="550a0-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="550a0-154">Implementar Hola imagen tooyour Kubernetes clúster</span><span class="sxs-lookup"><span data-stu-id="550a0-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="550a0-155">Este tutorial implementa la aplicación hello con `kubectl`, a continuación, le permiten implementación de hello tooexplore a través de la interfaz web de hello Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="550a0-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="550a0-156">Implementar con la interfaz web de hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="550a0-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="550a0-157">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="550a0-157">Open a command prompt.</span></span>

1. <span data-ttu-id="550a0-158">Abra el sitio Web de configuración de hello para el clúster de Kubernetes en el explorador predeterminado:</span><span class="sxs-lookup"><span data-stu-id="550a0-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="550a0-159">Cuando se abre el sitio Web de configuración de Kubernetes de hello en el explorador, demasiado haga clic en el vínculo de hello**implementar una aplicación en contenedores**:</span><span class="sxs-lookup"><span data-stu-id="550a0-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Sitio web para la configuración de Kubernetes][KB01]

1. <span data-ttu-id="550a0-161">Cuando Hola **implementar una aplicación en contenedores** se muestra la página, especifique Hola siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="550a0-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="550a0-162">a.</span><span class="sxs-lookup"><span data-stu-id="550a0-162">a.</span></span> <span data-ttu-id="550a0-163">Seleccione **Specify app details below** (Especificar detalles de la aplicación a continuación).</span><span class="sxs-lookup"><span data-stu-id="550a0-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="550a0-164">b.</span><span class="sxs-lookup"><span data-stu-id="550a0-164">b.</span></span> <span data-ttu-id="550a0-165">Escriba su nombre de aplicación de arranque de primavera de hello **nombre de la aplicación**; por ejemplo: "*gs-spring-arranque-docker*".</span><span class="sxs-lookup"><span data-stu-id="550a0-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="550a0-166">c.</span><span class="sxs-lookup"><span data-stu-id="550a0-166">c.</span></span> <span data-ttu-id="550a0-167">Escriba la imagen de servidor y un contenedor de inicio de sesión de versiones anteriores de hello **imagen de contenedor**; por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="550a0-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="550a0-168">d.</span><span class="sxs-lookup"><span data-stu-id="550a0-168">d.</span></span> <span data-ttu-id="550a0-169">Elija **externo** para hello **servicio**.</span><span class="sxs-lookup"><span data-stu-id="550a0-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="550a0-170">e.</span><span class="sxs-lookup"><span data-stu-id="550a0-170">e.</span></span> <span data-ttu-id="550a0-171">Especifique los puertos internos y externos en hello **puerto** y **puerto de destino** cuadros de texto.</span><span class="sxs-lookup"><span data-stu-id="550a0-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Sitio web para la configuración de Kubernetes][KB02]


1. <span data-ttu-id="550a0-173">Haga clic en **implementar** contenedor de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="550a0-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Implementar un contenedor][KB05]

1. <span data-ttu-id="550a0-175">Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).</span><span class="sxs-lookup"><span data-stu-id="550a0-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servicios de Kubernetes][KB06]

1. <span data-ttu-id="550a0-177">Si hace clic en el vínculo de Hola para **extremos externos**, puede ver la aplicación de arranque de primavera ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="550a0-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="550a0-180">Implementación con kubectl</span><span class="sxs-lookup"><span data-stu-id="550a0-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="550a0-181">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="550a0-181">Open a command prompt.</span></span>

1. <span data-ttu-id="550a0-182">Ejecutar el contenedor en el clúster de hello Kubernetes mediante hello `kubectl run` comando.</span><span class="sxs-lookup"><span data-stu-id="550a0-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="550a0-183">Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa de Hola.</span><span class="sxs-lookup"><span data-stu-id="550a0-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="550a0-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="550a0-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="550a0-185">En este comando:</span><span class="sxs-lookup"><span data-stu-id="550a0-185">In this command:</span></span>

   * <span data-ttu-id="550a0-186">nombre del contenedor de Hello `gs-spring-boot-docker` especificado inmediatamente después de hello `run` comando</span><span class="sxs-lookup"><span data-stu-id="550a0-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="550a0-187">Hola `--image` parámetro especifica Hola combinados de servidor de inicio de sesión y nombre de la imagen como`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="550a0-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="550a0-188">Exponer el clúster Kubernetes externamente mediante hello `kubectl expose` comando.</span><span class="sxs-lookup"><span data-stu-id="550a0-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="550a0-189">Especifique el nombre del servicio, Hola orientados al público TCP puerto usado tooaccess Hola aplicación y puerto de destino interno de hello que escucha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="550a0-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="550a0-190">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="550a0-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="550a0-191">En este comando:</span><span class="sxs-lookup"><span data-stu-id="550a0-191">In this command:</span></span>

   * <span data-ttu-id="550a0-192">nombre del contenedor de Hello `gs-spring-boot-docker` especificado inmediatamente después de hello `expose deployment` comando</span><span class="sxs-lookup"><span data-stu-id="550a0-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="550a0-193">Hola `--type` parámetro especifica ese clúster Hola utiliza el equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="550a0-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="550a0-194">Hola `--port` parámetro especifica Hola orientados al público el puerto TCP 80.</span><span class="sxs-lookup"><span data-stu-id="550a0-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="550a0-195">El acceso a la aplicación hello en este puerto.</span><span class="sxs-lookup"><span data-stu-id="550a0-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="550a0-196">Hola `--target-port` parámetro especifica Hola interno el puerto TCP 8080.</span><span class="sxs-lookup"><span data-stu-id="550a0-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="550a0-197">equilibrador de carga de Hello reenvía las solicitudes aplicación de tooyour en este puerto.</span><span class="sxs-lookup"><span data-stu-id="550a0-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="550a0-198">Una vez que se implementa la aplicación hello toohello clúster, consultar la dirección IP externa de Hola y abrirlo en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="550a0-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="550a0-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="550a0-200">Next steps</span></span>

<span data-ttu-id="550a0-201">Para obtener más información acerca del uso de arranque del muelle en Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="550a0-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="550a0-202">Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello</span><span class="sxs-lookup"><span data-stu-id="550a0-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="550a0-203">Implementar una aplicación de arranque del muelle en Linux en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="550a0-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="550a0-204">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="550a0-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="550a0-205">Para obtener más información acerca de hello Spring arranque en el proyecto de ejemplo de Docker, consulte [arranque Spring en Introducción a Docker].</span><span class="sxs-lookup"><span data-stu-id="550a0-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="550a0-206">Hola siguientes vínculos proporciona información adicional acerca de cómo crear aplicaciones de arranque de primavera:</span><span class="sxs-lookup"><span data-stu-id="550a0-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="550a0-207">Para obtener más información acerca de cómo crear una sencilla aplicación de arranque de primavera, vea Hola primavera Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="550a0-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="550a0-208">Hello vínculos siguientes proporcionan información adicional sobre el uso de Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="550a0-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="550a0-209">Implementación de un clúster de Kubernetes para los contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="550a0-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="550a0-210">Con hello Kubernetes web interfaz de usuario con el servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="550a0-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="550a0-211">Para obtener más información sobre el uso de la interfaz de línea de comandos de Kubernetes está disponible en hello **kubectl** Guía de usuario en <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="550a0-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="550a0-212">sitio Web de Kubernetes de Hello tiene varios artículos que tratan sobre el uso de imágenes en registros privados:</span><span class="sxs-lookup"><span data-stu-id="550a0-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="550a0-213">[Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="550a0-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="550a0-214">[Espacios de nombres]</span><span class="sxs-lookup"><span data-stu-id="550a0-214">[Namespaces]</span></span>
* <span data-ttu-id="550a0-215">[Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="550a0-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="550a0-216">Para obtener más ejemplos de cómo toouse imágenes de Docker personalizado con Azure, consulte [con una imagen personalizada de Docker para la aplicación Web de Azure en Linux].</span><span class="sxs-lookup"><span data-stu-id="550a0-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[interfaz de línea de comandos (CLI) de Azure]: /cli/azure/overview
[Contenedor Service (ACS) de azure]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[con una imagen personalizada de Docker para la aplicación Web de Azure en Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[arranque primavera]: http://projects.spring.io/spring-boot/
[arranque Spring en Introducción a Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)
[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
