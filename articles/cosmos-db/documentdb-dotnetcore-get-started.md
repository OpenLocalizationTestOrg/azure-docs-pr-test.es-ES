---
title: "Azure Cosmos DB: tutorial de introducción a las API de DocumentDB con .NET Core | Microsoft Docs"
description: "Un tutorial que crea una base de datos en línea y la aplicación de consola de C# con hello Azure Cosmos DB documentos API .NET Core SDK."
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
ms.openlocfilehash: 5e7efb327252e9e73e9b2a340820eeecc6937fa5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a><span data-ttu-id="f5213-103">Azure Cosmos DB: Introducción a .NET Core y de saludo API de documentos</span><span class="sxs-lookup"><span data-stu-id="f5213-103">Azure Cosmos DB: Getting started with hello DocumentDB API and .NET Core</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5213-104">.NET</span><span class="sxs-lookup"><span data-stu-id="f5213-104">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f5213-105">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f5213-105">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f5213-106">Node.js para MongoDB</span><span class="sxs-lookup"><span data-stu-id="f5213-106">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f5213-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="f5213-107">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f5213-108">Java</span><span class="sxs-lookup"><span data-stu-id="f5213-108">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f5213-109">C++</span><span class="sxs-lookup"><span data-stu-id="f5213-109">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f5213-110">Bienvenido toohello API de documentos para la base de datos de Azure Cosmos introducción con el tutorial de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f5213-110">Welcome toohello DocumentDB API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="f5213-111">Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.</span><span class="sxs-lookup"><span data-stu-id="f5213-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f5213-112">Describiremos:</span><span class="sxs-lookup"><span data-stu-id="f5213-112">We'll cover:</span></span>

* <span data-ttu-id="f5213-113">Creación y conexión de cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="f5213-113">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="f5213-114">Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5213-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="f5213-115">Creación de una base de datos en línea</span><span class="sxs-lookup"><span data-stu-id="f5213-115">Creating an online database</span></span>
* <span data-ttu-id="f5213-116">Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="f5213-116">Creating a collection</span></span>
* <span data-ttu-id="f5213-117">Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="f5213-117">Creating JSON documents</span></span>
* <span data-ttu-id="f5213-118">Consultar la colección de Hola</span><span class="sxs-lookup"><span data-stu-id="f5213-118">Querying hello collection</span></span>
* <span data-ttu-id="f5213-119">Sustitución de un documento</span><span class="sxs-lookup"><span data-stu-id="f5213-119">Replacing a document</span></span>
* <span data-ttu-id="f5213-120">Eliminación de un documento</span><span class="sxs-lookup"><span data-stu-id="f5213-120">Deleting a document</span></span>
* <span data-ttu-id="f5213-121">Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="f5213-121">Deleting hello database</span></span>

<span data-ttu-id="f5213-122">¿No tiene tiempo?</span><span class="sxs-lookup"><span data-stu-id="f5213-122">Don't have time?</span></span> <span data-ttu-id="f5213-123">¡No se preocupe!</span><span class="sxs-lookup"><span data-stu-id="f5213-123">Don't worry!</span></span> <span data-ttu-id="f5213-124">está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f5213-124">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="f5213-125">Saltar toohello [Obtenga una sección de solución completa de hello](#GetSolution) para obtener instrucciones rápidas.</span><span class="sxs-lookup"><span data-stu-id="f5213-125">Jump toohello [Get hello complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f5213-126">¿Desea toobuild una Xamarin iOS, Android o formularios utilizando la aplicación Hola documentos API y SDK para .NET Core?</span><span class="sxs-lookup"><span data-stu-id="f5213-126">Want toobuild a Xamarin iOS, Android, or Forms application using hello DocumentDB API and .NET Core SDK?</span></span> <span data-ttu-id="f5213-127">Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f5213-128">Hello Azure Cosmos DB .NET Core SDK utilizada en este tutorial aún no es compatible con aplicaciones de la plataforma Universal de Windows (UWP).</span><span class="sxs-lookup"><span data-stu-id="f5213-128">hello Azure Cosmos DB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps.</span></span> <span data-ttu-id="f5213-129">Para obtener una versión de vista previa de hello .NET Core SDK que admite las aplicaciones UWP, enviar correo electrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f5213-129">For a preview version of hello .NET Core SDK that does support UWP apps, send email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

<span data-ttu-id="f5213-130">Comencemos.</span><span class="sxs-lookup"><span data-stu-id="f5213-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5213-131">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="f5213-131">Prerequisites</span></span>
<span data-ttu-id="f5213-132">Asegúrese de que tiene Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f5213-132">Please make sure you have hello following:</span></span>

* <span data-ttu-id="f5213-133">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f5213-133">An active Azure account.</span></span> <span data-ttu-id="f5213-134">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f5213-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="f5213-135">Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f5213-135">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="f5213-136">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f5213-136">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="f5213-137">Si está trabajando en Mac OS o Linux, puede desarrollar aplicaciones de .NET Core de Hola de línea de comandos mediante la instalación de hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) para la plataforma de Hola de su elección.</span><span class="sxs-lookup"><span data-stu-id="f5213-137">If you're working on MacOS or Linux, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) for hello platform of your choice.</span></span> 
    * <span data-ttu-id="f5213-138">Si está trabajando en Windows, puede desarrollar aplicaciones de .NET Core de Hola de línea de comandos mediante la instalación de hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="f5213-138">If you're working on Windows, you can develop .NET Core apps from hello command-line by installing hello [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="f5213-139">Puede usar su propio editor o descargar [Visual Studio Code](https://code.visualstudio.com/), que es gratuito y funciona en Windows, Linux y MacOS.</span><span class="sxs-lookup"><span data-stu-id="f5213-139">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f5213-140">Paso 1: Creación de una cuenta de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5213-140">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f5213-141">Vamos a crear una cuenta de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-141">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f5213-142">Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="f5213-142">If you already have an account you want toouse, you can skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="f5213-143">Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[la instalación de la solución de Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="f5213-143">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f5213-144"><a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f5213-144"><a id="SetupVS"></a>Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="f5213-145">Abra **Visual Studio 2017** en el equipo.</span><span class="sxs-lookup"><span data-stu-id="f5213-145">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="f5213-146">En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="f5213-146">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="f5213-147">Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **.NET Core** / **Aplicación de consola (.NET Core)**, denomine el proyecto **DocumentDBGettingStarted**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f5213-147">In hello **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Captura de pantalla de ventana nuevo proyecto de hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="f5213-149">Hola **el Explorador de soluciones**, haga clic con el botón secundario en **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="f5213-149">In hello **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="f5213-150">A continuación, sin salir de menú de hello, haga clic en **administrar paquetes de NuGet...** .</span><span class="sxs-lookup"><span data-stu-id="f5213-150">Then without leaving hello menu, click on **Manage NuGet Packages...**.</span></span>

   ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="f5213-152">Hola **NuGet** , haga clic en **examinar** en parte superior de Hola de ventana hello y tipo **documentdb de azure** en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-152">In hello **NuGet** tab, click **Browse** at hello top of hello window, and type **azure documentdb** in hello search box.</span></span>
7. <span data-ttu-id="f5213-153">En los resultados de hello, buscar **Microsoft.Azure.DocumentDB.Core** y haga clic en **instalar**.</span><span class="sxs-lookup"><span data-stu-id="f5213-153">Within hello results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="f5213-154">Id. de paquete de Hola para hello biblioteca de cliente de documentos para .NET Core es [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="f5213-154">hello package ID for hello DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="f5213-155">Si su destino es una versión de .NET Framework (como net461) incompatible con este paquete de Nuget para .NET Core, use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), que es compatible con todas las versiones de .NET Framework a partir de .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="f5213-155">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="f5213-156">Mensajes de Hola, acepte las instalaciones del paquete de NuGet de Hola y el contrato de licencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-156">At hello prompts, accept hello NuGet package installations and hello license agreement.</span></span>

<span data-ttu-id="f5213-157">Estupendo.</span><span class="sxs-lookup"><span data-stu-id="f5213-157">Great!</span></span> <span data-ttu-id="f5213-158">Ahora que hemos terminado el programa de instalación de hello, vamos a empezar a escribir código.</span><span class="sxs-lookup"><span data-stu-id="f5213-158">Now that we finished hello setup, let's start writing some code.</span></span> <span data-ttu-id="f5213-159">Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f5213-159">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <span data-ttu-id="f5213-160"><a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan</span><span class="sxs-lookup"><span data-stu-id="f5213-160"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="f5213-161">En primer lugar, agregue estas referencias toohello a partir de la aplicación de C#, en el archivo Program.cs de hello:</span><span class="sxs-lookup"><span data-stu-id="f5213-161">First, add these references toohello beginning of your C# application, in hello Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART tooYOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> <span data-ttu-id="f5213-162">En Ordenar toocomplete este tutorial, asegúrese de que agregar las dependencias de hello anteriores.</span><span class="sxs-lookup"><span data-stu-id="f5213-162">In order toocomplete this tutorial, make sure you add hello dependencies above.</span></span>

<span data-ttu-id="f5213-163">Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.</span><span class="sxs-lookup"><span data-stu-id="f5213-163">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="f5213-164">A continuación, head toohello [Portal de Azure](https://portal.azure.com) tooretrieve el URI y la clave principal.</span><span class="sxs-lookup"><span data-stu-id="f5213-164">Next, head toohello [Azure Portal](https://portal.azure.com) tooretrieve your URI and primary key.</span></span> <span data-ttu-id="f5213-165">Hello Azure Cosmos DB URI y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-165">hello Azure Cosmos DB URI and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="f5213-166">Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**.</span><span class="sxs-lookup"><span data-stu-id="f5213-166">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="f5213-167">Copiar Hola URI desde el portal de Hola y pegarlos en `<your endpoint URI>` en el archivo program.cs de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-167">Copy hello URI from hello portal and paste it into `<your endpoint URI>` in hello program.cs file.</span></span> <span data-ttu-id="f5213-168">A continuación, copia Hola clave principal del portal de Hola y péguelo en `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="f5213-168">Then copy hello PRIMARY KEY from hello portal and paste it into `<your key>`.</span></span> <span data-ttu-id="f5213-169">Si usas hello Azure Cosmos DB emulador, utilice `https://localhost:8081` como punto de conexión de Hola y clave de autorización bien definido de Hola de [cómo usar toodevelop Hola emulador de base de datos de Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-169">If you are using hello Azure Cosmos DB Emulator, use `https://localhost:8081` as hello endpoint, and hello well-defined authorization key from [How toodevelop using hello Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="f5213-170">Realizar seguro hello tooremove < y >, pero deje Hola comillas dobles en el punto de conexión y la clave.</span><span class="sxs-lookup"><span data-stu-id="f5213-170">Make sure tooremove hello < and > but leave hello double quotes around your endpoint and key.</span></span>

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de C#.][keys]

<span data-ttu-id="f5213-173">Comenzaremos Hola obtener iniciada aplicación mediante la creación de una nueva instancia de hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f5213-173">We'll start hello getting started application by creating a new instance of hello **DocumentClient**.</span></span>

<span data-ttu-id="f5213-174">A continuación hello **Main** método, agregar esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia de nuestro nuevo **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="f5213-174">Below hello **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART tooYOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="f5213-175">Agregar código de hello siguiente toorun su tarea asincrónica de la **Main** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-175">Add hello following code toorun your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="f5213-176">Hola **Main** método detectará las excepciones y escribirlos toohello consola.</span><span class="sxs-lookup"><span data-stu-id="f5213-176">hello **Main** method will catch exceptions and write them toohello console.</span></span>

```csharp
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
```

<span data-ttu-id="f5213-177">Hola presione **DocumentDBGettingStarted** botón toobuild y ejecute la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f5213-177">Press hello **DocumentDBGettingStarted** button toobuild and run hello application.</span></span>

<span data-ttu-id="f5213-178">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-178">Congratulations!</span></span> <span data-ttu-id="f5213-179">Se ha conectado correctamente la cuenta de base de datos de Azure Cosmos tooan, ahora Echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f5213-179">You have successfully connected tooan Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="f5213-180">Paso 4: Creación de una base de datos</span><span class="sxs-lookup"><span data-stu-id="f5213-180">Step 4: Create a database</span></span>
<span data-ttu-id="f5213-181">Antes de agregar código de hello para la creación de una base de datos, agregue un método auxiliar para escribir toohello consola.</span><span class="sxs-lookup"><span data-stu-id="f5213-181">Before you add hello code for creating a database, add a helper method for writing toohello console.</span></span>

<span data-ttu-id="f5213-182">Copie y pegue hello **WriteToConsoleAndPromptToContinue** method hello **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-182">Copy and paste hello **WriteToConsoleAndPromptToContinue** method underneath hello **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="f5213-183">La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="f5213-183">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="f5213-184">Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.</span><span class="sxs-lookup"><span data-stu-id="f5213-184">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="f5213-185">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-185">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello client creation.</span></span> <span data-ttu-id="f5213-186">Así se creará una base de datos denominada *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="f5213-186">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="f5213-187">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-187">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-188">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-188">Congratulations!</span></span> <span data-ttu-id="f5213-189">Ha creado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-189">You have successfully created an Azure Cosmos DB database.</span></span>  

## <span data-ttu-id="f5213-190"><a id="CreateColl"></a>Paso 5: Creación de una colección</span><span class="sxs-lookup"><span data-stu-id="f5213-190"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f5213-191">**CreateDocumentCollectionAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios.</span><span class="sxs-lookup"><span data-stu-id="f5213-191">**CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="f5213-192">Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f5213-192">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>

<span data-ttu-id="f5213-193">A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="f5213-193">A [collection](documentdb-resources.md#collections) can be created by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="f5213-194">Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f5213-194">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="f5213-195">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-195">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello database creation.</span></span> <span data-ttu-id="f5213-196">Esto creará una colección de documentos denominada *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="f5213-196">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="f5213-197">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-197">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-198">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-198">Congratulations!</span></span> <span data-ttu-id="f5213-199">Ha creado correctamente una colección de documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-199">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <span data-ttu-id="f5213-200"><a id="CreateDoc"></a>Paso 6: Creación de documentos JSON</span><span class="sxs-lookup"><span data-stu-id="f5213-200"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="f5213-201">A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase.</span><span class="sxs-lookup"><span data-stu-id="f5213-201">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="f5213-202">Los documentos son contenido JSON definido por el usuario (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="f5213-202">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f5213-203">Ahora podemos insertar uno o varios documentos.</span><span class="sxs-lookup"><span data-stu-id="f5213-203">We can now insert one or more documents.</span></span> <span data-ttu-id="f5213-204">Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-204">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="f5213-205">En primer lugar, necesitamos toocreate una **familia** clases que representan objetos almacenados en la base de datos de Azure Cosmos en este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="f5213-205">First, we need toocreate a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="f5213-206">También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**.</span><span class="sxs-lookup"><span data-stu-id="f5213-206">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="f5213-207">Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON.</span><span class="sxs-lookup"><span data-stu-id="f5213-207">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="f5213-208">Crear estas clases mediante la adición de hello siguientes subclases internos después de hello **GetStartedDemo** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-208">Create these classes by adding hello following internal sub-classes after hello **GetStartedDemo** method.</span></span>

<span data-ttu-id="f5213-209">Copie y pegue hello **familia**, **primario**, **secundarios**, **mascota**, y **dirección** clases debajo Hola **WriteToConsoleAndPromptToContinue** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-209">Copy and paste hello **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath hello **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
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
```

<span data-ttu-id="f5213-210">Copie y pegue hello **CreateFamilyDocumentIfNotExists** método debajo de su **CreateDocumentCollectionIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-210">Copy and paste hello **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="f5213-211">E insertar otros dos documentos, uno para hello Andersen familia y hello Wakefield familia.</span><span class="sxs-lookup"><span data-stu-id="f5213-211">And insert two documents, one each for hello Andersen Family and hello Wakefield Family.</span></span>

<span data-ttu-id="f5213-212">Copie y pegue el código de hello que sigue a `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** método debajo de creación de colección de documentos de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-212">Copy and paste hello code that follows `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** method underneath hello document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

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

<span data-ttu-id="f5213-213">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-213">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-214">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-214">Congratulations!</span></span> <span data-ttu-id="f5213-215">Ha creado correctamente dos documentos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-215">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagrama que ilustra relación jerárquica Hola entre la cuenta de hello, base de datos en línea hello, colección de Hola y documentos de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="f5213-217"><a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f5213-217"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f5213-218">Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.</span><span class="sxs-lookup"><span data-stu-id="f5213-218">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="f5213-219">Hello código de ejemplo siguiente muestra varias consultas: usar ambos SQL de base de datos de Azure Cosmos sintaxis, así como LINQ - que podemos ejecutar contra Hola se insertan en el paso anterior de hello documentos.</span><span class="sxs-lookup"><span data-stu-id="f5213-219">hello following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against hello documents we inserted in hello previous step.</span></span>

<span data-ttu-id="f5213-220">Copie y pegue hello **ExecuteSimpleQuery** método debajo de su **CreateFamilyDocumentIfNotExists** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-220">Copy and paste hello **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
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
```

<span data-ttu-id="f5213-221">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de documentos de segundo de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-221">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="f5213-222">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-222">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-223">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-223">Congratulations!</span></span> <span data-ttu-id="f5213-224">Ha consultado correctamente una colección de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-224">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="f5213-225">Hello siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado y hello misma lógica aplica también la consulta LINQ de toohello.</span><span class="sxs-lookup"><span data-stu-id="f5213-225">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created, and hello same logic applies toohello LINQ query as well.</span></span>

![Diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="f5213-227">Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección.</span><span class="sxs-lookup"><span data-stu-id="f5213-227">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="f5213-228">Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija.</span><span class="sxs-lookup"><span data-stu-id="f5213-228">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="f5213-229">Documentos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="f5213-229">DocumentDB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

## <span data-ttu-id="f5213-230"><a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON</span><span class="sxs-lookup"><span data-stu-id="f5213-230"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="f5213-231">Azure Cosmos DB admite la sustitución de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f5213-231">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="f5213-232">Copie y pegue hello **ReplaceFamilyDocument** método debajo de su **ExecuteSimpleQuery** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-232">Copy and paste hello **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f5213-233">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de la ejecución de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-233">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello query execution.</span></span> <span data-ttu-id="f5213-234">Después de reemplazar el documento de hello, ejecutará Hola mismo volver a consultar tooview Hola cambiado documento.</span><span class="sxs-lookup"><span data-stu-id="f5213-234">After replacing hello document, this will run hello same query again tooview hello changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="f5213-235">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-235">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-236">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-236">Congratulations!</span></span> <span data-ttu-id="f5213-237">Ha sustituido correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-237">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f5213-238"><a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON</span><span class="sxs-lookup"><span data-stu-id="f5213-238"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="f5213-239">Azure Cosmos DB admite la eliminación de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="f5213-239">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="f5213-240">Copie y pegue hello **DeleteFamilyDocument** método debajo de su **ReplaceFamilyDocument** método.</span><span class="sxs-lookup"><span data-stu-id="f5213-240">Copy and paste hello **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f5213-241">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de la segunda ejecución de la consulta de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-241">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="f5213-242">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-242">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-243">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-243">Congratulations!</span></span> <span data-ttu-id="f5213-244">Ha eliminado correctamente un documento de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-244">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f5213-245"><a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="f5213-245"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="f5213-246">Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).</span><span class="sxs-lookup"><span data-stu-id="f5213-246">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f5213-247">Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** method documento Hola Eliminar base de datos completa de toodelete hello y todos los recursos de los elementos secundarios.</span><span class="sxs-lookup"><span data-stu-id="f5213-247">Copy and paste hello following code tooyour **GetStartedDemo** method underneath hello document delete toodelete hello entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="f5213-248">Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f5213-248">Press hello **DocumentDBGettingStarted** button toorun your application.</span></span>

<span data-ttu-id="f5213-249">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-249">Congratulations!</span></span> <span data-ttu-id="f5213-250">Ha eliminado correctamente una base de datos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f5213-250">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="f5213-251"><a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#</span><span class="sxs-lookup"><span data-stu-id="f5213-251"><a id="Run"></a>Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="f5213-252">Hola presione **DocumentDBGettingStarted** botón de aplicación de Visual Studio toobuild hello en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="f5213-252">Press hello **DocumentDBGettingStarted** button in Visual Studio toobuild hello application in debug mode.</span></span>

<span data-ttu-id="f5213-253">Debería ver la salida de hello de la aplicación iniciada get en la ventana de la consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="f5213-253">You should see hello output of your get started app in hello console window.</span></span> <span data-ttu-id="f5213-254">salida de Hello mostrará resultados Hola de hello las consultas se agregan y se debe coincidir con el texto de ejemplo de Hola a continuación.</span><span class="sxs-lookup"><span data-stu-id="f5213-254">hello output will show hello results of hello queries we added and should match hello example text below.</span></span>

```
Created FamilyDB_oa
Press any key toocontinue ...
Created FamilyCollection_oa
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
```

<span data-ttu-id="f5213-255">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="f5213-255">Congratulations!</span></span> <span data-ttu-id="f5213-256">Ha completado el tutorial de Hola y tiene una aplicación de consola de C# de trabajo.</span><span class="sxs-lookup"><span data-stu-id="f5213-256">You've completed hello tutorial and have a working C# console application!</span></span>

## <span data-ttu-id="f5213-257"><a id="GetSolution"></a>Obtener la solución del tutorial completo Hola</span><span class="sxs-lookup"><span data-stu-id="f5213-257"><a id="GetSolution"></a> Get hello complete tutorial solution</span></span>
<span data-ttu-id="f5213-258">solución GetStarted de hello toobuild que contiene todos los ejemplos de hello en este artículo, se necesita Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="f5213-258">toobuild hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="f5213-259">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="f5213-259">An active Azure account.</span></span> <span data-ttu-id="f5213-260">Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f5213-260">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="f5213-261">Una [cuenta de Azure Cosmos DB][create-documentdb-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="f5213-261">An [Azure Cosmos DB account][create-documentdb-dotnet.md#create-account].</span></span>
* <span data-ttu-id="f5213-262">Hola [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solución disponible en GitHub.</span><span class="sxs-lookup"><span data-stu-id="f5213-262">hello [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="f5213-263">toorestore Hola referencias toohello API de documentos Azure Cosmos DB SDK para .NET Core en Visual Studio, haga clic en hello **GetStarted** solución en el Explorador de soluciones y, a continuación, haga clic en **habilitar Restaurar el paquete NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f5213-263">toorestore hello references toohello DocumentDB API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click hello **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="f5213-264">A continuación, en el archivo Program.cs de hello, actualizar valores de hello EndpointUrl y AuthorizationKey tal y como se describe en [conectar la cuenta de base de datos de Azure Cosmos tooan](#Connect).</span><span class="sxs-lookup"><span data-stu-id="f5213-264">Next, in hello Program.cs file, update hello EndpointUrl and AuthorizationKey values as described in [Connect tooan Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5213-265">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f5213-265">Next steps</span></span>
* <span data-ttu-id="f5213-266">¿Desea un tutorial de ASP.NET MVC más complejo?</span><span class="sxs-lookup"><span data-stu-id="f5213-266">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="f5213-267">Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-267">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="f5213-268">¿Desea toodevelop una Xamarin iOS, Android o formularios utilizando la aplicación Hola API de documentos Azure Cosmos DB SDK para .NET Core?</span><span class="sxs-lookup"><span data-stu-id="f5213-268">Want toodevelop a Xamarin iOS, Android, or Forms application using hello DocumentDB API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="f5213-269">Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-269">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="f5213-270">¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos?</span><span class="sxs-lookup"><span data-stu-id="f5213-270">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="f5213-271">Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-271">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="f5213-272">Obtenga información acerca de cómo demasiado[solicitudes, uso y almacenamiento de base de datos de Monitor Azure Cosmos](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="f5213-272">Learn how too[Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="f5213-273">Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="f5213-273">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f5213-274">toolearn más información acerca del modelo de programación de hello, consulte [base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="f5213-274">toolearn more about hello programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
