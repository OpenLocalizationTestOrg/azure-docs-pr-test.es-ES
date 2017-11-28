---
title: "aaaDeploy una aplicación Web de arranque de primavera en Linux en el servicio de contenedor de Azure | Documentos de Microsoft"
description: "Este tutorial le guía aunque Hola pasos toodeploy una aplicación Spring arranque como una aplicación web de Linux en Microsoft Azure."
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
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a><span data-ttu-id="4e840-103">Implementar una aplicación de arranque del muelle en Linux en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="4e840-103">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>

<span data-ttu-id="4e840-104">Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="4e840-104">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="4e840-105">Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java.</span><span class="sxs-lookup"><span data-stu-id="4e840-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="4e840-106">**[cliente de Docker]**  es soluciones de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.</span><span class="sxs-lookup"><span data-stu-id="4e840-106">**[Docker]** is open-source solutions that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="4e840-107">Este tutorial le guía a través mediante Docker toodevelop e implementar un host de Linux de arranque Spring aplicación tooa Hola [contenedor Service (ACS) de Azure].</span><span class="sxs-lookup"><span data-stu-id="4e840-107">This tutorial walks you through using Docker toodevelop and deploy a Spring Boot application tooa Linux host in hello [Azure Container Service (ACS)].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e840-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4e840-108">Prerequisites</span></span>

<span data-ttu-id="4e840-109">En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="4e840-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="4e840-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="4e840-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="4e840-111">Hola [interfaz de línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="4e840-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="4e840-112">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="4e840-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="4e840-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="4e840-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="4e840-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="4e840-114">A [Git] client.</span></span>
* <span data-ttu-id="4e840-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="4e840-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4e840-116">Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="4e840-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="4e840-117">Crear Hola Spring arranque en la aplicación web de introducción a Docker</span><span class="sxs-lookup"><span data-stu-id="4e840-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="4e840-118">Hello pasos siguientes le guían a través de los pasos de hello toocreate requiere una sencilla aplicación web de arranque de primavera y probar de forma local.</span><span class="sxs-lookup"><span data-stu-id="4e840-118">hello following steps walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="4e840-119">Abra un símbolo y crear un directorio local toohold la aplicación y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="4e840-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="4e840-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="4e840-121">Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio Hola creado; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="4e840-122">Cambiar directorio toohello completado proyecto; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-122">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="4e840-123">Compilar el archivo JAR de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-123">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="4e840-124">Una vez creada la aplicación web de hello, cambie el directorio toohello `target` directorio donde el archivo JAR de Hola se encuentra e inicia la aplicación web de hello; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-124">Once hello web app has been created, change directory toohello `target` directory where hello JAR file is located and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. <span data-ttu-id="4e840-125">Probar la aplicación web de hello examinando tooit localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="4e840-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="4e840-126">Por ejemplo, si tienes curl disponible y configurado toorun de servidor de Tomcat hello en el puerto 80:</span><span class="sxs-lookup"><span data-stu-id="4e840-126">For example, if you have curl available and you configured hello Tomcat server toorun on port 80:</span></span>
   ```
   curl http://localhost
   ```

1. <span data-ttu-id="4e840-127">Debería ver el siguiente mensaje de Hola: **Docker ¡Hello World!**</span><span class="sxs-lookup"><span data-stu-id="4e840-127">You should see hello following message displayed: **Hello Docker World!**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a><span data-ttu-id="4e840-129">Crear un registro de contenedor de Azure toouse como un registro de Docker privada</span><span class="sxs-lookup"><span data-stu-id="4e840-129">Create an Azure Container Registry toouse as a Private Docker Registry</span></span>

<span data-ttu-id="4e840-130">Hello pasos siguientes le guían a través mediante hello toocreate portal Azure un registro de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="4e840-130">hello following steps walk you through using hello Azure portal toocreate an Azure Container Registry.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4e840-131">Si desea que toouse Hola CLI de Azure en lugar de hello portal de Azure, siga los pasos de hello en [crear un registro de contenedor de Docker privado mediante hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="4e840-131">If you want toouse hello Azure CLI instead of hello Azure portal, follow hello steps in [Create a private Docker container registry using hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).</span></span>
>

1. <span data-ttu-id="4e840-132">Examinar toohello [portal de Azure] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4e840-132">Browse toohello [Azure portal] and sign in.</span></span>

   <span data-ttu-id="4e840-133">Una vez que haya iniciado sesión tooyour cuenta en hello portal de Azure, puede seguir los pasos de Hola Hola [crear un registro de contenedor de Docker privado mediante el portal de Azure de hello] artículo, que se paraphrased en hello siguiendo los pasos para hello simplificar la conveniencia.</span><span class="sxs-lookup"><span data-stu-id="4e840-133">Once you have signed in tooyour account on hello Azure portal, you can follow hello steps in hello [Create a private Docker container registry using hello Azure portal] article, which are paraphrased in hello following steps for hello sake of expediency.</span></span>

1. <span data-ttu-id="4e840-134">Haga clic en el icono de menú de Hola de **+ nuevo**, a continuación, haga clic en **contenedores**y, a continuación, haga clic en **registro de contenedor de Azure**.</span><span class="sxs-lookup"><span data-stu-id="4e840-134">Click hello menu icon for **+ New**, then click **Containers**, and then click **Azure Container Registry**.</span></span>
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. <span data-ttu-id="4e840-136">Cuando se muestra la página de información de hello para la plantilla de registro de contenedor de Azure de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="4e840-136">When hello information page for hello Azure Container Registry template is displayed, click **Create**.</span></span> 

   ![Crear una instancia de Azure Container Registry][AR02]

1. <span data-ttu-id="4e840-138">Cuando Hola **crear registro de contenedor** se muestra la página, escriba su **nombre del registro** y **grupo de recursos**, elija **habilitar** para Hola **usuario Admin**y, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="4e840-138">When hello **Create container registry** page is displayed, enter your **Registry name** and **Resource group**, choose **Enable** for hello **Admin user**, and then click **Create**.</span></span>

   ![Configurar Azure Container Registry][AR03]

1. <span data-ttu-id="4e840-140">Una vez que se ha creado el registro de contenedor, vaya tooyour del registro de contenedor en hello portal de Azure y, a continuación, haga clic en **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="4e840-140">Once your container registry has been created, navigate tooyour container registry in hello Azure portal, and then click **Access Keys**.</span></span> <span data-ttu-id="4e840-141">Tome nota de hello username y password para obtener instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e840-141">Take note of hello username and password for hello next steps.</span></span>

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a><span data-ttu-id="4e840-143">Configurar Maven toouse las claves de acceso del registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="4e840-143">Configure Maven toouse your Azure Container Registry access keys</span></span>

1. <span data-ttu-id="4e840-144">Desplácese toohello el directorio de configuración para la instalación de Maven y abra hello *settings.xml* archivo con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="4e840-144">Navigate toohello configuration directory for your Maven installation and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="4e840-145">Agregar la configuración de acceso del registro de contenedor de Azure desde la sección anterior de Hola de este tutorial toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-145">Add your Azure Container Registry access settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="4e840-146">Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera, (por ejemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completa*"), abra hello y *pom.xml* archivo con un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="4e840-146">Navigate toohello completed project directory for your Spring Boot application, (for example: "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="4e840-147">Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-147">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="4e840-148">Hola de actualización `<plugins>` colección Hola *pom.xml* de archivos para que Hola `<plugin>` contiene Hola inicio de sesión del registro y la dirección del nombre del servidor para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="4e840-148">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry from hello previous section of this tutorial.</span></span> <span data-ttu-id="4e840-149">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-149">For example:</span></span>

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

1. <span data-ttu-id="4e840-150">Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera y ejecute hello tras la aplicación de comando toorebuild Hola e inserte Hola contenedor tooyour del registro de contenedor de Azure:</span><span class="sxs-lookup"><span data-stu-id="4e840-150">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure Container Registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> <span data-ttu-id="4e840-151">Cuando está realizando la inserción de su tooAzure de contenedor de Docker, puede recibir un mensaje de error es tooone similar de hello seguir incluso aunque el contenedor de Docker se creó correctamente:</span><span class="sxs-lookup"><span data-stu-id="4e840-151">When you are pushing your Docker container tooAzure, you may receive an error message that is similar tooone of hello following even though your Docker container was created successfully:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="4e840-152">Si esto ocurre, puede que necesite toosign en tooyour cuenta de Azure desde la línea de comandos de Docker de hello; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-152">If this happens, you may need toosign in tooyour Azure account from hello Docker command line; for example:</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="4e840-153">A continuación, puede insertar el contenedor desde la línea de comandos de hello; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="4e840-153">You can then push your container from hello command line; for example:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a><span data-ttu-id="4e840-154">Crear una aplicación web en Linux en Azure App Service mediante la imagen de contenedor</span><span class="sxs-lookup"><span data-stu-id="4e840-154">Create a web app on Linux on Azure App Service using your container image</span></span>

1. <span data-ttu-id="4e840-155">Examinar toohello [portal de Azure] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4e840-155">Browse toohello [Azure portal] and sign in.</span></span>

1. <span data-ttu-id="4e840-156">Haga clic en el icono de menú de Hola de **+ nuevo**, a continuación, haga clic en **Web y móvil**y, a continuación, haga clic en **aplicación Web en Linux**.</span><span class="sxs-lookup"><span data-stu-id="4e840-156">Click hello menu icon for **+ New**, then click **Web + Mobile**, and then click **Web App on Linux**.</span></span>
   
   ![Crear una nueva aplicación web en hello portal de Azure][LX01]

1. <span data-ttu-id="4e840-158">Cuando Hola **aplicación Web en Linux** se muestra la página, escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4e840-158">When hello **Web App on Linux** page is displayed, enter hello following information:</span></span>

   <span data-ttu-id="4e840-159">a.</span><span class="sxs-lookup"><span data-stu-id="4e840-159">a.</span></span> <span data-ttu-id="4e840-160">Escriba un nombre único para hello **nombre de la aplicación**; por ejemplo: "*wingtiptoyslinux*."</span><span class="sxs-lookup"><span data-stu-id="4e840-160">Enter a unique name for hello **App name**; for example: "*wingtiptoyslinux*."</span></span>

   <span data-ttu-id="4e840-161">b.</span><span class="sxs-lookup"><span data-stu-id="4e840-161">b.</span></span> <span data-ttu-id="4e840-162">Elija su **suscripción** desde la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e840-162">Choose your **Subscription** from hello drop-down list.</span></span>

   <span data-ttu-id="4e840-163">c.</span><span class="sxs-lookup"><span data-stu-id="4e840-163">c.</span></span> <span data-ttu-id="4e840-164">Elegir una existente **grupo de recursos**, o especificar un nuevo grupo de recursos de nombre toocreate.</span><span class="sxs-lookup"><span data-stu-id="4e840-164">Choose an existing **Resource Group**, or specify a name toocreate a new resource group.</span></span>

   <span data-ttu-id="4e840-165">d.</span><span class="sxs-lookup"><span data-stu-id="4e840-165">d.</span></span> <span data-ttu-id="4e840-166">Haga clic en **configurar contenedor** y escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="4e840-166">Click **Configure container** and enter hello following information:</span></span>

      * <span data-ttu-id="4e840-167">Seleccione **Registro privado**.</span><span class="sxs-lookup"><span data-stu-id="4e840-167">Choose **Private registry**.</span></span>

      * <span data-ttu-id="4e840-168">**Imagen y etiqueta opcional**: especifique el nombre del contenedor del ejemplo anterior, por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span><span class="sxs-lookup"><span data-stu-id="4e840-168">**Image and optional tag**: Specify your container name from earlier; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"</span></span>

      * <span data-ttu-id="4e840-169">**Dirección URL del servidor**: especifique la dirección URL del Registro del ejemplo anterior, por ejemplo: "*https://wingtiptoysregistry.azurecr.io*".</span><span class="sxs-lookup"><span data-stu-id="4e840-169">**Server URL**: Specify your registry URL from earlier; for example: "*https://wingtiptoysregistry.azurecr.io*"</span></span>

      * <span data-ttu-id="4e840-170">**Nombre de usuario de inicio de sesión** y **Contraseña**: especifique las credenciales de inicio de sesión de las **Claves de acceso** que ha usado en los pasos anteriores.</span><span class="sxs-lookup"><span data-stu-id="4e840-170">**Login username** and **Password**: Specify your login credentials from your **Access Keys** that you used in previous steps.</span></span>
   
   <span data-ttu-id="4e840-171">e.</span><span class="sxs-lookup"><span data-stu-id="4e840-171">e.</span></span> <span data-ttu-id="4e840-172">Una vez que se han introducido todos Hola por encima de la información, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4e840-172">Once you have entered all of hello above information, click **OK**.</span></span>

   ![Configurar aplicaciones web][LX02]

1. <span data-ttu-id="4e840-174">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="4e840-174">Click **Create**.</span></span>

> [!NOTE]
>
> <span data-ttu-id="4e840-175">Azure asignará automáticamente el servidor de Tomcat de tooembedded de las solicitudes de Internet que se ejecuta en los puertos estándar Hola de 80 o 8080.</span><span class="sxs-lookup"><span data-stu-id="4e840-175">Azure will automatically map Internet requests tooembedded Tomcat server that is running on hello standard ports of 80 or 8080.</span></span> <span data-ttu-id="4e840-176">Sin embargo, si configuró el toorun de servidor de Tomcat incrustado en un puerto personalizado, debe tooadd una aplicación web tooyour variables de entorno que define el puerto de hello para el servidor de Tomcat incrustado.</span><span class="sxs-lookup"><span data-stu-id="4e840-176">However, if you configured your embedded Tomcat server toorun on a custom port, you need tooadd an environment variable tooyour web app that defines hello port for your embedded Tomcat server.</span></span> <span data-ttu-id="4e840-177">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="4e840-177">toodo so, use hello following steps:</span></span>
>
> 1. <span data-ttu-id="4e840-178">Examinar toohello [portal de Azure] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="4e840-178">Browse toohello [Azure portal] and sign in.</span></span>
> 
> 2. <span data-ttu-id="4e840-179">Haga clic en el icono de Hola para **servicios de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="4e840-179">Click hello icon for **App Services**.</span></span> <span data-ttu-id="4e840-180">(Vea el elemento #1 en la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="4e840-180">(See item #1 in hello image below.)</span></span>
>
> 3. <span data-ttu-id="4e840-181">Seleccione la aplicación web de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e840-181">Select your web app from hello list.</span></span> <span data-ttu-id="4e840-182">(Elemento #2 en la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="4e840-182">(Item #2 in hello image below.)</span></span>
>
> 4. <span data-ttu-id="4e840-183">Haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="4e840-183">Click **Application Settings**.</span></span> <span data-ttu-id="4e840-184">(Elemento #3 en la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="4e840-184">(Item #3 in hello image below.)</span></span>
>
> 5. <span data-ttu-id="4e840-185">Hola **configuración de la aplicación** sección, agregue una nueva variable de entorno denominada **puerto** y escriba su número de puerto personalizado para el valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="4e840-185">In hello **App settings** section, add a new environment variable named **PORT** and enter your custom port number for hello value.</span></span> <span data-ttu-id="4e840-186">(Elemento #4 de la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="4e840-186">(Item #4 in hello image below.)</span></span>
>
> 6. <span data-ttu-id="4e840-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4e840-187">Click **Save**.</span></span> <span data-ttu-id="4e840-188">(Elemento #5 en la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="4e840-188">(Item #5 in hello image below.)</span></span>
>
> ![Guardar un número de puerto personalizado en hello portal de Azure][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a><span data-ttu-id="4e840-190">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4e840-190">Next steps</span></span>

<span data-ttu-id="4e840-191">Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="4e840-191">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="4e840-192">Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello</span><span class="sxs-lookup"><span data-stu-id="4e840-192">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="4e840-193">Implementar una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="4e840-193">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="4e840-194">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="4e840-194">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="4e840-195">Para obtener más información acerca de hello Spring arranque en el proyecto de ejemplo de Docker, consulte [arranque Spring en Introducción a Docker].</span><span class="sxs-lookup"><span data-stu-id="4e840-195">For further details about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="4e840-196">Para obtener ayuda acerca de cómo empezar a usar sus propias aplicaciones de arranque de primavera, vea hello **primavera Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="4e840-196">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="4e840-197">Para obtener más información acerca de cómo empezar a crear una sencilla aplicación de arranque de primavera, vea Hola primavera Initializr en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="4e840-197">For more information about getting started with creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="4e840-198">Para obtener más ejemplos de cómo toouse imágenes de Docker personalizado con Azure, consulte [con una imagen personalizada de Docker para la aplicación Web de Azure en Linux].</span><span class="sxs-lookup"><span data-stu-id="4e840-198">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[interfaz de línea de comandos (CLI) de Azure]: /cli/azure/overview
[contenedor Service (ACS) de Azure]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[portal de Azure]: https://portal.azure.com/
[crear un registro de contenedor de Docker privado mediante el portal de Azure de hello]: /azure/container-registry/container-registry-get-started-portal
[con una imagen personalizada de Docker para la aplicación Web de Azure en Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[arranque primavera]: http://projects.spring.io/spring-boot/
[arranque Spring en Introducción a Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

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
