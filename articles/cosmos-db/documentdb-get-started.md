---
title: "Azure Cosmos DB: tutorial de introducción a las API de DocumentDB | Microsoft Docs"
description: "Un tutorial que crea una base de datos en línea y la aplicación de consola de C# con hello API de documentos."
keywords: "tutorial de nosql, base de datos en línea, aplicación de consola de c#"
services: cosmos-db
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2017
ms.author: anhoh
ms.openlocfilehash: 65a181f715a670987492ad7815ef2ec94498e84d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="48834-104">Azure Cosmos DB: tutorial de introducción a las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="48834-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48834-105">.NET</span><span class="sxs-lookup"><span data-stu-id="48834-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="48834-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="48834-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="48834-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="48834-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="48834-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="48834-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="48834-109">Java</span><span class="sxs-lookup"><span data-stu-id="48834-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="48834-110">C++</span><span class="sxs-lookup"><span data-stu-id="48834-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="48834-111">Bienvenida toohello API de documentos de base de datos de Azure Cosmos tutorial de introducción.</span><span class="sxs-lookup"><span data-stu-id="48834-111">Welcome toohello Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="48834-112">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="48834-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="48834-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="48834-113">We'll cover:</span></span>

* <span data-ttu-id="48834-114">Creación y conexión de cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="48834-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="48834-115">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48834-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="48834-116">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="48834-116">Creating an online database</span></span>
* <span data-ttu-id="48834-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="48834-117">Creating a collection</span></span>
* <span data-ttu-id="48834-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="48834-118">Creating JSON documents</span></span>
* <span data-ttu-id="48834-119">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="48834-119">Querying hello collection</span></span>
* <span data-ttu-id="48834-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="48834-120">Replacing a document</span></span>
* <span data-ttu-id="48834-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="48834-121">Deleting a document</span></span>
* <span data-ttu-id="48834-122">Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="48834-122">Deleting hello database</span></span>

<span data-ttu-id="48834-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="48834-123">Don't have time?</span></span> <span data-ttu-id="48834-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="48834-124">Don't worry!</span></span> <span data-ttu-id="48834-125">está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="48834-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="48834-126">Saltar toohello [Obtenga una sección de solución del tutorial de NoSQL completa hello](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="48834-126">Jump toohello [Get hello complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="48834-127">Después, por favor, use Hola botones de voto en hello superior o inferior de esta página toogive nos comentarios.</span><span class="sxs-lookup"><span data-stu-id="48834-127">Afterwards, please use hello voting buttons at hello top or bottom of this page toogive us feedback.</span></span> <span data-ttu-id="48834-128">Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="48834-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="48834-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="48834-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48834-130">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="48834-130">Prerequisites</span></span>
<span data-ttu-id="48834-131">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="48834-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="48834-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="48834-132">An active Azure account.</span></span> <span data-ttu-id="48834-133">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="48834-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="48834-134">Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="48834-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="48834-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="48834-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="48834-136">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="48834-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="48834-137">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="48834-138">Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="48834-138">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="48834-139">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[la instalación de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="48834-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="48834-140"><a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="48834-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="48834-141">Abra **Visual Studio 2017** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="48834-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="48834-142">En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="48834-142">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="48834-143">Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola**, nombre el proyecto y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48834-143">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="48834-144">![Captura de pantalla de ventana nuevo proyecto de hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="48834-144">![Screen shot of hello New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="48834-145">Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**</span><span class="sxs-lookup"><span data-stu-id="48834-145">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="48834-147">Hola **Nuget** , haga clic en **examinar**y el tipo de **documentdb de azure** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-147">In hello **Nuget** tab, click **Browse**, and type **azure documentdb** in hello search box.</span></span>
6. <span data-ttu-id="48834-148">En los resultados de hello, buscar **Microsoft.Azure.DocumentDB** y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="48834-148">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="48834-149">Id. de paquete de Hola para hello biblioteca cliente de API de documentos de base de datos de Azure Cosmos es [biblioteca de cliente de Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="48834-149">hello package ID for hello Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="48834-150">![Captura de pantalla de hello Nuget menú para buscar el SDK de cliente de base de datos de Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="48834-150">![Screen shot of hello Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="48834-151">Si aparece un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="48834-151">If you get a messages about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="48834-152">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="48834-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="48834-153">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="48834-153">Great!</span></span> <span data-ttu-id="48834-154">Ahora que hemos terminado el programa de instalación de hello, vamos a empezar a escribir código.</span><span class="sxs-lookup"><span data-stu-id="48834-154">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="48834-155">Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="48834-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="48834-156"><a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="48834-156"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="48834-157">En primer lugar, agregue estas referencias toohello a partir de la aplicación de C#, en el archivo Program.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="48834-157">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="48834-158">En el tutorial de orden toocomplete hello, asegúrese de que agregar dependencias de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="48834-158">In order toocomplete hello tutorial, make sure you add hello dependencies above.</span></span>
> 
> 

<span data-ttu-id="48834-159">Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="48834-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="48834-160">A continuación, hacer copia de head toohello [Portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="48834-160">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="48834-161">dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-161">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="48834-162">Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="48834-162">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="48834-163">Copiar Hola URI desde el portal de Hola y pegarlos en `<your endpoint URL>` en el archivo program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-163">Copy hello URI from hello portal and paste it into `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="48834-164">A continuación, copia Hola clave principal del portal de Hola y péguelo en `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="48834-164">Then copy hello PRIMARY KEY from hello portal and paste it into `<your primary key>`.</span></span>

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de C#.][keys]

<span data-ttu-id="48834-167">A continuación, comenzaremos aplicación hello mediante la creación de una nueva instancia de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="48834-167">Next, we'll start hello application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="48834-168">A continuación hello **Main** método, agregar esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia de nuestro nuevo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="48834-168">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="48834-169">Agregar código de hello siguiente toorun su tarea asincrónica de la **Main** método.</span><span class="sxs-lookup"><span data-stu-id="48834-169">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="48834-170">Hola **Main** método detectará las excepciones y escribirlos toohello consola.</span><span class="sxs-lookup"><span data-stu-id="48834-170">hello **Main** method will catch exceptions and write them toohello console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART tooYOUR CODE
            try
            {
                    Program p = new Program();
                    p.GetStartedDemo().Wait();
            }
            catch (DocumentClientException de)
            {
                    Exception baseException = de.GetBaseException();
                    Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
            }
            catch (Exception e)
            {
                    Exception baseException = e.GetBaseException();
                    Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
            }
            finally
            {
                    Console.WriteLine("End of demo, press any key tooexit.");
                    Console.ReadKey();
            }

<span data-ttu-id="48834-171">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-171">Press **F5** toorun your application.</span></span> <span data-ttu-id="48834-172">salida de la ventana Consola Hello muestra mensajes de bienvenida `End of demo, press any key tooexit.` confirmar que se ha realizado la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-172">hello console window output displays hello message `End of demo, press any key tooexit.` confirming that hello connection was made.</span></span>  <span data-ttu-id="48834-173">A continuación, puede cerrar la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-173">You can then close hello console window.</span></span> 

<span data-ttu-id="48834-174">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-174">Congratulations!</span></span> <span data-ttu-id="48834-175">Se ha conectado correctamente la cuenta de base de datos de Azure Cosmos tooan, ahora Echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="48834-175">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="48834-176">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="48834-176">Step 4: Create a database</span></span>
<span data-ttu-id="48834-177">Antes de agregar código de hello para la creación de una base de datos, agregue un método auxiliar para escribir toohello consola.</span><span class="sxs-lookup"><span data-stu-id="48834-177">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="48834-178">Copie y pegue hello **WriteToConsoleAndPromptToContinue** método después de hello **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="48834-178">Copy and paste hello **WriteToConsoleAndPromptToContinue** method after hello **GetStartedDemo** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="48834-179">La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="48834-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="48834-180">Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.</span><span class="sxs-lookup"><span data-stu-id="48834-180">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="48834-181">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-181">Copy and paste hello following code tooyour **GetStartedDemo** method after hello client creation.</span></span> <span data-ttu-id="48834-182">Así se creará una base de datos denominada *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="48834-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="48834-183">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-183">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-184">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-184">Congratulations!</span></span> <span data-ttu-id="48834-185">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="48834-186"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="48834-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="48834-187">**CreateDocumentCollectionIfNotExistsAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="48834-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="48834-188">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="48834-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="48834-189">A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="48834-189">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="48834-190">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="48834-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="48834-191">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-191">Copy and paste hello following code tooyour **GetStartedDemo** method after hello database creation.</span></span> <span data-ttu-id="48834-192">Esto creará una colección de documentos llamada *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="48834-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="48834-193">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-193">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-194">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-194">Congratulations!</span></span> <span data-ttu-id="48834-195">Ha creado correctamente una colección de documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="48834-196"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="48834-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="48834-197">A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="48834-197">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="48834-198">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="48834-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="48834-199">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="48834-199">We can now insert one or more documents.</span></span> <span data-ttu-id="48834-200">Si ya tiene datos que le gustaría toostore en la base de datos, puede usar base de datos de Azure Cosmos hello [herramienta de migración de datos](import-data.md) datos de hello tooimport en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="48834-200">If you already have data you'd like toostore in your database, you can use hello Azure Cosmos DB [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

<span data-ttu-id="48834-201">En primer lugar, necesitamos toocreate una **familia** clases que representan objetos almacenados en la base de datos de Azure Cosmos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="48834-201">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="48834-202">También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**.</span><span class="sxs-lookup"><span data-stu-id="48834-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="48834-203">Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON.</span><span class="sxs-lookup"><span data-stu-id="48834-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="48834-204">Crear estas clases mediante la adición de hello siguientes subclases internos después de hello **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="48834-204">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="48834-205">Copie y pegue hello **familia**, **primario**, **secundarios**, **mascota**, y **dirección** clases después Hola **WriteToConsoleAndPromptToContinue** método.</span><span class="sxs-lookup"><span data-stu-id="48834-205">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after hello **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
    }

    // ADD THIS PART tooYOUR CODE
    public class Family
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        public string LastName { get; set; }
        public Parent[] Parents { get; set; }
        public Child[] Children { get; set; }
        public Address Address { get; set; }
        public bool IsRegistered { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class Parent
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
    }

    public class Child
    {
        public string FamilyName { get; set; }
        public string FirstName { get; set; }
        public string Gender { get; set; }
        public int Grade { get; set; }
        public Pet[] Pets { get; set; }
    }

    public class Pet
    {
        public string GivenName { get; set; }
    }

    public class Address
    {
        public string State { get; set; }
        public string County { get; set; }
        public string City { get; set; }
    }

<span data-ttu-id="48834-206">Copie y pegue hello **CreateFamilyDocumentIfNotExists** método debajo de su **dirección** clase.</span><span class="sxs-lookup"><span data-stu-id="48834-206">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
            this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
                this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
            }
            else
            {
                throw;
            }
        }
    }

<span data-ttu-id="48834-207">E insertar otros dos documentos, uno para hello Andersen familia y hello Wakefield familia.</span><span class="sxs-lookup"><span data-stu-id="48834-207">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="48834-208">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de colección de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="48834-208">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART tooYOUR CODE
    Family andersenFamily = new Family
    {
            Id = "Andersen.1",
            LastName = "Andersen",
            Parents = new Parent[]
            {
                    new Parent { FirstName = "Thomas" },
                    new Parent { FirstName = "Mary Kay" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FirstName = "Henriette Thaulow",
                            Gender = "female",
                            Grade = 5,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Fluffy" }
                            }
                    }
            },
            Address = new Address { State = "WA", County = "King", City = "Seattle" },
            IsRegistered = true
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

    Family wakefieldFamily = new Family
    {
            Id = "Wakefield.7",
            LastName = "Wakefield",
            Parents = new Parent[]
            {
                    new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                    new Parent { FamilyName = "Miller", FirstName = "Ben" }
            },
            Children = new Child[]
            {
                    new Child
                    {
                            FamilyName = "Merriam",
                            FirstName = "Jesse",
                            Gender = "female",
                            Grade = 8,
                            Pets = new Pet[]
                            {
                                    new Pet { GivenName = "Goofy" },
                                    new Pet { GivenName = "Shadow" }
                            }
                    },
                    new Child
                    {
                            FamilyName = "Miller",
                            FirstName = "Lisa",
                            Gender = "female",
                            Grade = 1
                    }
            },
            Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
            IsRegistered = false
    };

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="48834-209">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-209">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-210">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-210">Congratulations!</span></span> <span data-ttu-id="48834-211">Ha creado correctamente dos documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que ilustra relación jerárquica Hola entre la cuenta de hello, base de datos en línea hello, colección de Hola y documentos de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="48834-213"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="48834-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="48834-214">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="48834-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="48834-215">Hello código de ejemplo siguiente muestra varias consultas: usar ambos SQL de base de datos de Azure Cosmos sintaxis, así como LINQ - que podemos ejecutar contra Hola se insertan en el paso anterior de hello documentos.</span><span class="sxs-lookup"><span data-stu-id="48834-215">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="48834-216">Copie y pegue hello **ExecuteSimpleQuery** método después de su **CreateFamilyDocumentIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="48834-216">Copy and paste hello **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find hello Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // hello query is executed synchronously here, but can also be executed asynchronously via hello IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute hello same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

<span data-ttu-id="48834-217">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de hello segundo documento.</span><span class="sxs-lookup"><span data-stu-id="48834-217">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="48834-218">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-218">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-219">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-219">Congratulations!</span></span> <span data-ttu-id="48834-220">Ha consultado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="48834-221">Hello siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado y hello misma lógica aplica también la consulta LINQ de toohello.</span><span class="sxs-lookup"><span data-stu-id="48834-221">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="48834-223">Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección.</span><span class="sxs-lookup"><span data-stu-id="48834-223">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="48834-224">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="48834-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="48834-225">Base de datos de Azure Cosmos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="48834-225">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="48834-226"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="48834-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="48834-227">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="48834-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="48834-228">Copie y pegue hello **ReplaceFamilyDocument** método después de su **ExecuteSimpleQuery** método.</span><span class="sxs-lookup"><span data-stu-id="48834-228">Copy and paste hello **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="48834-229">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la ejecución de consulta de hello, al final de hello del método hello.</span><span class="sxs-lookup"><span data-stu-id="48834-229">Copy and paste hello following code tooyour **GetStartedDemo** method after hello query execution, at hello end of hello method.</span></span> <span data-ttu-id="48834-230">Después de reemplazar el documento de hello, ejecutará Hola mismo volver a consultar tooview Hola cambiado documento.</span><span class="sxs-lookup"><span data-stu-id="48834-230">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="48834-231">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-231">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-232">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-232">Congratulations!</span></span> <span data-ttu-id="48834-233">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="48834-234"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="48834-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="48834-235">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="48834-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="48834-236">Copie y pegue hello **DeleteFamilyDocument** método después de su **ReplaceFamilyDocument** método.</span><span class="sxs-lookup"><span data-stu-id="48834-236">Copy and paste hello **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="48834-237">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la ejecución de consulta segundo hello, al final de hello del método hello.</span><span class="sxs-lookup"><span data-stu-id="48834-237">Copy and paste hello following code tooyour **GetStartedDemo** method after hello second query execution, at hello end of hello method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="48834-238">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-238">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-239">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-239">Congratulations!</span></span> <span data-ttu-id="48834-240">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="48834-241"><a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="48834-241"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="48834-242">Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).</span><span class="sxs-lookup"><span data-stu-id="48834-242">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="48834-243">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después documento Hola Eliminar base de datos completa de toodelete hello y todos los recursos de los elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="48834-243">Copy and paste hello following code tooyour **GetStartedDemo** method after hello document delete toodelete hello entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="48834-244">Presione **F5** toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="48834-244">Press **F5** toorun your application.</span></span>

<span data-ttu-id="48834-245">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-245">Congratulations!</span></span> <span data-ttu-id="48834-246">Ha eliminado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="48834-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="48834-247"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="48834-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="48834-248">Presione F5 en la aplicación de Visual Studio toobuild hello en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="48834-248">Hit F5 in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="48834-249">Debería ver la salida de hello de la aplicación iniciada get en una ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="48834-249">You should see hello output of your get started app in a console window.</span></span> <span data-ttu-id="48834-250">salida de Hello mostrará resultados Hola de hello las consultas se agregan y se debe coincidir con el texto de ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="48834-250">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

    Created FamilyDB
    Press any key toocontinue ...
    Created FamilyCollection
    Press any key toocontinue ...
    Created Family Andersen.1
    Press any key toocontinue ...
    Created Family Wakefield.7
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key toocontinue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key tooexit.

<span data-ttu-id="48834-251">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="48834-251">Congratulations!</span></span> <span data-ttu-id="48834-252">Ha completado el tutorial de Hola y tiene una aplicación de consola de C# de trabajo.</span><span class="sxs-lookup"><span data-stu-id="48834-252">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="48834-253"><a id="GetSolution"></a>Obtener la solución del tutorial completo Hola</span><span class="sxs-lookup"><span data-stu-id="48834-253"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="48834-254">Si no dispone de tiempo hello toocomplete los pasos de este tutorial o ejemplos de código desea toodownload Hola simplemente, puede obtenerlo de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="48834-254">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="48834-255">solución de GetStarted de toobuild hello, necesitará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="48834-255">toobuild hello GetStarted solution, you will need hello following:</span></span>

* <span data-ttu-id="48834-256">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="48834-256">An active Azure account.</span></span> <span data-ttu-id="48834-257">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="48834-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="48834-258">Una [cuenta de Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="48834-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="48834-259">Hola [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solución disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="48834-259">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="48834-260">toorestore Hola referencias toohello Cosmos DB .NET SDK de Azure en Visual Studio, haga clic en hello **GetStarted** solución en el Explorador de soluciones y, a continuación, haga clic en **habilite la restauración del paquete NuGet**.</span><span class="sxs-lookup"><span data-stu-id="48834-260">toorestore hello references toohello Azure Cosmos DB .NET SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="48834-261">A continuación, en el archivo App.config de hello, actualizar valores de hello EndpointUrl y AuthorizationKey tal y como se describe en [conectar la cuenta de base de datos de Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="48834-261">Next, in hello App.config file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="48834-262">Y, eso es todo, genérela y habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="48834-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="48834-263">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="48834-263">Next steps</span></span>
* <span data-ttu-id="48834-264">¿Desea un tutorial de ASP.NET MVC más complejo?</span><span class="sxs-lookup"><span data-stu-id="48834-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="48834-265">Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="48834-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="48834-266">¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="48834-266">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="48834-267">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="48834-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="48834-268">Obtenga información acerca de cómo demasiado[supervisar las solicitudes, uso y almacenamiento de base de datos de Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="48834-268">Learn how too[monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="48834-269">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="48834-269">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="48834-270">toolearn más información acerca de la base de datos de Cosmos de Azure, consulte [Bienvenido tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="48834-270">toolearn more about Azure Cosmos DB, see [Welcome tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
