---
title: "aaaCreate una aplicación web en Azure que se conecta tooMongoDB que se ejecuta en una máquina virtual"
description: "Un tutorial que le enseña cómo toouse Git toodeploy una tooAzure de aplicación ASP.NET, servicio de aplicaciones de conectado tooMongoDB en una máquina Virtual de Azure."
tags: azure-portal
services: app-service\web, virtual-machines
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: adf7a472-ae00-45a8-aec4-06247e21318b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: cephalin
ms.openlocfilehash: 1f5f42c28c3c294d92c9ebf1499374931d47c010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a>Crear una aplicación web de Azure que se conecta tooMongoDB que se ejecuta en una máquina virtual
Con Git, puede implementar un tooAzure de aplicación aplicación del servicio de aplicaciones Web ASP.NET. En este tutorial, compilará un front-end MVC de ASP.NET simple aplicación de lista de tareas que se conecta la base de datos de MongoDB de tooa ejecuta en una máquina virtual en Azure.  [MongoDB][MongoDB] es una conocida base de datos NoSQL de código abierto y alto rendimiento. Después de ejecutar y probar la aplicación de ASP.NET de hello en el equipo de desarrollo, se cargará hello tooApp de aplicación Web del servicio de aplicaciones mediante Git.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="background-knowledge"></a>Conocimientos previos
El conocimiento de la siguiente hello es útil para este tutorial, aunque no es necesario:

* controlador de Hello C# para MongoDB. Para obtener más información sobre cómo desarrollar aplicaciones de C# con MongoDB, vea Hola MongoDB [Center de lenguaje CSharp][MongoC#LangCenter]. 
* marco de aplicación web de Hello ASP. NET. Puede obtener información sobre esto en hello [sitio Web de ASP.net][ASP.NET].
* marco de aplicación de web de ASP .NET MVC Hola. Puede obtener información sobre esto en hello [sitio Web de ASP.NET MVC][MVCWebSite].
* Azure. Puede comenzar leyendo [Azure][WindowsAzure].

## <a name="prerequisites"></a>Requisitos previos
* [Visual Studio Express 2013 para Web][VSEWeb] o [Visual Studio 2013][VSUlt]
* [SDK de Azure para .NET](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* Una suscripción de Microsoft Azure activa

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a>Creación de una máquina virtual e instalación de MongoDB
En este tutorial se presupone que ha creado una máquina virtual en Azure. Después de crear la máquina virtual de hello necesita tooinstall MongoDB en la máquina virtual de hello:

* toocreate una máquina virtual de Windows e instale MongoDB, consulte [MongoDB instalar en una máquina virtual que ejecute Windows Server en Azure][InstallMongoOnWindowsVM].

Una vez haya creado la máquina virtual de Hola en Azure e instalado MongoDB, sea seguro tooremember Hola DNS nombre de máquina virtual de hello (por ejemplo, "testlinuxvm.cloudapp.net") y el puerto externo de Hola MongoDB que especificó en el punto de conexión de Hola.  Necesitará esta información más adelante en el tutorial Hola.

<a id="createapp"></a>

## <a name="create-hello-application"></a>Crear aplicación hello
En esta sección creará una aplicación de ASP.NET denominada "Mi lista de tareas" mediante el uso de Visual Studio y realizar una aplicación del servicio de aplicaciones Web de tooAzure de implementación inicial. Va a ejecutar localmente la aplicación hello, pero se conectar la máquina virtual de tooyour en Azure y utilizará la instancia de MongoDB Hola que ha creado no existe.

1. En Visual Studio, haga clic en **Nuevo proyecto**.
   
    ![Página de inicio de nuevo proyecto][StartPageNewProject]
2. Hola **nuevo proyecto** ventana, en el panel izquierdo de hello, seleccione **Visual C#**y, a continuación, seleccione **Web**. En el panel central de hello, seleccione **aplicación Web ASP.NET**. En la parte inferior de hello, denomine el proyecto "MyTaskListApp" y, a continuación, haga clic en **Aceptar**.
   
    ![Cuadro de diálogo Nuevo proyecto][NewProjectMyTaskListApp]
3. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, seleccione **MVC**y, a continuación, haga clic en **Aceptar**.
   
    ![Seleccione la plantilla MVC][VS2013SelectMVCTemplate]
4. Si ya no se inició sesión en Microsoft Azure, es posible que toosign solicitada en. Siga toosign de mensajes de Hola en Azure.
5. Una vez que ha iniciado sesión, puede comenzar a configurar la aplicación web de Servicio de aplicaciones. Especificar hello **nombre de aplicación Web**, **plan de servicio de aplicaciones**, **grupo de recursos**, y **región**, a continuación, haga clic en **crear**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. Una vez finalizada la creación del proyecto de hello, espere hello web app toobe creado en el servicio de aplicación de Azure como se indica en hello **actividad de servicio de aplicación de Azure** ventana. A continuación, haga clic en **toothis de MyTaskListApp publicar aplicación Web ahora**.
7. Haga clic en **Publicar**.
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    Una vez que la aplicación de ASP.NET de forma predeterminada está publicada tooAzure aplicaciones de Web del servicio de aplicación, se iniciará en el Explorador de Hola.

## <a name="install-hello-mongodb-c-driver"></a>Instalar Hola controlador MongoDB C#
MongoDB ofrece compatibilidad de cliente para las aplicaciones de C# mediante un controlador, que debe tooinstall en el equipo de desarrollo local. Hola C# controlador está disponible a través de NuGet.

Hola tooinstall controlador MongoDB C#:

1. En **el Explorador de soluciones**, contextual hello **MyTaskListApp** de proyecto y seleccione **NuGetPackages administrar**.
   
    ![Administración de paquetes de NuGet][VS2013ManageNuGetPackages]
2. Hola **administrar paquetes de NuGet** ventana, en el panel izquierdo de hello, haga clic en **Online**. Hola **buscar en línea** en hello derecho, escriba "mongodb.driver".  Haga clic en **instalar** controlador de hello tooinstall.
   
    ![Búsqueda del controlador C# de MongoDB][SearchforMongoDBCSharpDriver]
3. Haga clic en **acepto** tooaccept hello 10gen, Inc. de términos de licencia.
4. Haga clic en **cerrar** después de que ha instalado el controlador de Hola.
    ![Se ha instalado el controlador C# de MongoDB][MongoDBCsharpDriverInstalled]

Hola MongoDB C# controlador ya está instalado.  Referencias toohello **MongoDB.Bson**, **MongoDB.Driver**, y **MongoDB.Driver.Core** bibliotecas se han agregado toohello proyecto.

![Referencias del controlador C# de MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a>Adición de un modelo
En **el Explorador de soluciones**, contextual hello *modelos* carpeta y **agregar** un nuevo **clase** y asígnele el nombre *TaskModel.cs* .  En *TaskModel.cs*, reemplace código existente de hello con hello siguiente código:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MongoDB.Bson.Serialization.Attributes;
    using MongoDB.Bson.Serialization.IdGenerators;
    using MongoDB.Bson;

    namespace MyTaskListApp.Models
    {
        public class MyTask
        {
            [BsonId(IdGenerator = typeof(CombGuidGenerator))]
            public Guid Id { get; set; }

            [BsonElement("Name")]
            public string Name { get; set; }

            [BsonElement("Category")]
            public string Category { get; set; }

            [BsonElement("Date")]
            public DateTime Date { get; set; }

            [BsonElement("CreatedDate")]
            public DateTime CreatedDate { get; set; }

        }
    }

## <a name="add-hello-data-access-layer"></a>Agregar capa de acceso a datos de Hola
En **el Explorador de soluciones**, contextual hello *MyTaskListApp* proyecto y **agregar** una **nueva carpeta** denominado *DAL*.  Menú contextual hello *DAL* carpeta y **agregar** un nuevo **clase**. Archivo de clase de nombre hello *Dal.cs*.  En *Dal.cs*, reemplace código existente de hello con hello siguiente código:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;


    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            private MongoServer mongoServer = null;
            private bool disposed = false;

            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from hello MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }

            // Creates a Task and inserts it into hello collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }

            private IMongoCollection<MyTask> GetTasksCollection()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
                MongoClient client = new MongoClient(connectionString);
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }

            # region IDisposable

            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        if (mongoServer != null)
                        {
                            this.mongoServer.Disconnect();
                        }
                    }
                }

                this.disposed = true;
            }

            # endregion
        }
    }

## <a name="add-a-controller"></a>Adición de un controlador
Abra hello *controllers\homecontroller* en el archivo **el Explorador de soluciones** y reemplace el código existente de hello con siguiente de hello:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.Mvc;
    using MyTaskListApp.Models;
    using System.Configuration;

    namespace MyTaskListApp.Controllers
    {
        public class HomeController : Controller, IDisposable
        {
            private Dal dal = new Dal();
            private bool disposed = false;
            //
            // GET: /MyTask/

            public ActionResult Index()
            {
                return View(dal.GetAllTasks());
            }

            //
            // GET: /MyTask/Create

            public ActionResult Create()
            {
                return View();
            }

            //
            // POST: /MyTask/Create

            [HttpPost]
            public ActionResult Create(MyTask task)
            {
                try
                {
                    dal.CreateTask(task);
                    return RedirectToAction("Index");
                }
                catch
                {
                    return View();
                }
            }

            public ActionResult About()
            {
                return View();
            }

            # region IDisposable

            new protected void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }

            new protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                        this.dal.Dispose();
                    }
                }

                this.disposed = true;
            }

            # endregion

        }
    }

## <a name="set-up-hello-styles"></a>Establecer estilos de Hola
título de hello toochange al principio de Hola de página de hello, abra hello *Views\Shared\\_Layout.cshtml* en el archivo **el Explorador de soluciones** y reemplace "Nombre de la aplicación" en el encabezado de la barra de navegación de Hola a "mi tarea Aplicación lista"para que tenga un aspecto similar al siguiente:

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

En orden tooset menú de la lista de tareas de hello, abra hello *\Views\Home\Index.cshtml* archivo y reemplace código existente de hello con hello siguiente código:

    @model IEnumerable<MyTaskListApp.Models.MyTask>

    @{
        ViewBag.Title = "My Task List";
    }

    <h2>My Task List</h2>

    <table border="1">
        <tr>
            <th>Task</th>
            <th>Category</th>
            <th>Date</th>

        </tr>

    @foreach (var item in Model) {
        <tr>
            <td>
                @Html.DisplayFor(modelItem => item.Name)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Category)
            </td>
            <td>
                @Html.DisplayFor(modelItem => item.Date)
            </td>

        </tr>
    }

    </table>
    <div>  @Html.Partial("Create", new MyTaskListApp.Models.MyTask())</div>


tooadd Hola capacidad toocreate una nueva tarea, haga clic en hello *Views\Home\\*  carpeta y **agregar** una **vista**.  Nombre de la vista de hello *crear*. Reemplace el código de hello con hello siguiente:

    @model MyTaskListApp.Models.MyTask

    <script src="@Url.Content("~/Scripts/jquery-1.10.2.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.min.js")" type="text/javascript"></script>
    <script src="@Url.Content("~/Scripts/jquery.validate.unobtrusive.min.js")" type="text/javascript"></script>

    @using (Html.BeginForm("Create", "Home")) {
        @Html.ValidationSummary(true)
        <fieldset>
            <legend>New Task</legend>

            <div class="editor-label">
                @Html.LabelFor(model => model.Name)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Name)
                @Html.ValidationMessageFor(model => model.Name)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Category)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Category)
                @Html.ValidationMessageFor(model => model.Category)
            </div>

            <div class="editor-label">
                @Html.LabelFor(model => model.Date)
            </div>
            <div class="editor-field">
                @Html.EditorFor(model => model.Date)
                @Html.ValidationMessageFor(model => model.Date)
            </div>

            <p>
                <input type="submit" value="Create" />
            </p>
        </fieldset>
    }

**Explorador de soluciones** debe tener la siguiente apariencia:

![Explorador de soluciones][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a>Establece la cadena de conexión de MongoDB Hola
En **el Explorador de soluciones**, abra hello *DAL/Dal.cs* archivo. Encontrar Hola después de la línea de código:

    private string connectionString = "mongodb://<vm-dns-name>";

Reemplace `<vm-dns-name>` con el nombre DNS de Hola de máquina virtual de hello ejecutando MongoDB que creó en hello [crear una máquina virtual e instale MongoDB] [ Create a virtual machine and install MongoDB] paso de este tutorial.  nombre DNS de hello toofind de la máquina virtual, vaya toohello Portal de Azure, seleccione **máquinas virtuales**y busque **nombre DNS**.

Si el nombre DNS de Hola de máquina virtual de hello es "testlinuxvm.cloudapp.net" y MongoDB está escuchando en el puerto predeterminado de hello 27017, línea de cadena de conexión de Hola de código será similar:

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

Si el punto de conexión de máquina virtual de hello especifica otro puerto externo para MongoDB, puede especificar puerto de hello en la cadena de conexión de hello:

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

Para más información sobre las cadenas de conexión de MongoDB, consulte [Connections][MongoConnectionStrings] (Conexiones).

## <a name="test-hello-local-deployment"></a>Probar la implementación local de Hola
Seleccione de la aplicación en el equipo de desarrollo, toorun **Iniciar depuración** de hello **depurar** menú o presione **F5**. IIS Express se inicia y un explorador se abre e inicia la página principal de la aplicación hello.  Puede agregar una nueva tarea, que se agregará la base de datos de MongoDB toohello ejecutando en la máquina virtual de Azure.

![Aplicación My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a>Publicar aplicaciones de tooAzure aplicación de servicio Web
En esta sección publicará la aplicación del servicio de aplicaciones Web tooAzure de cambios.

1. En el Explorador de soluciones, haga nuevamente clic con el botón derecho en **MyTaskListApp** y, a continuación, haga clic en **Publicar**.
2. Haga clic en **Publicar**.
   
    Ahora debería ver la aplicación web se ejecuta en el servicio de aplicaciones de Azure y obtener acceso a la base de datos de MongoDB de hello en máquinas virtuales de Azure.

## <a name="summary"></a>Resumen
Ahora se ha implementado correctamente su tooAzure de aplicación aplicación del servicio de aplicaciones Web ASP.NET. aplicación web de tooview hello:

1. Inicie sesión en hello Portal de Azure.
2. Haga clic en **Aplicaciones web**. 
3. Seleccione la aplicación web en hello **aplicaciones Web** lista.

Para más información sobre el desarrollo de aplicaciones C# en relación con MongoDB, consulte el [Centro de lenguaje CSharp][MongoC#LangCenter]. 

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- HYPERLINKS -->

[AzurePortal]: http://manage.windowsazure.com
[WindowsAzure]: http://www.windowsazure.com
[MongoC#LangCenter]: http://docs.mongodb.org/ecosystem/drivers/csharp/
[MVCWebSite]: http://www.asp.net/mvc
[ASP.NET]: http://www.asp.net/
[MongoConnectionStrings]: http://www.mongodb.org/display/DOCS/Connections
[MongoDB]: http://www.mongodb.org
[InstallMongoOnWindowsVM]:../virtual-machines/windows/classic/install-mongodb.md
[VSEWeb]: http://www.microsoft.com/visualstudio/eng/2013-downloads#d-2013-express
[VSUlt]: http://www.microsoft.com/visualstudio/eng/2013-downloads

<!-- IMAGES -->


[StartPageNewProject]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProject.png
[NewProjectMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/NewProjectMyTaskListApp.png
[VS2013SelectMVCTemplate]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013SelectMVCTemplate.png
[VS2013DefaultMVCApplication]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013DefaultMVCApplication.png
[VS2013ManageNuGetPackages]: ./media/web-sites-dotnet-store-data-mongodb-vm/VS2013ManageNuGetPackages.png
[SearchforMongoDBCSharpDriver]: ./media/web-sites-dotnet-store-data-mongodb-vm/SearchforMongoDBCSharpDriver.png
[MongoDBCsharpDriverInstalled]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCsharpDriverInstalled.png
[MongoDBCSharpDriverReferences]: ./media/web-sites-dotnet-store-data-mongodb-vm/MongoDBCSharpDriverReferences.png
[SolutionExplorerMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/SolutionExplorerMyTaskListApp.png
[TaskListAppBlank]: ./media/web-sites-dotnet-store-data-mongodb-vm/TaskListAppBlank.png
[WAWSCreateWebSite]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSCreateWebSite.png
[WAWSDashboardMyTaskListApp]: ./media/web-sites-dotnet-store-data-mongodb-vm/WAWSDashboardMyTaskListApp.png
[Image9]: ./media/web-sites-dotnet-store-data-mongodb-vm/RepoReady.png
[Image10]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitInstructions.png
[Image11]: ./media/web-sites-dotnet-store-data-mongodb-vm/GitDeploymentComplete.png

<!-- TOC BOOKMARKS -->
[Create a virtual machine and install MongoDB]: #virtualmachine
[Create and run hello My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy hello ASP.NET application toohello web site using Git]: #deployapp
