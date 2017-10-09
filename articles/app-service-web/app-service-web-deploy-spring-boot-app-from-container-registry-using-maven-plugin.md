---
title: "aaaHow toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una aplicación de arranque del muelle en el registro de contenedor de Azure tooAzure servicio de aplicaciones"
description: "Este tutorial le guiará aunque Hola pasos toodeploy una aplicación de arranque del muelle en el registro de contenedor de Azure tooAzure tooAzure servicio de aplicaciones mediante el uso de un complemento de Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a><span data-ttu-id="793cb-103">Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una aplicación de arranque del muelle en el registro de contenedor de Azure tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="793cb-103">How toouse hello Maven Plugin for Azure Web Apps toodeploy a Spring Boot app in Azure Container Registry tooAzure App Service</span></span>

<span data-ttu-id="793cb-104">Hola  **[Spring Framework]**  es un marco de código abierto popular que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web.</span><span class="sxs-lookup"><span data-stu-id="793cb-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="793cb-105">Este tutorial utiliza una aplicación de ejemplo creada con [arranque primavera], un enfoque basado en la convención para el uso de primavera tooget a trabajar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="793cb-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="793cb-106">Este artículo demuestra cómo toodeploy una tooAzure de aplicación de arranque Spring de ejemplo del registro de contenedor y después usar Hola Maven complemento para aplicaciones Web de Azure toodeploy su tooAzure aplicación servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="793cb-106">This article demonstrates how toodeploy a sample Spring Boot application tooAzure Container Registry, and then use hello Maven Plugin for Azure Web Apps toodeploy your application tooAzure App Service.</span></span>

> [!NOTE]
>
> <span data-ttu-id="793cb-107">Hola Maven complemento para las aplicaciones Web de Azure está disponible actualmente como una vista previa.</span><span class="sxs-lookup"><span data-stu-id="793cb-107">hello Maven Plugin for Azure Web Apps is currently available as a preview.</span></span> <span data-ttu-id="793cb-108">Por ahora, se admite solo la publicación FTP, aunque características adicionales están planificadas para futuras Hola.</span><span class="sxs-lookup"><span data-stu-id="793cb-108">For now, only FTP publishing is supported, although additional features are planned for hello future.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="793cb-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="793cb-109">Prerequisites</span></span>

<span data-ttu-id="793cb-110">En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="793cb-110">In order toocomplete hello steps in this tutorial, you need toohave hello following prerequisites:</span></span>

* <span data-ttu-id="793cb-111">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="793cb-111">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="793cb-112">Hola [interfaz de línea de comandos (CLI) de Azure].</span><span class="sxs-lookup"><span data-stu-id="793cb-112">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="793cb-113">Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="793cb-113">An up-to-date [Java Development Kit (JDK)], version 1.7 or later.</span></span>
* <span data-ttu-id="793cb-114">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="793cb-114">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="793cb-115">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="793cb-115">A [Git] client.</span></span>
* <span data-ttu-id="793cb-116">Un [cliente de Docker].</span><span class="sxs-lookup"><span data-stu-id="793cb-116">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="793cb-117">Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.</span><span class="sxs-lookup"><span data-stu-id="793cb-117">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a><span data-ttu-id="793cb-118">Ejemplo de Hola a Clone Spring arranque en la aplicación web de Docker</span><span class="sxs-lookup"><span data-stu-id="793cb-118">Clone hello sample Spring Boot on Docker web app</span></span>

<span data-ttu-id="793cb-119">En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.</span><span class="sxs-lookup"><span data-stu-id="793cb-119">In this section, you clone a containerized Spring Boot application and test it locally.</span></span>

1. <span data-ttu-id="793cb-120">Abra un símbolo del sistema o la ventana de terminal y cree un directorio local toohold la aplicación de arranque de primavera y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-120">Open a command prompt or terminal window and create a local directory toohold your Spring Boot application, and change toothat directory; for example:</span></span>
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="793cb-121">-- o --</span><span class="sxs-lookup"><span data-stu-id="793cb-121">-- or --</span></span>
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="793cb-122">Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio Hola creado; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-122">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory you created; for example:</span></span>
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. <span data-ttu-id="793cb-123">Cambiar directorio toohello completado proyecto; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-123">Change directory toohello completed project; for example:</span></span>
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. <span data-ttu-id="793cb-124">Compilar el archivo JAR de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-124">Build hello JAR file using Maven; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="793cb-125">Cuándo se ha creado la aplicación web de hello, iniciar la aplicación web de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-125">When hello web app has been created, start hello web app using Maven; for example:</span></span>
   ```shell
   mvn spring-boot:run
   ```

1. <span data-ttu-id="793cb-126">Probar la aplicación web de hello examinando tooit localmente mediante un explorador web.</span><span class="sxs-lookup"><span data-stu-id="793cb-126">Test hello web app by browsing tooit locally using a web browser.</span></span> <span data-ttu-id="793cb-127">Por ejemplo, podría utilizar Hola siguiente comando si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="793cb-127">For example, you could use hello following command if you have curl available:</span></span>
   ```shell
   curl http://localhost:8080
   ```

1. <span data-ttu-id="793cb-128">Debería ver el siguiente mensaje de Hola: **Docker Hola a todos**</span><span class="sxs-lookup"><span data-stu-id="793cb-128">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-service-principal"></a><span data-ttu-id="793cb-130">Creación de una entidad de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="793cb-130">Create an Azure service principal</span></span>

<span data-ttu-id="793cb-131">En esta sección, creará un Azure entidad de servicio que Hola usos de complemento de Maven al implementar su tooAzure de contenedor.</span><span class="sxs-lookup"><span data-stu-id="793cb-131">In this section, you create an Azure service principal that hello Maven plugin uses when deploying your container tooAzure.</span></span>

1. <span data-ttu-id="793cb-132">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="793cb-132">Open a command prompt.</span></span>

1. <span data-ttu-id="793cb-133">Inicio de sesión en su cuenta de Azure mediante el uso de Hola CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="793cb-133">Sign into your Azure account by using hello Azure CLI:</span></span>
   ```azurecli
   az login
   ```
   <span data-ttu-id="793cb-134">Siga Hola instrucciones toocomplete Hola inicio de sesión en proceso.</span><span class="sxs-lookup"><span data-stu-id="793cb-134">Follow hello instructions toocomplete hello sign-in process.</span></span>

1. <span data-ttu-id="793cb-135">Cree una entidad de servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="793cb-135">Create an Azure service principal:</span></span>
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   <span data-ttu-id="793cb-136">Donde `uuuuuuuu` es el nombre de usuario de Hola y `pppppppp` es contraseña Hola Hola principal de servicio.</span><span class="sxs-lookup"><span data-stu-id="793cb-136">Where `uuuuuuuu` is hello user name and `pppppppp` is hello password for hello service principal.</span></span>

1. <span data-ttu-id="793cb-137">Azure responde con JSON similar al siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="793cb-137">Azure responds with JSON that resembles hello following example:</span></span>
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
   > <span data-ttu-id="793cb-138">Utilizará valores de hello de esta respuesta JSON cuando configura hello Maven complemento toodeploy tooAzure de su contenedor.</span><span class="sxs-lookup"><span data-stu-id="793cb-138">You will use hello values from this JSON response when you configure hello Maven plugin toodeploy your container tooAzure.</span></span> <span data-ttu-id="793cb-139">Hola `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición, que son usado en este ejemplo se toomake toomap más fácil estos valores tootheir respectivos elementos cuando se configura el Maven `settings.xml` archivo Hola a continuación sección.</span><span class="sxs-lookup"><span data-stu-id="793cb-139">hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, and `tttttttt` are placeholder values, which are used in this example toomake it easier toomap these values tootheir respective elements when you configure your Maven `settings.xml` file in hello next section.</span></span>
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="793cb-140">Crear un registro de contenedor de Azure mediante Hola CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="793cb-140">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="793cb-141">Abra el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="793cb-141">Open a command prompt.</span></span>

1. <span data-ttu-id="793cb-142">Inicie sesión en tooyour cuenta de Azure:</span><span class="sxs-lookup"><span data-stu-id="793cb-142">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="793cb-143">Crear un grupo de recursos para hello recursos de Azure que usará en este artículo:</span><span class="sxs-lookup"><span data-stu-id="793cb-143">Create a resource group for hello Azure resources you will use in this article:</span></span>
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   <span data-ttu-id="793cb-144">Reemplace `wingtiptoysresources` en este ejemplo por un nombre único para el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="793cb-144">Replace `wingtiptoysresources` in this example with a unique name for your resource group.</span></span>

1. <span data-ttu-id="793cb-145">Crear un registro de contenedor de Azure privada en grupo de recursos de hello para la aplicación de arranque de primavera:</span><span class="sxs-lookup"><span data-stu-id="793cb-145">Create a private Azure container registry in hello resource group for your Spring Boot app:</span></span> 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   <span data-ttu-id="793cb-146">Reemplace `wingtiptoysregistry` en este ejemplo por un nombre único para el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="793cb-146">Replace `wingtiptoysregistry` in this example with a unique name for your container registry.</span></span>

1. <span data-ttu-id="793cb-147">Recuperar la contraseña de hello para el registro de contenedor:</span><span class="sxs-lookup"><span data-stu-id="793cb-147">Retrieve hello password for your container registry:</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   <span data-ttu-id="793cb-148">Azure responderá con la contraseña; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-148">Azure will respond with your password; for example:</span></span>
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a><span data-ttu-id="793cb-149">Agregar el registro de contenedor de Azure y la configuración de Maven de tooyour principal de servicio de Azure</span><span class="sxs-lookup"><span data-stu-id="793cb-149">Add your Azure container registry and Azure service principal tooyour Maven settings</span></span>

1. <span data-ttu-id="793cb-150">Abra su Maven `settings.xml` un archivo en un editor de texto; este archivo puede encontrarse en una ruta de acceso como hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="793cb-150">Open your Maven `settings.xml` file in a text editor; this file might be in a path like hello following examples:</span></span>
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. <span data-ttu-id="793cb-151">Agregar la configuración de acceso del registro de contenedor de Azure desde la sección anterior de Hola de este artículo toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-151">Add your Azure Container Registry access settings from hello previous section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   <span data-ttu-id="793cb-152">Donde:</span><span class="sxs-lookup"><span data-stu-id="793cb-152">Where:</span></span>
   <span data-ttu-id="793cb-153">Elemento</span><span class="sxs-lookup"><span data-stu-id="793cb-153">Element</span></span> | <span data-ttu-id="793cb-154">Descripción</span><span class="sxs-lookup"><span data-stu-id="793cb-154">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="793cb-155">Contiene el nombre de Hola de seguridad del registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="793cb-155">Contains hello name of your private Azure container registry.</span></span>
   `<username>` | <span data-ttu-id="793cb-156">Contiene el nombre de Hola de seguridad del registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="793cb-156">Contains hello name of your private Azure container registry.</span></span>
   `<password>` | <span data-ttu-id="793cb-157">Contiene la contraseña de hello que recuperó en la sección anterior de Hola de este artículo.</span><span class="sxs-lookup"><span data-stu-id="793cb-157">Contains hello password you retrieved in hello previous section of this article.</span></span>

1. <span data-ttu-id="793cb-158">Agregar la configuración de entidad de seguridad de servicio de Azure de una sección anterior de este artículo toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-158">Add your Azure service principal settings from an earlier section of this article toohello `<servers>` collection in hello *settings.xml* file; for example:</span></span>

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
   <span data-ttu-id="793cb-159">Donde:</span><span class="sxs-lookup"><span data-stu-id="793cb-159">Where:</span></span>
   <span data-ttu-id="793cb-160">Elemento</span><span class="sxs-lookup"><span data-stu-id="793cb-160">Element</span></span> | <span data-ttu-id="793cb-161">Descripción</span><span class="sxs-lookup"><span data-stu-id="793cb-161">Description</span></span>
   ---|---|---
   `<id>` | <span data-ttu-id="793cb-162">Especifica un nombre único que Maven use toolook su configuración de seguridad cuando se implementa la tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="793cb-162">Specifies a unique name which Maven uses toolook up your security settings when you deploy your web app tooAzure.</span></span>
   `<client>` | <span data-ttu-id="793cb-163">Contiene Hola `appId` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="793cb-163">Contains hello `appId` value from your service principal.</span></span>
   `<tenant>` | <span data-ttu-id="793cb-164">Contiene Hola `tenant` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="793cb-164">Contains hello `tenant` value from your service principal.</span></span>
   `<key>` | <span data-ttu-id="793cb-165">Contiene Hola `password` valor de la entidad de seguridad de servicio.</span><span class="sxs-lookup"><span data-stu-id="793cb-165">Contains hello `password` value from your service principal.</span></span>
   `<environment>` | <span data-ttu-id="793cb-166">Define el entorno de nube de Azure de destino de hello, que es `AZURE` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="793cb-166">Defines hello target Azure cloud environment, which is `AZURE` in this example.</span></span> <span data-ttu-id="793cb-167">(Una lista completa de los entornos de está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación)</span><span class="sxs-lookup"><span data-stu-id="793cb-167">(A full list of environments is available in hello [Maven Plugin for Azure Web Apps] documentation)</span></span>

1. <span data-ttu-id="793cb-168">Guarde y cierre hello *settings.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="793cb-168">Save and close hello *settings.xml* file.</span></span>

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a><span data-ttu-id="793cb-169">Generar a su Docker imagen de contenedor e insertarlo tooyour registro de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="793cb-169">Build your Docker container image and push it tooyour Azure container registry</span></span>

1. <span data-ttu-id="793cb-170">Navegue toohello completado el directorio del proyecto para la aplicación de arranque de primavera (p. ej. "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), abra hello y *pom.xml* archivo con una editor de texto.</span><span class="sxs-lookup"><span data-stu-id="793cb-170">Navigate toohello completed project directory for your Spring Boot application, (e.g. "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="793cb-171">Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-171">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry from hello previous section of this tutorial; for example:</span></span>

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   <span data-ttu-id="793cb-172">Donde:</span><span class="sxs-lookup"><span data-stu-id="793cb-172">Where:</span></span>
   <span data-ttu-id="793cb-173">Elemento</span><span class="sxs-lookup"><span data-stu-id="793cb-173">Element</span></span> | <span data-ttu-id="793cb-174">Descripción</span><span class="sxs-lookup"><span data-stu-id="793cb-174">Description</span></span>
   ---|---|---
   `<azure.containerRegistry>` | <span data-ttu-id="793cb-175">Especifica el nombre de Hola de seguridad del registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="793cb-175">Specifies hello name of your private Azure container registry.</span></span>
   `<docker.image.prefix>` | <span data-ttu-id="793cb-176">Especifica la URL Hola de seguridad del registro de contenedor de Azure privada, que se crea agregando ". azurecr.io" nombre de toohello de seguridad del registro de contenedor privado.</span><span class="sxs-lookup"><span data-stu-id="793cb-176">Specifies hello URL of your private Azure container registry, which is derived by appending ".azurecr.io" toohello name of your private container registry.</span></span>

1. <span data-ttu-id="793cb-177">Compruebe que `<plugin>` para hello Docker complemento en su *pom.xml* archivo contiene propiedades correctas de Hola para hello inicio de sesión del registro y la dirección del nombre del servidor del paso anterior de hello en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="793cb-177">Verify that `<plugin>` for hello Docker plugin in your *pom.xml* file contains hello correct properties for hello login server address and registry name from hello previous step in this tutorial.</span></span> <span data-ttu-id="793cb-178">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-178">For example:</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   <span data-ttu-id="793cb-179">Donde:</span><span class="sxs-lookup"><span data-stu-id="793cb-179">Where:</span></span>
   <span data-ttu-id="793cb-180">Elemento</span><span class="sxs-lookup"><span data-stu-id="793cb-180">Element</span></span> | <span data-ttu-id="793cb-181">Descripción</span><span class="sxs-lookup"><span data-stu-id="793cb-181">Description</span></span>
   ---|---|---
   `<serverId>` | <span data-ttu-id="793cb-182">Especifica la propiedad de Hola que contiene el nombre de seguridad del registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="793cb-182">Specifies hello property which contains name of your private Azure container registry.</span></span>
   `<registryUrl>` | <span data-ttu-id="793cb-183">Especifica la propiedad de Hola que contiene la dirección URL de Hola de seguridad del registro de contenedor de Azure privada.</span><span class="sxs-lookup"><span data-stu-id="793cb-183">Specifies hello property which contains hello URL of your private Azure container registry.</span></span>

1. <span data-ttu-id="793cb-184">Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera y ejecute hello tras la aplicación de comando toorebuild Hola e inserte Hola contenedor tooyour del registro de contenedor de Azure:</span><span class="sxs-lookup"><span data-stu-id="793cb-184">Navigate toohello completed project directory for your Spring Boot application and run hello following command toorebuild hello application and push hello container tooyour Azure container registry:</span></span>

   ```
   mvn package docker:build -DpushImage 
   ```

1. <span data-ttu-id="793cb-185">OPCIONAL: Examinar toohello [portal de Azure] y compruebe que hay una imagen de contenedor de Docker denominada **gs-spring-arranque-docker** en el registro de contenedor.</span><span class="sxs-lookup"><span data-stu-id="793cb-185">OPTIONAL: Browse toohello [Azure portal] and verify that there is Docker container image named **gs-spring-boot-docker** in your container registry.</span></span>

   ![Comprobar contenedor en Azure Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a><span data-ttu-id="793cb-187">Personalizar su pom.xml, a continuación, compilar e implementar su tooAzure de contenedor</span><span class="sxs-lookup"><span data-stu-id="793cb-187">Customize your pom.xml, then build and deploy your container tooAzure</span></span>

<span data-ttu-id="793cb-188">Abra hello `pom.xml` de archivos para la aplicación de arranque del muelle en un editor de texto y, a continuación, busque hello `<plugin>` (elemento) para `azure-webapp-maven-plugin`.</span><span class="sxs-lookup"><span data-stu-id="793cb-188">Open hello `pom.xml` file for your Spring Boot application in a text editor, and then locate hello `<plugin>` element for `azure-webapp-maven-plugin`.</span></span> <span data-ttu-id="793cb-189">Este elemento debe ser similar a Hola siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-189">This element should resemble hello following example:</span></span>

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
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

<span data-ttu-id="793cb-190">Hay varios valores que se pueden modificar para hello Maven complemento y obtener una descripción detallada de cada uno de estos elementos está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación.</span><span class="sxs-lookup"><span data-stu-id="793cb-190">There are several values that you can modify for hello Maven plugin, and a detailed description for each of these elements is available in hello [Maven Plugin for Azure Web Apps] documentation.</span></span> <span data-ttu-id="793cb-191">Dicho esto, hay varios valores que merece la pena destacar en este artículo:</span><span class="sxs-lookup"><span data-stu-id="793cb-191">That being said, there are several values that are worth highlighting in this article:</span></span>

<span data-ttu-id="793cb-192">Elemento</span><span class="sxs-lookup"><span data-stu-id="793cb-192">Element</span></span> | <span data-ttu-id="793cb-193">Descripción</span><span class="sxs-lookup"><span data-stu-id="793cb-193">Description</span></span>
---|---|---
`<version>` | <span data-ttu-id="793cb-194">Especifica la versión de Hola de hello [Maven complemento para las aplicaciones Web de Azure].</span><span class="sxs-lookup"><span data-stu-id="793cb-194">Specifies hello version of hello [Maven Plugin for Azure Web Apps].</span></span> <span data-ttu-id="793cb-195">Debe comprobar la versión de Hola enumerada en hello [repositorio Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que utilizas Hola versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="793cb-195">You should check hello version listed in hello [Maven Central Respository](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure that you are using hello latest version.</span></span>
`<authentication>` | <span data-ttu-id="793cb-196">Especifica la información de autenticación de Hola de Azure, que en este ejemplo contiene un `<serverId>` elemento que contiene `azure-auth`; Maven usa ese toolook valor valores de entidad de seguridad de servicio de Azure de hello en su Maven *settings.xml* archivo, que se define en una sección anterior de este artículo.</span><span class="sxs-lookup"><span data-stu-id="793cb-196">Specifies hello authentication information for Azure, which in this example contains a `<serverId>` element that contains `azure-auth`; Maven uses that value toolook up hello Azure service principal values in your Maven *settings.xml* file, which you defined in an earlier section of this article.</span></span>
`<resourceGroup>` | <span data-ttu-id="793cb-197">Especifica el grupo de recursos de destino de hello, que es `wingtiptoysresources` en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="793cb-197">Specifies hello target resource group, which is `wingtiptoysresources` in this example.</span></span> <span data-ttu-id="793cb-198">Si aún no existe, se creará el grupo de recursos de Hola durante la implementación.</span><span class="sxs-lookup"><span data-stu-id="793cb-198">hello resource group will be created during deployment if it does not already exist.</span></span>
`<appName>` | <span data-ttu-id="793cb-199">Especifica el nombre de destino de hello para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="793cb-199">Specifies hello target name for your web app.</span></span> <span data-ttu-id="793cb-200">En este ejemplo, es el nombre de destino de hello `maven-linux-app-${maven.build.timestamp}`, donde hello `${maven.build.timestamp}` se anexa un sufijo por este conflicto de tooavoid de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="793cb-200">In this example, hello target name is `maven-linux-app-${maven.build.timestamp}`, where hello `${maven.build.timestamp}` suffix is appended in this example tooavoid conflict.</span></span> <span data-ttu-id="793cb-201">(marca de tiempo de hello es opcional; puede especificar cualquier cadena única para el nombre de la aplicación hello).</span><span class="sxs-lookup"><span data-stu-id="793cb-201">(hello timestamp is optional; you can specify any unique string for hello app name.)</span></span>
`<region>` | <span data-ttu-id="793cb-202">Especifica la región de destino de hello, que en este ejemplo es `westus`.</span><span class="sxs-lookup"><span data-stu-id="793cb-202">Specifies hello target region, which in this example is `westus`.</span></span> <span data-ttu-id="793cb-203">(Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)</span><span class="sxs-lookup"><span data-stu-id="793cb-203">(A full list is in hello [Maven Plugin for Azure Web Apps] documentation.)</span></span>
`<containerSettings>` | <span data-ttu-id="793cb-204">Especifica las propiedades de Hola que contienen el nombre de Hola y la dirección URL del contenedor.</span><span class="sxs-lookup"><span data-stu-id="793cb-204">Specifies hello properties which contain hello name and URL of your container.</span></span>
`<appSettings>` | <span data-ttu-id="793cb-205">Especifica los valores únicos para Maven toouse al implementar su tooAzure de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="793cb-205">Specifies any unique settings for Maven toouse when deploying your web app tooAzure.</span></span> <span data-ttu-id="793cb-206">En este ejemplo, un `<property>` elemento contiene un par nombre/valor de los elementos secundarios que especifican Hola puerto para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="793cb-206">In this example, a `<property>` element contains a name/value pair of child elements that specify hello port for your app.</span></span>

> [!NOTE]
>
> <span data-ttu-id="793cb-207">número de puerto de Hello configuración toochange hello en este ejemplo solo son necesarios cuando está cambiando el puerto de Hola de predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="793cb-207">hello settings toochange hello port number in this example are only necessary when you are changing hello port from hello default.</span></span>
>

1. <span data-ttu-id="793cb-208">Desde el símbolo del sistema de Hola o ventana de terminal que estaba usando anteriormente, volver a generar archivo JAR de hello mediante Maven si ha realizado los cambios toohello *pom.xml* archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-208">From hello command prompt or terminal window that you were using earlier, rebuild hello JAR file using Maven if you made any changes toohello *pom.xml* file; for example:</span></span>
   ```shell
   mvn clean package
   ```

1. <span data-ttu-id="793cb-209">Implementar la tooAzure de aplicación web mediante el uso de Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-209">Deploy your web app tooAzure by using Maven; for example:</span></span>
   ```shell
   mvn azure-webapp:deploy
   ```

<span data-ttu-id="793cb-210">Maven implementará su tooAzure de aplicación web; Si la aplicación web de hello aún no existe, se creará.</span><span class="sxs-lookup"><span data-stu-id="793cb-210">Maven will deploy your web app tooAzure; if hello web app does not already exist, it will be created.</span></span>

> [!NOTE]
>
> <span data-ttu-id="793cb-211">Si región Hola que se especifica en hello `<region>` elemento de su *pom.xml* archivo no tiene suficientes servidores disponibles al iniciar la implementación, es posible que vea un toohello de error similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="793cb-211">If hello region which you specify in hello `<region>` element of your *pom.xml* file does not have enough servers available when you start your deployment, you might see an error similar toohello following example:</span></span>
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
> <span data-ttu-id="793cb-212">Si esto ocurre, puede especificar que otra región y vuelva a ejecutar Hola Maven comando toodeploy la aplicación.</span><span class="sxs-lookup"><span data-stu-id="793cb-212">If this happens, you can specify another region and re-run hello Maven command toodeploy your application.</span></span>
>
>

<span data-ttu-id="793cb-213">Cuando se ha implementado la web, será capaz de toomanage mediante hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="793cb-213">When your web has been deployed, you will be able toomanage it by using hello [Azure portal].</span></span>

* <span data-ttu-id="793cb-214">La aplicación web aparecerá en **App Services**:</span><span class="sxs-lookup"><span data-stu-id="793cb-214">Your web app will be listed in **App Services**:</span></span>

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* <span data-ttu-id="793cb-216">Y Hola dirección URL para la aplicación web se mostrarán en hello **Introducción** para la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="793cb-216">And hello URL for your web app will be listed in hello **Overview** for your web app:</span></span>

   ![Determinar la dirección URL de hello para la aplicación web][AP02]

## <a name="next-steps"></a><span data-ttu-id="793cb-218">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="793cb-218">Next steps</span></span>

<span data-ttu-id="793cb-219">Para obtener más información acerca de hello varias tecnologías descritas en este artículo, consulte Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="793cb-219">For more information about hello various technologies discussed in this article, see hello following articles:</span></span>

* <span data-ttu-id="793cb-220">[Maven complemento para las aplicaciones Web de Azure]</span><span class="sxs-lookup"><span data-stu-id="793cb-220">[Maven Plugin for Azure Web Apps]</span></span>

* [<span data-ttu-id="793cb-221">Inicie sesión en tooAzure de hello CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="793cb-221">Log in tooAzure from hello Azure CLI</span></span>](/azure/xplat-cli-connect)

* [<span data-ttu-id="793cb-222">Creación de una entidad de servicio de Azure con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="793cb-222">Create an Azure service principal with Azure CLI 2.0</span></span>](/cli/azure/create-an-azure-service-principal-azure-cli)

* [<span data-ttu-id="793cb-223">Referencia de configuración de Maven</span><span class="sxs-lookup"><span data-stu-id="793cb-223">Maven Settings Reference</span></span>](https://maven.apache.org/settings.html)

* <span data-ttu-id="793cb-224">[Complemento Docker para Maven]</span><span class="sxs-lookup"><span data-stu-id="793cb-224">[Docker plugin for Maven]</span></span>

<!-- URL List -->

[interfaz de línea de comandos (CLI) de Azure]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portal de Azure]: https://portal.azure.com/
[Maven complemento para las aplicaciones Web de Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[cliente de Docker]: https://www.docker.com/
[Complemento Docker para Maven]: https://github.com/spotify/docker-maven-plugin
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[arranque primavera]: http://projects.spring.io/spring-boot/
[arranque Spring en Introducción a Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
