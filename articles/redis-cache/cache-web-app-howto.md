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
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="8143d-103">¿Cómo toocreate una aplicación Web con caché en Redis</span><span class="sxs-lookup"><span data-stu-id="8143d-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8143d-104">.NET</span><span class="sxs-lookup"><span data-stu-id="8143d-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="8143d-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="8143d-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="8143d-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="8143d-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="8143d-107">Java</span><span class="sxs-lookup"><span data-stu-id="8143d-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="8143d-108">Python</span><span class="sxs-lookup"><span data-stu-id="8143d-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="8143d-109">Este tutorial se muestra cómo toocreate e implementar una aplicación web ASP.NET web application tooa en el servicio de aplicación de Azure mediante Visual Studio de 2017.</span><span class="sxs-lookup"><span data-stu-id="8143d-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="8143d-110">aplicación de ejemplo de Hola muestra una lista de las estadísticas de equipo de una base de datos y muestra distintas maneras toouse Azure Redis Cache toostore y recuperar datos de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="8143d-111">Al completar el tutorial de hello, tendrá una aplicación web en ejecución que lee y escribe tooa base de datos optimizado con caché en Redis de Azure y hospedadas en Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="8143d-112">Aprenderá a realizar los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="8143d-112">You'll learn:</span></span>

* <span data-ttu-id="8143d-113">¿Cómo toocreate un 5 de MVC de ASP.NET web aplicación en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8143d-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="8143d-114">¿Cómo tooaccess datos desde una base de datos mediante Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8143d-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="8143d-115">Cómo tooimprove el rendimiento y reducir la carga de la base de datos, almacenar y recuperar datos mediante caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="8143d-116">Cómo toouse un Redis ordena conjunto tooretrieve Hola top 5 equipos.</span><span class="sxs-lookup"><span data-stu-id="8143d-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="8143d-117">¿Cómo tooprovision Hola recursos de Azure para la aplicación hello mediante una plantilla de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8143d-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="8143d-118">¿Cómo toopublish Hola tooAzure de aplicación con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8143d-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8143d-119">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8143d-119">Prerequisites</span></span>
<span data-ttu-id="8143d-120">tutorial de hello toocomplete, debe tener Hola siguiendo los requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="8143d-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="8143d-121">Cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="8143d-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="8143d-122">Visual Studio de 2017 con hello Azure SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="8143d-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="8143d-123">Cuenta de Azure</span><span class="sxs-lookup"><span data-stu-id="8143d-123">Azure account</span></span>
<span data-ttu-id="8143d-124">Es necesario un tutorial de hello toocomplete cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="8143d-125">Puede:</span><span class="sxs-lookup"><span data-stu-id="8143d-125">You can:</span></span>

* <span data-ttu-id="8143d-126">[Abrir una cuenta de Azure gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="8143d-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="8143d-127">Obtenga créditos que pueden ser utilizado tootry out servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="8143d-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="8143d-128">Incluso después de que se agoten los créditos hello, puede mantener la cuenta de hello y usar características y servicios de Azure gratuitos.</span><span class="sxs-lookup"><span data-stu-id="8143d-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="8143d-129">[Activar los beneficios de suscripción a Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="8143d-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="8143d-130">Su suscripción a MSDN le proporciona créditos todos los meses que puede usar para servicios de Azure de pago.</span><span class="sxs-lookup"><span data-stu-id="8143d-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="8143d-131">Visual Studio de 2017 con hello Azure SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="8143d-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="8143d-132">tutorial de Hola se ha escrito para Visual Studio de 2017 con hello [Azure SDK para .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="8143d-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="8143d-133">Hola 2.9.5 del SDK de Azure se incluye con el instalador de Visual Studio Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="8143d-134">Si tiene Visual Studio 2015, puede seguir el tutorial Hola con hello [Azure SDK para .NET](../dotnet-sdk.md) 2.8.2 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="8143d-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="8143d-135">[Descarga Hola SDK más reciente de Azure para Visual Studio 2015 aquí](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="8143d-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="8143d-136">Visual Studio se instala automáticamente con hello SDK si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="8143d-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="8143d-137">Apariencia de algunas pantallas puede ser distinta de las ilustraciones de Hola que se muestra en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8143d-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="8143d-138">Si tiene Visual Studio 2013, puede [descarga Hola SDK más reciente de Azure para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="8143d-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="8143d-139">Apariencia de algunas pantallas puede ser distinta de las ilustraciones de Hola que se muestra en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8143d-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="8143d-140">Crear proyecto de Visual Studio Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="8143d-141">Abra Visual Studio y haga clic en **Archivo**, **Nuevo**, **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="8143d-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="8143d-142">Expanda hello **Visual C#** nodo Hola **plantillas** lista, seleccione **nube**y haga clic en **aplicación Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="8143d-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="8143d-143">Asegúrese de que se selecciona **.NET Framework 4.5.2** o superior.</span><span class="sxs-lookup"><span data-stu-id="8143d-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="8143d-144">Tipo de **ContosoTeamStats** en hello **nombre** cuadro de texto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Crear proyecto][cache-create-project]
3. <span data-ttu-id="8143d-146">Seleccione **MVC** como tipo de proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="8143d-147">Asegúrese de que **sin autenticación** se especifica para hello **autenticación** configuración.</span><span class="sxs-lookup"><span data-stu-id="8143d-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="8143d-148">Según su versión de Visual Studio, se puede establecer a predeterminado de Hola toosomething else.</span><span class="sxs-lookup"><span data-stu-id="8143d-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="8143d-149">toochange, haga clic en **Cambiar autenticación** y seleccione **sin autenticación**.</span><span class="sxs-lookup"><span data-stu-id="8143d-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="8143d-150">Si está siguiendo junto con Visual Studio 2015, desactive hello **Host en la nube de hello** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="8143d-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="8143d-151">Deberá [aprovisionar Hola recursos de Azure](#provision-the-azure-resources) y [publicar Hola aplicación tooAzure](#publish-the-application-to-azure) en los siguientes pasos de tutorial Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="8143d-152">Para obtener un ejemplo de aprovisionamiento de una aplicación de servicio de aplicaciones web de Visual Studio dejando **Host en la nube de hello** activa, consulte [empezar a trabajar con aplicaciones Web en el servicio de aplicaciones de Azure, con ASP.NET y Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8143d-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![Seleccionar plantilla de proyecto][cache-select-template]
4. <span data-ttu-id="8143d-154">Haga clic en **Aceptar** proyecto de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="8143d-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="8143d-155">Crear hello aplicación ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="8143d-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="8143d-156">En esta sección del tutorial de hello, podrá crear aplicación básica de Hola que lee y muestra las estadísticas de equipo de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="8143d-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="8143d-157">Agregar paquete de NuGet Entity Framework Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="8143d-158">Agregar modelo Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="8143d-159">Agregar controlador Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="8143d-160">Configurar vistas de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="8143d-161">Agregar paquete de NuGet Entity Framework Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="8143d-162">Haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.</span><span class="sxs-lookup"><span data-stu-id="8143d-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="8143d-163">Ejecución hello después del comando de hello **Package Manager Console** ventana.</span><span class="sxs-lookup"><span data-stu-id="8143d-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="8143d-164">Para obtener más información acerca de este paquete, vea hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) página de NuGet.</span><span class="sxs-lookup"><span data-stu-id="8143d-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="8143d-165">Agregar modelo Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-165">Add hello model</span></span>
1. <span data-ttu-id="8143d-166">Haga clic con el botón derecho en **Modelos** en el **Explorador de soluciones** y elija **Agregar**, **Clase**.</span><span class="sxs-lookup"><span data-stu-id="8143d-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Agregar modelo][cache-model-add-class]
2. <span data-ttu-id="8143d-168">Escriba `Team` nombre de la clase hello y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![Agregar de clase de modelo][cache-model-add-class-dialog]
3. <span data-ttu-id="8143d-170">Reemplace hello `using` las instrucciones en la parte superior de Hola de hello `Team.cs` archivo con la siguiente hello `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8143d-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="8143d-171">Reemplace la definición de Hola de hello `Team` clase con hello siguiente fragmento de código que contiene un controlador actualizado, `Team` clase definición, así como otras clases de aplicación auxiliar de Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="8143d-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="8143d-172">Para obtener más información sobre Hola código primer enfoque tooEntity marco de trabajo que se utiliza en este tutorial, vea [código primera tooa nueva base de datos](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="8143d-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="8143d-173">En **el Explorador de soluciones**, haga doble clic en **web.config** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="8143d-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="8143d-175">Agregue los siguiente hello `connectionStrings` sección.</span><span class="sxs-lookup"><span data-stu-id="8143d-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="8143d-176">Hola nombre de cadena de conexión de hello debe coincidir con hello de hello clase de contexto de base de datos de Entity Framework que es `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="8143d-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="8143d-177">Puede agregar nuevos hello `connectionStrings` sección después `configSections`, tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

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
    > <span data-ttu-id="8143d-178">La cadena de conexión puede ser diferente en función de la versión de Hola de Visual Studio y SQL Server Express edition utiliza tutorial de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8143d-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="8143d-179">plantilla de Hello web.config debe ser toomatch configurado la instalación y puede contener `Data Source` como entradas `(LocalDB)\v11.0` (de SQL Server Express 2012) o `Data Source=(LocalDB)\MSSQLLocalDB` (de SQL Server Express 2014 o versiones posteriores).</span><span class="sxs-lookup"><span data-stu-id="8143d-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="8143d-180">Para más información acerca de las cadenas de conexión y las versiones de SQL Express, consulte [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb).</span><span class="sxs-lookup"><span data-stu-id="8143d-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="8143d-181">Agregar controlador Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-181">Add hello controller</span></span>
1. <span data-ttu-id="8143d-182">Presione **F6** proyecto de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="8143d-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="8143d-183">En **el Explorador de soluciones**, contextual hello **controladores** carpeta y elija **agregar**, **controlador**.</span><span class="sxs-lookup"><span data-stu-id="8143d-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Agregar controlador][cache-add-controller]
3. <span data-ttu-id="8143d-185">Seleccione **Controlador de MVC 5 con vistas que usa Entity Framework** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="8143d-186">Si se produce un error después de hacer clic **agregar**, asegúrese de que ha generado el proyecto de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="8143d-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Agregar controlador][cache-add-controller-class]
4. <span data-ttu-id="8143d-188">Seleccione **equipo (ContosoTeamStats.Models)** de hello **clase modelo** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="8143d-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="8143d-189">Seleccione **TeamContext (ContosoTeamStats.Models)** de hello **clase de contexto de datos** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="8143d-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="8143d-190">Tipo de `TeamsController` en hello **controlador** cuadro de texto Nombre (si no se rellena automáticamente).</span><span class="sxs-lookup"><span data-stu-id="8143d-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="8143d-191">Haga clic en **agregar** toocreate Hola clase de controlador y agregar vistas predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Configurar controlador][cache-configure-controller]
5. <span data-ttu-id="8143d-193">En **el Explorador de soluciones**, expanda **Global.asax** y haga doble clic en **Global.asax.cs** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="8143d-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="8143d-195">Agregar Hola siguiendo dos `using` instrucciones al principio de hello del archivo de hello en hello otro `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8143d-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="8143d-196">Agregar Hola después de la línea de código al final de Hola de hello `Application_Start` método.</span><span class="sxs-lookup"><span data-stu-id="8143d-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="8143d-197">En el **Explorador de soluciones**, expanda `App_Start` y haga doble clic en `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="8143d-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="8143d-199">Reemplace `controller = "Home"` Hola después el código de hello `RegisterRoutes` método con `controller = "Teams"` tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="8143d-200">Configurar vistas de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-200">Configure hello views</span></span>
1. <span data-ttu-id="8143d-201">En **el Explorador de soluciones**, expanda hello **vistas** hello carpeta y, a continuación, **Shared** carpeta y haga doble clic en **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="8143d-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="8143d-203">Cambiar contenido Hola de hello `title` elemento y reemplace `My ASP.NET Application` con `Contoso Team Stats` tal y como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="8143d-204">Hola `body` sección, actualice primero hello `Html.ActionLink` instrucción y reemplazar `Application name` con `Contoso Team Stats` y reemplace `Home` con `Teams`.</span><span class="sxs-lookup"><span data-stu-id="8143d-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="8143d-205">Antes: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="8143d-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="8143d-206">Después: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="8143d-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Cambios de código][cache-layout-cshtml-code]
2. <span data-ttu-id="8143d-208">Presione **CTRL+F5** toobuild y ejecutar una aplicación Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="8143d-209">Esta versión de la aplicación hello lee resultados Hola directamente desde la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="8143d-210">Hola Nota **crear nuevo**, **editar**, **detalles**, y **eliminar** las acciones que automáticamente agregan toohello aplicación Hola **Controlador de MVC 5 con vistas, mediante Entity Framework** scaffolding.</span><span class="sxs-lookup"><span data-stu-id="8143d-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="8143d-211">En la sección siguiente de Hola de tutorial Hola agregará acceso a datos de Hola de toooptimize de caché en Redis y proporcionan características adicionales de aplicaciones toohello.</span><span class="sxs-lookup"><span data-stu-id="8143d-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Aplicación de inicio][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="8143d-213">Configurar toouse de aplicación Hola caché en Redis</span><span class="sxs-lookup"><span data-stu-id="8143d-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="8143d-214">En esta sección del tutorial de hello, podrá configurar toostore de aplicación de ejemplo de Hola y recuperar las estadísticas de equipo Contoso de una instancia de caché en Redis de Azure mediante hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cliente de caché.</span><span class="sxs-lookup"><span data-stu-id="8143d-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="8143d-215">Configurar la aplicación de hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="8143d-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="8143d-216">Actualizar hello TeamsController clase tooreturn los resultados de caché de Hola o base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="8143d-217">Actualizar Hola crear, editar y eliminar métodos toowork con caché de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="8143d-218">Actualizar toowork de vista de índice de los equipos de hello con caché Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="8143d-219">Configurar la aplicación de hello toouse StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="8143d-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="8143d-220">tooconfigure una aplicación cliente en Visual Studio mediante Hola paquete de StackExchange.Redis NuGet, haga clic en **Administrador de paquetes de NuGet**, **Package Manager Console** de hello **herramientas** menú.</span><span class="sxs-lookup"><span data-stu-id="8143d-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="8143d-221">Ejecución hello después del comando de hello `Package Manager Console` ventana.</span><span class="sxs-lookup"><span data-stu-id="8143d-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="8143d-222">Hola NuGet paquete descarga y agrega Hola requiere referencias de ensamblado para su tooaccess de aplicación de cliente caché en Redis de Azure con el cliente de caché de StackExchange.Redis Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="8143d-223">Si prefiere una versión con nombre seguro de hello toouse `StackExchange.Redis` biblioteca de cliente, instalación hello `StackExchange.Redis.StrongName` paquete.</span><span class="sxs-lookup"><span data-stu-id="8143d-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="8143d-224">En **el Explorador de soluciones**, expanda hello **controladores** carpeta y haga doble clic en **TeamsController.cs** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="8143d-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![Controlador de equipos][cache-teamscontroller]
4. <span data-ttu-id="8143d-226">Agregar Hola siguiendo dos `using` instrucciones demasiado**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="8143d-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="8143d-227">Agregar Hola siguiendo dos toohello propiedades `TeamsController` clase.</span><span class="sxs-lookup"><span data-stu-id="8143d-227">Add hello following two properties toohello `TeamsController` class.</span></span>

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

6. <span data-ttu-id="8143d-228">Crear un archivo en el equipo denominado `WebAppPlusCacheAppSecrets.config` y lo coloca en una ubicación que no se comprueba con el código fuente de saludo de la aplicación de ejemplo, debe decidir toocheck en otra parte.</span><span class="sxs-lookup"><span data-stu-id="8143d-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="8143d-229">En este Hola ejemplo `AppSettingsSecrets.config` archivo se encuentra en `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="8143d-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="8143d-230">Editar hello `WebAppPlusCacheAppSecrets.config` de archivos y agregar Hola después de contenido.</span><span class="sxs-lookup"><span data-stu-id="8143d-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="8143d-231">Si ejecuta aplicación hello localmente esta información es instancia de caché en Redis de Azure tooyour tooconnect usado.</span><span class="sxs-lookup"><span data-stu-id="8143d-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="8143d-232">Más adelante en el tutorial Hola podrá aprovisionar una caché en Redis de Azure y actualice la contraseña y nombre de la memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="8143d-233">Si no tiene pensado toorun aplicación de ejemplo de Hola localmente puede omitir la creación de hello de este archivo y los pasos subsiguientes de Hola que hacen referencia a archivo hello, porque cuando se implementa la aplicación de hello tooAzure recupera información de conexión de caché de Hola de aplicación hello configuración para la aplicación Web de hello y no desde este archivo.</span><span class="sxs-lookup"><span data-stu-id="8143d-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="8143d-234">Desde hello `WebAppPlusCacheAppSecrets.config` no se ha implementado tooAzure con la aplicación, no es necesario a menos que vayan toorun aplicación de hello localmente.</span><span class="sxs-lookup"><span data-stu-id="8143d-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="8143d-235">En **el Explorador de soluciones**, haga doble clic en **web.config** tooopen lo.</span><span class="sxs-lookup"><span data-stu-id="8143d-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="8143d-237">Agregue los siguiente hello `file` atributo toohello `appSettings` elemento.</span><span class="sxs-lookup"><span data-stu-id="8143d-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="8143d-238">Si utiliza un nombre de archivo diferente o una ubicación, sustituya esos valores para que se muestran en el ejemplo de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="8143d-239">Antes: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="8143d-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="8143d-240">Después: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="8143d-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="8143d-241">en tiempo de ejecución ASP.NET de Hello combina el contenido de Hola de archivo externos de hello con marcado Hola Hola `<appSettings>` elemento.</span><span class="sxs-lookup"><span data-stu-id="8143d-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="8143d-242">en tiempo de ejecución de Hello omite el atributo de archivo de hello si no se encuentra el archivo especificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="8143d-243">Los secretos (caché de tooyour de cadena de conexión de hello) no se incluyen como parte del código fuente de hello para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="8143d-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="8143d-244">Al implementar su tooAzure de aplicación web, Hola `WebAppPlusCacheAppSecrests.config` no se implementarán archivo (es decir, lo que desea).</span><span class="sxs-lookup"><span data-stu-id="8143d-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="8143d-245">Hay varias toospecify formas estos secretos en Azure y, en este tutorial se configuran automáticamente para cuando se [aprovisionar Hola recursos de Azure](#provision-the-azure-resources) en un paso posterior del tutorial.</span><span class="sxs-lookup"><span data-stu-id="8143d-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="8143d-246">Para obtener más información sobre cómo trabajar con secretos en Azure, consulte [las prácticas recomendadas para la implementación de las contraseñas y otros datos confidenciales tooASP.NET y servicio de aplicaciones de Azure](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="8143d-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="8143d-247">Actualizar hello TeamsController clase tooreturn los resultados de caché de Hola o base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="8143d-248">En este ejemplo, se pueden recuperar estadísticas de equipo de base de datos de Hola o desde la caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="8143d-249">Estadísticas de equipo se almacenan en caché de Hola como un número de serie `List<Team>`y también como un conjunto ordenado con tipos de datos de Redis.</span><span class="sxs-lookup"><span data-stu-id="8143d-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="8143d-250">Al recuperar elementos de un conjunto ordenado, puede recuperar algunos, todos o consultar algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="8143d-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="8143d-251">En este ejemplo, podrá consultar conjunto Hola ordenado para hello top 5 los equipos ordenados según el número de wins.</span><span class="sxs-lookup"><span data-stu-id="8143d-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="8143d-252">No es necesario toostore Hola estadísticas de equipo en varios formatos en memoria caché de hello en orden toouse caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="8143d-253">Este tutorial usa varios toodemonstrate formatos algunas de maneras diferentes de Hola y distintos tipos de datos puede usar datos de toocache.</span><span class="sxs-lookup"><span data-stu-id="8143d-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="8143d-254">Agregue los siguiente Hola `using` instrucciones toohello `TeamsController.cs` archivo en la parte superior de hello con hello otro `using` instrucciones.</span><span class="sxs-lookup"><span data-stu-id="8143d-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="8143d-255">Reemplazar actual hello `public ActionResult Index()` implementación del método con hello después de la implementación.</span><span class="sxs-lookup"><span data-stu-id="8143d-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

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


1. <span data-ttu-id="8143d-256">Agregar Hola después de tres toohello métodos `TeamsController` Hola de clase tooimplement `playGames`, `clearCache`, y `rebuildDB` tipos de acciones de hello switch (instrucción) agregada en el fragmento de código anterior de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="8143d-257">Hola `PlayGames` método actualiza las estadísticas de equipo de hello, simulando una temporada de juegos, guarda Hola base de datos de resultados toohello y borra Hola han quedado obsoletas en datos de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="8143d-258">Hola `RebuildDB` base de datos de método reinicializa Hola conjunto predeterminado de Hola de equipos, genera estadísticas para ellos y borra Hola han quedado obsoletas en datos de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

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

    <span data-ttu-id="8143d-259">Hola `ClearCachedTeams` método quita las estadísticas de equipo almacenado en caché de memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="8143d-260">Agregar Hola después de cuatro toohello métodos `TeamsController` hello de la clase tooimplement distintas maneras de recuperar las estadísticas de equipo de Hola de caché de Hola y de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="8143d-261">Cada uno de estos métodos devuelve una `List<Team>` que se muestra a continuación, vista de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="8143d-262">Hola `GetFromDB` método lee las estadísticas de equipo de Hola de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
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

    <span data-ttu-id="8143d-263">Hola `GetFromList` método lee las estadísticas de equipo de Hola de memoria caché como un número de serie `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="8143d-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="8143d-264">Si se produce un error de caché, estadísticas de equipo de Hola se leen desde la base de datos de hello y, a continuación, se almacena en caché de Hola durante la próxima vez.</span><span class="sxs-lookup"><span data-stu-id="8143d-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="8143d-265">En este ejemplo usamos JSON.NET serialización tooserialize Hola .NET objetos tooand de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="8143d-266">Para obtener más información, consulte [cómo los objetos en caché en Redis de Azure toowork con .NET](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="8143d-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

    <span data-ttu-id="8143d-267">Hola `GetFromSortedSet` método lee las estadísticas de equipo de Hola de un conjunto ordenado en caché.</span><span class="sxs-lookup"><span data-stu-id="8143d-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="8143d-268">Si se produce un error de caché, estadísticas de equipo de Hola se leen de base de datos de Hola y almacenadas en memoria caché de Hola como un conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="8143d-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

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

    <span data-ttu-id="8143d-269">Hola `GetFromSortedSetTop5` método lee conjunto superior de 5 equipos de hello en caché ordenados de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="8143d-270">Se inicia mediante la comprobación de caché de hello existencia Hola de hello `teamsSortedSet` clave.</span><span class="sxs-lookup"><span data-stu-id="8143d-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="8143d-271">Si esta clave no está presente, Hola `GetFromSortedSet` método se llama tooread estadísticas de equipo de Hola y almacenarlos en caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="8143d-272">A continuación, hello conjunto ordenado en caché se consulta para hello top 5 los equipos que se devuelven.</span><span class="sxs-lookup"><span data-stu-id="8143d-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

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

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="8143d-273">Actualizar Hola crear, editar y eliminar métodos toowork con caché de Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="8143d-274">código de scaffolding de Hola que se generó como parte de este ejemplo incluye los métodos tooadd, editar y eliminar los equipos.</span><span class="sxs-lookup"><span data-stu-id="8143d-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="8143d-275">Cada vez que un equipo es agregar, editar o quitar, datos de hello en memoria caché de Hola quedan anticuados.</span><span class="sxs-lookup"><span data-stu-id="8143d-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="8143d-276">En esta sección, modificará estos hello tooclear de tres métodos en caché los equipos para que no se sincronizado con la base de datos de hello caché Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="8143d-277">Examinar toohello `Create(Team team)` método Hola `TeamsController` clase.</span><span class="sxs-lookup"><span data-stu-id="8143d-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="8143d-278">Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="8143d-279">Examinar toohello `Edit(Team team)` método Hola `TeamsController` clase.</span><span class="sxs-lookup"><span data-stu-id="8143d-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="8143d-280">Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


1. <span data-ttu-id="8143d-281">Examinar toohello `DeleteConfirmed(int id)` método Hola `TeamsController` clase.</span><span class="sxs-lookup"><span data-stu-id="8143d-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="8143d-282">Agregar una llamada toohello `ClearCachedTeams` método, como se muestra en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

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


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="8143d-283">Actualizar toowork de vista de índice de los equipos de hello con caché Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="8143d-284">En **el Explorador de soluciones**, expanda hello **vistas** carpeta y, a continuación, hello **equipos** carpeta y haga doble clic en **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="8143d-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="8143d-286">Cerca de hello parte superior del archivo hello, busque Hola siguiente elemento de párrafo.</span><span class="sxs-lookup"><span data-stu-id="8143d-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Tabla de acciones][cache-teams-index-table]
   
    <span data-ttu-id="8143d-288">Se trata de hello vínculo toocreate un nuevo equipo.</span><span class="sxs-lookup"><span data-stu-id="8143d-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="8143d-289">Reemplace el elemento de párrafo de hello con hello en la tabla siguiente.</span><span class="sxs-lookup"><span data-stu-id="8143d-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="8143d-290">Esta tabla tiene vínculos de acción para crear un nuevo equipo, reproducir una nueva estación de juegos, borrar la memoria caché de hello, recuperar los equipos de Hola de caché de hello en varios formatos, recuperar los equipos de Hola de base de datos de Hola y volver a generar Hola base de datos con datos de ejemplo nueva.</span><span class="sxs-lookup"><span data-stu-id="8143d-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

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


1. <span data-ttu-id="8143d-291">Desplazar hacia abajo de toohello de hello **Index.cshtml** de archivos y agregue Hola siguiente `tr` elemento para que sea la última fila de Hola Hola última tabla archivo hello.</span><span class="sxs-lookup"><span data-stu-id="8143d-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="8143d-292">Esta fila muestra el valor de Hola de `ViewBag.Msg` que contiene un informe de estado sobre la operación actual de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="8143d-293">Hola `ViewBag.Msg` se establece al hacer clic en cualquiera de los vínculos de acción de hello del paso anterior Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Mensaje de estado][cache-status-message]
2. <span data-ttu-id="8143d-295">Presione **F6** proyecto de hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="8143d-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="8143d-296">Aprovisionar Hola recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="8143d-296">Provision hello Azure resources</span></span>
<span data-ttu-id="8143d-297">toohost su aplicación en Azure, primero debe aprovisionar Hola servicios de Azure que requiera la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8143d-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="8143d-298">aplicación de ejemplo de Hola en este tutorial usa Hola después de los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="8143d-299">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="8143d-299">Azure Redis Cache</span></span>
* <span data-ttu-id="8143d-300">Aplicación web del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="8143d-300">App Service Web App</span></span>
* <span data-ttu-id="8143d-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="8143d-301">SQL Database</span></span>

<span data-ttu-id="8143d-302">toodeploy estos grupo de recursos nuevos o existentes de tooa de servicios de su elección, haga clic en hello después **implementar tooAzure** botón.</span><span class="sxs-lookup"><span data-stu-id="8143d-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="8143d-303">[! [Implementar tooAzure] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8143d-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="8143d-304">Esto **implementar tooAzure** botón usa hello [crear una aplicación Web más caché en Redis más base de datos SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates) plantilla tooprovision estos servicios y el conjunto de Hola cadena de conexión de configuración de aplicación de hello hello y base de datos SQL para hello cadena de conexión de caché en Redis de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="8143d-305">Si no tiene ninguna cuenta de Azure, puede [crear una gratis](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en unos minutos.</span><span class="sxs-lookup"><span data-stu-id="8143d-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="8143d-306">Si hace clic en hello **implementar tooAzure** botón toma toohello portal de Azure e inicia Hola el proceso de creación de recursos de hello descritos por plantilla de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![Implementar tooAzure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="8143d-308">Hola **Fundamentos** sección, seleccione hello toouse de suscripción de Azure, seleccione un grupo de recursos existente o cree uno nuevo y especificar la ubicación del grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="8143d-309">Hola **configuración** sección, especifique un **inicio de sesión de administrador** (no use **administración**), **contraseña de inicio de sesión de administrador**y  **Nombre de la base de datos**.</span><span class="sxs-lookup"><span data-stu-id="8143d-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="8143d-310">Hola se configuran otros parámetros para un servicio gratuito de aplicación aloja el plan y las opciones de bajo costo para Hola base de datos SQL y de caché en Redis de Azure, que no tiene un nivel gratis.</span><span class="sxs-lookup"><span data-stu-id="8143d-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Implementar tooAzure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="8143d-312">Después de establecer la configuración de hello deseado, desplácese toohello final de página de hello, términos de lectura hello y condiciones y comprobar hello **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="8143d-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="8143d-313">Haga clic en toobegin aprovisionar recursos de hello, **compra**.</span><span class="sxs-lookup"><span data-stu-id="8143d-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="8143d-314">progreso de hello tooview de la implementación, haga clic en el icono de notificación de Hola y haga clic en **implementación iniciada**.</span><span class="sxs-lookup"><span data-stu-id="8143d-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Implementación iniciada][cache-deployment-started]

<span data-ttu-id="8143d-316">Puede ver estado de saludo de la implementación en hello **Microsoft.Template** hoja.</span><span class="sxs-lookup"><span data-stu-id="8143d-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![Implementar tooAzure][cache-deploy-to-azure-step-3]

<span data-ttu-id="8143d-318">Cuando se complete el aprovisionamiento, puede publicar su tooAzure de aplicación desde Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8143d-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="8143d-319">Se muestran los errores que pueden producirse durante el proceso de aprovisionamiento de hello en hello **Microsoft.Template** hoja.</span><span class="sxs-lookup"><span data-stu-id="8143d-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="8143d-320">Algunos errores comunes son demasiadas instancias de SQL Server o demasiados planes de hospedaje del Servicio de aplicaciones gratis por suscripción.</span><span class="sxs-lookup"><span data-stu-id="8143d-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="8143d-321">Resuelva los errores y reinicie el proceso de hello haciendo clic en **volver a implementar** en hello **Microsoft.Template** hoja o hello **implementar tooAzure** botón en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8143d-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="8143d-322">Publicar tooAzure de aplicación Hola</span><span class="sxs-lookup"><span data-stu-id="8143d-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="8143d-323">En este paso del tutorial de hello, podrá publicar Hola aplicación tooAzure y ejecútelo en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="8143d-324">Menú contextual hello **ContosoTeamStats** proyecto en Visual Studio y elija **publicar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publicar][cache-publish-app]
2. <span data-ttu-id="8143d-326">Haga clic en **Microsoft Azure App Service**, elija **Seleccionar existente** y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publicar][cache-publish-to-app-service]
3. <span data-ttu-id="8143d-328">Seleccione la suscripción de hello usa al crear Hola recursos de Azure, expanda el grupo de recursos de Hola que contienen recursos de Hola y Hola seleccione deseado de aplicación Web.</span><span class="sxs-lookup"><span data-stu-id="8143d-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="8143d-329">Si usa hello **implementar tooAzure** el nombre de la aplicación Web se inicia con el botón **sitio Web** seguido de algunos caracteres adicionales.</span><span class="sxs-lookup"><span data-stu-id="8143d-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Seleccionar aplicación web][cache-select-web-app]
4. <span data-ttu-id="8143d-331">Haga clic en **Aceptar** hello toobegin proceso de publicación.</span><span class="sxs-lookup"><span data-stu-id="8143d-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="8143d-332">Transcurridos unos instantes completa Hola proceso de publicación y se inicie un explorador con hello ejecutando la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="8143d-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="8143d-333">Si obtiene un error al validar o publicación de DNS y Hola proceso para el aprovisionamiento hello recursos de Azure para la aplicación hello recientemente finalizó, espere unos instantes y vuelva a intentarlo.</span><span class="sxs-lookup"><span data-stu-id="8143d-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Caché agregada][cache-added-to-application]

<span data-ttu-id="8143d-335">Hello siguiente tabla describe cada vínculo de acción de la aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="8143d-336">Acción</span><span class="sxs-lookup"><span data-stu-id="8143d-336">Action</span></span> | <span data-ttu-id="8143d-337">Descripción</span><span class="sxs-lookup"><span data-stu-id="8143d-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8143d-338">Crear nuevo</span><span class="sxs-lookup"><span data-stu-id="8143d-338">Create New</span></span> |<span data-ttu-id="8143d-339">Crear un nuevo equipo.</span><span class="sxs-lookup"><span data-stu-id="8143d-339">Create a new Team.</span></span> |
| <span data-ttu-id="8143d-340">Reproducir temporada</span><span class="sxs-lookup"><span data-stu-id="8143d-340">Play Season</span></span> |<span data-ttu-id="8143d-341">Reproducir una temporada de juegos, estadísticas de equipo de Hola de actualización, y desactive cualquiera obsoleto datos de equipo de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="8143d-342">Borrar caché</span><span class="sxs-lookup"><span data-stu-id="8143d-342">Clear Cache</span></span> |<span data-ttu-id="8143d-343">Estadísticas del equipo desactive Hola de caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="8143d-344">Mostrar de la caché</span><span class="sxs-lookup"><span data-stu-id="8143d-344">List from Cache</span></span> |<span data-ttu-id="8143d-345">Recuperar estadísticas de equipo de Hola de memoria caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="8143d-346">Si se produce un error de caché, estadísticas de Hola de carga de base de datos de Hola y guarde toohello caché para la próxima vez.</span><span class="sxs-lookup"><span data-stu-id="8143d-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="8143d-347">Conjunto ordenado de caché</span><span class="sxs-lookup"><span data-stu-id="8143d-347">Sorted Set from Cache</span></span> |<span data-ttu-id="8143d-348">Recuperar estadísticas de equipo de Hola desde caché de hello utilizando un conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="8143d-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="8143d-349">Si se produce un error de caché, cargue estadísticas de Hola de base de datos de Hola y guardar la memoria caché de toohello mediante un conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="8143d-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="8143d-350">5 equipos principales de la caché</span><span class="sxs-lookup"><span data-stu-id="8143d-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="8143d-351">Recuperar los equipos de 5 superior Hola desde caché de hello utilizando un conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="8143d-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="8143d-352">Si se produce un error de caché, cargue estadísticas de Hola de base de datos de Hola y guardar la memoria caché de toohello mediante un conjunto ordenado.</span><span class="sxs-lookup"><span data-stu-id="8143d-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="8143d-353">Cargar de la base de datos</span><span class="sxs-lookup"><span data-stu-id="8143d-353">Load from DB</span></span> |<span data-ttu-id="8143d-354">Recuperar estadísticas de equipo de Hola de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="8143d-355">Recompilar base de datos</span><span class="sxs-lookup"><span data-stu-id="8143d-355">Rebuild DB</span></span> |<span data-ttu-id="8143d-356">Volver a generar la base de datos de Hola y cargarla con datos de ejemplo de equipo.</span><span class="sxs-lookup"><span data-stu-id="8143d-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="8143d-357">Editar, Detalles, Eliminar</span><span class="sxs-lookup"><span data-stu-id="8143d-357">Edit / Details / Delete</span></span> |<span data-ttu-id="8143d-358">Editar un equipo, ver los detalles de un equipo, eliminar un equipo.</span><span class="sxs-lookup"><span data-stu-id="8143d-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="8143d-359">Haga clic en algunas de las acciones de Hola y experimentar con la recuperación de datos de Hola de orígenes diferentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="8143d-360">No hello las diferencias en hello tarda toocomplete Hola varias maneras de recuperar datos de Hola de base de datos de Hola y caché de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="8143d-361">Eliminar recursos de hello cuando haya terminado con la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="8143d-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="8143d-362">Cuando haya terminado con la aplicación de tutorial de ejemplo de Hola, puede eliminar hello Azure utilizados en tooconserve de orden de costo de recursos y recursos.</span><span class="sxs-lookup"><span data-stu-id="8143d-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="8143d-363">Si usas hello **implementar tooAzure** botón en hello [Hola de aprovisionar recursos de Azure](#provision-the-azure-resources) sección y todos los recursos están contenidos en hello mismo grupo de recursos, puede eliminarlos de forma conjunta en uno operación mediante la eliminación de grupo de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="8143d-364">Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y haga clic en **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="8143d-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="8143d-365">Nombre del tipo hello de su grupo de recursos en hello **filtrar elementos...**  cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="8143d-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="8143d-366">Haga clic en **...**  toohello derecha de su grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8143d-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="8143d-367">Hacer clic en **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-367">Click **Delete**.</span></span>
   
    ![Eliminar][cache-delete-resource-group]
5. <span data-ttu-id="8143d-369">Nombre del tipo hello de su grupo de recursos y haga clic en **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="8143d-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![Confirmar eliminación][cache-delete-confirm]

<span data-ttu-id="8143d-371">Después de unos pocos recursos de hello momentos se eliminan grupo y todos sus recursos independientes.</span><span class="sxs-lookup"><span data-stu-id="8143d-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8143d-372">Tenga en cuenta que la eliminación de un grupo de recursos es irreversible y ese grupo de recursos de Hola y todos los recursos de hello en él se eliminan permanentemente.</span><span class="sxs-lookup"><span data-stu-id="8143d-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="8143d-373">Asegúrese de que no elimina accidentalmente grupo de recursos incorrecto de Hola o de recursos.</span><span class="sxs-lookup"><span data-stu-id="8143d-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="8143d-374">Si crea recursos de Hola para hospedar este ejemplo dentro de un grupo de recursos existente, puede eliminar cada recurso individualmente de sus módulos respectivos.</span><span class="sxs-lookup"><span data-stu-id="8143d-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="8143d-375">Ejecutar la aplicación de ejemplo de Hola en el equipo local</span><span class="sxs-lookup"><span data-stu-id="8143d-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="8143d-376">aplicación de hello toorun localmente en su equipo, necesita una caché en Redis de Azure de la instancia en qué toocache los datos.</span><span class="sxs-lookup"><span data-stu-id="8143d-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="8143d-377">Si ha publicado su aplicación tooAzure tal y como se describe en la sección anterior de hello, puede usar la instancia de caché en Redis de Azure de Hola que se haya proporcionado durante ese paso.</span><span class="sxs-lookup"><span data-stu-id="8143d-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="8143d-378">Si tiene otra instancia de caché en Redis de Azure existente, puede utilizar ese toorun este ejemplo localmente.</span><span class="sxs-lookup"><span data-stu-id="8143d-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="8143d-379">Si necesita toocreate una instancia de caché en Redis de Azure, puede seguir los pasos de hello en [crear una memoria caché](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="8143d-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="8143d-380">Una vez que ha seleccionado o creado Hola caché toouse, examinar la caché de toohello Hola portal de Azure y recuperar hello [nombre de host](cache-configure.md#properties) y [las claves de acceso](cache-configure.md#access-keys) de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="8143d-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="8143d-381">Para obtener instrucciones, consulte [Configuración de opciones de la memoria caché en Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="8143d-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="8143d-382">Abra Hola `WebAppPlusCacheAppSecrets.config` archivo que creó durante la hello [configurar toouse de aplicación Hola caché en Redis](#configure-the-application-to-use-redis-cache) paso de este tutorial con hello editor de su elección.</span><span class="sxs-lookup"><span data-stu-id="8143d-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="8143d-383">Editar hello `value` de atributo y reemplace `MyCache.redis.cache.windows.net` con hello [nombre de host](cache-configure.md#properties) de la memoria caché y especificar cualquier hello [clave primaria o secundaria](cache-configure.md#access-keys) de la memoria caché como contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="8143d-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="8143d-384">Presione **CTRL+F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8143d-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="8143d-385">Tenga en cuenta que porque la aplicación hello, incluida la base de datos de hello, se ejecuta localmente y hello caché en Redis hospedada en Azure, Hola caché puede aparecer toounder-realizar Hola bases de datos.</span><span class="sxs-lookup"><span data-stu-id="8143d-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="8143d-386">Para obtener el mejor rendimiento, Hola aplicación cliente y debe ser instancia de caché en Redis de Azure en hello misma ubicación.</span><span class="sxs-lookup"><span data-stu-id="8143d-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8143d-387">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8143d-387">Next steps</span></span>
* <span data-ttu-id="8143d-388">Obtenga más información sobre [Introducción a ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) en hello [ASP.NET](http://asp.net/) sitio.</span><span class="sxs-lookup"><span data-stu-id="8143d-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="8143d-389">Para obtener más ejemplos de creación de una aplicación Web ASP.NET en el servicio de aplicaciones, consulte [crear e implementar una aplicación web ASP.NET en el servicio de aplicación de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) conectar 2015 [demostración](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="8143d-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="8143d-390">Encontrará tutoriales más rápidos de demostración de hello HealthClinic.biz, [tutoriales de herramientas de desarrollador de Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="8143d-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="8143d-391">Obtener más información sobre hello [código primera tooa nueva base de datos](https://msdn.microsoft.com/data/jj193542) enfocar tooEntity marco de trabajo que se utiliza en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8143d-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="8143d-392">Más información sobre las [aplicaciones web del Servicio de aplicaciones de Azure](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8143d-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="8143d-393">Obtenga información acerca de cómo demasiado[monitor](cache-how-to-monitor.md) la memoria caché en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8143d-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="8143d-394">Exploración de las características premium de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="8143d-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="8143d-395">La persistencia de tooconfigure para una caché en Redis de Azure Premium</span><span class="sxs-lookup"><span data-stu-id="8143d-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="8143d-396">¿Cómo tooconfigure agrupación en clústeres para una caché en Redis de Azure Premium</span><span class="sxs-lookup"><span data-stu-id="8143d-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="8143d-397">¿Cómo admiten tooconfigure red Virtual para una caché de Redis de Azure Premium</span><span class="sxs-lookup"><span data-stu-id="8143d-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="8143d-398">Vea hello [preguntas más frecuentes de caché de Redis Azure](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) para obtener más detalles sobre el tamaño, el rendimiento y el ancho de banda con las cachés premium.</span><span class="sxs-lookup"><span data-stu-id="8143d-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

