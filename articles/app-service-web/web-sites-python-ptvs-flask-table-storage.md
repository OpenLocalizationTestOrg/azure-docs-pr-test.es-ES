---
title: Flask y Almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio
description: "Obtenga información acerca de cómo usar las herramientas de Python para Visual Studio para crear una aplicación web de Flask que almacene datos en Almacenamiento de tablas de Azure y se pueda implementar en Aplicaciones web del Servicio de aplicaciones de Azure."
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
ms.openlocfilehash: 2e1bc8eebd0b67b965cc70ac4b5dfe03c4720ddf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="flask-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="913fd-103">Flask y Almacenamiento de tablas de Azure en Azure con Python Tools 2.2 para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="913fd-103">Flask and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="913fd-104">En este tutorial, usaremos las [Herramientas de Python para Visual Studio] a fin de crear una aplicación web de sondeos sencilla mediante una de las plantillas de ejemplo de PTVS.</span><span class="sxs-lookup"><span data-stu-id="913fd-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="913fd-105">Este tutorial también se encuentra disponible como [vídeo](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span><span class="sxs-lookup"><span data-stu-id="913fd-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=qUtZWtPwbTk).</span></span>

<span data-ttu-id="913fd-106">La aplicación web de sondeos define una abstracción para su repositorio, por lo que puede alternar fácilmente entre los diferentes tipos de repositorios (en memoria, almacenamiento de tablas de Azure y MongoDB).</span><span class="sxs-lookup"><span data-stu-id="913fd-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="913fd-107">Facilitaremos información acerca de cómo crear una cuenta de almacenamiento de Azure, cómo configurar la aplicación web para usar el Almacenamiento de tablas de Azure y cómo publicar la aplicación web en [Aplicaciones web del Servicio de aplicaciones de Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="913fd-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="913fd-108">Consulte el [Centro para desarrolladores de Python] para tener acceso a más artículos que tratan sobre el desarrollo de Aplicaciones web del Servicio de aplicaciones de Azure con PTVS mediante el uso de marcos web Bottle, Flask y Django, con MongoDB, Almacenamiento de tablas de Azure y los servicios de Base de datos MySQL y SQL.</span><span class="sxs-lookup"><span data-stu-id="913fd-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="913fd-109">Si bien estos artículos se centran en el Servicio de aplicaciones, los pasos son similares a los que se aplican para desarrollar [Servicios en la nube de Azure].</span><span class="sxs-lookup"><span data-stu-id="913fd-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="913fd-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="913fd-110">Prerequisites</span></span>
* <span data-ttu-id="913fd-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="913fd-111">Visual Studio 2015</span></span>
* <span data-ttu-id="913fd-112">[Python Tools 2.2 para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="913fd-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="913fd-113">[Python Tools 2.2 para archivos VSIX de ejemplo de Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="913fd-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="913fd-114">[Herramientas de Azure SDK para VS 2015]</span><span class="sxs-lookup"><span data-stu-id="913fd-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="913fd-115">[Python 2.7 de 32 bits] o [Python 3.4 de 32 bits]</span><span class="sxs-lookup"><span data-stu-id="913fd-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="913fd-116">Si desea empezar a trabajar con el Servicio de aplicaciones de Azure antes de inscribirse para abrir una cuenta de Azure, vaya a [Prueba del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde podrá crear inmediatamente una aplicación web de inicio de corta duración en el Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="913fd-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="913fd-117">No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.</span><span class="sxs-lookup"><span data-stu-id="913fd-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="913fd-118">Creación del proyecto</span><span class="sxs-lookup"><span data-stu-id="913fd-118">Create the Project</span></span>
<span data-ttu-id="913fd-119">En esta sección, vamos a crear un proyecto de Visual Studio con la utilización de una plantilla de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="913fd-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="913fd-120">Vamos a crear un entorno virtual e instalar los paquetes necesarios.</span><span class="sxs-lookup"><span data-stu-id="913fd-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="913fd-121">A continuación, vamos a ejecutar la aplicación localmente con el repositorio en memoria predeterminado.</span><span class="sxs-lookup"><span data-stu-id="913fd-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="913fd-122">En Visual Studio, seleccione **Archivo**, **Nuevo proyecto**.</span><span class="sxs-lookup"><span data-stu-id="913fd-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="913fd-123">Las plantillas de proyecto de los [Python Tools 2.2 para archivos VSIX de ejemplo de Visual Studio] se encuentran disponibles en **Python**, **Ejemplos**.</span><span class="sxs-lookup"><span data-stu-id="913fd-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="913fd-124">Seleccione **Polls Flask Web Project** (Proyecto web de Flask para sondeos) y haga clic en OK (Aceptar) para crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="913fd-124">Select **Polls Flask Web Project** and click OK to create the project.</span></span>
   
     ![Cuadro de diálogo Nuevo proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskNewProject.png)
3. <span data-ttu-id="913fd-126">Se le pedirá que instale paquetes externos.</span><span class="sxs-lookup"><span data-stu-id="913fd-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="913fd-127">Seleccione **Instalar en un entorno virtual**.</span><span class="sxs-lookup"><span data-stu-id="913fd-127">Select **Install into a virtual environment**.</span></span>
   
     ![Cuadro de diálogo Paquetes externos](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskExternalPackages.png)
4. <span data-ttu-id="913fd-129">Seleccione **Python 2.7** o **Python 3.4** como intérprete de base.</span><span class="sxs-lookup"><span data-stu-id="913fd-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Cuadro de diálogo Agregar entorno virtual](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="913fd-131">Presione `F5`para confirmar que la aplicación funciona.</span><span class="sxs-lookup"><span data-stu-id="913fd-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="913fd-132">De forma predeterminada, la aplicación usa un repositorio en memoria que no requiere ninguna configuración.</span><span class="sxs-lookup"><span data-stu-id="913fd-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="913fd-133">Todos los datos se pierden cuando el servidor web se detiene.</span><span class="sxs-lookup"><span data-stu-id="913fd-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="913fd-134">Haga clic en **Create Sample Polls**(Crear sondeos de ejemplo) y, a continuación, haga clic en un sondeo y vote.</span><span class="sxs-lookup"><span data-stu-id="913fd-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="913fd-136">Creación de una cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="913fd-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="913fd-137">Necesita una cuenta de almacenamiento de Azure para usar operaciones de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="913fd-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="913fd-138">Siga estos pasos para crear una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="913fd-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="913fd-139">Inicie sesión en el [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="913fd-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="913fd-140">Haga clic en el icono **Nuevo**, situado en la parte superior izquierda del portal, y haga clic en **Datos y almacenamiento** > **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="913fd-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span> <span data-ttu-id="913fd-141">Haga clic en **Crear** y asigne un nombre único a la cuenta de almacenamiento y cree un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) nuevo para ella.</span><span class="sxs-lookup"><span data-stu-id="913fd-141">Click on **Create**, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Creación rápida](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="913fd-143">Una vez creada la cuenta de almacenamiento, el botón **Notificaciones** emitirá el mensaje **CORRECTO** parpadeante en color verde y la hoja de la cuenta de almacenamiento se abrirá para mostrar que pertenece al nuevo grupo de recursos que ha creado.</span><span class="sxs-lookup"><span data-stu-id="913fd-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="913fd-144">Haga clic en la parte **Claves de acceso** de la hoja de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="913fd-144">Click the **Access Keys** part in the storage account's blade.</span></span> <span data-ttu-id="913fd-145">Anote el nombre de la cuenta y la clave1.</span><span class="sxs-lookup"><span data-stu-id="913fd-145">Take note of the account name and the key1.</span></span>
   
      ![simétricas](./media/web-sites-python-ptvs-flask-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="913fd-147">Necesitamos esta información para configurar el proyecto en la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="913fd-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="913fd-148">Configuración del proyecto</span><span class="sxs-lookup"><span data-stu-id="913fd-148">Configure the Project</span></span>
<span data-ttu-id="913fd-149">En esta sección, vamos a configurar nuestra aplicación para usar la cuenta de almacenamiento que acabamos de crear.</span><span class="sxs-lookup"><span data-stu-id="913fd-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="913fd-150">Observaremos cómo obtener la configuración de la conexión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="913fd-150">We'll see how to obtain connection settings from the Azure Portal.</span></span> <span data-ttu-id="913fd-151">A continuación, ejecutaremos la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="913fd-151">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="913fd-152">En Visual Studio, haga clic con el botón derecho en el Explorador de soluciones y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="913fd-152">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="913fd-153">Haga clic en la pestaña **Depurar** .</span><span class="sxs-lookup"><span data-stu-id="913fd-153">Click on the **Debug** tab.</span></span>
   
     ![Configuración de depuración del proyecto](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="913fd-155">Establezca los valores de las variables del entorno que necesita la aplicación en **Depurar comando del servidor**, **Entorno**.</span><span class="sxs-lookup"><span data-stu-id="913fd-155">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="913fd-156">De esta forma se definirán las variables del entorno para **Iniciar depuración**.</span><span class="sxs-lookup"><span data-stu-id="913fd-156">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="913fd-157">Si desea que las variables se definan al **Iniciar sin depurar**, establezca los mismos valores en **Ejecutar comando del servidor**.</span><span class="sxs-lookup"><span data-stu-id="913fd-157">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="913fd-158">De forma alternativa, puede definir las variables del entorno con el Panel de control de Windows.</span><span class="sxs-lookup"><span data-stu-id="913fd-158">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="913fd-159">Se trata de una opción más conveniente si desea evitar que las credenciales se almacenen en el archivo de proyecto / de código fuente.</span><span class="sxs-lookup"><span data-stu-id="913fd-159">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="913fd-160">Tenga en cuenta que necesitará reiniciar Visual Studio para que los nuevos valores del entorno estén disponibles en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="913fd-160">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="913fd-161">El código que implementa el repositorio de Almacenamiento de tablas de Azure se encuentra en **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="913fd-161">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="913fd-162">Consulte la [documentación] para obtener más información sobre cómo usar el servicio Tabla en Python.</span><span class="sxs-lookup"><span data-stu-id="913fd-162">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="913fd-163">Presione `F5`para ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="913fd-163">Run the application with `F5`.</span></span> <span data-ttu-id="913fd-164">Los sondeos creados con **Create Sample Polls** (Crear sondeos de ejemplo) y los datos enviados al votar se serializarán en el Almacenamiento de tablas de Azure.</span><span class="sxs-lookup"><span data-stu-id="913fd-164">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="913fd-165">El entorno virtual de Python 2.7 pueden producir una interrupción de excepción en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="913fd-165">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="913fd-166">Presione `F5` para continuar cargando el proyecto web.</span><span class="sxs-lookup"><span data-stu-id="913fd-166">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="913fd-167">Vaya a la página **Acerca de** para comprobar que la aplicación usa el repositorio de **Azure Table Storage**.</span><span class="sxs-lookup"><span data-stu-id="913fd-167">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="913fd-169">Exploración del Almacenamiento de tablas de Azure</span><span class="sxs-lookup"><span data-stu-id="913fd-169">Explore the Azure Table Storage</span></span>
<span data-ttu-id="913fd-170">Es fácil ver y editar tablas de almacenamiento con Cloud Explorer en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="913fd-170">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="913fd-171">En esta sección, vamos a utilizar el Explorador de servidores para ver el contenido de las tablas de la aplicación de sondeos.</span><span class="sxs-lookup"><span data-stu-id="913fd-171">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="913fd-172">Para esto es necesario que estén instaladas las Herramientas de Microsoft Azure, que se encuentran disponibles como parte del [SDK de Azure para .NET].</span><span class="sxs-lookup"><span data-stu-id="913fd-172">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="913fd-173">Abra **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="913fd-173">Open **Cloud Explorer**.</span></span> <span data-ttu-id="913fd-174">Expanda **Cuentas de almacenamiento**, su cuenta de almacenamiento y, después, **Tablas**.</span><span class="sxs-lookup"><span data-stu-id="913fd-174">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="913fd-176">Haga doble clic en la tabla **polls** o **choices** para ver el contenido de la tabla en una ventana de documento, así como para agregar/quitar/editar entidades.</span><span class="sxs-lookup"><span data-stu-id="913fd-176">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![Resultados de la consulta de tabla](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="913fd-178">Publicación de aplicación web del Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="913fd-178">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="913fd-179">El SDK de Azure .NET ofrece una forma fácil de implementar la aplicación web en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="913fd-179">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="913fd-180">En el **Explorador de soluciones**, haga clic con el botón derecho en el nodo del proyecto y seleccione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="913fd-180">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Cuadro de diálogo Publicación web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="913fd-182">Haga clic en **Aplicaciones web de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="913fd-182">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="913fd-183">Haga clic en **Nuevo** para crear una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="913fd-183">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="913fd-184">Rellene los campos siguientes y haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="913fd-184">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="913fd-185">**Nombre de aplicación web**</span><span class="sxs-lookup"><span data-stu-id="913fd-185">**Web App name**</span></span>
   * <span data-ttu-id="913fd-186">**Plan del Servicio de aplicaciones**</span><span class="sxs-lookup"><span data-stu-id="913fd-186">**App Service plan**</span></span>
   * <span data-ttu-id="913fd-187">**Grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="913fd-187">**Resource group**</span></span>
   * <span data-ttu-id="913fd-188">**Región**</span><span class="sxs-lookup"><span data-stu-id="913fd-188">**Region**</span></span>
   * <span data-ttu-id="913fd-189">Deje **Servidor de base de datos** establecido en **No hay base de datos**</span><span class="sxs-lookup"><span data-stu-id="913fd-189">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="913fd-190">Acepte todos los valores predeterminados y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="913fd-190">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="913fd-191">El explorador web se abrirá automáticamente en la aplicación web publicada.</span><span class="sxs-lookup"><span data-stu-id="913fd-191">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="913fd-192">Si va hasta la página Acerca de, observará que usa el repositorio **En memoria** y no el repositorio de **Azure Table Storage**.</span><span class="sxs-lookup"><span data-stu-id="913fd-192">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="913fd-193">Esto se debe a que las variables del entorno no están definidas en la instancia de Aplicaciones web del Servicio de aplicaciones de Azure, por lo que usa los valores predeterminados especificados en **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="913fd-193">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="913fd-194">Configuración de la instancia de Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="913fd-194">Configure the Web Apps instance</span></span>
<span data-ttu-id="913fd-195">En esta sección, vamos a configurar las variables del entorno para la instancia de Aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="913fd-195">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="913fd-196">En [Azure Portal](https://portal.azure.com), abra la hoja de la aplicación web haciendo clic en **Examinar** > **App Services** > el nombre de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="913fd-196">In [Azure Portal](https://portal.azure.com), open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="913fd-197">En la hoja de la aplicación web, haga clic en **Toda la configuración** y en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="913fd-197">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="913fd-198">Desplácese hacia abajo hasta la sección **Configuración de la aplicación** y defina los valores para **REPOSITORY\_NAME**, **STORAGE\_NAME** y **STORAGE\_KEY**, como se describe en la sección anterior **Configuración del proyecto**.</span><span class="sxs-lookup"><span data-stu-id="913fd-198">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![Configuración de la aplicación](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="913fd-200">Haga clic en **Save**(Guardar).</span><span class="sxs-lookup"><span data-stu-id="913fd-200">Click on **Save**.</span></span> <span data-ttu-id="913fd-201">Después de que haya recibido las notificaciones de que se han aplicado los cambios, haga clic en **Examinar** desde la hoja principal de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="913fd-201">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="913fd-202">La aplicación web ahora debe funcionar según lo previsto, con la utilización del repositorio de **Almacenamiento de tablas de Azure** .</span><span class="sxs-lookup"><span data-stu-id="913fd-202">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="913fd-203">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="913fd-203">Congratulations!</span></span>
   
     ![Explorador web](./media/web-sites-python-ptvs-flask-table-storage/PollsFlaskAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="913fd-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="913fd-205">Next steps</span></span>
<span data-ttu-id="913fd-206">Siga estos vínculos para obtener más información acerca de Python Tools para Visual Studio, Flask y Almacenamiento de Tabla de Azure.</span><span class="sxs-lookup"><span data-stu-id="913fd-206">Follow these links to learn more about Python Tools for Visual Studio, Flask and Azure Table Storage.</span></span>

* <span data-ttu-id="913fd-207">[Documentación sobre Python Tools para Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="913fd-207">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="913fd-208">[Proyectos web]</span><span class="sxs-lookup"><span data-stu-id="913fd-208">[Web Projects]</span></span>
  * <span data-ttu-id="913fd-209">[Proyectos de servicio en la nube]</span><span class="sxs-lookup"><span data-stu-id="913fd-209">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="913fd-210">[Depuración remota en Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="913fd-210">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="913fd-211">[Documentación de Flask]</span><span class="sxs-lookup"><span data-stu-id="913fd-211">[Flask Documentation]</span></span>
* <span data-ttu-id="913fd-212">[Almacenamiento de Azure]</span><span class="sxs-lookup"><span data-stu-id="913fd-212">[Azure Storage]</span></span>
* <span data-ttu-id="913fd-213">[SDK de Azure para Python]</span><span class="sxs-lookup"><span data-stu-id="913fd-213">[Azure SDK for Python]</span></span>
* <span data-ttu-id="913fd-214">[Uso del servicio de almacenamiento de tablas desde Python]</span><span class="sxs-lookup"><span data-stu-id="913fd-214">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="913fd-215">Lo que ha cambiado</span><span class="sxs-lookup"><span data-stu-id="913fd-215">What's changed</span></span>
* <span data-ttu-id="913fd-216">Para obtener una guía del cambio de Sitios web a Servicio de aplicaciones, consulte: [Servicio de aplicaciones de Azure y su impacto en los servicios de Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="913fd-216">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Centro para desarrolladores de Python]: /develop/python/
[Servicios en la nube de Azure]: ../cloud-services/cloud-services-python-ptvs.md
[documentación]:../cosmos-db/table-storage-how-to-use-python.md
[Uso del servicio de almacenamiento de tablas desde Python]:../cosmos-db/table-storage-how-to-use-python.md

<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[SDK de Azure para .NET]: http://azure.microsoft.com/downloads/
[Herramientas de Python para Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 para Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
[Python Tools 2.2 para archivos VSIX de ejemplo de Visual Studio]: http://go.microsoft.com/fwlink/?LinkID=624025
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
