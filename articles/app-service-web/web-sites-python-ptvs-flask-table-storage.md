---
title: aaaFlask y almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo toouse Hola Python Tools para Visual Studio toocreate una aplicación web matraz que almacena los datos en el almacenamiento de tabla de Azure e implementarlo tooAzure aplicación del servicio Web de aplicaciones."
services: app-service\web
tags: python
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: d8e70a29-aca1-4010-95f5-cfe769e3be06
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 1a09d4cc78078a00492ba4fe7e2075df96fb0380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="cddd3-103">Flask y Almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cddd3-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="cddd3-104">En este tutorial, usaremos [Python Tools para Visual Studio] sondea de toocreate una sencilla aplicación web con una de las plantillas de ejemplo de Hola PTVS.</span><span class="sxs-lookup"><span data-stu-id="cddd3-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="cddd3-105">Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="cddd3-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="cddd3-106">aplicación web de Hello sondeos define una abstracción para el repositorio, por lo que puede cambiar fácilmente entre los distintos tipos de repositorios (en memoria, almacenamiento de tablas de Azure, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="cddd3-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="cddd3-107">Obtendrá información sobre cómo cuenta toocreate un almacenamiento de Azure, cómo tooconfigure Hola toouse de aplicación web el almacenamiento de tabla de Azure y cómo toopublish Hola aplicación web demasiado[aplicaciones de Web del servicio de aplicación de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="cddd3-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="cddd3-108">Vea hello [Centro para desarrolladores de Python] para ver más artículos que cubren el desarrollo de aplicaciones de Web del servicio de aplicación de Azure con PTVS mediante Bottle por sí solo, matraz y Django web marcos de trabajo, con los servicios de MongoDB, almacenamiento de tabla de Azure, MySQL y base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="cddd3-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="cddd3-109">Aunque en este artículo se centra en el servicio de aplicaciones, los pasos de hello son similares al desarrollar [servicios en la nube].</span><span class="sxs-lookup"><span data-stu-id="cddd3-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cddd3-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="cddd3-110">Prerequisites</span></span>
* <span data-ttu-id="cddd3-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cddd3-111">Visual Studio 2015</span></span>
* <span data-ttu-id="cddd3-112">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cddd3-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="cddd3-113">[Python Tools 2.2 para Visual Studio ejemplos VSIX]</span><span class="sxs-lookup"><span data-stu-id="cddd3-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="cddd3-114">[Herramientas de Azure SDK para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="cddd3-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="cddd3-115">[Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="cddd3-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="cddd3-116">Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cddd3-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="cddd3-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="cddd3-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="cddd3-118">Crear proyecto de hello</span><span class="sxs-lookup"><span data-stu-id="cddd3-118">Create hello Project</span></span>
<span data-ttu-id="cddd3-119">En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="cddd3-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="cddd3-120">Vamos a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="cddd3-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="cddd3-121">A continuación, ejecutaremos la aplicación hello localmente mediante el repositorio de hello predeterminado en memoria.</span><span class="sxs-lookup"><span data-stu-id="cddd3-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="cddd3-122">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="cddd3-123">Hola plantillas de proyecto de hello [Python Tools 2.2 para Visual Studio ejemplos VSIX] están disponibles en **Python**, **ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="cddd3-124">Seleccione **sondeos matraz Web Project** y haga clic en Aceptar toocreate Hola proyecto.</span><span class="sxs-lookup"><span data-stu-id="cddd3-124">Select **Polls Flask Web Project** and click OK toocreate hello project.</span></span>
   
     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="cddd3-126">Es posible que los paquetes externos tooinstall solicitadas.</span><span class="sxs-lookup"><span data-stu-id="cddd3-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="cddd3-127">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-127">Select **Install into a virtual environment**.</span></span>
   
     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="cddd3-129">Seleccione **Python 2.7** o **3.4 de Python** como intérprete base Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="cddd3-131">Confirme que la aplicación hello funciona presionando `F5`.</span><span class="sxs-lookup"><span data-stu-id="cddd3-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="cddd3-132">De forma predeterminada, la aplicación hello usa un repositorio en memoria que no requiere ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="cddd3-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="cddd3-133">Todos los datos se pierde cuando hello web server está detenido.</span><span class="sxs-lookup"><span data-stu-id="cddd3-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="cddd3-134">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo) y, a continuación, haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="cddd3-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="cddd3-136">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="cddd3-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="cddd3-137">operaciones de almacenamiento de toouse, necesita una cuenta de almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="cddd3-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="cddd3-138">Siga estos pasos para crear una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="cddd3-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="cddd3-139">Inicie sesión en hello [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cddd3-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cddd3-140">Haga clic en hello **New** icono en la parte superior de hello deja de hello Portal, a continuación, haga clic en **datos + almacenamiento** > **cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="cddd3-141">Haga clic en **crear**, a continuación, asigne un nombre único de cuenta de almacenamiento de Hola y crear un nuevo [grupo de recursos](../azure-resource-manager/resource-group-overview.md) para él.</span><span class="sxs-lookup"><span data-stu-id="cddd3-141">Click on **Create**, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Creación rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="cddd3-143">Cuando se ha creado la cuenta de almacenamiento de hello, Hola **notificaciones** botón parpadeará en un color verde **correcto** y está abierta la hoja de la cuenta de almacenamiento de hello tooshow que pertenece toohello nuevo recurso de grupo, creado.</span><span class="sxs-lookup"><span data-stu-id="cddd3-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="cddd3-144">Haga clic en hello **teclas de acceso** parte de la hoja de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-144">Click hello **Access Keys** part in hello storage account's blade.</span></span> <span data-ttu-id="cddd3-145">Tome nota del nombre de la cuenta de Hola y Hola key1.</span><span class="sxs-lookup"><span data-stu-id="cddd3-145">Take note of hello account name and hello key1.</span></span>
   
      ![simétricas](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="cddd3-147">Necesitamos esta información tooconfigure el proyecto en la sección siguiente de Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="cddd3-148">Configurar proyecto Hola</span><span class="sxs-lookup"><span data-stu-id="cddd3-148">Configure hello Project</span></span>
<span data-ttu-id="cddd3-149">En esta sección, vamos a configurar la cuenta de almacenamiento de aplicación toouse Hola que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="cddd3-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="cddd3-150">Veremos cómo tooobtain configuración de conexión de Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="cddd3-150">We'll see how tooobtain connection settings from hello Azure Portal.</span></span> <span data-ttu-id="cddd3-151">A continuación, ejecutaremos aplicación hello localmente.</span><span class="sxs-lookup"><span data-stu-id="cddd3-151">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="cddd3-152">En Visual Studio, haga clic con el botón derecho en el Explorador de soluciones y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="cddd3-153">Haga clic en hello **depurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="cddd3-153">Click on hello **Debug** tab.</span></span>
   
     ![Configuración de depuración del proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="cddd3-155">Establecer valores de hello de variables de entorno requeridos por la aplicación hello en **Depurar comandos de servidor**, **entorno**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-155">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="cddd3-156">Este modo, establecerá las variables de entorno de hello cuando se **Iniciar depuración**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-156">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="cddd3-157">Si desea que Hola variables toobe establece cuando se **iniciar sin depurar**, Hola conjunto mismos valores en **ejecutar comando de servidor** también.</span><span class="sxs-lookup"><span data-stu-id="cddd3-157">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="cddd3-158">Como alternativa, puede definir variables de entorno mediante el Panel de Control de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="cddd3-158">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="cddd3-159">Se trata de una mejor opción si desea tooavoid almacenar credenciales en el código fuente o archivo de proyecto.</span><span class="sxs-lookup"><span data-stu-id="cddd3-159">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="cddd3-160">Tenga en cuenta que necesitará toorestart Visual Studio para la aplicación de hello nuevo entorno valores toobe toohello disponibles.</span><span class="sxs-lookup"><span data-stu-id="cddd3-160">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="cddd3-161">código de Hello que implementa el repositorio de almacenamiento de tablas Azure Hola se encuentra en **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-161">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="cddd3-162">Vea hello [documentación] para obtener más información acerca de cómo toouse servicio de tablas de Python.</span><span class="sxs-lookup"><span data-stu-id="cddd3-162">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="cddd3-163">Ejecutar la aplicación hello con `F5`.</span><span class="sxs-lookup"><span data-stu-id="cddd3-163">Run hello application with `F5`.</span></span> <span data-ttu-id="cddd3-164">Sondeos que se crean con **crear sondeos de ejemplo** y datos de hello enviados votando se van a serializar en el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="cddd3-164">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="cddd3-165">Hola entorno Virtual de Python 2.7 puede producir una interrupción de excepción en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cddd3-165">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="cddd3-166">Presione `F5` toocontinue cargar el proyecto web de Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-166">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="cddd3-167">Examinar toohello **sobre** tooverify de página que Hola aplicación está usando hello **almacenamiento de tablas Azure** repositorio.</span><span class="sxs-lookup"><span data-stu-id="cddd3-167">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="cddd3-169">Explorar Hola almacenamiento de tabla de Azure</span><span class="sxs-lookup"><span data-stu-id="cddd3-169">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="cddd3-170">Es fácil tooview y editar tablas de almacenamiento mediante el Explorador de nube en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cddd3-170">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="cddd3-171">En esta sección, vamos a usar contenido de hello tooview de explorador de servidores de las tablas de aplicación de sondeos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-171">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="cddd3-172">Para ello, toobe de Microsoft Azure Tools instalado, que están disponibles como parte del programa Hola a [Azure SDK para .NET].</span><span class="sxs-lookup"><span data-stu-id="cddd3-172">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="cddd3-173">Abra **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="cddd3-174">Expanda **Cuentas de almacenamiento**, su cuenta de almacenamiento y, después, **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="cddd3-176">Haga doble clic en hello **sondeos** o **opciones** tabla tooview Hola contenido de tabla de hello en una ventana de documento, así como agregar/quitar/editar entidades.</span><span class="sxs-lookup"><span data-stu-id="cddd3-176">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados de la consulta de tabla](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="cddd3-178">Publicar hello web app tooAzure servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cddd3-178">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="cddd3-179">Hello Azure SDK para .NET proporciona una manera sencilla de toodeploy su tooAzure de aplicación web servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cddd3-179">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="cddd3-180">En **el Explorador de soluciones**, haga doble clic en el nodo del proyecto de Hola y seleccione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-180">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="cddd3-182">Haga clic en **Aplicaciones web de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="cddd3-183">Haga clic en **New** toocreate una nueva aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cddd3-183">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="cddd3-184">Rellene Hola después de campos y haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-184">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="cddd3-185">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="cddd3-185">**Web App name**</span></span>
   * <span data-ttu-id="cddd3-186">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="cddd3-186">**App Service plan**</span></span>
   * <span data-ttu-id="cddd3-187">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="cddd3-187">**Resource group**</span></span>
   * <span data-ttu-id="cddd3-188">**Región**</span><span class="sxs-lookup"><span data-stu-id="cddd3-188">**Region**</span></span>
   * <span data-ttu-id="cddd3-189">Deje **servidor de base de datos** establecido demasiado**ninguna base de datos**</span><span class="sxs-lookup"><span data-stu-id="cddd3-189">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="cddd3-190">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="cddd3-191">El explorador web abrirá automáticamente aplicaciones web publicadas de toohello.</span><span class="sxs-lookup"><span data-stu-id="cddd3-191">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="cddd3-192">Si examina toohello acerca de la página, verá que usa hello **en memoria** repositorio, no hello **almacenamiento de tablas Azure** repositorio.</span><span class="sxs-lookup"><span data-stu-id="cddd3-192">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="cddd3-193">Eso es porque no se establecen variables de entorno de hello en la instancia de aplicaciones Web de hello en el servicio de aplicación de Azure, por lo que utiliza valores predeterminados de hello especificados en **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-193">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="cddd3-194">Configurar la instancia de aplicaciones Web de Hola</span><span class="sxs-lookup"><span data-stu-id="cddd3-194">Configure hello Web Apps instance</span></span>
<span data-ttu-id="cddd3-195">En esta sección, vamos a configurar las variables de entorno para la instancia de aplicaciones Web de Hola.</span><span class="sxs-lookup"><span data-stu-id="cddd3-195">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="cddd3-196">En [Portal de Azure](https://portal.azure.com), abra la hoja de la aplicación hello web haciendo clic en **examinar** > **servicios de aplicaciones** > el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="cddd3-196">In [Azure Portal](https://portal.azure.com), open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="cddd3-197">En la hoja de la aplicación web, haga clic en **Toda la configuración** y en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="cddd3-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="cddd3-198">Desplácese hacia abajo toohello **configuración de la aplicación** sección y establecer valores de hello para **repositorio\_nombre**, **almacenamiento\_nombre** y  **ALMACENAMIENTO\_clave** tal y como se describe en hello **configurar proyectos de hello** sección anterior.</span><span class="sxs-lookup"><span data-stu-id="cddd3-198">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![Configuración de la aplicación](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="cddd3-200">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="cddd3-200">Click on **Save**.</span></span> <span data-ttu-id="cddd3-201">Después de que ha recibido notificaciones de Hola que se aplicaran los cambios de hello, haga clic en **examinar** desde la hoja principal de hello Web app.</span><span class="sxs-lookup"><span data-stu-id="cddd3-201">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="cddd3-202">Debería ver el trabajo de aplicación web de hello según lo esperado, con hello **almacenamiento de tablas Azure** repositorio.</span><span class="sxs-lookup"><span data-stu-id="cddd3-202">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="cddd3-203">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="cddd3-203">Congratulations!</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="cddd3-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cddd3-205">Next steps</span></span>
<span data-ttu-id="cddd3-206">Siga estos toolearn de vínculos más información acerca de Python Tools para Visual Studio, matraz y el almacenamiento de tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="cddd3-206">Follow these links toolearn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="cddd3-207">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="cddd3-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="cddd3-208">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="cddd3-208">[Web Projects]</span></span>
  * <span data-ttu-id="cddd3-209">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="cddd3-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="cddd3-210">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="cddd3-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="cddd3-211">[Documentación de Flask]</span><span class="sxs-lookup"><span data-stu-id="cddd3-211">[Flask Documentation]</span></span>
* <span data-ttu-id="cddd3-212">[Almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="cddd3-212">[Azure Storage]</span></span>
* <span data-ttu-id="cddd3-213">[SDK de Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="cddd3-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="cddd3-214">[¿Cómo tooUse Hola servicio de almacenamiento de tabla de Python]</span><span class="sxs-lookup"><span data-stu-id="cddd3-214">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="cddd3-215">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="cddd3-215">What's changed</span></span>
* <span data-ttu-id="cddd3-216">Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="cddd3-216">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro para desarrolladores de Python]: /develop/python/
[servicios en la nube]: ../cloud-services/cloud-services-python-ptvs.md
[documentación]:../cosmos-db/table-storage-how-to-use-python.md
[¿Cómo tooUse Hola servicio de almacenamiento de tabla de Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK para .NET]: http://azure.microsoft.com/downloads/
[Python Tools para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para Visual Studio ejemplos VSIX]: http://go.microsoft.com/fwlink/?LinkID=624025
[Herramientas de Azure SDK para VS 2015]: http://go.microsoft.com/fwlink/?linkid=518003
[Python 2.7 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 de 32 bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentación sobre Python Tools para Visual Studio]: http://aka.ms/ptvsdocs
[Documentación de Flask]: http://flask.pocoo.org/
[Depuración remota en Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Proyectos web]: http://go.microsoft.com/fwlink/?LinkId=624027
[Proyectos de servicio en la nube]: http://go.microsoft.com/fwlink/?LinkId=624028
[Almacenamiento de Azure]: http://azure.microsoft.com/documentation/services/storage/
[SDK de Azure para Python]: https://github.com/Azure/azure-sdk-for-python
