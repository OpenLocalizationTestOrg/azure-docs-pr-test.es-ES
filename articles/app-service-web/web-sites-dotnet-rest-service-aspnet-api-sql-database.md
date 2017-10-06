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
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a>Crear un servicio REST con la Web API de ASP.NET y la base de datos SQL en el servicio de aplicaciones de Azure
Este tutorial muestra cómo toodeploy un ASP.NET web app tooan [servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714) mediante el Asistente para la publicación Web de hello en Visual Studio 2013 o Visual Studio 2013 Community Edition. 

Puede abrir una cuenta de Azure de forma gratuita y, si ya no tiene Visual Studio 2013, Hola SDK instala automáticamente Visual Studio 2013 para Web Express. De este modo, puede empezar a desarrollar contenido para Azure sin coste alguno.

En este tutorial se supone que no tiene ninguna experiencia previa con Azure. Al finalizar este tutorial, tendrá una aplicación web simple de la seguridad y la ejecución en nube Hola.

Aprenderá a realizar los siguientes procedimientos:

* ¿Cómo tooenable Hola a su equipo de desarrollo de Azure mediante la instalación del SDK de Azure.
* ¿Cómo toocreate un 5 de MVC de ASP.NET de Visual Studio del proyecto y publíquelo tooan aplicación de Azure.
* ¿Cómo se llama toouse Hola ASP.NET Web API tooenable API de REST.
* Cómo toouse SQL base de datos toostore datos en Azure.
* Cómo toopublish aplicación actualiza tooAzure.

Podrá crear una aplicación web simple lista de contactos que se basa en ASP.NET MVC 5 y utiliza Hola ADO.NET Entity Framework para el acceso a la base de datos. Hola siguientes ilustración muestra hello completado aplicación:

![captura de pantalla de sitio web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a>Crear proyecto de Hola
1. Inicie Visual Studio 2013.
2. De hello **archivo** menú haga clic en **nuevo proyecto**.
3. Hola **nuevo proyecto** cuadro de diálogo, expanda **Visual C#** y seleccione **Web** y, a continuación, seleccione **aplicación Web ASP.NET**. Nombre de la aplicación hello **ContactManager** y haga clic en **Aceptar**.
   
    ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, seleccione hello **MVC** plantilla, verificación **API Web** y, a continuación, haga clic en **Cambiar autenticación**.
5. Hola **Cambiar autenticación** cuadro de diálogo, haga clic en **sin autenticación**y, a continuación, haga clic en **Aceptar**.
   
    ![Sin autenticación](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    aplicación de ejemplo de Hola que está creando no tiene características que requieren los usuarios toolog en. Para obtener información acerca de cómo tooimplement las características de autenticación y autorización, consulte hello [pasos](#nextsteps) sección Hola final de este tutorial. 
6. Hola **nuevo proyecto ASP.NET** cuadro de diálogo, hacer seguro hello **Host Hola nube** está activada y haga clic en **Aceptar**.

Si no se suscribieron anteriormente en tooAzure, es posible que toosign solicitada en.

1. Asistente para configuración de Hello le sugerirá un nombre único basado en *ContactManager* (vea la imagen de hello siguiente). Seleccione una región cerca de usted. Puede usar [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") centro de datos de latencia más baja de toofind Hola. 
2. Si no ha creado un servidor de base de datos anteriormente, seleccione **Crear nuevo servidor**, escriba un nombre de usuario de base de datos y la contraseña.
   
    ![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

Si tiene un servidor de base de datos, use ese toocreate una nueva base de datos. Servidores de base de datos son un recurso muy valioso y, por lo general desea toocreate varias bases de datos en hello mismo servidor de pruebas y desarrollo en lugar de crear un servidor de base de datos por base de datos. Asegúrese de que el sitio web y la base de datos están en hello misma región.

![Configuración de Sitio web de Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a>Conjunto Hola encabezado y pie de página
1. En **el Explorador de soluciones**, expanda hello *Views\Shared* hello abierto y la carpeta *_Layout.cshtml* archivo.
   
    ![_Layout.cshtml en el Explorador de soluciones][newapp004]
2. Reemplazar contenido Hola de hello *Views\Shared_Layout.cshtml* archivo con el siguiente código de hello:

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

marcado de Hello anteriormente cambia el nombre de aplicación desde "Mi aplicación de ASP.NET" hello demasiado "Póngase en contacto con el administrador" y lo quita Hola vínculos demasiado**inicio**, **sobre** y **póngase en contacto con**.

### <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
1. Presione la aplicación de hello toorun CTRL + F5.
   página de inicio de aplicación Hola aparece en explorador predeterminado de Hola.
    ![página principal de tooDo lista](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)

Esto es todo lo que necesita toodo para aplicación de hello toocreate ahora que va a implementar tooAzure. Más adelante agregará la funcionalidad de base de datos.

## <a name="deploy-hello-application-tooazure"></a>Implementar Hola aplicación tooAzure
1. En Visual Studio, haga clic en proyecto de hello en **el Explorador de soluciones** y seleccione **publicar** desde el menú contextual de Hola.
   
    ![Opción Publicar del menú contextual del proyecto][PublishVSSolution]
   
    Hola **Publicar Web** abre el asistente.
2. Haga clic en **Publicar**.

![Pestaña Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

Visual Studio comienza el proceso de Hola de copiar archivos de hello toohello servidor de Azure. Hola **salida** ventana muestra qué acciones de implementación se realizaron y notifica la finalización correcta de la implementación de Hola.

1. explorador predeterminado de Hola abre automáticamente toohello URL del sitio de hello implementado.
   
   aplicación Hola que ha creado ahora se está ejecutando en la nube de Hola.
   
   ![página de inicio de lista tooDo ejecuta en Azure][rxz2]

## <a name="add-a-database-toohello-application"></a>Agregar una aplicación de base de datos toohello
A continuación, podrá actualizar Hola MVC aplicación tooadd Hola capacidad toodisplay y actualizar los contactos y almacenar datos de hello en una base de datos. aplicación Hello usará tooread y base de datos de hello Entity Framework toocreate hello y actualizar los datos de la base de datos de Hola.

### <a name="add-data-model-classes-for-hello-contacts"></a>Agregar clases del modelo de datos para los contactos de Hola
Se empieza por crear un modelo de datos sencillo en código.

1. En **el Explorador de soluciones**, haga clic en carpeta de modelos de hello, haga clic en **agregar**y, a continuación, **clase**.
   
    ![Agregar clase en el menú contextual de la carpeta Models][adddb001]
2. Hola **Agregar nuevo elemento** cuadro de diálogo, el nuevo archivo de clase de nombre hello *Contact.cs*y, a continuación, haga clic en **agregar**.
   
    ![Cuadro de diálogo Add New Item][adddb002]
3. Reemplace el contenido de Hola de archivo de hello Contacts.cs con el siguiente código de hello.
   
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

Hola **póngase en contacto con** clase define los datos de Hola que va a almacenar para cada contacto, además de una clave principal, ContactID, que es necesaria para la base de datos de Hola. Puede obtener más información acerca de los modelos de datos en hello [pasos](#nextsteps) sección Hola final de este tutorial.

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a>Crear páginas web que permiten toowork de los usuarios de aplicación con los contactos de Hola
Hello característica scaffolding de ASP.NET MVC Hola puedan generar automáticamente código que realiza crear, leer, actualizar y eliminar acciones (CRUD).

## <a name="add-a-controller-and-a-view-for-hello-data"></a>Agregar un controlador y una vista de datos de Hola
1. En **el Explorador de soluciones**, expanda la carpeta de controladores de Hola.
2. Compile el proyecto de hello **(Ctrl + Mayús + B)**. (Debe generar el proyecto de hello antes de usar el mecanismo de scaffolding.) 
3. Haga clic en carpeta de controladores de Hola y haga clic en **agregar**y, a continuación, haga clic en **controlador**.
   
    ![Agregar controlador en el menú contextual de la carpeta Controllers][addcode001]
4. Hola **agregar scaffolding** cuadro de diálogo, seleccione **controlador de MVC con vistas que usan Entity Framework** y haga clic en **agregar**.
   
   ![Agregar controlador](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. Establece el nombre del controlador de hello demasiado**HomeController**. Seleccione **Contact** como su clase de modelo. Haga clic en hello **nuevo contexto de datos** botón y acepte el valor predeterminado Hola "ContactManager.Models.ContactManagerContext" para hello **nuevo tipo de contexto de datos**. Haga clic en **Agregar**.

    Un cuadro de diálogo le pedirá que: "un archivo con nombre hello HomeController ya existe. ¿Desea tooreplace lo? ". Haga clic en **Sí**. Se está sobrescribiendo Hola controlador Home que se creó con el nuevo proyecto de Hola. Usaremos Hola nuevo inicio controlador para nuestra lista de contactos.

    Visual Studio crea métodos y vistas de controlador para las operaciones CRUD de base de datos que afectan a los objetos **Contact** .

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a>Habilitar las migraciones, crear base de datos de hello, agregar datos de ejemplo y un inicializador de datos
Hola siguiente tarea es hello tooenable [migraciones de Code First](http://curah.microsoft.com/55220) característica de base de datos de pedido toocreate Hola basado en hello data model que creó.

1. Hola **herramientas** menú, seleccione **Administrador de paquetes de biblioteca** y, a continuación, **Package Manager Console**.
   
    ![Package Manager Console en el menú Herramientas][addcode008]
2. Hola **Package Manager Console** ventana, escriba el siguiente comando de hello:
   
        enable-migrations 
   
    Hola **enable-migrations** comando crea un *migraciones* carpeta y lo coloca en esa carpeta una *archivo Configuration.cs que* archivos que se pueden editar tooconfigure migraciones. 
3. Hola **Package Manager Console** ventana, escriba el siguiente comando de hello:
   
        add-migration Initial
   
    Hola **inicial de migración agregar** comando genera una clase denominada  **&lt;date_stamp&gt;inicial** que crea la base de datos de Hola. Hola primer parámetro ( *inicial* ) es toocreate arbitrario y se utiliza Hola nombre de archivo hello. Puede ver los nuevos archivos de clase hello en **el Explorador de soluciones**.
   
    Hola **inicial** clase hello **una** método crea la tabla de contactos de Hola y Hola **hacia abajo** lo coloca (método) (se utiliza cuando se desea estado anterior de tooreturn toohello).
4. Abra hello *Migrations\Configuration.cs* archivo. 
5. Agregar Hola después de los espacios de nombres. 
   
         using ContactManager.Models;
6. Reemplace hello *inicialización* método con el siguiente código de hello:
   
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
   
    Este código anterior inicializará en base de datos de hello con información de contacto de Hola. Para obtener más información sobre la base de datos de Hola la propagación, vea [bases de datos de depuración de Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).
7. Hola **Package Manager Console** escriba Hola comando:
   
        update-database
   
    ![Comandos de Package Manager Console][addcode009]
   
    Hola **Actualizar base de datos** ejecuciones Hola primera migración que crea la base de datos de Hola. De forma predeterminada, se crea la base de datos de hello como una base de datos de SQL Server Express LocalDB.
8. Presione la aplicación de hello toorun CTRL + F5. 

aplicación Hello muestra datos de valor de inicialización de Hola y proporciona editar información detallada y vínculos de eliminación.

![Vista MVC de los datos][rxz3]

## <a name="edit-hello-view"></a>Editar vista de Hola
1. Abra hello *Views\Home\Index.cshtml* archivo. En el paso siguiente de hello, se reemplazará marcado Hola generado con el código que usa [jQuery](http://jquery.com/) y [Knockout.js](http://knockoutjs.com/). Este nuevo código recupera la lista de Hola de contactos del uso de API web y enlaza hello JSON y, a continuación, póngase en contacto con datos toohello interfaz de usuario mediante knockout.js. Para obtener más información, vea hello [pasos](#nextsteps) sección Hola final de este tutorial. 
2. Reemplace el contenido de hello del archivo hello con hello siguiente código.
   
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
3. Haga clic en carpeta de contenido de Hola y haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento...** .
   
    ![Incorporación de una hoja de estilo en el menú contextual de la carpeta Content][addcode005]
4. Hola **Agregar nuevo elemento** diálogo cuadro, escriba **estilo** en Hola cuadro de búsqueda de derecho superior y, a continuación, seleccione **hoja de estilos**.
    ![Cuadro de diálogo Add New Item][rxStyle]
5. Archivo de nombre hello *Contacts.css* y haga clic en **agregar**. Reemplace el contenido de hello del archivo hello con hello siguiente código.
   
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
   
    Usaremos esta hoja de estilos de diseño de hello, colores y estilos utilizados en la aplicación de administrador de contactos de hello.
6. Abra hello *App_Start\BundleConfig.cs* archivo.
7. Agregar Hola después Hola de código tooregister [Knockout](http://knockoutjs.com/index.html "KO") complemento.
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    Este ejemplo con knockout toosimplify dinámica código JavaScript que controla las plantillas de pantalla de Hola.
8. Modificar Hola de hello contenido/css entrada tooregister *contacts.css* hoja de estilos. Hola de cambio después de línea:
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   Por:
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. Hola Package Manager Console, ejecute hello después comando tooinstall Knockout.
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a>Agregar un controlador para la interfaz Web API Restful Hola
1. En el **Explorador de soluciones**, haga clic con el botón derecho en Controladores y haga clic en **Agregar** y luego en **Controlador...** 
2. Hola **agregar scaffolding** diálogo cuadro, escriba **Web API 2 controlador con acciones que usan Entity Framework** y, a continuación, haga clic en **agregar**.
   
    ![Incorporación de un controlador API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. Hola **Agregar controlador** diálogo cuadro, escriba "ContactsController" como el nombre del controlador. Seleccione "Póngase en contacto con (ContactManager.Models)" para hello **clase modelo**.  Mantener valor predeterminado de Hola para hello **clase de contexto de datos**. 
4. Haga clic en **Agregar**.

### <a name="run-hello-application-locally"></a>Ejecutar la aplicación hello localmente
1. Presione la aplicación de hello toorun CTRL + F5.
   
    ![Página de índice][intro001]
2. Escriba un contacto y haga clic en **Agregar**. aplicación Hello devuelve una página de inicio de toohello y muestra contacto Hola especificado.
   
    ![Página de índice con elementos de lista de tareas pendientes][addwebapi004]
3. En el Explorador de hello, anexar **/api/contactos** toohello URL.
   
    dirección URL de Hello resultante tendrá un aspecto similar http://localhost:1234/api/contactos. web RESTful Hola API agregó devuelve contactos Hola almacenado. Firefox y Chrome mostrará datos de hello en formato XML.
   
    ![Página de índice con elementos de lista de tareas pendientes][rxFFchrome]

    Internet Explorer se le pedirá que tooopen o guardar contactos Hola.

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi006]


    Puede abrir Hola devuelve contactos en el Bloc de notas o en un explorador.

    Este resultado lo puede consumir otra aplicación como una página web móvil o aplicación.

    ![Cuadro de diálogo de almacenamiento de la API web.][addwebapi007]

    **Advertencia de seguridad**: en este punto, la aplicación es inseguro y sea vulnerable tooCSRF ataque. Más adelante en el tutorial Hola se quitará esta vulnerabilidad. Para más información, consulte [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks] (Impedimento de ataques de falsificación de solicitud entre sitios (CSRF)).
## <a name="add-xsrf-protection"></a>Incorporación de protección de XSRF
Falsificación de solicitud entre sitios (también conocido como XSRF o CSRF) es un ataque contra las aplicaciones hospedadas en web mediante el cual un sitio Web malintencionado puede influir en la interacción de hello entre un explorador del cliente y un sitio Web de confianza para ese explorador. Estos ataques se realizan porque los exploradores web enviará los tokens de autenticación automáticamente con cada sitio Web tooa de solicitud. ejemplo de Hola canónico es una cookie de autenticación, como ASP. Vale de autenticación de formularios de NET. Sin embargo, los sitios web que utilicen cualquier mecanismo de autenticación persistente (como Autenticación de Windows, Basic, entre otras) podrían ser objetivos de esos ataques.

Un ataque XSRF es distinto de un ataque de suplantación de identidad (phishing). Ataques de suplantación de identidad requieren interacción por parte del sujeto Hola. En un ataque de suplantación de identidad, un sitio Web malintencionado imiten el sitio Web de destino de Hola y víctima de hello es engañada para proporcionar el atacante toohello de información confidencial. En un ataque XSRF, no suele haber ninguna interacción necesarios de la víctima Hola. En su lugar, el atacante de hello depende explorador Hola enviar automáticamente todos los sitios Web de destino de toohello cookies relevante.

Para obtener más información, vea hello [Abrir proyecto de seguridad de aplicación Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto **ContactManager**, haga clic en **Agregar** y luego en **Clase**.
2. Archivo de nombre hello *ValidateHttpAntiForgeryTokenAttribute.cs* y agregue el siguiente código de hello:
   
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
3. Agregue Hola siguiente *con* toohello instrucción contratos controlador, por lo que tendrá acceso toohello **[ValidateHttpAntiForgeryToken]** atributo.
   
        using ContactManager.Filters;
4. Agregar hello **[ValidateHttpAntiForgeryToken]** atributo toohello métodos de entrada de hello **ContactsController** tooprotect, frente a amenazas XSRF. Va a agregar toohello "PutContact", "PostContact" y **DeleteContact** métodos de acción.
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. Hola de actualización *Scripts* sección de hello *Views\Home\Index.cshtml* tooinclude código tooget hello XSRF símbolos (tokens) de archivos.
   
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

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a>Publicar tooAzure de actualización de aplicación Hola y de base de datos SQL
aplicación de hello toopublish, repita procedimiento Hola que ha seguido anteriormente.

1. En **el Explorador de soluciones**, haga clic en proyecto de Hola y seleccione **publicar**.
   
    ![Publicar][rxP]
2. Haga clic en hello **configuración** ficha.
3. En **ContactsManagerContext(ContactsManagerContext)**, haga clic en hello **v** icono toochange *cadena de conexión remota* toohello de cadena de conexión para el contacto de Hola base de datos. Haga clic en **ContactDB**.
   
    ![Settings](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. Casilla de Hola para **ejecutar migraciones de Code First (se ejecuta al iniciarse la aplicación)**.
5. Haga clic en **Siguiente** y luego en **Vista previa**. Visual Studio muestra una lista de archivos de Hola que se agregaron o actualizaron.
6. Haga clic en **Publicar**.
   Una vez finalizada la implementación de hello, abre el Explorador de hello toohello página de inicio de la aplicación hello.
   
    ![Página de índice sin contactos][intro001]
   
    Hola Visual Studio publicar cadena de conexión de proceso que se configuran automáticamente Hola Hola implementado *Web.config* archivo toopoint toohello base de datos SQL. También configura migraciones de Code First tooautomatically Hola Actualizar base de datos toohello última versión primera aplicación de hello tiempo hello tiene acceso a la base de datos de hello después de la implementación.
   
    Como resultado de esta configuración, Code First creado Hola base de datos mediante la ejecución de código de hello en hello **inicial** clase que creó anteriormente. Lo hacía esta Hola primera hora Hola aplicación intentó tooaccess Hola base de datos después de la implementación.
7. Escriba un contacto como lo hizo cuando se ejecuta la aplicación de hello localmente, tooverify que se ha realizado correctamente en la implementación de la base de datos.

Cuando aparezca ese elemento de Hola que escriba se guarda y aparece en la página del Administrador de contacto de hello, sabrá que se han almacenado en la base de datos de Hola.

![Página de índice con contactos][addwebapi004]

aplicación Hello está ejecutando ahora en nube hello, mediante toostore de base de datos SQL sus datos. Cuando termine de probar la aplicación hello en Azure, elimínelo. aplicación Hello es público y no tiene un acceso de toolimit mecanismo.

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Otra forma que toostore los datos en una aplicación de Azure están toouse almacenamiento de Azure, que proporcionan almacenamiento de datos no relacionales en forma de Hola de blobs y tablas. Hola siguientes vínculos proporciona más información acerca la API Web, ASP.NET MVC y Windows Azure.

* [Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial] (Introducción a Entity Framework con MVC)
* [Introducción tooASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [Su primer ASP.NET Web API](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [Depuración de WAWS](web-sites-dotnet-troubleshoot-visual-studio.md)

Esta aplicación de ejemplo hello y tutorial se escribió por [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) con la asistencia de Tom Dykstra y Barry Dorrans (Twitter [ @blowdart ](https://twitter.com/blowdart)). 

Por favor, votar en qué le gustó o lo que le gustaría toosee mejorado, no solo acerca del tutorial de hello propio, sino también acerca de los productos de Hola que muestra. Sus comentarios nos ayudarán a clasificar las mejoras por orden de prioridad. Estamos especialmente interesados en Buscar es cuánto interés no existe en la automatización más para el proceso de Hola de configurar e implementar la base de datos de pertenencia de Hola. 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

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

