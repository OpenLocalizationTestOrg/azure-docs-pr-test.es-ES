---
title: "Azure Cosmos DB: tutorial de introducción a las API de DocumentDB | Microsoft Docs"
description: "Tutorial en el que se crea una base de datos en línea y la aplicación de consola de C# con la API de DocumentDB."
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
ms.openlocfilehash: 72f66081a6409f980ec6bca5188f585489245a36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a><span data-ttu-id="ce16e-104">Azure Cosmos DB: tutorial de introducción a las API de DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ce16e-104">Azure Cosmos DB: DocumentDB API getting started tutorial</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce16e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="ce16e-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="ce16e-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ce16e-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="ce16e-107">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="ce16e-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="ce16e-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="ce16e-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="ce16e-109">Java</span><span class="sxs-lookup"><span data-stu-id="ce16e-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="ce16e-110">C++</span><span class="sxs-lookup"><span data-stu-id="ce16e-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="ce16e-111">Le damos la bienvenida al tutorial de introducción a las API de DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-111">Welcome to the Azure Cosmos DB DocumentDB API getting started tutorial!</span></span> <span data-ttu-id="ce16e-112">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="ce16e-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="ce16e-113">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="ce16e-113">We'll cover:</span></span>

* <span data-ttu-id="ce16e-114">Creación de una cuenta de Azure Cosmos DB y conexión a ella</span><span class="sxs-lookup"><span data-stu-id="ce16e-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="ce16e-115">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce16e-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="ce16e-116">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="ce16e-116">Creating an online database</span></span>
* <span data-ttu-id="ce16e-117">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="ce16e-117">Creating a collection</span></span>
* <span data-ttu-id="ce16e-118">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="ce16e-118">Creating JSON documents</span></span>
* <span data-ttu-id="ce16e-119">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="ce16e-119">Querying the collection</span></span>
* <span data-ttu-id="ce16e-120">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="ce16e-120">Replacing a document</span></span>
* <span data-ttu-id="ce16e-121">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="ce16e-121">Deleting a document</span></span>
* <span data-ttu-id="ce16e-122">Eliminación de la base de datos</span><span class="sxs-lookup"><span data-stu-id="ce16e-122">Deleting the database</span></span>

<span data-ttu-id="ce16e-123">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="ce16e-123">Don't have time?</span></span> <span data-ttu-id="ce16e-124">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="ce16e-124">Don't worry!</span></span> <span data-ttu-id="ce16e-125">La solución completa está disponible en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ce16e-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="ce16e-126">Para obtener instrucciones rápidas, diríjase a la [sección Obtener la solución completa del tutorial de NoSQL](#GetSolution).</span><span class="sxs-lookup"><span data-stu-id="ce16e-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="ce16e-127">Después, utilice los botones de votación situados en la parte superior o inferior de esta página para proporcionarnos sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="ce16e-127">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="ce16e-128">Si quiere que nos pongamos en contacto directamente con usted, puede incluir su dirección de correo electrónico en los comentarios.</span><span class="sxs-lookup"><span data-stu-id="ce16e-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="ce16e-129">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="ce16e-129">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce16e-130">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ce16e-130">Prerequisites</span></span>
<span data-ttu-id="ce16e-131">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce16e-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="ce16e-132">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ce16e-132">An active Azure account.</span></span> <span data-ttu-id="ce16e-133">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ce16e-133">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="ce16e-134">Como alternativa, en este tutorial puede usar el [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ce16e-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="ce16e-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="ce16e-135">[Visual Studio Community 2017](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="ce16e-136">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ce16e-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="ce16e-137">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="ce16e-138">Si ya tiene una cuenta que desea usar, puede ir directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ce16e-138">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="ce16e-139">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="ce16e-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="ce16e-140"><a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ce16e-140"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="ce16e-141">Abra **Visual Studio 2017** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="ce16e-141">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="ce16e-142">En el menú **Archivo**, seleccione **Nuevo** y elija **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-142">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="ce16e-143">En el cuadro de diálogo **Nuevo proyecto**, seleccione **Plantillas** / **Visual C#** / **Aplicación de consola**, asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-143">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="ce16e-144">![Captura de pantalla de la ventana Nuevo proyecto](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="ce16e-144">![Screen shot of the New Project window](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="ce16e-145">En el **Explorador de soluciones**, haga clic con el botón derecho en la nueva aplicación de la consola, que se encuentra en la solución de Visual Studio y, a continuación, haga clic en **Administrar paquetes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="ce16e-145">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Captura de pantalla del menú contextual del proyecto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="ce16e-147">En la pestaña **Nuget** haga clic en **Examinar** y escriba **azure documentdb** en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="ce16e-147">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="ce16e-148">En los resultados, busque **Microsoft.Azure.DocumentDB** y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-148">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="ce16e-149">El identificador del paquete de la biblioteca de cliente de API de DocumentDB de Azure Cosmos DB es la [biblioteca de cliente de Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="ce16e-149">The package ID for the Azure Cosmos DB DocumentDB API Client Library is [Microsoft Azure DocumentDB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="ce16e-150">![Captura de pantalla del menú de NuGet para encontrar el SDK de cliente de Azure Cosmos DB](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="ce16e-150">![Screen shot of the Nuget Menu for finding Azure Cosmos DB Client SDK](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="ce16e-151">Si recibe un mensaje acerca de la revisión de los cambios de la solución, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-151">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="ce16e-152">Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-152">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="ce16e-153">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="ce16e-153">Great!</span></span> <span data-ttu-id="ce16e-154">Ahora que hemos terminado la configuración, comencemos a escribir algo de código.</span><span class="sxs-lookup"><span data-stu-id="ce16e-154">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="ce16e-155">Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="ce16e-155">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <span data-ttu-id="ce16e-156"><a id="Connect"></a>Paso 3: Conexión a una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ce16e-156"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="ce16e-157">En primer lugar, agregue estas referencias al principio de la aplicación de C#, en el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="ce16e-157">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> <span data-ttu-id="ce16e-158">Para poder completar este tutorial, asegúrese de que agrega las dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="ce16e-158">In order to complete the tutorial, make sure you add the dependencies above.</span></span>
> 
> 

<span data-ttu-id="ce16e-159">Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="ce16e-159">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="ce16e-160">A continuación, vuelva a [Azure Portal](https://portal.azure.com) para recuperar la dirección URL del punto de conexión y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="ce16e-160">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="ce16e-161">La dirección URL del punto de conexión y la clave principal son necesarias para que la aplicación sepa a dónde debe conectarse y para que Azure Cosmos DB confíe en la conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-161">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="ce16e-162">En Azure Portal, vaya a la cuenta de Azure Cosmos DB y haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-162">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="ce16e-163">Copie el URI desde el Portal y péguelo en `<your endpoint URL>` en el archivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="ce16e-163">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="ce16e-164">Después, copie la CLAVE PRINCIPAL del Portal y péguela en `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="ce16e-164">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Captura de pantalla del Portal de Azure usada por el tutorial de NoSQL para crear una aplicación de consola de C#.][keys]

<span data-ttu-id="ce16e-167">A continuación, se iniciará la aplicación, para lo que crearemos una nueva instancia de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-167">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="ce16e-168">Debajo del método **Main**, agregue esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia del nuevo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-168">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="ce16e-169">Agregue el siguiente código para ejecutar la tarea asincrónica desde el método **Main** .</span><span class="sxs-lookup"><span data-stu-id="ce16e-169">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="ce16e-170">El método **Main** detectará las excepciones y las escribirá en la consola.</span><span class="sxs-lookup"><span data-stu-id="ce16e-170">The **Main** method will catch exceptions and write them to the console.</span></span>

    static void Main(string[] args)
    {
            // ADD THIS PART TO YOUR CODE
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
                    Console.WriteLine("End of demo, press any key to exit.");
                    Console.ReadKey();
            }

<span data-ttu-id="ce16e-171">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-171">Press **F5** to run your application.</span></span> <span data-ttu-id="ce16e-172">La salida de la ventana de consola muestra el mensaje `End of demo, press any key to exit.` que confirma que se realizó la conexión.</span><span class="sxs-lookup"><span data-stu-id="ce16e-172">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="ce16e-173">A continuación, puede cerrar la ventana de consola.</span><span class="sxs-lookup"><span data-stu-id="ce16e-173">You can then close the console window.</span></span> 

<span data-ttu-id="ce16e-174">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-174">Congratulations!</span></span> <span data-ttu-id="ce16e-175">Se ha conectado correctamente a una cuenta de Azure Cosmos DB y ahora se explicará cómo trabajar con recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-175">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="ce16e-176">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="ce16e-176">Step 4: Create a database</span></span>
<span data-ttu-id="ce16e-177">Antes de agregar el código para crear una base de datos, agregue un método auxiliar para escribirlo en la consola.</span><span class="sxs-lookup"><span data-stu-id="ce16e-177">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="ce16e-178">Copie y pegue el método **WriteToConsoleAndPromptToContinue** después del método **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-178">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="ce16e-179">Puede crearse una [base de datos](documentdb-resources.md#databases) de Azure Cosmos DB mediante el método [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-179">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="ce16e-180">Una base de datos es un contenedor lógico de almacenamiento de documentos JSON particionado en recopilaciones.</span><span class="sxs-lookup"><span data-stu-id="ce16e-180">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="ce16e-181">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la creación del cliente.</span><span class="sxs-lookup"><span data-stu-id="ce16e-181">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="ce16e-182">Así se creará una base de datos denominada *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="ce16e-182">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="ce16e-183">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-183">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-184">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-184">Congratulations!</span></span> <span data-ttu-id="ce16e-185">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-185">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="ce16e-186"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="ce16e-186"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="ce16e-187">**CreateDocumentCollectionIfNotExistsAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="ce16e-187">**CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="ce16e-188">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="ce16e-188">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="ce16e-189">Para crear un objeto [collection](documentdb-resources.md#collections) se puede utilizar el método [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-189">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="ce16e-190">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ce16e-190">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="ce16e-191">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la creación de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="ce16e-191">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="ce16e-192">Esto creará una colección de documentos llamada *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="ce16e-192">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="ce16e-193">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-193">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-194">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-194">Congratulations!</span></span> <span data-ttu-id="ce16e-195">Ha creado correctamente una colección de documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-195">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="ce16e-196"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="ce16e-196"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="ce16e-197">Un [documento](documentdb-resources.md#documents) puede crearse mediante el método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-197">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="ce16e-198">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="ce16e-198">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="ce16e-199">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="ce16e-199">We can now insert one or more documents.</span></span> <span data-ttu-id="ce16e-200">Si ya dispone de datos que desea almacenar en la base de datos, puede usar la [herramienta de migración de datos](import-data.md) de Azure Cosmos DB para importar los datos en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="ce16e-200">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="ce16e-201">En primer lugar, es preciso crear una clase denominada **Family** que represente los objetos almacenados en Azure Cosmos DB en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="ce16e-201">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="ce16e-202">También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-202">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="ce16e-203">Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON.</span><span class="sxs-lookup"><span data-stu-id="ce16e-203">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="ce16e-204">Para agregar estas clases, agregue las siguientes subclases internas después del método **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="ce16e-204">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="ce16e-205">Copie y pegue las clases **Family**, **Parent**, **Child**, **Pet** y **Address** después del método **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-205">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="ce16e-206">Copie y pegue el método **CreateFamilyDocumentIfNotExists** debajo de la clase **Address**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-206">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="ce16e-207">E inserte dos documentos, uno para la familia Andersen y otro para la familia Wakefield.</span><span class="sxs-lookup"><span data-stu-id="ce16e-207">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="ce16e-208">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la creación de la colección de documentos.</span><span class="sxs-lookup"><span data-stu-id="ce16e-208">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


    // ADD THIS PART TO YOUR CODE
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

<span data-ttu-id="ce16e-209">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-209">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-210">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-210">Congratulations!</span></span> <span data-ttu-id="ce16e-211">Ha creado correctamente dos documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-211">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que muestra la relación jerárquica entre la cuenta, la base de datos en línea, la colección y los documentos usados por el tutorial NoSQL para crear una aplicación de consola de C#.](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="ce16e-213"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ce16e-213"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="ce16e-214">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="ce16e-214">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="ce16e-215">En el siguiente ejemplo se muestran diversas consultas (usando la sintaxis SQL tanto de Azure Cosmos DB como de LINQ) que podemos ejecutar en los documentos que hemos insertado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="ce16e-215">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="ce16e-216">Copie y pegue el método **ExecuteSimpleQuery** después del método **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-216">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

            // Here we find the Andersen family via its LastName
            IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(f => f.LastName == "Andersen");

            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (Family family in familyQuery)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            // Now execute the same query via direct SQL
            IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                    "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                    queryOptions);

            Console.WriteLine("Running direct SQL query...");
            foreach (Family family in familyQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", family);
            }

            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="ce16e-217">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la creación del segundo documento.</span><span class="sxs-lookup"><span data-stu-id="ce16e-217">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="ce16e-218">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-218">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-219">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-219">Congratulations!</span></span> <span data-ttu-id="ce16e-220">Ha consultado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-220">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="ce16e-221">El siguiente diagrama muestra la denominación de la sintaxis de la consulta SQL de Azure Cosmos DB en la colección creada y se aplica la misma lógica a la consulta LINQ.</span><span class="sxs-lookup"><span data-stu-id="ce16e-221">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagrama que ilustra el ámbito y el significado de la consulta usada por el tutorial de NoSQL para crear una aplicación de consola de C#.](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="ce16e-223">La palabra clave [FROM](documentdb-sql-query.md#FromClause) es opcional en la consulta porque las consultas de Azure Cosmos DB ya tienen como ámbito una única colección.</span><span class="sxs-lookup"><span data-stu-id="ce16e-223">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="ce16e-224">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="ce16e-224">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="ce16e-225">Azure Cosmos DB deducirá la familia, la raíz o el nombre de variable elegido y hará referencia a la colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="ce16e-225">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="ce16e-226"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="ce16e-226"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="ce16e-227">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="ce16e-227">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="ce16e-228">Copie y pegue el método **ReplaceFamilyDocument** después del método **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-228">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="ce16e-229">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la ejecución de la consulta y al final del método.</span><span class="sxs-lookup"><span data-stu-id="ce16e-229">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="ce16e-230">Después de reemplazar el documento, este volverá a ejecutar la misma consulta para ver el documento modificado.</span><span class="sxs-lookup"><span data-stu-id="ce16e-230">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="ce16e-231">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-231">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-232">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-232">Congratulations!</span></span> <span data-ttu-id="ce16e-233">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-233">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ce16e-234"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="ce16e-234"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="ce16e-235">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="ce16e-235">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="ce16e-236">Copie y pegue el método **DeleteFamilyDocument** después del método **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="ce16e-236">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="ce16e-237">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la ejecución de la segunda consulta y al final del método.</span><span class="sxs-lookup"><span data-stu-id="ce16e-237">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="ce16e-238">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-238">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-239">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-239">Congratulations!</span></span> <span data-ttu-id="ce16e-240">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-240">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="ce16e-241"><a id="DeleteDatabase"></a>Paso 10: Eliminar la base de datos</span><span class="sxs-lookup"><span data-stu-id="ce16e-241"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="ce16e-242">La eliminación de la base de datos creada quitará la base de datos y todos los recursos secundarios (colecciones, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="ce16e-242">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="ce16e-243">Copie y pegue el código siguiente en el método **GetStartedDemo** después de la sección "delete" del documento para eliminar toda la base de datos y todos los recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="ce16e-243">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="ce16e-244">Presione **F5** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ce16e-244">Press **F5** to run your application.</span></span>

<span data-ttu-id="ce16e-245">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-245">Congratulations!</span></span> <span data-ttu-id="ce16e-246">Ha eliminado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ce16e-246">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="ce16e-247"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="ce16e-247"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="ce16e-248">Presione F5 en Visual Studio para compilar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="ce16e-248">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="ce16e-249">Ahora debería ver la salida de la aplicación de introducción en la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="ce16e-249">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="ce16e-250">La salida mostrará los resultados de las consultas que hemos agregado y debe coincidir con el texto de ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="ce16e-250">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
    Press any key to continue ...
    Created Family Andersen.1
    Press any key to continue ...
    Created Family Wakefield.7
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Replaced Family Andersen.1
    Press any key to continue ...
    Running LINQ query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Running direct SQL query...
        Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
    Deleted Family Andersen.1
    End of demo, press any key to exit.

<span data-ttu-id="ce16e-251">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ce16e-251">Congratulations!</span></span> <span data-ttu-id="ce16e-252">Ha completado este tutorial y tiene una aplicación de consola de C# en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="ce16e-252">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="ce16e-253"><a id="GetSolution"></a> Obtención de la solución completa del tutorial</span><span class="sxs-lookup"><span data-stu-id="ce16e-253"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="ce16e-254">Si no dispuso de tiempo para completar los pasos de este tutorial, o simplemente desea descargar los ejemplos de código, puede obtenerlos de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ce16e-254">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="ce16e-255">Para compilar la solución GetStarted, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="ce16e-255">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="ce16e-256">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="ce16e-256">An active Azure account.</span></span> <span data-ttu-id="ce16e-257">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="ce16e-257">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="ce16e-258">Una [cuenta de Azure Cosmos DB][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="ce16e-258">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="ce16e-259">La solución [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce16e-259">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="ce16e-260">Para restaurar las referencias al SDK de .NET para Azure Cosmos DB en Visual Studio, haga clic con el botón derecho en la solución **GetStarted** en el Explorador de soluciones y, después, haga clic en **Enable NuGet Package Restore** (Habilitar la restauración del paquete NuGet).</span><span class="sxs-lookup"><span data-stu-id="ce16e-260">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="ce16e-261">A continuación, en el archivo App.config, actualice los valores EndpointUrl y AuthorizationKey como se describe en el artículo sobre la [Conexión a una cuenta de Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="ce16e-261">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="ce16e-262">Y, eso es todo, genérela y habrá terminado.</span><span class="sxs-lookup"><span data-stu-id="ce16e-262">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="ce16e-263">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce16e-263">Next steps</span></span>
* <span data-ttu-id="ce16e-264">¿Desea un tutorial de ASP.NET MVC más complejo?</span><span class="sxs-lookup"><span data-stu-id="ce16e-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="ce16e-265">Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="ce16e-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="ce16e-266">¿Desea realizar pruebas de escala y de rendimiento con Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="ce16e-266">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="ce16e-267">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="ce16e-267">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="ce16e-268">Obtenga más información sobre cómo [supervisar las solicitudes, el uso y el almacenamiento de Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="ce16e-268">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="ce16e-269">Ejecute las consultas en nuestro conjunto de datos de ejemplo en el [área de consultas](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="ce16e-269">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="ce16e-270">Para más información sobre Azure Cosmos DB, consulte [Bienvenido a Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="ce16e-270">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
