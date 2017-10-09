---
title: "Hola a aaaBuild una aplicación .NET de base de datos de Azure Cosmos con API de tabla | Documentos de Microsoft"
description: "Introducción a Tables API para Azure Cosmos DB mediante .NET"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a><span data-ttu-id="b3cec-103">Azure Cosmos DB: Crear una aplicación de .NET mediante Hola API de tabla</span><span class="sxs-lookup"><span data-stu-id="b3cec-103">Azure Cosmos DB: Build a .NET application using hello Table API</span></span>

<span data-ttu-id="b3cec-104">Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b3cec-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="b3cec-105">Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="b3cec-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="b3cec-106">Este inicio rápido se muestra cómo toocreate una base de datos de Azure Cosmos cuenta y crear una tabla dentro de esa cuenta con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cec-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, and create a table within that account using hello Azure portal.</span></span> <span data-ttu-id="b3cec-107">Necesitará, a continuación, escribir código tooinsert, actualización y eliminar las entidades así como ejecutar algunas consultas usando Hola nueva [tabla de Premium de almacenamiento de Windows Azure](https://aka.ms/premiumtablenuget) paquete NuGet (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="b3cec-107">You'll then write code tooinsert, update, and delete entities, and run some queries using hello new [Windows Azure Storage Premium Table](https://aka.ms/premiumtablenuget) (preview) package from NuGet.</span></span> <span data-ttu-id="b3cec-108">Esta biblioteca tiene Hola mismas clases y firmas de método como público hello [SDK de almacenamiento de Windows Azure](https://www.nuget.org/packages/WindowsAzure.Storage), pero también tiene cuentas Hola capacidad tooconnect tooAzure Cosmos DB con hello [API de tabla](table-introduction.md) (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="b3cec-108">This library has hello same classes and method signatures as hello public [Windows Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also has hello ability tooconnect tooAzure Cosmos DB accounts using hello [Table API](table-introduction.md) (preview).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b3cec-109">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="b3cec-109">Prerequisites</span></span>

<span data-ttu-id="b3cec-110">Si aún no tiene Visual Studio de 2017 instalado, puede descargar y usar hello **libre** [2017 Community Edition de Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b3cec-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="b3cec-111">Asegúrese de que habilitar **desarrollo Azure** durante la instalación de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="b3cec-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="b3cec-112">Creación de una cuenta de base de datos</span><span class="sxs-lookup"><span data-stu-id="b3cec-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a><span data-ttu-id="b3cec-113">Adición de una tabla</span><span class="sxs-lookup"><span data-stu-id="b3cec-113">Add a table</span></span>

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a><span data-ttu-id="b3cec-114">Agregar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="b3cec-114">Add sample data</span></span>

<span data-ttu-id="b3cec-115">Ahora puede agregar datos tooyour nueva tabla mediante el Explorador de datos (vista previa).</span><span class="sxs-lookup"><span data-stu-id="b3cec-115">You can now add data tooyour new table using Data Explorer (Preview).</span></span>

1. <span data-ttu-id="b3cec-116">En el Explorador de datos, expanda **sample-table** y haga clic en **Entidades** y en **Agregar entidad**.</span><span class="sxs-lookup"><span data-stu-id="b3cec-116">In Data Explorer, expand **sample-table**, click **Entities**, and then click **Add Entity**.</span></span>

   ![Crear nuevas entidades en el Explorador de datos en hello portal de Azure](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. <span data-ttu-id="b3cec-118">Ahora agregue el cuadro de valor de datos toohello PartitionKey y RowKey cuadro de valor y haga clic en **Agregar entidad**.</span><span class="sxs-lookup"><span data-stu-id="b3cec-118">Now add data toohello PartitionKey value box and RowKey value box, and click **Add Entity**.</span></span>

   ![Establecer Hola clave de partición y clave de fila para una nueva entidad](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    <span data-ttu-id="b3cec-120">Ahora puede agregar más entidades tooyour tabla, edite las entidades o consultar los datos en el Explorador de datos.</span><span class="sxs-lookup"><span data-stu-id="b3cec-120">You can now add more entities tooyour table, edit your entities, or query your data in Data Explorer.</span></span> <span data-ttu-id="b3cec-121">Explorador de datos también es donde puede escalar el rendimiento y agregar procedimientos almacenados, funciones definidas por el usuario y tabla de tooyour de desencadenadores.</span><span class="sxs-lookup"><span data-stu-id="b3cec-121">Data Explorer is also where you can scale your throughput and add stored procedures, user defined functions, and triggers tooyour table.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="b3cec-122">Clonar aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="b3cec-122">Clone hello sample application</span></span>

<span data-ttu-id="b3cec-123">Ahora vamos a clonar una aplicación de la tabla de github, establezca la cadena de conexión de Hola y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="b3cec-123">Now let's clone a Table app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="b3cec-124">Podrá ver lo fácil que es toowork con datos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="b3cec-124">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="b3cec-125">Abra una ventana de terminal de git, como git bash, y `cd` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b3cec-125">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="b3cec-126">Ejecute hello después de repositorio de ejemplo de comando tooclone Hola.</span><span class="sxs-lookup"><span data-stu-id="b3cec-126">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. <span data-ttu-id="b3cec-127">A continuación, abra el archivo de solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3cec-127">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="b3cec-128">Revise el código de hello</span><span class="sxs-lookup"><span data-stu-id="b3cec-128">Review hello code</span></span>

<span data-ttu-id="b3cec-129">Vamos a hacer una revisión rápida de lo que sucede en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b3cec-129">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="b3cec-130">Archivo de hello abra Program.cs y encontrará que estas líneas de código crean Hola recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b3cec-130">Open hello Program.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="b3cec-131">Hola CloudTableClient se inicializa.</span><span class="sxs-lookup"><span data-stu-id="b3cec-131">hello CloudTableClient is initialized.</span></span>

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* <span data-ttu-id="b3cec-132">Si no existe, se crea una nueva tabla.</span><span class="sxs-lookup"><span data-stu-id="b3cec-132">A new table is created if it does not exist.</span></span>

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* <span data-ttu-id="b3cec-133">Se crea un nuevo contenedor de tabla.</span><span class="sxs-lookup"><span data-stu-id="b3cec-133">A new Table container is created.</span></span> <span data-ttu-id="b3cec-134">Puede observar este tooregular muy similar de código SDK de almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cec-134">You will notice this code very similar tooregular Azure Table storage SDK.</span></span> 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="b3cec-135">Actualizar la cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="b3cec-135">Update your connection string</span></span>

<span data-ttu-id="b3cec-136">Ahora actualizaremos información hello de la cadena de conexión para que la aplicación puede comunicarse tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b3cec-136">Now we'll update hello connection string information so your app can talk tooAzure Cosmos DB.</span></span> 

1. <span data-ttu-id="b3cec-137">En Visual Studio, abra el archivo app.config de hello.</span><span class="sxs-lookup"><span data-stu-id="b3cec-137">In Visual Studio, open hello app.config file.</span></span> 

2. <span data-ttu-id="b3cec-138">Hola [portal de Azure](http://portal.azure.com/), Hola base de datos de Azure Cosmos deje de menú de navegación, haga clic en **cadena de conexión**.</span><span class="sxs-lookup"><span data-stu-id="b3cec-138">In hello [Azure portal](http://portal.azure.com/), in hello Azure Cosmos DB left navigation menu, click **Connection String**.</span></span> <span data-ttu-id="b3cec-139">En el nuevo panel de hello haga clic en botón Copiar de hello para la cadena de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3cec-139">Then in hello new pane click hello copy button for hello connection string.</span></span> 

    ![Ver y copiar Hola extremo y la clave de cuenta en el panel de la cadena de conexión de Hola](./media/create-table-dotnet/keys.png)

3. <span data-ttu-id="b3cec-141">Pegue el valor de hello en el archivo app.config de hello como valor de Hola de hello PremiumStorageConnectionString.</span><span class="sxs-lookup"><span data-stu-id="b3cec-141">Paste hello value into hello app.config file as hello value of hello PremiumStorageConnectionString.</span></span> 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    <span data-ttu-id="b3cec-142">Puede dejar hello StandardStorageConnectionString tal cual.</span><span class="sxs-lookup"><span data-stu-id="b3cec-142">You can leave hello StandardStorageConnectionString as is.</span></span>

<span data-ttu-id="b3cec-143">Ahora ha actualizado la aplicación con toda la información de hello debe toocommunicate con base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b3cec-143">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

## <a name="run-hello-web-app"></a><span data-ttu-id="b3cec-144">Ejecutar la aplicación web de hello</span><span class="sxs-lookup"><span data-stu-id="b3cec-144">Run hello web app</span></span>

1. <span data-ttu-id="b3cec-145">En Visual Studio, haga doble clic en hello **PremiumTableGetStarted** proyecto **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b3cec-145">In Visual Studio, right-click on hello **PremiumTableGetStarted** project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="b3cec-146">Hola NuGet **examinar** , escriba *WindowsAzure.Storage PremiumTable*.</span><span class="sxs-lookup"><span data-stu-id="b3cec-146">In hello NuGet **Browse** box, type *WindowsAzure.Storage-PremiumTable*.</span></span>

3. <span data-ttu-id="b3cec-147">Comprobar hello **incluir versión preliminar** cuadro.</span><span class="sxs-lookup"><span data-stu-id="b3cec-147">Check hello **Include prerelease** box.</span></span> 

4. <span data-ttu-id="b3cec-148">Desde los resultados de hello, instalar hello **WindowsAzure.Storage PremiumTable** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="b3cec-148">From hello results, install hello **WindowsAzure.Storage-PremiumTable** library.</span></span> <span data-ttu-id="b3cec-149">Esto instala vista previa de hello paquete de la API de tabla de base de datos de Azure Cosmos, así como todas las dependencias.</span><span class="sxs-lookup"><span data-stu-id="b3cec-149">This installs hello preview Azure Cosmos DB Table API package as well as all dependencies.</span></span> <span data-ttu-id="b3cec-150">Tenga en cuenta que se trata de un paquete de NuGet diferentes que Hola paquete de almacenamiento de Windows Azure usa almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="b3cec-150">Note that this is a different NuGet package than hello Windows Azure Storage package used by Azure Table storage.</span></span> 

5. <span data-ttu-id="b3cec-151">Haga clic en CTRL + F5 aplicación hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="b3cec-151">Click CTRL + F5 toorun hello application.</span></span>

    <span data-ttu-id="b3cec-152">ventana de la consola de Hello muestra los datos de Hola que se agregan, recuperar, consultar, reemplazan y eliminan de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3cec-152">hello console window displays hello data being added, retrieved, queried, replaced and deleted from hello table.</span></span> <span data-ttu-id="b3cec-153">Cuando se completa el script de Hola, presione cualquier ventana de la consola de clave tooclose Hola.</span><span class="sxs-lookup"><span data-stu-id="b3cec-153">When hello script completes, press any key tooclose hello console window.</span></span> 
    
    ![Salida de la consola de inicio rápido de Hola](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. <span data-ttu-id="b3cec-155">Si desea que las nuevas entidades de Hola de toosee en el Explorador de datos, simplemente comenta líneas 188 208 en program.cs, por lo que no se eliminan, ejecute a continuación, muestra de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="b3cec-155">If you want toosee hello new entities in Data Explorer, just comment out lines 188-208 in program.cs so they aren't deleted, then run hello sample again.</span></span> 

    <span data-ttu-id="b3cec-156">Ahora puede volver atrás tooData Explorer, haga clic en **actualizar**, expanda hello **personas** de tabla y haga clic en **entidades**y, a continuación, trabajar con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="b3cec-156">You can now go back tooData Explorer, click **Refresh**, expand hello **people** table and click **Entities**, and then work with this new data.</span></span> 

    ![Nuevas entidades en el Explorador de datos](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="b3cec-158">Revise los SLA de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="b3cec-158">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="b3cec-159">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="b3cec-159">Clean up resources</span></span>

<span data-ttu-id="b3cec-160">Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:</span><span class="sxs-lookup"><span data-stu-id="b3cec-160">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="b3cec-161">En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó.</span><span class="sxs-lookup"><span data-stu-id="b3cec-161">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="b3cec-162">En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="b3cec-162">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3cec-163">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3cec-163">Next steps</span></span>

<span data-ttu-id="b3cec-164">En este tutorial, ha aprendido cómo crear una tabla mediante Hola Explorador de datos toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3cec-164">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a table using hello Data Explorer, and run an app.</span></span>  <span data-ttu-id="b3cec-165">Ahora puede consultar los datos mediante Hola API de tabla.</span><span class="sxs-lookup"><span data-stu-id="b3cec-165">Now you can query your data using hello Table API.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="b3cec-166">Consulta con hello API de tabla</span><span class="sxs-lookup"><span data-stu-id="b3cec-166">Query using hello Table API</span></span>](tutorial-query-table.md)

