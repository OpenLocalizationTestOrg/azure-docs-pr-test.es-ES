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
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera

Hola [Maven complemento para las aplicaciones Web de Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) para [Maven Apache](http://maven.apache.org/) proporciona una perfecta integración del servicio de aplicaciones de Azure en proyectos de Maven y optimiza el proceso de Hola para las aplicaciones web de los desarrolladores toodeploy tooAzure servicio de aplicaciones.

Este artículo muestra cómo utilizar hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque de primavera servicios de aplicaciones de ejemplo.

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

## <a name="clone-hello-sample-spring-boot-web-app"></a>Aplicación web de clon hello ejemplo arranque primavera

En esta sección, va a clonar una aplicación de Spring Boot terminada y a probarla de forma local.

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

1. Hola clon [Spring Introducción arranque] proyecto de ejemplo en el directorio Hola creado; por ejemplo:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Cambiar directorio toohello completado proyecto; Por ejemplo:
   ```shell
   cd gs-spring-boot/complete
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

1. Debería ver el siguiente mensaje de Hola: **Greetings de arranque de primavera!**

## <a name="create-an-azure-service-principal"></a>Creación de una entidad de servicio de Azure

En esta sección, creará un Azure entidad de servicio que Hola usos de complemento de Maven al implementar su tooAzure de aplicación web.

1. Abra el símbolo del sistema.

1. Inicio de sesión en su cuenta de Azure mediante el uso de Hola CLI de Azure:
   ```shell
   az login
   ```
   Siga Hola instrucciones toocomplete Hola inicio de sesión en proceso.

1. Cree una entidad de servicio de Azure:
   ```shell
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
   > Utilizará valores de hello de esta respuesta JSON cuando configura hello Maven complemento toodeploy su tooAzure de aplicación web. Hola `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, y `tttttttt` son valores de marcador de posición, que son usado en este ejemplo se toomake toomap más fácil estos valores tootheir respectivos elementos cuando se configura el Maven `settings.xml` archivo Hola a continuación sección.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Configurar la entidad de seguridad de servicio de Azure de Maven toouse

En esta sección, utiliza valores de hello de la autenticación de hello tooconfigure principal de servicio de Azure que Maven usa al implementar su tooAzure de aplicación web.

1. Abra su Maven `settings.xml` un archivo en un editor de texto; este archivo puede encontrarse en una ruta de acceso como hello en los ejemplos siguientes:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Agregar la configuración de entidad de seguridad de servicio de Azure desde la sección anterior de Hola de este tutorial toohello `<servers>` colección Hola *settings.xml* archivo; por ejemplo:

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

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>OPCIONAL: Personalizar la pom.xml antes de implementar su tooAzure de aplicación web

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

Hay varios valores que se pueden modificar para hello Maven complemento y obtener una descripción detallada de cada uno de estos elementos está disponible en hello [Maven complemento para las aplicaciones Web de Azure] documentación. Dicho esto, hay varios valores que merece la pena destacar en este artículo:

Elemento | Descripción
---|---|---
`<version>` | Especifica la versión de Hola de hello [Maven complemento para las aplicaciones Web de Azure]. Debe comprobar la versión de Hola enumerada en hello [repositorio Central de Maven](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure que utilizas Hola versión más reciente.
`<authentication>` | Especifica la información de autenticación de Hola de Azure, que en este ejemplo contiene un `<serverId>` elemento que contiene `azure-auth`; Maven usa ese toolook valor valores de entidad de seguridad de servicio de Azure de hello en su Maven *settings.xml* archivo, que se define en una sección anterior de este artículo.
`<resourceGroup>` | Especifica el grupo de recursos de destino de hello, que es `maven-plugin` en este ejemplo. grupo de recursos de Hola se crea durante la implementación si aún no existe.
`<appName>` | Especifica el nombre de destino de hello para la aplicación web. En este ejemplo, es el nombre de destino de hello `maven-web-app-${maven.build.timestamp}`, donde hello `${maven.build.timestamp}` se anexa un sufijo por este conflicto de tooavoid de ejemplo. (marca de tiempo de hello es opcional; puede especificar cualquier cadena única para el nombre de la aplicación hello).
`<region>` | Especifica la región de destino de hello, que en este ejemplo es `westus`. (Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)
`<javaVersion>` | Especifica la versión de tiempo de ejecución de Java de hello para la aplicación web. (Es una lista completa de hello [Maven complemento para las aplicaciones Web de Azure] documentación.)
`<deploymentType>` | Especifica el tipo de implementación para la aplicación web. Por ahora, solo se admite `ftp`, aunque la compatibilidad con otros tipos de implementación está en la fase de desarrollo.
`<resources>` | Especifica los recursos y destinos que Maven usa al implementar su tooAzure de aplicación web. En este ejemplo, dos `<resource>` elementos especifican que Maven implementará el archivo JAR de Hola para su aplicación web y hello *web.config* archivo de proyecto de inicio de primavera de Hola.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Compilar e implementar su tooAzure de aplicación web

Una vez haya configurado todos los valores de hello en hello anteriores secciones de este artículo, está listo toodeploy su tooAzure de aplicación web. toodo por lo tanto, use Hola pasos:

1. Desde el símbolo del sistema de Hola o ventana de terminal que estaba usando anteriormente, volver a generar archivo JAR de hello mediante Maven si ha realizado los cambios toohello *pom.xml* archivo; por ejemplo:
   ```shell
   mvn clean package
   ```

1. Implementar la tooAzure de aplicación web mediante el uso de Maven; Por ejemplo:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementará su tooAzure de aplicación web; Si la aplicación web de hello aún no existe, se creará.

Cuando se ha implementado la web, será capaz de toomanage mediante hello [portal de Azure].

* La aplicación web aparecerá en **App Services**:

   ![Aplicación web en la lista de App Services de Azure Portal][AP01]

* Y Hola dirección URL para la aplicación web se mostrarán en hello **Introducción** para la aplicación web:

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

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de hello varias tecnologías descritas en este artículo, consulte Hola siguientes artículos:

* [Maven complemento para las aplicaciones Web de Azure]

* [Inicie sesión en tooAzure de hello CLI de Azure](/azure/xplat-cli-connect)

* [Cómo toouse hello Maven complemento para aplicaciones Web de Azure toodeploy una tooAzure de aplicación de arranque del muelle en contenedores](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Referencia de configuración de Maven](https://maven.apache.org/settings.html)

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
