---
title: "Implementación de una aplicación de Spring Boot en Azure App Service | Microsoft Docs"
description: "Este tutorial guiará a los desarrolladores a través de los pasos necesarios para implementar una aplicación web inicial de Spring Boot en Azure App Service."
services: app-service\web
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
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 0c388862d927a1492745832225c686670c071f86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-to-the-azure-app-service"></a><span data-ttu-id="9a808-103">Implementación de una aplicación de Spring Boot en Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9a808-103">Deploy a Spring Boot Application to the Azure App Service</span></span>

<span data-ttu-id="9a808-104">**[Spring Framework]** es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones a nivel empresarial. Uno de los proyectos más populares basados en esta plataforma es [Spring Boot], que ofrece un método simplificado para crear aplicaciones Java independientes.</span><span class="sxs-lookup"><span data-stu-id="9a808-104">The **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of the more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="9a808-105">Este tutorial le guiará a través de la creación de una aplicación web inicial de Spring Boot y su implementación en [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="9a808-105">This tutorial will walk you though creating the sample Spring Boot Getting Started web app and deploying it to [Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9a808-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9a808-106">Prerequisites</span></span>

<span data-ttu-id="9a808-107">Para poder realizar los pasos de este tutorial, necesitará tener lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a808-107">In order to complete the steps in this tutorial, you need to have the following:</span></span>

* <span data-ttu-id="9a808-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="9a808-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="9a808-109">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="9a808-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="9a808-110">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="9a808-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="9a808-111">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="9a808-111">A [Git] client.</span></span>

## <a name="create-the-spring-boot-getting-started-web-app"></a><span data-ttu-id="9a808-112">Creación de la aplicación web inicial de Spring Boot</span><span class="sxs-lookup"><span data-stu-id="9a808-112">Create the Spring Boot Getting Started web app</span></span>

<span data-ttu-id="9a808-113">Los siguientes pasos le guiarán por las fases necesarias para crear una aplicación web de Spring Boot sencilla y probarla de forma local.</span><span class="sxs-lookup"><span data-stu-id="9a808-113">The following steps will walk you through the steps that are required to create a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="9a808-114">Abra el símbolo del sistema, cree un directorio local para alojar la aplicación y cambie a dicho directorio, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-114">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="9a808-115">-- o --</span><span class="sxs-lookup"><span data-stu-id="9a808-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="9a808-116">Clone el proyecto de ejemplo [inicial de Spring Boot] en el directorio recién creado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-116">Clone the [Spring Boot Getting Started] sample project into the directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="9a808-117">Cambie de directorio al del proyecto finalizado, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-117">Change directory to the completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="9a808-118">Compile el archivo JAR con Maven, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-118">Build the JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="9a808-119">Una vez creada la aplicación web, cambie el directorio al del archivo JAR e inicie la aplicación web, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-119">Once the web app has been created, change directory to the JAR file and start the web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="9a808-120">Compruebe la aplicación web. Para ello, vaya a http://localhost:8080 con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="9a808-120">Test the web app by browsing to http://localhost:8080 using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="9a808-121">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="9a808-121">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="9a808-123">Creación de una aplicación web de Azure para usarla con Java</span><span class="sxs-lookup"><span data-stu-id="9a808-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="9a808-124">Los siguientes pasos le guiarán por las diferentes fases de creación de una aplicación web de Azure, de ajuste de la configuración necesaria para Java y de configuración de las credenciales de FTP.</span><span class="sxs-lookup"><span data-stu-id="9a808-124">The following steps will walk you through the steps to create an Azure Web App, configure the required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="9a808-125">Vaya a [Azure Portal] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="9a808-125">Browse to the [Azure portal] and log in.</span></span>

1. <span data-ttu-id="9a808-126">Una vez que haya iniciado sesión en la cuenta de Azure Portal, haga clic en el icono de menú de **App Services**:</span><span class="sxs-lookup"><span data-stu-id="9a808-126">Once you have logged into your account on the Azure portal, click the menu icon for **App Services**:</span></span>
   
   ![Portal de Azure][AZ01]

1. <span data-ttu-id="9a808-128">Cuando aparezca la página **App Services**, haga clic en **+ Agregar** para crear un nuevo elemento de App Service.</span><span class="sxs-lookup"><span data-stu-id="9a808-128">When the **App Services** page is displayed, click **+ Add** to create a new App Service.</span></span>

   ![Creación de un elemento App Service][AZ02]

1. <span data-ttu-id="9a808-130">Cuando aparezca la lista de plantillas de aplicaciones web, haga clic en el vínculo de la aplicación web básica de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9a808-130">When the list of web app templates is displayed, click the link for the basic Microsoft Web App.</span></span>

   ![Plantillas de aplicaciones web][AZ03]

1. <span data-ttu-id="9a808-132">Cuando aparezca la página de información de plantillas de aplicaciones web, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a808-132">When the information page for the Web App template is displayed, click **Create**.</span></span>

   ![Crear aplicación web][AZ04]

1. <span data-ttu-id="9a808-134">Proporcione un nombre único para la aplicación web y especifique cualquier configuración adicional. A continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="9a808-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Creación de configuración de aplicaciones web][AZ05]

1. <span data-ttu-id="9a808-136">Una vez creada la aplicación web, haga clic en el icono de menú de **App Services** y, a continuación, haga clic en la aplicación web recién creada:</span><span class="sxs-lookup"><span data-stu-id="9a808-136">Once your web app has been created, click the menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lista de aplicaciones web][AZ06]

1. <span data-ttu-id="9a808-138">Cuando aparezca la aplicación web, especifique la versión de Java. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a808-138">When your web app is displayed, specify the Java version by using the following steps:</span></span>

   <span data-ttu-id="9a808-139">a.</span><span class="sxs-lookup"><span data-stu-id="9a808-139">a.</span></span> <span data-ttu-id="9a808-140">Haga clic en el elemento de menú **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="9a808-140">Click the **Application Settings** menu item.</span></span>

   <span data-ttu-id="9a808-141">b.</span><span class="sxs-lookup"><span data-stu-id="9a808-141">b.</span></span> <span data-ttu-id="9a808-142">Seleccione **Java 8** como versión de Java.</span><span class="sxs-lookup"><span data-stu-id="9a808-142">Choose **Java 8** for the Java version.</span></span>

   <span data-ttu-id="9a808-143">c.</span><span class="sxs-lookup"><span data-stu-id="9a808-143">c.</span></span> <span data-ttu-id="9a808-144">Seleccione **Más reciente** como versión secundaria de Java.</span><span class="sxs-lookup"><span data-stu-id="9a808-144">Choose **Newest** for the minor Java version.</span></span>

   <span data-ttu-id="9a808-145">d.</span><span class="sxs-lookup"><span data-stu-id="9a808-145">d.</span></span> <span data-ttu-id="9a808-146">Seleccione **Newest Tomcat 8.5** como contenedor web.</span><span class="sxs-lookup"><span data-stu-id="9a808-146">Choose **Newest Tomcat 8.5** for the web container.</span></span> <span data-ttu-id="9a808-147">(Este contenedor en realidad no se usará. Azure usará el contenedor de la aplicación de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="9a808-147">(This container will not actually be used; Azure will use the container from your Spring Boot application.)</span></span>

   <span data-ttu-id="9a808-148">e.</span><span class="sxs-lookup"><span data-stu-id="9a808-148">e.</span></span> <span data-ttu-id="9a808-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a808-149">Click **Save**.</span></span>

   ![Configuración de la aplicación][AZ07]

1. <span data-ttu-id="9a808-151">Especifique las credenciales de implementación de FTP. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a808-151">Specify your FTP deployment credentials by using the following steps:</span></span>

   <span data-ttu-id="9a808-152">a.</span><span class="sxs-lookup"><span data-stu-id="9a808-152">a.</span></span> <span data-ttu-id="9a808-153">Haga clic en el elemento de menú **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="9a808-153">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="9a808-154">b.</span><span class="sxs-lookup"><span data-stu-id="9a808-154">b.</span></span> <span data-ttu-id="9a808-155">Especifique el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="9a808-155">Specify your username and password.</span></span>

   <span data-ttu-id="9a808-156">c.</span><span class="sxs-lookup"><span data-stu-id="9a808-156">c.</span></span> <span data-ttu-id="9a808-157">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9a808-157">Click **Save**.</span></span>

   ![Especificación de credenciales de implementación][AZ08]

1. <span data-ttu-id="9a808-159">Recupere la información de conexión del FTP. Para ello, siga los siguientes pasos:</span><span class="sxs-lookup"><span data-stu-id="9a808-159">Retrieve your FTP connection information by using the following steps:</span></span>

   <span data-ttu-id="9a808-160">a.</span><span class="sxs-lookup"><span data-stu-id="9a808-160">a.</span></span> <span data-ttu-id="9a808-161">Haga clic en el elemento de menú **Credenciales de implementación**.</span><span class="sxs-lookup"><span data-stu-id="9a808-161">Click the **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="9a808-162">b.</span><span class="sxs-lookup"><span data-stu-id="9a808-162">b.</span></span> <span data-ttu-id="9a808-163">Copie el nombre de usuario y la URL del FTP completos, y guárdelos para la siguiente sección del tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a808-163">Copy your full FTP username and URL and save them for the next section of this tutorial.</span></span>

   ![URL y credenciales de FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-to-azure"></a><span data-ttu-id="9a808-165">Implementación de la aplicación web de Spring Boot en Azure</span><span class="sxs-lookup"><span data-stu-id="9a808-165">Deploy your Spring Boot web app to Azure</span></span>

<span data-ttu-id="9a808-166">Los siguientes pasos le guiarán por las fases necesarias para implementar la aplicación web de Spring Boot en Azure.</span><span class="sxs-lookup"><span data-stu-id="9a808-166">The following steps will walk you through the steps to deploy your Spring Boot web app to Azure.</span></span>

1. <span data-ttu-id="9a808-167">Abra un editor de texto, como el Bloc de notas de Windows, y pegue el siguiente texto en un nuevo documento. A continuación, guarde el archivo como *web.config*:</span><span class="sxs-lookup"><span data-stu-id="9a808-167">Open a text editor such as Windows Notepad and paste the following text into a new document, then save the file as *web.config*:</span></span>
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. <span data-ttu-id="9a808-168">Después de guardar el archivo *web.config* en el sistema, conéctese a la aplicación web a través de FTP con la URL, el nombre de usuario y la contraseña de la sección anterior de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9a808-168">After you have saved the *web.config* file to your system, connect to your web app via FTP using the URL, username, and password from the preceding section of this tutorial.</span></span> <span data-ttu-id="9a808-169">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="9a808-170">Cambie el directorio remoto a la carpeta raíz de la aplicación web (que se encuentra en */sitio/wwwRaíz*) y, a continuación, copie el archivo JAR de la aplicación de Spring Boot y el archivo *web.config* anterior.</span><span class="sxs-lookup"><span data-stu-id="9a808-170">Change the remote directory to the root folder of your web app, (which is at */site/wwwroot*), then copy the JAR file from your Spring Boot application and the *web.config* from earlier.</span></span> <span data-ttu-id="9a808-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9a808-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="9a808-172">Una vez implementados los archivos JAR y *web.config* en la aplicación web, debe reiniciar esta con Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="9a808-172">After you have deployed your JAR and *web.config* files to your web app, you need to restart your web app using the Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="9a808-173">Compruebe la aplicación web. Para ello, acceda a la URL de la aplicación con un explorador web, o bien utilice una sintaxis como la del siguiente ejemplo si tiene cURL disponible:</span><span class="sxs-lookup"><span data-stu-id="9a808-173">Test the web app by browsing to your web app's URL using a web browser, or use the syntax like the following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="9a808-174">Debería aparecer el siguiente mensaje: **Greetings from Spring Boot!** (Saludos de Spring Boot).</span><span class="sxs-lookup"><span data-stu-id="9a808-174">You should see the following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB02]

## <a name="next-steps"></a><span data-ttu-id="9a808-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9a808-176">Next steps</span></span>

<span data-ttu-id="9a808-177">Para obtener más información sobre el uso de aplicaciones de Spring Boot en Azure, consulte los siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="9a808-177">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="9a808-178">Implementación de una aplicación de Spring Boot en Linux en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="9a808-178">Deploy a Spring Boot Application on Linux in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="9a808-179">Implementación de una aplicación de Spring Boot en un clúster de Kubernetes en Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="9a808-179">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="9a808-180">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure] y [Java Tools for Visual Studio Team Services] (Herramientas de Java para Visual Studio Team Services).</span><span class="sxs-lookup"><span data-stu-id="9a808-180">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="9a808-181">Para obtener más información sobre la implementación de aplicaciones web en Azure mediante FTP, consulte [Implementación de la aplicación en Azure App Service mediante FTP/S].</span><span class="sxs-lookup"><span data-stu-id="9a808-181">For additional information about depoying web apps to Azure using FTP, see [Deploy your app to Azure App Service using FTP/S].</span></span>

<span data-ttu-id="9a808-182">Para obtener más información sobre el proyecto de ejemplo de Spring Boot, consulte [inicial de Spring Boot].</span><span class="sxs-lookup"><span data-stu-id="9a808-182">For further details about the Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="9a808-183">Para obtener ayuda para dar sus primeros pasos con sus propias aplicaciones de Spring Boot, consulte **Spring Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="9a808-183">For help with getting started with your own Spring Boot applications, see the **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="9a808-184">Para obtener más información sobre configuración de valores adicionales para la aplicación web, consulte [Configuración de aplicaciones web en Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="9a808-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

<span data-ttu-id="9a808-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span><span class="sxs-lookup"><span data-stu-id="9a808-185">[Azure App Service]: https://azure.microsoft.com/services/app-service/</span></span>
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
<span data-ttu-id="9a808-186">[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="9a808-186">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="9a808-187">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="9a808-187">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="9a808-188">[Configuración de aplicaciones web en Azure App Service]: /azure/app-service-web/web-sites-configure</span><span class="sxs-lookup"><span data-stu-id="9a808-188">[Configure web apps in Azure App Service]: /azure/app-service-web/web-sites-configure</span></span>
<span data-ttu-id="9a808-189">[Implementación de la aplicación en Azure App Service mediante FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span><span class="sxs-lookup"><span data-stu-id="9a808-189">[Deploy your app to Azure App Service using FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp</span></span>
<span data-ttu-id="9a808-190">[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="9a808-190">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="9a808-191">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="9a808-191">[Git]: https://github.com/</span></span>
<span data-ttu-id="9a808-192">[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="9a808-192">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="9a808-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="9a808-193">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="9a808-194">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="9a808-194">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="9a808-195">[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="9a808-195">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="9a808-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="9a808-196">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="9a808-197">[inicial de Spring Boot]: https://github.com/spring-guides/gs-spring-boot</span><span class="sxs-lookup"><span data-stu-id="9a808-197">[Spring Boot Getting Started]: https://github.com/spring-guides/gs-spring-boot</span></span>
<span data-ttu-id="9a808-198">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="9a808-198">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
