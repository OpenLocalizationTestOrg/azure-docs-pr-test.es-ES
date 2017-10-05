---
title: "Creación de una aplicación web de Azure que se conecta a MongoDB en una máquina virtual"
description: "Un tutorial que le enseña a usar Git para implementar una aplicación ASP.NET en un Servicio de aplicaciones de Azure conectado a MongoDB en una máquina virtual de Azure."
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
ms.openlocfilehash: a3f289ed9c764d0859573de4f834e042d0f103c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-in-azure-that-connects-to-mongodb-running-on-a-virtual-machine"></a><span data-ttu-id="79687-103">Creación de una aplicación web de Azure que se conecta a MongoDB en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="79687-103">Create a web app in Azure that connects to MongoDB running on a virtual machine</span></span>
<span data-ttu-id="79687-104">Puede utilizar Git para implementar una aplicación ASP.NET en Aplicaciones web de Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-104">Using Git, you can deploy an ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="79687-105">En este tutorial, generará una aplicación de lista de tareas ASP.NET MVC front-end simple que se conecta a una base de datos MongoDB en una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-105">In this tutorial, you will build a simple front-end ASP.NET MVC task list application that connects to a MongoDB database running on a virtual machine in Azure.</span></span>  <span data-ttu-id="79687-106">[MongoDB][MongoDB] es una conocida base de datos NoSQL de código abierto y alto rendimiento.</span><span class="sxs-lookup"><span data-stu-id="79687-106">[MongoDB][MongoDB] is a popular open source, high performance NoSQL database.</span></span> <span data-ttu-id="79687-107">Después de ejecutar y realizar la prueba de la aplicación ASP.NET en el equipo de desarrollo, cargará la aplicación en Aplicaciones web de Servicio de aplicaciones con Git.</span><span class="sxs-lookup"><span data-stu-id="79687-107">After running and testing the ASP.NET application on your development computer, you will upload the application to App Service Web Apps using Git.</span></span>

> [!NOTE]
> <span data-ttu-id="79687-108">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="79687-108">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="79687-109">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="79687-109">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="background-knowledge"></a><span data-ttu-id="79687-110">Conocimientos previos</span><span class="sxs-lookup"><span data-stu-id="79687-110">Background knowledge</span></span>
<span data-ttu-id="79687-111">El conocimiento de los siguientes aspectos es útil para este tutorial, aunque no es obligatorio:</span><span class="sxs-lookup"><span data-stu-id="79687-111">Knowledge of the following is useful for this tutorial, though not required:</span></span>

* <span data-ttu-id="79687-112">El controlador C# para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="79687-112">The C# driver for MongoDB.</span></span> <span data-ttu-id="79687-113">Para más información sobre el desarrollo de aplicaciones C# en relación con MongoDB, consulte el [Centro de lenguaje CSharp de MongoDB][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="79687-113">For more information on developing C# applications against MongoDB, see the MongoDB [CSharp Language Center][MongoC#LangCenter].</span></span> 
* <span data-ttu-id="79687-114">El marco de la aplicación web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="79687-114">The ASP .NET web application framework.</span></span> <span data-ttu-id="79687-115">Puede obtener toda la información en el [sitio web de ASP.net][ASP.NET].</span><span class="sxs-lookup"><span data-stu-id="79687-115">You can learn all about it at the [ASP.net website][ASP.NET].</span></span>
* <span data-ttu-id="79687-116">El marco de la aplicación web ASP .NET MVC.</span><span class="sxs-lookup"><span data-stu-id="79687-116">The ASP .NET MVC web application framework.</span></span> <span data-ttu-id="79687-117">Puede obtener toda la información en el [sitio web de ASP.NET MVC][MVCWebSite].</span><span class="sxs-lookup"><span data-stu-id="79687-117">You can learn all about it at the [ASP.NET MVC website][MVCWebSite].</span></span>
* <span data-ttu-id="79687-118">Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-118">Azure.</span></span> <span data-ttu-id="79687-119">Puede comenzar leyendo [Azure][WindowsAzure].</span><span class="sxs-lookup"><span data-stu-id="79687-119">You can get started reading at [Azure][WindowsAzure].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79687-120">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="79687-120">Prerequisites</span></span>
* <span data-ttu-id="79687-121">[Visual Studio Express 2013 para Web][VSEWeb] o [Visual Studio 2013][VSUlt]</span><span class="sxs-lookup"><span data-stu-id="79687-121">[Visual Studio Express 2013 for Web][VSEWeb] or [Visual Studio 2013][VSUlt]</span></span>
* [<span data-ttu-id="79687-122">SDK de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="79687-122">Azure SDK for .NET</span></span>](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409)
* <span data-ttu-id="79687-123">Una suscripción de Microsoft Azure activa</span><span class="sxs-lookup"><span data-stu-id="79687-123">An active Microsoft Azure subscription</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

<a id="virtualmachine"></a> 

## <a name="create-a-virtual-machine-and-install-mongodb"></a><span data-ttu-id="79687-124">Creación de una máquina virtual e instalación de MongoDB</span><span class="sxs-lookup"><span data-stu-id="79687-124">Create a virtual machine and install MongoDB</span></span>
<span data-ttu-id="79687-125">En este tutorial se presupone que ha creado una máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-125">This tutorial assumes you have created a virtual machine in Azure.</span></span> <span data-ttu-id="79687-126">Después de crear la máquina virtual, tiene que instalar MongoDB en la misma:</span><span class="sxs-lookup"><span data-stu-id="79687-126">After creating the virtual machine you need to install MongoDB on the virtual machine:</span></span>

* <span data-ttu-id="79687-127">Para crear una máquina virtual Windows e instalar MongoDB, consulte [Instalación de MongoDB en una máquina virtual con Windows Server en Azure][InstallMongoOnWindowsVM].</span><span class="sxs-lookup"><span data-stu-id="79687-127">To create a Windows virtual machine and install MongoDB, see [Install MongoDB on a virtual machine running Windows Server in Azure][InstallMongoOnWindowsVM].</span></span>

<span data-ttu-id="79687-128">Después de haber creado la máquina virtual en Azure e instalado MongoDB, asegúrese de recordar el nombre de DNS de la máquina virtual ("testlinuxvm.cloudapp.net", por ejemplo) y el puerto externo de MongoDB que especificó en el extremo.</span><span class="sxs-lookup"><span data-stu-id="79687-128">After you have created the virtual machine in Azure and installed MongoDB, be sure to remember the DNS name of the virtual machine ("testlinuxvm.cloudapp.net", for example) and the external port for MongoDB that you specified in the endpoint.</span></span>  <span data-ttu-id="79687-129">Necesitará esta información posteriormente en el tutorial.</span><span class="sxs-lookup"><span data-stu-id="79687-129">You will need this information later in the tutorial.</span></span>

<a id="createapp"></a>

## <a name="create-the-application"></a><span data-ttu-id="79687-130">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="79687-130">Create the application</span></span>
<span data-ttu-id="79687-131">En esta sección creará una aplicación ASP.NET denominada "My Task List" mediante Visual Studio y realizará una implementación inicial en las Aplicaciones web del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-131">In this section you will create an ASP.NET application called "My Task List" by using Visual Studio and perform an initial deployment to Azure App Service Web Apps.</span></span> <span data-ttu-id="79687-132">Ejecutará la aplicación localmente, pero se conectará con la máquina virtual en Azure y usará la instancia de MongoDB creada ahí.</span><span class="sxs-lookup"><span data-stu-id="79687-132">You will run the application locally, but it will connect to your virtual machine on Azure and use the MongoDB instance that you created there.</span></span>

1. <span data-ttu-id="79687-133">En Visual Studio, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="79687-133">In Visual Studio, click **New Project**.</span></span>
   
    ![Página de inicio de nuevo proyecto][StartPageNewProject]
2. <span data-ttu-id="79687-135">En la ventana **Nuevo proyecto**, en el panel izquierdo, seleccione **Visual C#** y, a continuación, seleccione **Web**.</span><span class="sxs-lookup"><span data-stu-id="79687-135">In the **New Project** window, in the left pane, select **Visual C#**, and then select **Web**.</span></span> <span data-ttu-id="79687-136">En el panel intermedio, seleccione **Aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="79687-136">In the middle pane, select **ASP.NET  Web Application**.</span></span> <span data-ttu-id="79687-137">En la parte inferior, utilice el nombre "MyTaskListApp" para el proyecto y, a continuación, haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="79687-137">At the bottom, name your project "MyTaskListApp," and then click **OK**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto][NewProjectMyTaskListApp]
3. <span data-ttu-id="79687-139">En el cuadro de diálogo **Nuevo proyecto de ASP.NET**, seleccione **MVC** y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="79687-139">In the **New ASP.NET Project** dialog box, select **MVC**, and then click **OK**.</span></span>
   
    ![Seleccione la plantilla MVC][VS2013SelectMVCTemplate]
4. <span data-ttu-id="79687-141">Si ya no está registrado en Microsoft Azure, se le solicitará que inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="79687-141">If you aren't already signed into Microsoft Azure, you will be prompted to sign in.</span></span> <span data-ttu-id="79687-142">Siga las indicaciones para iniciar sesión en Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-142">Follow the prompts to sign into Azure.</span></span>
5. <span data-ttu-id="79687-143">Una vez que ha iniciado sesión, puede comenzar a configurar la aplicación web de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="79687-143">Once you are signed in, you can start configuring your App Service web app.</span></span> <span data-ttu-id="79687-144">Especifique el **nombre de aplicación web**, el **plan de App Service**, **Grupo de recursos** y **Región** y, luego, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="79687-144">Specify the **Web App name**, **App Service plan**, **Resource group**, and **Region**, then click **Create**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSConfigureWebAppSettings.png)
6. <span data-ttu-id="79687-145">Una vez completada la creación del proyecto, se espera para que la aplicación web que se creará en el servicio de aplicación de Azure como se indica en la ventana **Actividad de Servicio de aplicaciones de Azure** .</span><span class="sxs-lookup"><span data-stu-id="79687-145">After the project creation completes, wait for the web app to be created in Azure App Service as indicated in the **Azure App Service Activity** window.</span></span> <span data-ttu-id="79687-146">A continuación, haga clic en **Publicar MyTaskListApp en esta aplicación web ahora**.</span><span class="sxs-lookup"><span data-stu-id="79687-146">Then, click **Publish MyTaskListApp to this Web App now**.</span></span>
7. <span data-ttu-id="79687-147">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="79687-147">Click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-store-data-mongodb-vm/VSPublishWeb.png)
   
    <span data-ttu-id="79687-148">Una vez publicada la aplicación ASP.NET de forma predeterminada en las aplicaciones web de Servicio de aplicaciones de Azure, se iniciará en el explorador.</span><span class="sxs-lookup"><span data-stu-id="79687-148">Once your default ASP.NET application is published to Azure App Service Web Apps, it will be launched in the browser.</span></span>

## <a name="install-the-mongodb-c-driver"></a><span data-ttu-id="79687-149">Instalación del controlador C# de MongoDB</span><span class="sxs-lookup"><span data-stu-id="79687-149">Install the MongoDB C# driver</span></span>
<span data-ttu-id="79687-150">MongoDB ofrece soporte de cliente para aplicaciones C# a través de un controlador, que tiene que instalar en el equipo de desarrollo local.</span><span class="sxs-lookup"><span data-stu-id="79687-150">MongoDB offers client-side support for C# applications through a driver, which you need to install on your local development computer.</span></span> <span data-ttu-id="79687-151">El controlador C# se encuentra disponible a través de NuGet.</span><span class="sxs-lookup"><span data-stu-id="79687-151">The C# driver is available through NuGet.</span></span>

<span data-ttu-id="79687-152">Para instalar el controlador C# de MongoDB:</span><span class="sxs-lookup"><span data-stu-id="79687-152">To install the MongoDB C# driver:</span></span>

1. <span data-ttu-id="79687-153">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **MyTaskListApp** y seleccione **Administrar NuGetPackages**.</span><span class="sxs-lookup"><span data-stu-id="79687-153">In **Solution Explorer**, right-click the **MyTaskListApp** project and select **Manage NuGetPackages**.</span></span>
   
    ![Administración de paquetes de NuGet][VS2013ManageNuGetPackages]
2. <span data-ttu-id="79687-155">En la ventana **Administrar paquetes de NuGet**, en el panel izquierdo, haga clic en **En línea**.</span><span class="sxs-lookup"><span data-stu-id="79687-155">In the **Manage NuGet Packages** window, in the left pane, click **Online**.</span></span> <span data-ttu-id="79687-156">En el cuadro **Buscar en línea** de la derecha, escriba "mongodb.driver".</span><span class="sxs-lookup"><span data-stu-id="79687-156">In the **Search Online** box on the right, type "mongodb.driver".</span></span>  <span data-ttu-id="79687-157">Haga clic en **Instalar** para instalar el controlador.</span><span class="sxs-lookup"><span data-stu-id="79687-157">Click **Install** to install the driver.</span></span>
   
    ![Búsqueda del controlador C# de MongoDB][SearchforMongoDBCSharpDriver]
3. <span data-ttu-id="79687-159">Haga clic en **Acepto** para aceptar los términos de licencia de 10gen, Inc.</span><span class="sxs-lookup"><span data-stu-id="79687-159">Click **I Accept** to accept the 10gen, Inc. license terms.</span></span>
4. <span data-ttu-id="79687-160">Haga clic en **Cerrar** una vez que se haya instalado el controlador.</span><span class="sxs-lookup"><span data-stu-id="79687-160">Click **Close** after the driver has installed.</span></span>
    <span data-ttu-id="79687-161">![Se ha instalado el controlador C# de MongoDB][MongoDBCsharpDriverInstalled]</span><span class="sxs-lookup"><span data-stu-id="79687-161">![MongoDB C# Driver Installed][MongoDBCsharpDriverInstalled]</span></span>

<span data-ttu-id="79687-162">El controlador C# de MongoDB está ahora instalado.</span><span class="sxs-lookup"><span data-stu-id="79687-162">The MongoDB C# driver is now installed.</span></span>  <span data-ttu-id="79687-163">Se han agregado al proyecto referencias a las bibliotecas **MongoDB.Bson**, **MongoDB.Driver** y **MongoDB.Driver.Core**.</span><span class="sxs-lookup"><span data-stu-id="79687-163">References to the **MongoDB.Bson**, **MongoDB.Driver**, and **MongoDB.Driver.Core**  libraries have been added to the project.</span></span>

![Referencias del controlador C# de MongoDB][MongoDBCSharpDriverReferences]

## <a name="add-a-model"></a><span data-ttu-id="79687-165">Adición de un modelo</span><span class="sxs-lookup"><span data-stu-id="79687-165">Add a model</span></span>
<span data-ttu-id="79687-166">En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta *Models* y seleccione **Agregar** una nueva **Clase** y asígnele el nombre *TaskModel.cs*.</span><span class="sxs-lookup"><span data-stu-id="79687-166">In **Solution Explorer**, right-click the *Models* folder and **Add** a new **Class** and name it *TaskModel.cs*.</span></span>  <span data-ttu-id="79687-167">En *TaskModel.cs*, reemplace el código existente por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="79687-167">In *TaskModel.cs*, replace the existing code with the following code:</span></span>

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

## <a name="add-the-data-access-layer"></a><span data-ttu-id="79687-168">Incorporación de un nivel de acceso de datos</span><span class="sxs-lookup"><span data-stu-id="79687-168">Add the data access layer</span></span>
<span data-ttu-id="79687-169">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto *MyTaskListApp* y seleccione **Agregar** una **Carpeta nueva** llamada *DAL*.</span><span class="sxs-lookup"><span data-stu-id="79687-169">In **Solution Explorer**, right-click the *MyTaskListApp* project and **Add** a **New Folder** named *DAL*.</span></span>  <span data-ttu-id="79687-170">Haga clic con el botón derecho en la carpeta *DAL* y use la opción **Agregar** una nueva **Clase**.</span><span class="sxs-lookup"><span data-stu-id="79687-170">Right-click the *DAL* folder and **Add** a new **Class**.</span></span> <span data-ttu-id="79687-171">Utilice el nombre de archivo de clase *Dal.cs*.</span><span class="sxs-lookup"><span data-stu-id="79687-171">Name the class file *Dal.cs*.</span></span>  <span data-ttu-id="79687-172">En *Dal.cs*, reemplace el código existente por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="79687-172">In *Dal.cs*, replace the existing code with the following code:</span></span>

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

            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net"
            private string connectionString = "mongodb://mongodbsrv20151211.cloudapp.net";

            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";

            // Default constructor.        
            public Dal()
            {
            }

            // Gets all Task items from the MongoDB server.        
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

            // Creates a Task and inserts it into the collection in MongoDB.
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

## <a name="add-a-controller"></a><span data-ttu-id="79687-173">Adición de un controlador</span><span class="sxs-lookup"><span data-stu-id="79687-173">Add a controller</span></span>
<span data-ttu-id="79687-174">Abra el archivo *Controllers\HomeController.cs* en el **Explorador de soluciones** y reemplace el código existente por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79687-174">Open the *Controllers\HomeController.cs* file in **Solution Explorer** and replace the existing code with the following:</span></span>

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

## <a name="set-up-the-styles"></a><span data-ttu-id="79687-175">Configuración de estilos</span><span class="sxs-lookup"><span data-stu-id="79687-175">Set up the styles</span></span>
<span data-ttu-id="79687-176">Para cambiar el título en la parte superior de la página, abra el archivo *Views\Shared\\_Layout.cshtml* en el **Explorador de soluciones** y reemplace "Application name" en el encabezado de la barra de exploración por "My Task List Application" de manera que tenga la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="79687-176">To change the title at the top of the page, open the *Views\Shared\\_Layout.cshtml* file in **Solution Explorer** and replace "Application name" in the navbar header with "My Task List Application" so that it looks like this:</span></span>

     @Html.ActionLink("My Task List Application", "Index", "Home", null, new { @class = "navbar-brand" })

<span data-ttu-id="79687-177">Para configurar el menú Task List, abra el archivo *\Views\Home\Index.cshtml* y reemplace el código existente por el siguiente código:</span><span class="sxs-lookup"><span data-stu-id="79687-177">In order to set up the Task List menu, open the *\Views\Home\Index.cshtml* file and replace the existing code with the following code:</span></span>

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


<span data-ttu-id="79687-178">Para agregar la capacidad de crear una nueva tarea, haga clic con el botón derecho en la carpeta *Views\Home\\\* y use la opción **Agregar** para agregar una vista en **Vista**.</span><span class="sxs-lookup"><span data-stu-id="79687-178">To add the ability to create a new task, right-click the *Views\Home\\* folder and **Add** a **View**.</span></span>  <span data-ttu-id="79687-179">Asigne a la vista el nombre *Create*.</span><span class="sxs-lookup"><span data-stu-id="79687-179">Name the view *Create*.</span></span> <span data-ttu-id="79687-180">Reemplace el código por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="79687-180">Replace the code with the following:</span></span>

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

<span data-ttu-id="79687-181">**Explorador de soluciones** debe tener la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="79687-181">**Solution Explorer** should look like this:</span></span>

![Explorador de soluciones][SolutionExplorerMyTaskListApp]

## <a name="set-the-mongodb-connection-string"></a><span data-ttu-id="79687-183">Establecimiento de la cadena de conexión de MongoDB</span><span class="sxs-lookup"><span data-stu-id="79687-183">Set the MongoDB connection string</span></span>
<span data-ttu-id="79687-184">En el **Explorador de soluciones**, abra el archivo *DAL/Dal.cs* .</span><span class="sxs-lookup"><span data-stu-id="79687-184">In **Solution Explorer**, open the *DAL/Dal.cs* file.</span></span> <span data-ttu-id="79687-185">Busque la siguiente línea de código:</span><span class="sxs-lookup"><span data-stu-id="79687-185">Find the following line of code:</span></span>

    private string connectionString = "mongodb://<vm-dns-name>";

<span data-ttu-id="79687-186">Reemplace `<vm-dns-name>` por el nombre DNS de la máquina virtual que ejecuta el MongoDB que creó en el paso [Creación de una máquina virtual e instalación de MongoDB][Create a virtual machine and install MongoDB] de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="79687-186">Replace `<vm-dns-name>` with the DNS name of the virtual machine running MongoDB you created in the [Create a virtual machine and install MongoDB][Create a virtual machine and install MongoDB] step of this tutorial.</span></span>  <span data-ttu-id="79687-187">Para buscar el nombre de DNS de la máquina virtual, vaya a Azure Portal, seleccione **Máquinas virtuales** y busque **Nombre DNS**.</span><span class="sxs-lookup"><span data-stu-id="79687-187">To find the DNS name of your virtual machine, go to the Azure Portal, select **Virtual Machines**, and find **DNS Name**.</span></span>

<span data-ttu-id="79687-188">Si el nombre de DNS de la máquina virtual es "testlinuxvm.cloudapp.net" y MongoDB está escuchando en el puerto predeterminado 27017, la línea de la cadena de conexión del código tendrá la siguiente apariencia:</span><span class="sxs-lookup"><span data-stu-id="79687-188">If the DNS name of the virtual machine is "testlinuxvm.cloudapp.net" and MongoDB is listening on the default port 27017, the connection string line of code will look like:</span></span>

    private string connectionString = "mongodb://testlinuxvm.cloudapp.net";

<span data-ttu-id="79687-189">Si el extremo de la máquina virtual especifica un puerto externo distinto para MongoDB, puede especificar el puerto en la cadena de conexión:</span><span class="sxs-lookup"><span data-stu-id="79687-189">If the virtual machine endpoint specifies a different external port for MongoDB, you can specifiy the port in the connection string:</span></span>

     private string connectionString = "mongodb://testlinuxvm.cloudapp.net:12345";

<span data-ttu-id="79687-190">Para más información sobre las cadenas de conexión de MongoDB, consulte [Connections][MongoConnectionStrings] (Conexiones).</span><span class="sxs-lookup"><span data-stu-id="79687-190">For more information on MongoDB connection strings, see [Connections][MongoConnectionStrings].</span></span>

## <a name="test-the-local-deployment"></a><span data-ttu-id="79687-191">Prueba de la implementación local</span><span class="sxs-lookup"><span data-stu-id="79687-191">Test the local deployment</span></span>
<span data-ttu-id="79687-192">Para ejecutar la aplicación en el equipo de desarrollo, seleccione **Iniciar depuración** en el menú **Depurar** o presione **F5**.</span><span class="sxs-lookup"><span data-stu-id="79687-192">To run your application on your development computer, select **Start Debugging** from the **Debug** menu or hit **F5**.</span></span> <span data-ttu-id="79687-193">IIS Express se iniciará y se abrirá un explorador y se iniciará la página principal de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="79687-193">IIS Express starts and a browser opens and launches the application's home page.</span></span>  <span data-ttu-id="79687-194">Puede agregar una nueva tarea, que se agregará a la base de datos de MongoDB que se ejecuta en la máquina virtual en Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-194">You can add a new task, which will be added to the MongoDB database running on your virtual machine in Azure.</span></span>

![Aplicación My Task List][TaskListAppBlank]

## <a name="publish-to-azure-app-service-web-apps"></a><span data-ttu-id="79687-196">Publicación de aplicaciones web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="79687-196">Publish to Azure App Service Web Apps</span></span>
<span data-ttu-id="79687-197">En esta sección publicará los cambios en las aplicaciones web del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-197">In this section you will publish your changes to Azure App Service Web Apps.</span></span>

1. <span data-ttu-id="79687-198">En el Explorador de soluciones, haga nuevamente clic con el botón derecho en **MyTaskListApp** y, a continuación, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="79687-198">In Solution Explorer, right-click **MyTaskListApp** again and click **Publish**.</span></span>
2. <span data-ttu-id="79687-199">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="79687-199">Click **Publish**.</span></span>
   
    <span data-ttu-id="79687-200">Ahora debe ver la aplicación web ejecutándose en Servicio de aplicaciones de Azure y accediendo a la base de datos MongoDB en máquinas virtuales de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-200">You should now see your web app running in Azure App Service and accessing the MongoDB database in Azure Virtual Machines.</span></span>

## <a name="summary"></a><span data-ttu-id="79687-201">Resumen</span><span class="sxs-lookup"><span data-stu-id="79687-201">Summary</span></span>
<span data-ttu-id="79687-202">Ha implementado correctamente la aplicación ASP.NET en aplicaciones web de Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-202">You have now successfully deployed your ASP.NET application to Azure App Service Web Apps.</span></span> <span data-ttu-id="79687-203">Para ver la aplicación web:</span><span class="sxs-lookup"><span data-stu-id="79687-203">To view the web app:</span></span>

1. <span data-ttu-id="79687-204">Inicie sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="79687-204">Log into the Azure Portal.</span></span>
2. <span data-ttu-id="79687-205">Haga clic en **Aplicaciones web**.</span><span class="sxs-lookup"><span data-stu-id="79687-205">Click **Web apps**.</span></span> 
3. <span data-ttu-id="79687-206">Seleccione la aplicación web en la lista **Aplicaciones web** .</span><span class="sxs-lookup"><span data-stu-id="79687-206">Select your web app in the **Web Apps** list.</span></span>

<span data-ttu-id="79687-207">Para más información sobre el desarrollo de aplicaciones C# en relación con MongoDB, consulte el [Centro de lenguaje CSharp][MongoC#LangCenter].</span><span class="sxs-lookup"><span data-stu-id="79687-207">For more information on developing C# applications against MongoDB, see [CSharp Language Center][MongoC#LangCenter].</span></span> 

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
[Create and run the My Task List ASP.NET application on your development computer]: #createapp
[Create an Azure web site]: #createwebsite
[Deploy the ASP.NET application to the web site using Git]: #deployapp
