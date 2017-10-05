---
title: Tutorial de desarrollo de aplicaciones Java con Azure Cosmos DB | Microsoft Docs
description: "En este tutorial de aplicaciones web de Java, aprenderá a usar Azure Cosmos DB y la API de DocumentDB para almacenar datos y acceder a ellos desde una aplicación de Java hospedada en Azure Websites."
keywords: Application development, database tutorial, java application, java web application tutorial, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="69c34-104">Compilación de una aplicación web de Java mediante Azure Cosmos DB y la API de DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="69c34-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69c34-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69c34-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="69c34-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="69c34-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="69c34-107">Java</span><span class="sxs-lookup"><span data-stu-id="69c34-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="69c34-108">Python</span><span class="sxs-lookup"><span data-stu-id="69c34-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="69c34-109">En este tutorial de aplicación web Java aprenderá a usar el servicio [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) para almacenar datos y acceder a ellos desde una aplicación de Java hospedada en Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="69c34-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="69c34-110">En este tema, aprenderá:</span><span class="sxs-lookup"><span data-stu-id="69c34-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="69c34-111">Cómo crear una aplicación de JavaServer Pages (JSP) básica en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69c34-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="69c34-112">Cómo trabajar con el servicio Azure Cosmos DB con el [SDK de Java de Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="69c34-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="69c34-113">Este tutorial de aplicación Java muestra cómo crear una aplicación de administración de tareas basadas en web que permite crear, recuperar y marcar tareas como completadas, tal como se muestra en la siguiente imagen.</span><span class="sxs-lookup"><span data-stu-id="69c34-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="69c34-114">Las tareas de la lista ToDo se almacenan como documentos JSON en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69c34-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplicación Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="69c34-116">En este tutorial de desarrollo de aplicaciones se supone que tiene experiencia anterior en el uso de Java.</span><span class="sxs-lookup"><span data-stu-id="69c34-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="69c34-117">Si no está familiarizado con Java o con las [herramientas de requisitos previos](#Prerequisites), se recomienda que descargue el proyecto completo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) de GitHub y lo compile mediante las [instrucciones que se encuentran al final de este artículo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="69c34-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="69c34-118">Una vez compilado, puede revisar el artículo para obtener información sobre el código en el contexto del proyecto.</span><span class="sxs-lookup"><span data-stu-id="69c34-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="69c34-119"><a id="Prerequisites"></a>Requisitos previos para este tutorial de aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="69c34-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="69c34-120">Antes de comenzar este tutorial de desarrollo de aplicaciones, debe disponer de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69c34-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="69c34-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="69c34-121">An active Azure account.</span></span> <span data-ttu-id="69c34-122">En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="69c34-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="69c34-123">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="69c34-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="69c34-124">OR</span><span class="sxs-lookup"><span data-stu-id="69c34-124">OR</span></span>

    <span data-ttu-id="69c34-125">Una instalación local del [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="69c34-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="69c34-126"><seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg></span><span class="sxs-lookup"><span data-stu-id="69c34-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="69c34-127">IDE de Eclipse para desarrolladores de Java EE.</span><span class="sxs-lookup"><span data-stu-id="69c34-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="69c34-128">Un sitio web de Azure con un entorno de tiempo de ejecución Java (por ejemplo, Tomcat o Jetty) habilitado.</span><span class="sxs-lookup"><span data-stu-id="69c34-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="69c34-129">Si va a instalar estas herramientas por primera vez, coreservlets.com proporciona un ejemplo paso a paso del proceso de instalación en la sección de inicio rápido de su artículo [Tutorial: Instalación de TomCat7 y uso con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) .</span><span class="sxs-lookup"><span data-stu-id="69c34-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="69c34-130"><a id="CreateDB"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="69c34-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="69c34-131">Para comenzar, creemos una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69c34-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="69c34-132">Si ya tiene una cuenta o si usa el Emulador de Azure Cosmos DB para este tutorial, puede ir directamente al [Paso 2: Creación de la aplicación de Java JSP](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="69c34-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="69c34-133"><a id="CreateJSP"></a>Paso 2: Creación de la aplicación JSP de Java</span><span class="sxs-lookup"><span data-stu-id="69c34-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="69c34-134">Para crear la aplicación JSP:</span><span class="sxs-lookup"><span data-stu-id="69c34-134">To create the JSP application:</span></span>

1. <span data-ttu-id="69c34-135">En primer lugar, empezaremos por la creación de un proyecto Java.</span><span class="sxs-lookup"><span data-stu-id="69c34-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="69c34-136">Inicie Eclipse, haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).</span><span class="sxs-lookup"><span data-stu-id="69c34-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="69c34-137">Si **Dynamic Web Project** (Proyecto web dinámico) no aparece como proyecto disponible, haga lo siguiente: haga clic en **File** (Archivo), **New** (Nuevo), **Project** (Proyecto), expanda **Web**, haga clic en **Dynamic Web Project** (Proyecto web dinámico) y haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Desarrollo de aplicaciones Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="69c34-139">Escriba un nombre de proyecto en el cuadro **Project name** (Nombre de proyecto) y en el menú desplegable **Target Runtime** (Tiempo de ejecución de destino), seleccione opcionalmente un valor (por ejemplo, Apache Tomcat v7.0) y, a continuación, haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="69c34-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="69c34-140">Si selecciona un tiempo de ejecución de destino, puede ejecutar el proyecto localmente a través de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="69c34-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="69c34-141">En Eclipse, en la vista del explorador de proyectos, expanda el proyecto.</span><span class="sxs-lookup"><span data-stu-id="69c34-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="69c34-142">Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="69c34-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="69c34-143">En el cuadro de diálogo **New JSP File** (Nuevo archivo JSP), asigne al archivo el nombre **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="69c34-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="69c34-144">Mantenga la carpeta principal como **WebContent**, como se muestra en la ilustración siguiente y, a continuación, haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Creación de un nuevo archivo JSP - Tutorial de aplicación web de Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="69c34-146">En el cuadro de diálogo **Select JSP Template** (Seleccionar plantilla JSP), para cumplir con el objetivo de este tutorial, seleccione **New JSP File (html)** (Nuevo archivo JSP [html]) y haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="69c34-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="69c34-147">Cuando el archivo index.jsp se abra en Eclipse, agregue texto para mostrar **Hola a todos** dentro del elemento existente.</span><span class="sxs-lookup"><span data-stu-id="69c34-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="69c34-148">dentro del elemento <body> existente.</span><span class="sxs-lookup"><span data-stu-id="69c34-148">within the existing <body> element.</span></span> <span data-ttu-id="69c34-149">El contenido actualizado <body> debe ser similar al código siguiente:</span><span class="sxs-lookup"><span data-stu-id="69c34-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="69c34-150">Guarde el archivo index.jsp.</span><span class="sxs-lookup"><span data-stu-id="69c34-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="69c34-151">Si ha establecido un tiempo de ejecución de destino en el paso 2, puede hacer clic en **Project** (Proyecto) y, a continuación, en **Run** (Ejecutar) para ejecutar su aplicación de JSP localmente:</span><span class="sxs-lookup"><span data-stu-id="69c34-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World – Tutorial de aplicación de Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="69c34-153"><a id="InstallSDK"></a>Paso 3: Instalación del SDK de Java de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="69c34-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="69c34-154">La manera más sencilla de insertar el SDK de Java de DocumentDB y sus dependencias es a través de [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="69c34-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="69c34-155">Para ello, deberá convertir su proyecto en un proyecto Maven realizando los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="69c34-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="69c34-156">Haga clic con el botón derecho en el proyecto en el explorador de proyectos, haga clic en **Configure** (Configurar) y en **Convert to Maven Project** (Convertir en proyecto Maven).</span><span class="sxs-lookup"><span data-stu-id="69c34-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="69c34-157">En la ventana **Crear nueva POM**, acepte los valores predeterminados y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="69c34-158">En **Explorador de proyectos**, abra el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="69c34-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="69c34-159">En la ficha **Dependencias**, en el panel **Dependencias**, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="69c34-160">En la ventana **Seleccionar dependencia** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69c34-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="69c34-161">En el cuadro **GroupId**, escriba com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="69c34-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="69c34-162">En el cuadro **Id. de artefacto**, escriba azure-documentdb.</span><span class="sxs-lookup"><span data-stu-id="69c34-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="69c34-163">En el cuadro **Versión**, escriba 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="69c34-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![Instalación del SDK de la aplicación Java en DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="69c34-165">O bien, agregue el XML de dependencia para identificador de grupo y un identificador de artefacto directamente al archivo pom.xml mediante un editor de texto:</span><span class="sxs-lookup"><span data-stu-id="69c34-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="69c34-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span><span class="sxs-lookup"><span data-stu-id="69c34-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="69c34-167">Haga clic en **Aceptar** y Maven instalará el SDK de Java de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="69c34-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="69c34-168">Guarde el archivo pom.xml.</span><span class="sxs-lookup"><span data-stu-id="69c34-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="69c34-169"><a id="UseService"></a>Paso 4: Uso del servicio Azure Cosmos DB en una aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="69c34-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="69c34-170">En primer lugar, vamos a definir el objeto TodoItem en TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="69c34-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="69c34-171">En este proyecto, estamos usando [Project Lombok](http://projectlombok.org/) para generar el constructor, los captadores, los establecedores y un generador.</span><span class="sxs-lookup"><span data-stu-id="69c34-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="69c34-172">Como alternativa, puede escribir este código manualmente o dejar que el IDE lo genere.</span><span class="sxs-lookup"><span data-stu-id="69c34-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="69c34-173">Para invocar el servicio Azure Cosmos DB, debe crear una nueva instancia de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="69c34-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="69c34-174">En general, es mejor volver a utilizar **DocumentClient** , en lugar de construir un nuevo cliente para cada solicitud posterior.</span><span class="sxs-lookup"><span data-stu-id="69c34-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="69c34-175">Podemos volver a usar el cliente ajustando el cliente en una **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="69c34-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="69c34-176">En DocumentClientFactory.java, tendrá que pegar el valor URI y CLAVE PRINCIPAL que guardó en el portapapeles en el [paso 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="69c34-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="69c34-177">Reemplace [YOUR\_ENDPOINT\_HERE] por el URI y reemplace [YOUR\_KEY\_HERE] por su CLAVE PRINCIPAL.</span><span class="sxs-lookup"><span data-stu-id="69c34-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="69c34-178">Ahora debe crear un objeto de acceso a datos (DAO) para abstraer la conservación de nuestros elementos ToDo en Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="69c34-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="69c34-179">Para guardar los elementos ToDo en una colección, el cliente necesitará saber en qué base de datos y colección se conservarán (como se hace referencia por los self-links).</span><span class="sxs-lookup"><span data-stu-id="69c34-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="69c34-180">En general, es mejor almacenar en memoria caché la base de datos y la colección cuando sea posible para evitar recorridos de ida y vuelta adicionales a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="69c34-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="69c34-181">El código siguiente muestra cómo recuperar nuestra base de datos y colección si existe, o crear una nueva si no existe:</span><span class="sxs-lookup"><span data-stu-id="69c34-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="69c34-182">El siguiente paso es escribir algo de código para conservar los TodoItems en la colección.</span><span class="sxs-lookup"><span data-stu-id="69c34-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="69c34-183">En este ejemplo, usaremos [Gson](https://code.google.com/p/google-gson/) para serializar y deserializar TodoItem Plain Old Java Objects (POJO, objetos de Java antiguos sin formato de tareas pendientes) en los documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="69c34-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="69c34-184">Al igual que las colecciones y las bases de datos de Azure Cosmos DB, a los documentos también se hace referencia mediante autovínculos.</span><span class="sxs-lookup"><span data-stu-id="69c34-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="69c34-185">La siguiente función auxiliar nos permite recuperar documentos por otro atributo (por ejemplo, "id") en lugar del self-link:</span><span class="sxs-lookup"><span data-stu-id="69c34-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="69c34-186">Podemos usar el método auxiliar del paso 5 para recuperar un documento JSON de TodoItem por id. y deserializarlo para un POJO:</span><span class="sxs-lookup"><span data-stu-id="69c34-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="69c34-187">También podemos utilizar el DocumentClient para obtener una colección o lista de TodoItems con SQL de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="69c34-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="69c34-188">Hay muchas maneras de actualizar un documento con el DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="69c34-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="69c34-189">En nuestra aplicación de lista Todo, queremos poder alternar si se ha completado un TodoItem.</span><span class="sxs-lookup"><span data-stu-id="69c34-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="69c34-190">Esto se logra actualizando el atributo "completado" dentro del documento:</span><span class="sxs-lookup"><span data-stu-id="69c34-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="69c34-191">Por último, queremos la capacidad de eliminar un TodoItem de nuestra lista.</span><span class="sxs-lookup"><span data-stu-id="69c34-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="69c34-192">Para ello, podemos utilizar el método auxiliar que hemos escrito anteriormente para recuperar el self-link y, a continuación, indicar al cliente que lo elimine:</span><span class="sxs-lookup"><span data-stu-id="69c34-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="69c34-193"><a id="Wire"></a>Paso 5: Reunión del resto del proyecto de desarrollo de aplicación en Java</span><span class="sxs-lookup"><span data-stu-id="69c34-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="69c34-194">Ahora que hemos terminado la parte divertida, todo lo que queda por hacer es crear una interfaz de usuario rápida y conectarla a nuestro DAO.</span><span class="sxs-lookup"><span data-stu-id="69c34-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="69c34-195">En primer lugar, empecemos por crear un controlador para llamar a nuestro DAO:</span><span class="sxs-lookup"><span data-stu-id="69c34-195">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="69c34-196">En una aplicación más compleja, el controlador puede alojar lógica empresarial complicada encima del DAO.</span><span class="sxs-lookup"><span data-stu-id="69c34-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="69c34-197">A continuación, crearemos un servlet para enrutar las solicitudes HTTP al controlador:</span><span class="sxs-lookup"><span data-stu-id="69c34-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="69c34-198">Necesitaremos una interfaz de usuario web que mostrar al usuario.</span><span class="sxs-lookup"><span data-stu-id="69c34-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="69c34-199">Vamos volver a escribir el archivo index.jsp que creamos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="69c34-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="69c34-200">Y por último, escriba algo de JavaScript del lado del cliente para vincular juntos la interfaz de usuario web y el servlet:</span><span class="sxs-lookup"><span data-stu-id="69c34-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="69c34-201">¡Increíble!</span><span class="sxs-lookup"><span data-stu-id="69c34-201">Awesome!</span></span> <span data-ttu-id="69c34-202">Ahora todo lo que queda por hacer es probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="69c34-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="69c34-203">Ejecute la aplicación localmente y agregue algunos elementos Todo rellenando el nombre del elemento y la categoría y haciendo clic en **Agregar tarea**.</span><span class="sxs-lookup"><span data-stu-id="69c34-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="69c34-204">Una vez que aparece el elemento, puede actualizar si está completo. Para ello, alterne la casilla y haga clic en **Actualizar tareas**.</span><span class="sxs-lookup"><span data-stu-id="69c34-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="69c34-205"><a id="Deploy"></a>Paso 6: Implementación de la aplicación Java en Azure WebSites</span><span class="sxs-lookup"><span data-stu-id="69c34-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="69c34-206">Azure WebSites consigue que la implementación de aplicaciones de Java sea tan sencilla como exportar su aplicación como un archivo WAR y cargarla mediante el control de código fuente (por ejemplo, Git) o FTP.</span><span class="sxs-lookup"><span data-stu-id="69c34-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="69c34-207">Para exportar la aplicación como un archivo WAR, haga clic con el botón derecho en el proyecto en **Explorador de proyectos**, haga clic en **Exportar** y, a continuación, haga clic en **Archivo WAR**.</span><span class="sxs-lookup"><span data-stu-id="69c34-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="69c34-208">En la ventana **Exportar WAR** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69c34-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="69c34-209">En el cuadro Proyecto web, escriba azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="69c34-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="69c34-210">En el cuadro de destino, seleccione un destino para guardar el archivo WAR.</span><span class="sxs-lookup"><span data-stu-id="69c34-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="69c34-211">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="69c34-211">Click **Finish**.</span></span>
3. <span data-ttu-id="69c34-212">Ahora que tiene a mano un archivo WAR, simplemente puede cargarlo en el directorio **webapps** del sitio web de Azure.</span><span class="sxs-lookup"><span data-stu-id="69c34-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="69c34-213">Para obtener instrucciones sobre cómo cargar el archivo, consulte [Adición de una aplicación Java a Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="69c34-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="69c34-214">Una vez que se cargue el archivo WAR en el directorio webapps, el entorno de tiempo de ejecución detectará que lo ha agregado y lo cargará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="69c34-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="69c34-215">Para ver el producto terminado, vaya a http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ y comience a agregar las tareas.</span><span class="sxs-lookup"><span data-stu-id="69c34-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="69c34-216"><a id="GetProject"></a>Obtenga el proyecto desde GitHub</span><span class="sxs-lookup"><span data-stu-id="69c34-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="69c34-217">Todos los ejemplos de este tutorial se incluyen en el proyecto [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) en GitHub.</span><span class="sxs-lookup"><span data-stu-id="69c34-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="69c34-218">Para importar el proyecto todo en Eclipse, asegúrese de disponer del software y los recursos que aparecen en la sección [Requisitos previos](#Prerequisites) y haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="69c34-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="69c34-219">Instale [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="69c34-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="69c34-220">Lombok se utiliza para generar constructores, captadores y establecedores en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="69c34-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="69c34-221">Una vez haya descargado el archivo lombok.jar, haga doble clic en él para instalarlo o instálelo desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="69c34-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="69c34-222">Si Eclipse está abierto, ciérrelo y reinícielo para cargar Lombok.</span><span class="sxs-lookup"><span data-stu-id="69c34-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="69c34-223">En Eclipse, en el menú **File** (Archivo), haga clic en **Import** (Importar).</span><span class="sxs-lookup"><span data-stu-id="69c34-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="69c34-224">En la ventana **Import** (Importar), haga clic en **Git**, en **Projects from Git** (Proyectos de Git) y luego en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="69c34-225">En la pantalla **Select Repository Source** (Seleccionar origen del repositorio), haga clic en **Clone URI** (Clonar URI).</span><span class="sxs-lookup"><span data-stu-id="69c34-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="69c34-226">En la pantalla **Source Git Repository** (Repositorio Git de origen), en el cuadro **URI**, escriba https://github.com/Azure-Samples/java-todo-app.git y luego haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="69c34-227">En la pantalla **Branch Selection** (Selección de rama), asegúrese de que está seleccionado **master** (principal) y luego haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="69c34-228">En la pantalla **Local Destination** (Destino local), haga clic en **Browse** (Examinar) para seleccionar una carpeta donde se pueda copiar el repositorio y luego haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="69c34-229">En la pantalla **Select a wizard to use for importing projects** (Seleccionar un asistente para usar en la importación de proyectos), asegúrese de que la opción **Import existing projects** (Importar proyectos existentes) esté seleccionada y luego haga clic en **Next** (Siguiente).</span><span class="sxs-lookup"><span data-stu-id="69c34-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="69c34-230">En la pantalla **Import Projects** (Proyectos de importación), anule la selección del proyecto **DocumentDB** y luego haga clic en **Finish** (Finalizar).</span><span class="sxs-lookup"><span data-stu-id="69c34-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="69c34-231">El proyecto DocumentDB contiene el SDK de Java de Azure Cosmos DB, que se agregará como dependencia.</span><span class="sxs-lookup"><span data-stu-id="69c34-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="69c34-232">En **explorador de proyectos**, vaya a azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java y reemplace los valores HOST y MASTER_KEY por los de URI y PRIMARY KEY de la cuenta de Azure Cosmos DB y luego guarde el archivo.</span><span class="sxs-lookup"><span data-stu-id="69c34-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="69c34-233">Para obtener más información, consulte el [paso 1. Creación de una cuenta de base de datos de Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="69c34-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="69c34-234">En **Project Explorer** (Explorador de proyectos), haga clic con el botón derecho en **azure-documentdb-java-sample**, haga clic en **Build Path** (Ruta de acceso de compilación) y luego haga clic en **Configure Build Path** (Configurar ruta de acceso de compilación).</span><span class="sxs-lookup"><span data-stu-id="69c34-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="69c34-235">En la pantalla **Java Build Path** (Ruta de compilación de Java), en el panel derecho, seleccione la pestaña **Bibliotecas** y luego haga clic en **Add External JARs** (Agregar JAR externos).</span><span class="sxs-lookup"><span data-stu-id="69c34-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="69c34-236">Desplácese hasta la ubicación del archivo lombok.jar y haga clic en **Abrir** y, a continuación, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="69c34-237">Use el paso 12 para abrir la ventana **Propiedades** de nuevo y, a continuación, en el panel izquierdo haga clic en **Targeted Runtimes** (Tiempos de ejecución de destino).</span><span class="sxs-lookup"><span data-stu-id="69c34-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="69c34-238">En la pantalla **Targeted Runtimes** (Tiempos de ejecución de destino), haga clic en **Nuevo**, seleccione **Apache Tomcat v7.0** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="69c34-239">Use el paso 12 para abrir de nuevo la ventana **Propiedades** y, a continuación, en el panel izquierdo, haga clic en **Project Facets** (Facetas del proyecto).</span><span class="sxs-lookup"><span data-stu-id="69c34-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="69c34-240">En la pantalla **Project Facets** (Facetas del proyecto), seleccione **Dynamic Web Module** (Módulo web dinámico) y **Java** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="69c34-241">En la ficha **Servidores** en la parte inferior de la pantalla, haga clic con el botón derecho en **Tomcat v7.0 Server at localhost** (Tomcat v7.0 Server en localhost) y luego haga clic en **Add and Remove** (Agregar y quitar).</span><span class="sxs-lookup"><span data-stu-id="69c34-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="69c34-242">En la ventana **Agregar y quitar**, mueva **azure-documentdb-java-sample** al cuadro **Configurado** y luego haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="69c34-243">En la pestaña **Servidor**, haga clic en **Tomcat v7.0 Server at localhost** (Tomcat v7.0 Server en localhost) y luego haga clic en **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="69c34-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="69c34-244">En un explorador, vaya a http://localhost:8080/azure-documentdb-java-sample/ y comience a agregar a la lista de tareas.</span><span class="sxs-lookup"><span data-stu-id="69c34-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="69c34-245">Tenga en cuenta que si ha cambiado los valores de puerto predeterminados, debe cambiar 8080 por el valor seleccionado.</span><span class="sxs-lookup"><span data-stu-id="69c34-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="69c34-246">Para implementar el proyecto en un sitio web de Azure, consulte el [paso 6. Implementación de la aplicación para Azure WebSites](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="69c34-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
