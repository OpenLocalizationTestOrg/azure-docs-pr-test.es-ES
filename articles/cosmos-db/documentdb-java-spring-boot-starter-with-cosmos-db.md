---
title: aaaHow toouse Hola Spring arranque inicio con una API de documentos de base de datos de Azure Cosmos
description: "Obtenga información acerca de cómo tooconfigure una aplicación crea con hello Spring arranque inicializador con hello Azure Cosmos DB documentos API."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring Boot Starter, Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>¿Cómo toouse Hola Spring arranque inicial a la API de documentos de base de datos de Azure Cosmos

## <a name="overview"></a>Información general

Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial. Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java. los desarrolladores de toohelp comenzar con el arranque de primavera, varios paquetes de arranque de primavera de ejemplo están disponibles en <https://github.com/spring-guides/>. Además toochoosing de lista de Hola de arranque básica de primavera de proyectos, hello  **[primavera Initializr]**  ayuda a los desarrolladores a empezar a trabajar con la creación de aplicaciones de arranque Spring personalizadas.

Base de datos de Cosmos Azure es un servicio de base de datos distribuidos globalmente que permite a los desarrolladores toowork con datos mediante una variedad de API estándar, como documentos, MongoDB, gráfico y las API de tabla. Inicio de arranque de primavera de Microsoft permite que las aplicaciones de arranque de primavera de toouse a los desarrolladores que se integran fácilmente con base de datos de Azure Cosmos mediante el uso de DocumentDB APIs.

Este artículo muestra cómo crear una base de datos de Azure Cosmos utilizando Hola portal de Azure, para después utilizarla hello **Initializr primavera** toocreate una aplicación java personalizado y, a continuación, agregue Hola Spring arranque Starter funcionalidad tooyour personalizado datos de la aplicación toostore en y recuperan los datos de la base de datos de Azure Cosmos utilizando Hola API de documentos.

## <a name="prerequisites"></a>Requisitos previos

Hola siguiendo los requisitos previos es necesarios en los pasos de orden toofollow hello en este artículo:

* Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].

* Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.

* [Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Crear una base de datos de Azure Cosmos mediante Hola portal de Azure

1. Examinar toohello Azure portal en <https://portal.azure.com/> y haga clic en **+ nuevo**.

   ![Azure Portal][AZ01]

1. Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.

   ![Azure Portal][AZ02]

1. En hello **base de datos de Azure Cosmos** escriba Hola siguiente información:

   * Escriba un nombre único **identificador**, que se usará como Hola URI para la base de datos. Por ejemplo, *wingtiptoysdata.documents.azure.com*.
   * Elija **SQL (base de datos de documento)** para hello API.
   * Elija hello **suscripción** desea toouse para la base de datos.
   * Especifique si toocreate un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos existente.
   * Especificar hello **ubicación** para la base de datos.
   
   Cuando se han especificado estas opciones, haga clic en **crear** toocreate la base de datos.

   ![Azure Portal][AZ03]

1. Cuando se ha creado la base de datos, se muestra en su Azure **panel**, así como en hello **todos los recursos** y **base de datos de Azure Cosmos** páginas. Puede hacer clic en la base de datos en cualquiera de esos página de propiedades de ubicaciones tooopen hello de la memoria caché.

   ![Azure Portal][AZ04]

1. Cuando se muestra la página de propiedades de hello para la base de datos, haga clic en **las claves de acceso** y copie las URI y claves de acceso de la base de datos; usará estos valores en la aplicación de arranque de primavera.

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Crear una sencilla aplicación de arranque de primavera con hello Initializr primavera

1. Examinar demasiado<https://start.spring.io/>.

1. Especifique que desea toogenerate una **Maven** proyecto con **Java**, escriba Hola **grupo** y **artefacto** nombres para la aplicación, y a continuación, haga clic en botón Hola demasiado**generar proyecto**.

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > Hola primavera Initializr usa hello **grupo** y **artefacto** nombre del paquete de nombres toocreate Hola; por ejemplo: *com.example.wintiptoys*.
   >

1. Cuando se le solicite, descargue la ruta de acceso de hello proyecto tooa en el equipo local.

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. Una vez extraídos los archivos de hello en el sistema local, la aplicación de arranque de primavera simple estará lista para su edición.

   ![Archivos de proyecto personalizados de Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Configurar su Hola de toouse aplicación Spring arranque inicial de arranque de primavera de Azure

1. Busque hello *pom.xml* archivo hello directorio de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   O bien

   `/users/example/home/wingtiptoys/pom.xml`

   ![Busque el archivo de hello pom.xml][PM01]

1. Abra hello *pom.xml* un archivo en un editor de texto y agregue Hola después toolist líneas de `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Editar archivo de hello pom.xml][PM02]

1. Guarde y cierre hello *pom.xml* archivo.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Configurar la base de datos de Azure Cosmos de su toouse de aplicación de arranque de primavera

1. Busque hello *application.properties* archivo Hola *recursos* directorio de la aplicación; por ejemplo:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   O bien

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Busque el archivo de hello application.properties][RE01]

1. Abra hello *application.properties* un archivo en un editor de texto y agregue Hola líneas toohello archivo siguiente y reemplace los valores de ejemplo de Hola con propiedades adecuadas de hello para la base de datos:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Editar archivo de hello application.properties][RE02]

1. Guarde y cierre hello *application.properties* archivo.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Agregar funcionalidad de base de datos básicos de tooimplement de código de ejemplo

En esta sección creará dos clases de Java para almacenar los datos de usuario y, a continuación, modifique la toocreate de clase de aplicación principal una instancia de clase de usuario de Hola y guardarlo tooyour base de datos.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definición de una clase básica para almacenar datos de usuario

1. Crear un nuevo archivo denominado *User.java* hello en el mismo directorio que el archivo de Java de aplicación principal.

1. Abra hello *User.java* un archivo en un editor de texto y agregue el siguiente Hola líneas toohello archivo toodefine una clase de usuario genérica que se almacena y recupera los valores de la base de datos:

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. Guarde y cierre hello *User.java* archivo.

### <a name="define-a-data-repository-interface"></a>Definición de una interfaz del repositorio de datos

1. Crear un nuevo archivo denominado *UserRepository.java* hello en el mismo directorio que el archivo de Java de aplicación principal.

1. Abra hello *UserRepository.java* un archivo en un editor de texto y agregue el siguiente Hola líneas toohello archivo toodefine una interfaz de repositorio del usuario que extiende la interfaz de repositorio de documentos de hello predeterminada:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Guarde y cierre hello *UserRepository.java* archivo.

### <a name="modify-hello-main-application-class"></a>Modificar la clase de aplicación principal de hello

1. Buscar archivo de Java de aplicación principal de hello en el directorio del paquete de saludo de la aplicación; Por ejemplo:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   O bien

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Buscar archivo de hello aplicación Java][JV01]

1. Abrir archivo de Java de aplicación principal de hello en un editor de texto y agregue Hola líneas toohello archivo siguiente:

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. Guarde y cierre el archivo de Java de hello aplicación principal.

## <a name="build-and-test-your-app"></a>Compilación y prueba de la aplicación

1. Abra un símbolo del sistema y cambie la carpeta toohello del directorio donde el *pom.xml* está ubicado archivo; por ejemplo:

   `cd C:\SpringBoot\wingtiptoys`

   O bien

   `cd /users/example/home/wingtiptoys`

1. Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. La aplicación mostrará varios mensajes de tiempo de ejecución, y debe aparecer un mensaje Hola `User: testFirstName testLastName` tooindicate que los valores se han almacenado correctamente y se recuperan de la base de datos de muestra.

   ![Salida correcta de la aplicación hello][JV02]

1. OPCIONAL: Puede usar contenido de Hola Hola tooview portal Azure de la base de datos de Azure Cosmos desde la página de propiedades de hello para la base de datos haciendo clic en **Document Explorer**y, a continuación, seleccionar y elemento de Hola de hello muestra lista tooview contenido.

   ![Con hello Document Explorer tooview sus datos][JV03]

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el uso de la base de datos de Azure Cosmos y Java, vea Hola siguientes artículos:

* [Documentación sobre Azure Cosmos DB]

* [Base de datos de Cosmos Azure: Compilar una aplicación de API de documentos con Java y Hola portal de Azure][Build a DocumentDB API app with Java]

Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:

* [Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Spring Boot DocumenDB Starter para Azure)

* [Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Ejecuta una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].

<!-- URL List -->

[Documentación sobre Azure Cosmos DB]: /azure/cosmos-db/
[Centro para desarrolladores de Java de Azure]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[cuenta de Azure gratuita]: https://azure.microsoft.com/pricing/free-trial/
[herramientas de Java para Visual Studio Team Services]: https://java.visualstudio.com/
[ventajas como suscriptor de MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[arranque primavera]: http://projects.spring.io/spring-boot/
[primavera Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
