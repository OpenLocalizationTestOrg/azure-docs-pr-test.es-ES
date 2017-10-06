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
# <a name="create-a-web-app-in-azure-that-connects-toomongodb-running-on-a-virtual-machine"></a><span data-ttu-id="7ab24-103">Crear una aplicación web de Azure que se conecta tooMongoDB que se ejecuta en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7ab24-103">Create a web app in Azure that connects tooMongoDB running on a virtual machine</span></span>
<span data-ttu-id="7ab24-104">Con Git, puede implementar un tooAzure de aplicación aplicación del servicio de aplicaciones Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7ab24-104">Using Git, you can deploy an ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="7ab24-105">En este tutorial, compilará un front-end MVC de ASP.NET simple aplicación de lista de tareas que se conecta la base de datos de MongoDB de tooa ejecuta en una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects tooa MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="7ab24-106">[MongoDB][MongoDB] es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="7ab24-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="7ab24-107">Después de ejecutar y probar la aplicación de ASP.NET de hello en el equipo de desarrollo, se cargará hello tooApp de aplicación Web del servicio de aplicaciones mediante Git.</span><span class="sxs-lookup"><span data-stu-id="7ab24-107">After running and testing hello ASP.NET application on your development computer, you will upload hello application tooApp Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="7ab24-108">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7ab24-108">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="7ab24-109">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="7ab24-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="7ab24-110">Conocimientos previos</span><span class="sxs-lookup"><span data-stu-id="7ab24-110">Background knowledge</span></span>
<span data-ttu-id="7ab24-111">El conocimiento de la siguiente hello es útil para este tutorial, aunque no es necesario:</span><span class="sxs-lookup"><span data-stu-id="7ab24-111">Knowledge of hello following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="7ab24-112">controlador de Hello C# para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7ab24-112">hello C# driver for MongoDB.</span></span> <span data-ttu-id="7ab24-113">Para obtener más información sobre cómo desarrollar aplicaciones de C# con MongoDB, vea Hola MongoDB [Center de lenguaje CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="7ab24-113">For more information on developing C# applications against MongoDB, see hello MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="7ab24-114">marco de aplicación web de Hello ASP. NET.</span><span class="sxs-lookup"><span data-stu-id="7ab24-114">hello ASP .NET web application framework.</span></span> <span data-ttu-id="7ab24-115">Puede obtener información sobre esto en hello [sitio Web de ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="7ab24-115">You can learn all about it at hello [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="7ab24-116">marco de aplicación de web de ASP .NET MVC Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab24-116">hello ASP .NET MVC web application framework.</span></span> <span data-ttu-id="7ab24-117">Puede obtener información sobre esto en hello [sitio Web de ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="7ab24-117">You can learn all about it at hello [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="7ab24-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-118">Azure.</span></span> <span data-ttu-id="7ab24-119">Puede comenzar leyendo [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="7ab24-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ab24-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="7ab24-120">Prerequisites</span></span>
* <span data-ttu-id="7ab24-121">[Visual Studio Express 2013 para Web][VSEWeb] o [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="7ab24-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="7ab24-122">SDK de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="7ab24-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="7ab24-123">Una suscripción de Microsoft Azure activa</span><span class="sxs-lookup"><span data-stu-id="7ab24-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="7ab24-124">Creación de una máquina virtual e instalación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="7ab24-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="7ab24-125">En este tutorial se presupone que ha creado una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="7ab24-126">Después de crear la máquina virtual de hello necesita tooinstall MongoDB en la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="7ab24-126">After creating hello virtual machine you need tooinstall MongoDB on hello virtual machine:</span></span>

* <span data-ttu-id="7ab24-127">toocreate una máquina virtual de Windows e instale MongoDB, consulte [MongoDB instalar en una máquina virtual que ejecute Windows Server en Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="7ab24-127">toocreate a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="7ab24-128">Una vez haya creado la máquina virtual de Hola en Azure e instalado MongoDB, sea seguro tooremember Hola DNS nombre de máquina virtual de hello (por ejemplo, "testlinuxvm.cloudapp.net") y el puerto externo de Hola MongoDB que especificó en el punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab24-128">After you have created hello virtual machine in Azure and installed MongoDB, be sure tooremember hello DNS name of hello virtual machine ("testlinuxvm.cloudapp.net", for example) and hello external port for MongoDB that you specified in hello endpoint.</span></span>  <span data-ttu-id="7ab24-129">Necesitará esta información más adelante en el tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab24-129">You will need this information later in hello tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-hello-application"></a><span data-ttu-id="7ab24-130">Crear aplicación hello</span><span class="sxs-lookup"><span data-stu-id="7ab24-130">Create hello application</span></span>
<span data-ttu-id="7ab24-131">En esta sección creará una aplicación de ASP.NET denominada "Mi lista de tareas" mediante el uso de Visual Studio y realizar una aplicación del servicio de aplicaciones Web de tooAzure de implementación inicial.</span><span class="sxs-lookup"><span data-stu-id="7ab24-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment tooAzure App Service Web Apps.</span></span> <span data-ttu-id="7ab24-132">Va a ejecutar localmente la aplicación hello, pero se conectar la máquina virtual de tooyour en Azure y utilizará la instancia de MongoDB Hola que ha creado no existe.</span><span class="sxs-lookup"><span data-stu-id="7ab24-132">You will run hello application locally, but it will connect tooyour virtual machine on Azure and use hello MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="7ab24-133">En Visual Studio, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Página de inicio de nuevo proyecto][StartPageNewProject]
2. <span data-ttu-id="7ab24-135">Hola **nuevo proyecto** ventana, en el panel izquierdo de hello, seleccione **Visual C#**y, a continuación, seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-135">In hello **New Project** window, in hello left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="7ab24-136">En el panel central de hello, seleccione **aplicación Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-136">In hello middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="7ab24-137">En la parte inferior de hello, denomine el proyecto "MyTaskListApp" y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-137">At hello bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][NewProjectMyTaskListApp]
3. <span data-ttu-id="7ab24-139">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, seleccione **MVC**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-139">In hello **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Seleccione la plantilla MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="7ab24-141">Si ya no se inició sesión en Microsoft Azure, es posible que toosign solicitada en.</span><span class="sxs-lookup"><span data-stu-id="7ab24-141">If you aren't already signed into Microsoft Azure, you will be prompted toosign in.</span></span> <span data-ttu-id="7ab24-142">Siga toosign de mensajes de Hola en Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-142">Follow hello prompts toosign into Azure.</span></span>
5. <span data-ttu-id="7ab24-143">Una vez que ha iniciado sesión, puede comenzar a configurar la aplicación web de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7ab24-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="7ab24-144">Especificar hello **nombre de aplicación Web**, **plan de servicio de aplicaciones**, **grupo de recursos**, y **región**, a continuación, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-144">Specify hello **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="7ab24-145">Una vez finalizada la creación del proyecto de hello, espere hello web app toobe creado en el servicio de aplicación de Azure como se indica en hello **actividad de servicio de aplicación de Azure** ventana.</span><span class="sxs-lookup"><span data-stu-id="7ab24-145">After hello project creation completes, wait for hello web app toobe created in Azure App Service as indicated in hello **Azure App Service Activity** window.</span></span> <span data-ttu-id="7ab24-146">A continuación, haga clic en **toothis de MyTaskListApp publicar aplicación Web ahora**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-146">Then, click **Publish MyTaskListApp toothis Web App now**.</span></span>
7. <span data-ttu-id="7ab24-147">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="7ab24-148">Una vez que la aplicación de ASP.NET de forma predeterminada está publicada tooAzure aplicaciones de Web del servicio de aplicación, se iniciará en el Explorador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab24-148">Once your default ASP.NET application is published tooAzure App Service Web Apps, it will be launched in hello browser.</span></span>

## <a name="install-hello-mongodb-c-driver"></a><span data-ttu-id="7ab24-149">Instalar Hola controlador MongoDB C#</span><span class="sxs-lookup"><span data-stu-id="7ab24-149">Install hello MongoDB C# driver</span></span>
<span data-ttu-id="7ab24-150">MongoDB ofrece compatibilidad de cliente para las aplicaciones de C# mediante un controlador, que debe tooinstall en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="7ab24-150">MongoDB offers client-side support for C# applications through a driver, which you need tooinstall on your local development computer.</span></span> <span data-ttu-id="7ab24-151">Hola C# controlador está disponible a través de NuGet.</span><span class="sxs-lookup"><span data-stu-id="7ab24-151">hello C# driver is available through NuGet.</span></span>

<span data-ttu-id="7ab24-152">Hola tooinstall controlador MongoDB C#:</span><span class="sxs-lookup"><span data-stu-id="7ab24-152">tooinstall hello MongoDB C# driver:</span></span>

1. <span data-ttu-id="7ab24-153">En **el Explorador de soluciones**, contextual hello **MyTaskListApp** de proyecto y seleccione **NuGetPackages administrar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-153">In **Solution Explorer**, right-click hello **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Administración de paquetes de NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="7ab24-155">Hola **administrar paquetes de NuGet** ventana, en el panel izquierdo de hello, haga clic en **Online**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-155">In hello **Manage NuGet Packages** window, in hello left pane, click **Online**.</span></span> <span data-ttu-id="7ab24-156">Hola **buscar en línea** en hello derecho, escriba "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="7ab24-156">In hello **Search Online** box on hello right, type "mongodb.driver".</span></span>  <span data-ttu-id="7ab24-157">Haga clic en **instalar** controlador de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="7ab24-157">Click **Install** tooinstall hello driver.</span></span>
   
    ![Búsqueda del controlador C# de MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="7ab24-159">Haga clic en **acepto** tooaccept hello 10gen, Inc. de términos de licencia.</span><span class="sxs-lookup"><span data-stu-id="7ab24-159">Click **I Accept** tooaccept hello 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="7ab24-160">Haga clic en **cerrar** después de que ha instalado el controlador de Hola.</span><span class="sxs-lookup"><span data-stu-id="7ab24-160">Click **Close** after hello driver has installed.</span></span>
    <span data-ttu-id="7ab24-161">![Se ha instalado el controlador C# de MongoDB][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="7ab24-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="7ab24-162">Hola MongoDB C# controlador ya está instalado.</span><span class="sxs-lookup"><span data-stu-id="7ab24-162">hello MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="7ab24-163">Referencias toohello **MongoDB.Bson**, **MongoDB.Driver**, y **MongoDB.Driver.Core** bibliotecas se han agregado toohello proyecto.</span><span class="sxs-lookup"><span data-stu-id="7ab24-163">References toohello **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added toohello project.</span></span>

![Referencias del controlador C# de MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="7ab24-165">Adición de un modelo</span><span class="sxs-lookup"><span data-stu-id="7ab24-165">Add a model</span></span>
<span data-ttu-id="7ab24-166">En **el Explorador de soluciones**, contextual hello *modelos* carpeta y **agregar** un nuevo **clase** y asígnele el nombre *TaskModel.cs* .</span><span class="sxs-lookup"><span data-stu-id="7ab24-166">In **Solution Explorer**, right-click hello *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="7ab24-167">En *TaskModel.cs*, reemplace código existente de hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7ab24-167">In *TaskModel.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-hello-data-access-layer"></a><span data-ttu-id="7ab24-168">Agregar capa de acceso a datos de Hola</span><span class="sxs-lookup"><span data-stu-id="7ab24-168">Add hello data access layer</span></span>
<span data-ttu-id="7ab24-169">En **el Explorador de soluciones**, contextual hello *MyTaskListApp* proyecto y **agregar** una **nueva carpeta** denominado *DAL*.</span><span class="sxs-lookup"><span data-stu-id="7ab24-169">In **Solution Explorer**, right-click hello *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="7ab24-170">Menú contextual hello *DAL* carpeta y **agregar** un nuevo **clase**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-170">Right-click hello *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="7ab24-171">Archivo de clase de nombre hello *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="7ab24-171">Name hello class file *Dal.cs*.</span></span>  <span data-ttu-id="7ab24-172">En *Dal.cs*, reemplace código existente de hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7ab24-172">In *Dal.cs*, replace hello existing code with hello following code:</span></span>

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

## <a name="add-a-controller"></a><span data-ttu-id="7ab24-173">Adición de un controlador</span><span class="sxs-lookup"><span data-stu-id="7ab24-173">Add a controller</span></span>
<span data-ttu-id="7ab24-174">Abra hello *controllers\homecontroller* en el archivo **el Explorador de soluciones** y reemplace el código existente de hello con siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="7ab24-174">Open hello *Controllers\HomeController.cs* file in **Solution Explorer** and replace hello existing code with hello following:</span></span>

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

## <a name="set-up-hello-styles"></a><span data-ttu-id="7ab24-175">Establecer estilos de Hola</span><span class="sxs-lookup"><span data-stu-id="7ab24-175">Set up hello styles</span></span>
<span data-ttu-id="7ab24-176">título de hello toochange al principio de Hola de página de hello, abra hello *Views\Shared\\_Layout.cshtml* en el archivo **el Explorador de soluciones** y reemplace "Nombre de la aplicación" en el encabezado de la barra de navegación de Hola a "mi tarea Aplicación lista"para que tenga un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ab24-176">toochange hello title at hello top of hello page, open hello *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in hello navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="7ab24-177">En orden tooset menú de la lista de tareas de hello, abra hello *\Views\Home\Index.cshtml* archivo y reemplace código existente de hello con hello siguiente código:</span><span class="sxs-lookup"><span data-stu-id="7ab24-177">In order tooset up hello Task List menu, open hello *\Views\Home\Index.cshtml* file and replace hello existing code with hello following code:</span></span>

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


<span data-ttu-id="7ab24-178">tooadd Hola capacidad toocreate una nueva tarea, haga clic en hello *Views\Home\\*  carpeta y **agregar** una **vista**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-178">tooadd hello ability toocreate a new task, right-click hello *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="7ab24-179">Nombre de la vista de hello *crear*.</span><span class="sxs-lookup"><span data-stu-id="7ab24-179">Name hello view *Create*.</span></span> <span data-ttu-id="7ab24-180">Reemplace el código de hello con hello siguiente:</span><span class="sxs-lookup"><span data-stu-id="7ab24-180">Replace hello code with hello following:</span></span>

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

<span data-ttu-id="7ab24-181">**Explorador de soluciones** debe tener la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="7ab24-181">**Solution Explorer** should look like this:</span></span>

![Explorador de soluciones][SolutionExplorerMyTaskListApp]

## <a name="set-hello-mongodb-connection-string"></a><span data-ttu-id="7ab24-183">Establece la cadena de conexión de MongoDB Hola</span><span class="sxs-lookup"><span data-stu-id="7ab24-183">Set hello MongoDB connection string</span></span>
<span data-ttu-id="7ab24-184">En **el Explorador de soluciones**, abra hello *DAL/Dal.cs* archivo.</span><span class="sxs-lookup"><span data-stu-id="7ab24-184">In **Solution Explorer**, open hello *DAL/Dal.cs* file.</span></span> <span data-ttu-id="7ab24-185">Encontrar Hola después de la línea de código:</span><span class="sxs-lookup"><span data-stu-id="7ab24-185">Find hello following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="7ab24-186">Reemplace `<vm-dns-name>` con el nombre DNS de Hola de máquina virtual de hello ejecutando MongoDB que creó en hello [crear una máquina virtual e instale MongoDB] [ Create a virtual machine and install MongoDB] paso de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="7ab24-186">Replace `<vm-dns-name>` with hello DNS name of hello virtual machine running MongoDB you created in hello [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="7ab24-187">nombre DNS de hello toofind de la máquina virtual, vaya toohello Portal de Azure, seleccione **máquinas virtuales**y busque **nombre DNS**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-187">toofind hello DNS name of your virtual machine, go toohello Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="7ab24-188">Si el nombre DNS de Hola de máquina virtual de hello es "testlinuxvm.cloudapp.net" y MongoDB está escuchando en el puerto predeterminado de hello 27017, línea de cadena de conexión de Hola de código será similar:</span><span class="sxs-lookup"><span data-stu-id="7ab24-188">If hello DNS name of hello virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on hello default port 27017, hello connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="7ab24-189">Si el punto de conexión de máquina virtual de hello especifica otro puerto externo para MongoDB, puede especificar puerto de hello en la cadena de conexión de hello:</span><span class="sxs-lookup"><span data-stu-id="7ab24-189">If hello virtual machine endpoint specifies a different external port for MongoDB, you can specifiy hello port in hello connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="7ab24-190">Para más información sobre las cadenas de conexión de MongoDB, consulte [Connections][MongoConnectionStrings] (Conexiones).</span><span class="sxs-lookup"><span data-stu-id="7ab24-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-hello-local-deployment"></a><span data-ttu-id="7ab24-191">Probar la implementación local de Hola</span><span class="sxs-lookup"><span data-stu-id="7ab24-191">Test hello local deployment</span></span>
<span data-ttu-id="7ab24-192">Seleccione de la aplicación en el equipo de desarrollo, toorun **Iniciar depuración** de hello **depurar** menú o presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-192">toorun your application on your development computer, select **Start Debugging** from hello **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="7ab24-193">IIS Express se inicia y un explorador se abre e inicia la página principal de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7ab24-193">IIS Express starts and a browser opens and launches hello application's home page.</span></span>  <span data-ttu-id="7ab24-194">Puede agregar una nueva tarea, que se agregará la base de datos de MongoDB toohello ejecutando en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-194">You can add a new task, which will be added toohello MongoDB database running on your virtual machine in Azure.</span></span>

![Aplicación My Task List][TaskListAppBlank]

## <a name="publish-tooazure-app-service-web-apps"></a><span data-ttu-id="7ab24-196">Publicar aplicaciones de tooAzure aplicación de servicio Web</span><span class="sxs-lookup"><span data-stu-id="7ab24-196">Publish tooAzure App Service Web Apps</span></span>
<span data-ttu-id="7ab24-197">En esta sección publicará la aplicación del servicio de aplicaciones Web tooAzure de cambios.</span><span class="sxs-lookup"><span data-stu-id="7ab24-197">In this section you will publish your changes tooAzure App Service Web Apps.</span></span>

1. <span data-ttu-id="7ab24-198">En el Explorador de soluciones, haga nuevamente clic con el botón derecho en **MyTaskListApp** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="7ab24-199">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="7ab24-200">Ahora debería ver la aplicación web se ejecuta en el servicio de aplicaciones de Azure y obtener acceso a la base de datos de MongoDB de hello en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-200">You should now see your web app running in Azure App Service and accessing hello MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="7ab24-201">Resumen</span><span class="sxs-lookup"><span data-stu-id="7ab24-201">Summary</span></span>
<span data-ttu-id="7ab24-202">Ahora se ha implementado correctamente su tooAzure de aplicación aplicación del servicio de aplicaciones Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="7ab24-202">You have now successfully deployed your ASP.NET application tooAzure App Service Web Apps.</span></span> <span data-ttu-id="7ab24-203">aplicación web de tooview hello:</span><span class="sxs-lookup"><span data-stu-id="7ab24-203">tooview hello web app:</span></span>

1. <span data-ttu-id="7ab24-204">Inicie sesión en hello Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ab24-204">Log into hello Azure Portal.</span></span>
2. <span data-ttu-id="7ab24-205">Haga clic en **Aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="7ab24-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="7ab24-206">Seleccione la aplicación web en hello **aplicaciones Web** lista.</span><span class="sxs-lookup"><span data-stu-id="7ab24-206">Select your web app in hello **Web Apps** list.</span></span>

<span data-ttu-id="7ab24-207">Para más información sobre el desarrollo de aplicaciones C# en relación con MongoDB, consulte el [Centro de lenguaje CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="7ab24-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
