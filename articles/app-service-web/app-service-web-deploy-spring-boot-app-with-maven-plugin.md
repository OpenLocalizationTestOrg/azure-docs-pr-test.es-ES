---
title: "aaaHow toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera"
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
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a><span data-ttu-id="c09fd-103">Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera</span><span class="sxs-lookup"><span data-stu-id="c09fd-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app tooAzure</span></span>

<span data-ttu-id="c09fd-104">Hola [Maven complemento para las aplicaciones Web de Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Maven Apache](http://maven.apache.org/) proporciona una perfecta integración del servicio de aplicaciones de Azure en proyectos de Maven y optimiza el proceso de Hola para las aplicaciones web de los desarrolladores toodeploy tooAzure servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="c09fd-104">hello [Maven Plugin for Azure Web Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) for [Apache Maven](http://maven.apache.org/) provides seamless integration of Azure App Service into Maven projects, and streamlines hello process for developers toodeploy web apps tooAzure App Service.</span></span>

<span data-ttu-id="c09fd-105">Este artículo muestra cómo utilizar hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera servicios de aplicaciones de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-105">This article demonstrates using hello Maven Plugin for Azure Web Apps toodeploy a sample Spring Boot application tooAzure App Services.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c09fd-106">Hola Maven complemento para las aplicaciones Web de Azure está disponible actualmente como una vista previa.</span><span class="sxs-lookup"><span data-stu-id="c09fd-106">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="c09fd-107">Por ahora, se admite solo la publicación FTP, aunque características adicionales están planificadas para futuras Hola.</span><span class="sxs-lookup"><span data-stu-id="c09fd-107">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="c09fd-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c09fd-108">Prerequisites</span></span>

<span data-ttu-id="c09fd-109">En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="c09fd-109">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="c09fd-110">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="c09fd-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="c09fd-111">Hola [interfaz de línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="c09fd-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="c09fd-112">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="c09fd-112">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="c09fd-113">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="c09fd-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="c09fd-114">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="c09fd-114">A [Git] client.</span></span>

## <a name="clone-hello-sample-spring-boot-web-app"></a><span data-ttu-id="c09fd-115">Aplicación web de clon hello ejemplo arranque primavera</span><span class="sxs-lookup"><span data-stu-id="c09fd-115">Clone hello sample Spring Boot web app</span></span>

<span data-ttu-id="c09fd-116">En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="c09fd-116">In this section, you clone a completed Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="c09fd-117">Abra un símbolo del sistema o la ventana de terminal y cree un directorio local toohold la aplicación de arranque de primavera y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-117">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="c09fd-118">-- o --</span><span class="sxs-lookup"><span data-stu-id="c09fd-118">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="c09fd-119">Hola clon [Spring Introducción arranque] proyecto de ejemplo en el directorio Hola creado; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-119">Clone hello [Spring Boot Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. <span data-ttu-id="c09fd-120">Cambiar directorio toohello completado proyecto; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-120">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot/complete
   ```

1. <span data-ttu-id="c09fd-121">Compilar el archivo JAR de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-121">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c09fd-122">Cuándo se ha creado la aplicación web de hello, iniciar la aplicación web de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-122">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="c09fd-123">Probar la aplicación web de hello examinando tooit localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-123">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="c09fd-124">Por ejemplo, podría utilizar Hola siguiente comando si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="c09fd-124">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="c09fd-125">Debería ver el siguiente mensaje de Hola: **Greetings de arranque de primavera!**</span><span class="sxs-lookup"><span data-stu-id="c09fd-125">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="c09fd-126">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="c09fd-126">Create an Azure service principal</span></span>

<span data-ttu-id="c09fd-127">En esta sección, creará un Azure entidad de servicio que Hola usos de complemento de Maven al implementar su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-127">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="c09fd-128">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="c09fd-128">Open a command prompt.</span></span>

1. <span data-ttu-id="c09fd-129">Inicio de sesión en su cuenta de Azure mediante el uso de Hola CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="c09fd-129">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```shell
   az login
   ```
   <span data-ttu-id="c09fd-130">Siga Hola instrucciones toocomplete Hola inicio de sesión en proceso.</span><span class="sxs-lookup"><span data-stu-id="c09fd-130">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="c09fd-131">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="c09fd-131">Create an Azure service principal:</span></span>
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="c09fd-132">Donde `uuuuuuuu` es el nombre de usuario de Hola y `pppppppp` es contraseña Hola Hola principal de servicio.</span><span class="sxs-lookup"><span data-stu-id="c09fd-132">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="c09fd-133">Azure responde con JSON similar al siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="c09fd-133">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="c09fd-134">Utilizará valores de hello de esta respuesta JSON cuando configura hello Maven complemento toodeploy su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-134">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your web app tooAzure.</span></span> <span data-ttu-id="c09fd-135">Hola `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición, que son usado en este ejemplo se toomake toomap más fácil estos valores tootheir respectivos elementos cuando se configura el Maven `settings.xml` archivo Hola a continuación sección.</span><span class="sxs-lookup"><span data-stu-id="c09fd-135">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a><span data-ttu-id="c09fd-136">Configurar la entidad de seguridad de servicio de Azure de Maven toouse</span><span class="sxs-lookup"><span data-stu-id="c09fd-136">Configure Maven toouse your Azure service principal</span></span>

<span data-ttu-id="c09fd-137">En esta sección, utiliza valores de hello de la autenticación de hello tooconfigure principal de servicio de Azure que Maven usa al implementar su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-137">In this section, you use hello values from your Azure service principal tooconfigure hello authentication that Maven uses when deploying your web app tooAzure.</span></span>

1. <span data-ttu-id="c09fd-138">Abra su Maven `settings.xml` un archivo en un editor de texto; este archivo puede encontrarse en una ruta de acceso como hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="c09fd-138">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="c09fd-139">Agregar la configuración de entidad de seguridad de servicio de Azure desde la sección anterior de Hola de este tutorial toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-139">Add your Azure service principal settings from hello previous section of this tutorial toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="c09fd-140">Donde:</span><span class="sxs-lookup"><span data-stu-id="c09fd-140">Where:</span></span>
   <span data-ttu-id="c09fd-141">Elemento</span><span class="sxs-lookup"><span data-stu-id="c09fd-141">Element</span></span> | <span data-ttu-id="c09fd-142">Descripción</span><span class="sxs-lookup"><span data-stu-id="c09fd-142">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="c09fd-143">Especifica un nombre único que Maven use toolook su configuración de seguridad cuando se implementa la tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-143">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="c09fd-144">Contiene Hola `appId` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c09fd-144">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="c09fd-145">Contiene Hola `tenant` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c09fd-145">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="c09fd-146">Contiene Hola `password` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c09fd-146">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="c09fd-147">Define el entorno de nube de Azure de destino de hello, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-147">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="c09fd-148">(Una lista completa de los entornos de está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación)</span><span class="sxs-lookup"><span data-stu-id="c09fd-148">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="c09fd-149">Guarde y cierre hello *settings.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-149">Save and close hello *settings.xml* file.</span></span>

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a><span data-ttu-id="c09fd-150">OPCIONAL: Personalizar la pom.xml antes de implementar su tooAzure de aplicación web</span><span class="sxs-lookup"><span data-stu-id="c09fd-150">OPTIONAL: Customize your pom.xml before deploying your web app tooAzure</span></span>

<span data-ttu-id="c09fd-151">Abra hello `pom.xml` de archivos para la aplicación de arranque del muelle en un editor de texto y, a continuación, busque hello `<plugin>` (elemento) para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="c09fd-151">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="c09fd-152">Este elemento debe ser similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-152">This element should resemble hello following example:</span></span>

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
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

<span data-ttu-id="c09fd-153">Hay varios valores que se pueden modificar para hello Maven complemento y obtener una descripción detallada de cada uno de estos elementos está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación.</span><span class="sxs-lookup"><span data-stu-id="c09fd-153">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="c09fd-154">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-154">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="c09fd-155">Elemento</span><span class="sxs-lookup"><span data-stu-id="c09fd-155">Element</span></span> | <span data-ttu-id="c09fd-156">Descripción</span><span class="sxs-lookup"><span data-stu-id="c09fd-156">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="c09fd-157">Especifica la versión de Hola de hello [Maven complemento para las aplicaciones Web de Azure].</span><span class="sxs-lookup"><span data-stu-id="c09fd-157">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="c09fd-158">Debe comprobar la versión de Hola enumerada en hello [repositorio Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que utilizas Hola versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="c09fd-158">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="c09fd-159">Especifica la información de autenticación de Hola de Azure, que en este ejemplo contiene un `<serverId>` elemento que contiene `azure-auth`; Maven usa ese toolook valor valores de entidad de seguridad de servicio de Azure de hello en su Maven *settings.xml* archivo, que se define en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-159">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="c09fd-160">Especifica el grupo de recursos de destino de hello, que es `maven-plugin` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-160">Specifies hello target resource group, which is `maven-plugin` in this example.</span></span> <span data-ttu-id="c09fd-161">grupo de recursos de Hola se crea durante la implementación si aún no existe.</span><span class="sxs-lookup"><span data-stu-id="c09fd-161">hello resource group is created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="c09fd-162">Especifica el nombre de destino de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-162">Specifies hello target name for your web app.</span></span> <span data-ttu-id="c09fd-163">En este ejemplo, es el nombre de destino de hello `maven-web-app-${maven.build.timestamp}`, donde hello `${maven.build.timestamp}` se anexa un sufijo por este conflicto de tooavoid de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-163">In this example, hello target name is `maven-web-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="c09fd-164">(marca de tiempo de hello es opcional; puede especificar cualquier cadena única para el nombre de la aplicación hello).</span><span class="sxs-lookup"><span data-stu-id="c09fd-164">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="c09fd-165">Especifica la región de destino de hello, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="c09fd-165">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="c09fd-166">(Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)</span><span class="sxs-lookup"><span data-stu-id="c09fd-166">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<javaVersion>` | <span data-ttu-id="c09fd-167">Especifica la versión de tiempo de ejecución de Java de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-167">Specifies hello Java runtime version for your web app.</span></span> <span data-ttu-id="c09fd-168">(Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)</span><span class="sxs-lookup"><span data-stu-id="c09fd-168">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<deploymentType>` | <span data-ttu-id="c09fd-169">Especifica el tipo de implementación para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-169">Specifies deployment type for your web app.</span></span> <span data-ttu-id="c09fd-170">Por ahora, solo se admite `ftp`, aunque la compatibilidad con otros tipos de implementación está en la fase de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="c09fd-170">For now, only `ftp` is supported, although support for other deployment types is in development.</span></span>
`<resources>` | <span data-ttu-id="c09fd-171">Especifica los recursos y destinos que Maven usa al implementar su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-171">Specifies resources and target destinations which Maven uses when deploying your web app tooAzure.</span></span> <span data-ttu-id="c09fd-172">En este ejemplo, dos `<resource>` elementos especifican que Maven implementará el archivo JAR de Hola para su aplicación web y hello *web.config* archivo de proyecto de inicio de primavera de Hola.</span><span class="sxs-lookup"><span data-stu-id="c09fd-172">In this example, two `<resource>` elements specify that Maven will deploy hello JAR file for your web app and hello *web.config* file from hello Spring Boot project.</span></span>

## <a name="build-and-deploy-your-web-app-tooazure"></a><span data-ttu-id="c09fd-173">Compilar e implementar su tooAzure de aplicación web</span><span class="sxs-lookup"><span data-stu-id="c09fd-173">Build and deploy your web app tooAzure</span></span>

<span data-ttu-id="c09fd-174">Una vez haya configurado todos los valores de hello en hello anteriores secciones de este artículo, está listo toodeploy su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="c09fd-174">Once you have configured all of hello settings in hello preceding sections of this article, you are ready toodeploy your web app tooAzure.</span></span> <span data-ttu-id="c09fd-175">toodo por lo tanto, use Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="c09fd-175">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="c09fd-176">Desde el símbolo del sistema de Hola o ventana de terminal que estaba usando anteriormente, volver a generar archivo JAR de hello mediante Maven si ha realizado los cambios toohello *pom.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-176">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="c09fd-177">Implementar la tooAzure de aplicación web mediante el uso de Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="c09fd-177">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="c09fd-178">Maven implementará su tooAzure de aplicación web; Si la aplicación web de hello aún no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="c09fd-178">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

<span data-ttu-id="c09fd-179">Cuando se ha implementado la web, será capaz de toomanage mediante hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="c09fd-179">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="c09fd-180">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="c09fd-180">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="c09fd-182">Y Hola dirección URL para la aplicación web se mostrarán en hello **Introducción** para la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="c09fd-182">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c09fd-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c09fd-184">Next steps</span></span>

<span data-ttu-id="c09fd-185">Para obtener más información acerca de hello varias tecnologías descritas en este artículo, consulte Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="c09fd-185">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="c09fd-186">[Maven complemento para las aplicaciones Web de Azure]</span><span class="sxs-lookup"><span data-stu-id="c09fd-186">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="c09fd-187">Inicie sesión en tooAzure de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c09fd-187">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="c09fd-188">Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque del muelle en contenedores</span><span class="sxs-lookup"><span data-stu-id="c09fd-188">How toouse hello Maven Plugin for Azure Web Apps toodeploy a containerized Spring Boot app tooAzure</span></span>](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [<span data-ttu-id="c09fd-189">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c09fd-189">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="c09fd-190">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="c09fd-190">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

<!-- URL List -->

[interfaz de línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal de Azure]: https://portal.azure.com/
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Introducción arranque]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven complemento para las aplicaciones Web de Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
