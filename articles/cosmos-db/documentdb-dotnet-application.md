---
title: 'Tutorial de ASP.NET MVC para Azure Cosmos DB: desarrollo de aplicaciones web | Microsoft Docs'
description: "ASP.NET MVC tutorial toocreate una aplicación web MVC con base de datos de Azure Cosmos. Almacenará el código JSON y accederá a los datos desde una aplicación ToDo hospedada en Sitios web de Azure. Tutorial de ASP NET MVC paso a paso."
keywords: "tutorial de asp.net mvc, desarrollo de aplicaciones web, aplicación web de mvc, tutorial de asp net mvc paso a paso"
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: mimig
ms.openlocfilehash: dac2a9599b395524533e6fe14983789ff095331f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395809351"></a>Tutorial de ASP.NET MVC: desarrollo de aplicaciones web con Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

toohighlight cómo puede aprovechar la base de datos de Azure Cosmos toostore y consultar documentos JSON eficazmente, este artículo proporciona un ejemplo paso a paso to-end que se muestra cómo una aplicación de lista de tareas con la base de datos de Azure Cosmos toobuild. tareas de Hola se almacenará como documentos JSON en la base de datos de Azure Cosmos.

![Captura de pantalla de lista de tareas de hello aplicación web MVC creado por este tutorial: tutorial paso a paso de ASP NET MVC](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-image01.png)

Este tutorial muestra cómo toouse Hola base de datos de Azure Cosmos servicio toostore y acceso a los datos desde una aplicación web de MVC de ASP.NET hospedado en Azure. Si desea obtener un tutorial que se centra en la base de datos de Azure Cosmos y no hello componentes de MVC de ASP.NET, vea [compilar una aplicación de consola de C# de Azure Cosmos DB](documentdb-get-started.md).

> [!TIP]
> En este tutorial se supone que tiene experiencia previa con ASP.NET MVC y Sitios web Azure. Si es nuevo tooASP.NET o hello [herramientas requisitos previos](#_Toc395637760), le recomendamos que descargue el proyecto de ejemplo completo de Hola de [GitHub] [ GitHub] y siga las instrucciones de hello en en este ejemplo. Una vez que se generan, puede revisar esta información de toogain de artículo en el código de hello en contexto de Hola de proyecto de Hola.
> 
> 

## <a name="_Toc395637760"></a>Requisitos previos del tutorial de base de datos
Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene Hola siguientes:

* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/). 

    OR

    Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).
* [Visual Studio 2017](http://www.visualstudio.com/).  
* Microsoft Azure SDK para .NET de Visual Studio de 2017 disponible a través de hello instalador de Visual Studio.

Se han realizado todas las capturas de pantalla de hello en este artículo mediante Microsoft Visual Studio Comunidad 2017. Si el sistema está configurado con una versión diferente, es posible que los filtros y opciones no coincidirán completamente, pero si Hola por encima de los requisitos previos se cumplen esta solución debería funcionar.

## <a name="_Toc395637761"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB
Para comenzar, creemos una cuenta de Azure Cosmos DB. Si ya tiene una cuenta SQL (documentos) de la base de datos de Azure Cosmos o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[crear una nueva aplicación MVC de ASP.NET](#_Toc395637762).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
Se le indicará cómo toocreate una nueva aplicación de MVC de ASP.NET de hello principio a fin. 

## <a name="_Toc395637762"></a>Paso 2: Creación de una aplicación ASP.NET MVC nueva

1. En Visual Studio, en hello **archivo** menú, seleccione demasiado**New**y, a continuación, haga clic en **proyecto**. Hola **nuevo proyecto** aparece el cuadro de diálogo.

2. Hola **tipos de proyecto** panel, expanda **plantillas**, **Visual C#**, **Web**y, a continuación, seleccione **aplicación Web ASP.NET** .

      ![Captura de pantalla del cuadro de diálogo nuevo proyecto de hello con el tipo de proyecto de aplicación Web ASP.NET de hello resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. Hola **nombre** cuadro, escriba un nombre hello del proyecto de Hola. Este tutorial usa Hola nombre "todo". Si elige un valor distinto de esto toouse, siempre que este tutorial se habla de espacio de nombres de tareas de hello, deberá toouse de ejemplos de código de hello proporciona tooadjust lo que se denomina la aplicación. 
4. Haga clic en **examinar** toonavigate toohello carpeta donde como proyecto de hello toocreate y, a continuación, haga clic en **Aceptar**.
   
      Hola **nueva aplicación Web ASP.NET** aparece el cuadro de diálogo.
   
    ![Captura de pantalla del cuadro de diálogo nueva aplicación Web ASP.NET de Hola a plantilla de aplicación de MVC Hola resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. En el panel de plantillas de hello, seleccione **MVC**.

6. Haga clic en **Aceptar** y dejar que Visual Studio lo alrededor de la plantilla vacía de ASP.NET MVC de scaffolding Hola. 

          
7. Una vez que Visual Studio ha terminado de crear la aplicación de MVC reutilizable de hello tiene una aplicación de ASP.NET vacía que se puede ejecutar localmente.
   
    Se podrá omitir ejecución proyecto Hola localmente porque estoy seguro de que hemos Hola visto todos los ASP.NET "¡Hello World" aplicación. Vamos a tooadding recta base de datos de Azure Cosmos toothis proyecto y compilar la aplicación.

## <a name="_Toc395637767"></a>Paso 3: Agregar proyecto de aplicación web de base de datos de Azure Cosmos tooyour MVC
Ahora que tenemos la mayoría de establecimiento de ASP.NET MVC Hola que necesitamos para esta solución, vamos a obtener toohello real propósito de este tutorial, para agregar la aplicación web de base de datos de Azure Cosmos tooour MVC.

1. Hello Azure Cosmos DB .NET SDK se empaqueta y distribuye como un paquete de NuGet. tooget Hola paquete de NuGet en Visual Studio, use el Administrador de paquetes de NuGet hello en Visual Studio con el botón secundario en el proyecto de hello en **el Explorador de soluciones** y, a continuación, haga clic en **administrar paquetes de NuGet**.
   
    ![Captura de pantalla de hello haga clic en Opciones de proyecto de aplicación web de hello en el Explorador de soluciones, con administrar paquetes de NuGet resaltado.](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    Hola **administrar paquetes de NuGet** aparece el cuadro de diálogo.
2. Hola NuGet **examinar** , escriba ***Azure DocumentDB***. (nombre del paquete hello no ha sido actualizada tooAzure Cosmos DB.)
   
    Desde los resultados de hello, instalar hello **Microsoft.Azure.DocumentDB Microsoft** paquete. Esto descargará e instalará el paquete de la base de datos de Azure Cosmos de hello, así como todas las dependencias, como Newtonsoft.Json. Haga clic en **Aceptar** en hello **vista previa** ventana, y **acepto** en hello **la aceptación de licencia** ventana toocomplete Hola install.
   
    ![Captura de pantalla de la ventana Administrar paquetes de NuGet de hello, con hello resaltado de la biblioteca del cliente de documentos de Microsoft Azure](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      O bien puede usar Hola paquete de hello tooinstall Package Manager Console. toodo así, sucesivamente hello **herramientas** menú, haga clic en **Administrador de paquetes de NuGet**y, a continuación, haga clic en **Package Manager Console**. En el símbolo del sistema de hello, escriba Hola siguiente.
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. Una vez instalado el paquete de hello, la solución de Visual Studio debe parecerse al siguiente de hello con dos nuevas referencias de agregado, Microsoft.Azure.Documents.Client y Newtonsoft.Json.
   
    ![Captura de pantalla de dos referencias de hello agrega proyecto de datos JSON de toohello en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a>Paso 4: Configurar Hola aplicación ASP.NET MVC
Ahora vamos a Agregar aplicación de MVC de toothis de modelos, vistas y controladores de hello:

* [Adición de un modelo](#_Toc395637764).
* [Adición de un controlador](#_Toc395637765).
* [Adición de vistas](#_Toc395637766).

### <a name="_Toc395637764"></a>Adición de un modelo de datos JSON
Empecemos creando hello **M** en MVC, Hola modelo. 

1. En **el Explorador de soluciones**, contextual hello **modelos** carpeta, haga clic en **agregar**y, a continuación, haga clic en **clase**.
   
      Hola **Agregar nuevo elemento** aparece el cuadro de diálogo.
2. Ponga a la nueva clase el nombre **Item.cs** y haga clic en **Agregar**. 
3. En este nuevo **Item.cs** , agregue el siguiente Hola después Hola última *mediante la instrucción*.
   
        using Newtonsoft.Json;
4. Ahora, reemplace este código 
   
        public class Item
        {
        }
   
    con hello al siguiente código.
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    Todos los datos de la base de datos de Azure Cosmos se pasan a través de conexión de Hola y almacenar como JSON. manera de Hola de toocontrol los objetos se serializan/deserializar JSON.NET puede usar hello **JsonProperty** atributo como se muestra en hello **elemento** clase que acabamos de crear. No se cuentan **tienen** toodo esto pero desea tooensure que mi propiedades sigan convenciones de nomenclatura de hello JSON camelCase. 
   
    No solo puede controlar formato Hola Hola del nombre de propiedad cuando entra en JSON, pero puede cambiar completamente las propiedades de .NET como hizo con hello **descripción** propiedad. 

### <a name="_Toc395637765"></a>Adición de un controlador
Que se encarga de hello **M**, ahora vamos a crear hello **C** en MVC, una clase de controlador.

1. En **el Explorador de soluciones**, contextual hello **controladores** carpeta, haga clic en **agregar**y, a continuación, haga clic en **controlador**.
   
    Hola **agregar scaffolding** aparece el cuadro de diálogo.
2. Seleccione **Controlador MVC 5 - Vacío** y, a continuación, haga clic en **Agregar**.
   
    ![Captura de pantalla del cuadro de diálogo Agregar scaffolding Hola con hello controlador de MVC 5 - opción vacía resaltada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. Asigne un nombre al nuevo controlador, **ItemController.**
   
    ![Captura de pantalla del cuadro de diálogo Agregar controlador Hola](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    Una vez que se crea el archivo hello, debe ser similar a la solución de Visual Studio siguiente Hola con nuevo archivo de ItemController.cs hello en **el Explorador de soluciones**. También se muestra el nuevo archivo de Item.cs Hola creado anteriormente.
   
    ![Captura de pantalla de hello solución de Visual Studio - Explorador de soluciones con el archivo ItemController.cs nuevo de Hola y Item.cs resaltado](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    Puede cerrar ItemController.cs, volveremos tooit más tarde. 

### <a name="_Toc395637766"></a>Adición de vistas
Ahora, vamos a crear hello **V** en MVC, Hola vistas:

* [Adición de una vista de índice de elementos](#AddItemIndexView).
* [Adición de una vista de elementos nuevos](#AddNewIndexView).
* [Adición de una vista de edición de elementos](#_Toc395888515).

#### <a name="AddItemIndexView"></a>Adición de una vista de índice de elementos
1. En **el Explorador de soluciones**, expanda hello **vistas** carpeta, contextual Hola vacía **elemento** carpeta que Visual Studio crea automáticamente cuando se agrega hello  **ItemController** anterior, haga clic en **agregar**y, a continuación, haga clic en **vista**.
   
    ![Captura de pantalla del explorador de soluciones con la carpeta de elementos de hello creados por Visual Studio con comandos de agregar vista Hola resaltados](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. Hola **agregar vista** diálogo cuadro, Hola siguientes:
   
   * Hola **nombre de la vista** , escriba ***índice***.
   * Hola **plantilla** cuadro, seleccione ***lista***.
   * Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.
   * En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.
     
   ![Cuadro de diálogo Agregar vista de captura de pantalla que muestra hello](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. Después de que se hayan establecido todos estos valores, haga clic en **Agregar** y permita que Visual Studio cree una nueva vista de plantilla. Una vez que se hace esto, se abrirá el archivo cshtml hello que se creó. Podemos cerrar ese archivo en Visual Studio como se volverá tooit más tarde.

#### <a name="AddNewIndexView"></a>Adición de una vista de elementos nuevos
Toohow similar que hemos creado un **índice del elemento** vista, ahora crearemos una nueva vista para crear nuevas **elementos**.

1. En **el Explorador de soluciones**, contextual hello **elemento** de nuevo, haga clic en la carpeta **agregar**y, a continuación, haga clic en **vista**.
2. Hola **agregar vista** diálogo cuadro, Hola siguientes:
   
   * Hola **nombre de la vista** , escriba ***crear***.
   * Hola **plantilla** cuadro, seleccione ***crear***.
   * Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.
   * En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.
   * Haga clic en **Agregar**.
   
#### <a name="_Toc395888515"></a>Adición de una vista de edición de elementos
Por último, agregue una última vista para editar un **elemento** Hola igual que antes.

1. En **el Explorador de soluciones**, contextual hello **elemento** de nuevo, haga clic en la carpeta **agregar**y, a continuación, haga clic en **vista**.
2. Hola **agregar vista** diálogo cuadro, Hola siguientes:
   
   * Hola **nombre de la vista** , escriba ***editar***.
   * Hola **plantilla** cuadro, seleccione ***editar***.
   * Hola **clase modelo** cuadro, seleccione ***elemento (lista de tareas. Modelos)***.
   * En el cuadro de página de diseño de hello, escriba ***~/Views/Shared/_Layout.cshtml***.
   * Haga clic en **Agregar**.

Una vez hecho esto, cierre todos los documentos de cshtml de hello en Visual Studio como se devolverán vistas toothese más tarde.

## <a name="_Toc395637769"></a>Paso 5: Conexión de Azure Cosmos DB
Ahora que se prepara material MVC estándar hello, vamos a activar el código de hello tooadding para la base de datos de Azure Cosmos. 

En esta sección, se agregará código que sigue Hola toohandle:

* [Lista de elementos incompletos](#_Toc395637770).
* [Adición de elementos](#_Toc395637771).
* [Edición de elementos](#_Toc395637772).

### <a name="_Toc395637770"></a>Lista de elementos incompletos en la aplicación web MVC
Hello primer toodo de lo aquí es agregar una clase que contiene todos los tooconnect tooand usar base de datos de Azure Cosmos lógica de Hola. En este tutorial se a encapsular toda esta lógica en la clase de repositorio de tooa denominada DocumentDBRepository. 

1. En **el Explorador de soluciones**, haga doble clic en el proyecto de hello, haga clic en **agregar**y, a continuación, haga clic en **clase**. Hola nueva clase el nombre **DocumentDBRepository** y haga clic en **agregar**.
2. Hola recién creado **DocumentDBRepository** clase y agregue Hola siguiente *mediante instrucciones* anteriormente hello *espacio de nombres* declaración
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net
        
    Ahora, reemplace este código 
   
        public class DocumentDBRepository
        {
        }
   
    con hello al siguiente código.
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
    
3. Le estamos leer algunos valores de configuración, abra hello **Web.config** archivo de la aplicación y agregue Hola después de líneas que aparecen bajo hello `<AppSettings>` sección.
   
        <add key="endpoint" value="enter hello URI from hello Keys blade of hello Azure Portal"/>
        <add key="authKey" value="enter hello PRIMARY KEY, or hello SECONDARY KEY, from hello Keys blade of hello Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. Ahora, actualice los valores de hello de *extremo* y *SFF* mediante la hoja de claves de Hola de hello Portal de Azure. Usar hello **URI** de hoja de claves de hello como valor de Hola de configuración de punto de conexión de Hola y Hola de uso **PRIMARY KEY**, o **clave secundaria** de hoja de claves de hello como valor de Hola Hola configuración de SFF.

    Que se encarga de cableado de repositorio de base de datos de Azure Cosmos hello, ahora vamos a agrega la lógica de la aplicación.

1. Hello lo primero que queremos toobe puede toodo con una aplicación de lista de tareas es elementos incompleta de toodisplay Hola.  Copie y pegue Hola siguiente fragmento de código en cualquier lugar de hello **DocumentDBRepository** clase.
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. Abra hello **ItemController** se agregó anteriormente y agregue los siguientes hello *mediante instrucciones* por encima de la declaración de espacio de nombres de Hola.
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    Si el proyecto no se denomina "todo", a continuación, necesita tooupdate con "lista de tareas. Modelos"; nombre de hello tooreflect del proyecto.
   
    Ahora, reemplace este código
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    con hello al siguiente código.
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. Abra **Global.asax.cs** y agregue Hola después línea toohello **Application_Start** (método) 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

En este momento la solución debe ser capaz de toobuild sin errores.

Si ha ejecutado ahora la aplicación hello, quedarían toohello **HomeController** hello y **índice** vista de ese controlador. Se trata de comportamiento predeterminado de Hola para proyecto de plantilla MVC Hola que elegimos al principio de hello pero no queremos! Vamos a cambiar Hola enrutamiento en este tooalter de aplicación de MVC este comportamiento.

Abra ***aplicación\_Start\RouteConfig.cs*** y busque la línea hello a partir de "valores predeterminados:" y cámbielo hello tooresemble después.

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

Ahora Esto indica a ASP.NET MVC que si no ha especificado un valor en toocontrol de dirección URL de Hola Hola comportamiento de enrutamiento que, en lugar de **inicio**, use **elemento** como controlador de Hola y usuario **índice** como vista de Hola.

Ahora si ejecuta la aplicación hello, llamará a su **ItemController** que se llame en clase de repositorio toohello y use Hola GetItems método tooreturn todos Hola elementos incompletos toohello **vistas** \\ **Elemento**\\**índice** vista. 

Si crea y ejecuta este proyecto ahora, deberá ver algo parecido a esto.    

![Captura de pantalla de creados por este tutorial de base de datos de aplicación del web de lista de tareas Hola](./media/documentdb-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a>Adición de elementos
Pongamos algunos elementos en nuestra base de datos, así tendremos algo más que un toolook cuadrícula vacía en.

Agreguemos algún código de registro de hello toopersist Azure Cosmos DBRepository y ItemController en la base de datos de Azure Cosmos.

1. Agregar Hola siguiendo el método tooyour **DocumentDBRepository** clase.
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   Este método simplemente toma un objeto pasado tooit y lo almacena en la base de datos de Azure Cosmos.
2. Abra el archivo de ItemController.cs hello y agregue Hola siguiente fragmento de código dentro de la clase hello. Se trata cómo ASP.NET MVC sabe qué toodo para hello **crear** acción. En este caso simplemente representación Hola asociado vista Create.cshtml que creó anteriormente.
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    Ahora necesitamos algunos más código de este controlador que acepte el envío de Hola Hola **crear** vista.
3. Agregar Hola siguiente bloque de código toohello clase ItemController.cs que indica qué toodo con un formulario POST para este controlador de MVC de ASP.NET.
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    Este código llama en toohello DocumentDBRepository y utiliza hello CreateItemAsync método toopersist Hola todo elemento toohello base de datos nueva. 
   
    **Nota de seguridad**: Hola **ValidateAntiForgeryToken** atributo se utiliza aquí toohelp proteger esta aplicación frente a ataques de falsificación de solicitud entre sitios. Hay más tooit que limitarse a agregar este atributo, las vistas necesitan toowork con este token antifalsificación así. Para obtener más información sobre el sujeto de Hola y ejemplos de cómo tooimplement esto correctamente, vea [evitar falsificación de solicitud entre sitios][Preventing Cross-Site Request Forgery]. Hola código fuente ofrecido en [GitHub] [ GitHub] tiene implementación completa de hello en su lugar.
   
    **Nota de seguridad**: También utilizamos hello **enlazar** atributo toohelp de parámetro de método hello protegerse exceso contabilización ataques. Para más información, consulte el artículo sobre [operaciones CRUD básicas en ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].

Esto concluye Hola código necesario tooadd nueva elementos tooour base de datos.

### <a name="_Toc395637772"></a>Edición de elementos
Hay una última cosa que nos toodo, y que es tooadd Hola capacidad tooedit **elementos** en la base de datos de Hola y toomark como completa. Hello vista de edición ya se ha agregado toohello proyecto, por lo que debemos tooadd algunos código controlador tooour y toohello **DocumentDBRepository** clase de nuevo.

1. Agregar Hola después toohello **DocumentDBRepository** clase.
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    Hola primero de estos métodos, **GetItem** captura un elemento de la base de datos de Cosmos de Azure que se pasa toohello Atrás **ItemController** y, a continuación, en toohello **editar** vista.
   
    Hola segundo de los métodos de Hola que acabamos de agregar reemplaza hello **documento** en la base de datos de Azure Cosmos con la versión de Hola de hello **documento** pasados desde hello **ItemController**.
2. Agregar Hola después toohello **ItemController** clase.
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    Hello primer método controla Hola Http GET que se produce cuando hace clic en usuario de hello en hello **editar** vínculo de hello **índice** vista. Este método captura un [ **documento** ](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) de base de datos de Azure Cosmos y pasa toohello **editar** vista.
   
    Hola **editar** vista, a continuación, realizará un Http POST toohello **IndexController**. 
   
    segundo método de Hello agregamos identificadores pasar Hola actualizar objeto tooAzure Cosmos DB toobe se conserva en la base de datos de Hola.

¡Eso es todo, que es todo lo necesario toorun nuestra aplicación, se muestran incompletos **elementos**, agregar nuevas **elementos**y editar **elementos**.

## <a name="_Toc395637773"></a>Paso 6: Ejecutar aplicación hello localmente
aplicación de hello tootest en el equipo local, Hola siguientes:

1. Presione F5 en la aplicación de Visual Studio toobuild hello en modo de depuración. Debe compilar la aplicación hello e iniciar un explorador con la página de cuadrícula vacía Hola que hemos visto antes:
   
    ![Captura de pantalla de creados por este tutorial de base de datos de aplicación del web de lista de tareas Hola](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. Haga clic en hello **crear nuevo** vincular y agregar valores toohello **nombre** y **descripción** campos. Deje hello **completado** casilla de verificación no está seleccionada en caso contrario Hola de nuevo **elemento** se agregarán en un estado completado y no aparecerán en la lista inicial de Hola.
   
    ![Captura de pantalla de hello Crear vista](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. Haga clic en **crear** y es redirigido toohello Atrás **índice** vista y su **elemento** aparece en la lista de Hola.
   
    ![Captura de pantalla de hello vista de índice](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    Sentirse tooadd libre más unos **elementos** tooyour lista de tareas.
    
4. Haga clic en **editar** tooan siguiente **elemento** en la lista de Hola y se toman toohello **editar** vista en la que puede actualizar cualquier propiedad de su objeto, incluidos hello  **Completado** marca. Si marca hello **completar** marca y haga clic en **guardar**, hello **elemento** se quita de la lista de Hola de tareas incompletas.
   
    ![Captura de pantalla de hello vista de índice con hello completado casilla activada](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. Una vez que ha probado la aplicación hello, presione toostop Ctrl + F5 para depurar aplicación Hola. Está listo toodeploy.

## <a name="_Toc395637774"></a>Paso 7: Implementar Hola aplicación tooAzure servicio de aplicaciones 
Ahora que tiene la aplicación completa de hello funciona correctamente con la base de datos de Azure Cosmos vamos toodeploy esta tooAzure de aplicación web servicio de aplicaciones.  

1. Esta aplicación todos los necesita toodo no toopublish es haga doble clic en el proyecto de hello en **el Explorador de soluciones** y haga clic en **publicar**.
   
    ![Captura de pantalla de hello opción Publicar en el Explorador de soluciones](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. Hola **publicar** cuadro de diálogo, haga clic en **servicio de aplicaciones de Microsoft Azure**, a continuación, seleccione **crear nuevo** toocreate un servicio de aplicaciones de perfil, o haga clic en **seleccionar Existente** toouse un perfil existente.

    ![Cuadro de diálogo Publicar en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. Si tiene un perfil de Azure App Service existente, escriba el nombre de la suscripción. Hola de uso **vista** filtrar toosort por tipo de recurso o grupo de recursos, a continuación, seleccione el servicio de aplicaciones de Azure. 
   
    ![Cuadro de diálogo App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. toocreate un nuevo perfil de servicio de aplicaciones de Azure, haga clic en **crear nuevo** en hello **publicar** cuadro de diálogo. Hola **crear servicio en la aplicación** cuadro de diálogo, escriba el nombre de la aplicación Web y la suscripción adecuada, el grupo de recursos y el plan de servicio de aplicaciones, a continuación, haga clic en **crear**.

    ![Cuadro de diálogo Crear App Service en Visual Studio](./media/documentdb-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

En pocos segundos, Visual Studio terminará de publicar la aplicación web y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.



## <a name="_Toc395637775"></a>Pasos siguientes
¡Enhorabuena! Simplemente había creado su primer ASP.NET MVC de aplicación web mediante la base de datos de Azure Cosmos y haberlo publicado tooAzure. Hola código fuente de la aplicación completa de hello, incluidos los detalles de Hola y eliminar funciones que no se incluyeron en este tutorial se puede descargar o clonado a partir de [GitHub][GitHub]. Por lo que si está interesado en Agregar aplicación tooyour, agarre el código de hello y Agregar aplicación toothis.

aplicación de tooyour tooadd funcionalidad adicional, revisión Hola API disponibles en hello [biblioteca de .NET de base de datos de Azure Cosmos](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) y Siéntase libre toocontribute toohello Azure Cosmos DB .NET Library en [GitHub] [GitHub]. 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
