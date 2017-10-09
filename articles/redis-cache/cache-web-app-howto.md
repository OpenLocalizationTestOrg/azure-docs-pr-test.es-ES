---
title: "aaaHow toocreate una aplicación Web con caché en Redis | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una aplicación Web con caché en Redis"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a>¿Cómo toocreate una aplicación Web con caché en Redis
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

Este tutorial se muestra cómo toocreate e implementar una aplicación web ASP.NET web application tooa en el servicio de aplicación de Azure mediante Visual Studio de 2017. aplicación de ejemplo de Hola muestra una lista de las estadísticas de equipo de una base de datos y muestra distintas maneras toouse Azure Redis Cache toostore y recuperar datos de caché de Hola. Al completar el tutorial de hello, tendrá una aplicación web en ejecución que lee y escribe tooa base de datos optimizado con caché en Redis de Azure y hospedadas en Azure.

Aprenderá a realizar los siguientes procedimientos:

* ¿Cómo toocreate un 5 de MVC de ASP.NET web aplicación en Visual Studio.
* ¿Cómo tooaccess datos desde una base de datos mediante Entity Framework.
* Cómo tooimprove el rendimiento y reducir la carga de la base de datos, almacenar y recuperar datos mediante caché en Redis de Azure.
* Cómo toouse un Redis ordena conjunto tooretrieve Hola top 5 equipos.
* ¿Cómo tooprovision Hola recursos de Azure para la aplicación hello mediante una plantilla de administrador de recursos.
* ¿Cómo toopublish Hola tooAzure de aplicación con Visual Studio.

## <a name="prerequisites"></a>Requisitos previos
tutorial de hello toocomplete, debe tener Hola siguiendo los requisitos previos.

* [Cuenta de Azure](#azure-account)
* [Visual Studio de 2017 con hello Azure SDK para .NET](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a>Cuenta de Azure
Es necesario un tutorial de hello toocomplete cuenta de Azure. Puede:

* [Abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero). Obtenga créditos que pueden ser utilizado tootry out servicios de Azure de pago. Incluso después de que se agoten los créditos hello, puede mantener la cuenta de hello y usar características y servicios de Azure gratuitos.
* [Activar los beneficios de suscripción a Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero). Su suscripción a MSDN le proporciona créditos todos los meses que puede usar para servicios de Azure de pago.

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a>Visual Studio de 2017 con hello Azure SDK para .NET
tutorial de Hola se ha escrito para Visual Studio de 2017 con hello [Azure SDK para .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools). Hola 2.9.5 del SDK de Azure se incluye con el instalador de Visual Studio Hola.

Si tiene Visual Studio 2015, puede seguir el tutorial Hola con hello [Azure SDK para .NET](../dotnet-sdk.md) 2.8.2 o una versión posterior. [Descarga Hola SDK más reciente de Azure para Visual Studio 2015 aquí](http://go.microsoft.com/fwlink/?linkid=518003). Visual Studio se instala automáticamente con hello SDK si aún no lo tiene. Apariencia de algunas pantallas puede ser distinta de las ilustraciones de Hola que se muestra en este tutorial.

Si tiene Visual Studio 2013, puede [descarga Hola SDK más reciente de Azure para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322). Apariencia de algunas pantallas puede ser distinta de las ilustraciones de Hola que se muestra en este tutorial.

## <a name="create-hello-visual-studio-project"></a>Crear proyecto de Visual Studio Hola
1. Abra Visual Studio y haga clic en **Archivo**, **Nuevo**, **Proyecto**.
2. Expanda hello **Visual C#** nodo Hola **plantillas** lista, seleccione **nube**y haga clic en **aplicación Web ASP.NET**. Asegúrese de que se selecciona **.NET Framework 4.5.2** o superior.  Tipo de **ContosoTeamStats** en hello **nombre** cuadro de texto y haga clic en **Aceptar**.
   
    ![Crear proyecto][cache-create-project]
3. Seleccione **MVC** como tipo de proyecto de Hola. 

    Asegúrese de que **sin autenticación** se especifica para hello **autenticación** configuración. Según su versión de Visual Studio, se puede establecer a predeterminado de Hola toosomething else. toochange, haga clic en **Cambiar autenticación** y seleccione **sin autenticación**.

    Si está siguiendo junto con Visual Studio 2015, desactive hello **Host en la nube de hello** casilla de verificación. Deberá [aprovisionar Hola recursos de Azure](#provision-the-azure-resources) y [publicar Hola aplicación tooAzure](#publish-the-application-to-azure) en los siguientes pasos de tutorial Hola. Para obtener un ejemplo de aprovisionamiento de una aplicación de servicio de aplicaciones web de Visual Studio dejando **Host en la nube de hello** activa, consulte [empezar a trabajar con aplicaciones Web en el servicio de aplicaciones de Azure, con ASP.NET y Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).
   
    ![Seleccionar plantilla de proyecto][cache-select-template]
4. Haga clic en **Aceptar** proyecto de hello toocreate.

## <a name="create-hello-aspnet-mvc-application"></a>Crear hello aplicación ASP.NET MVC
En esta sección del tutorial de hello, podrá crear aplicación básica de Hola que lee y muestra las estadísticas de equipo de una base de datos.

* [Agregar paquete de NuGet Entity Framework Hola](#add-the-entity-framework-nuget-package)
* [Agregar modelo Hola](#add-the-model)
* [Agregar controlador Hola](#add-the-controller)
* [Configurar vistas de Hola](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a>Agregar paquete de NuGet Entity Framework Hola

1. Haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.
2. Ejecución hello después del comando de hello **Package Manager Console** ventana.
    
    ```
    Install-Package EntityFramework
    ```

Para obtener más información acerca de este paquete, vea hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) página de NuGet.

### <a name="add-hello-model"></a>Agregar modelo Hola
1. Haga clic con el botón derecho en **Modelos** en el **Explorador de soluciones** y elija **Agregar**, **Clase**. 
   
    ![Agregar modelo][cache-model-add-class]
2. Escriba `Team` nombre de la clase hello y haga clic en **agregar**.
   
    ![Agregar de clase de modelo][cache-model-add-class-dialog]
3. Reemplace hello `using` las instrucciones en la parte superior de Hola de hello `Team.cs` archivo con la siguiente hello `using` instrucciones.

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. Reemplace la definición de Hola de hello `Team` clase con hello siguiente fragmento de código que contiene un controlador actualizado, `Team` clase definición, así como otras clases de aplicación auxiliar de Entity Framework. Para obtener más información sobre Hola código primer enfoque tooEntity marco de trabajo que se utiliza en este tutorial, vea [código primera tooa nueva base de datos](https://msdn.microsoft.com/data/jj193542).

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. En **el Explorador de soluciones**, haga doble clic en **web.config** tooopen lo.
   
    ![Web.config][cache-web-config]
2. Agregue los siguiente hello `connectionStrings` sección. Hola nombre de cadena de conexión de hello debe coincidir con hello de hello clase de contexto de base de datos de Entity Framework que es `TeamContext`.

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    Puede agregar nuevos hello `connectionStrings` sección después `configSections`, tal y como se muestra en el siguiente ejemplo de Hola.

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > La cadena de conexión puede ser diferente en función de la versión de Hola de Visual Studio y SQL Server Express edition utiliza tutorial de hello toocomplete. plantilla de Hello web.config debe ser toomatch configurado la instalación y puede contener `Data Source` como entradas `(LocalDB)\v11.0` (de SQL Server Express 2012) o `Data Source=(LocalDB)\MSSQLLocalDB` (de SQL Server Express 2014 o versiones posteriores). Para más información acerca de las cadenas de conexión y las versiones de SQL Express, consulte [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).

### <a name="add-hello-controller"></a>Agregar controlador Hola
1. Presione **F6** proyecto de hello toobuild. 
2. En **el Explorador de soluciones**, contextual hello **controladores** carpeta y elija **agregar**, **controlador**.
   
    ![Agregar controlador][cache-add-controller]
3. Seleccione **Controlador de MVC 5 con vistas que usa Entity Framework** y haga clic en **Agregar**. Si se produce un error después de hacer clic **agregar**, asegúrese de que ha generado el proyecto de hello en primer lugar.
   
    ![Agregar controlador][cache-add-controller-class]
4. Seleccione **equipo (ContosoTeamStats.Models)** de hello **clase modelo** lista desplegable. Seleccione **TeamContext (ContosoTeamStats.Models)** de hello **clase de contexto de datos** lista desplegable. Tipo de `TeamsController` en hello **controlador** cuadro de texto Nombre (si no se rellena automáticamente). Haga clic en **agregar** toocreate Hola clase de controlador y agregar vistas predeterminadas de Hola.
   
    ![Configurar controlador][cache-configure-controller]
5. En **el Explorador de soluciones**, expanda **Global.asax** y haga doble clic en **Global.asax.cs** tooopen lo.
   
    ![Global.asax.cs][cache-global-asax]
6. Agregar Hola siguiendo dos `using` instrucciones al principio de hello del archivo de hello en hello otro `using` instrucciones.

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. Agregar Hola después de la línea de código al final de Hola de hello `Application_Start` método.

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. En el **Explorador de soluciones**, expanda `App_Start` y haga doble clic en `RouteConfig.cs`.
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. Reemplace `controller = "Home"` Hola después el código de hello `RegisterRoutes` método con `controller = "Teams"` tal y como se muestra en el siguiente ejemplo de Hola.

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a>Configurar vistas de Hola
1. En **el Explorador de soluciones**, expanda hello **vistas** hello carpeta y, a continuación, **Shared** carpeta y haga doble clic en **_Layout.cshtml**. 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. Cambiar contenido Hola de hello `title` elemento y reemplace `My ASP.NET Application` con `Contoso Team Stats` tal y como se muestra en el siguiente ejemplo de Hola.

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. Hola `body` sección, actualice primero hello `Html.ActionLink` instrucción y reemplazar `Application name` con `Contoso Team Stats` y reemplace `Home` con `Teams`.
   
   * Antes: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`
   * Después: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`
     
     ![Cambios de código][cache-layout-cshtml-code]
2. Presione **CTRL+F5** toobuild y ejecutar una aplicación Hola. Esta versión de la aplicación hello lee resultados Hola directamente desde la base de datos de Hola. Hola Nota **crear nuevo**, **editar**, **detalles**, y **eliminar** las acciones que automáticamente agregan toohello aplicación Hola **Controlador de MVC 5 con vistas, mediante Entity Framework** scaffolding. En la sección siguiente de Hola de tutorial Hola agregará acceso a datos de Hola de toooptimize de caché en Redis y proporcionan características adicionales de aplicaciones toohello.

![Aplicación de inicio][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a>Configurar toouse de aplicación Hola caché en Redis
En esta sección del tutorial de hello, podrá configurar toostore de aplicación de ejemplo de Hola y recuperar las estadísticas de equipo Contoso de una instancia de caché en Redis de Azure mediante hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cliente de caché.

* [Configurar la aplicación de hello toouse StackExchange.Redis](#configure-the-application-to-use-stackexchangeredis)
* [Actualizar hello TeamsController clase tooreturn los resultados de caché de Hola o base de datos de Hola](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [Actualizar Hola crear, editar y eliminar métodos toowork con caché de Hola](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [Actualizar toowork de vista de índice de los equipos de hello con caché Hola](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a>Configurar la aplicación de hello toouse StackExchange.Redis
1. tooconfigure una aplicación cliente en Visual Studio mediante Hola paquete de StackExchange.Redis NuGet, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.
2. Ejecución hello después del comando de hello `Package Manager Console` ventana.
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado para su tooaccess de aplicación de cliente caché en Redis de Azure con el cliente de caché de StackExchange.Redis Hola. Si prefiere una versión con nombre seguro de hello toouse `StackExchange.Redis` biblioteca de cliente, instalación hello `StackExchange.Redis.StrongName` paquete.
3. En **el Explorador de soluciones**, expanda hello **controladores** carpeta y haga doble clic en **TeamsController.cs** tooopen lo.
   
    ![Controlador de equipos][cache-teamscontroller]
4. Agregar Hola siguiendo dos `using` instrucciones demasiado**TeamsController.cs**.

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. Agregar Hola siguiendo dos toohello propiedades `TeamsController` clase.

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. Crear un archivo en el equipo denominado `WebAppPlusCacheAppSecrets.config` y lo coloca en una ubicación que no se comprueba con el código fuente de saludo de la aplicación de ejemplo, debe decidir toocheck en otra parte. En este Hola ejemplo `AppSettingsSecrets.config` archivo se encuentra en `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.
   
    Editar hello `WebAppPlusCacheAppSecrets.config` de archivos y agregar Hola después de contenido. Si ejecuta aplicación hello localmente esta información es instancia de caché en Redis de Azure tooyour tooconnect usado. Más adelante en el tutorial Hola podrá aprovisionar una caché en Redis de Azure y actualice la contraseña y nombre de la memoria caché de Hola. Si no tiene pensado toorun aplicación de ejemplo de Hola localmente puede omitir la creación de hello de este archivo y los pasos subsiguientes de Hola que hacen referencia a archivo hello, porque cuando se implementa la aplicación de hello tooAzure recupera información de conexión de caché de Hola de aplicación hello configuración para la aplicación Web de hello y no desde este archivo. Desde hello `WebAppPlusCacheAppSecrets.config` no se ha implementado tooAzure con la aplicación, no es necesario a menos que vayan toorun aplicación de hello localmente.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. En **el Explorador de soluciones**, haga doble clic en **web.config** tooopen lo.
   
    ![Web.config][cache-web-config]
2. Agregue los siguiente hello `file` atributo toohello `appSettings` elemento. Si utiliza un nombre de archivo diferente o una ubicación, sustituya esos valores para que se muestran en el ejemplo de Hola Hola.
   
   * Antes: `<appSettings>`
   * Después: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`
     
   en tiempo de ejecución ASP.NET de Hello combina el contenido de Hola de archivo externos de hello con marcado Hola Hola `<appSettings>` elemento. en tiempo de ejecución de Hello omite el atributo de archivo de hello si no se encuentra el archivo especificado de Hola. Los secretos (caché de tooyour de cadena de conexión de hello) no se incluyen como parte del código fuente de hello para la aplicación hello. Al implementar su tooAzure de aplicación web, Hola `WebAppPlusCacheAppSecrests.config` no se implementarán archivo (es decir, lo que desea). Hay varias toospecify formas estos secretos en Azure y, en este tutorial se configuran automáticamente para cuando se [aprovisionar Hola recursos de Azure](#provision-the-azure-resources) en un paso posterior del tutorial. Para obtener más información sobre cómo trabajar con secretos en Azure, consulte [las prácticas recomendadas para la implementación de las contraseñas y otros datos confidenciales tooASP.NET y servicio de aplicaciones de Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a>Actualizar hello TeamsController clase tooreturn los resultados de caché de Hola o base de datos de Hola
En este ejemplo, se pueden recuperar estadísticas de equipo de base de datos de Hola o desde la caché de Hola. Estadísticas de equipo se almacenan en caché de Hola como un número de serie `List<Team>`y también como un conjunto ordenado con tipos de datos de Redis. Al recuperar elementos de un conjunto ordenado, puede recuperar algunos, todos o consultar algunos de ellos. En este ejemplo, podrá consultar conjunto Hola ordenado para hello top 5 los equipos ordenados según el número de wins.

> [!NOTE]
> No es necesario toostore Hola estadísticas de equipo en varios formatos en memoria caché de hello en orden toouse caché en Redis de Azure. Este tutorial usa varios toodemonstrate formatos algunas de maneras diferentes de Hola y distintos tipos de datos puede usar datos de toocache.
> 
> 

1. Agregue los siguiente Hola `using` instrucciones toohello `TeamsController.cs` archivo en la parte superior de hello con hello otro `using` instrucciones.

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. Reemplazar actual hello `public ActionResult Index()` implementación del método con hello después de la implementación.

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. Agregar Hola después de tres toohello métodos `TeamsController` Hola de clase tooimplement `playGames`, `clearCache`, y `rebuildDB` tipos de acciones de hello switch (instrucción) agregada en el fragmento de código anterior de Hola.
   
    Hola `PlayGames` método actualiza las estadísticas de equipo de hello, simulando una temporada de juegos, guarda Hola base de datos de resultados toohello y borra Hola han quedado obsoletas en datos de caché de Hola.

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hola `RebuildDB` base de datos de método reinicializa Hola conjunto predeterminado de Hola de equipos, genera estadísticas para ellos y borra Hola han quedado obsoletas en datos de caché de Hola.

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    Hola `ClearCachedTeams` método quita las estadísticas de equipo almacenado en caché de memoria caché de Hola.

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. Agregar Hola después de cuatro toohello métodos `TeamsController` hello de la clase tooimplement distintas maneras de recuperar las estadísticas de equipo de Hola de caché de Hola y de base de datos de Hola. Cada uno de estos métodos devuelve una `List<Team>` que se muestra a continuación, vista de Hola.
   
    Hola `GetFromDB` método lee las estadísticas de equipo de Hola de base de datos de Hola.
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    Hola `GetFromList` método lee las estadísticas de equipo de Hola de memoria caché como un número de serie `List<Team>`. Si se produce un error de caché, estadísticas de equipo de Hola se leen desde la base de datos de hello y, a continuación, se almacena en caché de Hola durante la próxima vez. En este ejemplo usamos JSON.NET serialización tooserialize Hola .NET objetos tooand de caché de Hola. Para obtener más información, consulte [cómo los objetos en caché en Redis de Azure toowork con .NET](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    Hola `GetFromSortedSet` método lee las estadísticas de equipo de Hola de un conjunto ordenado en caché. Si se produce un error de caché, estadísticas de equipo de Hola se leen de base de datos de Hola y almacenadas en memoria caché de Hola como un conjunto ordenado.

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    Hola `GetFromSortedSetTop5` método lee conjunto superior de 5 equipos de hello en caché ordenados de Hola. Se inicia mediante la comprobación de caché de hello existencia Hola de hello `teamsSortedSet` clave. Si esta clave no está presente, Hola `GetFromSortedSet` método se llama tooread estadísticas de equipo de Hola y almacenarlos en caché de Hola. A continuación, hello conjunto ordenado en caché se consulta para hello top 5 los equipos que se devuelven.

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a>Actualizar Hola crear, editar y eliminar métodos toowork con caché de Hola
código de scaffolding de Hola que se generó como parte de este ejemplo incluye los métodos tooadd, editar y eliminar los equipos. Cada vez que un equipo es agregar, editar o quitar, datos de hello en memoria caché de Hola quedan anticuados. En esta sección, modificará estos hello tooclear de tres métodos en caché los equipos para que no se sincronizado con la base de datos de hello caché Hola.

1. Examinar toohello `Create(Team team)` método Hola `TeamsController` clase. Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. Examinar toohello `Edit(Team team)` método Hola `TeamsController` clase. Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. Examinar toohello `DeleteConfirmed(int id)` método Hola `TeamsController` clase. Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a>Actualizar toowork de vista de índice de los equipos de hello con caché Hola
1. En **el Explorador de soluciones**, expanda hello **vistas** carpeta y, a continuación, hello **equipos** carpeta y haga doble clic en **Index.cshtml**.
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. Cerca de hello parte superior del archivo hello, busque Hola siguiente elemento de párrafo.
   
    ![Tabla de acciones][cache-teams-index-table]
   
    Se trata de hello vínculo toocreate un nuevo equipo. Reemplace el elemento de párrafo de hello con hello en la tabla siguiente. Esta tabla tiene vínculos de acción para crear un nuevo equipo, reproducir una nueva estación de juegos, borrar la memoria caché de hello, recuperar los equipos de Hola de caché de hello en varios formatos, recuperar los equipos de Hola de base de datos de Hola y volver a generar Hola base de datos con datos de ejemplo nueva.

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. Desplazar hacia abajo de toohello de hello **Index.cshtml** de archivos y agregue Hola siguiente `tr` elemento para que sea la última fila de Hola Hola última tabla archivo hello.
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    Esta fila muestra el valor de Hola de `ViewBag.Msg` que contiene un informe de estado sobre la operación actual de Hola. Hola `ViewBag.Msg` se establece al hacer clic en cualquiera de los vínculos de acción de hello del paso anterior Hola.   
   
    ![Mensaje de estado][cache-status-message]
2. Presione **F6** proyecto de hello toobuild.

## <a name="provision-hello-azure-resources"></a>Aprovisionar Hola recursos de Azure
toohost su aplicación en Azure, primero debe aprovisionar Hola servicios de Azure que requiera la aplicación. aplicación de ejemplo de Hola en este tutorial usa Hola después de los servicios de Azure.

* Azure Redis Cache
* Aplicación web del Servicio de aplicaciones
* SQL Database

toodeploy estos grupo de recursos nuevos o existentes de tooa de servicios de su elección, haga clic en hello después **implementar tooAzure** botón.

[! [Implementar tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)

Esto **implementar tooAzure** botón usa hello [crear una aplicación Web más caché en Redis más base de datos SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) plantilla tooprovision estos servicios y el conjunto de Hola cadena de conexión de configuración de aplicación de hello hello y base de datos SQL para hello cadena de conexión de caché en Redis de Azure.

> [!NOTE]
> Si no tiene ninguna cuenta de Azure, puede [crear una gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en unos minutos.
> 
> 

Si hace clic en hello **implementar tooAzure** botón toma toohello portal de Azure e inicia Hola el proceso de creación de recursos de hello descritos por plantilla de Hola.

![Implementar tooAzure][cache-deploy-to-azure-step-1]

1. Hola **Fundamentos** sección, seleccione hello toouse de suscripción de Azure, seleccione un grupo de recursos existente o cree uno nuevo y especificar la ubicación del grupo de recursos de Hola.
2. Hola **configuración** sección, especifique un **inicio de sesión de administrador** (no use **administración**), **contraseña de inicio de sesión de administrador**y  **Nombre de la base de datos**. Hola se configuran otros parámetros para un servicio gratuito de aplicación aloja el plan y las opciones de bajo costo para Hola base de datos SQL y de caché en Redis de Azure, que no tiene un nivel gratis.

    ![Implementar tooAzure][cache-deploy-to-azure-step-2]

3. Después de establecer la configuración de hello deseado, desplácese toohello final de página de hello, términos de lectura hello y condiciones y comprobar hello **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** casilla de verificación.
4. Haga clic en toobegin aprovisionar recursos de hello, **compra**.

progreso de hello tooview de la implementación, haga clic en el icono de notificación de Hola y haga clic en **implementación iniciada**.

![Implementación iniciada][cache-deployment-started]

Puede ver estado de saludo de la implementación en hello **Microsoft.Template** hoja.

![Implementar tooAzure][cache-deploy-to-azure-step-3]

Cuando se complete el aprovisionamiento, puede publicar su tooAzure de aplicación desde Visual Studio.

> [!NOTE]
> Se muestran los errores que pueden producirse durante el proceso de aprovisionamiento de hello en hello **Microsoft.Template** hoja. Algunos errores comunes son demasiadas instancias de SQL Server o demasiados planes de hospedaje del Servicio de aplicaciones gratis por suscripción. Resuelva los errores y reinicie el proceso de hello haciendo clic en **volver a implementar** en hello **Microsoft.Template** hoja o hello **implementar tooAzure** botón en este tutorial.
> 
> 

## <a name="publish-hello-application-tooazure"></a>Publicar tooAzure de aplicación Hola
En este paso del tutorial de hello, podrá publicar Hola aplicación tooAzure y ejecútelo en la nube de Hola.

1. Menú contextual hello **ContosoTeamStats** proyecto en Visual Studio y elija **publicar**.
   
    ![Publicar][cache-publish-app]
2. Haga clic en **Microsoft Azure App Service**, elija **Seleccionar existente** y haga clic en **Publicar**.
   
    ![Publicar][cache-publish-to-app-service]
3. Seleccione la suscripción de hello usa al crear Hola recursos de Azure, expanda el grupo de recursos de Hola que contienen recursos de Hola y Hola seleccione deseado de aplicación Web. Si usa hello **implementar tooAzure** el nombre de la aplicación Web se inicia con el botón **sitio Web** seguido de algunos caracteres adicionales.
   
    ![Seleccionar aplicación web][cache-select-web-app]
4. Haga clic en **Aceptar** hello toobegin proceso de publicación. Transcurridos unos instantes completa Hola proceso de publicación y se inicie un explorador con hello ejecutando la aplicación de ejemplo. Si obtiene un error al validar o publicación de DNS y Hola proceso para el aprovisionamiento hello recursos de Azure para la aplicación hello recientemente finalizó, espere unos instantes y vuelva a intentarlo.
   
    ![Caché agregada][cache-added-to-application]

Hello siguiente tabla describe cada vínculo de acción de la aplicación de ejemplo de Hola.

| Acción | Descripción |
| --- | --- |
| Crear nuevo |Crear un nuevo equipo. |
| Reproducir temporada |Reproducir una temporada de juegos, estadísticas de equipo de Hola de actualización, y desactive cualquiera obsoleto datos de equipo de caché de Hola. |
| Borrar caché |Estadísticas del equipo desactive Hola de caché de Hola. |
| Mostrar de la caché |Recuperar estadísticas de equipo de Hola de memoria caché de Hola. Si se produce un error de caché, estadísticas de Hola de carga de base de datos de Hola y guarde toohello caché para la próxima vez. |
| Conjunto ordenado de caché |Recuperar estadísticas de equipo de Hola desde caché de hello utilizando un conjunto ordenado. Si se produce un error de caché, cargue estadísticas de Hola de base de datos de Hola y guardar la memoria caché de toohello mediante un conjunto ordenado. |
| 5 equipos principales de la caché |Recuperar los equipos de 5 superior Hola desde caché de hello utilizando un conjunto ordenado. Si se produce un error de caché, cargue estadísticas de Hola de base de datos de Hola y guardar la memoria caché de toohello mediante un conjunto ordenado. |
| Cargar de la base de datos |Recuperar estadísticas de equipo de Hola de base de datos de Hola. |
| Recompilar base de datos |Volver a generar la base de datos de Hola y cargarla con datos de ejemplo de equipo. |
| Editar, Detalles, Eliminar |Editar un equipo, ver los detalles de un equipo, eliminar un equipo. |

Haga clic en algunas de las acciones de Hola y experimentar con la recuperación de datos de Hola de orígenes diferentes de Hola. No hello las diferencias en hello tarda toocomplete Hola varias maneras de recuperar datos de Hola de base de datos de Hola y caché de Hola.

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a>Eliminar recursos de hello cuando haya terminado con la aplicación hello
Cuando haya terminado con la aplicación de tutorial de ejemplo de Hola, puede eliminar hello Azure utilizados en tooconserve de orden de costo de recursos y recursos. Si usas hello **implementar tooAzure** botón en hello [Hola de aprovisionar recursos de Azure](#provision-the-azure-resources) sección y todos los recursos están contenidos en hello mismo grupo de recursos, puede eliminarlos de forma conjunta en uno operación mediante la eliminación de grupo de recursos de Hola.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y haga clic en **grupos de recursos**.
2. Nombre del tipo hello de su grupo de recursos en hello **filtrar elementos...**  cuadro de texto.
3. Haga clic en **...**  toohello derecha de su grupo de recursos.
4. Hacer clic en **Eliminar**.
   
    ![Eliminar][cache-delete-resource-group]
5. Nombre del tipo hello de su grupo de recursos y haga clic en **eliminar**.
   
    ![Confirmar eliminación][cache-delete-confirm]

Después de unos pocos recursos de hello momentos se eliminan grupo y todos sus recursos independientes.

> [!IMPORTANT]
> Tenga en cuenta que la eliminación de un grupo de recursos es irreversible y ese grupo de recursos de Hola y todos los recursos de hello en él se eliminan permanentemente. Asegúrese de que no elimina accidentalmente grupo de recursos incorrecto de Hola o de recursos. Si crea recursos de Hola para hospedar este ejemplo dentro de un grupo de recursos existente, puede eliminar cada recurso individualmente de sus módulos respectivos.
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a>Ejecutar la aplicación de ejemplo de Hola en el equipo local
aplicación de hello toorun localmente en su equipo, necesita una caché en Redis de Azure de la instancia en qué toocache los datos. 

* Si ha publicado su aplicación tooAzure tal y como se describe en la sección anterior de hello, puede usar la instancia de caché en Redis de Azure de Hola que se haya proporcionado durante ese paso.
* Si tiene otra instancia de caché en Redis de Azure existente, puede utilizar ese toorun este ejemplo localmente.
* Si necesita toocreate una instancia de caché en Redis de Azure, puede seguir los pasos de hello en [crear una memoria caché](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).

Una vez que ha seleccionado o creado Hola caché toouse, examinar la caché de toohello Hola portal de Azure y recuperar hello [nombre de host](cache-configure.md#properties) y [las claves de acceso](cache-configure.md#access-keys) de la memoria caché. Para obtener instrucciones, consulte [Configuración de opciones de la memoria caché en Redis](cache-configure.md#configure-redis-cache-settings).

1. Abra Hola `WebAppPlusCacheAppSecrets.config` archivo que creó durante la hello [configurar toouse de aplicación Hola caché en Redis](#configure-the-application-to-use-redis-cache) paso de este tutorial con hello editor de su elección.
2. Editar hello `value` de atributo y reemplace `MyCache.redis.cache.windows.net` con hello [nombre de host](cache-configure.md#properties) de la memoria caché y especificar cualquier hello [clave primaria o secundaria](cache-configure.md#access-keys) de la memoria caché como contraseña de Hola.

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. Presione **CTRL+F5** aplicación de hello toorun.

> [!NOTE]
> Tenga en cuenta que porque la aplicación hello, incluida la base de datos de hello, se ejecuta localmente y hello caché en Redis hospedada en Azure, Hola caché puede aparecer toounder-realizar Hola bases de datos. Para obtener el mejor rendimiento, Hola aplicación cliente y debe ser instancia de caché en Redis de Azure en hello misma ubicación. 
> 
> 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga más información sobre [Introducción a ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) en hello [ASP.NET](http://asp.net/) sitio.
* Para obtener más ejemplos de creación de una aplicación Web ASP.NET en el servicio de aplicaciones, consulte [crear e implementar una aplicación web ASP.NET en el servicio de aplicación de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) conectar 2015 [demostración](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).
  * Encontrará tutoriales más rápidos de demostración de hello HealthClinic.biz, [tutoriales de herramientas de desarrollador de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).
* Obtener más información sobre hello [código primera tooa nueva base de datos](https://msdn.microsoft.com/data/jj193542) enfocar tooEntity marco de trabajo que se utiliza en este tutorial.
* Más información sobre las [aplicaciones web del Servicio de aplicaciones de Azure](../app-service-web/app-service-web-overview.md).
* Obtenga información acerca de cómo demasiado[monitor](cache-how-to-monitor.md) la memoria caché en hello portal de Azure.
* Exploración de las características premium de Caché en Redis de Azure
  
  * [La persistencia de tooconfigure para una caché en Redis de Azure Premium](cache-how-to-premium-persistence.md)
  * [¿Cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium](cache-how-to-premium-clustering.md)
  * [¿Cómo admiten tooconfigure red Virtual para una caché de Redis de Azure Premium](cache-how-to-premium-vnet.md)
  * Vea hello [preguntas más frecuentes de caché de Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obtener más detalles sobre el tamaño, el rendimiento y el ancho de banda con las cachés premium.

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

