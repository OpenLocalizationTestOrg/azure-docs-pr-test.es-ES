---
title: "una aplicación ASP.NET en Azure con la base de datos SQL aaaBuild | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooget un ASP.NET aplicación trabajando en Azure, con conexión tooa base de datos SQL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a>Compilación de una aplicación ASP.NET en Azure con SQL Database

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático. Este tutorial muestra cómo toodeploy un ASP.NET controladas por datos web de aplicación en Azure y conéctela demasiado[base de datos de SQL Azure](../sql-database/sql-database-technical-overview.md). Cuando haya terminado, tendrá una aplicación ASP.NET que se ejecuta en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) y conectado tooSQL base de datos.

![Aplicación ASP.NET publicada en la aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una base de datos SQL en Azure
> * Conectar un tooSQL de aplicación ASP.NET base de datos
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Registros de flujo de Azure tooyour terminal
> * Administrar aplicación Hola Hola portal de Azure

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial:

* Instalar [2017 de Visual Studio](https://www.visualstudio.com/downloads/) con hello siguiendo las cargas de trabajo:
  - **ASP.NET y desarrollo web**
  - **Desarrollo de Azure**

  ![ASP.NET y desarrollo web y desarrollo de Azure (en web y en la nube)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>Descargar el ejemplo hello

[Descargar el proyecto de ejemplo de Hola](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).

Extraer (Descomprimir) hello *master.zip-dotnet-sqldb-tutorial* archivo.

proyecto de ejemplo de Hola contiene básico [ASP.NET MVC](https://www.asp.net/mvc) aplicación CRUD (crear-lectura-actualización-eliminación) con [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).

### <a name="run-hello-app"></a>Ejecutar aplicación hello

Abra hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* archivo en Visual Studio. 

Tipo `Ctrl+F5` toorun Hola aplicación sin depuración. aplicación Hello se muestra en el explorador predeterminado. Seleccione hello **crear nuevo** vincular y crear un par *tareas* elementos. 

![Cuadro de diálogo New ASP.NET Project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

Hola de prueba **editar**, **detalles**, y **eliminar** vínculos.

aplicación Hello usa un tooconnect de contexto de base de datos con la base de datos de Hola. En este ejemplo, el contexto de base de datos de hello usa una cadena de conexión denominada `MyDbConnection`. cadena de conexión de Hola se establecerá en hello *Web.config* de archivos y que se hace referencia en hello *Models/MyDatabaseContext.cs* archivo. nombre de cadena de conexión de Hola se utiliza más adelante en hello tooconnect tutorial hello web de Azure aplicación tooan base de datos de SQL Azure. 

## <a name="publish-tooazure-with-sql-database"></a>Publicar tooAzure con base de datos SQL

Hola **el Explorador de soluciones**, haga clic en el **DotNetAppSqlDb** de proyecto y seleccione **publicar**.

![Publicar desde el Explorador de soluciones](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

Asegúrese de que **Microsoft Azure App Service** está seleccionado y haga clic en **Publicar**.

![Publicar desde la página de información general del proyecto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

Publicación abre hello **crear servicio en la aplicación** cuadro de diálogo, lo que ayuda a crear todos los Hola recursos de Azure necesita toorun la aplicación web ASP.NET en Azure.

### <a name="sign-in-tooazure"></a>Inicie sesión en tooAzure

Hola **crear servicio en la aplicación** cuadro de diálogo, haga clic en **agregar una cuenta**y, a continuación, inicie sesión en tooyour suscripción de Azure. Si ya ha iniciado sesión en una cuenta de Microsoft, asegúrese de que esa cuenta contiene la suscripción de Azure. Si inició sesión Hola cuenta Microsoft no tiene su suscripción de Azure, haga clic en él cuenta correcta de hello tooadd.
   
![Inicie sesión en tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

Una vez iniciado sesión, está listo toocreate que Hola a todos los recursos que necesita para la aplicación web de Azure en este cuadro de diálogo.

### <a name="configure-hello-web-app-name"></a>Configurar el nombre de la aplicación hello

Puede mantener el nombre de la aplicación hello generado o cambiar nombre único de tooanother (caracteres válidos son `a-z`, `0-9`, y `-`). nombre de la aplicación Hello se usa como parte de la dirección URL predeterminada de hello para la aplicación (`<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre de la aplicación web). nombre de la aplicación Hello debe toobe único en todas las aplicaciones de Azure. 

![Cuadro de diálogo Create App Service (Crear App Service)](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a>Crear un grupo de recursos

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Siguiente demasiado**grupo de recursos**, haga clic en **nuevo**.

![TooResource siguiente grupo, haga clic en nuevo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

Grupo de recursos de nombre hello **myResourceGroup**.

> [!NOTE]
> No haga clic en **Crear**. En primer lugar debe tooset una base de datos SQL en un paso posterior.

### <a name="create-an-app-service-plan"></a>Creación de un plan de App Service

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Siguiente demasiado**Plan de servicio de aplicaciones**, haga clic en **nuevo**. 

Hola **configurar un Plan de servicio de aplicaciones** cuadro de diálogo Configurar nuevo plan de servicio de aplicaciones Hola con hello después de configuración:

![Creación de un plan de App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| Configuración  | Valor sugerido | Para obtener más información |
| ----------------- | ------------ | ----|
|**Plan de App Service**| myAppServicePlan | [Planes de App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|**Ubicación**| Europa occidental | [Regiones de Azure](https://azure.microsoft.com/regions/) |
|**Tamaño**| Gratuito | [Planes de tarifa](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a>Creación de una instancia de SQL Server

Antes de crear una base de datos, necesita un [servidor lógico de Azure SQL Database](../sql-database/sql-database-features.md). Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo.

Seleccione **Explorar otros servicios de Azure**.

![Configurar el nombre de la aplicación web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

Hola **servicios** , haga clic en hello  **+**  icono siguiente demasiado**base de datos SQL**. 

![En la ficha de servicios de hello, haga clic en icono + hello tooSQL siguiente base de datos.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

Hola **Configurar base de datos de SQL** cuadro de diálogo, haga clic en **New** siguiente demasiado**SQL Server**. 

Se genera un nombre de servidor único. Este nombre se usa como parte de la dirección URL predeterminada de hello para el servidor lógico, `<server_name>.database.windows.net`. Debe ser único entre todas las instancias de servidor lógico de Azure. Puede cambiar el nombre del servidor de hello, pero para este tutorial, mantenga el valor de hello generado.

Agregue un nombre de usuario y una contraseña de administrador y luego seleccione **Aceptar**. Para conocer los requisitos de complejidad de la contraseña, consulte [Directivas de contraseñas](/sql/relational-databases/security/password-policy).

Recuerde este nombre de usuario y esta contraseña. Necesite servidor lógico de toomanage Hola instancia posteriormente.

![Creación de una instancia de SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a>una Base de datos SQL

Hola **Configurar base de datos de SQL** cuadro de diálogo: 

* Mantener generada de manera predeterminada hello **nombre de base de datos**.
* En **Nombre de la cadena de conexión**, escriba *MyDbConnection*. Este nombre debe coincidir con la cadena de conexión de Hola que se hace referencia en *Models/MyDatabaseContext.cs*.
* Seleccione **Aceptar**.

![Configuración de SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

Hola **crear servicio en la aplicación** cuadro de diálogo muestra los recursos de Hola que haya creado. Haga clic en **Crear**. 

![recursos de Hola que ha creado](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

Una vez que finalice el Asistente de hello, crear recursos de Azure de hello, publica su tooAzure de aplicación ASP.NET. El explorador predeterminado se inicia con la aplicación toohello implementado de hello dirección URL. 

Agregue algunos elementos de tareas pendientes.

![Aplicación ASP.NET publicada en la aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

¡Enhorabuena! La aplicación ASP.NET orientada a datos se ejecuta en directo en Azure App Service.

## <a name="access-hello-sql-database-locally"></a>Hola de acceso base de datos SQL localmente

Visual Studio le permite explorar y administrar la base de datos SQL nueva fácilmente en hello **Explorador de objetos de SQL Server**.

### <a name="create-a-database-connection"></a>Creación de una conexión de base de datos

De hello **vista** menú, seleccione **Explorador de objetos de SQL Server**.

En la parte superior de Hola de **Explorador de objetos de SQL Server**, haga clic en hello **agregar SQL Server** botón.

### <a name="configure-hello-database-connection"></a>Configurar conexión de base de datos de Hola

Hola **conectar** cuadro de diálogo, expanda hello **Azure** nodo. Aquí se muestran todas las instancias de SQL Database de Azure.

Seleccione hello `DotNetAppSqlDb` base de datos SQL. conexión de Hola que creó anteriormente se rellena automáticamente en la parte inferior de Hola.

Escriba la contraseña de administrador de base de datos de Hola que creó anteriormente y haga clic en **conectar**.

![Configuración de la conexión de base de datos de Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a>Permitir la conexión de cliente desde el equipo

Hola **crear una nueva regla de firewall** se abre el cuadro de diálogo. De forma predeterminada, la instancia de SQL Database solo permite conexiones desde servicios de Azure, como la aplicación web de Azure. tooconnect tooyour la base de datos, cree una regla de firewall en la instancia de base de datos SQL de Hola. regla de firewall de Hello permite Hola de dirección IP pública del equipo local.

cuadro de diálogo de Hello ya se rellena con la dirección IP pública de su equipo.

Asegúrese de que **Add my client IP** (Agregar mi IP de cliente) está seleccionado y haga clic en **Aceptar**. 

![Configuración del firewall para la instancia de SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

Una vez que Visual Studio finaliza la creación de la configuración de firewall de hello para la instancia de base de datos SQL, la conexión se muestra en **Explorador de objetos de SQL Server**.

En este caso, puede realizar operaciones de base de datos más habituales hello, como consultas de ejecución, crean vistas y procedimientos almacenados y mucho más. 

Haga doble clic en hello `Todoes` de tabla y seleccione **ver datos**. 

![Exploración de objetos de SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a>Actualización de aplicaciones con Migraciones de Code First

Puede utilizar herramientas conocidas de hello en Visual Studio tooupdate la base de datos y la aplicación web en Azure. En este paso, usar migraciones de Code First en Entity Framework toomake un esquema de base de datos de cambio tooyour y publicarlo tooAzure.

Para más información sobre el uso de Entity Framework Code First Migrations, consulte [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Introducción a Entity Framework 6 Code First mediante MVC 5).

### <a name="update-your-data-model"></a>Actualización del modelo de datos

Abra _Models\Todo.cs_ en el editor de código de hello. Agregar Hola después de la propiedad toohello `ToDo` clase:

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a>Ejecución de Migraciones de Code First

Ejecutar algunos comandos toomake actualizaciones tooyour base de datos local. 

De hello **herramientas** menú, haga clic en **Administrador de paquetes de NuGet** > **Package Manager Console**.

En la ventana de la consola de administrador de paquetes de saludo, habilitar migraciones de Code First:

```PowerShell
Enable-Migrations
```

Agregue una migración:

```PowerShell
Add-Migration AddProperty
```

Actualizar la base de datos local de hello:

```PowerShell
Update-Database
```

Tipo `Ctrl+F5` toorun Hola aplicación. Hola de prueba editar detalles y crear los vínculos.

Si la aplicación hello carga sin errores, se ha realizado correctamente en migraciones de Code First. Sin embargo, su aspecto aún página Hola iguales porque la lógica de aplicación no usa esta nueva propiedad todavía. 

### <a name="use-hello-new-property"></a>Use la nueva propiedad de Hola

Realizar algunos cambios en su Hola de toouse código `Done` propiedad. Para simplificar, en este tutorial, va hello toochange `Index` y `Create` vistas de propiedad de hello toosee en acción.

Abra _Controllers\TodosController.cs_.

Buscar hello `Create()` método y agregue `Done` toohello lista de propiedades de hello `Bind` atributo. Cuando haya terminado, su `Create()` firma del método es similar a Hola siguiente código:

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

Abra _Views\Todos\Create.cshtml_.

Hola código Razor, debería ver un `<div class="form-group">` elemento que utiliza `model.Description`y, a continuación, otra `<div class="form-group">` elemento que utiliza `model.CreatedDate`. Inmediatamente después de estos dos elementos, agregue otro elemento `<div class="form-group">` que use `model.Done`:

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

Abra _Views\Todos\Index.cshtml_.

Busque Hola vacía `<th></th>` elemento. Justo encima de este elemento, agregue después el código Razor de hello:

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

Buscar hello `<td>` elemento que contiene Hola `Html.ActionLink()` métodos auxiliares. Justo encima de este elemento, agregue después el código Razor de hello:

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

Eso es todo lo necesario toosee cambios de Hola Hola `Index` y `Create` vistas. 

Tipo `Ctrl+F5` toorun Hola aplicación.

Ahora puede agregar una tarea pendiente y marcar **Listo**. A continuación se debería mostrar en su página principal como un elemento completado. Recuerde que hello `Edit` vista no muestra hello `Done` campo, ya que no ha cambiado hello `Edit` vista.

### <a name="enable-code-first-migrations-in-azure"></a>Habilitación de Migraciones de Code First en Azure

Ahora que el código de cambios, incluida la migración de base de datos, puedes publicación aplicación de Azure web tooyour y actualizar la base de datos de SQL con migraciones de Code First demasiado.

Igual que antes, haga clic con el botón derecho en su proyecto y seleccione **Publicar**.

Haga clic en **configuración** tooopen Hola Asistente para la publicación.

![Abrir la configuración de publicación](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

En el Asistente de hello, haga clic en **siguiente**.

Asegúrese de que esa cadena de conexión de hello para la base de datos de SQL se rellena en **MyDatabaseContext (MyDbConnection)**. Puede que necesite hello tooselect **myToDoAppDb** base de datos de la lista desplegable de Hola. 

Seleccione **Ejecutar Migraciones de Code First (se ejecuta al iniciar la aplicación)** y luego haga clic en **Guardar**.

![Habilitar Migraciones de Code First en una aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a>Publicación de los cambios

Ahora que ha habilitado Migraciones de Code First en su aplicación web de Azure, publique los cambios en el código.

Hola, página de publicación, haga clic en **publicar**.

Intente volver a agregar elementos de tareas pendientes y seleccione **Listo**; se mostrarán en su página de inicio como un elemento completado.

![Aplicación web de Azure después de aplicar Migraciones de Code First](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

Aún se muestran todas las tareas pendientes existentes. Cuando vuelva a publicar su aplicación de ASP.NET, los datos existentes en su instancia de SQL Database no se perderán. Además, migraciones de Code First solo cambia el esquema de datos de Hola y deja intactos los datos existentes.


## <a name="stream-application-logs"></a>Transmisión de registros de aplicación

Puede transmitir los mensajes de seguimiento directamente desde su tooVisual de aplicación web de Azure Studio.

Abra _Controllers\TodosController.cs_.

Cada acción comienza con un método `Trace.WriteLine()`. Este código se agrega tooshow también cómo tooadd seguimiento mensajes de aplicación web de Azure de tooyour.

### <a name="open-server-explorer"></a>Apertura del Explorador de servidores

De hello **vista** menú, seleccione **Explorador de servidores**. Puede configurar el registro de la aplicación web de Azure en el **Explorador de servidores**. 

### <a name="enable-log-streaming"></a>Habilitación de la secuencia de registros

En el **Explorador de servidores**, expanda **Azure** > **App Service**.

Expanda hello **myResourceGroup** grupo de recursos, que se creó al crear aplicación web de Azure de hello por primera vez.

Haga clic con el botón derecho en la aplicación web de Azure y seleccione **Ver registros de streaming**.

![Habilitación de la secuencia de registros](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

Hello registros son ahora se envía en hello **salida** ventana. 

![Secuencia de registros en la ventana Salida](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

Sin embargo, aún no ve ningún seguimiento mensajes de saludo. Que porque, cuando selecciona **ver registros de Streaming**, la aplicación web de Azure establece el nivel de seguimiento de hello demasiado`Error`, que sólo registra los eventos de error (con hello `Trace.TraceError()` método).

### <a name="change-trace-levels"></a>Cambio de los niveles de seguimiento

seguimiento de hello toochange niveles toooutput otros mensajes de seguimiento, vaya vuelve demasiado**Explorador de servidores**.

Haga clic con el botón derecho en la aplicación web de Azure y seleccione **Configuración**.

Hola **(sistema de archivos) del registro de aplicaciones** lista desplegable, seleccione **detallado**. Haga clic en **Guardar**.

![TooVerbose de nivel de seguimiento de cambios](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> Puede experimentar con diferentes niveles toosee qué tipos de mensajes se muestran para cada nivel. Por ejemplo, hello **información** nivel incluye todos los archivos creados por `Trace.TraceInformation()`, `Trace.TraceWarning()`, y `Trace.TraceError()`, pero no los archivos creados por `Trace.WriteLine()`.
>
>

En el explorador, intente hacer clic en torno a aplicación de lista de tareas pendientes de hello en Azure. los mensajes de seguimiento de Hello ahora se transmiten toohello **salida** ventana de Visual Studio.

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a>Detención de las secuencias de registro

toostop Hola servicio de transmisión por secuencias de registro, haga clic en hello **detener la supervisión de** botón en hello **salida** ventana.

![Detención de las secuencias de registro](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a>Administración de la aplicación web de Azure

Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó. 



Hola menú izquierdo, haga clic en **servicio de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

Ha llegado a la página de la aplicación web. 

De forma predeterminada, el portal de hello muestra hello **Introducción** página. Esta página proporciona una visión del funcionamiento de la aplicación. En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar. pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir. 

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:

> [!div class="checklist"]
> * Crear una base de datos SQL en Azure
> * Conectar un tooSQL de aplicación ASP.NET base de datos
> * Implementar Hola aplicación tooAzure
> * Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello
> * Registros de flujo de Azure tooyour terminal
> * Administrar aplicación Hola Hola portal de Azure

Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre toohello web app.

> [!div class="nextstepaction"]
> [Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web](app-service-web-tutorial-custom-domain.md)
