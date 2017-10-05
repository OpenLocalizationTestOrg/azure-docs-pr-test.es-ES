---
title: "Implementación de una aplicación web Spring Boot en Linux en Azure Container Service | Microsoft Docs"
description: "Este tutorial le guiará por los pasos necesarios para implementar una aplicación Spring Boot como una aplicación web de Linux en Microsoft Azure."
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
ms.openlocfilehash: 5f0b470bd46cfeaf00b3092dbe9db507ed50f622
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-the-azure-container-service"></a><span data-ttu-id="fe60e-103">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="fe60e-103">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>

<span data-ttu-id="fe60e-104">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="fe60e-104">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="fe60e-105">Uno de los proyectos más populares que se basa en esa plataforma es [Spring Boot], que proporciona un enfoque simplificado para crear aplicaciones de Java independientes.</span><span class="sxs-lookup"><span data-stu-id="fe60e-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="fe60e-106">**[cliente de Docker]** es una solución de código abierto que ayuda a los desarrolladores a automatizar la implementación, el escalado y la administración de sus aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="fe60e-106">**[Docker]** is open-source solutions that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="fe60e-107">En este tutorial se explica cómo usar Docker para desarrollar e implementar una aplicación de Spring Boot en un host de Linux en [Azure Container Service (ACS)].</span><span class="sxs-lookup"><span data-stu-id="fe60e-107">This tutorial walks you through using Docker to develop and deploy a Spring Boot application to a Linux host in the [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fe60e-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="fe60e-108">Prerequisites</span></span>

<span data-ttu-id="fe60e-109">Para poder realizar los pasos de este tutorial, necesitará tener los siguientes requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="fe60e-109">In order to complete the steps in this tutorial, you need to have the following prerequisites:</span></span>

* <span data-ttu-id="fe60e-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="fe60e-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="fe60e-111">La [Interfaz de la línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="fe60e-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="fe60e-112">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="fe60e-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="fe60e-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="fe60e-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="fe60e-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="fe60e-114">A [Git] client.</span></span>
* <span data-ttu-id="fe60e-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="fe60e-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe60e-116">Dados los requisitos de virtualización de este tutorial, los pasos que se describen en este artículo no se pueden seguir en una máquina virtual; es preciso usar un equipo físico con características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="fe60e-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="fe60e-117">Creación de la aplicación web Spring Boot on Docker Getting Started</span><span class="sxs-lookup"><span data-stu-id="fe60e-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="fe60e-118">Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="fe60e-118">The following steps walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="fe60e-119">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="fe60e-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="fe60e-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="fe60e-121">Clone el proyecto de ejemplo [inicial de Spring Boot en Docker] en el directorio que ha creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="fe60e-122">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-122">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="fe60e-123">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-123">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="fe60e-124">Una vez creada la aplicación web, cambie el directorio al directorio `target` donde se encuentra el archivo JAR e inicie la aplicación web, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-124">Once the web app has been created, change directory to the `target` directory where the JAR file is located and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="fe60e-125">Pruebe la aplicación web. Para ello, navegue a ella localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="fe60e-125">Test the web app by browsing to it locally using a web browser.</span></span> <span data-ttu-id="fe60e-126">Por ejemplo, si tiene curl disponible y ha configurado el servidor Tomcat para que se ejecute en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="fe60e-126">For example, if you have curl available and you configured the Tomcat server to run on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="fe60e-127">Debería aparecer el siguiente mensaje: **Hello Docker World!**</span><span class="sxs-lookup"><span data-stu-id="fe60e-127">You should see the following message displayed: **Hello Docker World!**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-to-use-as-a-private-docker-registry"></a><span data-ttu-id="fe60e-129">Crear una instancia de Azure Container Registry para usarla como un Registro de Docker privado</span><span class="sxs-lookup"><span data-stu-id="fe60e-129">Create an Azure Container Registry to use as a Private Docker Registry</span></span>

<span data-ttu-id="fe60e-130">Los siguientes pasos le muestran cómo usar Azure Portal para crear una instancia de Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="fe60e-130">The following steps walk you through using the Azure portal to create an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe60e-131">Si quiere usar la CLI de Azure en lugar de Azure Portal, siga los pasos descritos en [Creación de un registro de contenedor privado de Docker con la CLI de Azure 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fe60e-131">If you want to use the Azure CLI instead of the Azure portal, follow the steps in [Create a private Docker container registry using the Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="fe60e-132">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="fe60e-132">Browse to the [Azure portal] and sign in.</span></span>

   <span data-ttu-id="fe60e-133">Una vez que haya iniciado sesión en su cuenta en Azure Portal, puede seguir los pasos descritos en el artículo [Creación de un registro de contenedor privado de Docker con la CLI de Azure], que se vuelven a explicar en los pasos siguientes para mayor comodidad.</span><span class="sxs-lookup"><span data-stu-id="fe60e-133">Once you have signed in to your account on the Azure portal, you can follow the steps in the [Create a private Docker container registry using the Azure portal] article, which are paraphrased in the following steps for the sake of expediency.</span></span>

1. <span data-ttu-id="fe60e-134">Haga clic en el icono de menú **+ Nuevo**, en **Contenedores** y en **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-134">Click the menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. <span data-ttu-id="fe60e-136">Cuando aparezca la página de información de la plantilla de Azure Container Registry, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-136">When the information page for the Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Crear una instancia de Azure Container Registry][AR02]

1. <span data-ttu-id="fe60e-138">Cuando aparezca la página **Crear Registro de contenedor**, escriba su **Nombre del Registro** y **Grupo de recursos**, elija **Habilitar** para el **Usuario administrador** y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-138">When the **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for the **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][AR03]

1. <span data-ttu-id="fe60e-140">Una vez que se haya creado el Registro de contenedor, desplácese hasta él en Azure Portal y haga clic en **Claves de acceso**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-140">Once your container registry has been created, navigate to your container registry in the Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="fe60e-141">Tome nota del nombre de usuario y la contraseña para usarlos en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="fe60e-141">Take note of the username and password for the next steps.</span></span>

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="configure-maven-to-use-your-azure-container-registry-access-keys"></a><span data-ttu-id="fe60e-143">Configurar Maven para que use las claves de acceso de Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="fe60e-143">Configure Maven to use your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="fe60e-144">Navegue hasta el directorio de configuración de la instalación de Maven y abra el archivo *settings.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fe60e-144">Navigate to the configuration directory for your Maven installation and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="fe60e-145">Agregue la configuración de acceso de Azure Container Registry de la sección anterior de este tutorial a la colección `<servers>` en el archivo *settings.xml*, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-145">Add your Azure Container Registry access settings from the previous section of this tutorial to the `<servers>` collection in the *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="fe60e-146">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") y abra el archivo *pom.xml* con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="fe60e-146">Navigate to the completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="fe60e-147">Actualice la colección `<properties>` del archivo *pom.xml* con el valor del servidor de inicio de sesión de Azure Container Registry de la sección anterior de este tutorial, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-147">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry from the previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="fe60e-148">Actualice la colección `<plugins>` del archivo *pom.xml* de modo que `<plugin>` contenga la dirección del servidor de inicio de sesión y el nombre de Registro de Azure Container Registry de la sección anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="fe60e-148">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry from the previous section of this tutorial.</span></span> <span data-ttu-id="fe60e-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-149">For example:</span></span>

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

1. <span data-ttu-id="fe60e-150">Navegue hasta el directorio de proyecto completado de la aplicación Spring Boot y ejecute el siguiente comando para recompilar la aplicación e insertar el contenedor en Azure Container Registry:</span><span class="sxs-lookup"><span data-stu-id="fe60e-150">Navigate to the completed project directory for your Spring Boot application and run the following command to rebuild the application and push the container to your Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="fe60e-151">Cuando inserte el contenedor de Docker en Azure, podría recibir un mensaje de error similar a uno de los siguientes, incluso si el contenedor de Docker se ha creado correctamente:</span><span class="sxs-lookup"><span data-stu-id="fe60e-151">When you are pushing your Docker container to Azure, you may receive an error message that is similar to one of the following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="fe60e-152">Si esto ocurre, es posible que deba iniciar sesión en la cuenta de Azure desde la línea de comandos de Docker, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-152">If this happens, you may need to sign in to your Azure account from the Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="fe60e-153">Después, puede insertar el contenedor desde la línea de comandos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="fe60e-153">You can then push your container from the command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="fe60e-154">Crear una aplicación web en Linux en Azure App Service mediante la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="fe60e-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="fe60e-155">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="fe60e-155">Browse to the [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="fe60e-156">Haga clic en el icono de menú **+ Nuevo**, en **Web y móvil** y en **Web App on Linux** (Aplicación web en Linux).</span><span class="sxs-lookup"><span data-stu-id="fe60e-156">Click the menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Crear una aplicación web en Azure Portal][LX01]

1. <span data-ttu-id="fe60e-158">Cuando aparezca la página **Aplicación web en Linux**, especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe60e-158">When the **Web App on Linux** page is displayed, enter the following information:</span></span>

   <span data-ttu-id="fe60e-159">a.</span><span class="sxs-lookup"><span data-stu-id="fe60e-159">a.</span></span> <span data-ttu-id="fe60e-160">Escriba un nombre único para el **Nombre de la aplicación**, por ejemplo: "*wingtiptoyslinux*".</span><span class="sxs-lookup"><span data-stu-id="fe60e-160">Enter a unique name for the **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="fe60e-161">b.</span><span class="sxs-lookup"><span data-stu-id="fe60e-161">b.</span></span> <span data-ttu-id="fe60e-162">Seleccione su **Suscripción** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="fe60e-162">Choose your **Subscription** from the drop-down list.</span></span>

   <span data-ttu-id="fe60e-163">c.</span><span class="sxs-lookup"><span data-stu-id="fe60e-163">c.</span></span> <span data-ttu-id="fe60e-164">Seleccione un **Grupo de recursos** existente o especifique un nombre para crear uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="fe60e-164">Choose an existing **Resource Group**, or specify a name to create a new resource group.</span></span>

   <span data-ttu-id="fe60e-165">d.</span><span class="sxs-lookup"><span data-stu-id="fe60e-165">d.</span></span> <span data-ttu-id="fe60e-166">Haga clic en **Configurar contenedor** y especifique la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="fe60e-166">Click **Configure container** and enter the following information:</span></span>

      * <span data-ttu-id="fe60e-167">Seleccione **Registro privado**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="fe60e-168">**Imagen y etiqueta opcional**: especifique el nombre del contenedor del ejemplo anterior, por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="fe60e-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="fe60e-169">**Dirección URL del servidor**: especifique la dirección URL del Registro del ejemplo anterior, por ejemplo: "*https://wingtiptoysregistry.azurecr.io*".</span><span class="sxs-lookup"><span data-stu-id="fe60e-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="fe60e-170">**Nombre de usuario de inicio de sesión** y **Contraseña**: especifique las credenciales de inicio de sesión de las **Claves de acceso** que ha usado en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="fe60e-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="fe60e-171">e.</span><span class="sxs-lookup"><span data-stu-id="fe60e-171">e.</span></span> <span data-ttu-id="fe60e-172">Cuando haya especificado la información anterior, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-172">Once you have entered all of the above information, click **OK**.</span></span>

   ![Configurar aplicaciones web][LX02]

1. <span data-ttu-id="fe60e-174">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="fe60e-175">Azure asignará automáticamente las solicitudes de Internet al servidor Tomcat integrado que se ejecuta en los puertos estándar 80 u 8080.</span><span class="sxs-lookup"><span data-stu-id="fe60e-175">Azure will automatically map Internet requests to embedded Tomcat server that is running on the standard ports of 80 or 8080.</span></span> <span data-ttu-id="fe60e-176">Aun así, si ha configurado el servidor Tomcat integrado para que se ejecute en un puerto personalizado, debe agregar una variable de entorno a la aplicación web que defina el puerto del servidor Tomcat integrado.</span><span class="sxs-lookup"><span data-stu-id="fe60e-176">However, if you configured your embedded Tomcat server to run on a custom port, you need to add an environment variable to your web app that defines the port for your embedded Tomcat server.</span></span> <span data-ttu-id="fe60e-177">Para ello, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="fe60e-177">To do so, use the following steps:</span></span>
>
> 1. <span data-ttu-id="fe60e-178">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="fe60e-178">Browse to the [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="fe60e-179">Haga clic en el icono de **App Services**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-179">Click the icon for **App Services**.</span></span> <span data-ttu-id="fe60e-180">(Vea el elemento n.º 1 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="fe60e-180">(See item #1 in the image below.)</span></span>
>
> 3. <span data-ttu-id="fe60e-181">Seleccione la aplicación web en la lista.</span><span class="sxs-lookup"><span data-stu-id="fe60e-181">Select your web app from the list.</span></span> <span data-ttu-id="fe60e-182">(Vea el elemento n.º 2 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="fe60e-182">(Item #2 in the image below.)</span></span>
>
> 4. <span data-ttu-id="fe60e-183">Haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-183">Click **Application Settings**.</span></span> <span data-ttu-id="fe60e-184">(Vea el elemento n.º 3 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="fe60e-184">(Item #3 in the image below.)</span></span>
>
> 5. <span data-ttu-id="fe60e-185">En la sección **Configuración de la aplicación**, agregue una nueva variable de entorno denominada **PORT** y especifique como valor su número de puerto personalizado.</span><span class="sxs-lookup"><span data-stu-id="fe60e-185">In the **App settings** section, add a new environment variable named **PORT** and enter your custom port number for the value.</span></span> <span data-ttu-id="fe60e-186">(Vea el elemento n.º 4 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="fe60e-186">(Item #4 in the image below.)</span></span>
>
> 6. <span data-ttu-id="fe60e-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="fe60e-187">Click **Save**.</span></span> <span data-ttu-id="fe60e-188">(Vea el elemento n.º 5 de la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="fe60e-188">(Item #5 in the image below.)</span></span>
>
> ![Guardar un número de puerto personalizado en Azure Portal][LX03]
>

<!--
##  OPTIONAL: Configure the embedded Tomcat server to run on a different port

The embedded Tomcat server in the sample Spring Boot application is configured to run on port 8080 by default. However, if you want to run the embedded Tomcat server to run on a different port, such as port 80 for local testing, you can configure the port by using the following steps.

1. Go to the *resources* directory (or create the directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open the *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify the **server** setting so that the server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close the *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="fe60e-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe60e-190">Next steps</span></span>

<span data-ttu-id="fe60e-191">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="fe60e-191">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="fe60e-192">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="fe60e-192">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="fe60e-193">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="fe60e-193">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="fe60e-194">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="fe60e-194">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="fe60e-195">Para obtener más información sobre el proyecto de ejemplo Spring Boot en Docker, vea [inicial de Spring Boot en Docker] (Introducción a Spring Boot en Docker).</span><span class="sxs-lookup"><span data-stu-id="fe60e-195">For further details about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="fe60e-196">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="fe60e-196">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="fe60e-197">Para obtener más información sobre cómo empezar a crear una sencilla aplicación Spring Boot, vea Spring Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="fe60e-197">For more information about getting started with creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="fe60e-198">Para ver más ejemplos de cómo usar imágenes de Docker personalizadas con Azure, consulte [Uso de una imagen personalizada de Docker para Web App on Linux de Azure].</span><span class="sxs-lookup"><span data-stu-id="fe60e-198">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="fe60e-199">[Interfaz de la línea de comandos (CLI) de Azure]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="fe60e-199">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="fe60e-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="fe60e-200">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="fe60e-201">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="fe60e-201">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="fe60e-202">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="fe60e-202">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="fe60e-203">[Creación de un registro de contenedor privado de Docker con la CLI de Azure]: /azure/container-registry/container-registry-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="fe60e-203">[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal</span></span>
<span data-ttu-id="fe60e-204">[Uso de una imagen personalizada de Docker para Web App on Linux de Azure]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="fe60e-204">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="fe60e-205">[cliente de Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="fe60e-205">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="fe60e-206">[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="fe60e-206">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="fe60e-207">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="fe60e-207">[Git]: https://github.com/</span></span>
<span data-ttu-id="fe60e-208">[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="fe60e-208">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="fe60e-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="fe60e-209">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="fe60e-210">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="fe60e-210">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="fe60e-211">[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="fe60e-211">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="fe60e-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="fe60e-212">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="fe60e-213">[inicial de Spring Boot en Docker]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="fe60e-213">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="fe60e-214">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="fe60e-214">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
