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
# <a name="azure-cosmos-db-documentdb-api-getting-started-tutorial"></a>Azure Cosmos DB: tutorial de introducción a las API de DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bienvenida toohello API de documentos de base de datos de Azure Cosmos tutorial de introducción. Después de seguir este tutorial, tendrá una aplicación de consola que crea recursos de Azure Cosmos DB y los consulta.

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

¿No tiene tiempo? ¡No se preocupe! está disponible en la solución completa de Hello [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). Saltar toohello [Obtenga una sección de solución del tutorial de NoSQL completa hello](#GetSolution) para obtener instrucciones rápidas.

Después, por favor, use Hola botones de voto en hello superior o inferior de esta página toogive nos comentarios. Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.

Comencemos.

## <a name="prerequisites"></a>Requisitos previos
Asegúrese de que tiene Hola siguientes:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, puede usar hello [emulador de base de datos de Azure Cosmos](local-emulator.md) para este tutorial.
* [Visual Studio Community 2017](http://www.visualstudio.com/).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Paso 1: Creación de una cuenta de Azure Cosmos DB
Vamos a crear una cuenta de Azure Cosmos DB. Si ya tiene una cuenta que desee toouse, puede pasar demasiado[la instalación de la solución de Visual Studio](#SetupVS). Si usas hello Azure Cosmos DB emulador, siga los pasos de hello en [emulador de base de datos de Azure Cosmos](local-emulator.md) toosetup Hola emulador y pase demasiado[la instalación de la solución de Visual Studio](#SetupVS).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Paso 2: Configuración de la solución de Visual Studio
1. Abra **Visual Studio 2017** en el equipo.
2. En hello **archivo** menú, seleccione **New**y, a continuación, elija **proyecto**.
3. Hola **nuevo proyecto** cuadro de diálogo, seleccione **plantillas** / **Visual C#** / **aplicación de consola**, nombre el proyecto y, a continuación, haga clic en **Aceptar**.
   ![Captura de pantalla de ventana nuevo proyecto de hello](./media/documentdb-get-started/nosql-tutorial-new-project-2.png)
4. Hola **el Explorador de soluciones**, haga clic con el botón secundario en la nueva aplicación de consola, que se encuentra en la solución de Visual Studio, y, a continuación, haga clic en **administrar paquetes de NuGet...**
    
    ![Captura de pantalla de hello derecha menú Clicked Hola proyecto](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. Hola **Nuget** , haga clic en **examinar**y el tipo de **documentdb de azure** en el cuadro de búsqueda de Hola.
6. En los resultados de hello, buscar **Microsoft.Azure.DocumentDB** y haga clic en **instalar**.
   Id. de paquete de Hola para hello biblioteca cliente de API de documentos de base de datos de Azure Cosmos es [biblioteca de cliente de Microsoft Azure DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).
   ![Captura de pantalla de hello Nuget menú para buscar el SDK de cliente de base de datos de Azure Cosmos](./media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)

    Si aparece un mensaje acerca de la revisión de la solución de toohello de cambios, haga clic en **Aceptar**. Si recibe un mensaje acerca de la aceptación de licencia, haga clic en **Acepto**.

Estupendo. Ahora que hemos terminado el programa de instalación de hello, vamos a empezar a escribir código. Puede buscar un proyecto con código completo de este tutorial en [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).

## <a id="Connect"></a>Paso 3: Conectar la cuenta de base de datos de Azure Cosmos tooan
En primer lugar, agregue estas referencias toohello a partir de la aplicación de C#, en el archivo Program.cs de hello:

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART tooYOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> En el tutorial de orden toocomplete hello, asegúrese de que agregar dependencias de hello anteriores.
> 
> 

Ahora, agregue estas dos constantes y la variable *client* debajo de la clase pública *Program*.

    public class Program
    {
        // ADD THIS PART tooYOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

A continuación, hacer copia de head toohello [Portal de Azure](https://portal.azure.com) tooretrieve la dirección URL del extremo y la clave principal. dirección URL del extremo de Hola y clave principal son necesarios para su aplicación toounderstand donde tooconnect y para la base de datos de Azure Cosmos tootrust conexión de la aplicación.

Hola Portal de Azure, navegar por la cuenta de base de datos de Azure Cosmos tooyour y, a continuación, haga clic en **claves**.

Copiar Hola URI desde el portal de Hola y pegarlos en `<your endpoint URL>` en el archivo program.cs de Hola. A continuación, copia Hola clave principal del portal de Hola y péguelo en `<your primary key>`.

![Captura de pantalla de hello Portal de Azure usan Hola NoSQL tutorial toocreate una aplicación de consola de C#. Muestra una base de datos de Azure Cosmos cuenta, con centro activo Hola resaltado, Hola resaltado en la hoja de cuenta de base de datos de Azure Cosmos Hola de botón de claves y valores URI, la clave principal y la clave secundaria de hello resaltan en hello hoja de claves][keys]

A continuación, comenzaremos aplicación hello mediante la creación de una nueva instancia de hello **DocumentClient**.

A continuación hello **Main** método, agregar esta nueva tarea asincrónica denominada **GetStartedDemo**, que creará una instancia de nuestro nuevo **DocumentClient**.

    static void Main(string[] args)
    {
    }

    // ADD THIS PART tooYOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

Agregar código de hello siguiente toorun su tarea asincrónica de la **Main** método. Hola **Main** método detectará las excepciones y escribirlos toohello consola.

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

Presione **F5** toorun la aplicación. salida de la ventana Consola Hello muestra mensajes de bienvenida `End of demo, press any key tooexit.` confirmar que se ha realizado la conexión de Hola.  A continuación, puede cerrar la ventana de la consola de Hola. 

¡Enhorabuena! Se ha conectado correctamente la cuenta de base de datos de Azure Cosmos tooan, ahora Echemos un vistazo a trabajar con los recursos de base de datos de Azure Cosmos.  

## <a name="step-4-create-a-database"></a>Paso 4: Creación de una base de datos
Antes de agregar código de hello para la creación de una base de datos, agregue un método auxiliar para escribir toohello consola.

Copie y pegue hello **WriteToConsoleAndPromptToContinue** método después de hello **GetStartedDemo** método.

    // ADD THIS PART tooYOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key toocontinue ...");
            Console.ReadKey();
    }

La base de datos de Azure Cosmos [base de datos](documentdb-resources.md#databases) pueden crearse mediante el uso de hello [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método de hello **DocumentClient** clase. Una base de datos es el contenedor lógico de Hola de almacenamiento de documentos JSON particionado entre colecciones.

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de cliente de Hola. Así se creará una base de datos denominada *FamilyDB*.

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART tooYOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha creado correctamente una base de datos de Azure Cosmos DB.  

## <a id="CreateColl"></a>Paso 5: Creación de una colección
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** creará una nueva colección con un rendimiento reservado, lo que tiene implicaciones en los precios. Para obtener más información, visite nuestra [página de precios](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

A [colección](documentdb-resources.md#collections) pueden crearse mediante el uso de hello [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método de hello **DocumentClient** clase. Una colección es un contenedor de documentos JSON asociado a la lógica de aplicación de JavaScript.

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de la base de datos de Hola. Esto creará una colección de documentos llamada *FamilyCollection*.

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART tooYOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha creado correctamente una colección de documentos de Azure Cosmos DB.  

## <a id="CreateDoc"></a>Paso 6: Creación de documentos JSON
A [documento](documentdb-resources.md#documents) pueden crearse mediante el uso de hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) método de hello **DocumentClient** clase. Los documentos son contenido JSON definido por el usuario (arbitrario). Ahora podemos insertar uno o varios documentos. Si ya tiene datos que le gustaría toostore en la base de datos, puede usar base de datos de Azure Cosmos hello [herramienta de migración de datos](import-data.md) datos de hello tooimport en una base de datos.

En primer lugar, necesitamos toocreate una **familia** clases que representan objetos almacenados en la base de datos de Azure Cosmos en este ejemplo. También se crearán las subclases **Parent**, **Child**, **Pet**, **Address** que se usan dentro de **Family**. Tenga en cuenta que los documentos deben tener una propiedad **Id** serializada como **id** en JSON. Crear estas clases mediante la adición de hello siguientes subclases internos después de hello **GetStartedDemo** método.

Copie y pegue hello **familia**, **primario**, **secundarios**, **mascota**, y **dirección** clases después Hola **WriteToConsoleAndPromptToContinue** método.

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

Copie y pegue hello **CreateFamilyDocumentIfNotExists** método debajo de su **dirección** clase.

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

E insertar otros dos documentos, uno para hello Andersen familia y hello Wakefield familia.

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de colección de documentos de Hola.

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

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha creado correctamente dos documentos de Azure Cosmos DB.  

![Diagrama que ilustra relación jerárquica Hola entre la cuenta de hello, base de datos en línea hello, colección de Hola y documentos de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Paso 7: Consulta de los recursos de Azure Cosmos DB
Azure Cosmos DB admite [consultas](documentdb-sql-query.md) enriquecidas en los documentos JSON que se almacenan en las colecciones.  Hello código de ejemplo siguiente muestra varias consultas: usar ambos SQL de base de datos de Azure Cosmos sintaxis, así como LINQ - que podemos ejecutar contra Hola se insertan en el paso anterior de hello documentos.

Copie y pegue hello **ExecuteSimpleQuery** método después de su **CreateFamilyDocumentIfNotExists** método.

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

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la creación de hello segundo documento.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART tooYOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha consultado correctamente una colección de Azure Cosmos DB.

Hello siguiente diagrama ilustra cómo consulta de base de datos SQL de Azure Cosmos Hola sintaxis se llama en la colección de Hola que ha creado y hello misma lógica aplica también la consulta LINQ de toohello.

![Diagrama que ilustra el ámbito de Hola y lo que significa de consulta de hello usa Hola NoSQL tutorial toocreate una aplicación de consola de C#](./media/documentdb-get-started/nosql-tutorial-collection-documents.png)

Hola [FROM](documentdb-sql-query.md#FromClause) palabra clave es opcional en la consulta de hello porque las consultas de base de datos de Azure Cosmos ya están tooa ámbito sola colección. Por lo tanto, «FROM Families f" se puede intercambiar por  "FROM root r", o cualquier otra variable de nombre que elija. Base de datos de Azure Cosmos deducirá que familias, raíz o nombre de variable de hello eligió, referencia Hola colección actual de forma predeterminada.

## <a id="ReplaceDocument"></a>Paso 8: Reemplazar un documento JSON
Azure Cosmos DB admite la sustitución de documentos JSON.  

Copie y pegue hello **ReplaceFamilyDocument** método después de su **ExecuteSimpleQuery** método.

    // ADD THIS PART tooYOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la ejecución de consulta de hello, al final de hello del método hello. Después de reemplazar el documento de hello, ejecutará Hola mismo volver a consultar tooview Hola cambiado documento.

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART tooYOUR CODE
    // Update hello Grade of hello Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha sustituido correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDocument"></a>Paso 9: Eliminar documento JSON
Azure Cosmos DB admite la eliminación de documentos JSON.  

Copie y pegue hello **DeleteFamilyDocument** método después de su **ReplaceFamilyDocument** método.

    // ADD THIS PART tooYOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después de la ejecución de consulta segundo hello, al final de hello del método hello.

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART tooCODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha eliminado correctamente un documento de Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Paso 10: Eliminar base de datos de Hola
Eliminando Hola creada la base de datos quitará la base de datos de Hola y todos los recursos de los elementos secundarios (colecciones, documentos, etcetera).

Copiar y pegar siguiente de hello código tooyour **GetStartedDemo** método después documento Hola Eliminar base de datos completa de toodelete hello y todos los recursos de los elementos secundarios.

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART tooCODE
    // Clean up/delete hello database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

Presione **F5** toorun la aplicación.

¡Enhorabuena! Ha eliminado correctamente una base de datos de Azure Cosmos DB.

## <a id="Run"></a>Paso 11: Ejecutar la aplicación de consola de C#
Presione F5 en la aplicación de Visual Studio toobuild hello en modo de depuración.

Debería ver la salida de hello de la aplicación iniciada get en una ventana de consola. salida de Hello mostrará resultados Hola de hello las consultas se agregan y se debe coincidir con el texto de ejemplo de Hola a continuación.

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

¡Enhorabuena! Ha completado el tutorial de Hola y tiene una aplicación de consola de C# de trabajo.

## <a id="GetSolution"></a>Obtener la solución del tutorial completo Hola
Si no dispone de tiempo hello toocomplete los pasos de este tutorial o ejemplos de código desea toodownload Hola simplemente, puede obtenerlo de [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started). 

solución de GetStarted de toobuild hello, necesitará siguiente hello:

* Una cuenta de Azure activa. Si no tiene una, puede registrarse para obtener una [cuenta gratuita](https://azure.microsoft.com/free/).
* Una [cuenta de Azure Cosmos DB][cosmos-db-create-account].
* Hola [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solución disponible en GitHub.

toorestore Hola referencias toohello Cosmos DB .NET SDK de Azure en Visual Studio, haga clic en hello **GetStarted** solución en el Explorador de soluciones y, a continuación, haga clic en **habilite la restauración del paquete NuGet**. A continuación, en el archivo App.config de hello, actualizar valores de hello EndpointUrl y AuthorizationKey tal y como se describe en [conectar la cuenta de base de datos de Azure Cosmos tooan](#Connect).

Y, eso es todo, genérela y habrá terminado.


## <a name="next-steps"></a>Pasos siguientes
* ¿Desea un tutorial de ASP.NET MVC más complejo? Consulte el [Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB](documentdb-dotnet-application.md).
* ¿Desea tooperform escala y rendimiento de pruebas con la base de datos de Azure Cosmos? Consulte [Pruebas de escala y rendimiento con Azure Cosmos DB](performance-testing.md).
* Obtenga información acerca de cómo demasiado[supervisar las solicitudes, uso y almacenamiento de base de datos de Azure Cosmos](monitor-accounts.md).
* Ejecutar consultas en el conjunto de datos de ejemplo de Hola [Query Playground](https://www.documentdb.com/sql/demo).
* toolearn más información acerca de la base de datos de Cosmos de Azure, consulte [Bienvenido tooAzure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-documentdb-dotnet.md#create-account
