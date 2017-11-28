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
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="bbbfc-103">Compilación de una aplicación ASP.NET en Azure con SQL Database</span><span class="sxs-lookup"><span data-stu-id="bbbfc-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="bbbfc-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) proporciona un servicio de hospedaje web muy escalable y con aplicación de revisiones de un modo automático.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="bbbfc-105">Este tutorial muestra cómo toodeploy un ASP.NET controladas por datos web de aplicación en Azure y conéctela demasiado[base de datos de SQL Azure](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="bbbfc-106">Cuando haya terminado, tendrá una aplicación ASP.NET que se ejecuta en [servicio de aplicaciones de Azure](../app-service/app-service-value-prop-what-is.md) y conectado tooSQL base de datos.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Aplicación ASP.NET publicada en la aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="bbbfc-108">En este tutorial, aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbbfc-109">Crear una base de datos SQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="bbbfc-110">Conectar un tooSQL de aplicación ASP.NET base de datos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="bbbfc-111">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bbbfc-112">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bbbfc-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="bbbfc-113">Registros de flujo de Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="bbbfc-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="bbbfc-114">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbbfc-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-115">Prerequisites</span></span>

<span data-ttu-id="bbbfc-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="bbbfc-117">Instalar [2017 de Visual Studio](https://www.visualstudio.com/downloads/) con hello siguiendo las cargas de trabajo:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="bbbfc-118">**ASP.NET y desarrollo web**</span><span class="sxs-lookup"><span data-stu-id="bbbfc-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="bbbfc-119">**Desarrollo de Azure**</span><span class="sxs-lookup"><span data-stu-id="bbbfc-119">**Azure development**</span></span>

  ![ASP.NET y desarrollo web y desarrollo de Azure (en web y en la nube)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="bbbfc-121">Descargar el ejemplo hello</span><span class="sxs-lookup"><span data-stu-id="bbbfc-121">Download hello sample</span></span>

<span data-ttu-id="bbbfc-122">[Descargar el proyecto de ejemplo de Hola](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="bbbfc-123">Extraer (Descomprimir) hello *master.zip-dotnet-sqldb-tutorial* archivo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="bbbfc-124">proyecto de ejemplo de Hola contiene básico [ASP.NET MVC](https://www.asp.net/mvc) aplicación CRUD (crear-lectura-actualización-eliminación) con [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="bbbfc-125">Ejecutar aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bbbfc-125">Run hello app</span></span>

<span data-ttu-id="bbbfc-126">Abra hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* archivo en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="bbbfc-127">Tipo `Ctrl+F5` toorun Hola aplicación sin depuración.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="bbbfc-128">aplicación Hello se muestra en el explorador predeterminado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="bbbfc-129">Seleccione hello **crear nuevo** vincular y crear un par *tareas* elementos.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Cuadro de diálogo New ASP.NET Project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="bbbfc-131">Hola de prueba **editar**, **detalles**, y **eliminar** vínculos.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="bbbfc-132">aplicación Hello usa un tooconnect de contexto de base de datos con la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="bbbfc-133">En este ejemplo, el contexto de base de datos de hello usa una cadena de conexión denominada `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="bbbfc-134">cadena de conexión de Hola se establecerá en hello *Web.config* de archivos y que se hace referencia en hello *Models/MyDatabaseContext.cs* archivo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="bbbfc-135">nombre de cadena de conexión de Hola se utiliza más adelante en hello tooconnect tutorial hello web de Azure aplicación tooan base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="bbbfc-136">Publicar tooAzure con base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bbbfc-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="bbbfc-137">Hola **el Explorador de soluciones**, haga clic en el **DotNetAppSqlDb** de proyecto y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publicar desde el Explorador de soluciones](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="bbbfc-139">Asegúrese de que **Microsoft Azure App Service** está seleccionado y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publicar desde la página de información general del proyecto](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="bbbfc-141">Publicación abre hello **crear servicio en la aplicación** cuadro de diálogo, lo que ayuda a crear todos los Hola recursos de Azure necesita toorun la aplicación web ASP.NET en Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="bbbfc-142">Inicie sesión en tooAzure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-142">Sign in tooAzure</span></span>

<span data-ttu-id="bbbfc-143">Hola **crear servicio en la aplicación** cuadro de diálogo, haga clic en **agregar una cuenta**y, a continuación, inicie sesión en tooyour suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="bbbfc-144">Si ya ha iniciado sesión en una cuenta de Microsoft, asegúrese de que esa cuenta contiene la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="bbbfc-145">Si inició sesión Hola cuenta Microsoft no tiene su suscripción de Azure, haga clic en él cuenta correcta de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Inicie sesión en tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="bbbfc-147">Una vez iniciado sesión, está listo toocreate que Hola a todos los recursos que necesita para la aplicación web de Azure en este cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="bbbfc-148">Configurar el nombre de la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bbbfc-148">Configure hello web app name</span></span>

<span data-ttu-id="bbbfc-149">Puede mantener el nombre de la aplicación hello generado o cambiar nombre único de tooanother (caracteres válidos son `a-z`, `0-9`, y `-`).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="bbbfc-150">nombre de la aplicación Hello se usa como parte de la dirección URL predeterminada de hello para la aplicación (`<app_name>.azurewebsites.net`, donde `<app_name>` es el nombre de la aplicación web).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="bbbfc-151">nombre de la aplicación Hello debe toobe único en todas las aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Cuadro de diálogo Create App Service (Crear App Service)](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="bbbfc-153">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="bbbfc-154">Siguiente demasiado**grupo de recursos**, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-154">Next too**Resource Group**, click **New**.</span></span>

![TooResource siguiente grupo, haga clic en nuevo.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="bbbfc-156">Grupo de recursos de nombre hello **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="bbbfc-157">No haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-157">Do not click **Create**.</span></span> <span data-ttu-id="bbbfc-158">En primer lugar debe tooset una base de datos SQL en un paso posterior.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="bbbfc-159">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="bbbfc-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="bbbfc-160">Siguiente demasiado**Plan de servicio de aplicaciones**, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="bbbfc-161">Hola **configurar un Plan de servicio de aplicaciones** cuadro de diálogo Configurar nuevo plan de servicio de aplicaciones Hola con hello después de configuración:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Creación de un plan de App Service](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="bbbfc-163">Configuración</span><span class="sxs-lookup"><span data-stu-id="bbbfc-163">Setting</span></span>  | <span data-ttu-id="bbbfc-164">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="bbbfc-164">Suggested value</span></span> | <span data-ttu-id="bbbfc-165">Para obtener más información</span><span class="sxs-lookup"><span data-stu-id="bbbfc-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="bbbfc-166">**Plan de App Service**</span><span class="sxs-lookup"><span data-stu-id="bbbfc-166">**App Service Plan**</span></span>| <span data-ttu-id="bbbfc-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="bbbfc-167">myAppServicePlan</span></span> | [<span data-ttu-id="bbbfc-168">Planes de App Service</span><span class="sxs-lookup"><span data-stu-id="bbbfc-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="bbbfc-169">**Ubicación**</span><span class="sxs-lookup"><span data-stu-id="bbbfc-169">**Location**</span></span>| <span data-ttu-id="bbbfc-170">Europa occidental</span><span class="sxs-lookup"><span data-stu-id="bbbfc-170">West Europe</span></span> | [<span data-ttu-id="bbbfc-171">Regiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="bbbfc-172">**Tamaño**</span><span class="sxs-lookup"><span data-stu-id="bbbfc-172">**Size**</span></span>| <span data-ttu-id="bbbfc-173">Gratuito</span><span class="sxs-lookup"><span data-stu-id="bbbfc-173">Free</span></span> | [<span data-ttu-id="bbbfc-174">Planes de tarifa</span><span class="sxs-lookup"><span data-stu-id="bbbfc-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="bbbfc-175">Creación de una instancia de SQL Server</span><span class="sxs-lookup"><span data-stu-id="bbbfc-175">Create a SQL Server instance</span></span>

<span data-ttu-id="bbbfc-176">Antes de crear una base de datos, necesita un [servidor lógico de Azure SQL Database](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="bbbfc-177">Un servidor lógico contiene un conjunto de bases de datos administradas como un grupo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="bbbfc-178">Seleccione **Explorar otros servicios de Azure**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-178">Select **Explore additional Azure services**.</span></span>

![Configurar el nombre de la aplicación web](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="bbbfc-180">Hola **servicios** , haga clic en hello  **+**  icono siguiente demasiado**base de datos SQL**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![En la ficha de servicios de hello, haga clic en icono + hello tooSQL siguiente base de datos.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="bbbfc-182">Hola **Configurar base de datos de SQL** cuadro de diálogo, haga clic en **New** siguiente demasiado**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="bbbfc-183">Se genera un nombre de servidor único.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-183">A unique server name is generated.</span></span> <span data-ttu-id="bbbfc-184">Este nombre se usa como parte de la dirección URL predeterminada de hello para el servidor lógico, `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="bbbfc-185">Debe ser único entre todas las instancias de servidor lógico de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="bbbfc-186">Puede cambiar el nombre del servidor de hello, pero para este tutorial, mantenga el valor de hello generado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="bbbfc-187">Agregue un nombre de usuario y una contraseña de administrador y luego seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="bbbfc-188">Para conocer los requisitos de complejidad de la contraseña, consulte [Directivas de contraseñas](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="bbbfc-189">Recuerde este nombre de usuario y esta contraseña.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-189">Remember this username and password.</span></span> <span data-ttu-id="bbbfc-190">Necesite servidor lógico de toomanage Hola instancia posteriormente.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-190">You need them toomanage hello logical server instance later.</span></span>

![Creación de una instancia de SQL Server](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="bbbfc-192">una Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bbbfc-192">Create a SQL Database</span></span>

<span data-ttu-id="bbbfc-193">Hola **Configurar base de datos de SQL** cuadro de diálogo:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="bbbfc-194">Mantener generada de manera predeterminada hello **nombre de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="bbbfc-195">En **Nombre de la cadena de conexión**, escriba *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="bbbfc-196">Este nombre debe coincidir con la cadena de conexión de Hola que se hace referencia en *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="bbbfc-197">Seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-197">Select **OK**.</span></span>

![Configuración de SQL Database](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="bbbfc-199">Hola **crear servicio en la aplicación** cuadro de diálogo muestra los recursos de Hola que haya creado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="bbbfc-200">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-200">Click **Create**.</span></span> 

![recursos de Hola que ha creado](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="bbbfc-202">Una vez que finalice el Asistente de hello, crear recursos de Azure de hello, publica su tooAzure de aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="bbbfc-203">El explorador predeterminado se inicia con la aplicación toohello implementado de hello dirección URL.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="bbbfc-204">Agregue algunos elementos de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-204">Add a few to-do items.</span></span>

![Aplicación ASP.NET publicada en la aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="bbbfc-206">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="bbbfc-206">Congratulations!</span></span> <span data-ttu-id="bbbfc-207">La aplicación ASP.NET orientada a datos se ejecuta en directo en Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="bbbfc-208">Hola de acceso base de datos SQL localmente</span><span class="sxs-lookup"><span data-stu-id="bbbfc-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="bbbfc-209">Visual Studio le permite explorar y administrar la base de datos SQL nueva fácilmente en hello **Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="bbbfc-210">Creación de una conexión de base de datos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-210">Create a database connection</span></span>

<span data-ttu-id="bbbfc-211">De hello **vista** menú, seleccione **Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="bbbfc-212">En la parte superior de Hola de **Explorador de objetos de SQL Server**, haga clic en hello **agregar SQL Server** botón.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="bbbfc-213">Configurar conexión de base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="bbbfc-213">Configure hello database connection</span></span>

<span data-ttu-id="bbbfc-214">Hola **conectar** cuadro de diálogo, expanda hello **Azure** nodo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="bbbfc-215">Aquí se muestran todas las instancias de SQL Database de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="bbbfc-216">Seleccione hello `DotNetAppSqlDb` base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="bbbfc-217">conexión de Hola que creó anteriormente se rellena automáticamente en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="bbbfc-218">Escriba la contraseña de administrador de base de datos de Hola que creó anteriormente y haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Configuración de la conexión de base de datos de Visual Studio](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="bbbfc-220">Permitir la conexión de cliente desde el equipo</span><span class="sxs-lookup"><span data-stu-id="bbbfc-220">Allow client connection from your computer</span></span>

<span data-ttu-id="bbbfc-221">Hola **crear una nueva regla de firewall** se abre el cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="bbbfc-222">De forma predeterminada, la instancia de SQL Database solo permite conexiones desde servicios de Azure, como la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="bbbfc-223">tooconnect tooyour la base de datos, cree una regla de firewall en la instancia de base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="bbbfc-224">regla de firewall de Hello permite Hola de dirección IP pública del equipo local.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="bbbfc-225">cuadro de diálogo de Hello ya se rellena con la dirección IP pública de su equipo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="bbbfc-226">Asegúrese de que **Add my client IP** (Agregar mi IP de cliente) está seleccionado y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Configuración del firewall para la instancia de SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="bbbfc-228">Una vez que Visual Studio finaliza la creación de la configuración de firewall de hello para la instancia de base de datos SQL, la conexión se muestra en **Explorador de objetos de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="bbbfc-229">En este caso, puede realizar operaciones de base de datos más habituales hello, como consultas de ejecución, crean vistas y procedimientos almacenados y mucho más.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="bbbfc-230">Haga doble clic en hello `Todoes` de tabla y seleccione **ver datos**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Exploración de objetos de SQL Database](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="bbbfc-232">Actualización de aplicaciones con Migraciones de Code First</span><span class="sxs-lookup"><span data-stu-id="bbbfc-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="bbbfc-233">Puede utilizar herramientas conocidas de hello en Visual Studio tooupdate la base de datos y la aplicación web en Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="bbbfc-234">En este paso, usar migraciones de Code First en Entity Framework toomake un esquema de base de datos de cambio tooyour y publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="bbbfc-235">Para más información sobre el uso de Entity Framework Code First Migrations, consulte [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application) (Introducción a Entity Framework 6 Code First mediante MVC 5).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="bbbfc-236">Actualización del modelo de datos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-236">Update your data model</span></span>

<span data-ttu-id="bbbfc-237">Abra _Models\Todo.cs_ en el editor de código de hello.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="bbbfc-238">Agregar Hola después de la propiedad toohello `ToDo` clase:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="bbbfc-239">Ejecución de Migraciones de Code First</span><span class="sxs-lookup"><span data-stu-id="bbbfc-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="bbbfc-240">Ejecutar algunos comandos toomake actualizaciones tooyour base de datos local.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="bbbfc-241">De hello **herramientas** menú, haga clic en **Administrador de paquetes de NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="bbbfc-242">En la ventana de la consola de administrador de paquetes de saludo, habilitar migraciones de Code First:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="bbbfc-243">Agregue una migración:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="bbbfc-244">Actualizar la base de datos local de hello:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="bbbfc-245">Tipo `Ctrl+F5` toorun Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="bbbfc-246">Hola de prueba editar detalles y crear los vínculos.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="bbbfc-247">Si la aplicación hello carga sin errores, se ha realizado correctamente en migraciones de Code First.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="bbbfc-248">Sin embargo, su aspecto aún página Hola iguales porque la lógica de aplicación no usa esta nueva propiedad todavía.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="bbbfc-249">Use la nueva propiedad de Hola</span><span class="sxs-lookup"><span data-stu-id="bbbfc-249">Use hello new property</span></span>

<span data-ttu-id="bbbfc-250">Realizar algunos cambios en su Hola de toouse código `Done` propiedad.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="bbbfc-251">Para simplificar, en este tutorial, va hello toochange `Index` y `Create` vistas de propiedad de hello toosee en acción.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="bbbfc-252">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="bbbfc-253">Buscar hello `Create()` método y agregue `Done` toohello lista de propiedades de hello `Bind` atributo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="bbbfc-254">Cuando haya terminado, su `Create()` firma del método es similar a Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="bbbfc-255">Abra _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="bbbfc-256">Hola código Razor, debería ver un `<div class="form-group">` elemento que utiliza `model.Description`y, a continuación, otra `<div class="form-group">` elemento que utiliza `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="bbbfc-257">Inmediatamente después de estos dos elementos, agregue otro elemento `<div class="form-group">` que use `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="bbbfc-258">Abra _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="bbbfc-259">Busque Hola vacía `<th></th>` elemento.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="bbbfc-260">Justo encima de este elemento, agregue después el código Razor de hello:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="bbbfc-261">Buscar hello `<td>` elemento que contiene Hola `Html.ActionLink()` métodos auxiliares.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="bbbfc-262">Justo encima de este elemento, agregue después el código Razor de hello:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="bbbfc-263">Eso es todo lo necesario toosee cambios de Hola Hola `Index` y `Create` vistas.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="bbbfc-264">Tipo `Ctrl+F5` toorun Hola aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="bbbfc-265">Ahora puede agregar una tarea pendiente y marcar **Listo**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="bbbfc-266">A continuación se debería mostrar en su página principal como un elemento completado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="bbbfc-267">Recuerde que hello `Edit` vista no muestra hello `Done` campo, ya que no ha cambiado hello `Edit` vista.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="bbbfc-268">Habilitación de Migraciones de Code First en Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="bbbfc-269">Ahora que el código de cambios, incluida la migración de base de datos, puedes publicación aplicación de Azure web tooyour y actualizar la base de datos de SQL con migraciones de Code First demasiado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="bbbfc-270">Igual que antes, haga clic con el botón derecho en su proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="bbbfc-271">Haga clic en **configuración** tooopen Hola Asistente para la publicación.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Abrir la configuración de publicación](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="bbbfc-273">En el Asistente de hello, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="bbbfc-274">Asegúrese de que esa cadena de conexión de hello para la base de datos de SQL se rellena en **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="bbbfc-275">Puede que necesite hello tooselect **myToDoAppDb** base de datos de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="bbbfc-276">Seleccione **Ejecutar Migraciones de Code First (se ejecuta al iniciar la aplicación)** y luego haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Habilitar Migraciones de Code First en una aplicación web de Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="bbbfc-278">Publicación de los cambios</span><span class="sxs-lookup"><span data-stu-id="bbbfc-278">Publish your changes</span></span>

<span data-ttu-id="bbbfc-279">Ahora que ha habilitado Migraciones de Code First en su aplicación web de Azure, publique los cambios en el código.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="bbbfc-280">Hola, página de publicación, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="bbbfc-281">Intente volver a agregar elementos de tareas pendientes y seleccione **Listo**; se mostrarán en su página de inicio como un elemento completado.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Aplicación web de Azure después de aplicar Migraciones de Code First](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="bbbfc-283">Aún se muestran todas las tareas pendientes existentes.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="bbbfc-284">Cuando vuelva a publicar su aplicación de ASP.NET, los datos existentes en su instancia de SQL Database no se perderán.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="bbbfc-285">Además, migraciones de Code First solo cambia el esquema de datos de Hola y deja intactos los datos existentes.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="bbbfc-286">Transmisión de registros de aplicación</span><span class="sxs-lookup"><span data-stu-id="bbbfc-286">Stream application logs</span></span>

<span data-ttu-id="bbbfc-287">Puede transmitir los mensajes de seguimiento directamente desde su tooVisual de aplicación web de Azure Studio.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="bbbfc-288">Abra _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="bbbfc-289">Cada acción comienza con un método `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="bbbfc-290">Este código se agrega tooshow también cómo tooadd seguimiento mensajes de aplicación web de Azure de tooyour.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="bbbfc-291">Apertura del Explorador de servidores</span><span class="sxs-lookup"><span data-stu-id="bbbfc-291">Open Server Explorer</span></span>

<span data-ttu-id="bbbfc-292">De hello **vista** menú, seleccione **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="bbbfc-293">Puede configurar el registro de la aplicación web de Azure en el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="bbbfc-294">Habilitación de la secuencia de registros</span><span class="sxs-lookup"><span data-stu-id="bbbfc-294">Enable log streaming</span></span>

<span data-ttu-id="bbbfc-295">En el **Explorador de servidores**, expanda **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="bbbfc-296">Expanda hello **myResourceGroup** grupo de recursos, que se creó al crear aplicación web de Azure de hello por primera vez.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="bbbfc-297">Haga clic con el botón derecho en la aplicación web de Azure y seleccione **Ver registros de streaming**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Habilitación de la secuencia de registros](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="bbbfc-299">Hello registros son ahora se envía en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-299">hello logs are now streamed into hello **Output** window.</span></span> 

![Secuencia de registros en la ventana Salida](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="bbbfc-301">Sin embargo, aún no ve ningún seguimiento mensajes de saludo.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="bbbfc-302">Que porque, cuando selecciona **ver registros de Streaming**, la aplicación web de Azure establece el nivel de seguimiento de hello demasiado`Error`, que sólo registra los eventos de error (con hello `Trace.TraceError()` método).</span><span class="sxs-lookup"><span data-stu-id="bbbfc-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="bbbfc-303">Cambio de los niveles de seguimiento</span><span class="sxs-lookup"><span data-stu-id="bbbfc-303">Change trace levels</span></span>

<span data-ttu-id="bbbfc-304">seguimiento de hello toochange niveles toooutput otros mensajes de seguimiento, vaya vuelve demasiado**Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="bbbfc-305">Haga clic con el botón derecho en la aplicación web de Azure y seleccione **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="bbbfc-306">Hola **(sistema de archivos) del registro de aplicaciones** lista desplegable, seleccione **detallado**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="bbbfc-307">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-307">Click **Save**.</span></span>

![TooVerbose de nivel de seguimiento de cambios](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="bbbfc-309">Puede experimentar con diferentes niveles toosee qué tipos de mensajes se muestran para cada nivel.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="bbbfc-310">Por ejemplo, hello **información** nivel incluye todos los archivos creados por `Trace.TraceInformation()`, `Trace.TraceWarning()`, y `Trace.TraceError()`, pero no los archivos creados por `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="bbbfc-311">En el explorador, intente hacer clic en torno a aplicación de lista de tareas pendientes de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="bbbfc-312">los mensajes de seguimiento de Hello ahora se transmiten toohello **salida** ventana de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="bbbfc-313">Detención de las secuencias de registro</span><span class="sxs-lookup"><span data-stu-id="bbbfc-313">Stop log streaming</span></span>

<span data-ttu-id="bbbfc-314">toostop Hola servicio de transmisión por secuencias de registro, haga clic en hello **detener la supervisión de** botón en hello **salida** ventana.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Detención de las secuencias de registro](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="bbbfc-316">Administración de la aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-316">Manage your Azure web app</span></span>

<span data-ttu-id="bbbfc-317">Vaya toohello [portal de Azure](https://portal.azure.com) toosee hello web aplicación que creó.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="bbbfc-318">Hola menú izquierdo, haga clic en **servicio de aplicaciones**, a continuación, haga clic en nombre de saludo de la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Aplicación de navegación del portal tooAzure web](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="bbbfc-320">Ha llegado a la página de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="bbbfc-321">De forma predeterminada, el portal de hello muestra hello **Introducción** página.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="bbbfc-322">Esta página proporciona una visión del funcionamiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="bbbfc-323">En este caso, también puede realizar tareas de administración básicas como examinar, detener, iniciar, reiniciar y eliminar.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="bbbfc-324">pestañas: Hola a la izquierda Hola de página Hola páginas de configuración diferente de hello que puede abrir.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![Página de App Service en Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="bbbfc-326">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbbfc-326">Next steps</span></span>

<span data-ttu-id="bbbfc-327">En este tutorial, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="bbbfc-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbbfc-328">Crear una base de datos SQL en Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="bbbfc-329">Conectar un tooSQL de aplicación ASP.NET base de datos</span><span class="sxs-lookup"><span data-stu-id="bbbfc-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="bbbfc-330">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="bbbfc-331">Actualizar el modelo de datos de Hola y volver a implementar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="bbbfc-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="bbbfc-332">Registros de flujo de Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="bbbfc-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="bbbfc-333">Administrar aplicación Hola Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="bbbfc-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="bbbfc-334">Avanzar toohello siguiente tutorial toolearn cómo toomap un DNS personalizado nombre toohello web app.</span><span class="sxs-lookup"><span data-stu-id="bbbfc-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbbfc-335">Asignar un tooAzure de nombre DNS personalizado existente aplicaciones Web</span><span class="sxs-lookup"><span data-stu-id="bbbfc-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
