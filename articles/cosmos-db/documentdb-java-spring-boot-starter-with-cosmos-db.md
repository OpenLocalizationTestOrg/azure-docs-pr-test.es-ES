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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="2ac2f-104">¿Cómo toouse Hola Spring arranque inicial a la API de documentos de base de datos de Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="2ac2f-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="2ac2f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2ac2f-105">Overview</span></span>

<span data-ttu-id="2ac2f-106">Hola  **[Spring Framework]**  es una solución de código abierto que ayuda a los desarrolladores de Java a crear aplicaciones de nivel empresarial.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="2ac2f-107">Uno de los proyectos de más populares de Hola que se compila sobre dicha plataforma es [arranque primavera], que proporciona un enfoque simplificado para crear aplicaciones independientes de Java.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="2ac2f-108">los desarrolladores de toohelp comenzar con el arranque de primavera, varios paquetes de arranque de primavera de ejemplo están disponibles en <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="2ac2f-109">Además toochoosing de lista de Hola de arranque básica de primavera de proyectos, hello  **[primavera Initializr]**  ayuda a los desarrolladores a empezar a trabajar con la creación de aplicaciones de arranque Spring personalizadas.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="2ac2f-110">Base de datos de Cosmos Azure es un servicio de base de datos distribuidos globalmente que permite a los desarrolladores toowork con datos mediante una variedad de API estándar, como documentos, MongoDB, gráfico y las API de tabla.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="2ac2f-111">Inicio de arranque de primavera de Microsoft permite que las aplicaciones de arranque de primavera de toouse a los desarrolladores que se integran fácilmente con base de datos de Azure Cosmos mediante el uso de DocumentDB APIs.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="2ac2f-112">Este artículo muestra cómo crear una base de datos de Azure Cosmos utilizando Hola portal de Azure, para después utilizarla hello **Initializr primavera** toocreate una aplicación java personalizado y, a continuación, agregue Hola Spring arranque Starter funcionalidad tooyour personalizado datos de la aplicación toostore en y recuperan los datos de la base de datos de Azure Cosmos utilizando Hola API de documentos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ac2f-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2ac2f-113">Prerequisites</span></span>

<span data-ttu-id="2ac2f-114">Hola siguiendo los requisitos previos es necesarios en los pasos de orden toofollow hello en este artículo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="2ac2f-115">Una suscripción de Azure. Si todavía no la tiene, puede activar sus [ventajas como suscriptor de MSDN] o registrarse para obtener una [cuenta de Azure gratuita].</span><span class="sxs-lookup"><span data-stu-id="2ac2f-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="2ac2f-116">Un [kit de desarrollo de Java (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), versión 1.7 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="2ac2f-117">[Apache Maven](http://maven.apache.org/), versión 3.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="2ac2f-118">Crear una base de datos de Azure Cosmos mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="2ac2f-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="2ac2f-119">Examinar toohello Azure portal en <https://portal.azure.com/> y haga clic en **+ nuevo**.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="2ac2f-121">Haga clic en **Bases de datos** y luego haga clic en **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="2ac2f-123">En hello **base de datos de Azure Cosmos** escriba Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="2ac2f-124">Escriba un nombre único **identificador**, que se usará como Hola URI para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="2ac2f-125">Por ejemplo, *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="2ac2f-126">Elija **SQL (base de datos de documento)** para hello API.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="2ac2f-127">Elija hello **suscripción** desea toouse para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="2ac2f-128">Especifique si toocreate un nuevo **grupo de recursos** para la base de datos o elija un grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="2ac2f-129">Especificar hello **ubicación** para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="2ac2f-130">Cuando se han especificado estas opciones, haga clic en **crear** toocreate la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="2ac2f-132">Cuando se ha creado la base de datos, se muestra en su Azure **panel**, así como en hello **todos los recursos** y **base de datos de Azure Cosmos** páginas.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="2ac2f-133">Puede hacer clic en la base de datos en cualquiera de esos página de propiedades de ubicaciones tooopen hello de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="2ac2f-135">Cuando se muestra la página de propiedades de hello para la base de datos, haga clic en **las claves de acceso** y copie las URI y claves de acceso de la base de datos; usará estos valores en la aplicación de arranque de primavera.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="2ac2f-137">Crear una sencilla aplicación de arranque de primavera con hello Initializr primavera</span><span class="sxs-lookup"><span data-stu-id="2ac2f-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="2ac2f-138">Examinar demasiado<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="2ac2f-139">Especifique que desea toogenerate una **Maven** proyecto con **Java**, escriba Hola **grupo** y **artefacto** nombres para la aplicación, y a continuación, haga clic en botón Hola demasiado**generar proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Opciones básicas de Spring Initializr][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="2ac2f-141">Hola primavera Initializr usa hello **grupo** y **artefacto** nombre del paquete de nombres toocreate Hola; por ejemplo: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="2ac2f-142">Cuando se le solicite, descargue la ruta de acceso de hello proyecto tooa en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Descarga del proyecto personalizado de Spring Boot][SI02]

1. <span data-ttu-id="2ac2f-144">Una vez extraídos los archivos de hello en el sistema local, la aplicación de arranque de primavera simple estará lista para su edición.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Archivos de proyecto personalizados de Spring Boot][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="2ac2f-146">Configurar su Hola de toouse aplicación Spring arranque inicial de arranque de primavera de Azure</span><span class="sxs-lookup"><span data-stu-id="2ac2f-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="2ac2f-147">Busque hello *pom.xml* archivo hello directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="2ac2f-148">O bien</span><span class="sxs-lookup"><span data-stu-id="2ac2f-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Busque el archivo de hello pom.xml][PM01]

1. <span data-ttu-id="2ac2f-150">Abra hello *pom.xml* un archivo en un editor de texto y agregue Hola después toolist líneas de `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Editar archivo de hello pom.xml][PM02]

1. <span data-ttu-id="2ac2f-152">Guarde y cierre hello *pom.xml* archivo.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="2ac2f-153">Configurar la base de datos de Azure Cosmos de su toouse de aplicación de arranque de primavera</span><span class="sxs-lookup"><span data-stu-id="2ac2f-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="2ac2f-154">Busque hello *application.properties* archivo Hola *recursos* directorio de la aplicación; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="2ac2f-155">O bien</span><span class="sxs-lookup"><span data-stu-id="2ac2f-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Busque el archivo de hello application.properties][RE01]

1. <span data-ttu-id="2ac2f-157">Abra hello *application.properties* un archivo en un editor de texto y agregue Hola líneas toohello archivo siguiente y reemplace los valores de ejemplo de Hola con propiedades adecuadas de hello para la base de datos:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Editar archivo de hello application.properties][RE02]

1. <span data-ttu-id="2ac2f-159">Guarde y cierre hello *application.properties* archivo.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="2ac2f-160">Agregar funcionalidad de base de datos básicos de tooimplement de código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2ac2f-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="2ac2f-161">En esta sección creará dos clases de Java para almacenar los datos de usuario y, a continuación, modifique la toocreate de clase de aplicación principal una instancia de clase de usuario de Hola y guardarlo tooyour base de datos.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="2ac2f-162">Definición de una clase básica para almacenar datos de usuario</span><span class="sxs-lookup"><span data-stu-id="2ac2f-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="2ac2f-163">Crear un nuevo archivo denominado *User.java* hello en el mismo directorio que el archivo de Java de aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="2ac2f-164">Abra hello *User.java* un archivo en un editor de texto y agregue el siguiente Hola líneas toohello archivo toodefine una clase de usuario genérica que se almacena y recupera los valores de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="2ac2f-165">Guarde y cierre hello *User.java* archivo.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="2ac2f-166">Definición de una interfaz del repositorio de datos</span><span class="sxs-lookup"><span data-stu-id="2ac2f-166">Define a data repository interface</span></span>

1. <span data-ttu-id="2ac2f-167">Crear un nuevo archivo denominado *UserRepository.java* hello en el mismo directorio que el archivo de Java de aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="2ac2f-168">Abra hello *UserRepository.java* un archivo en un editor de texto y agregue el siguiente Hola líneas toohello archivo toodefine una interfaz de repositorio del usuario que extiende la interfaz de repositorio de documentos de hello predeterminada:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="2ac2f-169">Guarde y cierre hello *UserRepository.java* archivo.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="2ac2f-170">Modificar la clase de aplicación principal de hello</span><span class="sxs-lookup"><span data-stu-id="2ac2f-170">Modify hello main application class</span></span>

1. <span data-ttu-id="2ac2f-171">Buscar archivo de Java de aplicación principal de hello en el directorio del paquete de saludo de la aplicación; Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="2ac2f-172">O bien</span><span class="sxs-lookup"><span data-stu-id="2ac2f-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Buscar archivo de hello aplicación Java][JV01]

1. <span data-ttu-id="2ac2f-174">Abrir archivo de Java de aplicación principal de hello en un editor de texto y agregue Hola líneas toohello archivo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

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

1. <span data-ttu-id="2ac2f-175">Guarde y cierre el archivo de Java de hello aplicación principal.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="2ac2f-176">Compilación y prueba de la aplicación</span><span class="sxs-lookup"><span data-stu-id="2ac2f-176">Build and test your app</span></span>

1. <span data-ttu-id="2ac2f-177">Abra un símbolo del sistema y cambie la carpeta toohello del directorio donde el *pom.xml* está ubicado archivo; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="2ac2f-178">O bien</span><span class="sxs-lookup"><span data-stu-id="2ac2f-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="2ac2f-179">Compile la aplicación de Spring Boot con Maven y ejecútela; por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="2ac2f-180">La aplicación mostrará varios mensajes de tiempo de ejecución, y debe aparecer un mensaje Hola `User: testFirstName testLastName` tooindicate que los valores se han almacenado correctamente y se recuperan de la base de datos de muestra.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Salida correcta de la aplicación hello][JV02]

1. <span data-ttu-id="2ac2f-182">OPCIONAL: Puede usar contenido de Hola Hola tooview portal Azure de la base de datos de Azure Cosmos desde la página de propiedades de hello para la base de datos haciendo clic en **Document Explorer**y, a continuación, seleccionar y elemento de Hola de hello muestra lista tooview contenido.</span><span class="sxs-lookup"><span data-stu-id="2ac2f-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Con hello Document Explorer tooview sus datos][JV03]

## <a name="next-steps"></a><span data-ttu-id="2ac2f-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2ac2f-184">Next steps</span></span>

<span data-ttu-id="2ac2f-185">Para obtener más información sobre el uso de la base de datos de Azure Cosmos y Java, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="2ac2f-186">[Documentación sobre Azure Cosmos DB]</span><span class="sxs-lookup"><span data-stu-id="2ac2f-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="2ac2f-187">[Base de datos de Cosmos Azure: Compilar una aplicación de API de documentos con Java y Hola portal de Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="2ac2f-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="2ac2f-188">Para obtener más información sobre el uso de las aplicaciones de arranque del muelle en Azure, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="2ac2f-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* <span data-ttu-id="2ac2f-189">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample) (Spring Boot DocumenDB Starter para Azure)</span><span class="sxs-lookup"><span data-stu-id="2ac2f-189">[Spring Boot DocumenDB Starter for Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)</span></span>

* [<span data-ttu-id="2ac2f-190">Implementar un servicio de aplicaciones de Azure de aplicación de arranque Spring toohello</span><span class="sxs-lookup"><span data-stu-id="2ac2f-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="2ac2f-191">Ejecuta una aplicación de arranque del muelle en un Kubernetes clúster en hello servicio de contenedor de Azure</span><span class="sxs-lookup"><span data-stu-id="2ac2f-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="2ac2f-192">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure] hello y [herramientas de Java para Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="2ac2f-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

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
