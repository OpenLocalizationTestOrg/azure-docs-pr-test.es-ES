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
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Implementar una aplicación de arranque del muelle en Linux en hello servicio de contenedor de Azure

Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java.

**[cliente de Docker]**  es soluciones de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, ajuste de escala y administración de las aplicaciones que se ejecutan en contenedores.

Este tutorial le guía a través mediante Docker toodevelop e implementar un host de Linux de arranque Spring aplicación tooa Hola [contenedor Service (ACS) de Azure].

## <a name="prerequisites"></a>Requisitos previos

En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Hola [interfaz de línea de comandos (CLI) de Azure].
* Un [kit para desarrolladores de Java (JDK)] actualizado.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un [cliente de Docker].

> [!NOTE]
>
> Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Crear Hola Spring arranque en la aplicación web de introducción a Docker

Hello pasos siguientes le guían a través de los pasos de hello toocreate requiere una sencilla aplicación web de arranque de primavera y probar de forma local.

1. Abra un símbolo y crear un directorio local toohold la aplicación y cambie el directorio toothat; Por ejemplo:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio Hola creado; por ejemplo:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Cambiar directorio toohello completado proyecto; Por ejemplo:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Compilar el archivo JAR de hello mediante Maven; Por ejemplo:
   ```
   mvn package
   ```

1. Una vez creada la aplicación web de hello, cambie el directorio toohello `target` directorio donde el archivo JAR de Hola se encuentra e inicia la aplicación web de hello; por ejemplo:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Probar la aplicación web de hello examinando tooit localmente mediante un explorador web. Por ejemplo, si tienes curl disponible y configurado toorun de servidor de Tomcat hello en el puerto 80:
   ```
   curl http://localhost
   ```

1. Debería ver el siguiente mensaje de Hola: **Docker ¡Hello World!**

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Crear un registro de contenedor de Azure toouse como un registro de Docker privada

Hello pasos siguientes le guían a través mediante hello toocreate portal Azure un registro de contenedor de Azure.

> [!NOTE]
>
> Si desea que toouse Hola CLI de Azure en lugar de hello portal de Azure, siga los pasos de hello en [crear un registro de contenedor de Docker privado mediante hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Examinar toohello [portal de Azure] e inicie sesión.

   Una vez que haya iniciado sesión tooyour cuenta en hello portal de Azure, puede seguir los pasos de Hola Hola [crear un registro de contenedor de Docker privado mediante el portal de Azure de hello] artículo, que se paraphrased en hello siguiendo los pasos para hello simplificar la conveniencia.

1. Haga clic en el icono de menú de Hola de **+ nuevo**, a continuación, haga clic en **contenedores**y, a continuación, haga clic en **registro de contenedor de Azure**.
   
   ![Crear una instancia de Azure Container Registry][AR01]

1. Cuando se muestra la página de información de hello para la plantilla de registro de contenedor de Azure de hello, haga clic en **crear**. 

   ![Crear una instancia de Azure Container Registry][AR02]

1. Cuando Hola **crear registro de contenedor** se muestra la página, escriba su **nombre del registro** y **grupo de recursos**, elija **habilitar** para Hola **usuario Admin**y, a continuación, haga clic en **crear**.

   ![Configurar Azure Container Registry][AR03]

1. Una vez que se ha creado el registro de contenedor, vaya tooyour del registro de contenedor en hello portal de Azure y, a continuación, haga clic en **teclas de acceso**. Tome nota de hello username y password para obtener instrucciones de Hola.

   ![Claves de acceso de Azure Container Registry][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Configurar Maven toouse las claves de acceso del registro de contenedor de Azure

1. Desplácese toohello el directorio de configuración para la instalación de Maven y abra hello *settings.xml* archivo con un editor de texto.

1. Agregar la configuración de acceso del registro de contenedor de Azure desde la sección anterior de Hola de este tutorial toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera, (por ejemplo: "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completa*"), abra hello y *pom.xml* archivo con un editor de texto.

1. Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial; por ejemplo:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hola de actualización `<plugins>` colección Hola *pom.xml* de archivos para que Hola `<plugin>` contiene Hola inicio de sesión del registro y la dirección del nombre del servidor para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial. Por ejemplo:

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

1. Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera y ejecute hello tras la aplicación de comando toorebuild Hola e inserte Hola contenedor tooyour del registro de contenedor de Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Cuando está realizando la inserción de su tooAzure de contenedor de Docker, puede recibir un mensaje de error es tooone similar de hello seguir incluso aunque el contenedor de Docker se creó correctamente:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Si esto ocurre, puede que necesite toosign en tooyour cuenta de Azure desde la línea de comandos de Docker de hello; Por ejemplo:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> A continuación, puede insertar el contenedor desde la línea de comandos de hello; Por ejemplo:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Crear una aplicación web en Linux en Azure App Service mediante la imagen de contenedor

1. Examinar toohello [portal de Azure] e inicie sesión.

1. Haga clic en el icono de menú de Hola de **+ nuevo**, a continuación, haga clic en **Web y móvil**y, a continuación, haga clic en **aplicación Web en Linux**.
   
   ![Crear una nueva aplicación web en hello portal de Azure][LX01]

1. Cuando Hola **aplicación Web en Linux** se muestra la página, escriba Hola siguiente información:

   a. Escriba un nombre único para hello **nombre de la aplicación**; por ejemplo: "*wingtiptoyslinux*."

   b. Elija su **suscripción** desde la lista desplegable de Hola.

   c. Elegir una existente **grupo de recursos**, o especificar un nuevo grupo de recursos de nombre toocreate.

   d. Haga clic en **configurar contenedor** y escriba Hola siguiente información:

      * Seleccione **Registro privado**.

      * **Imagen y etiqueta opcional**: especifique el nombre del contenedor del ejemplo anterior, por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

      * **Dirección URL del servidor**: especifique la dirección URL del Registro del ejemplo anterior, por ejemplo: "*https://wingtiptoysregistry.azurecr.io*".

      * **Nombre de usuario de inicio de sesión** y **Contraseña**: especifique las credenciales de inicio de sesión de las **Claves de acceso** que ha usado en los pasos anteriores.
   
   e. Una vez que se han introducido todos Hola por encima de la información, haga clic en **Aceptar**.

   ![Configurar aplicaciones web][LX02]

1. Haga clic en **Crear**.

> [!NOTE]
>
> Azure asignará automáticamente el servidor de Tomcat de tooembedded de las solicitudes de Internet que se ejecuta en los puertos estándar Hola de 80 o 8080. Sin embargo, si configuró el toorun de servidor de Tomcat incrustado en un puerto personalizado, debe tooadd una aplicación web tooyour variables de entorno que define el puerto de hello para el servidor de Tomcat incrustado. toodo por lo tanto, use Hola pasos:
>
> 1. Examinar toohello [portal de Azure] e inicie sesión.
> 
> 2. Haga clic en el icono de Hola para **servicios de aplicaciones**. (Vea el elemento #1 en la imagen de hello siguiente).
>
> 3. Seleccione la aplicación web de lista de Hola. (Elemento #2 en la imagen de hello siguiente).
>
> 4. Haga clic en **Configuración de la aplicación**. (Elemento #3 en la imagen de hello siguiente).
>
> 5. Hola **configuración de la aplicación** sección, agregue una nueva variable de entorno denominada **puerto** y escriba su número de puerto personalizado para el valor de Hola. (Elemento #4 de la imagen de hello siguiente).
>
> 6. Haga clic en **Guardar**. (Elemento #5 en la imagen de hello siguiente).
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

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:

* [Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Implementar una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure](container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

Para obtener más información acerca de hello Spring arranque en el proyecto de ejemplo de Docker, consulte [arranque Spring en Introducción a Docker].

Para obtener ayuda acerca de cómo empezar a usar sus propias aplicaciones de arranque de primavera, vea hello **primavera Initializr** en https://start.spring.io/.

Para obtener más información acerca de cómo empezar a crear una sencilla aplicación de arranque de primavera, vea Hola primavera Initializr en https://start.spring.io/.

Para obtener más ejemplos de cómo toouse imágenes de Docker personalizado con Azure, consulte [con una imagen personalizada de Docker para la aplicación Web de Azure en Linux].

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
