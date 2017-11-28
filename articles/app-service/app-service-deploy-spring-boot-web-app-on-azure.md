---
title: "un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello aaaDeploy | Documentos de Microsoft"
description: "Este tutorial le guiará a los desarrolladores a través de hello pasos toodeploy Hola Spring arranque Introducción a web app tooAzure servicio de aplicaciones."
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
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a><span data-ttu-id="3f7fd-103">Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello</span><span class="sxs-lookup"><span data-stu-id="3f7fd-103">Deploy a Spring Boot Application toohello Azure App Service</span></span>

<span data-ttu-id="3f7fd-104">Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial, y uno de los proyectos de hello más popular que se basa en esa plataforma es [Arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-104">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications, and one of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span>

<span data-ttu-id="3f7fd-105">Este tutorial le guiará aunque crear ejemplo de Hola Spring arranque Introducción a la aplicación web e implementarla demasiado[servicio de aplicaciones de Azure].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-105">This tutorial will walk you though creating hello sample Spring Boot Getting Started web app and deploying it too[Azure App Service].</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3f7fd-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3f7fd-106">Prerequisites</span></span>

<span data-ttu-id="3f7fd-107">En orden toocomplete Hola los pasos de este tutorial, necesita toohave Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-107">In order toocomplete hello steps in this tutorial, you need toohave hello following:</span></span>

* <span data-ttu-id="3f7fd-108">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-108">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="3f7fd-109">Un [kit para desarrolladores de Java (JDK)] actualizado.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-109">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="3f7fd-110">La herramienta de compilación [Maven] de Apache (versión 3).</span><span class="sxs-lookup"><span data-stu-id="3f7fd-110">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="3f7fd-111">Un cliente [Git].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-111">A [Git] client.</span></span>

## <a name="create-hello-spring-boot-getting-started-web-app"></a><span data-ttu-id="3f7fd-112">Crear una aplicación web Spring arranque introducción de Hola</span><span class="sxs-lookup"><span data-stu-id="3f7fd-112">Create hello Spring Boot Getting Started web app</span></span>

<span data-ttu-id="3f7fd-113">Hello siguientes pasos le guiarán a través de los pasos de hello toocreate requiere una sencilla aplicación web de arranque de primavera y probar de forma local.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-113">hello following steps will walk you through hello steps that are required toocreate a simple Spring Boot web application and test it locally.</span></span>

1. <span data-ttu-id="3f7fd-114">Abra un símbolo y crear un directorio local toohold la aplicación y cambie el directorio toothat; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-114">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="3f7fd-115">-- o --</span><span class="sxs-lookup"><span data-stu-id="3f7fd-115">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="3f7fd-116">Hola clon [Spring Introducción arranque] proyecto de ejemplo en el directorio de Hola que acaba de crear; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-116">Clone hello [Spring Boot Getting Started] sample project into hello directory you just created; for example:</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. <span data-ttu-id="3f7fd-117">Cambiar directorio toohello completado proyecto; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-117">Change directory toohello completed project; for example:</span></span>
   ```
   cd gs-spring-boot
   cd complete
   ```

1. <span data-ttu-id="3f7fd-118">Compilar el archivo JAR de hello mediante Maven; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-118">Build hello JAR file using Maven; for example:</span></span>
   ```
   mvn package
   ```

1. <span data-ttu-id="3f7fd-119">Una vez creada la aplicación web de hello, cambiar el archivo JAR de directorio toohello e iniciar aplicación web de hello; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-119">Once hello web app has been created, change directory toohello JAR file and start hello web app; for example:</span></span>
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. <span data-ttu-id="3f7fd-120">Probar la aplicación web de hello examinando toohttp://localhost:8080 mediante un explorador web o utilizar una sintaxis de hello como Hola siguiente ejemplo, si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-120">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="3f7fd-121">Debería ver el siguiente mensaje de Hola: **Greetings de arranque de primavera!**</span><span class="sxs-lookup"><span data-stu-id="3f7fd-121">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a><span data-ttu-id="3f7fd-123">Creación de una aplicación web de Azure para usarla con Java</span><span class="sxs-lookup"><span data-stu-id="3f7fd-123">Create an Azure web app for use with Java</span></span>

<span data-ttu-id="3f7fd-124">Hola pasos se le guían a través de hello pasos toocreate una aplicación Web de Azure, configure opciones de hello necesario para Java y configurar las credenciales FTP.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-124">hello following steps will walk you through hello steps toocreate an Azure Web App, configure hello required settings for Java, and configure your FTP credentials.</span></span>

1. <span data-ttu-id="3f7fd-125">Examinar toohello [portal de Azure] e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-125">Browse toohello [Azure portal] and log in.</span></span>

1. <span data-ttu-id="3f7fd-126">Una vez que han iniciado sesión en su cuenta en hello portal de Azure, haga clic en el icono de menú de Hola para **servicios de aplicaciones**:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-126">Once you have logged into your account on hello Azure portal, click hello menu icon for **App Services**:</span></span>
   
   ![Azure Portal][AZ01]

1. <span data-ttu-id="3f7fd-128">Cuando Hola **servicios de aplicaciones** se muestra la página, haga clic en **+ agregar** toocreate un nuevo servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-128">When hello **App Services** page is displayed, click **+ Add** toocreate a new App Service.</span></span>

   ![Creación de un elemento App Service][AZ02]

1. <span data-ttu-id="3f7fd-130">Cuando se muestra la lista de Hola de plantillas de aplicación web, haga clic en vínculo Hola Hola básica aplicación Web de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-130">When hello list of web app templates is displayed, click hello link for hello basic Microsoft Web App.</span></span>

   ![Plantillas de aplicaciones web][AZ03]

1. <span data-ttu-id="3f7fd-132">Cuando se muestra la página de información de hello para la plantilla de aplicación Web de hello, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-132">When hello information page for hello Web App template is displayed, click **Create**.</span></span>

   ![Crear aplicación web][AZ04]

1. <span data-ttu-id="3f7fd-134">Proporcione un nombre único para la aplicación web y especifique cualquier configuración adicional. A continuación, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-134">Provide a unique name for your web app and specify any additional settings, and then **Create**.</span></span>

   ![Creación de configuración de aplicaciones web][AZ05]

1. <span data-ttu-id="3f7fd-136">Una vez creada la aplicación web, haga clic en el icono de menú de Hola para **servicios de aplicaciones**y, a continuación, haga clic en la aplicación web recién creado:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-136">Once your web app has been created, click hello menu icon for **App Services**, and then click your newly-created web app:</span></span>

   ![Lista de aplicaciones web][AZ06]

1. <span data-ttu-id="3f7fd-138">Cuando se muestra la aplicación web, especificar versión de Java de hello mediante Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-138">When your web app is displayed, specify hello Java version by using hello following steps:</span></span>

   <span data-ttu-id="3f7fd-139">a.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-139">a.</span></span> <span data-ttu-id="3f7fd-140">Haga clic en hello **configuración de la aplicación** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-140">Click hello **Application Settings** menu item.</span></span>

   <span data-ttu-id="3f7fd-141">b.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-141">b.</span></span> <span data-ttu-id="3f7fd-142">Elija **Java 8** para la versión de Java de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-142">Choose **Java 8** for hello Java version.</span></span>

   <span data-ttu-id="3f7fd-143">c.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-143">c.</span></span> <span data-ttu-id="3f7fd-144">Elija **más reciente** de versión secundaria de Java de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-144">Choose **Newest** for hello minor Java version.</span></span>

   <span data-ttu-id="3f7fd-145">d.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-145">d.</span></span> <span data-ttu-id="3f7fd-146">Elija **8.5 más recientes de Tomcat** para el contenedor de hello web.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-146">Choose **Newest Tomcat 8.5** for hello web container.</span></span> <span data-ttu-id="3f7fd-147">(Este contenedor no realmente se utilizará; Azure usará contenedor Hola desde la aplicación de arranque de primavera.)</span><span class="sxs-lookup"><span data-stu-id="3f7fd-147">(This container will not actually be used; Azure will use hello container from your Spring Boot application.)</span></span>

   <span data-ttu-id="3f7fd-148">e.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-148">e.</span></span> <span data-ttu-id="3f7fd-149">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-149">Click **Save**.</span></span>

   ![Configuración de la aplicación][AZ07]

1. <span data-ttu-id="3f7fd-151">Especificar las credenciales de implementación FTP mediante Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-151">Specify your FTP deployment credentials by using hello following steps:</span></span>

   <span data-ttu-id="3f7fd-152">a.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-152">a.</span></span> <span data-ttu-id="3f7fd-153">Haga clic en hello **las credenciales de implementación** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-153">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="3f7fd-154">b.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-154">b.</span></span> <span data-ttu-id="3f7fd-155">Especifique el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-155">Specify your username and password.</span></span>

   <span data-ttu-id="3f7fd-156">c.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-156">c.</span></span> <span data-ttu-id="3f7fd-157">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-157">Click **Save**.</span></span>

   ![Especificación de credenciales de implementación][AZ08]

1. <span data-ttu-id="3f7fd-159">Recuperar la información de conexión de FTP mediante Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-159">Retrieve your FTP connection information by using hello following steps:</span></span>

   <span data-ttu-id="3f7fd-160">a.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-160">a.</span></span> <span data-ttu-id="3f7fd-161">Haga clic en hello **las credenciales de implementación** elemento de menú.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-161">Click hello **Deployment Credentials** menu item.</span></span>

   <span data-ttu-id="3f7fd-162">b.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-162">b.</span></span> <span data-ttu-id="3f7fd-163">Copie el nombre de usuario FTP completo y la dirección URL y guardarlas para la siguiente sección de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-163">Copy your full FTP username and URL and save them for hello next section of this tutorial.</span></span>

   ![URL y credenciales de FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a><span data-ttu-id="3f7fd-165">Implementar su tooAzure de aplicación web de arranque de primavera</span><span class="sxs-lookup"><span data-stu-id="3f7fd-165">Deploy your Spring Boot web app tooAzure</span></span>

<span data-ttu-id="3f7fd-166">Hola pasos le guiará por hello pasos toodeploy su tooAzure de aplicación web de arranque del muelle.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-166">hello following steps will walk you through hello steps toodeploy your Spring Boot web app tooAzure.</span></span>

1. <span data-ttu-id="3f7fd-167">Abra un editor de texto como el Bloc de notas de Windows y pegar Hola después de texto en un nuevo documento y, a continuación, guarde el archivo hello como *web.config*:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-167">Open a text editor such as Windows Notepad and paste hello following text into a new document, then save hello file as *web.config*:</span></span>
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

1. <span data-ttu-id="3f7fd-168">Después de haber guardado hello *web.config* tooyour sistema de archivos, conectar aplicación web de tooyour a través de FTP mediante la dirección URL de hello, username y password de hello anterior sección de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-168">After you have saved hello *web.config* file tooyour system, connect tooyour web app via FTP using hello URL, username, and password from hello preceding section of this tutorial.</span></span> <span data-ttu-id="3f7fd-169">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-169">For example:</span></span>
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. <span data-ttu-id="3f7fd-170">Cambiar la carpeta raíz del Hola directorio remoto toohello de la aplicación web, (que se encuentra en */sitio/wwwroot*), a continuación, copie el archivo JAR de Hola desde la aplicación de arranque de primavera y Hola *web.config* desde versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-170">Change hello remote directory toohello root folder of your web app, (which is at */site/wwwroot*), then copy hello JAR file from your Spring Boot application and hello *web.config* from earlier.</span></span> <span data-ttu-id="3f7fd-171">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-171">For example:</span></span>
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. <span data-ttu-id="3f7fd-172">Después de haber implementado el JAR y *web.config* archivos tooyour web app, necesita toorestart su aplicación web con hello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-172">After you have deployed your JAR and *web.config* files tooyour web app, you need toorestart your web app using hello Azure portal:</span></span>

   ![][AZ10]

1. <span data-ttu-id="3f7fd-173">Probar la aplicación web de hello examinando la dirección URL de la aplicación de tooyour web mediante un explorador web o utilizar una sintaxis de hello como Hola siguiente ejemplo, si tienes curl disponible:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-173">Test hello web app by browsing tooyour web app's URL using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. <span data-ttu-id="3f7fd-174">Debería ver el siguiente mensaje de Hola: **Greetings de arranque de primavera!**</span><span class="sxs-lookup"><span data-stu-id="3f7fd-174">You should see hello following message displayed: **Greetings from Spring Boot!**</span></span>

   ![Buscar aplicación de ejemplo][SB02]

## <a name="next-steps"></a><span data-ttu-id="3f7fd-176">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f7fd-176">Next steps</span></span>

<span data-ttu-id="3f7fd-177">Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="3f7fd-177">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="3f7fd-178">Implementar una aplicación de arranque del muelle en Linux en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="3f7fd-178">Deploy a Spring Boot Application on Linux in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [<span data-ttu-id="3f7fd-179">Implementar una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="3f7fd-179">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="3f7fd-180">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-180">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="3f7fd-181">Para obtener información adicional sobre tooAzure de aplicaciones web depoying mediante FTP, consulte [implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-181">For additional information about depoying web apps tooAzure using FTP, see [Deploy your app tooAzure App Service using FTP/S].</span></span>

<span data-ttu-id="3f7fd-182">Para obtener más información sobre el proyecto de ejemplo de Hola Spring arranque, consulte [Spring Introducción arranque].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-182">For further details about hello Spring Boot sample project, see [Spring Boot Getting Started].</span></span>

<span data-ttu-id="3f7fd-183">Para obtener ayuda acerca de cómo empezar a usar sus propias aplicaciones de arranque de primavera, vea hello **primavera Initializr** en https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="3f7fd-183">For help with getting started with your own Spring Boot applications, see hello **Spring Initializr** at https://start.spring.io/.</span></span>

<span data-ttu-id="3f7fd-184">Para obtener más información sobre configuración de valores adicionales para la aplicación web, consulte [Configuración de aplicaciones web en Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="3f7fd-184">For more information about configuring additional settings for your web app, see [Configure web apps in Azure App Service].</span></span>

<!-- URL List -->

[servicio de aplicaciones de Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[portal de Azure]: https://portal.azure.com/
[Configuración de aplicaciones web en Azure App Service]: /azure/app-service-web/web-sites-configure
[implementar el servicio de aplicaciones mediante FTP/S de aplicación tooAzure]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[kit para desarrolladores de Java (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Arranque primavera]: http://projects.spring.io/spring-boot/
[Spring Introducción arranque]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

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
