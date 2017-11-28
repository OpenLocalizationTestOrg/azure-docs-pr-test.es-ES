---
title: "Azure Cosmos DB: tutorial de introducción a las API de DocumentDB con .NET Core | Microsoft Docs"
description: "Tutorial en el que crea una base de datos en línea y la aplicación de consola de C# mediante el SDK de .NET Core de la API de DocumentDB de Azure Cosmos DB."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: jhubbard
editor: 
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 7536978bbb1e41b6484b66fd1b51c900fc3e545d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-getting-started-with-the-documentdb-api-and-net-core"></a><span data-ttu-id="2856e-103">Azure Cosmos DB: introducción a la API de DocumentDB y .NET Core</span><span class="sxs-lookup"><span data-stu-id="2856e-103">Azure Cosmos DB: Getting started with the DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2856e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="2856e-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="2856e-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="2856e-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="2856e-106">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="2856e-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="2856e-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="2856e-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="2856e-108">Java</span><span class="sxs-lookup"><span data-stu-id="2856e-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="2856e-109">C++</span><span class="sxs-lookup"><span data-stu-id="2856e-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="2856e-110">Bienvenido al tutorial de introducción de la API de DocumentDB para Azure Cosmos DB con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2856e-110">Welcome to the DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="2856e-111">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="2856e-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="2856e-112">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="2856e-112">We'll cover:</span></span>

* <span data-ttu-id="2856e-113">Creación de una cuenta de Azure Cosmos DB y conexión a ella</span><span class="sxs-lookup"><span data-stu-id="2856e-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="2856e-114">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2856e-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="2856e-115">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="2856e-115">Creating an online database</span></span>
* <span data-ttu-id="2856e-116">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="2856e-116">Creating a collection</span></span>
* <span data-ttu-id="2856e-117">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="2856e-117">Creating JSON documents</span></span>
* <span data-ttu-id="2856e-118">Consulta de la colección</span><span class="sxs-lookup"><span data-stu-id="2856e-118">Querying the collection</span></span>
* <span data-ttu-id="2856e-119">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="2856e-119">Replacing a document</span></span>
* <span data-ttu-id="2856e-120">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="2856e-120">Deleting a document</span></span>
* <span data-ttu-id="2856e-121">Eliminación de la base de datos</span><span class="sxs-lookup"><span data-stu-id="2856e-121">Deleting the database</span></span>

<span data-ttu-id="2856e-122">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="2856e-122">Don't have time?</span></span> <span data-ttu-id="2856e-123">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="2856e-123">Don't worry!</span></span> <span data-ttu-id="2856e-124">La solución completa está disponible en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2856e-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="2856e-125">Para obtener instrucciones rápidas, diríjase a la sección [Obtener la solución completa del tutorial de NoSQL](#GetSolution) .</span><span class="sxs-lookup"><span data-stu-id="2856e-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="2856e-126">¿Desea compilar una aplicación de Xamarin iOS, Android o Forms mediante la API de DocumentDB y el SDK de .NET Core?</span><span class="sxs-lookup"><span data-stu-id="2856e-126">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="2856e-127">Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2856e-128">El SDK de .NET Core de Azure Cosmos DB que se usa en este tutorial no es aún compatible con aplicaciones de la Plataforma universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="2856e-128">The Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="2856e-129">Para obtener una versión preliminar del SDK de .NET Core que admita aplicaciones de UWP, envíe un correo electrónico a [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2856e-129">For a preview version of the .NET Core SDK that does support UWP apps, send email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="2856e-130">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="2856e-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2856e-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="2856e-131">Prerequisites</span></span>
<span data-ttu-id="2856e-132">Asegúrese de que dispone de lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2856e-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="2856e-133">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2856e-133">An active Azure account.</span></span> <span data-ttu-id="2856e-134">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2856e-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="2856e-135">Como alternativa, en este tutorial puede usar el [Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-135">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="2856e-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="2856e-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="2856e-137">Si está trabajando en MacOS o Linux, puede desarrollar aplicaciones de .NET Core desde la línea de comandos mediante la instalación del [SDK de .NET Core](https://www.microsoft.com/net/core#macos) para la plataforma que elija.</span><span class="sxs-lookup"><span data-stu-id="2856e-137">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="2856e-138">Si está trabajando en Windows, puede desarrollar aplicaciones de .NET Core desde la línea de comandos mediante la instalación del [SDK de .NET Core](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="2856e-138">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="2856e-139">Puede usar su propio editor o descargar [Visual Studio Code](https://code.visualstudio.com/), que es gratuito y funciona en Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="2856e-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="2856e-140">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2856e-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2856e-141">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="2856e-142">Si ya tiene una cuenta que desea usar, puede ir directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2856e-142">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="2856e-143">Si usa el Emulador de Azure Cosmos DB, siga los pasos que se indican en [Emulador de Azure Cosmos DB](local-emulator.md) para configurar el emulador y vaya directamente a [Configuración de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2856e-143">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="2856e-144"><a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2856e-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="2856e-145">Abra **Visual Studio 2017** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="2856e-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="2856e-146">En el menú **Archivo**, seleccione **Nuevo** y elija **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="2856e-146">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="2856e-147">En el cuadro de diálogo **Nuevo proyecto**, seleccione **Plantillas** / **Visual C#** / **.NET Core**/**Aplicación de consola (.NET Core)**, asigne un nombre a su proyecto **DocumentDBGettingStarted** y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2856e-147">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Captura de pantalla de la ventana Nuevo proyecto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="2856e-149">En el **Explorador de soluciones**, haga clic con el botón derecho en **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="2856e-149">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="2856e-150">Luego, sin dejar el menú, haga clic en **Administrar paquetes NuGet...**.</span><span class="sxs-lookup"><span data-stu-id="2856e-150">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Captura de pantalla del menú contextual del proyecto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="2856e-152">En la pestaña **NuGet** haga clic en **Examinar**, en la parte superior de la ventana, y escriba **azure documentdb** en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="2856e-152">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="2856e-153">En los resultados, busque **Microsoft.Azure.DocumentDB.Core** y haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="2856e-153">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="2856e-154">El identificador del paquete de la biblioteca de cliente de DocumentDB para .NET Core es [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="2856e-154">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="2856e-155">Si su destino es una versión de .NET Framework (como net461) incompatible con este paquete de Nuget para .NET Core, use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), que es compatible con todas las versiones de .NET Framework a partir de .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="2856e-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="2856e-156">Cuando se le solicite, acepte el contrato de licencia y las instalaciones de los paquetes de Nuget.</span><span class="sxs-lookup"><span data-stu-id="2856e-156">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="2856e-157">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="2856e-157">Great!</span></span> <span data-ttu-id="2856e-158">Ahora que hemos terminado la configuración, comencemos a escribir algo de código.</span><span class="sxs-lookup"><span data-stu-id="2856e-158">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="2856e-159">Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="2856e-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="2856e-160"><a id="Connect"></a>Paso 3: Conexión a una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2856e-160"><a id="Connect"></a>Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="2856e-161">En primer lugar, agregue estas referencias al principio de la aplicación de C#, en el archivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="2856e-161">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="2856e-162">Para poder completar este tutorial, asegúrese de agregar las dependencias anteriores.</span><span class="sxs-lookup"><span data-stu-id="2856e-162">In order to complete this tutorial, make sure you add the dependencies above.</span></span>

<span data-ttu-id="2856e-163">Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="2856e-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="2856e-164">Seguidamente, diríjase al [Portal de Azure](https://portal.azure.com) para recuperar el identificador URI y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="2856e-164">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="2856e-165">El URI y la clave principal de Azure Cosmos DB son necesarios para que la aplicación sepa a dónde debe conectarse y para que Azure Cosmos DB confíe en la conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-165">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="2856e-166">En Azure Portal, vaya a la cuenta de Azure Cosmos DB y haga clic en **Claves**.</span><span class="sxs-lookup"><span data-stu-id="2856e-166">In the Azure Portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="2856e-167">Copie el URI desde el Portal y péguelo en `<your endpoint URI>` en el archivo program.cs.</span><span class="sxs-lookup"><span data-stu-id="2856e-167">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="2856e-168">Después, copie la CLAVE PRINCIPAL del Portal y péguela en `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="2856e-168">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="2856e-169">Si está usando el Emulador de Azure Cosmos DB, utilice `https://localhost:8081` como punto de conexión y la clave de autorización bien definida del artículo sobre [Desarrollo con el Emulador de Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-169">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="2856e-170">Asegúrese de quitar el < and > pero deje las comillas dobles alrededor de la clave y el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="2856e-170">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Captura de pantalla del Portal de Azure usada por el tutorial de NoSQL para crear una aplicación de consola de C#.][keys]

<span data-ttu-id="2856e-173">Iniciaremos la aplicación de introducción, para lo que crearemos una nueva instancia de **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2856e-173">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="2856e-174">Debajo del método **Main**, agregue esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia del nuevo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2856e-174">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="2856e-175">Agregue el siguiente código para ejecutar la tarea asincrónica desde el método **Main** .</span><span class="sxs-lookup"><span data-stu-id="2856e-175">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="2856e-176">El método **Main** detectará las excepciones y las escribirá en la consola.</span><span class="sxs-lookup"><span data-stu-id="2856e-176">The **Main** method will catch exceptions and write them to the console.</span></span>

```csharp
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
```

<span data-ttu-id="2856e-177">Presione el botón **DocumentDBGettingStarted** para compilar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-177">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="2856e-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-178">Congratulations!</span></span> <span data-ttu-id="2856e-179">Se ha conectado correctamente a una cuenta de Azure Cosmos DB y ahora se explicará cómo trabajar con recursos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-179">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="2856e-180">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="2856e-180">Step 4: Create a database</span></span>
<span data-ttu-id="2856e-181">Antes de agregar el código para crear una base de datos, agregue un método auxiliar para escribirlo en la consola.</span><span class="sxs-lookup"><span data-stu-id="2856e-181">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="2856e-182">Copie y pegue el método **WriteToConsoleAndPromptToContinue** debajo del método **GetStartedDemo**.</span><span class="sxs-lookup"><span data-stu-id="2856e-182">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="2856e-183">Para crear una [base de datos](documentdb-resources.md#databases) de Azure Cosmos DB, puede usar el método [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2856e-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2856e-184">Una base de datos es un contenedor lógico de almacenamiento de documentos JSON particionado en recopilaciones.</span><span class="sxs-lookup"><span data-stu-id="2856e-184">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="2856e-185">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la creación del cliente.</span><span class="sxs-lookup"><span data-stu-id="2856e-185">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="2856e-186">Así se creará una base de datos denominada *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="2856e-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="2856e-187">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-187">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-188">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-188">Congratulations!</span></span> <span data-ttu-id="2856e-189">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="2856e-190"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="2856e-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="2856e-191">**CreateDocumentCollectionAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="2856e-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="2856e-192">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2856e-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="2856e-193">Una [colección](documentdb-resources.md#collections) puede crearse mediante el método [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2856e-193">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2856e-194">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2856e-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="2856e-195">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la creación de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="2856e-195">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="2856e-196">Esto creará una colección de documentos denominada *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="2856e-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="2856e-197">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-197">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-198">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-198">Congratulations!</span></span> <span data-ttu-id="2856e-199">Ha creado correctamente una colección de documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="2856e-200"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="2856e-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="2856e-201">Un [documento](documentdb-resources.md#documents) puede crearse mediante el método [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) de la clase **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2856e-201">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="2856e-202">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="2856e-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="2856e-203">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="2856e-203">We can now insert one or more documents.</span></span> <span data-ttu-id="2856e-204">Si ya dispone de datos que desea almacenar en la base de datos, puede usar la [herramienta de migración de datos](import-data.md) de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-204">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="2856e-205">En primer lugar, es preciso crear una clase denominada **Family** que represente los objetos almacenados en Azure Cosmos DB en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="2856e-205">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="2856e-206">También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**.</span><span class="sxs-lookup"><span data-stu-id="2856e-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="2856e-207">Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON.</span><span class="sxs-lookup"><span data-stu-id="2856e-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="2856e-208">Para agregar estas clases, agregue las siguientes subclases internas después del método **GetStartedDemo** .</span><span class="sxs-lookup"><span data-stu-id="2856e-208">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="2856e-209">Copie y pegue las clases **Family**, **Parent**, **Child**, **Pet** y **Address** debajo del método **WriteToConsoleAndPromptToContinue**.</span><span class="sxs-lookup"><span data-stu-id="2856e-209">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="2856e-210">Copie y pegue el método **CreateFamilyDocumentIfNotExists** debajo del método **CreateDocumentCollectionIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="2856e-210">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="2856e-211">E inserte dos documentos, uno para la familia Andersen y otro para la familia Wakefield.</span><span class="sxs-lookup"><span data-stu-id="2856e-211">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="2856e-212">Copie y pegue el código siguiente `// ADD THIS PART TO YOUR CODE` en el método **GetStartedDemo** debajo de la creación de la colección de documentos.</span><span class="sxs-lookup"><span data-stu-id="2856e-212">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

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

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="2856e-213">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-213">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-214">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-214">Congratulations!</span></span> <span data-ttu-id="2856e-215">Ha creado correctamente dos documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que muestra la relación jerárquica entre la cuenta, la base de datos en línea, la colección y los documentos usados por el tutorial NoSQL para crear una aplicación de consola de C#.](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="2856e-217"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2856e-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="2856e-218">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="2856e-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="2856e-219">En el siguiente ejemplo, se muestran diversas consultas (usando la sintaxis SQL tanto de Azure Cosmos DB como LINQ) que podemos ejecutar en los documentos que hemos insertado en el paso anterior.</span><span class="sxs-lookup"><span data-stu-id="2856e-219">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="2856e-220">Copie y pegue el método **ExecuteSimpleQuery** debajo del método **CreateFamilyDocumentIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="2856e-220">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="2856e-221">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la creación del segundo documento.</span><span class="sxs-lookup"><span data-stu-id="2856e-221">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="2856e-222">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-222">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-223">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-223">Congratulations!</span></span> <span data-ttu-id="2856e-224">Ha consultado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="2856e-225">El siguiente diagrama muestra la denominación de la sintaxis de la consulta SQL de Azure Cosmos DB en la colección creada y se aplica la misma lógica a la consulta LINQ.</span><span class="sxs-lookup"><span data-stu-id="2856e-225">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagrama que ilustra el ámbito y el significado de la consulta usada por el tutorial de NoSQL para crear una aplicación de consola de C#.](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="2856e-227">La palabra clave [FROM](documentdb-sql-query.md#FromClause) es opcional en la consulta porque las consultas de Azure Cosmos DB ya tienen como ámbito una única colección.</span><span class="sxs-lookup"><span data-stu-id="2856e-227">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="2856e-228">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="2856e-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="2856e-229">DocumentDB deducirá la familia, la raíz o el nombre de variable elegido y hará referencia a la colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2856e-229">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <span data-ttu-id="2856e-230"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="2856e-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="2856e-231">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="2856e-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="2856e-232">Copie y pegue el método **ReplaceFamilyDocument** debajo del método **ExecuteSimpleQuery**.</span><span class="sxs-lookup"><span data-stu-id="2856e-232">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="2856e-233">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la ejecución de la consulta.</span><span class="sxs-lookup"><span data-stu-id="2856e-233">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="2856e-234">Después de reemplazar el documento, este volverá a ejecutar la misma consulta para ver el documento modificado.</span><span class="sxs-lookup"><span data-stu-id="2856e-234">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="2856e-235">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-235">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-236">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-236">Congratulations!</span></span> <span data-ttu-id="2856e-237">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="2856e-238"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="2856e-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="2856e-239">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="2856e-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="2856e-240">Copie y pegue el método **DeleteFamilyDocument debajo** del método **ReplaceFamilyDocument**.</span><span class="sxs-lookup"><span data-stu-id="2856e-240">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="2856e-241">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la ejecución de la segunda consulta.</span><span class="sxs-lookup"><span data-stu-id="2856e-241">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="2856e-242">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-242">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-243">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-243">Congratulations!</span></span> <span data-ttu-id="2856e-244">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="2856e-245"><a id="DeleteDatabase"></a>Paso 10: Eliminar la base de datos</span><span class="sxs-lookup"><span data-stu-id="2856e-245"><a id="DeleteDatabase"></a>Step 10: Delete the database</span></span>
<span data-ttu-id="2856e-246">La eliminación de la base de datos creada quitará la base de datos y todos los recursos secundarios (colecciones, documentos, etc.).</span><span class="sxs-lookup"><span data-stu-id="2856e-246">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="2856e-247">Copie y pegue el código siguiente en el método **GetStartedDemo** debajo de la sección "delete" del documento para eliminar toda la base de datos y todos los recursos secundarios.</span><span class="sxs-lookup"><span data-stu-id="2856e-247">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="2856e-248">Presione el botón **DocumentDBGettingStarted** para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="2856e-248">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="2856e-249">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-249">Congratulations!</span></span> <span data-ttu-id="2856e-250">Ha eliminado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2856e-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="2856e-251"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="2856e-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="2856e-252">Presione el botón **DocumentDBGettingStarted** en Visual Studio para compilar la aplicación en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="2856e-252">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="2856e-253">Ahora debería ver la salida de la aplicación de introducción en la ventana de la consola.</span><span class="sxs-lookup"><span data-stu-id="2856e-253">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="2856e-254">La salida mostrará los resultados de las consultas que hemos agregado y debe coincidir con el texto de ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="2856e-254">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="2856e-255">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="2856e-255">Congratulations!</span></span> <span data-ttu-id="2856e-256">Ha completado este tutorial y tiene una aplicación de consola de C# en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="2856e-256">You've completed the tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="2856e-257"><a id="GetSolution"></a> Obtención de la solución completa del tutorial</span><span class="sxs-lookup"><span data-stu-id="2856e-257"><a id="GetSolution"></a> Get the complete tutorial solution</span></span>
<span data-ttu-id="2856e-258">Para compilar la solución GetStarted que contiene todos los ejemplos de este artículo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2856e-258">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="2856e-259">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="2856e-259">An active Azure account.</span></span> <span data-ttu-id="2856e-260">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="2856e-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="2856e-261">Una [cuenta de Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="2856e-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="2856e-262">La solución [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) está disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="2856e-262">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="2856e-263">Para restaurar las referencias a la API de DocumentDB para el SDK de .NET Core para Azure Cosmos DB en Visual Studio, haga clic con el botón derecho en la solución **GetStarted** en el Explorador de soluciones y, después, haga clic en **Enable NuGet Package Restore** (Habilitar la restauración del paquete NuGet).</span><span class="sxs-lookup"><span data-stu-id="2856e-263">To restore the references to the DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="2856e-264">A continuación, en el archivo Program.cs , actualice los valores EndpointUrl y AuthorizationKey como se describe en el artículo sobre la [Conexión a una cuenta de Azure Cosmos DB](#Connect).</span><span class="sxs-lookup"><span data-stu-id="2856e-264">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2856e-265">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2856e-265">Next steps</span></span>
* <span data-ttu-id="2856e-266">¿Desea un tutorial de ASP.NET MVC más complejo?</span><span class="sxs-lookup"><span data-stu-id="2856e-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="2856e-267">Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="2856e-268">¿Desea desarrollar una aplicación de Xamarin iOS, Android o Forms mediante la API de DocumentDB para el SDK de .NET Core de Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="2856e-268">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="2856e-269">Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="2856e-270">¿Desea realizar pruebas de escala y de rendimiento con Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="2856e-270">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="2856e-271">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="2856e-272">Obtenga más información sobre cómo [Supervisión de las solicitudes, uso y almacenamiento de Azure Cosmos DB](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="2856e-272">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="2856e-273">Ejecute las consultas en nuestro conjunto de datos de ejemplo en el [área de consultas](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="2856e-273">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="2856e-274">Para más información sobre el modelo de programación, consulte [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2856e-274">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
