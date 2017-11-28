---
title: aaaCreate una API de REST de Azure con ASP.NET y la base de datos SQL | Documentos de Microsoft
description: "Un tutorial que le enseña cómo toodeploy una aplicación que usa Hola ASP.NET Web API tooan aplicación web de Azure mediante Visual Studio."
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
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="6e61f-103">Crear un servicio REST con la Web API de ASP.NET y la base de datos SQL en el servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="6e61f-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="6e61f-104">Este tutorial muestra cómo toodeploy un ASP.NET web app tooan [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) mediante el Asistente para la publicación Web de hello en Visual Studio 2013 o Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="6e61f-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="6e61f-105">Puede abrir una cuenta de Azure de forma gratuita y, si ya no tiene Visual Studio 2013, Hola SDK instala automáticamente Visual Studio 2013 para Web Express.</span><span class="sxs-lookup"><span data-stu-id="6e61f-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="6e61f-106">De este modo, puede empezar a desarrollar contenido para Azure sin coste alguno.</span><span class="sxs-lookup"><span data-stu-id="6e61f-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="6e61f-107">En este tutorial se supone que no tiene ninguna experiencia previa con Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="6e61f-108">Al finalizar este tutorial, tendrá una aplicación web simple de la seguridad y la ejecución en nube Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="6e61f-109">Aprenderá a realizar los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="6e61f-109">You'll learn:</span></span>

* <span data-ttu-id="6e61f-110">¿Cómo tooenable Hola a su equipo de desarrollo de Azure mediante la instalación del SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="6e61f-111">¿Cómo toocreate un 5 de MVC de ASP.NET de Visual Studio del proyecto y publíquelo tooan aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="6e61f-112">¿Cómo se llama toouse Hola ASP.NET Web API tooenable API de REST.</span><span class="sxs-lookup"><span data-stu-id="6e61f-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="6e61f-113">Cómo toouse SQL base de datos toostore datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="6e61f-114">Cómo toopublish aplicación actualiza tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="6e61f-115">Podrá crear una aplicación web simple lista de contactos que se basa en ASP.NET MVC 5 y utiliza Hola ADO.NET Entity Framework para el acceso a la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="6e61f-116">Hola siguientes ilustración muestra hello completado aplicación:</span><span class="sxs-lookup"><span data-stu-id="6e61f-116">hello following illustration shows hello completed application:</span></span>

![captura de pantalla de sitio web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="6e61f-118">Crear proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-118">Create hello project</span></span>
1. <span data-ttu-id="6e61f-119">Inicie Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="6e61f-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="6e61f-120">De hello **archivo** menú haga clic en **nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="6e61f-121">Hola **nuevo proyecto** cuadro de diálogo, expanda **Visual C#** y seleccione **Web** y, a continuación, seleccione **aplicación Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="6e61f-122">Nombre de la aplicación hello **ContactManager** y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="6e61f-124">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, seleccione hello **MVC** plantilla, verificación **API Web** y, a continuación, haga clic en **Cambiar autenticación**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="6e61f-125">Hola **Cambiar autenticación** cuadro de diálogo, haga clic en **sin autenticación**y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Sin autenticación](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="6e61f-127">aplicación de ejemplo de Hola que está creando no tiene características que requieren los usuarios toolog en.</span><span class="sxs-lookup"><span data-stu-id="6e61f-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="6e61f-128">Para obtener información acerca de cómo tooimplement las características de autenticación y autorización, consulte hello [pasos](#nextsteps) sección Hola final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e61f-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="6e61f-129">Hola **nuevo proyecto ASP.NET** cuadro de diálogo, hacer seguro hello **Host Hola nube** está activada y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="6e61f-130">Si no se suscribieron anteriormente en tooAzure, es posible que toosign solicitada en.</span><span class="sxs-lookup"><span data-stu-id="6e61f-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="6e61f-131">Asistente para configuración de Hello le sugerirá un nombre único basado en *ContactManager* (vea la imagen de hello siguiente).</span><span class="sxs-lookup"><span data-stu-id="6e61f-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="6e61f-132">Seleccione una región cerca de usted.</span><span class="sxs-lookup"><span data-stu-id="6e61f-132">Select a region near you.</span></span> <span data-ttu-id="6e61f-133">Puede usar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") centro de datos de latencia más baja de toofind Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="6e61f-134">Si no ha creado un servidor de base de datos anteriormente, seleccione **Crear nuevo servidor**, escriba un nombre de usuario de base de datos y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="6e61f-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="6e61f-136">Si tiene un servidor de base de datos, use ese toocreate una nueva base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="6e61f-137">Servidores de base de datos son un recurso muy valioso y, por lo general desea toocreate varias bases de datos en hello mismo servidor de pruebas y desarrollo en lugar de crear un servidor de base de datos por base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="6e61f-138">Asegúrese de que el sitio web y la base de datos están en hello misma región.</span><span class="sxs-lookup"><span data-stu-id="6e61f-138">Make sure your web site and database are in hello same region.</span></span>

![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="6e61f-140">Conjunto Hola encabezado y pie de página</span><span class="sxs-lookup"><span data-stu-id="6e61f-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="6e61f-141">En **el Explorador de soluciones**, expanda hello *Views\Shared* hello abierto y la carpeta *_Layout.cshtml* archivo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml en el Explorador de soluciones][newapp004]
2. <span data-ttu-id="6e61f-143">Reemplazar contenido Hola de hello *Views\Shared_Layout.cshtml* archivo con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="6e61f-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

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

<span data-ttu-id="6e61f-144">marcado de Hello anteriormente cambia el nombre de aplicación desde "Mi aplicación de ASP.NET" hello demasiado "Póngase en contacto con el administrador" y lo quita Hola vínculos demasiado**inicio**, **sobre** y **póngase en contacto con**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="6e61f-145">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="6e61f-145">Run hello application locally</span></span>
1. <span data-ttu-id="6e61f-146">Presione la aplicación de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="6e61f-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="6e61f-147">página de inicio de aplicación Hola aparece en explorador predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="6e61f-148">![página principal de tooDo lista](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="6e61f-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="6e61f-149">Esto es todo lo que necesita toodo para aplicación de hello toocreate ahora que va a implementar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="6e61f-150">Más adelante agregará la funcionalidad de base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="6e61f-151">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="6e61f-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="6e61f-152">En Visual Studio, haga clic en proyecto de hello en **el Explorador de soluciones** y seleccione **publicar** desde el menú contextual de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Opción Publicar del menú contextual del proyecto][PublishVSSolution]
   
    <span data-ttu-id="6e61f-154">Hola **Publicar Web** abre el asistente.</span><span class="sxs-lookup"><span data-stu-id="6e61f-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="6e61f-155">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-155">Click **Publish**.</span></span>

![Pestaña Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="6e61f-157">Visual Studio comienza el proceso de Hola de copiar archivos de hello toohello servidor de Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="6e61f-158">Hola **salida** ventana muestra qué acciones de implementación se realizaron y notifica la finalización correcta de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="6e61f-159">explorador predeterminado de Hola abre automáticamente toohello URL del sitio de hello implementado.</span><span class="sxs-lookup"><span data-stu-id="6e61f-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="6e61f-160">aplicación Hola que ha creado ahora se está ejecutando en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-160">hello application you created is now running in hello cloud.</span></span>
   
   ![página de inicio de lista tooDo ejecuta en Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="6e61f-162">Agregar una aplicación de base de datos toohello</span><span class="sxs-lookup"><span data-stu-id="6e61f-162">Add a database toohello application</span></span>
<span data-ttu-id="6e61f-163">A continuación, podrá actualizar Hola MVC aplicación tooadd Hola capacidad toodisplay y actualizar los contactos y almacenar datos de hello en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="6e61f-164">aplicación Hello usará tooread y base de datos de hello Entity Framework toocreate hello y actualizar los datos de la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="6e61f-165">Agregar clases del modelo de datos para los contactos de Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="6e61f-166">Se empieza por crear un modelo de datos sencillo en código.</span><span class="sxs-lookup"><span data-stu-id="6e61f-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="6e61f-167">En **el Explorador de soluciones**, haga clic en carpeta de modelos de hello, haga clic en **agregar**y, a continuación, **clase**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Agregar clase en el menú contextual de la carpeta Models][adddb001]
2. <span data-ttu-id="6e61f-169">Hola **Agregar nuevo elemento** cuadro de diálogo, el nuevo archivo de clase de nombre hello *Contact.cs*y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Cuadro de diálogo Add New Item][adddb002]
3. <span data-ttu-id="6e61f-171">Reemplace el contenido de Hola de archivo de hello Contacts.cs con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="6e61f-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
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

<span data-ttu-id="6e61f-172">Hola **póngase en contacto con** clase define los datos de Hola que va a almacenar para cada contacto, además de una clave principal, ContactID, que es necesaria para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="6e61f-173">Puede obtener más información acerca de los modelos de datos en hello [pasos](#nextsteps) sección Hola final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e61f-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="6e61f-174">Crear páginas web que permiten toowork de los usuarios de aplicación con los contactos de Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="6e61f-175">Hello característica scaffolding de ASP.NET MVC Hola puedan generar automáticamente código que realiza crear, leer, actualizar y eliminar acciones (CRUD).</span><span class="sxs-lookup"><span data-stu-id="6e61f-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="6e61f-176">Agregar un controlador y una vista de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="6e61f-177">En **el Explorador de soluciones**, expanda la carpeta de controladores de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="6e61f-178">Compile el proyecto de hello **(Ctrl + Mayús + B)**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="6e61f-179">(Debe generar el proyecto de hello antes de usar el mecanismo de scaffolding.)</span><span class="sxs-lookup"><span data-stu-id="6e61f-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="6e61f-180">Haga clic en carpeta de controladores de Hola y haga clic en **agregar**y, a continuación, haga clic en **controlador**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Agregar controlador en el menú contextual de la carpeta Controllers][addcode001]
4. <span data-ttu-id="6e61f-182">Hola **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC con vistas que usan Entity Framework** y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Agregar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="6e61f-184">Establece el nombre del controlador de hello demasiado**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="6e61f-185">Seleccione **Contact** como su clase de modelo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="6e61f-186">Haga clic en hello **nuevo contexto de datos** botón y acepte el valor predeterminado Hola "ContactManager.Models.ContactManagerContext" para hello **nuevo tipo de contexto de datos**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="6e61f-187">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-187">Click **Add**.</span></span>

    <span data-ttu-id="6e61f-188">Un cuadro de diálogo le pedirá que: "un archivo con nombre hello HomeController ya existe.</span><span class="sxs-lookup"><span data-stu-id="6e61f-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="6e61f-189">¿Desea tooreplace lo? ".</span><span class="sxs-lookup"><span data-stu-id="6e61f-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="6e61f-190">Haga clic en **Sí**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-190">Click **Yes**.</span></span> <span data-ttu-id="6e61f-191">Se está sobrescribiendo Hola controlador Home que se creó con el nuevo proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="6e61f-192">Usaremos Hola nuevo inicio controlador para nuestra lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="6e61f-193">Visual Studio crea métodos y vistas de controlador para las operaciones CRUD de base de datos que afectan a los objetos **Contact** .</span><span class="sxs-lookup"><span data-stu-id="6e61f-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="6e61f-194">Habilitar las migraciones, crear base de datos de hello, agregar datos de ejemplo y un inicializador de datos</span><span class="sxs-lookup"><span data-stu-id="6e61f-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="6e61f-195">Hola siguiente tarea es hello tooenable [migraciones de Code First](http://curah.microsoft.com/55220) característica de base de datos de pedido toocreate Hola basado en hello data model que creó.</span><span class="sxs-lookup"><span data-stu-id="6e61f-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="6e61f-196">Hola **herramientas** menú, seleccione **Administrador de paquetes de biblioteca** y, a continuación, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Package Manager Console en el menú Herramientas][addcode008]
2. <span data-ttu-id="6e61f-198">Hola **Package Manager Console** ventana, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="6e61f-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="6e61f-199">Hola **enable-migrations** comando crea un *migraciones* carpeta y lo coloca en esa carpeta una *archivo Configuration.cs que* archivos que se pueden editar tooconfigure migraciones.</span><span class="sxs-lookup"><span data-stu-id="6e61f-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="6e61f-200">Hola **Package Manager Console** ventana, escriba el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="6e61f-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="6e61f-201">Hola **inicial de migración agregar** comando genera una clase denominada  **&lt;date_stamp&gt;inicial** que crea la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="6e61f-202">Hola primer parámetro ( *inicial* ) es toocreate arbitrario y se utiliza Hola nombre de archivo hello.</span><span class="sxs-lookup"><span data-stu-id="6e61f-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="6e61f-203">Puede ver los nuevos archivos de clase hello en **el Explorador de soluciones**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="6e61f-204">Hola **inicial** clase hello **una** método crea la tabla de contactos de Hola y Hola **hacia abajo** lo coloca (método) (se utiliza cuando se desea estado anterior de tooreturn toohello).</span><span class="sxs-lookup"><span data-stu-id="6e61f-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="6e61f-205">Abra hello *Migrations\Configuration.cs* archivo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="6e61f-206">Agregar Hola después de los espacios de nombres.</span><span class="sxs-lookup"><span data-stu-id="6e61f-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="6e61f-207">Reemplace hello *inicialización* método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="6e61f-207">Replace hello *Seed* method with hello following code:</span></span>
   
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
   
    <span data-ttu-id="6e61f-208">Este código anterior inicializará en base de datos de hello con información de contacto de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="6e61f-209">Para obtener más información sobre la base de datos de Hola la propagación, vea [bases de datos de depuración de Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e61f-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="6e61f-210">Hola **Package Manager Console** escriba Hola comando:</span><span class="sxs-lookup"><span data-stu-id="6e61f-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Comandos de Package Manager Console][addcode009]
   
    <span data-ttu-id="6e61f-212">Hola **Actualizar base de datos** ejecuciones Hola primera migración que crea la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="6e61f-213">De forma predeterminada, se crea la base de datos de hello como una base de datos de SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="6e61f-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="6e61f-214">Presione la aplicación de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="6e61f-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="6e61f-215">aplicación Hello muestra datos de valor de inicialización de Hola y proporciona editar información detallada y vínculos de eliminación.</span><span class="sxs-lookup"><span data-stu-id="6e61f-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Vista MVC de los datos][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="6e61f-217">Editar vista de Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-217">Edit hello View</span></span>
1. <span data-ttu-id="6e61f-218">Abra hello *Views\Home\Index.cshtml* archivo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="6e61f-219">En el paso siguiente de hello, se reemplazará marcado Hola generado con el código que usa [jQuery](http://jquery.com/) y [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="6e61f-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="6e61f-220">Este nuevo código recupera la lista de Hola de contactos del uso de API web y enlaza hello JSON y, a continuación, póngase en contacto con datos toohello interfaz de usuario mediante knockout.js.</span><span class="sxs-lookup"><span data-stu-id="6e61f-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="6e61f-221">Para obtener más información, vea hello [pasos](#nextsteps) sección Hola final de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e61f-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="6e61f-222">Reemplace el contenido de hello del archivo hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="6e61f-222">Replace hello contents of hello file with hello following code.</span></span>
   
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
3. <span data-ttu-id="6e61f-223">Haga clic en carpeta de contenido de Hola y haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento...** .</span><span class="sxs-lookup"><span data-stu-id="6e61f-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Incorporación de una hoja de estilo en el menú contextual de la carpeta Content][addcode005]
4. <span data-ttu-id="6e61f-225">Hola **Agregar nuevo elemento** diálogo cuadro, escriba **estilo** en Hola cuadro de búsqueda de derecho superior y, a continuación, seleccione **hoja de estilos**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="6e61f-226">![Cuadro de diálogo Add New Item][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="6e61f-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="6e61f-227">Archivo de nombre hello *Contacts.css* y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="6e61f-228">Reemplace el contenido de hello del archivo hello con hello siguiente código.</span><span class="sxs-lookup"><span data-stu-id="6e61f-228">Replace hello contents of hello file with hello following code.</span></span>
   
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
   
    <span data-ttu-id="6e61f-229">Usaremos esta hoja de estilos de diseño de hello, colores y estilos utilizados en la aplicación de administrador de contactos de hello.</span><span class="sxs-lookup"><span data-stu-id="6e61f-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="6e61f-230">Abra hello *App_Start\BundleConfig.cs* archivo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="6e61f-231">Agregar Hola después Hola de código tooregister [Knockout](http://knockoutjs.com/index.html "KO") complemento.</span><span class="sxs-lookup"><span data-stu-id="6e61f-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="6e61f-232">Este ejemplo con knockout toosimplify dinámica código JavaScript que controla las plantillas de pantalla de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="6e61f-233">Modificar Hola de hello contenido/css entrada tooregister *contacts.css* hoja de estilos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="6e61f-234">Hola de cambio después de línea:</span><span class="sxs-lookup"><span data-stu-id="6e61f-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="6e61f-235">Por:</span><span class="sxs-lookup"><span data-stu-id="6e61f-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="6e61f-236">Hola Package Manager Console, ejecute hello después comando tooinstall Knockout.</span><span class="sxs-lookup"><span data-stu-id="6e61f-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="6e61f-237">Agregar un controlador para la interfaz Web API Restful Hola</span><span class="sxs-lookup"><span data-stu-id="6e61f-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="6e61f-238">En el **Explorador de soluciones**, haga clic con el botón derecho en Controladores y haga clic en **Agregar** y luego en **Controlador...**</span><span class="sxs-lookup"><span data-stu-id="6e61f-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="6e61f-239">Hola **agregar scaffolding** diálogo cuadro, escriba **Web API 2 controlador con acciones que usan Entity Framework** y, a continuación, haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Incorporación de un controlador API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="6e61f-241">Hola **Agregar controlador** diálogo cuadro, escriba "ContactsController" como el nombre del controlador.</span><span class="sxs-lookup"><span data-stu-id="6e61f-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="6e61f-242">Seleccione "Póngase en contacto con (ContactManager.Models)" para hello **clase modelo**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="6e61f-243">Mantener valor predeterminado de Hola para hello **clase de contexto de datos**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="6e61f-244">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="6e61f-245">Ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="6e61f-245">Run hello application locally</span></span>
1. <span data-ttu-id="6e61f-246">Presione la aplicación de hello toorun CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="6e61f-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Página de índice][intro001]
2. <span data-ttu-id="6e61f-248">Escriba un contacto y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="6e61f-249">aplicación Hello devuelve una página de inicio de toohello y muestra contacto Hola especificado.</span><span class="sxs-lookup"><span data-stu-id="6e61f-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Página de índice con elementos de lista de tareas pendientes][addwebapi004]
3. <span data-ttu-id="6e61f-251">En el Explorador de hello, anexar **/api/contactos** toohello URL.</span><span class="sxs-lookup"><span data-stu-id="6e61f-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="6e61f-252">dirección URL de Hello resultante tendrá un aspecto similar http://localhost:1234/api/contactos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="6e61f-253">web RESTful Hola API agregó devuelve contactos Hola almacenado.</span><span class="sxs-lookup"><span data-stu-id="6e61f-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="6e61f-254">Firefox y Chrome mostrará datos de hello en formato XML.</span><span class="sxs-lookup"><span data-stu-id="6e61f-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Página de índice con elementos de lista de tareas pendientes][rxFFchrome]

    <span data-ttu-id="6e61f-256">Internet Explorer se le pedirá que tooopen o guardar contactos Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi006]


    <span data-ttu-id="6e61f-258">Puede abrir Hola devuelve contactos en el Bloc de notas o en un explorador.</span><span class="sxs-lookup"><span data-stu-id="6e61f-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="6e61f-259">Este resultado lo puede consumir otra aplicación como una página web móvil o aplicación.</span><span class="sxs-lookup"><span data-stu-id="6e61f-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi007]

    <span data-ttu-id="6e61f-261">**Advertencia de seguridad**: en este punto, la aplicación es inseguro y sea vulnerable tooCSRF ataque.</span><span class="sxs-lookup"><span data-stu-id="6e61f-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="6e61f-262">Más adelante en el tutorial Hola se quitará esta vulnerabilidad.</span><span class="sxs-lookup"><span data-stu-id="6e61f-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="6e61f-263">Para más información, consulte [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks] (Impedimento de ataques de falsificación de solicitud entre sitios (CSRF)).</span><span class="sxs-lookup"><span data-stu-id="6e61f-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="6e61f-264">Incorporación de protección de XSRF</span><span class="sxs-lookup"><span data-stu-id="6e61f-264">Add XSRF Protection</span></span>
<span data-ttu-id="6e61f-265">Falsificación de solicitud entre sitios (también conocido como XSRF o CSRF) es un ataque contra las aplicaciones hospedadas en web mediante el cual un sitio Web malintencionado puede influir en la interacción de hello entre un explorador del cliente y un sitio Web de confianza para ese explorador.</span><span class="sxs-lookup"><span data-stu-id="6e61f-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="6e61f-266">Estos ataques se realizan porque los exploradores web enviará los tokens de autenticación automáticamente con cada sitio Web tooa de solicitud.</span><span class="sxs-lookup"><span data-stu-id="6e61f-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="6e61f-267">ejemplo de Hola canónico es una cookie de autenticación, como ASP. Vale de autenticación de formularios de NET.</span><span class="sxs-lookup"><span data-stu-id="6e61f-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="6e61f-268">Sin embargo, los sitios web que utilicen cualquier mecanismo de autenticación persistente (como Autenticación de Windows, Basic, entre otras) podrían ser objetivos de esos ataques.</span><span class="sxs-lookup"><span data-stu-id="6e61f-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="6e61f-269">Un ataque XSRF es distinto de un ataque de suplantación de identidad (phishing).</span><span class="sxs-lookup"><span data-stu-id="6e61f-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="6e61f-270">Ataques de suplantación de identidad requieren interacción por parte del sujeto Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="6e61f-271">En un ataque de suplantación de identidad, un sitio Web malintencionado imiten el sitio Web de destino de Hola y víctima de hello es engañada para proporcionar el atacante toohello de información confidencial.</span><span class="sxs-lookup"><span data-stu-id="6e61f-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="6e61f-272">En un ataque XSRF, no suele haber ninguna interacción necesarios de la víctima Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="6e61f-273">En su lugar, el atacante de hello depende explorador Hola enviar automáticamente todos los sitios Web de destino de toohello cookies relevante.</span><span class="sxs-lookup"><span data-stu-id="6e61f-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="6e61f-274">Para obtener más información, vea hello [Abrir proyecto de seguridad de aplicación Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="6e61f-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="6e61f-275">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **ContactManager**, haga clic en **Agregar** y luego en **Clase**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="6e61f-276">Archivo de nombre hello *ValidateHttpAntiForgeryTokenAttribute.cs* y agregue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="6e61f-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
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
3. <span data-ttu-id="6e61f-277">Agregue Hola siguiente *con* toohello instrucción contratos controlador, por lo que tendrá acceso toohello **[ValidateHttpAntiForgeryToken]** atributo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="6e61f-278">Agregar hello **[ValidateHttpAntiForgeryToken]** atributo toohello métodos de entrada de hello **ContactsController** tooprotect, frente a amenazas XSRF.</span><span class="sxs-lookup"><span data-stu-id="6e61f-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="6e61f-279">Va a agregar toohello "PutContact", "PostContact" y **DeleteContact** métodos de acción.</span><span class="sxs-lookup"><span data-stu-id="6e61f-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="6e61f-280">Hola de actualización *Scripts* sección de hello *Views\Home\Index.cshtml* tooinclude código tooget hello XSRF símbolos (tokens) de archivos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="6e61f-281">Publicar tooAzure de actualización de aplicación Hola y de base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="6e61f-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="6e61f-282">aplicación de hello toopublish, repita procedimiento Hola que ha seguido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6e61f-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="6e61f-283">En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publicar][rxP]
2. <span data-ttu-id="6e61f-285">Haga clic en hello **configuración** ficha.</span><span class="sxs-lookup"><span data-stu-id="6e61f-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="6e61f-286">En **ContactsManagerContext(ContactsManagerContext)**, haga clic en hello **v** icono toochange *cadena de conexión remota* toohello de cadena de conexión para el contacto de Hola base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="6e61f-287">Haga clic en **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-287">Click **ContactDB**.</span></span>
   
    ![Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="6e61f-289">Casilla de Hola para **ejecutar migraciones de Code First (se ejecuta al iniciarse la aplicación)**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="6e61f-290">Haga clic en **Siguiente** y luego en **Vista previa**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="6e61f-291">Visual Studio muestra una lista de archivos de Hola que se agregaron o actualizaron.</span><span class="sxs-lookup"><span data-stu-id="6e61f-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="6e61f-292">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="6e61f-292">Click **Publish**.</span></span>
   <span data-ttu-id="6e61f-293">Una vez finalizada la implementación de hello, abre el Explorador de hello toohello página de inicio de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="6e61f-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Página de índice sin contactos][intro001]
   
    <span data-ttu-id="6e61f-295">Hola Visual Studio publicar cadena de conexión de proceso que se configuran automáticamente Hola Hola implementado *Web.config* archivo toopoint toohello base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="6e61f-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="6e61f-296">También configura migraciones de Code First tooautomatically Hola Actualizar base de datos toohello última versión primera aplicación de hello tiempo hello tiene acceso a la base de datos de hello después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="6e61f-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="6e61f-297">Como resultado de esta configuración, Code First creado Hola base de datos mediante la ejecución de código de hello en hello **inicial** clase que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="6e61f-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="6e61f-298">Lo hacía esta Hola primera hora Hola aplicación intentó tooaccess Hola base de datos después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="6e61f-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="6e61f-299">Escriba un contacto como lo hizo cuando se ejecuta la aplicación de hello localmente, tooverify que se ha realizado correctamente en la implementación de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="6e61f-300">Cuando aparezca ese elemento de Hola que escriba se guarda y aparece en la página del Administrador de contacto de hello, sabrá que se han almacenado en la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Página de índice con contactos][addwebapi004]

<span data-ttu-id="6e61f-302">aplicación Hello está ejecutando ahora en nube hello, mediante toostore de base de datos SQL sus datos.</span><span class="sxs-lookup"><span data-stu-id="6e61f-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="6e61f-303">Cuando termine de probar la aplicación hello en Azure, elimínelo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="6e61f-304">aplicación Hello es público y no tiene un acceso de toolimit mecanismo.</span><span class="sxs-lookup"><span data-stu-id="6e61f-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="6e61f-305">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6e61f-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6e61f-306">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="6e61f-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6e61f-307">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6e61f-307">Next Steps</span></span>
<span data-ttu-id="6e61f-308">Otra forma que toostore los datos en una aplicación de Azure están toouse almacenamiento de Azure, que proporcionan almacenamiento de datos no relacionales en forma de Hola de blobs y tablas.</span><span class="sxs-lookup"><span data-stu-id="6e61f-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="6e61f-309">Hola siguientes vínculos proporciona más información acerca la API Web, ASP.NET MVC y Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="6e61f-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="6e61f-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial] (Introducción a Entity Framework con MVC)</span><span class="sxs-lookup"><span data-stu-id="6e61f-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="6e61f-311">Introducción tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="6e61f-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="6e61f-312">Su primer ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="6e61f-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="6e61f-313">Depuración de WAWS</span><span class="sxs-lookup"><span data-stu-id="6e61f-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="6e61f-314">Esta aplicación de ejemplo hello y tutorial se escribió por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) con la asistencia de Tom Dykstra y Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="6e61f-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="6e61f-315">Por favor, votar en qué le gustó o lo que le gustaría toosee mejorado, no solo acerca del tutorial de hello propio, sino también acerca de los productos de Hola que muestra.</span><span class="sxs-lookup"><span data-stu-id="6e61f-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="6e61f-316">Sus comentarios nos ayudarán a clasificar las mejoras por orden de prioridad.</span><span class="sxs-lookup"><span data-stu-id="6e61f-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="6e61f-317">Estamos especialmente interesados en Buscar es cuánto interés no existe en la automatización más para el proceso de Hola de configurar e implementar la base de datos de pertenencia de Hola.</span><span class="sxs-lookup"><span data-stu-id="6e61f-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="6e61f-318">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="6e61f-318">What's changed</span></span>
* <span data-ttu-id="6e61f-319">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6e61f-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
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

