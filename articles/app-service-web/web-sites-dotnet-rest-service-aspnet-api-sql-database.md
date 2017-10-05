---
title: "Creación de una API de REST en Azure con ASP.NET y la base de datos SQL | Microsoft Docs"
description: "Un tutorial que le enseña cómo implementar una aplicación que utiliza la Web API de ASP.NET en una aplicación web de Azure con Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="6ff97-103">Crear un servicio REST con la Web API de ASP.NET y la base de datos SQL en el servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="6ff97-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="6ff97-104">En este tutorial se muestra cómo implementar una aplicación web ASP.NET en un [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) utilizando el Asistente para publicación web de Visual Studio 2013 o Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="6ff97-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="6ff97-105">Puede abrir una cuenta de Azure de manera gratuita y, si todavía no tiene Visual Studio 2013, el SDK instala automáticamente Visual Studio 2013 Express para Web.</span><span class="sxs-lookup"><span data-stu-id="6ff97-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="6ff97-106">De este modo, puede empezar a desarrollar contenido para Azure sin coste alguno.</span><span class="sxs-lookup"><span data-stu-id="6ff97-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="6ff97-107">En este tutorial se supone que no tiene ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff97-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="6ff97-108">Cuando acabe, tendrá una aplicación web sencilla que se ejecutará en la nube.</span><span class="sxs-lookup"><span data-stu-id="6ff97-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="6ff97-109">Aprenderá a realizar los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="6ff97-109">You'll learn:</span></span>

* <span data-ttu-id="6ff97-110">Habilitar su equipo para desarrollar contenido de Azure mediante la instalación del SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff97-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="6ff97-111">Cómo crear un proyecto ASP.NET MVC 5 de Visual Studio y publicarlo en una aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="6ff97-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="6ff97-112">Utilizar ASP.NET Web API para habilitar llamadas de API de RESTful</span><span class="sxs-lookup"><span data-stu-id="6ff97-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="6ff97-113">Utilizar una Base de datos SQL para almacenar datos en Azure</span><span class="sxs-lookup"><span data-stu-id="6ff97-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="6ff97-114">Publicar actualizaciones de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="6ff97-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="6ff97-115">Va a desarrollar una aplicación web de lista de contactos sencilla basada en ASP.NET MVC 5 y que utiliza ADO.NET Entity Framework para obtener acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="6ff97-116">La siguiente ilustración muestra la aplicación completada:</span><span class="sxs-lookup"><span data-stu-id="6ff97-116">The following illustration shows the completed application:</span></span>

![captura de pantalla de sitio web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="6ff97-118">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="6ff97-118">Create the project</span></span>
1. <span data-ttu-id="6ff97-119">Inicie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6ff97-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="6ff97-120">En el menú **Archivo**, haga clic en **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="6ff97-121">En el cuadro de diálogo **Nuevo proyecto**, expanda **Visual C#**, seleccione **Web** y, luego, **Aplicación web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="6ff97-122">Póngale a la aplicación el nombre **ContactManager** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="6ff97-124">En el cuadro de diálogo **Nuevo proyecto ASP.NET**, seleccione la plantilla **MVC**, active **API Web** y, luego, haga clic en **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="6ff97-125">En el cuadro de diálogo **Cambiar autenticación**, haga clic en **Sin autenticación** y, a continuación, en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Sin autenticación](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="6ff97-127">La aplicación de ejemplo que va a crear no dispondrá de características que requieran que los usuarios inicien sesión.</span><span class="sxs-lookup"><span data-stu-id="6ff97-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="6ff97-128">Para obtener información acerca de cómo implementar la autenticación y las características de autenticación, consulte la sección [Pasos siguientes](#nextsteps) al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ff97-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="6ff97-129">En el cuadro de diálogo **Nuevo proyecto ASP.NET**, asegúrese de que la opción **Host en la nube** está activada y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="6ff97-130">Si ha no iniciado sesión anteriormente en Azure, se le pedirá que lo haga.</span><span class="sxs-lookup"><span data-stu-id="6ff97-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="6ff97-131">El Asistente para configuración le sugerirá un nombre único basado en *ContactManager* (consulte la imagen siguiente).</span><span class="sxs-lookup"><span data-stu-id="6ff97-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="6ff97-132">Seleccione una región cerca de usted.</span><span class="sxs-lookup"><span data-stu-id="6ff97-132">Select a region near you.</span></span> <span data-ttu-id="6ff97-133">Puede usar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") para buscar el centro de datos de latencia más baja.</span><span class="sxs-lookup"><span data-stu-id="6ff97-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="6ff97-134">Si no ha creado un servidor de base de datos anteriormente, seleccione **Crear nuevo servidor**, escriba un nombre de usuario de base de datos y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="6ff97-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="6ff97-136">Si tiene un servidor de base de datos, úselo para crear una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="6ff97-137">Los servidores de base de datos son un valioso recurso y, por lo general, deseará crear varias bases de datos en el mismo servidor de pruebas y desarrollo en lugar de crear un servidor de base de datos por base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="6ff97-138">Asegúrese de que su sitio web y la base de datos están en la misma región.</span><span class="sxs-lookup"><span data-stu-id="6ff97-138">Make sure your web site and database are in the same region.</span></span>

![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="6ff97-140">Establecimiento del encabezado y pie de página</span><span class="sxs-lookup"><span data-stu-id="6ff97-140">Set the page header and footer</span></span>
1. <span data-ttu-id="6ff97-141">En el **Explorador de soluciones**, expanda la carpeta *Views\Shared* y abra el archivo *_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6ff97-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml en el Explorador de soluciones][newapp004]
2. <span data-ttu-id="6ff97-143">Reemplace el contenido del archivo *Views\Shared_Layout.cshtml* por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ff97-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="6ff97-144">El código anterior cambia el nombre de la aplicación "My ASP.NET App" a "Contact Manager" y quita los vínculos de **Inicio**, **Información** y **Contacto**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="6ff97-145">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="6ff97-145">Run the application locally</span></span>
1. <span data-ttu-id="6ff97-146">Presione CTRL+F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="6ff97-147">Aparece la página principal de la aplicación en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="6ff97-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="6ff97-148">![Página de inicio de lista de tareas pendientes](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="6ff97-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="6ff97-149">Esto es todo lo que necesita hacer por ahora para crear la aplicación que va a implementar en Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff97-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="6ff97-150">Más adelante agregará la funcionalidad de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="6ff97-151">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="6ff97-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="6ff97-152">En Visual Studio, haga clic con el botón derecho en el proyecto, en el **Explorador de soluciones** y seleccione **Publicar** en el menú contextual.</span><span class="sxs-lookup"><span data-stu-id="6ff97-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Opción Publicar del menú contextual del proyecto][PublishVSSolution]
   
    <span data-ttu-id="6ff97-154">Se abre el asistente para **publicación web** .</span><span class="sxs-lookup"><span data-stu-id="6ff97-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="6ff97-155">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-155">Click **Publish**.</span></span>

![Pestaña Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="6ff97-157">Visual Studio comienza el proceso de copiar los archivos en el servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff97-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="6ff97-158">La ventana **Salida** muestra qué acciones de implementación se realizaron e informa de la correcta finalización de la implementación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="6ff97-159">El explorador predeterminado se dirige automáticamente a la URL del sitio web implementado.</span><span class="sxs-lookup"><span data-stu-id="6ff97-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="6ff97-160">La aplicación creada ahora se ejecuta en la nube.</span><span class="sxs-lookup"><span data-stu-id="6ff97-160">The application you created is now running in the cloud.</span></span>
   
   ![Página de inicio de tareas pendientes ejecutándose en Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="6ff97-162">Incorporación de una base de datos a la aplicación</span><span class="sxs-lookup"><span data-stu-id="6ff97-162">Add a database to the application</span></span>
<span data-ttu-id="6ff97-163">A continuación, actualizará la aplicación MVC incorporando funciones que permitan mostrar y actualizar los contactos y almacenar los datos en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="6ff97-164">La aplicación utilizará Entity Framework para crear la base de datos y para leer y actualizar los datos que esta contiene.</span><span class="sxs-lookup"><span data-stu-id="6ff97-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="6ff97-165">Incorporación de clases de modelos de datos para los contactos</span><span class="sxs-lookup"><span data-stu-id="6ff97-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="6ff97-166">Se empieza por crear un modelo de datos sencillo en código.</span><span class="sxs-lookup"><span data-stu-id="6ff97-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="6ff97-167">En el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta Models, a continuación en **Agregar** y, por último, en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Agregar clase en el menú contextual de la carpeta Models][adddb001]
2. <span data-ttu-id="6ff97-169">En el cuadro de diálogo **Agregar nuevo elemento**, ponga al archivo de la nueva clase el nombre *Contact.cs* y, a continuación, haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Cuadro de diálogo Add New Item][adddb002]
3. <span data-ttu-id="6ff97-171">Reemplace el contenido del archivo Contacts.cs por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="6ff97-172">La clase **Contact** define qué datos se almacenarán para cada contacto, así como una clave principal, ContactID, necesaria para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="6ff97-173">Puede obtener más información sobre los modelos de datos en la sección [Pasos siguientes](#nextsteps) al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ff97-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="6ff97-174">Creación de páginas web que permiten a los usuarios de aplicaciones utilizar los contactos</span><span class="sxs-lookup"><span data-stu-id="6ff97-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="6ff97-175">La característica de scaffolding de ASP.NET MVC puede generar automáticamente código que realiza acciones de creación, lectura, actualización y eliminación (CRUD).</span><span class="sxs-lookup"><span data-stu-id="6ff97-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="6ff97-176">Incorporación de un controlador y una vista para los datos</span><span class="sxs-lookup"><span data-stu-id="6ff97-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="6ff97-177">En el **Explorador de soluciones**, expanda la carpeta Controllers.</span><span class="sxs-lookup"><span data-stu-id="6ff97-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="6ff97-178">Creación del proyecto **(Ctrl+Mayús+B)**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="6ff97-179">(Debe crear el proyecto antes de usar el mecanismo de scaffolding).</span><span class="sxs-lookup"><span data-stu-id="6ff97-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="6ff97-180">Haga clic con el botón derecho en la carpeta Controllers, haga clic en **Agregar** y luego en **Controlador**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Agregar controlador en el menú contextual de la carpeta Controllers][addcode001]
4. <span data-ttu-id="6ff97-182">En el cuadro de diálogo **Agregar scaffold**, seleccione **Controlador de MVC con vistas, usando Entity Framework** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Agregar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="6ff97-184">Asigne al controlador el nombre de **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="6ff97-185">Seleccione **Contact** como su clase de modelo.</span><span class="sxs-lookup"><span data-stu-id="6ff97-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="6ff97-186">Haga clic en el botón **Nuevo contexto de datos** y acepte el valor predeterminado "ContactManager.Models.ContactManagerContext" para **Nuevo tipo de contexto de datos**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="6ff97-187">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-187">Click **Add**.</span></span>

    <span data-ttu-id="6ff97-188">Aparecerá un cuadro de diálogo que le indicará que ya existe un archivo con el nombre HomeController.</span><span class="sxs-lookup"><span data-stu-id="6ff97-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="6ff97-189">Do you want to replace it?".</span><span class="sxs-lookup"><span data-stu-id="6ff97-189">Do you want to replace it?".</span></span> <span data-ttu-id="6ff97-190">Haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-190">Click **Yes**.</span></span> <span data-ttu-id="6ff97-191">Estamos sobrescribiendo el controlador de inicio que se creó con el nuevo proyecto.</span><span class="sxs-lookup"><span data-stu-id="6ff97-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="6ff97-192">Utilizaremos el nuevo controlador de inicio para nuestra lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="6ff97-193">Visual Studio crea métodos y vistas de controlador para las operaciones CRUD de base de datos que afectan a los objetos **Contact** .</span><span class="sxs-lookup"><span data-stu-id="6ff97-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="6ff97-194">Habilitación de las migraciones, creación de la base de datos e incorporación de datos de ejemplo y un inicializador de datos</span><span class="sxs-lookup"><span data-stu-id="6ff97-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="6ff97-195">La siguiente tarea consiste en habilitar la característica [Migraciones de Code First](http://curah.microsoft.com/55220) para crear la base de datos a partir del modelo de datos ya establecido.</span><span class="sxs-lookup"><span data-stu-id="6ff97-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="6ff97-196">En el menú **Herramientas**, seleccione **Administrador de paquetes de biblioteca** y, a continuación, **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager Console en el menú Herramientas][addcode008]
2. <span data-ttu-id="6ff97-198">En la ventana **Consola del Administrador de paquetas** , escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6ff97-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="6ff97-199">El comando **enable-migrations** crea una carpeta *Migrations* y guarda en ella un archivo *Configuration.cs* que puede editar para configurar las migraciones.</span><span class="sxs-lookup"><span data-stu-id="6ff97-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="6ff97-200">En la ventana **Consola del Administrador de paquetas** , escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="6ff97-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="6ff97-201">El comando **add-migration Initial** genera una clase denominada **&lt;date_stamp&gt;Initial** que crea la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="6ff97-202">El primer parámetro ( *Initial* ) es arbitrario y se utiliza para crear el nombre del archivo.</span><span class="sxs-lookup"><span data-stu-id="6ff97-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="6ff97-203">Puede ver los archivos de las nuevas clases en el **Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="6ff97-204">En la clase **Initial**, el método **Up** crea la tabla Contacts y el método **Down** (que se utiliza cuando se desea volver al estado anterior) la anula.</span><span class="sxs-lookup"><span data-stu-id="6ff97-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="6ff97-205">Abra el archivo *Migrations\Configuration.cs*.</span><span class="sxs-lookup"><span data-stu-id="6ff97-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="6ff97-206">Agregue los siguientes espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="6ff97-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="6ff97-207">Reemplace el método *Seed* por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ff97-207">Replace the *Seed* method with the following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="6ff97-208">El código anterior inicializará la base de datos con la información de contacto.</span><span class="sxs-lookup"><span data-stu-id="6ff97-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="6ff97-209">Para obtener más información sobre la inicialización de la base de datos, consulte [Depuración de bases de datos de Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ff97-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="6ff97-210">En **Consola del Administrador de paquetes** , escriba el comando:</span><span class="sxs-lookup"><span data-stu-id="6ff97-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Comandos de Package Manager Console][addcode009]
   
    <span data-ttu-id="6ff97-212">El comando **update-database** ejecuta la primera migración, lo que crea la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="6ff97-213">De manera predeterminada, la base de datos que se crea es una base de datos LocalDB de SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="6ff97-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="6ff97-214">Presione CTRL+F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="6ff97-215">La aplicación muestra los datos de inicialización y ofrece enlaces de edición, detalles y eliminación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Vista MVC de los datos][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="6ff97-217">Edición de la vista</span><span class="sxs-lookup"><span data-stu-id="6ff97-217">Edit the View</span></span>
1. <span data-ttu-id="6ff97-218">Abra el archivo *Views\Home\Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="6ff97-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="6ff97-219">En el paso siguiente, reemplazaremos la revisión generada por código que usa [jQuery](http://jquery.com/) y [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="6ff97-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="6ff97-220">Este nuevo código recupera la lista de contactos con la utilización de web API y JSON y, a continuación, enlaza los datos de contacto con la UI mediante knockout.js.</span><span class="sxs-lookup"><span data-stu-id="6ff97-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="6ff97-221">Consulte la sección [Pasos siguientes](#nextsteps) al final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6ff97-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="6ff97-222">Reemplace el contenido del archivo por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-222">Replace the contents of the file with the following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="6ff97-223">Haga clic con el botón derecho en la carpeta Contenido, luego en **Agregar** y, por último, en **Nuevo elemento...**</span><span class="sxs-lookup"><span data-stu-id="6ff97-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Incorporación de una hoja de estilo en el menú contextual de la carpeta Content][addcode005]
4. <span data-ttu-id="6ff97-225">En el cuadro de diálogo **Agregar nuevo elemento**, escriba **Estilo** en el cuadro de búsqueda superior derecho y luego seleccione **Hoja de estilo**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="6ff97-226">![Cuadro de diálogo Agregar nuevo elemento][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="6ff97-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="6ff97-227">Asigne al archivo el nombre *Contacts.css* y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="6ff97-228">Reemplace el contenido del archivo por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-228">Replace the contents of the file with the following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="6ff97-229">Utilizaremos la hoja de estilos para el diseño, los colores y el estilo utilizados en la aplicación del administrador de contactos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="6ff97-230">Abra el archivo *App_Start\BundleConfig.cs*.</span><span class="sxs-lookup"><span data-stu-id="6ff97-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="6ff97-231">Agregue el código siguiente para registrar el complemento [Knockout](http://knockoutjs.com/index.html "KO") .</span><span class="sxs-lookup"><span data-stu-id="6ff97-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="6ff97-232">Este ejemplo utiliza knockout para simplificar el código JavaScript dinámico que trata las plantillas de la pantalla.</span><span class="sxs-lookup"><span data-stu-id="6ff97-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="6ff97-233">Modifique la entrada contents/css para registrar la hoja de estilos *contacts.css* .</span><span class="sxs-lookup"><span data-stu-id="6ff97-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="6ff97-234">Cambie la línea siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ff97-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="6ff97-235">Por:</span><span class="sxs-lookup"><span data-stu-id="6ff97-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="6ff97-236">En Package Manager Console, ejecute el comando siguiente para instalar Knockout.</span><span class="sxs-lookup"><span data-stu-id="6ff97-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="6ff97-237">Incorporación de un controlador para la interfaz Restful de Web API</span><span class="sxs-lookup"><span data-stu-id="6ff97-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="6ff97-238">En el **Explorador de soluciones**, haga clic con el botón derecho en Controladores y haga clic en **Agregar** y luego en **Controlador...**</span><span class="sxs-lookup"><span data-stu-id="6ff97-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="6ff97-239">En el cuadro de diálogo **Agregar scaffold**, escriba **Controlador de Web API 2 con acciones, usando Entity Framework** y luego haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Incorporación de un controlador API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="6ff97-241">En el cuadro de diálogo **Agregar controlador** , escriba "ContactsController" como el nombre de controlador.</span><span class="sxs-lookup"><span data-stu-id="6ff97-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="6ff97-242">Seleccione "Contact (ContactManager.Models)" para la opción **Clase de modelo**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="6ff97-243">Mantenga el valor predeterminado para **Clase de contexto de datos**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="6ff97-244">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="6ff97-245">Ejecución de la aplicación de forma local</span><span class="sxs-lookup"><span data-stu-id="6ff97-245">Run the application locally</span></span>
1. <span data-ttu-id="6ff97-246">Presione CTRL+F5 para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Página de índice][intro001]
2. <span data-ttu-id="6ff97-248">Escriba un contacto y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="6ff97-249">La aplicación regresa a la página de inicio y muestra el contacto que ha introducido.</span><span class="sxs-lookup"><span data-stu-id="6ff97-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Página de índice con elementos de lista de tareas pendientes][addwebapi004]
3. <span data-ttu-id="6ff97-251">En el explorador, anexe **/api/contacts** a la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="6ff97-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="6ff97-252">La URL resultante se parecerá a http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="6ff97-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="6ff97-253">La API web de RESTful que ha agregado devuelve los contactos almacenados.</span><span class="sxs-lookup"><span data-stu-id="6ff97-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="6ff97-254">Firefox y Chrome mostrarán los datos en formato XML.</span><span class="sxs-lookup"><span data-stu-id="6ff97-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Página de índice con elementos de lista de tareas pendientes][rxFFchrome]

    <span data-ttu-id="6ff97-256">Internet Explorer le solicitará que abra o guarde los contactos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-256">IE will prompt you to open or save the contacts.</span></span>

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi006]


    <span data-ttu-id="6ff97-258">Puede abrir los contactos devueltos con el Bloc de notas o en un explorador.</span><span class="sxs-lookup"><span data-stu-id="6ff97-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="6ff97-259">Este resultado lo puede consumir otra aplicación como una página web móvil o aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi007]

    <span data-ttu-id="6ff97-261">**Administración de seguridad**: en este momento, la aplicación es insegura y vulnerable frente un ataque CSRF.</span><span class="sxs-lookup"><span data-stu-id="6ff97-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="6ff97-262">Más adelante en el tutorial eliminaremos esta vulnerabilidad.</span><span class="sxs-lookup"><span data-stu-id="6ff97-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="6ff97-263">Para más información, consulte [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks] (Impedimento de ataques de falsificación de solicitud entre sitios (CSRF)).</span><span class="sxs-lookup"><span data-stu-id="6ff97-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="6ff97-264">Incorporación de protección de XSRF</span><span class="sxs-lookup"><span data-stu-id="6ff97-264">Add XSRF Protection</span></span>
<span data-ttu-id="6ff97-265">La falsificación de solicitud entre sitios (también conocida como XSRF o CSRF) es un ataque contra aplicaciones hospedadas en web, en donde un sitio web malintencionado puede influir en la interacción entre un explorador cliente y un sitio web de confianza de ese explorador.</span><span class="sxs-lookup"><span data-stu-id="6ff97-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="6ff97-266">Estos ataques son posibles porque los exploradores web enviarán tokens de autenticación automáticamente con cada solicitud a un sitio web.</span><span class="sxs-lookup"><span data-stu-id="6ff97-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="6ff97-267">El ejemplo canónico es una cookie de autenticación, como el vale de autenticación de formularios de ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6ff97-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="6ff97-268">Sin embargo, los sitios web que utilicen cualquier mecanismo de autenticación persistente (como Autenticación de Windows, Basic, entre otras) podrían ser objetivos de esos ataques.</span><span class="sxs-lookup"><span data-stu-id="6ff97-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="6ff97-269">Un ataque XSRF es distinto de un ataque de suplantación de identidad (phishing).</span><span class="sxs-lookup"><span data-stu-id="6ff97-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="6ff97-270">Los ataques de suplantación de identidad requieren interacción de la víctima.</span><span class="sxs-lookup"><span data-stu-id="6ff97-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="6ff97-271">En un ataque de suplantación de identidad (phishing), un sitio web malintencionado imitará el sitio web de destino y engañará a la víctima para que proporcione información confidencial al atacante.</span><span class="sxs-lookup"><span data-stu-id="6ff97-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="6ff97-272">En un ataque XSRF, con frecuencia no hay interacción necesaria de la víctima.</span><span class="sxs-lookup"><span data-stu-id="6ff97-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="6ff97-273">Por el contrario, el atacante confía en el explorador enviando automáticamente todas las cookies relevantes al sitio web de destino.</span><span class="sxs-lookup"><span data-stu-id="6ff97-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="6ff97-274">Para más información, consulte [Proyecto de seguridad de aplicación web abierta](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="6ff97-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="6ff97-275">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **ContactManager**, haga clic en **Agregar** y luego en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="6ff97-276">Asigne al archivo el nombre *ValidateHttpAntiForgeryTokenAttribute.cs* y agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="6ff97-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="6ff97-277">Agregue la siguiente instrucción *using* al controlador de contratos para que tenga acceso al atributo **[ValidateHttpAntiForgeryToken]** .</span><span class="sxs-lookup"><span data-stu-id="6ff97-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="6ff97-278">Agregue el atributo **[ValidateHttpAntiForgeryToken]** a los métodos Post de **ContactsController** para protegerlo contra amenazas XSRF.</span><span class="sxs-lookup"><span data-stu-id="6ff97-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="6ff97-279">Lo agregará a los métodos de acciones "PutContact",  "PostContact" y **DeleteContact**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="6ff97-280">Actualice la sección *Scripts* del archivo *Views\Home\Index.cshtml* para incluir código y obtener los tokens de XSRF.</span><span class="sxs-lookup"><span data-stu-id="6ff97-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="6ff97-281">Publicación de la actualización de la aplicación en Azure y la base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="6ff97-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="6ff97-282">Para publicar la aplicación, repita el procedimiento que ha realizado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="6ff97-283">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto y, a continuación, seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publicar][rxP]
2. <span data-ttu-id="6ff97-285">Haga clic en la pestaña **Configuración** .</span><span class="sxs-lookup"><span data-stu-id="6ff97-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="6ff97-286">En **ContactsManagerContext(ContactsManagerContext)**, haga clic en el icono **v** para cambiar la *Cadena de conexión remota* de la cadena de conexión para la base de datos del contacto.</span><span class="sxs-lookup"><span data-stu-id="6ff97-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="6ff97-287">Haga clic en **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-287">Click **ContactDB**.</span></span>
   
    ![Configuración](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="6ff97-289">Active la casilla **Ejecutar migraciones Code First (se ejecuta al iniciar la aplicación)**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="6ff97-290">Haga clic en **Siguiente** y luego en **Vista previa**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="6ff97-291">Visual Studio muestra una lista de los archivos que se agregarán o actualizarán.</span><span class="sxs-lookup"><span data-stu-id="6ff97-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="6ff97-292">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6ff97-292">Click **Publish**.</span></span>
   <span data-ttu-id="6ff97-293">Una vez finalizada la implementación, el explorador se abre por la página de inicio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Página de índice sin contactos][intro001]
   
    <span data-ttu-id="6ff97-295">El proceso de publicación de Visual Studio configura automáticamente la cadena de conexión en el archivo *Web.config* implementado para apuntar a la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="6ff97-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="6ff97-296">También ha configurado las migraciones de Code First para actualizar automáticamente la base de datos a la versión más reciente la primera vez que la aplicación tiene acceso a la base de datos tras la implementación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="6ff97-297">Como resultado de esta configuración, Code First crea la base de datos con la ejecución del código en la clase **Initial** que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="6ff97-298">Lo realizó la primera vez que la aplicación intentó obtener acceso a la base de datos tras la implementación.</span><span class="sxs-lookup"><span data-stu-id="6ff97-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="6ff97-299">Introduzca un contacto de la misma forma que hizo al ejecutar la aplicación localmente, para comprobar que la implementación de la base de datos se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="6ff97-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="6ff97-300">Cuando ve que el elemento introducido se guarda y aparece en la página del administrador de contactos, sabe que se ha almacenado en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Página de índice con contactos][addwebapi004]

<span data-ttu-id="6ff97-302">La aplicación ahora se está ejecutando en la nube, utilizando Base de datos SQL para almacenar sus datos.</span><span class="sxs-lookup"><span data-stu-id="6ff97-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="6ff97-303">Después de finalizar la prueba de la aplicación en Azure, elimínela.</span><span class="sxs-lookup"><span data-stu-id="6ff97-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="6ff97-304">La aplicación es pública y no tiene un mecanismo para limitar el acceso.</span><span class="sxs-lookup"><span data-stu-id="6ff97-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="6ff97-305">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6ff97-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6ff97-306">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="6ff97-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6ff97-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ff97-307">Next Steps</span></span>
<span data-ttu-id="6ff97-308">Otra forma de almacenar datos en una aplicación de Azure consiste en utilizar el almacenamiento de Azure, que ofrece un almacenamiento de datos no relacional en forma de blobs y tablas.</span><span class="sxs-lookup"><span data-stu-id="6ff97-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="6ff97-309">En los vínculos siguientes se proporciona más información sobre Web API, ASP.NET MVC y Azure.</span><span class="sxs-lookup"><span data-stu-id="6ff97-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="6ff97-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial] (Introducción a Entity Framework con MVC)</span><span class="sxs-lookup"><span data-stu-id="6ff97-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="6ff97-311">Introducción a ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="6ff97-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="6ff97-312">Su primer ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6ff97-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="6ff97-313">Depuración de WAWS</span><span class="sxs-lookup"><span data-stu-id="6ff97-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="6ff97-314">Este tutorial y la aplicación de ejemplo fueron desarrollados por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) con la colaboración de Tom Dykstra y Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="6ff97-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="6ff97-315">Es importante que haga comentarios acerca de lo que le gustó o lo que le gustaría que mejorásemos, no solo en relación al tutorial en sí sino a los productos sobre los que trata.</span><span class="sxs-lookup"><span data-stu-id="6ff97-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="6ff97-316">Sus comentarios nos ayudarán a clasificar las mejoras por orden de prioridad.</span><span class="sxs-lookup"><span data-stu-id="6ff97-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="6ff97-317">Estamos especialmente interesados en averiguar el interés que despierta una mayor automatización para el proceso de configurar e implementar la base de datos de suscripciones.</span><span class="sxs-lookup"><span data-stu-id="6ff97-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="6ff97-318">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="6ff97-318">What's changed</span></span>
* <span data-ttu-id="6ff97-319">Para obtener una guía del cambio de Websites a App Service, consulte: [Azure App Service y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6ff97-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

