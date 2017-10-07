---
title: "una base de datos del gráfico de base de datos de Azure Cosmos con Java aaaCreate | Documentos de Microsoft"
description: "Presenta una Java código de ejemplo que puede usar datos de gráfico de consultas de tooconnect tooand en la base de datos de Azure Cosmos con Gremlin."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="f3050-103">Azure Cosmos DB: Crear una base de datos de gráfico con Java y Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f3050-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="f3050-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f3050-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="f3050-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="f3050-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="f3050-106">Este tutorial crea un gráfico de base de datos mediante Hola herramientas del portal Azure para la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3050-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="f3050-107">Este tutorial rápido muestra también cómo tooquickly crear una aplicación de consola de Java con una base de datos de gráfico con sistemas operativos de hello [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) controlador.</span><span class="sxs-lookup"><span data-stu-id="f3050-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="f3050-108">instrucciones de Hello en este tutorial rápido se pueden aplicar en cualquier sistema operativo que sea capaz de ejecutar Java.</span><span class="sxs-lookup"><span data-stu-id="f3050-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="f3050-109">Este inicio rápido le ayudará a familiarizarse con la creación y modificación de los recursos de gráfico en hello interfaz de usuario o mediante programación, lo que sea su preferencia.</span><span class="sxs-lookup"><span data-stu-id="f3050-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f3050-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f3050-110">Prerequisites</span></span>

* [<span data-ttu-id="f3050-111">Kit de desarrollo de Java (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="f3050-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="f3050-112">En Ubuntu, ejecute `apt-get install default-jdk` tooinstall Hola JDK.</span><span class="sxs-lookup"><span data-stu-id="f3050-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="f3050-113">Ser seguro tooset Hola JAVA_HOME entorno variable toopoint toohello carpeta donde está instalado Hola JDK.</span><span class="sxs-lookup"><span data-stu-id="f3050-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="f3050-114">[Descargar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) un archivo binario de [Maven](http://maven.apache.org/)</span><span class="sxs-lookup"><span data-stu-id="f3050-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="f3050-115">En Ubuntu, se pueden ejecutar `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="f3050-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="f3050-116">Git</span><span class="sxs-lookup"><span data-stu-id="f3050-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="f3050-117">En Ubuntu, se pueden ejecutar `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="f3050-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="f3050-118">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="f3050-118">Create a database account</span></span>

<span data-ttu-id="f3050-119">Antes de poder crear una base de datos del gráfico, debe toocreate una cuenta de base de datos Gremlin (gráfico) con la base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f3050-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="f3050-120">Agregar un grafo</span><span class="sxs-lookup"><span data-stu-id="f3050-120">Add a graph</span></span>

<span data-ttu-id="f3050-121">Ahora puede usar la herramienta de exploración de datos de Hola Hola toocreate portal Azure una base de datos del gráfico.</span><span class="sxs-lookup"><span data-stu-id="f3050-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="f3050-122">Hola portal de Azure, en el menú de navegación izquierdo de hello, haga clic en **Explorador de datos (vista previa)**.</span><span class="sxs-lookup"><span data-stu-id="f3050-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="f3050-123">Hola **Explorador de datos (vista previa)** hoja, haga clic en **nuevo gráfico**, a continuación, rellene la página de hello mediante Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="f3050-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="f3050-125">Configuración</span><span class="sxs-lookup"><span data-stu-id="f3050-125">Setting</span></span>|<span data-ttu-id="f3050-126">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="f3050-126">Suggested value</span></span>|<span data-ttu-id="f3050-127">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3050-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="f3050-128">Identificador de base de datos</span><span class="sxs-lookup"><span data-stu-id="f3050-128">Database ID</span></span>|<span data-ttu-id="f3050-129">sample-database</span><span class="sxs-lookup"><span data-stu-id="f3050-129">sample-database</span></span>|<span data-ttu-id="f3050-130">Id. de Hello para la nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="f3050-130">hello ID for your new database.</span></span> <span data-ttu-id="f3050-131">Los nombres de bases de datos deben tener entre 1 y 255 caracteres y no pueden contener `/ \ # ?` o un espacio al final.</span><span class="sxs-lookup"><span data-stu-id="f3050-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="f3050-132">Identificador de grafo</span><span class="sxs-lookup"><span data-stu-id="f3050-132">Graph ID</span></span>|<span data-ttu-id="f3050-133">sample-graph</span><span class="sxs-lookup"><span data-stu-id="f3050-133">sample-graph</span></span>|<span data-ttu-id="f3050-134">Id. de Hello para el nuevo gráfico.</span><span class="sxs-lookup"><span data-stu-id="f3050-134">hello ID for your new graph.</span></span> <span data-ttu-id="f3050-135">Los nombres de gráfico tienen Hola mismo carácter requisitos como identificadores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="f3050-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="f3050-136">Capacidad de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="f3050-136">Storage Capacity</span></span>| <span data-ttu-id="f3050-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="f3050-137">10 GB</span></span>|<span data-ttu-id="f3050-138">Deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-138">Leave hello default value.</span></span> <span data-ttu-id="f3050-139">Se trata de capacidad de almacenamiento de Hola de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="f3050-140">Rendimiento</span><span class="sxs-lookup"><span data-stu-id="f3050-140">Throughput</span></span>|<span data-ttu-id="f3050-141">400 RU</span><span class="sxs-lookup"><span data-stu-id="f3050-141">400 RUs</span></span>|<span data-ttu-id="f3050-142">Deje el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-142">Leave hello default value.</span></span> <span data-ttu-id="f3050-143">Se puede escalar el rendimiento de hello más tarde si desea que la latencia tooreduce.</span><span class="sxs-lookup"><span data-stu-id="f3050-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="f3050-144">Clave de partición</span><span class="sxs-lookup"><span data-stu-id="f3050-144">Partition key</span></span>|<span data-ttu-id="f3050-145">Déjelo en blanco</span><span class="sxs-lookup"><span data-stu-id="f3050-145">Leave blank</span></span>|<span data-ttu-id="f3050-146">A fin de Hola de este tutorial rápido, deje en blanco clave de partición de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="f3050-147">Una vez que se rellena el formulario de hello, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3050-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="f3050-148">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="f3050-148">Clone hello sample application</span></span>

<span data-ttu-id="f3050-149">Ahora vamos a clonar una aplicación de gráfico de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="f3050-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="f3050-150">Vea lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="f3050-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="f3050-151">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f3050-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="f3050-152">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="f3050-153">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="f3050-153">Review hello code</span></span>

<span data-ttu-id="f3050-154">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f3050-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="f3050-155">Abra hello `Program.java` archivo de hello \src\GetStarted carpeta y busque las siguientes líneas de código.</span><span class="sxs-lookup"><span data-stu-id="f3050-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="f3050-156">Hola Gremlin `Client` se inicializa desde la configuración de hello en `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="f3050-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="f3050-157">Una serie de pasos de Gremlin se ejecutan utilizando hello `client.submit` método.</span><span class="sxs-lookup"><span data-stu-id="f3050-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="f3050-158">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="f3050-158">Update your connection string</span></span>

1. <span data-ttu-id="f3050-159">Archivo de src/remote.yaml de hello abierto.</span><span class="sxs-lookup"><span data-stu-id="f3050-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="f3050-160">Rellene la *hosts*, *nombre de usuario*, y *contraseña* valores en el archivo de hello src/remote.yaml.</span><span class="sxs-lookup"><span data-stu-id="f3050-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="f3050-161">resto de Hola de configuración de hello no es necesario toobe cambiado.</span><span class="sxs-lookup"><span data-stu-id="f3050-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="f3050-162">Configuración</span><span class="sxs-lookup"><span data-stu-id="f3050-162">Setting</span></span>|<span data-ttu-id="f3050-163">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="f3050-163">Suggested value</span></span>|<span data-ttu-id="f3050-164">Descripción</span><span class="sxs-lookup"><span data-stu-id="f3050-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="f3050-165">Hosts</span><span class="sxs-lookup"><span data-stu-id="f3050-165">Hosts</span></span>|<span data-ttu-id="f3050-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="f3050-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="f3050-167">Consulte la captura de pantalla de hello sigue a esta tabla.</span><span class="sxs-lookup"><span data-stu-id="f3050-167">See hello screenshot following this table.</span></span> <span data-ttu-id="f3050-168">Este valor es el valor de URI Gremlin de hello en la página de información general de Hola de hello portal de Azure, entre corchetes, con hello finales: 443 / quitado.</span><span class="sxs-lookup"><span data-stu-id="f3050-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="f3050-169">Este valor también puede obtenerse de la pestaña de claves de hello, utilizando el valor URI de hello quitar https://, cambiar toographs de documentos y quitando finales Hola: 443 /.</span><span class="sxs-lookup"><span data-stu-id="f3050-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="f3050-170">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="f3050-170">Username</span></span>|<span data-ttu-id="f3050-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="f3050-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="f3050-172">Hola recursos de formulario de hello `/dbs/<db>/colls/<coll>` donde `<db>` es el nombre de base de datos existente y `<coll>` es el nombre de la colección existente.</span><span class="sxs-lookup"><span data-stu-id="f3050-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="f3050-173">Password</span><span class="sxs-lookup"><span data-stu-id="f3050-173">Password</span></span>|<span data-ttu-id="f3050-174">*Su clave maestra principal*</span><span class="sxs-lookup"><span data-stu-id="f3050-174">*Your primary master key*</span></span>|<span data-ttu-id="f3050-175">Vea Hola segunda captura de pantalla sigue a esta tabla.</span><span class="sxs-lookup"><span data-stu-id="f3050-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="f3050-176">Este valor es la clave principal, que puede recuperar de la página de claves de Hola de portal de Azure, en el cuadro de la clave principal de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="f3050-177">Copiar valor de hello usando Hola copia botón Hola derecha del cuadro de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="f3050-178">Para el valor de Hosts de hello, copie hello **Gremlin URI** valor de hello **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="f3050-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="f3050-179">Si está vacía, consulte las instrucciones de Hola de fila de Hosts de Hola Hola tabla sobre la creación de hello Gremlin URI de la hoja de claves de hello anterior.</span><span class="sxs-lookup"><span data-stu-id="f3050-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="f3050-180">![Visualizar y copiar valor de URI Gremlin de hello en la página de información general de Hola Hola portal de Azure](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="f3050-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="f3050-181">Para el valor de la contraseña de hello, copie hello **clave principal** de hello **claves** hoja: ![visualizar y copiar las claves de la clave principal en hello portal de Azure, página](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="f3050-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="f3050-182">Ejecutar la aplicación de consola de hello</span><span class="sxs-lookup"><span data-stu-id="f3050-182">Run hello console app</span></span>

1. <span data-ttu-id="f3050-183">En la ventana de terminal de git hello, `cd` toohello azure-cosmos-db-graph-java-getting-started carpeta.</span><span class="sxs-lookup"><span data-stu-id="f3050-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="f3050-184">En la ventana de terminal de git hello, escriba `mvn package` tooinstall Hola necesario paquetes de Java.</span><span class="sxs-lookup"><span data-stu-id="f3050-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="f3050-185">En la ventana de terminal de git hello, ejecute `mvn exec:java -D exec.mainClass=GetStarted.Program` en Hola ventana de terminal toostart la aplicación de Java.</span><span class="sxs-lookup"><span data-stu-id="f3050-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="f3050-186">ventana de terminal de Hello muestra vértices Hola añadidos toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="f3050-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="f3050-187">Una vez que finalice el programa de hello, cambiar atrás toohello portal de Azure en el Explorador de internet.</span><span class="sxs-lookup"><span data-stu-id="f3050-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="f3050-188">Revise y agregue datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f3050-188">Review and add sample data</span></span>

<span data-ttu-id="f3050-189">Ahora puede volver atrás tooData explorador y vea vértices Hola agregan toohello gráfico y agregar puntos de datos adicionales.</span><span class="sxs-lookup"><span data-stu-id="f3050-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="f3050-190">En el Explorador de datos, expanda hello **base de datos de ejemplo**/**gráfico de ejemplo**, haga clic en **gráfico**y, a continuación, haga clic en **aplicar filtro**.</span><span class="sxs-lookup"><span data-stu-id="f3050-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="f3050-192">Hola **resultados** lista, tenga en cuenta los nuevos usuarios de hello agregan toohello gráfico.</span><span class="sxs-lookup"><span data-stu-id="f3050-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="f3050-193">Seleccione **ben** y observe que ha conectado toorobin.</span><span class="sxs-lookup"><span data-stu-id="f3050-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="f3050-194">Puede moverse vértices hello en el Explorador de gráficos de hello, acercar y alejar y expandir el tamaño de la superficie del explorador de gráfico de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Nueva vértices en gráfico hello en el Explorador de datos Hola portal de Azure](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="f3050-196">Vamos a agregar unos nuevo gráfico toohello de los usuarios mediante Hola Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="f3050-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="f3050-197">Haga clic en hello **nuevo vértice** gráfico de botón tooadd datos tooyour.</span><span class="sxs-lookup"><span data-stu-id="f3050-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Crear nuevos documentos en el Explorador de datos en hello portal de Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="f3050-199">Escriba una etiqueta de *persona* , a continuación, escriba Hola siguiente claves y valores toocreate Hola primer vértice gráfico Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="f3050-200">Tenga en cuenta que puede crear propiedades únicas para cada persona en el grafo.</span><span class="sxs-lookup"><span data-stu-id="f3050-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="f3050-201">Solo Hola identificador clave es obligatoria.</span><span class="sxs-lookup"><span data-stu-id="f3050-201">Only hello id key is required.</span></span>

    <span data-ttu-id="f3050-202">key</span><span class="sxs-lookup"><span data-stu-id="f3050-202">key</span></span>|<span data-ttu-id="f3050-203">value</span><span class="sxs-lookup"><span data-stu-id="f3050-203">value</span></span>|<span data-ttu-id="f3050-204">Notas</span><span class="sxs-lookup"><span data-stu-id="f3050-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="f3050-205">id</span><span class="sxs-lookup"><span data-stu-id="f3050-205">id</span></span>|<span data-ttu-id="f3050-206">ashley</span><span class="sxs-lookup"><span data-stu-id="f3050-206">ashley</span></span>|<span data-ttu-id="f3050-207">Identificador único de Hola de vértice Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="f3050-208">Si no se especifica un identificador, se genera uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f3050-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="f3050-209">gender</span><span class="sxs-lookup"><span data-stu-id="f3050-209">gender</span></span>|<span data-ttu-id="f3050-210">mujer</span><span class="sxs-lookup"><span data-stu-id="f3050-210">female</span></span>| 
    <span data-ttu-id="f3050-211">técnico</span><span class="sxs-lookup"><span data-stu-id="f3050-211">tech</span></span> | <span data-ttu-id="f3050-212">Java</span><span class="sxs-lookup"><span data-stu-id="f3050-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="f3050-213">En este tutorial rápido se crea una colección sin particiones.</span><span class="sxs-lookup"><span data-stu-id="f3050-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="f3050-214">Sin embargo, si crea una colección con particiones mediante la especificación de una clave de partición durante la creación de la colección de hello, necesita clave de partición de hello tooinclude como una clave en cada nuevo vértice.</span><span class="sxs-lookup"><span data-stu-id="f3050-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="f3050-215">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3050-215">Click **OK**.</span></span> <span data-ttu-id="f3050-216">Puede que necesite tooexpand su toosee pantalla **Aceptar** en la parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="f3050-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="f3050-217">Haga clic en **Nuevo vértice** de nuevo y agregue otro usuario.</span><span class="sxs-lookup"><span data-stu-id="f3050-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="f3050-218">Escriba una etiqueta de *persona* escriba Hola siguiente claves y valores:</span><span class="sxs-lookup"><span data-stu-id="f3050-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="f3050-219">key</span><span class="sxs-lookup"><span data-stu-id="f3050-219">key</span></span>|<span data-ttu-id="f3050-220">value</span><span class="sxs-lookup"><span data-stu-id="f3050-220">value</span></span>|<span data-ttu-id="f3050-221">Notas</span><span class="sxs-lookup"><span data-stu-id="f3050-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="f3050-222">id</span><span class="sxs-lookup"><span data-stu-id="f3050-222">id</span></span>|<span data-ttu-id="f3050-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="f3050-223">rakesh</span></span>|<span data-ttu-id="f3050-224">Identificador único de Hola de vértice Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="f3050-225">Si no se especifica un identificador, se genera uno automáticamente.</span><span class="sxs-lookup"><span data-stu-id="f3050-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="f3050-226">gender</span><span class="sxs-lookup"><span data-stu-id="f3050-226">gender</span></span>|<span data-ttu-id="f3050-227">hombre</span><span class="sxs-lookup"><span data-stu-id="f3050-227">male</span></span>| 
    <span data-ttu-id="f3050-228">centro educativo</span><span class="sxs-lookup"><span data-stu-id="f3050-228">school</span></span>|<span data-ttu-id="f3050-229">MIT</span><span class="sxs-lookup"><span data-stu-id="f3050-229">MIT</span></span>| 

7. <span data-ttu-id="f3050-230">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f3050-230">Click **OK**.</span></span> 

8. <span data-ttu-id="f3050-231">Haga clic en **aplicar filtro** no tiene valor predeterminado de hello `g.V()` filtro.</span><span class="sxs-lookup"><span data-stu-id="f3050-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="f3050-232">Todos los usuarios de hello muestran ahora en hello **resultados** lista.</span><span class="sxs-lookup"><span data-stu-id="f3050-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="f3050-233">Si agrega más datos, puede usar filtros toolimit los resultados.</span><span class="sxs-lookup"><span data-stu-id="f3050-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="f3050-234">De forma predeterminada, usa el Explorador de datos `g.V()` tooretrieve todos los vértices en un gráfico, pero pueden cambiar ese tooa diferentes [consulta graph](tutorial-query-graph.md), como `g.V().count()`, tooreturn un recuento de todos los vértices de hello en el gráfico de hello en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f3050-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="f3050-235">Ahora podemos conectar a rakesh y ashley.</span><span class="sxs-lookup"><span data-stu-id="f3050-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="f3050-236">Asegúrese de **Ana** en seleccionado en hello **resultados** lista, a continuación, haga clic en botón de edición de hello siguiente demasiado**destinos** en la parte inferior derecha.</span><span class="sxs-lookup"><span data-stu-id="f3050-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="f3050-237">Puede que necesite toowiden su Hola de ventana toosee **propiedades** área.</span><span class="sxs-lookup"><span data-stu-id="f3050-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Cambiar el destino de Hola de un vértice en un gráfico](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="f3050-239">Hola **destino** cuadro, escriba *rakesh*y en hello **etiqueta de borde** cuadro, escriba *sabe*y, a continuación, haga clic en la casilla de verificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="f3050-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Adicion de una conexión entre ashley y rakesh en el Explorador de datos](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="f3050-241">Ahora seleccione **rakesh** desde la lista de resultados de Hola y vea que Ana y rakesh están conectados.</span><span class="sxs-lookup"><span data-stu-id="f3050-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Dos vértices conectados en el Explorador de datos](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="f3050-243">También puede usar procedimientos de explorador de datos toocreate almacenado, UDF y lógica de negocios de servidor de tooperform de desencadenadores, así como el rendimiento de escala.</span><span class="sxs-lookup"><span data-stu-id="f3050-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="f3050-244">Explorador de datos expone todo acceso a los datos de mediante programación integrada Hola disponible en las API de hello, pero proporciona un acceso sencillo tooyour datos Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f3050-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="f3050-245">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="f3050-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="f3050-246">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="f3050-246">Clean up resources</span></span>

<span data-ttu-id="f3050-247">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="f3050-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="f3050-248">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="f3050-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="f3050-249">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f3050-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3050-250">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f3050-250">Next steps</span></span>

<span data-ttu-id="f3050-251">En este tutorial, ha aprendido cómo crear un gráfico utilizando Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="f3050-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="f3050-252">Ahora puede crear consultas más complejas e implementar con Gremlin una lógica eficaz de recorrido del grafo.</span><span class="sxs-lookup"><span data-stu-id="f3050-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3050-253">Consulta mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="f3050-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

