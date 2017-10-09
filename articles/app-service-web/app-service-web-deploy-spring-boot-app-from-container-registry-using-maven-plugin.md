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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una aplicación de arranque del muelle en el registro de contenedor de Azure tooAzure servicio de aplicaciones

Hola  **[Spring Framework]**  es un marco de código abierto popular que ayuda a los desarrolladores de Java a crear aplicaciones de API, móviles y web. Este tutorial utiliza una aplicación de ejemplo creada con [arranque primavera], un enfoque basado en la convención para el uso de primavera tooget a trabajar rápidamente.

Este artículo demuestra cómo toodeploy una tooAzure de aplicación de arranque Spring de ejemplo del registro de contenedor y después usar Hola Maven complemento para aplicaciones Web de Azure toodeploy su tooAzure aplicación servicio de aplicaciones.

> [!NOTE]
>
> Hola Maven complemento para las aplicaciones Web de Azure está disponible actualmente como una vista previa. Por ahora, se admite solo la publicación FTP, aunque características adicionales están planificadas para futuras Hola.
>

## <a name="prerequisites"></a>Requisitos previos

En orden toocomplete Hola los pasos de este tutorial, necesita hello toohave siguiendo los requisitos previos:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].
* Hola [interfaz de línea de comandos (CLI) de Azure].
* Un [kit de desarrollo de Java (JDK)] actualizado, versión 1.7 o posterior.
* La herramienta de compilación [Maven] de Apache (versión 3).
* Un cliente [Git].
* Un [cliente de Docker].

> [!NOTE]
>
> Debido a requisitos de virtualización de toohello de este tutorial, no podrá seguir pasos de hello en este artículo en una máquina virtual; debe usar un equipo físico con las características de virtualización habilitadas.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Ejemplo de Hola a Clone Spring arranque en la aplicación web de Docker

En esta sección, clone una aplicación de Spring Boot en contenedor y pruébela de forma local.

1. Abra un símbolo del sistema o la ventana de terminal y cree un directorio local toohold la aplicación de arranque de primavera y cambie el directorio toothat; Por ejemplo:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- o --
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Hola clon [arranque Spring en Introducción a Docker] proyecto de ejemplo en el directorio Hola creado; por ejemplo:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Cambiar directorio toohello completado proyecto; Por ejemplo:
   ```shell
   cd gs-spring-boot-docker/complete
   ```

1. Compilar el archivo JAR de hello mediante Maven; Por ejemplo:
   ```shell
   mvn clean package
   ```

1. Cuándo se ha creado la aplicación web de hello, iniciar la aplicación web de hello mediante Maven; Por ejemplo:
   ```shell
   mvn spring-boot:run
   ```

1. Probar la aplicación web de hello examinando tooit localmente mediante un explorador web. Por ejemplo, podría utilizar Hola siguiente comando si tienes curl disponible:
   ```shell
   curl http://localhost:8080
   ```

1. Debería ver el siguiente mensaje de Hola: **Docker Hola a todos**

   ![Examen local de aplicación de ejemplo][SB01]

## <a name="create-an-azure-service-principal"></a>Creación de una entidad de servicio de Azure

En esta sección, creará un Azure entidad de servicio que Hola usos de complemento de Maven al implementar su tooAzure de contenedor.

1. Abra el símbolo del sistema.

1. Inicio de sesión en su cuenta de Azure mediante el uso de Hola CLI de Azure:
   ```azurecli
   az login
   ```
   Siga Hola instrucciones toocomplete Hola inicio de sesión en proceso.

1. Cree una entidad de servicio de Azure:
   ```azurecli
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Donde `uuuuuuuu` es el nombre de usuario de Hola y `pppppppp` es contraseña Hola Hola principal de servicio.

1. Azure responde con JSON similar al siguiente ejemplo de Hola:
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
   > Utilizará valores de hello de esta respuesta JSON cuando configura hello Maven complemento toodeploy tooAzure de su contenedor. Hola `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición, que son usado en este ejemplo se toomake toomap más fácil estos valores tootheir respectivos elementos cuando se configura el Maven `settings.xml` archivo Hola a continuación sección.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Crear un registro de contenedor de Azure mediante Hola CLI de Azure

1. Abra el símbolo del sistema.

1. Inicie sesión en tooyour cuenta de Azure:
   ```azurecli
   az login
   ```

1. Crear un grupo de recursos para hello recursos de Azure que usará en este artículo:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Reemplace `wingtiptoysresources` en este ejemplo por un nombre único para el grupo de recursos.

1. Crear un registro de contenedor de Azure privada en grupo de recursos de hello para la aplicación de arranque de primavera: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Reemplace `wingtiptoysregistry` en este ejemplo por un nombre único para el registro de contenedor.

1. Recuperar la contraseña de hello para el registro de contenedor:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure responderá con la contraseña; por ejemplo:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Agregar el registro de contenedor de Azure y la configuración de Maven de tooyour principal de servicio de Azure

1. Abra su Maven `settings.xml` un archivo en un editor de texto; este archivo puede encontrarse en una ruta de acceso como hello en los ejemplos siguientes:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Agregar la configuración de acceso del registro de contenedor de Azure desde la sección anterior de Hola de este artículo toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Donde:
   Elemento | Descripción
   ---|---|---
   `<id>` | Contiene el nombre de Hola de seguridad del registro de contenedor de Azure privada.
   `<username>` | Contiene el nombre de Hola de seguridad del registro de contenedor de Azure privada.
   `<password>` | Contiene la contraseña de hello que recuperó en la sección anterior de Hola de este artículo.

1. Agregar la configuración de entidad de seguridad de servicio de Azure de una sección anterior de este artículo toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:

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
   Donde:
   Elemento | Descripción
   ---|---|---
   `<id>` | Especifica un nombre único que Maven use toolook su configuración de seguridad cuando se implementa la tooAzure de aplicación web.
   `<client>` | Contiene Hola `appId` valor de la entidad de seguridad de servicio.
   `<tenant>` | Contiene Hola `tenant` valor de la entidad de seguridad de servicio.
   `<key>` | Contiene Hola `password` valor de la entidad de seguridad de servicio.
   `<environment>` | Define el entorno de nube de Azure de destino de hello, que es `AZURE` en este ejemplo. (Una lista completa de los entornos de está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación)

1. Guarde y cierre hello *settings.xml* archivo.

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Generar a su Docker imagen de contenedor e insertarlo tooyour registro de contenedor de Azure

1. Navegue toohello completado el directorio del proyecto para la aplicación de arranque de primavera (p. ej. "*C:\SpringBoot\gs-spring-boot-docker\complete*"o"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), abra hello y *pom.xml* archivo con una editor de texto.

1. Hola de actualización `<properties>` colección Hola *pom.xml* archivo con el valor de servidor de inicio de sesión de hello para el registro de contenedor de Azure desde la sección anterior de Hola de este tutorial; por ejemplo:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Donde:
   Elemento | Descripción
   ---|---|---
   `<azure.containerRegistry>` | Especifica el nombre de Hola de seguridad del registro de contenedor de Azure privada.
   `<docker.image.prefix>` | Especifica la URL Hola de seguridad del registro de contenedor de Azure privada, que se crea agregando ". azurecr.io" nombre de toohello de seguridad del registro de contenedor privado.

1. Compruebe que `<plugin>` para hello Docker complemento en su *pom.xml* archivo contiene propiedades correctas de Hola para hello inicio de sesión del registro y la dirección del nombre del servidor del paso anterior de hello en este tutorial. Por ejemplo:

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
   Donde:
   Elemento | Descripción
   ---|---|---
   `<serverId>` | Especifica la propiedad de Hola que contiene el nombre de seguridad del registro de contenedor de Azure privada.
   `<registryUrl>` | Especifica la propiedad de Hola que contiene la dirección URL de Hola de seguridad del registro de contenedor de Azure privada.

1. Navegar por el directorio del proyecto toohello completado para la aplicación de arranque de primavera y ejecute hello tras la aplicación de comando toorebuild Hola e inserte Hola contenedor tooyour del registro de contenedor de Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

1. OPCIONAL: Examinar toohello [portal de Azure] y compruebe que hay una imagen de contenedor de Docker denominada **gs-spring-arranque-docker** en el registro de contenedor.

   ![Comprobar contenedor en Azure Portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Personalizar su pom.xml, a continuación, compilar e implementar su tooAzure de contenedor

Abra hello `pom.xml` de archivos para la aplicación de arranque del muelle en un editor de texto y, a continuación, busque hello `<plugin>` (elemento) para `azure-webapp-maven-plugin`. Este elemento debe ser similar a Hola siguiente ejemplo:

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

Hay varios valores que se pueden modificar para hello Maven complemento y obtener una descripción detallada de cada uno de estos elementos está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación. Dicho esto, hay varios valores que merece la pena destacar en este artículo:

Elemento | Descripción
---|---|---
`<version>` | Especifica la versión de Hola de hello [Maven complemento para las aplicaciones Web de Azure]. Debe comprobar la versión de Hola enumerada en hello [repositorio Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que utilizas Hola versión más reciente.
`<authentication>` | Especifica la información de autenticación de Hola de Azure, que en este ejemplo contiene un `<serverId>` elemento que contiene `azure-auth`; Maven usa ese toolook valor valores de entidad de seguridad de servicio de Azure de hello en su Maven *settings.xml* archivo, que se define en una sección anterior de este artículo.
`<resourceGroup>` | Especifica el grupo de recursos de destino de hello, que es `wingtiptoysresources` en este ejemplo. Si aún no existe, se creará el grupo de recursos de Hola durante la implementación.
`<appName>` | Especifica el nombre de destino de hello para la aplicación web. En este ejemplo, es el nombre de destino de hello `maven-linux-app-${maven.build.timestamp}`, donde hello `${maven.build.timestamp}` se anexa un sufijo por este conflicto de tooavoid de ejemplo. (marca de tiempo de hello es opcional; puede especificar cualquier cadena única para el nombre de la aplicación hello).
`<region>` | Especifica la región de destino de hello, que en este ejemplo es `westus`. (Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)
`<containerSettings>` | Especifica las propiedades de Hola que contienen el nombre de Hola y la dirección URL del contenedor.
`<appSettings>` | Especifica los valores únicos para Maven toouse al implementar su tooAzure de aplicación web. En este ejemplo, un `<property>` elemento contiene un par nombre/valor de los elementos secundarios que especifican Hola puerto para la aplicación.

> [!NOTE]
>
> número de puerto de Hello configuración toochange hello en este ejemplo solo son necesarios cuando está cambiando el puerto de Hola de predeterminado de Hola.
>

1. Desde el símbolo del sistema de Hola o ventana de terminal que estaba usando anteriormente, volver a generar archivo JAR de hello mediante Maven si ha realizado los cambios toohello *pom.xml* archivo; por ejemplo:
   ```shell
   mvn clean package
   ```

1. Implementar la tooAzure de aplicación web mediante el uso de Maven; Por ejemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementará su tooAzure de aplicación web; Si la aplicación web de hello aún no existe, se creará.

> [!NOTE]
>
> Si región Hola que se especifica en hello `<region>` elemento de su *pom.xml* archivo no tiene suficientes servidores disponibles al iniciar la implementación, es posible que vea un toohello de error similar siguiente ejemplo:
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
> Si esto ocurre, puede especificar que otra región y vuelva a ejecutar Hola Maven comando toodeploy la aplicación.
>
>

Cuando se ha implementado la web, será capaz de toomanage mediante hello [portal de Azure].

* La aplicación web aparecerá en **App Services**:

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* Y Hola dirección URL para la aplicación web se mostrarán en hello **Introducción** para la aplicación web:

   ![Determinar la dirección URL de hello para la aplicación web][AP02]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de hello varias tecnologías descritas en este artículo, consulte Hola siguientes artículos:

* [Maven complemento para las aplicaciones Web de Azure]

* [Inicie sesión en tooAzure de hello CLI de Azure](/azure/xplat-cli-connect)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

* [Complemento Docker para Maven]

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
