---
title: tutorial de desarrollo de aplicaciones aaaJava con la base de datos de Azure Cosmos | Documentos de Microsoft
description: "Este tutorial de aplicación web de Java muestra cómo toouse Hola base de datos de Azure Cosmos Hola toostore de API de documentos y obtener acceso a datos desde una aplicación de Java hospedada en sitios Web de Azure."
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
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="c9eb5-104">Compilar una aplicación web de Java con base de datos de Azure Cosmos y Hola API de documentos</span><span class="sxs-lookup"><span data-stu-id="c9eb5-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c9eb5-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c9eb5-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="c9eb5-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="c9eb5-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="c9eb5-107">Java</span><span class="sxs-lookup"><span data-stu-id="c9eb5-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="c9eb5-108">Python</span><span class="sxs-lookup"><span data-stu-id="c9eb5-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="c9eb5-109">Este tutorial de aplicación web de Java muestra cómo hello toouse [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) servicio toostore y acceso a los datos desde una aplicación de Java que se hospeda en aplicaciones de Web del servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="c9eb5-110">En este tema, aprenderá:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="c9eb5-111">¿Cómo toobuild una aplicación básica de JavaServer Pages (JSP) en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="c9eb5-112">Cómo toowork con base de datos de Azure Cosmos hello service utilizando hello [SDK de Java de base de datos de Azure Cosmos](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="c9eb5-113">Este tutorial de la aplicación de Java muestra cómo las tareas de aplicación de administración de tareas de toocreate basada en web que permite marcar, recuperar y se toocreate como completada, tal como se muestra en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="c9eb5-114">Cada una de las tareas de hello en la lista de tareas de Hola se almacenan como documentos JSON en la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![Aplicación Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="c9eb5-116">En este tutorial de desarrollo de aplicaciones se supone que tiene experiencia anterior en el uso de Java.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="c9eb5-117">Si es nuevo tooJava o hello [herramientas requisitos previos](#Prerequisites), le recomendamos que descargue Hola completa [tareas](https://github.com/Azure-Samples/documentdb-java-todo-app) proyecto desde GitHub y compilarlas mediante [Hola instrucciones final Hola de este artículo](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="c9eb5-118">Una vez que se generan, puede revisar una visión general de hello artículo toogain en código de hello en contexto de Hola de proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="c9eb5-119"><a id="Prerequisites"></a>Requisitos previos para este tutorial de aplicación web de Java</span><span class="sxs-lookup"><span data-stu-id="c9eb5-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="c9eb5-120">Antes de empezar este tutorial de desarrollo de aplicaciones, debe tener el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c9eb5-121">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-121">An active Azure account.</span></span> <span data-ttu-id="c9eb5-122">En caso de no tener cuenta, puede crear una de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c9eb5-123">Para más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="c9eb5-124">OR</span><span class="sxs-lookup"><span data-stu-id="c9eb5-124">OR</span></span>

    <span data-ttu-id="c9eb5-125">Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="c9eb5-126"><seg>
  [Kit de desarrollo de Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</seg></span><span class="sxs-lookup"><span data-stu-id="c9eb5-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="c9eb5-127">IDE de Eclipse para desarrolladores de Java EE.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="c9eb5-128">Un sitio web de Azure con un entorno de tiempo de ejecución Java (por ejemplo, Tomcat o Jetty) habilitado.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="c9eb5-129">Si va a instalar estas herramientas para hello primera vez, coreservlets.com proporciona un ejemplo paso a paso del proceso de instalación de hello en la sección de inicio rápido de Hola de sus [Tutorial: instalar TomCat7 y su uso con Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artículo.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="c9eb5-130"><a id="CreateDB"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9eb5-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="c9eb5-131">Para comenzar, creemos una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="c9eb5-132">Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear la aplicación de Java JSP hello](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="c9eb5-133"><a id="CreateJSP"></a>Paso 2: Crear la aplicación de Java JSP hello</span><span class="sxs-lookup"><span data-stu-id="c9eb5-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="c9eb5-134">Hola toocreate aplicación JSP:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="c9eb5-135">En primer lugar, empezaremos por la creación de un proyecto Java.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="c9eb5-136">Inicie Eclipse, haga clic en **File** (Archivo), haga clic en **New** (Nuevo) y luego haga clic en **Dynamic Web Project** (Proyecto web dinámico).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="c9eb5-137">Si no ve **Dynamic Web Project** aparece como proyecto disponible, Hola siguientes: haga clic en **archivo**, haga clic en **New**, haga clic en **proyecto**..., expanda **Web**, haga clic en **Dynamic Web Project**y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![Desarrollo de aplicaciones Java JSP](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="c9eb5-139">Escriba un nombre de proyecto en hello **nombre del proyecto** cuadro y en hello **en tiempo de ejecución de destino** menú desplegable, seleccione opcionalmente un valor (por ejemplo, Apache Tomcat v7.0) y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="c9eb5-140">Al seleccionar un tiempo de ejecución de destino permite toorun el proyecto de forma local a través de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="c9eb5-141">En Eclipse, en la vista de explorador de proyectos de hello, expanda el proyecto.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="c9eb5-142">Haga clic con el botón derecho en **WebContent**, haga clic en **New** (Nuevo) y, después, en **JSP File** (Archivo JSP).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="c9eb5-143">Hola **New JSP File** cuadro de diálogo, archivo de nombre hello **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="c9eb5-144">Mantenga la carpeta principal de hello como **WebContent**, tal y como se muestra en Hola la siguiente ilustración y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Creación de un nuevo archivo JSP - Tutorial de aplicación web de Java](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="c9eb5-146">Hola **Select JSP Template** cuadro de diálogo, a fin de Hola de este tutorial, seleccione **New JSP File (html)**y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="c9eb5-147">Cuando se abre el archivo index.jsp de hello en Eclipse, agregar texto toodisplay **Hola a todos!**</span><span class="sxs-lookup"><span data-stu-id="c9eb5-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="c9eb5-148">dentro de hello existente <body> elemento.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-148">within hello existing <body> element.</span></span> <span data-ttu-id="c9eb5-149">Su actualizada <body> contenido debería ser similar a Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="c9eb5-150">Guarde el archivo index.jsp de hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="c9eb5-151">Si establece un tiempo de ejecución de destino en el paso 2, haga clic en **proyecto** y, a continuación, **ejecutar** toorun localmente la aplicación JSP:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World – Tutorial de aplicación de Java](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="c9eb5-153"><a id="InstallSDK"></a>Paso 3: Instalar Hola SDK de Java de documentos</span><span class="sxs-lookup"><span data-stu-id="c9eb5-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="c9eb5-154">Hola toopull de manera más fácil de hello SDK de Java de documentos y sus dependencias es a través de [Maven Apache](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="c9eb5-155">toodo esto, necesitará tooconvert los proyectos de maven tooa siguiendo los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="c9eb5-156">Haga clic en el proyecto en el Explorador de proyectos de Hola, haga clic en **configurar**, haga clic en **convertir tooMaven proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="c9eb5-157">Hola **crear nueva POM** ventana, acepte los valores predeterminados de Hola y haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="c9eb5-158">En **el Explorador de proyectos**, abra archivos de pom.xml Hola.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="c9eb5-159">En hello **dependencias** ficha Hola **dependencias** panel, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="c9eb5-160">Hola **seleccione dependencia** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="c9eb5-161">Hola **Id. de grupo** cuadro, escriba com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="c9eb5-162">Hola **el identificador del artefacto** cuadro, escriba documentos de azure.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="c9eb5-163">Hola **versión** cuadro, escriba 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![Instalación del SDK de la aplicación Java en DocumentDB](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="c9eb5-165">O Agregar dependencia Hola XML para el Id. de grupo y el identificador del artefacto directamente toohello pom.xml a través de un editor de texto:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="c9eb5-166"><dependency><groupId>com.microsoft.azure</groupId><artifactId>azure-documentdb</artifactId><version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="c9eb5-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="c9eb5-167">Haga clic en **Aceptar** y Maven instalará Hola SDK de Java de documentos.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="c9eb5-168">Guarde el archivo de hello pom.xml.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="c9eb5-169"><a id="UseService"></a>Paso 4: Usar servicio de base de datos de Azure Cosmos hello en una aplicación de Java</span><span class="sxs-lookup"><span data-stu-id="c9eb5-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="c9eb5-170">En primer lugar, vamos a definir objeto TodoItem de hello en TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="c9eb5-171">En este proyecto, usamos [proyecto Lombok](http://projectlombok.org/) toogenerate Hola constructor, captadores, establecedores y un generador.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="c9eb5-172">Como alternativa, puede escribir este código manualmente o hacer Hola IDE generarlo.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="c9eb5-173">servicio de base de datos de Azure Cosmos de hello tooinvoke, debe crear instancias de un nuevo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="c9eb5-174">En general, es mejor hello tooreuse **DocumentClient** : en lugar de construir un nuevo cliente para cada solicitud subsiguiente.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="c9eb5-175">Se puede reutilizar cliente hello ajustando cliente hello en un **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="c9eb5-176">En DocumentClientFactory.java, se necesita el valor de identificador URI y la clave principal de la Hola de toopaste guardó Portapapeles tooyour en [paso 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="c9eb5-177">Reemplace [YOUR\_ENDPOINT\_HERE] por el URI y reemplace [YOUR\_KEY\_HERE] por su CLAVE PRINCIPAL.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="c9eb5-178">Ahora vamos a crear un tooabstract de objeto de acceso a datos (DAO) conservar nuestro tooAzure de elementos de lista de tareas Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="c9eb5-179">En orden toosave cuantos elementos colección tooa, Hola debe cliente tooknow qué base de datos y la colección toopersist demasiado (al que hace referencia Self-Link).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="c9eb5-180">En general, es mejor base de datos de toocache hello y colección siempre que sea posible base de datos de toohello de tooavoid adicionales de ida y vuelta.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="c9eb5-181">Hello código siguiente muestra cómo tooretrieve nuestra base de datos y la colección, si existe, o cree uno nuevo si no existe:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="c9eb5-182">paso siguiente Hello es toowrite algunos hello de toopersist de código TodoItems en colección toohello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="c9eb5-183">En este ejemplo, usaremos [Gson](https://code.google.com/p/google-gson/) tooserialize y deserializar documentos de tooJSON TodoItem Java objetos estándar (POJOs).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="c9eb5-184">Al igual que las colecciones y las bases de datos de Azure Cosmos DB, a los documentos también se hace referencia mediante autovínculos.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="c9eb5-185">Hola siguientes auxiliar función permite nos recuperar documentos por otro atributo (por ejemplo, "id") en lugar de vínculos propios:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
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
6. <span data-ttu-id="c9eb5-186">Podemos usar el método de aplicación auxiliar de hello en el paso 5 tooretrieve un documento TodoItem JSON por Id. de y deserializarla tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="c9eb5-187">También podemos utilizar hello DocumentClient tooget una colección o lista de TodoItems mediante SQL de DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="c9eb5-188">Un documento con hello DocumentClient no hay tooupdate de muchas maneras.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="c9eb5-189">En nuestra aplicación de lista de tareas, queremos toobe capaz de tootoggle si un TodoItem ha finalizado.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="c9eb5-190">Esto puede lograrse mediante la actualización de un atributo "completa" en el documento de Hola Hola:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="c9eb5-191">Por último, queremos Hola capacidad toodelete un TodoItem de nuestra lista.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="c9eb5-192">toodo, podemos utilizar el método de aplicación auxiliar de hello indicamos anteriormente tooretrieve Hola vínculos propios y, a continuación, indicar Hola cliente toodelete:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="c9eb5-193"><a id="Wire"></a>Paso 5: El resto de Hola de Hola de proyecto de desarrollo de aplicaciones de Java cableado juntos</span><span class="sxs-lookup"><span data-stu-id="c9eb5-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="c9eb5-194">Ahora que hemos terminado fun Hola bits: lo único que queda es toobuild una interfaz de usuario rápida y vincularla tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="c9eb5-195">En primer lugar, puede empezar con la creación de un controlador toocall nuestro DAO:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="c9eb5-196">En una aplicación más compleja, controlador de hello puede alojar lógica de negocios complicado sobre Hola DAO.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="c9eb5-197">A continuación, vamos a crear un controlador de toohello de las solicitudes de servlet tooroute HTTP:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="c9eb5-198">Necesitaremos un usuario de toohello web toodisplay de interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="c9eb5-199">Vamos a volver a escribir hello index.jsp que hemos creado con anterioridad:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
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
   
            <!-- hello ToDo List -->
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
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="c9eb5-200">Por último, escribir alguna interfaz de usuario web de cliente JavaScript tootie Hola y Hola servlet juntos:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
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
   
              // Call api tooupdate todo items.
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
           * Install hello TodoApp
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
5. <span data-ttu-id="c9eb5-201">¡Increíble!</span><span class="sxs-lookup"><span data-stu-id="c9eb5-201">Awesome!</span></span> <span data-ttu-id="c9eb5-202">Ahora todo lo que queda es aplicación de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="c9eb5-203">Ejecutar la aplicación hello localmente y agregue algunos elementos de lista de tareas Rellenar en nombre del elemento de hello y una categoría y haciendo clic en **agregar tarea**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="c9eb5-204">Cuando aparezca el elemento de hello, puede actualizar si ha finalizado o desactiva la casilla de verificación de Hola y haciendo clic en **actualizar tareas**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="c9eb5-205"><a id="Deploy"></a>Paso 6: Implementar el tooAzure de aplicación de Java sitios Web</span><span class="sxs-lookup"><span data-stu-id="c9eb5-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="c9eb5-206">Azure WebSites consigue que la implementación de aplicaciones de Java sea tan sencilla como exportar su aplicación como un archivo WAR y cargarla mediante el control de código fuente (por ejemplo, Git) o FTP.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="c9eb5-207">tooexport la aplicación como un archivo WAR, haga clic en el proyecto en **el Explorador de proyectos**, haga clic en **exportar**y, a continuación, haga clic en **archivo WAR**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="c9eb5-208">Hola **exportar WAR** ventana, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="c9eb5-209">En el cuadro del proyecto Web hello, escriba azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="c9eb5-210">En el cuadro de destino de hello, elija un archivo WAR de destino toosave Hola.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="c9eb5-211">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="c9eb5-211">Click **Finish**.</span></span>
3. <span data-ttu-id="c9eb5-212">Ahora que tiene a mano en un archivo WAR, puede simplemente cargarlo tooyour sitio Web de Azure **móviles** directory.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="c9eb5-213">Para obtener instrucciones acerca de cómo cargar archivo hello, consulte [agregar una tooAzure de aplicación de Java aplicación del servicio de aplicaciones Web](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="c9eb5-214">Una vez que el archivo WAR de hello es el directorio de aplicaciones Web de toohello cargado, entorno de tiempo de ejecución de hello detectará que haya agregado y lo cargará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="c9eb5-215">tooview el producto acabado, navegue toohttp://YOUR\_sitio\_NAME.azurewebsites.net/azure-java-sample/ y empezar a agregar sus tareas.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="c9eb5-216"><a id="GetProject"></a>Obtener proyecto Hola desde GitHub</span><span class="sxs-lookup"><span data-stu-id="c9eb5-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="c9eb5-217">Todos los ejemplos de hello en este tutorial se incluyen en hello [tareas](https://github.com/Azure-Samples/documentdb-java-todo-app) proyecto en GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="c9eb5-218">proyecto de lista de tareas de tooimport hello en Eclipse, asegúrese de tener software de Hola y recursos que aparecen en hello [requisitos previos](#Prerequisites) sección, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c9eb5-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="c9eb5-219">Instale [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="c9eb5-220">Lombok es toogenerate usado constructores, captadores, establecedores en proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="c9eb5-221">Una vez que ha descargado el archivo de lombok.jar hello, haga doble clic en él tooinstall, o instalar desde la línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="c9eb5-222">Si Eclipse está abierto, ciérrelo y reinicie tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="c9eb5-223">En Eclipse, en hello **archivo** menú, haga clic en **importación**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="c9eb5-224">Hola **importación** ventana, haga clic en **Git**, haga clic en **proyectos desde Git**y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="c9eb5-225">En hello **Seleccionar origen de repositorio** pantalla, haga clic en **clon URI**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="c9eb5-226">En hello **repositorio de código fuente Git** pantalla Hola **URI** cuadro, escriba https://github.com/Azure-Samples/java-todo-app.git y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="c9eb5-227">En hello **selección rama** pantalla, asegúrese de que **maestro** está seleccionada y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="c9eb5-228">En hello **destino Local** pantalla, haga clic en **examinar** tooselect una carpeta donde se pueden copiar repositorio hello y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="c9eb5-229">En hello **seleccionar un toouse del Asistente para importar proyectos** pantalla, asegúrese de que **importar proyectos existentes** está seleccionada y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="c9eb5-230">En hello **importar proyectos** pantalla, anule la selección de hello **DocumentDB** del proyecto y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="c9eb5-231">proyecto de documentos de Hello contiene hello Azure Cosmos DB SDK de Java, que se agregará como una dependencia en su lugar.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="c9eb5-232">En **el Explorador de proyectos**, desplácese tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java y sustituirlos por valores HOST y MASTER_KEY Hola Hola URI y la clave principal para la cuenta de base de datos de Azure Cosmos y, a continuación, guardar el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="c9eb5-233">Para obtener más información, consulte el [paso 1. Creación de una cuenta de base de datos de Azure Cosmos DB](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="c9eb5-234">En **el Explorador de proyectos**, haga clic en hello **azure-documentdb-java-sample**, haga clic en **Build Path**y, a continuación, haga clic en **configurar Build Path**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="c9eb5-235">En hello **Java Build Path** pantalla, en el panel derecho de hello, seleccione hello **bibliotecas** ficha y, a continuación, haga clic en **agregar JAR externo**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="c9eb5-236">Navegue toohello ubicación del archivo de lombok.jar hello y haga clic en **abiertos**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="c9eb5-237">Hola de uso paso 12 tooopen **propiedades** ventana nuevo y, a continuación, en el panel izquierdo de hello haga clic en **tiempos de ejecución de destino**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="c9eb5-238">En hello **tiempos de ejecución de destino** pantalla, haga clic en **New**, seleccione **Apache Tomcat v7.0**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="c9eb5-239">Hola de uso paso 12 tooopen **propiedades** ventana nuevo y, a continuación, en el panel izquierdo de hello haga clic en **facetas de proyecto**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="c9eb5-240">En hello **proyecto facetas** pantalla, seleccione **módulo Web dinámico** y **Java**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="c9eb5-241">En hello **servidores** pestaña final Hola de pantalla de bienvenida, haga clic en **Tomcat v7.0 Server en localhost** y, a continuación, haga clic en **agregar y quitar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="c9eb5-242">En hello **agregar y quitar** ventana, mover **azure-documentdb-java-sample** toohello **configurado** cuadro y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="c9eb5-243">Hola **servidores** pestaña, haga clic en **Tomcat v7.0 Server en localhost**y, a continuación, haga clic en **reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="c9eb5-244">En un explorador, navegue toohttp://localhost:8080 / azure-documentdb-java-sample / y comenzar a agregar la lista de tareas de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="c9eb5-245">Tenga en cuenta que si cambia los valores de puerto predeterminado, cambie el valor de toohello de 8080 seleccionado.</span><span class="sxs-lookup"><span data-stu-id="c9eb5-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="c9eb5-246">vea el sitio web de Azure, de proyecto tooan de toodeploy [paso 6. Implementar los sitios Web de aplicación tooAzure](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="c9eb5-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
