---
title: "Implementación de una aplicación Spring Boot en Kubernetes en Azure Container Service | Microsoft Docs"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot en un clúster de Kubernetes en Microsoft Azure."
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
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="13ba2-103">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="13ba2-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="13ba2-104">**[Spring Framework]** es un popular marco de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web.</span><span class="sxs-lookup"><span data-stu-id="13ba2-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="13ba2-105">Este tutorial utiliza una aplicación de ejemplo creada mediante [Spring arranque], un enfoque basado en la convención para usar Spring para empezar a trabajar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="13ba2-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="13ba2-106">**[Kubernetes]** y **[cliente de Docker]** son soluciones de código abierto que ayudan a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="13ba2-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="13ba2-107">Este tutorial le guía en la combinación de estas dos populares tecnologías de código abierto para desarrollar e implementar una aplicación Spring Boot en Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="13ba2-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="13ba2-108">Más en concreto, *[Spring arranque]* se usa para el desarrollo de aplicaciones, *[Kubernetes]* para la implementación de contenedores y [Azure Container Service (ACS)] para hospedar su aplicación.</span><span class="sxs-lookup"><span data-stu-id="13ba2-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="13ba2-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="13ba2-109">Prerequisites</span></span>

* <span data-ttu-id="13ba2-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="13ba2-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="13ba2-111">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="13ba2-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="13ba2-112">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="13ba2-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="13ba2-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="13ba2-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="13ba2-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="13ba2-114">A [Git] client.</span></span>
* <span data-ttu-id="13ba2-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="13ba2-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="13ba2-116">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="13ba2-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="13ba2-117">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="13ba2-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="13ba2-118">Los siguientes pasos le guían a través de la creación de una aplicación web Spring Boot y la realización de pruebas de la misma de forma local.</span><span class="sxs-lookup"><span data-stu-id="13ba2-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="13ba2-119">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13ba2-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="13ba2-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="13ba2-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="13ba2-121">Clone el proyecto de ejemplo [Spring Boot on Docker Getting Started] en el directorio.</span><span class="sxs-lookup"><span data-stu-id="13ba2-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="13ba2-122">Cambie de directorio al del proyecto completado.</span><span class="sxs-lookup"><span data-stu-id="13ba2-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="13ba2-123">Utilice Maven para compilar y ejecutar la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="13ba2-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="13ba2-124">Pruebe la aplicación web examinando http://localhost:8080 o con el siguiente comando `curl`:</span><span class="sxs-lookup"><span data-stu-id="13ba2-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="13ba2-125">Debería aparecer el siguiente mensaje: **Hello Docker World**</span><span class="sxs-lookup"><span data-stu-id="13ba2-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="13ba2-127">Creación de una instancia de Azure Container Registry mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="13ba2-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="13ba2-128">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="13ba2-128">Open a command prompt.</span></span>

1. <span data-ttu-id="13ba2-129">Inicie sesión en una cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="13ba2-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="13ba2-130">Cree un grupo de recursos para los recursos de Azure que se usan en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="13ba2-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="13ba2-131">Crear una instancia de Azure Container Registry en el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="13ba2-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="13ba2-132">El tutorial inserta la aplicación de ejemplo en forma de imagen Docker en este registro en los pasos posteriores.</span><span class="sxs-lookup"><span data-stu-id="13ba2-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="13ba2-133">Reemplace `wingtiptoysregistry` por un nombre único para el registro.</span><span class="sxs-lookup"><span data-stu-id="13ba2-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="13ba2-134">Inserción de una aplicación en el registro de contenedor</span><span class="sxs-lookup"><span data-stu-id="13ba2-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="13ba2-135">Navegue hasta el directorio de configuración de la instalación de Maven (valor predeterminado ~/.m2/ o C:\Users\username\.m2) y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="13ba2-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="13ba2-136">Recupere la contraseña del registro de contenedor de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="13ba2-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="13ba2-137">Agregue el identificador y la contraseña de Azure Container Registry a una nueva colección `<server>` del archivo *settings.xml*.</span><span class="sxs-lookup"><span data-stu-id="13ba2-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="13ba2-138">`id` y `username` son el nombre del registro.</span><span class="sxs-lookup"><span data-stu-id="13ba2-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="13ba2-139">Use el valor `password` del comando anterior (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="13ba2-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="13ba2-140">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="13ba2-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="13ba2-141">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="13ba2-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="13ba2-142">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contiene la dirección del servidor de inicio de sesión y el nombre de registro de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="13ba2-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="13ba2-143">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para crear el contenedor Docker e insertar la imagen en el registro:</span><span class="sxs-lookup"><span data-stu-id="13ba2-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="13ba2-144">Cuando Maven inserta la imagen en Azure, puede recibir un mensaje de error similar a uno de los siguientes:</span><span class="sxs-lookup"><span data-stu-id="13ba2-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="13ba2-145">Si aparece este error, inicie sesión en Azure desde la línea de comandos de Docker.</span><span class="sxs-lookup"><span data-stu-id="13ba2-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="13ba2-146">Después, inserte el contenedor:</span><span class="sxs-lookup"><span data-stu-id="13ba2-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="13ba2-147">Creación de un clúster de Kubernetes en ACS mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="13ba2-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="13ba2-148">Cree un clúster de Kubernetes en Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="13ba2-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="13ba2-149">El siguiente comando crea un clúster de *Kubernetes* en el grupo de recursos *wingtiptoys-kubernetes*, con *wingtiptoys-objeto containerservice* como nombre de clúster y *wingtiptoys-kubernetes* como prefijo de DNS:</span><span class="sxs-lookup"><span data-stu-id="13ba2-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="13ba2-150">Esta operación puede tardar un tiempo en completarse.</span><span class="sxs-lookup"><span data-stu-id="13ba2-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="13ba2-151">Instale `kubectl` mediante la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="13ba2-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="13ba2-152">Los usuarios de Linux pueden tener anteceder este comando con `sudo`, ya que implementa la CLI de Kubernetes en `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="13ba2-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="13ba2-153">Descargar la información de configuración del clúster para que pueda administrar el clúster desde la interfaz web de Kubernetes y `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="13ba2-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="13ba2-154">Implementación de la imagen en un clúster de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="13ba2-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="13ba2-155">Este tutorial implementa la aplicación mediante `kubectl` y, después, le permite explorar la implementación a través de la interfaz de web de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="13ba2-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="13ba2-156">Implementación con la interfaz web de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="13ba2-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="13ba2-157">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="13ba2-157">Open a command prompt.</span></span>

1. <span data-ttu-id="13ba2-158">Abra el sitio web de configuración del clúster de Kubernetes en el explorador predeterminado:</span><span class="sxs-lookup"><span data-stu-id="13ba2-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="13ba2-159">Cuando el sitio web para la configuración de Kubernetes se abra en el explorador, haga clic en el vínculo para **implementar una aplicación en contenedores**:</span><span class="sxs-lookup"><span data-stu-id="13ba2-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Sitio web para la configuración de Kubernetes][KB01]

1. <span data-ttu-id="13ba2-161">Cuando se muestra la página **Deploy a containerized app** (Implementar una aplicación en contenedor), especifique las opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="13ba2-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="13ba2-162">a.</span><span class="sxs-lookup"><span data-stu-id="13ba2-162">a.</span></span> <span data-ttu-id="13ba2-163">Seleccione **Specify app details below** (Especificar detalles de la aplicación a continuación).</span><span class="sxs-lookup"><span data-stu-id="13ba2-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="13ba2-164">b.</span><span class="sxs-lookup"><span data-stu-id="13ba2-164">b.</span></span> <span data-ttu-id="13ba2-165">Escriba el nombre de la aplicación Spring Boot en **App name** (Nombre de aplicación); por ejemplo: "*gs-spring-boot-docker*".</span><span class="sxs-lookup"><span data-stu-id="13ba2-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="13ba2-166">c.</span><span class="sxs-lookup"><span data-stu-id="13ba2-166">c.</span></span> <span data-ttu-id="13ba2-167">Escriba el servidor de inicio de sesión y la imagen del contenedor de anteriormente en **Container image** (Imagen del contenedor); por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="13ba2-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="13ba2-168">d.</span><span class="sxs-lookup"><span data-stu-id="13ba2-168">d.</span></span> <span data-ttu-id="13ba2-169">Elija **External** (Externo) en **Service** (Servicio).</span><span class="sxs-lookup"><span data-stu-id="13ba2-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="13ba2-170">e.</span><span class="sxs-lookup"><span data-stu-id="13ba2-170">e.</span></span> <span data-ttu-id="13ba2-171">Especifique los puertos interno y externo en los cuadros de texto **Port** (Puerto) y **Target port** (Puerto de destino).</span><span class="sxs-lookup"><span data-stu-id="13ba2-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Sitio web para la configuración de Kubernetes][KB02]


1. <span data-ttu-id="13ba2-173">Haga clic en **Deploy** (Implementar) para implementar el contenedor.</span><span class="sxs-lookup"><span data-stu-id="13ba2-173">Click **Deploy** to deploy the container.</span></span>

   ![Implementar un contenedor][KB05]

1. <span data-ttu-id="13ba2-175">Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).</span><span class="sxs-lookup"><span data-stu-id="13ba2-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Servicios de Kubernetes][KB06]

1. <span data-ttu-id="13ba2-177">Si hace clic en el vínculo de **External endpoints** (Puntos de conexión externos), puede ver que la aplicación Spring Boot se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="13ba2-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="13ba2-180">Implementación con kubectl</span><span class="sxs-lookup"><span data-stu-id="13ba2-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="13ba2-181">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="13ba2-181">Open a command prompt.</span></span>

1. <span data-ttu-id="13ba2-182">Ejecute el contenedor en el clúster de Kubernetes mediante el comando `kubectl run`.</span><span class="sxs-lookup"><span data-stu-id="13ba2-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="13ba2-183">Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa.</span><span class="sxs-lookup"><span data-stu-id="13ba2-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="13ba2-184">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13ba2-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="13ba2-185">En este comando:</span><span class="sxs-lookup"><span data-stu-id="13ba2-185">In this command:</span></span>

   * <span data-ttu-id="13ba2-186">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `run`</span><span class="sxs-lookup"><span data-stu-id="13ba2-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="13ba2-187">El parámetro `--image` especifica la combinación de servidor de inicio de sesión y nombre de imagen como `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="13ba2-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="13ba2-188">Exponga externamente el clúster Kubernetes mediante el comando `kubectl expose`.</span><span class="sxs-lookup"><span data-stu-id="13ba2-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="13ba2-189">Especifique el nombre del servicio, el puerto TCP de acceso público utilizado para acceder a la aplicación y el puerto de destino interno en que escucha la aplicación.</span><span class="sxs-lookup"><span data-stu-id="13ba2-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="13ba2-190">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="13ba2-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="13ba2-191">En este comando:</span><span class="sxs-lookup"><span data-stu-id="13ba2-191">In this command:</span></span>

   * <span data-ttu-id="13ba2-192">El nombre del contenedor `gs-spring-boot-docker` se especifica inmediatamente después del comando `expose deployment`</span><span class="sxs-lookup"><span data-stu-id="13ba2-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="13ba2-193">El parámetro `--type` especifica que el clúster utiliza equilibrador de carga</span><span class="sxs-lookup"><span data-stu-id="13ba2-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="13ba2-194">El parámetro `--port` especifica el puerto TCP de acceso público, el 80.</span><span class="sxs-lookup"><span data-stu-id="13ba2-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="13ba2-195">El acceso a la aplicación se realiza a través de este puerto.</span><span class="sxs-lookup"><span data-stu-id="13ba2-195">You access the app on this port.</span></span>

   * <span data-ttu-id="13ba2-196">El parámetro `--target-port` especifica el puerto TCP interno, el 8080.</span><span class="sxs-lookup"><span data-stu-id="13ba2-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="13ba2-197">El equilibrador de carga reenvía las solicitudes a la aplicación en este puerto.</span><span class="sxs-lookup"><span data-stu-id="13ba2-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="13ba2-198">Una vez que la aplicación se implementa en el clúster, consulte la dirección IP externa y ábrala en el explorador web:</span><span class="sxs-lookup"><span data-stu-id="13ba2-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a><span data-ttu-id="13ba2-200">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="13ba2-200">Next steps</span></span>

<span data-ttu-id="13ba2-201">Para más información acerca del uso de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="13ba2-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="13ba2-202">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="13ba2-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="13ba2-203">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="13ba2-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="13ba2-204">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="13ba2-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="13ba2-205">Para más información acerca del proyecto de ejemplo Spring Boot on Docker, consulte [Spring Boot on Docker Getting Started].</span><span class="sxs-lookup"><span data-stu-id="13ba2-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="13ba2-206">Los vínculos siguientes proporcionan información adicional acerca de cómo crear aplicaciones Spring Boot:</span><span class="sxs-lookup"><span data-stu-id="13ba2-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="13ba2-207">Para más información acerca de cómo crear una sencilla aplicación Spring Boot, consulte Initializr Spring en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="13ba2-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="13ba2-208">Los vínculos siguientes proporcionan información adicional acerca del uso de Kubernetes con Azure:</span><span class="sxs-lookup"><span data-stu-id="13ba2-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="13ba2-209">Implementación de un clúster de Kubernetes para los contenedores de Linux</span><span class="sxs-lookup"><span data-stu-id="13ba2-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="13ba2-210">Uso de la interfaz de usuario web de Kubernetes con Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="13ba2-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="13ba2-211">Para más información acerca del uso de la interfaz de línea de comandos de Kubernetes, consulte la guía de usuario de **kubectl** en <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="13ba2-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="13ba2-212">El sitio web de Kubernetes tiene varios artículos que tratan el uso de imágenes en registros privados:</span><span class="sxs-lookup"><span data-stu-id="13ba2-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="13ba2-213">[Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="13ba2-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="13ba2-214">[Espacios de nombres]</span><span class="sxs-lookup"><span data-stu-id="13ba2-214">[Namespaces]</span></span>
* <span data-ttu-id="13ba2-215">[Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="13ba2-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="13ba2-216">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="13ba2-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="13ba2-217">[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="13ba2-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="13ba2-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="13ba2-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="13ba2-219">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="13ba2-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="13ba2-220">[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="13ba2-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="13ba2-221">[cliente de Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="13ba2-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="13ba2-222">[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="13ba2-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="13ba2-223">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="13ba2-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="13ba2-224">[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="13ba2-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="13ba2-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="13ba2-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="13ba2-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="13ba2-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="13ba2-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="13ba2-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="13ba2-228">[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="13ba2-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="13ba2-229">[Spring arranque]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="13ba2-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="13ba2-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="13ba2-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="13ba2-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="13ba2-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="13ba2-232">[Configure Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/ (Configurar cuentas de servicio para pods)</span><span class="sxs-lookup"><span data-stu-id="13ba2-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="13ba2-233">[Espacios de nombres]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="13ba2-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="13ba2-234">[Pull an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/ (Extraer una imagen de un registro privado)</span><span class="sxs-lookup"><span data-stu-id="13ba2-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

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
