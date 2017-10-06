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
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Implementar una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure

Hola  **[Spring Framework]**  es un marco de código abierto popular que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web. Este tutorial utiliza una aplicación de ejemplo creada con [arranque primavera], un enfoque basado en la convención para el uso de primavera tooget a trabajar rápidamente.

**[Kubernetes]**  y  **[cliente de Docker]**  son soluciones de código abierto que ayuda a los desarrolladores automatizar la implementación de hello, el ajuste de escala y la administración de sus aplicaciones que se ejecutan en contenedores.

Este tutorial guía aunque combinar estos toodevelop dos tecnologías populares, código abierto e implementar un tooMicrosoft de aplicación de arranque de primavera Azure. Más específicamente, use  *[arranque primavera]*  para el desarrollo de aplicaciones,  *[Kubernetes]*  para la implementación de contenedor y Hola [Contenedor Service (ACS) de azure] toohost la aplicación.

### <a name="prerequisites"></a>Requisitos previos

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

Hola pasos le guían por creando una aplicación web de arranque de primavera y las pruebas de forma local.

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

1. Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio de Hola.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Cambiar directorio toohello completado proyecto.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Utilice toobuild de Maven y aplicaciones de ejemplo de Hola de ejecución.
   ```
   mvn package spring-boot:run
   ```

1. Aplicación de prueba hello web examinando toohttp://localhost:8080 o con siguiente hello `curl` comando:
   ```
   curl http://localhost:8080
   ```

1. Debería ver el siguiente mensaje de Hola: **Docker Hola a todos**

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Crear un registro de contenedor de Azure mediante Hola CLI de Azure

1. Abra el símbolo del sistema.

1. Inicie sesión en tooyour cuenta de Azure:
   ```azurecli
   az login
   ```

1. Crear un grupo de recursos para hello recursos de Azure usados en este tutorial.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Crear un registro de contenedor de Azure privada en el grupo de recursos de Hola. tutorial de Hello inserta la aplicación de ejemplo de Hola como un registro de toothis de imágenes de Docker en pasos posteriores. Reemplace `wingtiptoysregistry` por un nombre único para el registro.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Error en el registro de aplicación toohello contenedor de inserción

1. Navegue toohello el directorio de configuración para la instalación de Maven (~/.m2/ predeterminado o C:\Users\username\.m2) abierto hello y *settings.xml* archivo con un editor de texto.

1. Recuperar la contraseña de hello para el registro de contenedor de hello CLI de Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Agregue los tooa del registro de contenedor de Azure de identificador y la contraseña nueva `<server>` colección Hola *settings.xml* archivo.
Hola `id` y `username` son Hola nombre del registro de hello. Hola de uso `password` valor del comando anterior de hello (sin comillas).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera (por ejemplo, "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker / completa*"), abra hello y *pom.xml* archivo con un editor de texto.

1. Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Hola de actualización `<plugins>` colección Hola *pom.xml* de archivos para que Hola `<plugin>` contiene Hola inicio de sesión del registro y la dirección del nombre del servidor para el registro de contenedor de Azure.

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

1. Navegue toohello completado el directorio del proyecto para la aplicación de arranque de primavera y ejecute hello después comando toobuild hello Docker contenedor e inserte Hola imagen toohello del registro:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Puede recibir un mensaje de error es tooone similar de siguientes hello cuando Maven inserta Hola imagen tooAzure:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Si recibe este error, inicie sesión en tooAzure de línea de comandos de Docker Hola.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Después, inserte el contenedor:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Cree un Kubernetes clúster en ACS con hello CLI de Azure

1. Cree un clúster de Kubernetes en Azure Container Service. Hello siguiente comando crea un *kubernetes* clúster Hola *wingtiptoys kubernetes* recursos grupo con *wingtiptoys-objeto containerservice* como clúster de Hola nombre, y *wingtiptoys kubernetes* como prefijo DNS de hello:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Este comando puede tardar un rato toocomplete.

1. Instalar `kubectl` utilizando Hola CLI de Azure. Los usuarios de Linux pueden tener tooprefix este comando con `sudo` desde que se implementa hello Kubernetes CLI demasiado`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Descargar la información de configuración de clúster de Hola para que pueda administrar el clúster desde la interfaz web de hello Kubernetes y `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Implementar Hola imagen tooyour Kubernetes clúster

Este tutorial implementa la aplicación hello con `kubectl`, a continuación, le permiten implementación de hello tooexplore a través de la interfaz web de hello Kubernetes.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Implementar con la interfaz web de hello Kubernetes

1. Abra el símbolo del sistema.

1. Abra el sitio Web de configuración de hello para el clúster de Kubernetes en el explorador predeterminado:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Cuando se abre el sitio Web de configuración de Kubernetes de hello en el explorador, demasiado haga clic en el vínculo de hello**implementar una aplicación en contenedores**:

   ![Sitio web para la configuración de Kubernetes][KB01]

1. Cuando Hola **implementar una aplicación en contenedores** se muestra la página, especifique Hola siguientes opciones:

   a. Seleccione **Specify app details below** (Especificar detalles de la aplicación a continuación).

   b. Escriba su nombre de aplicación de arranque de primavera de hello **nombre de la aplicación**; por ejemplo: "*gs-spring-arranque-docker*".

   c. Escriba la imagen de servidor y un contenedor de inicio de sesión de versiones anteriores de hello **imagen de contenedor**; por ejemplo: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Elija **externo** para hello **servicio**.

   e. Especifique los puertos internos y externos en hello **puerto** y **puerto de destino** cuadros de texto.

   ![Sitio web para la configuración de Kubernetes][KB02]


1. Haga clic en **implementar** contenedor de hello toodeploy.

   ![Implementar un contenedor][KB05]

1. Una vez que la aplicación se haya implementado, verá la aplicación Spring Boot en **Services** (Servicios).

   ![Servicios de Kubernetes][KB06]

1. Si hace clic en el vínculo de Hola para **extremos externos**, puede ver la aplicación de arranque de primavera ejecuta en Azure.

   ![Servicios de Kubernetes][KB07]

   ![Examen de la aplicación de ejemplo en Azure][SB02]


### <a name="deploy-with-kubectl"></a>Implementación con kubectl

1. Abra el símbolo del sistema.

1. Ejecutar el contenedor en el clúster de hello Kubernetes mediante hello `kubectl run` comando. Proporcione un nombre de servicio para la aplicación en Kubernetes y el nombre de la imagen completa de Hola. Por ejemplo:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   En este comando:

   * nombre del contenedor de Hello `gs-spring-boot-docker` especificado inmediatamente después de hello `run` comando

   * Hola `--image` parámetro especifica Hola combinados de servidor de inicio de sesión y nombre de la imagen como`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Exponer el clúster Kubernetes externamente mediante hello `kubectl expose` comando. Especifique el nombre del servicio, Hola orientados al público TCP puerto usado tooaccess Hola aplicación y puerto de destino interno de hello que escucha la aplicación. Por ejemplo:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   En este comando:

   * nombre del contenedor de Hello `gs-spring-boot-docker` especificado inmediatamente después de hello `expose deployment` comando

   * Hola `--type` parámetro especifica ese clúster Hola utiliza el equilibrador de carga

   * Hola `--port` parámetro especifica Hola orientados al público el puerto TCP 80. El acceso a la aplicación hello en este puerto.

   * Hola `--target-port` parámetro especifica Hola interno el puerto TCP 8080. equilibrador de carga de Hello reenvía las solicitudes aplicación de tooyour en este puerto.

1. Una vez que se implementa la aplicación hello toohello clúster, consultar la dirección IP externa de Hola y abrirlo en el explorador web:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Examen de la aplicación de ejemplo en Azure][SB02]


## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca del uso de arranque del muelle en Azure, vea Hola siguientes artículos:

* [Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Implementar una aplicación de arranque del muelle en Linux en hello servicio de contenedor de Azure](container-service-deploy-spring-boot-app-on-linux.md)

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

Para obtener más información acerca de hello Spring arranque en el proyecto de ejemplo de Docker, consulte [arranque Spring en Introducción a Docker].

Hola siguientes vínculos proporciona información adicional acerca de cómo crear aplicaciones de arranque de primavera:

* Para obtener más información acerca de cómo crear una sencilla aplicación de arranque de primavera, vea Hola primavera Initializr en https://start.spring.io/.

Hello vínculos siguientes proporcionan información adicional sobre el uso de Kubernetes con Azure:

* [Implementación de un clúster de Kubernetes para los contenedores de Linux](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Con hello Kubernetes web interfaz de usuario con el servicio de contenedor de Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Para obtener más información sobre el uso de la interfaz de línea de comandos de Kubernetes está disponible en hello **kubectl** Guía de usuario en <https://kubernetes.io/docs/user-guide/kubectl/>.

sitio Web de Kubernetes de Hello tiene varios artículos que tratan sobre el uso de imágenes en registros privados:

* [Configure Service Accounts for Pods] (Configurar cuentas de servicio para pods)
* [Espacios de nombres]
* [Pull an Image from a Private Registry] (Extraer una imagen de un registro privado)

Para obtener más ejemplos de cómo toouse imágenes de Docker personalizado con Azure, consulte [con una imagen personalizada de Docker para la aplicación Web de Azure en Linux].

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
