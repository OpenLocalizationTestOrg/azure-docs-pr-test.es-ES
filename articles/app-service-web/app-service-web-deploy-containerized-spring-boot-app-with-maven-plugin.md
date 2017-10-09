---
title: "aaaHow toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque del muelle en contenedores"
description: "Obtenga información acerca de cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: e7e760d4ef5bd4c92a4126a50a2b12e5c8f2b4a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-containerized-spring-boot-app-tooazure"></a><span data-ttu-id="b76b5-103">Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque del muelle en contenedores</span><span class="sxs-lookup"><span data-stu-id="b76b5-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>

<span data-ttu-id="b76b5-104">Hola [Maven complemento para las aplicaciones Web de Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Maven Apache](http://maven.apache.org/) proporciona una perfecta integración del servicio de aplicaciones de Azure en proyectos de Maven y optimiza el proceso de Hola para las aplicaciones web de los desarrolladores toodeploy tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b76b5-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service  into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service .</span></span>

<span data-ttu-id="b76b5-105">Este artículo muestra cómo utilizar hello Maven complemento para aplicaciones Web de Azure toodeploy una aplicación de arranque de primavera de ejemplo en un tooAzure de contenedor de Docker servicios de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b76b5-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application in a Docker container tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b76b5-106">Hola Maven complemento para las aplicaciones Web de Azure está disponible actualmente como una vista previa.</span><span class="sxs-lookup"><span data-stu-id="b76b5-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="b76b5-107">Por ahora, se admite solo la publicación FTP, aunque características adicionales están planificadas para futuras Hola.</span><span class="sxs-lookup"><span data-stu-id="b76b5-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="b76b5-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b76b5-108">Prerequisites</span></span>

<span data-ttu-id="b76b5-109">En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="b76b5-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="b76b5-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="b76b5-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="b76b5-111">Hola [interfaz de línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="b76b5-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="b76b5-112">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="b76b5-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="b76b5-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="b76b5-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="b76b5-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="b76b5-114">A [Git] client.</span></span>
* <span data-ttu-id="b76b5-115">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="b76b5-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b76b5-116">Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="b76b5-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="b76b5-117">Ejemplo de Hola a Clone Spring arranque en la aplicación web de Docker</span><span class="sxs-lookup"><span data-stu-id="b76b5-117">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="b76b5-118">En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.</span><span class="sxs-lookup"><span data-stu-id="b76b5-118">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="b76b5-119">Abra un símbolo del sistema o la ventana de terminal y cree un directorio local toohold la aplicación de arranque de primavera y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-119">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="b76b5-120">-- o --</span><span class="sxs-lookup"><span data-stu-id="b76b5-120">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="b76b5-121">Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio Hola creado; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="b76b5-122">Cambiar directorio toohello completado proyecto; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-122">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="b76b5-123">Compilar el archivo JAR de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-123">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b76b5-124">Cuándo se ha creado la aplicación web de hello, iniciar la aplicación web de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-124">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="b76b5-125">Probar la aplicación web de hello examinando tooit localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="b76b5-125">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="b76b5-126">Por ejemplo, podría utilizar Hola siguiente comando si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="b76b5-126">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="b76b5-127">Debería ver el siguiente mensaje de Hola: **Docker Hola a todos**</span><span class="sxs-lookup"><span data-stu-id="b76b5-127">You should see hello following message displayed: **Hello Docker World**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="b76b5-128">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="b76b5-128">Create an Azure service principal</span></span>

<span data-ttu-id="b76b5-129">En esta sección, creará un Azure entidad de servicio que Hola usos de complemento de Maven al implementar su tooAzure de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b76b5-129">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="b76b5-130">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="b76b5-130">Open a command prompt.</span></span>

1. <span data-ttu-id="b76b5-131">Inicio de sesión en su cuenta de Azure mediante el uso de Hola CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="b76b5-131">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="b76b5-132">Siga Hola instrucciones toocomplete Hola inicio de sesión en proceso.</span><span class="sxs-lookup"><span data-stu-id="b76b5-132">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="b76b5-133">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="b76b5-133">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="b76b5-134">Donde `uuuuuuuu` es el nombre de usuario de Hola y `pppppppp` es contraseña Hola Hola principal de servicio.</span><span class="sxs-lookup"><span data-stu-id="b76b5-134">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="b76b5-135">Azure responde con JSON similar al siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="b76b5-135">Azure responds with JSON that resembles hello following example:</span></span>
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > <span data-ttu-id="b76b5-136">Utilizará valores de hello de esta respuesta JSON cuando configura hello Maven complemento toodeploy tooAzure de su contenedor.</span><span class="sxs-lookup"><span data-stu-id="b76b5-136">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="b76b5-137">Hola `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición, que son usado en este ejemplo se toomake toomap más fácil estos valores tootheir respectivos elementos cuando se configura el Maven `settings.xml` archivo Hola a continuación sección.</span><span class="sxs-lookup"><span data-stu-id="b76b5-137">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="b76b5-138">Configurar la entidad de seguridad de servicio de Azure de Maven toouse</span><span class="sxs-lookup"><span data-stu-id="b76b5-138">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="b76b5-139">En esta sección, utiliza valores de hello de la autenticación de hello tooconfigure principal de servicio de Azure que va a usar Maven al implementar su tooAzure de contenedor.</span><span class="sxs-lookup"><span data-stu-id="b76b5-139">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven will use when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="b76b5-140">Abra su Maven `settings.xml` un archivo en un editor de texto; este archivo puede encontrarse en una ruta de acceso como hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="b76b5-140">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="b76b5-141">Agregar la configuración de entidad de seguridad de servicio de Azure desde la sección anterior de Hola de este tutorial toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-141">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   <span data-ttu-id="b76b5-142">Donde:</span><span class="sxs-lookup"><span data-stu-id="b76b5-142">Where:</span></span>
   <span data-ttu-id="b76b5-143">Elemento</span><span class="sxs-lookup"><span data-stu-id="b76b5-143">Element</span></span> | <span data-ttu-id="b76b5-144">Descripción</span><span class="sxs-lookup"><span data-stu-id="b76b5-144">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="b76b5-145">Especifica un nombre único que Maven use toolook su configuración de seguridad cuando se implementa la tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b76b5-145">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="b76b5-146">Contiene Hola `appId` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b76b5-146">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="b76b5-147">Contiene Hola `tenant` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b76b5-147">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="b76b5-148">Contiene Hola `password` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b76b5-148">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="b76b5-149">Define el entorno de nube de Azure de destino de hello, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b76b5-149">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="b76b5-150">(Una lista completa de los entornos de está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación)</span><span class="sxs-lookup"><span data-stu-id="b76b5-150">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="b76b5-151">Guarde y cierre hello *settings.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="b76b5-151">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-deploy-your-local-docker-file-toodocker-hub"></a><span data-ttu-id="b76b5-152">OPCIONAL: Implementar la tooDocker de archivo Docker Hub local</span><span class="sxs-lookup"><span data-stu-id="b76b5-152">OPTIONAL: Deploy your local Docker file tooDocker Hub</span></span>

<span data-ttu-id="b76b5-153">Si tiene una cuenta de Docker, puede generar a su Docker localmente la imagen de contenedor e insertarlo tooDocker concentrador.</span><span class="sxs-lookup"><span data-stu-id="b76b5-153">If you have a Docker account, you can build your Docker container image locally and push it tooDocker Hub.</span></span> <span data-ttu-id="b76b5-154">toodo por lo tanto, utilice Hola pasos.</span><span class="sxs-lookup"><span data-stu-id="b76b5-154">toodo so, use hello following steps.</span></span>

1. <span data-ttu-id="b76b5-155">Abra hello `pom.xml` archivo de la aplicación de arranque del muelle en un editor de texto.</span><span class="sxs-lookup"><span data-stu-id="b76b5-155">Open hello `pom.xml` file for your Spring Boot application in a text editor.</span></span>

1. <span data-ttu-id="b76b5-156">Busque hello `<imageName>` elemento secundario de hello `<containerSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="b76b5-156">Locate hello `<imageName>` child element of hello `<containerSettings>` element.</span></span>

1. <span data-ttu-id="b76b5-157">Hola de actualización `${docker.image.prefix}` valor con el nombre de la cuenta de Docker:</span><span class="sxs-lookup"><span data-stu-id="b76b5-157">Update hello `${docker.image.prefix}` value with your Docker account name:</span></span>
   ```xml
   <containerSettings>
      <imageName>mydockeraccountname/${project.artifactId}</imageName>
   </containerSettings>
   ```

1. <span data-ttu-id="b76b5-158">Elija uno de hello siguiendo métodos de implementación:</span><span class="sxs-lookup"><span data-stu-id="b76b5-158">Choose one of hello following deployment methods:</span></span>

   * <span data-ttu-id="b76b5-159">Generar la imagen de contenedor localmente con Maven y, a continuación, usar Docker toopush su tooDocker contenedor concentrador:</span><span class="sxs-lookup"><span data-stu-id="b76b5-159">Build your container image locally with Maven, and then use Docker toopush your container tooDocker Hub:</span></span>
      ```shell
      mvn clean package docker:build
      docker push
      ```
   
   * <span data-ttu-id="b76b5-160">Si tienes hello [complemento de Docker para Maven] instalado, puede generar automáticamente y su tooDocker de imagen de contenedor concentrador mediante el uso de Hola `-DpushImage` parámetro:</span><span class="sxs-lookup"><span data-stu-id="b76b5-160">If you have hello [Docker plugin for Maven] installed, you can automatically build and your container image tooDocker Hub by using hello `-DpushImage` parameter:</span></span>
      ```shell
      mvn clean package docker:build -DpushImage
      ```

## <a name="optional-customize-your-pomxml-before-deploying-your-container-tooazure"></a><span data-ttu-id="b76b5-161">OPCIONAL: Personalizar la pom.xml antes de implementar su tooAzure de contenedor</span><span class="sxs-lookup"><span data-stu-id="b76b5-161">OPTIONAL: Customize your pom.xml before deploying your container tooAzure</span></span>

<span data-ttu-id="b76b5-162">Abra hello `pom.xml` de archivos para la aplicación de arranque del muelle en un editor de texto y, a continuación, busque hello `<plugin>` (elemento) para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="b76b5-162">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="b76b5-163">Este elemento debe ser similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-163">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="b76b5-164">Hay varios valores que se pueden modificar para hello Maven complemento y obtener una descripción detallada de cada uno de estos elementos está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación.</span><span class="sxs-lookup"><span data-stu-id="b76b5-164">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="b76b5-165">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-165">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="b76b5-166">Elemento</span><span class="sxs-lookup"><span data-stu-id="b76b5-166">Element</span></span> | <span data-ttu-id="b76b5-167">Descripción</span><span class="sxs-lookup"><span data-stu-id="b76b5-167">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="b76b5-168">Especifica la versión de Hola de hello [Maven complemento para las aplicaciones Web de Azure].</span><span class="sxs-lookup"><span data-stu-id="b76b5-168">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="b76b5-169">Debe comprobar la versión de Hola enumerada en hello [repositorio Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que utilizas Hola versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="b76b5-169">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="b76b5-170">Especifica la información de autenticación de Hola de Azure, que en este ejemplo contiene un `<serverId>` elemento que contiene `azure-auth`; Maven usa ese toolook valor valores de entidad de seguridad de servicio de Azure de hello en su Maven *settings.xml* archivo, que se define en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="b76b5-170">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="b76b5-171">Especifica el grupo de recursos de destino de hello, que es `maven-plugin` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b76b5-171">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="b76b5-172">Si aún no existe, se creará el grupo de recursos de Hola durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="b76b5-172">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="b76b5-173">Especifica el nombre de destino de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b76b5-173">Specifies hello target name for your web app.</span></span> <span data-ttu-id="b76b5-174">En este ejemplo, es el nombre de destino de hello `maven-linux-app-${maven.build.timestamp}`, donde hello `${maven.build.timestamp}` se anexa un sufijo por este conflicto de tooavoid de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="b76b5-174">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="b76b5-175">(marca de tiempo de hello es opcional; puede especificar cualquier cadena única para el nombre de la aplicación hello).</span><span class="sxs-lookup"><span data-stu-id="b76b5-175">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="b76b5-176">Especifica la región de destino de hello, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="b76b5-176">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="b76b5-177">(Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)</span><span class="sxs-lookup"><span data-stu-id="b76b5-177">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<appSettings>` | <span data-ttu-id="b76b5-178">Especifica los valores únicos para Maven toouse al implementar su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="b76b5-178">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="b76b5-179">En este ejemplo, un `<property>` elemento contiene un par nombre/valor de los elementos secundarios que especifican Hola puerto para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b76b5-179">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b76b5-180">número de puerto de Hello configuración toochange hello en este ejemplo solo son necesarios cuando está cambiando el puerto de Hola de predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="b76b5-180">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

## <a name="build-and-deploy-your-container-tooazure"></a><span data-ttu-id="b76b5-181">Compilar e implementar su tooAzure de contenedor</span><span class="sxs-lookup"><span data-stu-id="b76b5-181">Build and deploy your container tooAzure</span></span>

<span data-ttu-id="b76b5-182">Una vez haya configurado todos los valores de hello en hello anteriores secciones de este artículo, está listo toodeploy tooAzure de su contenedor.</span><span class="sxs-lookup"><span data-stu-id="b76b5-182">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your container tooAzure.</span></span> <span data-ttu-id="b76b5-183">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="b76b5-183">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="b76b5-184">Desde el símbolo del sistema de Hola o ventana de terminal que estaba usando anteriormente, volver a generar archivo JAR de hello mediante Maven si ha realizado los cambios toohello *pom.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-184">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="b76b5-185">Implementar la tooAzure de aplicación web mediante el uso de Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-185">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="b76b5-186">Maven implementará su tooAzure de aplicación web; Si la aplicación web de hello aún no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="b76b5-186">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b76b5-187">Si región Hola que se especifica en hello `<region>` elemento de su *pom.xml* archivo no tiene suficientes servidores disponibles al iniciar la implementación, es posible que vea un toohello de error similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b76b5-187">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> <span data-ttu-id="b76b5-188">Si esto ocurre, puede especificar que otra región y vuelva a ejecutar Hola Maven comando toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b76b5-188">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="b76b5-189">Cuando se ha implementado la web, será capaz de toomanage mediante hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="b76b5-189">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="b76b5-190">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="b76b5-190">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="b76b5-192">Y Hola dirección URL para la aplicación web se mostrarán en hello **Introducción** para la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="b76b5-192">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de hello para la aplicación web][AP02]

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

## <a name="next-steps"></a><span data-ttu-id="b76b5-194">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b76b5-194">Next steps</span></span>

<span data-ttu-id="b76b5-195">Para obtener más información acerca de hello varias tecnologías descritas en este artículo, consulte Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="b76b5-195">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="b76b5-196">[Maven complemento para las aplicaciones Web de Azure]</span><span class="sxs-lookup"><span data-stu-id="b76b5-196">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="b76b5-197">Inicie sesión en tooAzure de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="b76b5-197">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="b76b5-198">Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="b76b5-198">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure App Service </span></span>](app-service-web-deploy-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="b76b5-199">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="b76b5-199">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="b76b5-200">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="b76b5-200">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="b76b5-201">[complemento de Docker para Maven]</span><span class="sxs-lookup"><span data-stu-id="b76b5-201">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[interfaz de línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal de Azure]: https://portal.azure.com/
[cliente de Docker]: https://www.docker.com/
[complemento de Docker para Maven]: https://github.com/spotify/docker-maven-plugin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[arranque Spring en Introducción a Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Maven complemento para las aplicaciones Web de Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin/AP02.png
