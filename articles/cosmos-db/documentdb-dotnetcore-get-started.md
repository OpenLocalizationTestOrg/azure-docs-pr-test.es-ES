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
# <a name="azure-cosmos-db-getting-started-with-hello-documentdb-api-and-net-core"></a>Azure Cosmos DB: Introducción a .NET Core y de saludo API de documentos
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenido toohello API de documentos para la base de datos de Azure Cosmos introducción con el tutorial de .NET Core. Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.

Describiremos:

* Creación y conexión de cuenta de base de datos de Azure Cosmos tooan
* Configuración de la solución de Visual Studio
* Creación de una base de datos en línea
* Creación de una colección
* Creación de documentos JSON
* Consultar la colección de Hola
* Sustitución de un documento
* Eliminación de un documento
* Eliminar base de datos de Hola

¿No tiene tiempo? ¡No se preocupe! está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started). Saltar toohello [Obtenga una sección de solución completa de hello](#GetSolution) para obtener instrucciones rápidas.

¿Desea toobuild una Xamarin iOS, Android o formularios utilizando la aplicación Hola documentos API y SDK para .NET Core? Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).

> [!NOTE]
> Hello Azure Cosmos DB .NET Core SDK utilizada en este tutorial aún no es compatible con aplicaciones de la plataforma Universal de Windows (UWP). Para obtener una versión de vista previa de hello .NET Core SDK que admite las aplicaciones UWP, enviar correo electrónico demasiado[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

Comencemos.

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.
* [Visual Studio 2017](https://www.visualstudio.com/vs/) 
    * Si está trabajando en Mac OS o Linux, puede desarrollar aplicaciones de .NET Core de Hola de línea de comandos mediante la instalación de hello [.NET Core SDK](https://www.microsoft.com/net/core#macos) para la plataforma de Hola de su elección. 
    * Si está trabajando en Windows, puede desarrollar aplicaciones de .NET Core de Hola de línea de comandos mediante la instalación de hello [.NET Core SDK](https://www.microsoft.com/net/core#windows). 
    * Puede usar su propio editor o descargar [Visual Studio Code](https://code.visualstudio.com/), que es gratuito y funciona en Windows, Linux y MacOS. 

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Vamos a crear una cuenta de Azure Cosmos DB. Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la solución de Visual Studio](#SetupVS). Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[la instalación de la solución de Visual Studio](#SetupVS).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio
1. Abra **Visual Studio 2017** en el equipo.
2. En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.
3. Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **.NET Core** / **Aplicación de consola (.NET Core)**, denomine el proyecto **DocumentDBGettingStarted**y, a continuación, haga clic en **Aceptar**.

   ![Captura de pantalla de ventana nuevo proyecto de hello](./media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. Hola **el Explorador de soluciones**, haga clic con el botón secundario en **DocumentDBGettingStarted**.
5. A continuación, sin salir de menú de hello, haga clic en **administrar paquetes de NuGet...** .

   ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. Hola **NuGet** , haga clic en **examinar** en parte superior de Hola de ventana hello y tipo **documentdb de azure** en el cuadro de búsqueda de Hola.
7. En los resultados de hello, buscar **Microsoft.Azure.DocumentDB.Core** y haga clic en **instalar**.
   Id. de paquete de Hola para hello biblioteca de cliente de documentos para .NET Core es [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core). Si su destino es una versión de .NET Framework (como net461) incompatible con este paquete de Nuget para .NET Core, use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB), que es compatible con todas las versiones de .NET Framework a partir de .NET Framework 4.5.
8. Mensajes de Hola, acepte las instalaciones del paquete de NuGet de Hola y el contrato de licencia de Hola.

Estupendo. Ahora que hemos terminado el programa de instalación de hello, vamos a empezar a escribir código. Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).

## <a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan
En primer lugar, agregue estas referencias toohello a partir de la aplicación de C#, en el archivo Program.cs de hello:

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
> En Ordenar toocomplete este tutorial, asegúrese de que agregar las dependencias de hello anteriores.

Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.

```csharp
class Program
{
    // ADD THIS PART tooYOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

A continuación, head toohello [Portal de Azure](https://portal.azure.com) tooretrieve el URI y la clave principal. Hello Azure Cosmos DB URI y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.

Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**.

Copiar Hola URI desde el portal de Hola y pegarlos en `<your endpoint URI>` en el archivo program.cs de Hola. A continuación, copia Hola clave principal del portal de Hola y péguelo en `<your key>`. Si usas hello Azure Cosmos DB emulador, utilice `https://localhost:8081` como punto de conexión de Hola y clave de autorización bien definido de Hola de [cómo usar toodevelop Hola emulador de base de datos de Azure Cosmos](local-emulator.md). Realizar seguro hello tooremove < y >, pero deje Hola comillas dobles en el punto de conexión y la clave.

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de C#. Muestra una base de datos de Azure Cosmos cuenta, con centro activo Hola resaltado, Hola resaltado en la hoja de cuenta de base de datos de Azure Cosmos Hola de botón de claves y valores URI, la clave principal y la clave secundaria de hello resaltan en hello hoja de claves][keys]

Comenzaremos Hola obtener iniciada aplicación mediante la creación de una nueva instancia de hello **DocumentClient**.

A continuación hello **Main** método, agregar esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia de nuestro nuevo **DocumentClient**.

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

Agregar código de hello siguiente toorun su tarea asincrónica de la **Main** método. Hola **Main** método detectará las excepciones y escribirlos toohello consola.

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

Hola presione **DocumentDBGettingStarted** botón toobuild y ejecute la aplicación hello.

¡Enhorabuena! Se ha conectado correctamente la cuenta de base de datos de Azure Cosmos tooan, ahora Echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.  

## <a name="step-4-create-a-database"></a>Paso 4: Creación de una base de datos
Antes de agregar código de hello para la creación de una base de datos, agregue un método auxiliar para escribir toohello consola.

Copie y pegue hello **WriteToConsoleAndPromptToContinue** method hello **GetStartedDemo** método.

```csharp
// ADD THIS PART tooYOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key toocontinue ...");
        Console.ReadKey();
}
```

La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método de hello **DocumentClient** clase. Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de cliente de Hola. Así se creará una base de datos denominada *FamilyDB*.

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha creado correctamente una base de datos de Azure Cosmos DB.  

## <a id="CreateColl"></a>Paso 5: Creación de una colección
> [!WARNING]
> **CreateDocumentCollectionAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios. Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).

A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método de hello **DocumentClient** clase. Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de la base de datos de Hola. Esto creará una colección de documentos denominada *FamilyCollection_oa*.

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART tooYOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha creado correctamente una colección de documentos de Azure Cosmos DB.  

## <a id="CreateDoc"></a>Paso 6: Creación de documentos JSON
A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase. Los documentos son contenido JSON definido por el usuario (arbitrario). Ahora podemos insertar uno o varios documentos. Si ya tiene datos que le gustaría toostore en la base de datos, puede usar Azure Cosmos DB [herramienta de migración de datos](import-data.md).

En primer lugar, necesitamos toocreate una **familia** clases que representan objetos almacenados en la base de datos de Azure Cosmos en este ejemplo. También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**. Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON. Crear estas clases mediante la adición de hello siguientes subclases internos después de hello **GetStartedDemo** método.

Copie y pegue hello **familia**, **primario**, **secundarios**, **mascota**, y **dirección** clases debajo Hola **WriteToConsoleAndPromptToContinue** método.

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

Copie y pegue hello **CreateFamilyDocumentIfNotExists** método debajo de su **CreateDocumentCollectionIfNotExists** método.

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

E insertar otros dos documentos, uno para hello Andersen familia y hello Wakefield familia.

Copie y pegue el código de hello que sigue a `// ADD THIS PART tooYOUR CODE` tooyour **GetStartedDemo** método debajo de creación de colección de documentos de Hola.

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

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha creado correctamente dos documentos de Azure Cosmos DB.  

![Diagrama que ilustra relación jerárquica Hola entre la cuenta de hello, base de datos en línea hello, colección de Hola y documentos de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB
Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.  Hello código de ejemplo siguiente muestra varias consultas: usar ambos SQL de base de datos de Azure Cosmos sintaxis, así como LINQ - que podemos ejecutar contra Hola se insertan en el paso anterior de hello documentos.

Copie y pegue hello **ExecuteSimpleQuery** método debajo de su **CreateFamilyDocumentIfNotExists** método.

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

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de creación de documentos de segundo de Hola.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART tooYOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha consultado correctamente una colección de Azure Cosmos DB.

Hello siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado y hello misma lógica aplica también la consulta LINQ de toohello.

![Diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección. Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija. Documentos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.

## <a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON
Azure Cosmos DB admite la sustitución de documentos JSON.  

Copie y pegue hello **ReplaceFamilyDocument** método debajo de su **ExecuteSimpleQuery** método.

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

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de la ejecución de la consulta de Hola. Después de reemplazar el documento de hello, ejecutará Hola mismo volver a consultar tooview Hola cambiado documento.

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooYOUR CODE
// Update hello Grade of hello Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha sustituido correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON
Azure Cosmos DB admite la eliminación de documentos JSON.  

Copie y pegue hello **DeleteFamilyDocument** método debajo de su **ReplaceFamilyDocument** método.

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

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método debajo de la segunda ejecución de la consulta de Hola.

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART tooCODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha eliminado correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola
Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** method documento Hola Eliminar base de datos completa de toodelete hello y todos los recursos de los elementos secundarios.

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART tooCODE
// Clean up/delete hello database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

Hola presione **DocumentDBGettingStarted** botón toorun la aplicación.

¡Enhorabuena! Ha eliminado correctamente una base de datos de Azure Cosmos DB.

## <a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#
Hola presione **DocumentDBGettingStarted** botón de aplicación de Visual Studio toobuild hello en modo de depuración.

Debería ver la salida de hello de la aplicación iniciada get en la ventana de la consola de Hola. salida de Hello mostrará resultados Hola de hello las consultas se agregan y se debe coincidir con el texto de ejemplo de Hola a continuación.

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

¡Enhorabuena! Ha completado el tutorial de Hola y tiene una aplicación de consola de C# de trabajo.

## <a id="GetSolution"></a>Obtener la solución del tutorial completo Hola
solución GetStarted de hello toobuild que contiene todos los ejemplos de hello en este artículo, se necesita Hola siguiente:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).
* Una [cuenta de Azure Cosmos DB][create-documentdb-dotnet.md#create-account].
* Hola [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solución disponible en GitHub.

toorestore Hola referencias toohello API de documentos Azure Cosmos DB SDK para .NET Core en Visual Studio, haga clic en hello **GetStarted** solución en el Explorador de soluciones y, a continuación, haga clic en **habilitar Restaurar el paquete NuGet**. A continuación, en el archivo Program.cs de hello, actualizar valores de hello EndpointUrl y AuthorizationKey tal y como se describe en [conectar la cuenta de base de datos de Azure Cosmos tooan](#Connect).

## <a name="next-steps"></a>Pasos siguientes
* ¿Desea un tutorial de ASP.NET MVC más complejo? Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).
* ¿Desea toodevelop una Xamarin iOS, Android o formularios utilizando la aplicación Hola API de documentos Azure Cosmos DB SDK para .NET Core? Consulte [Creación de aplicaciones móviles con Xamarin y Azure Cosmos DB](mobile-apps-with-xamarin.md).
* ¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos? Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).
* Obtenga información acerca de cómo demasiado[solicitudes, uso y almacenamiento de base de datos de Monitor Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn más información acerca del modelo de programación de hello, consulte [base de datos de Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

[create-documentdb-dotnet.md#create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png
