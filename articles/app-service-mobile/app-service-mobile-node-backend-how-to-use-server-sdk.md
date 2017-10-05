---
title: Trabajo con el SDK del servidor backend de Node.para Mobile Apps | Microsoft Docs
description: "Obtenga información sobre cómo trabajar con el SDK del servidor back-end de Node.js para Aplicaciones móviles del Servicio de aplicaciones de Azure."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: e7d97d3b-356e-4fb3-ba88-38ecbda5ea50
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: node
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 1d3aa7a0089279a8eafeb0ded951a5238e189eaa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="66d9e-103">Uso del SDK de Node.js de Aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-103">How to use the Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="66d9e-104">En este artículo se ofrece información detallada y ejemplos sobre cómo trabajar con un back-end de Node.js en Aplicaciones móviles del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-104">This article provides detailed information and examples showing how to work with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="66d9e-105"><a name="Introduction"></a>Introducción</span><span class="sxs-lookup"><span data-stu-id="66d9e-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="66d9e-106">Aplicaciones móviles del Servicio de aplicaciones de Azure proporciona la funcionalidad de agregar una API web de acceso a datos optimizada para móviles a una aplicación web.</span><span class="sxs-lookup"><span data-stu-id="66d9e-106">Azure App Service Mobile Apps provides the capability to add a mobile-optimized data access Web API to a web application.</span></span>  <span data-ttu-id="66d9e-107">El SDK de Aplicaciones móviles del Servicio de aplicaciones de Azure se proporciona para las aplicaciones web de ASP.NET y Node.js.</span><span class="sxs-lookup"><span data-stu-id="66d9e-107">The Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="66d9e-108">El SDK proporciona las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="66d9e-108">The SDK provides the following operations:</span></span>

* <span data-ttu-id="66d9e-109">Operaciones de tabla (lectura, inserción, actualización, eliminación) para el acceso a datos</span><span class="sxs-lookup"><span data-stu-id="66d9e-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="66d9e-110">Operaciones API personalizadas</span><span class="sxs-lookup"><span data-stu-id="66d9e-110">Custom API operations</span></span>

<span data-ttu-id="66d9e-111">Ambas operaciones se incluyen para autenticación en todos los proveedores de identidades permitidos por el Servicio de aplicaciones de Azure, incluidos los proveedores de identidades sociales, como Facebook, Twitter, Google y Microsoft, así como Azure Active Directory para la identidad de empresa.</span><span class="sxs-lookup"><span data-stu-id="66d9e-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="66d9e-112">Puede encontrar ejemplos para cada caso de uso en el [directorio de ejemplos de GitHub].</span><span class="sxs-lookup"><span data-stu-id="66d9e-112">You can find samples for each use case in the [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="66d9e-113">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="66d9e-113">Supported Platforms</span></span>
<span data-ttu-id="66d9e-114">El SDK de Node de Mobile Apps es compatible con la versión LTS actual de Node y posterior.</span><span class="sxs-lookup"><span data-stu-id="66d9e-114">The Azure Mobile Apps Node SDK supports the current LTS release of Node and later.</span></span>  <span data-ttu-id="66d9e-115">Al momento de redactar este artículo, la versión LTS más reciente es Node v4.5.0.</span><span class="sxs-lookup"><span data-stu-id="66d9e-115">As of writing, the latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="66d9e-116">Aunque es posible que funcionen otras versiones de Node, no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="66d9e-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="66d9e-117">El SDK de Node de Mobile Apps de Azure admite dos controladores de base de datos: el controlador node-mssql es compatible con instancias de SQL Azure y SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="66d9e-117">The Azure Mobile Apps Node SDK supports two database drivers - the node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="66d9e-118">El controlador sqlite3 admite bases de datos de SQLite en una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="66d9e-118">The sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="66d9e-119"><a name="howto-cmdline-basicapp"></a>Creación de un back-end de Node.js básico mediante la línea de comandos</span><span class="sxs-lookup"><span data-stu-id="66d9e-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using the Command Line</span></span>
<span data-ttu-id="66d9e-120">Cada back-end de Node.js de aplicación móvil del Servicio de aplicaciones de Azure se inicia como una aplicación ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="66d9e-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="66d9e-121">ExpressJS es el marco del servicio web más popular disponible para Node.js.</span><span class="sxs-lookup"><span data-stu-id="66d9e-121">ExpressJS is the most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="66d9e-122">Puede crear una aplicación [Express] básica de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="66d9e-123">En una ventana de comandos o de PowerShell, cree un directorio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="66d9e-124">Ejecute npm init para inicializar la estructura del paquete.</span><span class="sxs-lookup"><span data-stu-id="66d9e-124">Run npm init to initialize the package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="66d9e-125">El comando npm init le formulará una serie de preguntas para inicializar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-125">The npm init command asks a set of questions to initialize the project.</span></span>  <span data-ttu-id="66d9e-126">Vea el resultado del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="66d9e-126">See the example output:</span></span>

    ![La salida de npm init][0]
3. <span data-ttu-id="66d9e-128">Instalación de las bibliotecas express y azure-mobile-apps desde el repositorio npm.</span><span class="sxs-lookup"><span data-stu-id="66d9e-128">Install the express and azure-mobile-apps libraries from the npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="66d9e-129">Cree un archivo app.js para implementar el servidor móvil básico.</span><span class="sxs-lookup"><span data-stu-id="66d9e-129">Create an app.js file to implement the basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="66d9e-130">Esta aplicación crea una API web sencilla optimizada para móviles con un único punto de conexión (`/tables/TodoItem`) que proporciona el acceso no autenticado a un almacén de datos SQL subyacente mediante un esquema dinámico.</span><span class="sxs-lookup"><span data-stu-id="66d9e-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access to an underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="66d9e-131">Es adecuado para los siguientes inicios rápidos de la biblioteca de cliente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="66d9e-132">[Inicio rápido de cliente de Android]</span><span class="sxs-lookup"><span data-stu-id="66d9e-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-133">[Inicio rápido de cliente de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="66d9e-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-134">[Inicio rápido de cliente de iOS]</span><span class="sxs-lookup"><span data-stu-id="66d9e-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-135">[Inicio rápido de cliente de Windows]</span><span class="sxs-lookup"><span data-stu-id="66d9e-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-136">[Inicio rápido de cliente de Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="66d9e-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-137">[Inicio rápido de cliente de Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="66d9e-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="66d9e-138">[Inicio rápido de cliente de Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="66d9e-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="66d9e-139">Puede encontrar el código de esta aplicación básica en el [ejemplo "basicapp" en GitHub].</span><span class="sxs-lookup"><span data-stu-id="66d9e-139">You can find the code for this basic application in the [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="66d9e-140"><a name="howto-vs2015-basicapp"></a>Creación de un back-end de Node con Visual Studio de 2015</span><span class="sxs-lookup"><span data-stu-id="66d9e-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="66d9e-141">Visual Studio 2015 requiere una extensión para desarrollar aplicaciones Node.js en el IDE.</span><span class="sxs-lookup"><span data-stu-id="66d9e-141">Visual Studio 2015 requires an extension to develop Node.js applications within the IDE.</span></span>  <span data-ttu-id="66d9e-142">Para comenzar, instale [Node.js Tools 1.1 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="66d9e-142">To start, install the [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="66d9e-143">Una vez instalado Node.js Tools para Visual Studio, cree una aplicación Express 4.x:</span><span class="sxs-lookup"><span data-stu-id="66d9e-143">Once the Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="66d9e-144">Abra el cuadro de diálogo **Nuevo proyecto** (desde **Archivo** > **Nuevo** > **Proyecto...**).</span><span class="sxs-lookup"><span data-stu-id="66d9e-144">Open the **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="66d9e-145">Expanda **Plantillas** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="66d9e-146">Seleccione **Basic Azure Node.js Express 4 Application**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-146">Select the **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="66d9e-147">Rellene el nombre del proyecto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-147">Fill in the project name.</span></span>  <span data-ttu-id="66d9e-148">Haga clic en *Aceptar*.</span><span class="sxs-lookup"><span data-stu-id="66d9e-148">Click *OK*.</span></span>

    ![Nuevo proyecto de Visual Studio de 2015][1]
5. <span data-ttu-id="66d9e-150">Haga clic con el botón derecho en el nodo **npm** y seleccione **Install New npm packages...** (Instalar nuevos paquetes npm).</span><span class="sxs-lookup"><span data-stu-id="66d9e-150">Right-click the **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="66d9e-151">Quizá tenga que actualizar el catálogo npm al crear su primera aplicación de Node.js.</span><span class="sxs-lookup"><span data-stu-id="66d9e-151">You may need to refresh the npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="66d9e-152">Haga clic en **Actualizar** si es necesario.</span><span class="sxs-lookup"><span data-stu-id="66d9e-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="66d9e-153">Escriba *azure-mobile-apps* en el cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="66d9e-153">Enter *azure-mobile-apps* in the search box.</span></span>  <span data-ttu-id="66d9e-154">Haga clic en el **paquete azure-mobile-apps 2.0.0** y, después, en **Install Package** (Instalar paquete).</span><span class="sxs-lookup"><span data-stu-id="66d9e-154">Click the **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Instalar nuevos paquetes npm][2]
8. <span data-ttu-id="66d9e-156">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-156">Click **Close**.</span></span>
9. <span data-ttu-id="66d9e-157">Abra el archivo *app.js* para agregar compatibilidad con el SDK de Aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-157">Open the *app.js* file to add support for the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="66d9e-158">En la línea 6 al final de las instrucciones requiere de la biblioteca, agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-158">At line 6 at the bottom of the library require statements, add the following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="66d9e-159">Aproximadamente en línea 27 después de las demás instrucciones app.use, agregue el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-159">At approximately line 27 after the other app.use statements, add the following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="66d9e-160">Guarde el archivo .</span><span class="sxs-lookup"><span data-stu-id="66d9e-160">Save the file.</span></span>
10. <span data-ttu-id="66d9e-161">Ejecute la aplicación localmente (la API se sirve en http://localhost:3000) o publíquela en Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-161">Either run the application locally (the API is served on http://localhost:3000) or publish to Azure.</span></span>

### <span data-ttu-id="66d9e-162"><a name="create-node-backend-portal"></a>Creación de un back-end de Node.js mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using the Azure portal</span></span>
<span data-ttu-id="66d9e-163">Puede crear un nuevo back-end de aplicación móvil directamente en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-163">You can create a Mobile App backend right in the [Azure portal].</span></span> <span data-ttu-id="66d9e-164">Puede seguir los pasos que se muestran a continuación o crear un cliente y un servidor nuevos mediante el tutorial de [creación de aplicaciones móviles](app-service-mobile-ios-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="66d9e-164">You can either follow the following steps or create a client and server together by following the [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="66d9e-165">El tutorial contiene una versión simplificada de estas instrucciones y se recomienda su lectura para proyectos de prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-165">The tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="66d9e-166">En la hoja *Comenzar*, en **Create a table API** (Crear una API de tabla), elija **Node.js** como valor de **Backend language** (Lenguaje de back-end).</span><span class="sxs-lookup"><span data-stu-id="66d9e-166">Back in the *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="66d9e-167">Active la casilla "**Reconozco que esta acción sobrescribirá el contenido del sitio web**" y haga clic en **Crear tabla TodoItem**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-167">Check the box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="66d9e-168"><a name="download-quickstart"></a>Descarga del proyecto de código de inicio rápido de un back-end de Node.js mediante Git</span><span class="sxs-lookup"><span data-stu-id="66d9e-168"><a name="download-quickstart"></a>How to: Download the Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="66d9e-169">Al crear un nuevo back-end de aplicación móvil de Node.js mediante la hoja **Inicio rápido** del portal, se crea automáticamente un nuevo proyecto de Node.js y se implementa en su sitio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-169">When you create a Node.js Mobile App backend by using the portal **Quick start** blade, a Node.js project is created for you and deployed to your site.</span></span> <span data-ttu-id="66d9e-170">Puede agregar tablas y API, así como editar archivos de código para el back-end de Node.js en el portal.</span><span class="sxs-lookup"><span data-stu-id="66d9e-170">You can add tables and APIs and edit code files for the Node.js backend in the portal.</span></span> <span data-ttu-id="66d9e-171">Puede utilizar cualquiera de las herramientas de implementación para descargar el proyecto de back-end con el fin de agregar o modificar tablas y API, y publicar el proyecto de nuevo.</span><span class="sxs-lookup"><span data-stu-id="66d9e-171">You can also use various deployment tools to download the backend project so that you can add or modify tables and APIs, then republish the project.</span></span> <span data-ttu-id="66d9e-172">Para obtener más información, consulte la [guía de implementación de Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="66d9e-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="66d9e-173">El siguiente procedimiento usa un repositorio de Git para descargar el código del proyecto de inicio rápido.</span><span class="sxs-lookup"><span data-stu-id="66d9e-173">the following procedure uses a Git repository to download the quickstart project code.</span></span>

1. <span data-ttu-id="66d9e-174">Si aún no lo ha hecho, instale Git.</span><span class="sxs-lookup"><span data-stu-id="66d9e-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="66d9e-175">Los pasos requeridos para instalar Git varían según los sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-175">The steps required to install Git vary between operating systems.</span></span> <span data-ttu-id="66d9e-176">Consulte el artículo de [instalación de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para obtener una guía sobre la instalación y las distribuciones específicas del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="66d9e-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="66d9e-177">Siga los pasos de [Habilitación del repositorio de App Service](../app-service-web/app-service-deploy-local-git.md#Step3) para habilitar el repositorio de Git para el sitio del back-end y anote el nombre de usuario y de la contraseña de la implementación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-177">Follow the steps in [Enable the App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) to enable the Git repository for your backend site, making a note of the deployment username and password.</span></span>
3. <span data-ttu-id="66d9e-178">En la hoja para el back-end de la aplicación móvil, tome nota del valor de **URL de clonación de Git** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-178">In the blade for your Mobile App backend, make a note of the **Git clone URL** setting.</span></span>
4. <span data-ttu-id="66d9e-179">Ejecute el comando `git clone` mediante la URL de clonación de Git e introduzca la contraseña cuando sea necesario, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-179">Execute the `git clone` command using the Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="66d9e-180">Desplácese al directorio local, que en el ejemplo anterior es /todolist, y observe si se han descargado archivos del proyecto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-180">Browse to local directory, which in the preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="66d9e-181">Busque el archivo `todoitem.json` en el directorio `/tables`.</span><span class="sxs-lookup"><span data-stu-id="66d9e-181">Locate the `todoitem.json` file in the `/tables` directory.</span></span>  <span data-ttu-id="66d9e-182">Este archivo define permisos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="66d9e-183">También encontrará el archivo `todoitem.js` en el mismo directorio, que define los scripts de operaciones CRUD de la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-183">Also find the `todoitem.js` file in the same directory, which defines that CRUD operation scripts for the table.</span></span>
6. <span data-ttu-id="66d9e-184">Después de realizar cambios en archivos del proyecto, ejecute los siguientes comandos para agregar, confirmar y cargar los cambios en el sitio:</span><span class="sxs-lookup"><span data-stu-id="66d9e-184">After you have made changes to project files, execute the following commands to add, commit, then upload the changes to the site:</span></span>

        $ git commit -m "updated the table script"
        $ git push origin master

    <span data-ttu-id="66d9e-185">Al agregar nuevos archivos al proyecto, primero debe ejecutar el comando `git add .`.</span><span class="sxs-lookup"><span data-stu-id="66d9e-185">When you add new files to the project, you first need to execute the `git add .` command.</span></span>

<span data-ttu-id="66d9e-186">Cada vez que se inserta un nuevo conjunto de confirmaciones en el sitio, se vuelve a publicar el sitio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-186">The site is republished every time a new set of commits is pushed to the site.</span></span>

### <span data-ttu-id="66d9e-187"><a name="howto-publish-to-azure"></a>Publicación del back-end de Node.js en Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend to Azure</span></span>
<span data-ttu-id="66d9e-188">Microsoft Azure proporciona varios mecanismos para publicar su back-end de Node.js de Aplicaciones móviles del Servicio de aplicaciones de Azure en el servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to the Azure service.</span></span>  <span data-ttu-id="66d9e-189">Incluyen el uso de herramientas de implementación integradas en Visual Studio, herramientas de línea de comandos y opciones de implementación continua basadas en control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="66d9e-190">Para obtener más información sobre este tema, consulte la [guía de implementación de Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="66d9e-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="66d9e-191">El Servicio de aplicaciones de Azure tiene instrucciones específicas para la aplicación de Node.js que usted debe revisar antes de realizar la implementación:</span><span class="sxs-lookup"><span data-stu-id="66d9e-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="66d9e-192">[Especificación de una versión de Node.js en una aplicación Azure]</span><span class="sxs-lookup"><span data-stu-id="66d9e-192">How to [specify the Node Version]</span></span>
* <span data-ttu-id="66d9e-193">[Uso de módulos de Node]</span><span class="sxs-lookup"><span data-stu-id="66d9e-193">How to [use Node modules]</span></span>

### <span data-ttu-id="66d9e-194"><a name="howto-enable-homepage"></a>Habilitación de una página de inicio para la aplicación</span><span class="sxs-lookup"><span data-stu-id="66d9e-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="66d9e-195">Muchas aplicaciones son una combinación de aplicaciones web y móviles, y el marco de trabajo ExpressJS le permite combinar las dos facetas.</span><span class="sxs-lookup"><span data-stu-id="66d9e-195">Many applications are a combination of web and mobile apps and the ExpressJS framework allows you to combine the two facets.</span></span>  <span data-ttu-id="66d9e-196">Sin embargo, es posible que en ocasiones solo quiera implementar una interfaz móvil.</span><span class="sxs-lookup"><span data-stu-id="66d9e-196">Sometimes, however, you may wish to only implement a mobile interface.</span></span>  <span data-ttu-id="66d9e-197">Es útil proporcionar una página de aterrizaje para garantizar que el servicio de aplicaciones está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="66d9e-197">It is useful to provide a landing page to ensure the app service is up and running.</span></span>  <span data-ttu-id="66d9e-198">Puede proporcionar su propia página de inicio o habilitar una de carácter temporal.</span><span class="sxs-lookup"><span data-stu-id="66d9e-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="66d9e-199">Para habilitar una página de inicio temporal, utilice lo siguiente para crear instancias de Mobile Apps de Azure:</span><span class="sxs-lookup"><span data-stu-id="66d9e-199">To enable a temporary home page, use the following to instantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="66d9e-200">Puede agregar esta opción al archivo `azureMobile.js` si solo quiere que esta opción esté disponible al desarrollar de forma local.</span><span class="sxs-lookup"><span data-stu-id="66d9e-200">If you only want this option available when developing locally, you can add this setting to your `azureMobile.js` file.</span></span>

## <span data-ttu-id="66d9e-201"><a name="TableOperations"></a>Operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="66d9e-202">El SDK del servidor de Node.js de azure-mobile-apps proporciona mecanismos para exponer las tablas de datos almacenadas en Base de datos SQL de Azure como una WebAPI.</span><span class="sxs-lookup"><span data-stu-id="66d9e-202">The azure-mobile-apps Node.js Server SDK provides mechanisms to expose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="66d9e-203">Se proporcionan cinco operaciones.</span><span class="sxs-lookup"><span data-stu-id="66d9e-203">Five operations are provided.</span></span>

| <span data-ttu-id="66d9e-204">Operación</span><span class="sxs-lookup"><span data-stu-id="66d9e-204">Operation</span></span> | <span data-ttu-id="66d9e-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="66d9e-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="66d9e-206">GET /tables/*nombredelatabla*</span><span class="sxs-lookup"><span data-stu-id="66d9e-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="66d9e-207">Obtener todos los registros de la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-207">Get all records in the table</span></span> |
| <span data-ttu-id="66d9e-208">GET /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="66d9e-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="66d9e-209">Obtener un registros específico de la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-209">Get a specific record in the table</span></span> |
| <span data-ttu-id="66d9e-210">POST /tables/*nombredelatabla*</span><span class="sxs-lookup"><span data-stu-id="66d9e-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="66d9e-211">Crear un registro de la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-211">Create a record in the table</span></span> |
| <span data-ttu-id="66d9e-212">PATCH /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="66d9e-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="66d9e-213">Eliminar un registro de la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-213">Update a record in the table</span></span> |
| <span data-ttu-id="66d9e-214">DELETE /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="66d9e-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="66d9e-215">Eliminar un registro de la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-215">Delete a record in the table</span></span> |

<span data-ttu-id="66d9e-216">Esta WebAPI admite [OData] y amplía el esquema de tabla para admitir la [sincronización de datos sin conexión].</span><span class="sxs-lookup"><span data-stu-id="66d9e-216">This WebAPI supports [OData] and extends the table schema to support [offline data sync].</span></span>

### <span data-ttu-id="66d9e-217"><a name="howto-dynamicschema"></a>Definición de tablas con un esquema dinámico</span><span class="sxs-lookup"><span data-stu-id="66d9e-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="66d9e-218">Antes de usar una tabla, esta debe definirse.</span><span class="sxs-lookup"><span data-stu-id="66d9e-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="66d9e-219">Las tablas pueden definirse con un esquema estático (en el que el desarrollador define las columnas en el esquema) o dinámicamente (en el que el SDK controla el esquema según las solicitudes entrantes).</span><span class="sxs-lookup"><span data-stu-id="66d9e-219">Tables can be defined with a static schema (where the developer defines the columns within the schema) or dynamically (where the SDK controls the schema based on incoming requests).</span></span> <span data-ttu-id="66d9e-220">Además, el desarrollador puede controlar aspectos específicos de la WebAPI agregando código Javascript a la definición.</span><span class="sxs-lookup"><span data-stu-id="66d9e-220">In addition, the developer can control specific aspects of the WebAPI by adding Javascript code to the definition.</span></span>

<span data-ttu-id="66d9e-221">Como procedimiento recomendado, debe definir cada tabla en un archivo de Javascript en el directorio de tablas y luego usar el método tables.import() para importar las tablas.</span><span class="sxs-lookup"><span data-stu-id="66d9e-221">As a best practice, you should define each table in a Javascript file in the tables directory, then use the tables.import() method to import the tables.</span></span>  <span data-ttu-id="66d9e-222">Al ampliar la aplicación básica, el archivo app.js debe ajustarse:</span><span class="sxs-lookup"><span data-stu-id="66d9e-222">Extending the basic-app, the app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define the database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add the mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="66d9e-223">Defina la tabla en ./tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="66d9e-223">Define the table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for the table goes here

    module.exports = table;

<span data-ttu-id="66d9e-224">Las tablas usan el esquema dinámico de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="66d9e-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="66d9e-225">Para desactivar el esquema dinámico globalmente, establezca la opción **MS_DynamicSchema** de la aplicación en False en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66d9e-225">To turn off dynamic schema globally, set the App Setting **MS_DynamicSchema** to false within the Azure portal.</span></span>

<span data-ttu-id="66d9e-226">Puede encontrar un ejemplo completo en el [ejemplo "todo" en GitHub].</span><span class="sxs-lookup"><span data-stu-id="66d9e-226">You can find a complete example in the [todo sample on GitHub].</span></span>

### <span data-ttu-id="66d9e-227"><a name="howto-staticschema"></a>Definición de tablas con un esquema estático</span><span class="sxs-lookup"><span data-stu-id="66d9e-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="66d9e-228">Puede definir explícitamente las columnas que desea exponer a través de la WebAPI.</span><span class="sxs-lookup"><span data-stu-id="66d9e-228">You can explicitly define the columns to expose via the WebAPI.</span></span>  <span data-ttu-id="66d9e-229">El SDK de Node.js de azure-mobile-apps agregará automáticamente todas las columnas adicionales necesarias para la sincronización de datos sin conexión a la lista que se proporcione.</span><span class="sxs-lookup"><span data-stu-id="66d9e-229">The azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync to the list that you provide.</span></span>  <span data-ttu-id="66d9e-230">Por ejemplo, las aplicaciones de cliente de inicio rápido requieren una tabla con dos columnas: text (una cadena) y complete (un booleano).</span><span class="sxs-lookup"><span data-stu-id="66d9e-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="66d9e-231">Esta tabla se puede definir en el archivo JavaScript de definición de la tabla (ubicado en el directorio de tablas) de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-231">The table can be defined in the table definition JavaScript file (located in the tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="66d9e-232">Si define las tablas estáticamente, también debe llamar al método tables.initialize() para crear el esquema de base de datos en el inicio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-232">If you define tables statically, then you must also call the tables.initialize() method to create the database schema on startup.</span></span>  <span data-ttu-id="66d9e-233">El método tables.initialize() devuelve [Promise] , que se usa para asegurarse de que el servicio web no atienda solicitudes antes de que la base de datos se inicialice.</span><span class="sxs-lookup"><span data-stu-id="66d9e-233">The tables.initialize() method returns a [Promise] so that the web service does not serve requests before the database being initialized.</span></span>

### <span data-ttu-id="66d9e-234"><a name="howto-sqlexpress-setup"></a>Uso de SQL Express como almacén de datos de desarrollo en el equipo local</span><span class="sxs-lookup"><span data-stu-id="66d9e-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="66d9e-235">El SDK de Node de Aplicaciones móviles de Azure proporciona tres opciones de fábrica para servir datos:</span><span class="sxs-lookup"><span data-stu-id="66d9e-235">The Azure Mobile Apps The AzureMobile Apps Node SDK provides three options for serving data out of the box: SDK provides three options for serving data out of the box:</span></span>

* <span data-ttu-id="66d9e-236">Use el controlador **memory** para proporcionar un almacén de ejemplos no persistente</span><span class="sxs-lookup"><span data-stu-id="66d9e-236">Use the **memory** driver to provide a non-persistent example store</span></span>
* <span data-ttu-id="66d9e-237">Utilice el controlador **mssql** para ofrecer un almacén de datos SQL Express para desarrollo</span><span class="sxs-lookup"><span data-stu-id="66d9e-237">Use the **mssql** driver to provide a SQL Express data store for development</span></span>
* <span data-ttu-id="66d9e-238">Use el controlador **mssql** para ofrecer un almacén de datos de Base de datos SQL de Azure para producción</span><span class="sxs-lookup"><span data-stu-id="66d9e-238">Use the **mssql** driver to provide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="66d9e-239">El SDK de Node.js de Aplicaciones móviles de Azure usa el [paquete de mssql para Node.js] para establecer y usar una conexión tanto a SQL Express como a Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="66d9e-239">The Azure Mobile Apps Node.js SDK uses the [mssql Node.js package] to establish and use a connection to both SQL Express and SQL Database.</span></span>  <span data-ttu-id="66d9e-240">Este paquete requiere que habilite las conexiones TCP en la instancia de SQL Express.</span><span class="sxs-lookup"><span data-stu-id="66d9e-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="66d9e-241">El controlador memory no proporciona un conjunto completo de servicios para la realización de pruebas.</span><span class="sxs-lookup"><span data-stu-id="66d9e-241">The memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="66d9e-242">Si desea probar el back-end localmente, se recomienda el uso de un almacén de datos de SQL Express y del controlador mssql.</span><span class="sxs-lookup"><span data-stu-id="66d9e-242">If you wish to test your backend locally, we recommend the use of a SQL Express data store and the mssql driver.</span></span>
>
>

1. <span data-ttu-id="66d9e-243">Descargue e instale [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="66d9e-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="66d9e-244">Asegúrese de instalar la edición SQL Server 2014 Express con Tools.</span><span class="sxs-lookup"><span data-stu-id="66d9e-244">Ensure you install the SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="66d9e-245">A menos que necesite expresamente compatibilidad con 64 bits, la versión de 32 bits consumirá menos memoria cuando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="66d9e-245">Unless you explicitly require 64-bit support, the 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="66d9e-246">Ejecute el Administrador de configuración de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="66d9e-246">Run the SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="66d9e-247">Expanda el nodo **Configuración de red de SQL Server** en el menú de árbol de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="66d9e-247">Expand the **SQL Server Network Configuration** node in the left-hand tree menu.</span></span>
   2. <span data-ttu-id="66d9e-248">Haga clic en **Protocolos para SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="66d9e-249">Haga clic con el botón derecho en **TCP/IP** y seleccione **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="66d9e-250">Haga clic en **Aceptar** en el cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-250">Click **OK** in the pop-up dialog.</span></span>
   4. <span data-ttu-id="66d9e-251">Haga clic con el botón derecho en **TCP/IP** y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="66d9e-252">Haga clic en la pestaña **Direcciones IP** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-252">Click the **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="66d9e-253">Busque el nodo **IPAll** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-253">Find the **IPAll** node.</span></span>  <span data-ttu-id="66d9e-254">En el campo **Puerto TCP**, escriba **1433**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-254">In the **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="66d9e-255">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-255">Click **OK**.</span></span>  <span data-ttu-id="66d9e-256">Haga clic en **Aceptar** en el cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-256">Click **OK** in the pop-up dialog.</span></span>
   8. <span data-ttu-id="66d9e-257">Haga clic en **Servicios de SQL Server** en el menú de árbol de la izquierda.</span><span class="sxs-lookup"><span data-stu-id="66d9e-257">Click **SQL Server Services** in the left-hand tree menu.</span></span>
   9. <span data-ttu-id="66d9e-258">Haga clic con el botón derecho en **SQL Server (SQLEXPRESS)** y seleccione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="66d9e-259">Cierre el Administrador de configuración de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="66d9e-259">Close the SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="66d9e-260">Ejecute SQL Server 2014 Management Studio y conéctese a la instancia local de SQL Express.</span><span class="sxs-lookup"><span data-stu-id="66d9e-260">Run the SQL Server 2014 Management Studio and connect to your local SQL Express instance</span></span>

   1. <span data-ttu-id="66d9e-261">Haga clic con el botón derecho en la instancia del Explorador de objetos y seleccione **Propiedades**</span><span class="sxs-lookup"><span data-stu-id="66d9e-261">Right-click your instance in the Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="66d9e-262">Seleccione la página **Seguridad** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-262">Select the **Security** page.</span></span>
   3. <span data-ttu-id="66d9e-263">Asegúrese de que el **Modo de autenticación de Windows y SQL Server** está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="66d9e-263">Ensure the **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="66d9e-264">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="66d9e-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="66d9e-265">Expanda **Seguridad** > **Inicios de sesión** en el Explorador de objetos</span><span class="sxs-lookup"><span data-stu-id="66d9e-265">Expand **Security** > **Logins** in the Object Explorer</span></span>
   6. <span data-ttu-id="66d9e-266">Haga clic con el botón derecho en **Inicios de sesión** y seleccione **Nuevo inicio de sesión...**</span><span class="sxs-lookup"><span data-stu-id="66d9e-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="66d9e-267">Escriba un nombre de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="66d9e-267">Enter a Login name.</span></span>  <span data-ttu-id="66d9e-268">Seleccione **Autenticación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="66d9e-269">Escriba una contraseña, y vuelva a escribirla en **Confirmar contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-269">Enter a Password, then enter the same password in **Confirm password**.</span></span>  <span data-ttu-id="66d9e-270">La contraseña debe cumplir los requisitos de complejidad de Windows.</span><span class="sxs-lookup"><span data-stu-id="66d9e-270">The password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="66d9e-271">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="66d9e-271">Click **OK**</span></span>

          ![Add a new user to SQL Express][5]
   9. <span data-ttu-id="66d9e-272">Haga clic con el botón derecho en el nuevo inicio de sesión y seleccione **Propiedades**</span><span class="sxs-lookup"><span data-stu-id="66d9e-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="66d9e-273">Seleccione la página **Roles del servidor** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-273">Select the **Server Roles** page</span></span>
   11. <span data-ttu-id="66d9e-274">Active la casilla que se encuentra junto al rol del servidor **dbcreator** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-274">Check the box next to the **dbcreator** server role</span></span>
   12. <span data-ttu-id="66d9e-275">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="66d9e-275">Click **OK**</span></span>
   13. <span data-ttu-id="66d9e-276">Cierre SQL Server 2015 Management Studio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-276">Close the SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="66d9e-277">Asegúrese de que registrar el nombre de usuario y la contraseña que seleccionó.</span><span class="sxs-lookup"><span data-stu-id="66d9e-277">Ensure you record the username and password you selected.</span></span>  <span data-ttu-id="66d9e-278">Puede que necesite asignar permisos o roles de servidor adicionales dependiendo de los requisitos específicos de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-278">You may need to assign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="66d9e-279">La aplicación de Node.js lee la variable de entorno **SQLCONNSTR_MS_TableConnectionString** de la cadena de conexión de esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-279">The Node.js application reads the **SQLCONNSTR_MS_TableConnectionString** environment variable for the connection string for this database.</span></span>  <span data-ttu-id="66d9e-280">Se puede establecer en el entorno.</span><span class="sxs-lookup"><span data-stu-id="66d9e-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="66d9e-281">Por ejemplo, puede usar PowerShell para establecer esta variable de entorno:</span><span class="sxs-lookup"><span data-stu-id="66d9e-281">For example, you can use PowerShell to set this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="66d9e-282">Acceda a la base de datos a través de una conexión TCP/IP y proporcionar un nombre de usuario y una contraseña para la conexión.</span><span class="sxs-lookup"><span data-stu-id="66d9e-282">Access the database through a TCP/IP connection and provide a username and password for the connection.</span></span>

### <span data-ttu-id="66d9e-283"><a name="howto-config-localdev"></a>Configuración del proyecto para el desarrollo local</span><span class="sxs-lookup"><span data-stu-id="66d9e-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="66d9e-284">Aplicaciones móviles de Azure lee un archivo de JavaScript denominado *azureMobile.js* del sistema de archivos local.</span><span class="sxs-lookup"><span data-stu-id="66d9e-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from the local filesystem.</span></span>  <span data-ttu-id="66d9e-285">No use este archivo para configurar el SDK de Mobile Apps de Azure en producción; use en su lugar la configuración de la aplicación dentro de [Azure Portal] .</span><span class="sxs-lookup"><span data-stu-id="66d9e-285">Do not use this file to configure the Azure Mobile Apps SDK in production - use App Settings within the [Azure portal] instead.</span></span>  <span data-ttu-id="66d9e-286">El archivo *azureMobile.js* debe exportar un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="66d9e-286">The *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="66d9e-287">La configuración más común es la siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-287">The most common settings are:</span></span>

* <span data-ttu-id="66d9e-288">Database Settings</span><span class="sxs-lookup"><span data-stu-id="66d9e-288">Database Settings</span></span>
* <span data-ttu-id="66d9e-289">Configuración del registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="66d9e-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="66d9e-290">Configuración de CORS alternativa</span><span class="sxs-lookup"><span data-stu-id="66d9e-290">Alternate CORS Settings</span></span>

<span data-ttu-id="66d9e-291">Se muestra un archivo de ejemplo *azureMobile.js* que implementa la configuración de la base de datos anterior:</span><span class="sxs-lookup"><span data-stu-id="66d9e-291">An example *azureMobile.js* file implementing the preceding database settings follows:</span></span>

    module.exports = {
        cors: {
            origins: [ 'localhost' ]
        },
        data: {
            provider: 'mssql',
            server: '127.0.0.1',
            database: 'mytestdatabase',
            user: 'azuremobile',
            password: 'T3stPa55word'
        },
        logging: {
            level: 'verbose'
        }
    };

<span data-ttu-id="66d9e-292">Se recomienda que agregue *azureMobile.js* al archivo *.gitignore* (o a otro archivo de omisiones de control de código fuente) para evitar que las contraseñas se almacenen en la nube.</span><span class="sxs-lookup"><span data-stu-id="66d9e-292">We recommend that you add *azureMobile.js* to your *.gitignore* file (or other source code control ignore file) to prevent passwords from being stored in the cloud.</span></span>  <span data-ttu-id="66d9e-293">Configure siempre los valores de producción en la configuración de la aplicación dentro de [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-293">Always configure production settings in App Settings within the [Azure portal].</span></span>

### <span data-ttu-id="66d9e-294"><a name="howto-appsettings"></a>Configuración de aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="66d9e-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="66d9e-295">La mayoría de las opciones de configuración del archivo *azureMobile.js* tienen una configuración de aplicación equivalente en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-295">Most settings in the *azureMobile.js* file have an equivalent App Setting in the [Azure portal].</span></span>  <span data-ttu-id="66d9e-296">Para configurar la aplicación en Configuración de aplicaciones, use la siguiente lista:</span><span class="sxs-lookup"><span data-stu-id="66d9e-296">Use the following list to configure your app in App Settings:</span></span>

| <span data-ttu-id="66d9e-297">Configuración de aplicación</span><span class="sxs-lookup"><span data-stu-id="66d9e-297">App Setting</span></span> | <span data-ttu-id="66d9e-298">*azureMobile.js* </span><span class="sxs-lookup"><span data-stu-id="66d9e-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="66d9e-299">Descripción</span><span class="sxs-lookup"><span data-stu-id="66d9e-299">Description</span></span> | <span data-ttu-id="66d9e-300">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="66d9e-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="66d9e-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="66d9e-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="66d9e-302">name</span><span class="sxs-lookup"><span data-stu-id="66d9e-302">name</span></span> |<span data-ttu-id="66d9e-303">Nombre de la aplicación</span><span class="sxs-lookup"><span data-stu-id="66d9e-303">The name of the app</span></span> |<span data-ttu-id="66d9e-304">string</span><span class="sxs-lookup"><span data-stu-id="66d9e-304">string</span></span> |
| <span data-ttu-id="66d9e-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="66d9e-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="66d9e-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="66d9e-306">logging.level</span></span> |<span data-ttu-id="66d9e-307">Nivel mínimo de registro de mensajes en el registro</span><span class="sxs-lookup"><span data-stu-id="66d9e-307">Minimum log level of messages to log</span></span> |<span data-ttu-id="66d9e-308">error, advertencia, información, detallado, depuración, absurdo</span><span class="sxs-lookup"><span data-stu-id="66d9e-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="66d9e-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="66d9e-309">**MS_DebugMode**</span></span> |<span data-ttu-id="66d9e-310">debug</span><span class="sxs-lookup"><span data-stu-id="66d9e-310">debug</span></span> |<span data-ttu-id="66d9e-311">Habilitar o deshabilitar el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="66d9e-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="66d9e-312">true, false</span><span class="sxs-lookup"><span data-stu-id="66d9e-312">true, false</span></span> |
| <span data-ttu-id="66d9e-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="66d9e-313">**MS_TableSchema**</span></span> |<span data-ttu-id="66d9e-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="66d9e-314">data.schema</span></span> |<span data-ttu-id="66d9e-315">Nombre del esquema predeterminado para tablas SQL</span><span class="sxs-lookup"><span data-stu-id="66d9e-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="66d9e-316">cadena (valor predeterminado: dbo)</span><span class="sxs-lookup"><span data-stu-id="66d9e-316">string (default: dbo)</span></span> |
| <span data-ttu-id="66d9e-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="66d9e-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="66d9e-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="66d9e-318">data.dynamicSchema</span></span> |<span data-ttu-id="66d9e-319">Habilitar o deshabilitar el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="66d9e-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="66d9e-320">true, false</span><span class="sxs-lookup"><span data-stu-id="66d9e-320">true, false</span></span> |
| <span data-ttu-id="66d9e-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="66d9e-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="66d9e-322">version (establecida en undefined)</span><span class="sxs-lookup"><span data-stu-id="66d9e-322">version (set to undefined)</span></span> |<span data-ttu-id="66d9e-323">Deshabilita el encabezado X-ZUMO-Server-Version</span><span class="sxs-lookup"><span data-stu-id="66d9e-323">Disables the X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="66d9e-324">true, false</span><span class="sxs-lookup"><span data-stu-id="66d9e-324">true, false</span></span> |
| <span data-ttu-id="66d9e-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="66d9e-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="66d9e-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="66d9e-326">skipversioncheck</span></span> |<span data-ttu-id="66d9e-327">Deshabilita la comprobación de la versión de API de cliente</span><span class="sxs-lookup"><span data-stu-id="66d9e-327">Disables the client API version check</span></span> |<span data-ttu-id="66d9e-328">true, false</span><span class="sxs-lookup"><span data-stu-id="66d9e-328">true, false</span></span> |

<span data-ttu-id="66d9e-329">Para establecer una configuración de aplicación:</span><span class="sxs-lookup"><span data-stu-id="66d9e-329">To set an App Setting:</span></span>

1. <span data-ttu-id="66d9e-330">Inicie sesión en el [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-330">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="66d9e-331">Seleccione **Todos los recursos** o **App Services** y haga clic en el nombre de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="66d9e-331">Select **All resources** or **App Services** then click the name of your Mobile App.</span></span>
3. <span data-ttu-id="66d9e-332">La hoja Configuración se abre de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="66d9e-332">The Settings blade opens by default.</span></span> <span data-ttu-id="66d9e-333">En caso contrario, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="66d9e-334">Haga clic en **Configuración de aplicación** en el menú GENERAL.</span><span class="sxs-lookup"><span data-stu-id="66d9e-334">Click **Application settings** in the GENERAL menu.</span></span>
5. <span data-ttu-id="66d9e-335">Desplácese hasta la sección Configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-335">Scroll to the App Settings section.</span></span>
6. <span data-ttu-id="66d9e-336">Si la configuración de la aplicación ya existe, haga clic en el valor de configuración de la aplicación para editarlo.</span><span class="sxs-lookup"><span data-stu-id="66d9e-336">If your app setting already exists, click the value of the app setting to edit the value.</span></span>
7. <span data-ttu-id="66d9e-337">Si no existe, escriba la configuración de aplicación en el cuadro Clave y el valor en el cuadro Valor.</span><span class="sxs-lookup"><span data-stu-id="66d9e-337">If your app setting does not exist, enter the App Setting in the Key box and the value in the Value box.</span></span>
8. <span data-ttu-id="66d9e-338">Cuando termine, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="66d9e-339">Si cambia la mayoría de las opciones de configuración de la aplicación habrá que reiniciar el servicio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="66d9e-340"><a name="howto-use-sqlazure"></a>Uso de Base de datos SQL como almacén de datos de producción</span><span class="sxs-lookup"><span data-stu-id="66d9e-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="66d9e-341">El uso de Base de datos SQL de Azure como almacén de datos es idéntico en todos los tipos de aplicaciones del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="66d9e-342">Si todavía no lo ha hecho, siga estos pasos para crear un back-end de aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="66d9e-342">If you have not done so already, follow these steps to create a Mobile App backend.</span></span>

1. <span data-ttu-id="66d9e-343">Inicie sesión en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-343">Log in to the [Azure portal].</span></span>
2. <span data-ttu-id="66d9e-344">En la parte superior izquierda de la ventana, haga clic en el **+ nuevo** botón > **Web y móvil** > **aplicación móvil**, a continuación, proporcione un nombre para su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="66d9e-344">In the top left of the window, click the **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="66d9e-345">En el cuadro **Grupo de recursos** , escriba el mismo nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-345">In the **Resource Group** box, enter the same name as your app.</span></span>
4. <span data-ttu-id="66d9e-346">Se seleccionará el Plan de App Service predeterminado.</span><span class="sxs-lookup"><span data-stu-id="66d9e-346">The Default App Service plan is selected.</span></span>  <span data-ttu-id="66d9e-347">Si desea cambiar un Plan de App Service, haga clic en el Plan de App Service >**+ Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-347">If you wish to change your App Service plan, you can do so by clicking the App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="66d9e-348">Proporcione un nombre al Plan del Servicio de aplicaciones nuevo y seleccione una ubicación adecuada.</span><span class="sxs-lookup"><span data-stu-id="66d9e-348">Provide a name of the new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="66d9e-349">Haga clic en el nivel de precios y seleccione un nivel de precios adecuado para el servicio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-349">Click the Pricing tier and select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="66d9e-350">Seleccione **Ver todos** para ver más opciones de precios, como **Gratis** y **Compartido**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-350">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="66d9e-351">Una vez haya seleccionado el nivel de precios, haga clic en el botón **Seleccionar** botón.</span><span class="sxs-lookup"><span data-stu-id="66d9e-351">Once you have selected the pricing tier, click the **Select** button.</span></span>  <span data-ttu-id="66d9e-352">De nuevo en la hoja **Plan de App Service**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-352">Back in the **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="66d9e-353">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-353">Click **Create**.</span></span> <span data-ttu-id="66d9e-354">El aprovisionamiento de un back-end de la aplicación móvil puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="66d9e-355">Cuando se aprovisiona el back-end de la aplicación móvil, el portal abre la hoja **Configuración** del back-end de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="66d9e-355">Once the Mobile App backend is provisioned, the portal opens the **Settings** blade for the Mobile App backend.</span></span>

<span data-ttu-id="66d9e-356">Una vez creado el back-end de la aplicación móvil, puede conectar una base de datos SQL al back-end de la aplicación móvil o bien crear una nueva base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="66d9e-356">Once the Mobile App backend is created, you can choose to either connect an existing SQL database to your Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="66d9e-357">En esta sección, crearemos una nueva base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="66d9e-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="66d9e-358">Si ya hay una base de datos en la misma ubicación que el back-end de aplicación móvil, puede elegir **Usar una base de datos existente** y seleccionar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-358">If you already have a database in the same location as the mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="66d9e-359">No se recomienda el uso de una base de datos en una ubicación diferente debido a las elevadas latencias.</span><span class="sxs-lookup"><span data-stu-id="66d9e-359">The use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="66d9e-360">En el nuevo back-end de la aplicación móvil, haga clic en **Configuración** > **Aplicación móvi** > **lDatos** > **+Agregar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-360">In the new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="66d9e-361">En la hoja **Add data connection** (Agregar conexión de datos), haga clic en **SQL Database - Configure required settings** (Base de datos SQL - Configurar los valores obligatorios) > **Create a new database** (Crear una base de datos nueva).</span><span class="sxs-lookup"><span data-stu-id="66d9e-361">In the **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="66d9e-362">Escriba el nombre de la base de datos nueva en el campo **Nombre** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-362">Enter the name of the new database in the **Name** field.</span></span>
3. <span data-ttu-id="66d9e-363">Haga clic en **Servidor**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-363">Click **Server**.</span></span>  <span data-ttu-id="66d9e-364">En la hoja **Nuevo servidor**, escriba un nombre de servidor único en el campo **Nombre del servidor** y especifique unos valores apropiados en **Inicio de sesión del administrador del servidor** y **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-364">In the **New server** blade, enter a unique server name in the **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="66d9e-365">Asegúrese de que **Permitir que los servicios de Azure accedan al servidor** está activado.</span><span class="sxs-lookup"><span data-stu-id="66d9e-365">Ensure **Allow azure services to access server** is checked.</span></span>  <span data-ttu-id="66d9e-366">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-366">Click **OK**.</span></span>

    ![Creación de una Base de datos SQL de Azure][6]
4. <span data-ttu-id="66d9e-368">En la hoja **Nueva base de datos**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-368">On the **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="66d9e-369">En la hoja **Add data connection** (Agregar conexión de datos), seleccione **Connection string** (Cadena de conexión) y especifique el inicio de sesión y la contraseña que indicó al crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-369">Back on the **Add data connection** blade, select **Connection string**, enter the login and password that you provided when creating the database.</span></span>  <span data-ttu-id="66d9e-370">Si usa una base de datos existente, indique las credenciales de inicio de sesión de esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-370">If you use an existing database, provide the login credentials for that database.</span></span>  <span data-ttu-id="66d9e-371">Cuando las especifique, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="66d9e-372">De nuevo en la hoja **Add data connection** (Agregar conexión de datos), haga clic en **OK** (Aceptar) para crear la base de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-372">Back on the **Add data connection** blade again, click **OK** to create the database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="66d9e-373">La creación de la base de datos puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-373">Creation of the database can take a few minutes.</span></span>  <span data-ttu-id="66d9e-374">Use el área de **notificaciones** para supervisar el progreso de la implementación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-374">Use the **Notifications** area to monitor the progress of the deployment.</span></span>  <span data-ttu-id="66d9e-375">No continúe hasta que la base de datos se haya implementado correctamente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-375">Do not progress until the database has been deployed successfully.</span></span>  <span data-ttu-id="66d9e-376">Una vez implementada correctamente, se creará una cadena de conexión para la instancia de SQL Database en la configuración de la aplicación de back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="66d9e-376">Once successfully deployed, a Connection String is created for the SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="66d9e-377">Puede ver la configuración de esta aplicación en **Configuración** > **Configuración de aplicación** > **Cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-377">You can see this app setting in the **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="66d9e-378"><a name="howto-tables-auth"></a>Requerimiento de la autenticación para acceder a las tablas</span><span class="sxs-lookup"><span data-stu-id="66d9e-378"><a name="howto-tables-auth"></a>How to: Require authentication for access to tables</span></span>
<span data-ttu-id="66d9e-379">Si quiere usar la autenticación de App Service con el punto de conexión de tablas, tiene que configurar primero la autenticación de App Service en el [Azure Portal] .</span><span class="sxs-lookup"><span data-stu-id="66d9e-379">If you wish to use App Service Authentication with the tables endpoint, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="66d9e-380">Para obtener más información sobre cómo configurar la autenticación en un Servicio de aplicaciones de Azure, revise la Guía de configuración del proveedor de identidades que pretende usar:</span><span class="sxs-lookup"><span data-stu-id="66d9e-380">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="66d9e-381">[Configuración de la aplicación para usar el inicio de sesión de Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="66d9e-381">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="66d9e-382">[Configuración de la aplicación para usar el inicio de sesión de Facebook]</span><span class="sxs-lookup"><span data-stu-id="66d9e-382">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="66d9e-383">[Configuración de la aplicación para usar el inicio de sesión de Google]</span><span class="sxs-lookup"><span data-stu-id="66d9e-383">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="66d9e-384">[Configuración de la aplicación para usar el inicio de sesión de Microsoft]</span><span class="sxs-lookup"><span data-stu-id="66d9e-384">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="66d9e-385">[Configuración de la aplicación para usar el inicio de sesión de Twitter]</span><span class="sxs-lookup"><span data-stu-id="66d9e-385">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="66d9e-386">Cada tabla tiene una propiedad de acceso que se puede usar para controlar el acceso a la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-386">Each table has an access property that can be used to control access to the table.</span></span>  <span data-ttu-id="66d9e-387">En el ejemplo siguiente se muestra una tabla definida estáticamente con la autenticación necesaria.</span><span class="sxs-lookup"><span data-stu-id="66d9e-387">The following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="66d9e-388">La propiedad de acceso puede tomar uno de tres valores</span><span class="sxs-lookup"><span data-stu-id="66d9e-388">The access property can take one of three values</span></span>

* <span data-ttu-id="66d9e-389">*anonymous* indica que la aplicación cliente puede leer los datos sin autenticación</span><span class="sxs-lookup"><span data-stu-id="66d9e-389">*anonymous* indicates that the client application is allowed to read data without authentication</span></span>
* <span data-ttu-id="66d9e-390">*authenticated* indica que la aplicación cliente tiene que enviar un token de autenticación válido con la solicitud</span><span class="sxs-lookup"><span data-stu-id="66d9e-390">*authenticated* indicates that the client application must send a valid authentication token with the request</span></span>
* <span data-ttu-id="66d9e-391">*disabled* indica que esta tabla está deshabilitada actualmente</span><span class="sxs-lookup"><span data-stu-id="66d9e-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="66d9e-392">Si la propiedad de acceso no está definida, se permite el acceso no autenticado.</span><span class="sxs-lookup"><span data-stu-id="66d9e-392">If the access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="66d9e-393"><a name="howto-tables-getidentity"></a>Uso de notificaciones de autenticación con las tablas</span><span class="sxs-lookup"><span data-stu-id="66d9e-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="66d9e-394">Puede configurar varias notificaciones que se solicitan cuando se configura la autenticación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="66d9e-395">Estas notificaciones no suelen estar disponibles por medio del objeto `context.user` .</span><span class="sxs-lookup"><span data-stu-id="66d9e-395">These claims are not normally available through the `context.user` object.</span></span>  <span data-ttu-id="66d9e-396">Sin embargo, se pueden recuperar con el método `context.user.getIdentity()` .</span><span class="sxs-lookup"><span data-stu-id="66d9e-396">However, they can be retrieved using the `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="66d9e-397">El método `getIdentity()` devuelve una promesa que se resuelve en un objeto.</span><span class="sxs-lookup"><span data-stu-id="66d9e-397">The `getIdentity()` method returns a Promise that resolves to an object.</span></span>  <span data-ttu-id="66d9e-398">El objeto tiene como clave el método de autenticación (facebook, google, twitter, microsoftaccount o aad).</span><span class="sxs-lookup"><span data-stu-id="66d9e-398">The object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="66d9e-399">Por ejemplo, si establece la autenticación mediante una cuenta Microsoft y solicita la notificación de direcciones de correo electrónico, puede agregar la dirección de correo electrónico al registro con el controlador de tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-399">For example, if you set up Microsoft Account authentication and request the email addresses claim, you can add the email address to the record with the following table controller:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    // Create a new table definition
    var table = azureMobileApps.table();

    table.columns = {
        "emailAddress": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;
    table.access = 'authenticated';

    /**
    * Limit the context query to those records with the authenticated user email address
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds the email address from the claims to the context item - used for
    * insert operations
    * @param {Context} context the operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when the client does a request
    // READ - only return records belonging to the authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite the userId based on the authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong to the authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong to the authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="66d9e-400">Para ver qué notificaciones están disponibles, use un explorador web para ver el punto de conexión `/.auth/me` de su sitio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-400">To see what claims are available, use a web browser to view the `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="66d9e-401"><a name="howto-tables-disabled"></a>Deshabilitación del acceso a operaciones de tabla específicas</span><span class="sxs-lookup"><span data-stu-id="66d9e-401"><a name="howto-tables-disabled"></a>How to: Disable access to specific table operations</span></span>
<span data-ttu-id="66d9e-402">Además de aparecer en la tabla, la propiedad de acceso puede usarse para controlar operaciones individuales.</span><span class="sxs-lookup"><span data-stu-id="66d9e-402">In addition to appearing on the table, the access property can be used to control individual operations.</span></span>  <span data-ttu-id="66d9e-403">Hay cuatro operaciones:</span><span class="sxs-lookup"><span data-stu-id="66d9e-403">There are four operations:</span></span>

* <span data-ttu-id="66d9e-404">*read* es la operación GET de RESTful en la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-404">*read* is the RESTful GET operation on the table</span></span>
* <span data-ttu-id="66d9e-405">*insert* es la operación POST de RESTful en la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-405">*insert* is the RESTful POST operation on the table</span></span>
* <span data-ttu-id="66d9e-406">*update* es la operación PATCH de RESTful en la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-406">*update* is the RESTful PATCH operation on the table</span></span>
* <span data-ttu-id="66d9e-407">*delete* es la operación DELETE de RESTful en la tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-407">*delete* is the RESTful DELETE operation on the table</span></span>

<span data-ttu-id="66d9e-408">Por ejemplo, es posible que quiera proporcionar una tabla de solo lectura no autenticada:</span><span class="sxs-lookup"><span data-stu-id="66d9e-408">For example, you may wish to provide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="66d9e-409"><a name="howto-tables-query"></a>Ajuste de la consulta que se usa con las operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-409"><a name="howto-tables-query"></a>How to: Adjust the query that is used with table operations</span></span>
<span data-ttu-id="66d9e-410">Un requisito común para las operaciones de tabla consiste en proporcionar una vista restringida de los datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-410">A common requirement for table operations is to provide a restricted view of the data.</span></span>  <span data-ttu-id="66d9e-411">Por ejemplo, puede proporcionar una tabla que esté etiquetada con el identificador del usuario autenticado, como que el usuario solo pueda leer o actualizar sus propios registros.</span><span class="sxs-lookup"><span data-stu-id="66d9e-411">For example, you may provide a table that is tagged with the authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="66d9e-412">La definición de la tabla siguiente proporcionará esta funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="66d9e-412">The following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for the table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for the authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite the userId with the authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="66d9e-413">Las operaciones que normalmente ejecutan una consulta tendrán una propiedad de consulta que se puede ajustar con una cláusula where.</span><span class="sxs-lookup"><span data-stu-id="66d9e-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="66d9e-414">La propiedad de consulta es un objeto [QueryJS] que se usa para convertir una consulta de OData en algo que puede procesar el back-end de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-414">The query property is a [QueryJS] object that is used to convert an OData query to something that the data backend can process.</span></span>  <span data-ttu-id="66d9e-415">En los casos de igualdad simple (como el anterior), puede usarse una asignación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-415">For simple equality cases (like the preceding one), a map can be used.</span></span> <span data-ttu-id="66d9e-416">También puede agregar cláusulas SQL específicas:</span><span class="sxs-lookup"><span data-stu-id="66d9e-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="66d9e-417"><a name="howto-tables-softdelete"></a>Configuración de una eliminación temporal en una tabla</span><span class="sxs-lookup"><span data-stu-id="66d9e-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="66d9e-418">La eliminación temporal no elimina realmente los registros.</span><span class="sxs-lookup"><span data-stu-id="66d9e-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="66d9e-419">Los marca como eliminados dentro de la base de datos al establecer la columna de eliminados en true.</span><span class="sxs-lookup"><span data-stu-id="66d9e-419">Instead it marks them as deleted within the database by setting the deleted column to true.</span></span>  <span data-ttu-id="66d9e-420">El SDK de Aplicaciones móviles de Azure quita automáticamente los registros temporalmente eliminados de los resultados, a menos que el SDK de cliente móvil use IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="66d9e-420">The Azure Mobile Apps SDK automatically removes soft-deleted records from results unless the Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="66d9e-421">Si quiere configurar una tabla para la eliminación temporal, establezca la propiedad `softDelete` en el archivo de definición de tabla:</span><span class="sxs-lookup"><span data-stu-id="66d9e-421">To configure a table for soft delete, set the `softDelete` property in the table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="66d9e-422">Debe establecer un mecanismo para depurar registros, ya sea desde una aplicación cliente a través de un trabajo web, una función de Azure o mediante una API personalizada.</span><span class="sxs-lookup"><span data-stu-id="66d9e-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="66d9e-423"><a name="howto-tables-seeding"></a>Inicialización de la base de datos con datos</span><span class="sxs-lookup"><span data-stu-id="66d9e-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="66d9e-424">Al crear una nueva aplicación, puede inicializar una tabla con datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-424">When creating a new application, you may wish to seed a table with data.</span></span>  <span data-ttu-id="66d9e-425">Esto puede hacerse en el archivo JavaScript de definición de tabla de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="66d9e-425">This can be done within the table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define the columns within the table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };
    table.seed = [
        { text: 'Example 1', complete: false },
        { text: 'Example 2', complete: true }
    ];

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication to access the table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="66d9e-426">La inicialización de datos se ha realizado únicamente cuando se crea la tabla por el SDK de Mobile Apps de Azure.</span><span class="sxs-lookup"><span data-stu-id="66d9e-426">Seeding of data is only done when the table is created by the Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="66d9e-427">Si la tabla ya existe en la base de datos, no se inserta ningún dato en la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-427">If the table already exists within the database, no data is injected into the table.</span></span>  <span data-ttu-id="66d9e-428">Si el esquema dinámico está activado, se deducirá el esquema de los datos inicializados.</span><span class="sxs-lookup"><span data-stu-id="66d9e-428">If dynamic schema is turned on, then the schema is inferred from the seeded data.</span></span>

<span data-ttu-id="66d9e-429">Se recomienda llamar expresamente al método `tables.initialize()` para crear la tabla cuando el servicio comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="66d9e-429">We recommend that you explicitly call the `tables.initialize()` method to create the table when the service starts running.</span></span>

### <span data-ttu-id="66d9e-430"><a name="Swagger"></a>Habilitación de la compatibilidad con Swagger</span><span class="sxs-lookup"><span data-stu-id="66d9e-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="66d9e-431">Aplicaciones móviles del Servicio de aplicaciones de Azure incorpora compatibilidad con [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="66d9e-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="66d9e-432">Para habilitar la compatibilidad con Swagger, instale primero el archivo swagger-ui como una dependencia:</span><span class="sxs-lookup"><span data-stu-id="66d9e-432">To enable Swagger support, first install the swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="66d9e-433">Una vez instalado, puede habilitar la compatibilidad con Swagger en el constructor de Aplicaciones móviles de Azure:</span><span class="sxs-lookup"><span data-stu-id="66d9e-433">Once installed, you can enable Swagger support in the Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="66d9e-434">Es probable que solo quiera habilitar la compatibilidad con Swagger en las ediciones de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="66d9e-434">You probably only want to enable Swagger support in development editions.</span></span>  <span data-ttu-id="66d9e-435">Puede hacerlo mediante la configuración de aplicación `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="66d9e-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="66d9e-436">El punto de conexión de Swagger se encuentra en http://*yoursite*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="66d9e-436">The swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="66d9e-437">Puede acceder a la interfaz de usuario de Swagger a través del punto de conexión de `/swagger/ui` .</span><span class="sxs-lookup"><span data-stu-id="66d9e-437">You can access the Swagger UI via the `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="66d9e-438">Si elige pedir autenticación en la aplicación entera, se producirá un error en Swagger.</span><span class="sxs-lookup"><span data-stu-id="66d9e-438">if you choose to require authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="66d9e-439">Para obtener los mejores resultados, permita que pasen las solicitudes no autenticadas en la configuración de autenticación y autorización del Servicio de aplicaciones de Azure y, luego, controle la autenticación mediante la propiedad `table.access` .</span><span class="sxs-lookup"><span data-stu-id="66d9e-439">For best results, choose to allow unauthenticated requests through in the Azure App Service Authentication / Authorization settings, then control authentication using the `table.access` property.</span></span>

<span data-ttu-id="66d9e-440">También puede agregar la opción de Swagger a su archivo `azureMobile.js` si solo quiere que haya compatibilidad con Swagger al desarrollar de forma local.</span><span class="sxs-lookup"><span data-stu-id="66d9e-440">You can also add the Swagger option to your `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="66d9e-441"><a name="push">Notificaciones push</span><span class="sxs-lookup"><span data-stu-id="66d9e-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="66d9e-442">Las aplicaciones móviles se integran con los Centros de notificaciones de Azure para permitirle el envío de notificaciones push destinadas a millones de dispositivos en las plataformas más importantes.</span><span class="sxs-lookup"><span data-stu-id="66d9e-442">Mobile Apps integrates with Azure Notification Hubs to enable you to send targeted push notifications to millions of devices across all major platforms.</span></span> <span data-ttu-id="66d9e-443">Mediante el uso de los Centros de notificaciones puede enviar notificaciones push a dispositivos iOS, Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="66d9e-443">By using Notification Hubs, you can send push notifications to iOS, Android and Windows devices.</span></span> <span data-ttu-id="66d9e-444">Para más información sobre todo lo que puede hacer con los Centros de notificaciones, vea [Información general de los Centros de notificaciones](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66d9e-444">To learn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="66d9e-445"></a><a name="send-push"></a>Envío de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="66d9e-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="66d9e-446">El código siguiente muestra cómo utilizar el objeto de inserción para enviar una notificación push de difusión a dispositivos iOS registrados:</span><span class="sxs-lookup"><span data-stu-id="66d9e-446">The following code shows how to use the push object to send a broadcast push notification to registered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do the push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="66d9e-447">Al crear un registro de inserción de plantillas desde el cliente, puede enviar un mensaje de inserción de plantilla a dispositivos en todas las plataformas compatibles.</span><span class="sxs-lookup"><span data-stu-id="66d9e-447">By creating a template push registration from the client, you can instead send a template push message to devices on all supported platforms.</span></span> <span data-ttu-id="66d9e-448">El código siguiente muestra cómo enviar una notificación de plantilla:</span><span class="sxs-lookup"><span data-stu-id="66d9e-448">The following code shows how to send a template notification:</span></span>

    // Define the template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do the push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }


### <span data-ttu-id="66d9e-449"><a name="push-user"></a>Envío de notificaciones push a un usuario autenticado mediante etiquetas</span><span class="sxs-lookup"><span data-stu-id="66d9e-449"><a name="push-user"></a>How to: Send push notifications to an authenticated user using tags</span></span>
<span data-ttu-id="66d9e-450">Cuando un usuario autenticado se registra para las notificaciones push, se agrega automáticamente una etiqueta con el identificador de usuario al registro.</span><span class="sxs-lookup"><span data-stu-id="66d9e-450">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="66d9e-451">Mediante el uso de esta etiqueta, puede enviar notificaciones push a todos los dispositivos registrados por un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="66d9e-451">By using this tag, you can send push notifications to all devices registered by a specific user.</span></span> <span data-ttu-id="66d9e-452">El código siguiente obtiene el SID del usuario que realiza la solicitud y envía una notificación push de plantilla a cada registro de dispositivo para ese usuario:</span><span class="sxs-lookup"><span data-stu-id="66d9e-452">The following code gets the SID of user making the request and sends a template push notification to every device registration for that user:</span></span>

    // Only do the push if configured
    if (context.push) {
        // Send a notification to the current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log the error.
            }
        });
    }

<span data-ttu-id="66d9e-453">Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro.</span><span class="sxs-lookup"><span data-stu-id="66d9e-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="66d9e-454"><a name="CustomAPI"></a> API personalizadas</span><span class="sxs-lookup"><span data-stu-id="66d9e-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="66d9e-455"><a name="howto-customapi-basic"></a>Definición de una API personalizada</span><span class="sxs-lookup"><span data-stu-id="66d9e-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="66d9e-456">Además de la API de acceso a datos a través del punto de conexión /tables, Aplicaciones móviles de Azure puede proporcionar cobertura de API personalizada.</span><span class="sxs-lookup"><span data-stu-id="66d9e-456">In addition to the data access API via the /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="66d9e-457">Las API personalizadas se definen de forma similar a las definiciones de tabla y pueden tener acceso a las mismas utilidades, incluida la autenticación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-457">Custom APIs are defined in a similar way to the table definitions and can access all the same facilities, including authentication.</span></span>

<span data-ttu-id="66d9e-458">Si quiere usar la autenticación del Servicio de aplicaciones con la API personalizada, debe configurar primero la autenticación del Servicio de aplicaciones en el [Azure Portal] .</span><span class="sxs-lookup"><span data-stu-id="66d9e-458">If you wish to use App Service Authentication with a Custom API, you must configure App Service Authentication in the [Azure portal] first.</span></span>  <span data-ttu-id="66d9e-459">Para obtener más información sobre cómo configurar la autenticación en un Servicio de aplicaciones de Azure, revise la Guía de configuración del proveedor de identidades que pretende usar:</span><span class="sxs-lookup"><span data-stu-id="66d9e-459">For more details about configuring authentication in an Azure App Service, review the Configuration Guide for the identity provider you intend to use:</span></span>

* <span data-ttu-id="66d9e-460">[Configuración de la aplicación para usar el inicio de sesión de Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="66d9e-460">[How to configure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="66d9e-461">[Configuración de la aplicación para usar el inicio de sesión de Facebook]</span><span class="sxs-lookup"><span data-stu-id="66d9e-461">[How to configure Facebook Authentication]</span></span>
* <span data-ttu-id="66d9e-462">[Configuración de la aplicación para usar el inicio de sesión de Google]</span><span class="sxs-lookup"><span data-stu-id="66d9e-462">[How to configure Google Authentication]</span></span>
* <span data-ttu-id="66d9e-463">[Configuración de la aplicación para usar el inicio de sesión de Microsoft]</span><span class="sxs-lookup"><span data-stu-id="66d9e-463">[How to configure Microsoft Authentication]</span></span>
* <span data-ttu-id="66d9e-464">[Configuración de la aplicación para usar el inicio de sesión de Twitter]</span><span class="sxs-lookup"><span data-stu-id="66d9e-464">[How to configure Twitter Authentication]</span></span>

<span data-ttu-id="66d9e-465">Las API personalizadas se definen en forma muy parecida a la API de tablas.</span><span class="sxs-lookup"><span data-stu-id="66d9e-465">Custom APIs are defined in much the same way as the Tables API.</span></span>

1. <span data-ttu-id="66d9e-466">Crear un directorio **api** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-466">Create an **api** directory</span></span>
2. <span data-ttu-id="66d9e-467">Cree un archivo JavaScript de definición de API en el directorio **api** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-467">Create an API definition JavaScript file in the **api** directory.</span></span>
3. <span data-ttu-id="66d9e-468">Use el método import para importar el directorio **api** .</span><span class="sxs-lookup"><span data-stu-id="66d9e-468">Use the import method to import the **api** directory.</span></span>

<span data-ttu-id="66d9e-469">A continuación se muestra la definición de la api de prototipo basada en el ejemplo de aplicación básica usado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-469">Here is the prototype api definition based on the basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="66d9e-470">Veamos un ejemplo de una API sencilla que devolverá la fecha del servidor mediante el método *Date.now()* .</span><span class="sxs-lookup"><span data-stu-id="66d9e-470">Let's take an example API that returns the server date using the *Date.now()* method.</span></span>  <span data-ttu-id="66d9e-471">Este es el archivo api/date.js:</span><span class="sxs-lookup"><span data-stu-id="66d9e-471">Here is the api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="66d9e-472">Cada parámetro es uno de los verbos estándar de RESTful: GET, POST, PATCH o DELETE.</span><span class="sxs-lookup"><span data-stu-id="66d9e-472">Each parameter is one of the standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="66d9e-473">El método es una función estándar de [ExpressJS Middleware] que envía el la salida necesaria.</span><span class="sxs-lookup"><span data-stu-id="66d9e-473">The method is a standard [ExpressJS Middleware] function that sends the required output.</span></span>

### <span data-ttu-id="66d9e-474"><a name="howto-customapi-auth"></a>Autenticación necesaria para el acceso a una API personalizada</span><span class="sxs-lookup"><span data-stu-id="66d9e-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access to a custom API</span></span>
<span data-ttu-id="66d9e-475">El SDK de Aplicaciones móviles de Azure implementa la autenticación de la misma manera para el punto de conexión de las tablas y para las API personalizadas.</span><span class="sxs-lookup"><span data-stu-id="66d9e-475">Azure Mobile Apps SDK implements authentication in the same way for both the tables endpoint and custom APIs.</span></span>  <span data-ttu-id="66d9e-476">Para agregar autenticación a la API desarrollada en la sección anterior, agregue una propiedad **access** :</span><span class="sxs-lookup"><span data-stu-id="66d9e-476">To add authentication to the API developed in the previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="66d9e-477">También puede especificar la autenticación en operaciones específicas:</span><span class="sxs-lookup"><span data-stu-id="66d9e-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // The GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="66d9e-478">Debe usar el mismo token que se utiliza para el punto de conexión de tablas en las API personalizadas que requieren autenticación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-478">The same token that is used for the tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="66d9e-479"><a name="howto-customapi-auth"></a>Control de cargas de archivos de gran tamaño</span><span class="sxs-lookup"><span data-stu-id="66d9e-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="66d9e-480">El SDK de Aplicaciones móviles de Azure usa el [middleware de analizador de cuerpo](https://github.com/expressjs/body-parser) para aceptar y descodificar el contenido del cuerpo del envío.</span><span class="sxs-lookup"><span data-stu-id="66d9e-480">Azure Mobile Apps SDK uses the [body-parser middleware](https://github.com/expressjs/body-parser) to accept and decode body content in your submission.</span></span>  <span data-ttu-id="66d9e-481">Puede configurar previamente el analizador de cuerpo para aceptar tamaños mayores de cargas de archivos:</span><span class="sxs-lookup"><span data-stu-id="66d9e-481">You can pre-configure body-parser to accept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import the Custom API
    mobile.api.import('./api');

    // Add the mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="66d9e-482">El archivo está codificado en Base 64 antes de la transmisión,</span><span class="sxs-lookup"><span data-stu-id="66d9e-482">The file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="66d9e-483">por lo que aumenta el tamaño de la carga real y, por tanto, el que debe tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="66d9e-483">This increases the size of the actual upload (and hence the size you must account for).</span></span>

### <span data-ttu-id="66d9e-484"><a name="howto-customapi-sql"></a>Ejecución de instrucciones SQL personalizadas</span><span class="sxs-lookup"><span data-stu-id="66d9e-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="66d9e-485">El SDK de aplicaciones móviles de Azure permite el acceso a todo el contexto a través del objeto de solicitud, lo que le permite ejecutar fácilmente instrucciones SQL parametrizadas para el proveedor de datos definido:</span><span class="sxs-lookup"><span data-stu-id="66d9e-485">The Azure Mobile Apps SDK allows access to the entire Context through the request object, allowing you to execute parameterized SQL statements to the defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on to a later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define the query - anything that can be handled by the mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute the query.  The context for Azure Mobile Apps is available through
            // request.azureMobile - the data object contains the configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="66d9e-486"><a name="Debugging"></a>Depuración, y tablas y API fáciles</span><span class="sxs-lookup"><span data-stu-id="66d9e-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="66d9e-487"><a name="howto-diagnostic-logs"></a>Depuración, diagnóstico y solución de problemas de Mobile Apps de Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="66d9e-488">El Servicio de aplicaciones de Azure proporciona varias técnicas de depuración y de solución de problemas para las aplicaciones Node.js.</span><span class="sxs-lookup"><span data-stu-id="66d9e-488">The Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="66d9e-489">Consulte los siguientes artículos para empezar a solucionar problemas de su back-end móvil de Node.js.</span><span class="sxs-lookup"><span data-stu-id="66d9e-489">Refer to the following articles to get started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="66d9e-490">[Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="66d9e-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="66d9e-491">[Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="66d9e-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="66d9e-492">[Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="66d9e-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="66d9e-493">Las aplicaciones Node.js tienen acceso a una amplia gama de herramientas de registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="66d9e-493">Node.js applications have access to a wide range of diagnostic log tools.</span></span>  <span data-ttu-id="66d9e-494">Internamente, el SDK de Node.js de Aplicaciones móviles de Azure usa [Winston] para el registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="66d9e-494">Internally, the Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="66d9e-495">El registro se habilita automáticamente al habilitar el modo de depuración o al establecer la configuración de la aplicación **MS_DebugMode** en True en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-495">Logging is automatically enabled by enabling debug mode or by setting the **MS_DebugMode** app setting to true in the [Azure portal].</span></span> <span data-ttu-id="66d9e-496">Los registros generados aparecerán en los registros de diagnóstico en [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="66d9e-496">Generated logs appear in the Diagnostic Logs on the [Azure portal].</span></span>

### <span data-ttu-id="66d9e-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Uso de tablas fáciles en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in the Azure portal</span></span>
<span data-ttu-id="66d9e-498">Las tablas fáciles del portal le permiten crear y trabajar con tablas directamente en el portal.</span><span class="sxs-lookup"><span data-stu-id="66d9e-498">Easy Tables in the portal let you create and work with tables right in the portal.</span></span> <span data-ttu-id="66d9e-499">Incluso puede editar las operaciones de tabla mediante el editor del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66d9e-499">You can even edit table operations using the App Service Editor.</span></span>

<span data-ttu-id="66d9e-500">Al hacer clic en **Tablas fáciles** en la configuración del sitio del back-end, puede agregar, modificar o eliminar una tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="66d9e-501">También puede ver los datos de la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-501">You can also see data in the table.</span></span>

![Trabajo con tablas fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="66d9e-503">Los siguientes comandos están disponibles en la barra de comandos para una tabla:</span><span class="sxs-lookup"><span data-stu-id="66d9e-503">The following commands are available on the command bar for a table:</span></span>

* <span data-ttu-id="66d9e-504">**Cambiar permisos** : modifica el permiso para leer, insertar, actualizar y eliminar operaciones en la tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-504">**Change permissions** - modify the permission for read, insert, update and delete operations on the table.</span></span>
  <span data-ttu-id="66d9e-505">Las opciones son permitir el acceso anónimo, requerir autenticación o deshabilitar todos los accesos a la operación.</span><span class="sxs-lookup"><span data-stu-id="66d9e-505">Options are to allow anonymous access, to require authentication, or to disable all access to the operation.</span></span>
* <span data-ttu-id="66d9e-506">**Editar script** : el archivo de script de la tabla se abre en el editor del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66d9e-506">**Edit script** - the script file for the table is opened in the App Service Editor.</span></span>
* <span data-ttu-id="66d9e-507">**Administrar esquema** : agrega o elimina columnas o cambia el índice de tabla.</span><span class="sxs-lookup"><span data-stu-id="66d9e-507">**Manage schema** - add or delete columns or change the table index.</span></span>
* <span data-ttu-id="66d9e-508">**Borrar tabla** : trunca una tabla existente eliminando todas las filas de datos pero dejando el esquema sin cambiar.</span><span class="sxs-lookup"><span data-stu-id="66d9e-508">**Clear table** - truncates an existing table be deleting all data rows but leaving the schema unchanged.</span></span>
* <span data-ttu-id="66d9e-509">**Eliminar filas** : elimina filas individuales de datos.</span><span class="sxs-lookup"><span data-stu-id="66d9e-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="66d9e-510">**Ver registros de streaming** : le conecta con el servicio de registro de streaming de su sitio.</span><span class="sxs-lookup"><span data-stu-id="66d9e-510">**View streaming logs** - connects you to the streaming log service for your site.</span></span>

### <span data-ttu-id="66d9e-511"><a name="work-easy-apis"></a>Trabajo con API fáciles en el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="66d9e-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in the Azure portal</span></span>
<span data-ttu-id="66d9e-512">Las API fáciles del portal le permiten crear y trabajar con API personalizadas directamente en el portal.</span><span class="sxs-lookup"><span data-stu-id="66d9e-512">Easy APIs in the portal let you create and work with custom APIs right in the portal.</span></span> <span data-ttu-id="66d9e-513">Incluso puede editar scripts de API mediante el editor de App Service.</span><span class="sxs-lookup"><span data-stu-id="66d9e-513">You can edit API scripts using the App Service Editor.</span></span>

<span data-ttu-id="66d9e-514">Al hacer clic en **API fáciles** en la configuración del sitio del back-end, puede agregar un nuevo punto de conexión de API personalizado, así como modificar o eliminar un punto de conexión de API existente.</span><span class="sxs-lookup"><span data-stu-id="66d9e-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Trabajo con API fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="66d9e-516">En el portal, puede cambiar los permisos de acceso para una acción de HTTP determinada, editar el archivo de script de API en el editor de App Service o ver los registros de streaming.</span><span class="sxs-lookup"><span data-stu-id="66d9e-516">In the portal, you can change the access permissions for a given HTTP action, edit the API script file in the App Service Editor, or view the streaming logs.</span></span>

### <span data-ttu-id="66d9e-517"><a name="online-editor"></a>Edición de código en el editor del Servicio de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="66d9e-517"><a name="online-editor"></a>How to: Edit code in the App Service Editor</span></span>
<span data-ttu-id="66d9e-518">El Portal de Azure le permite editar los archivos de script de back-end de Node.js en el editor de Servicio de aplicaciones sin tener que descargar el proyecto en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="66d9e-518">The Azure portal lets you edit your Node.js backend script files in the App Service Editor without having to download the project to your local computer.</span></span> <span data-ttu-id="66d9e-519">Para editar archivos de script en el editor en línea:</span><span class="sxs-lookup"><span data-stu-id="66d9e-519">To edit script files in the online editor:</span></span>

1. <span data-ttu-id="66d9e-520">En la hoja de back-end de la aplicación móvil, haga clic en **Toda la configuración** > **Tablas fáciles** o **API fáciles**, haga clic en una tabla o API y luego en **Editar script**.</span><span class="sxs-lookup"><span data-stu-id="66d9e-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="66d9e-521">El archivo de script se abrirá en el editor del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66d9e-521">The script file is opened in the App Service Editor.</span></span>

    ![Editor del Servicio de aplicaciones](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="66d9e-523">Realice los cambios en el archivo de código en el editor en línea.</span><span class="sxs-lookup"><span data-stu-id="66d9e-523">Make your changes to the code file in the online editor.</span></span> <span data-ttu-id="66d9e-524">Los cambios se guardan automáticamente a medida que se escriben.</span><span class="sxs-lookup"><span data-stu-id="66d9e-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
<span data-ttu-id="66d9e-525">[Inicio rápido de cliente de Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-525">[Android Client QuickStart]: app-service-mobile-android-get-started.md</span></span>
<span data-ttu-id="66d9e-526">[Inicio rápido de cliente de Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-526">[Apache Cordova Client QuickStart]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="66d9e-527">[Inicio rápido de cliente de iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-527">[iOS Client QuickStart]: app-service-mobile-ios-get-started.md</span></span>
<span data-ttu-id="66d9e-528">[Inicio rápido de cliente de Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-528">[Xamarin.iOS Client QuickStart]: app-service-mobile-xamarin-ios-get-started.md</span></span>
<span data-ttu-id="66d9e-529">[Inicio rápido de cliente de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-529">[Xamarin.Android Client QuickStart]: app-service-mobile-xamarin-android-get-started.md</span></span>
<span data-ttu-id="66d9e-530">[Inicio rápido de cliente de Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-530">[Xamarin.Forms Client QuickStart]: app-service-mobile-xamarin-forms-get-started.md</span></span>
<span data-ttu-id="66d9e-531">[Inicio rápido de cliente de Windows]: app-service-mobile-windows-store-dotnet-get-started.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-531">[Windows Store Client QuickStart]: app-service-mobile-windows-store-dotnet-get-started.md</span></span>
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
<span data-ttu-id="66d9e-532">[sincronización de datos sin conexión]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-532">[offline data sync]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="66d9e-533">[Configuración de la aplicación para usar el inicio de sesión de Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-533">[How to configure Azure Active Directory Authentication]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="66d9e-534">[Configuración de la aplicación para usar el inicio de sesión de Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-534">[How to configure Facebook Authentication]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="66d9e-535">[Configuración de la aplicación para usar el inicio de sesión de Google]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-535">[How to configure Google Authentication]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="66d9e-536">[Configuración de la aplicación para usar el inicio de sesión de Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-536">[How to configure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="66d9e-537">[Configuración de la aplicación para usar el inicio de sesión de Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-537">[How to configure Twitter Authentication]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
<span data-ttu-id="66d9e-538">[guía de implementación de Azure App Service]: ../app-service-web/web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-538">[Azure App Service Deployment Guide]: ../app-service-web/web-sites-deploy.md</span></span>
<span data-ttu-id="66d9e-539">[Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-539">[Monitoring an Azure App Service]: ../app-service-web/web-sites-monitor.md</span></span>
<span data-ttu-id="66d9e-540">[Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-540">[Enable Diagnostic Logging in Azure App Service]: ../app-service-web/web-sites-enable-diagnostic-log.md</span></span>
<span data-ttu-id="66d9e-541">[Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-541">[Troubleshoot an Azure App Service in Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md</span></span>
<span data-ttu-id="66d9e-542">[Especificación de una versión de Node.js en una aplicación Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-542">[specify the Node Version]: ../nodejs-specify-node-version-azure-apps.md</span></span>
<span data-ttu-id="66d9e-543">[Uso de módulos de Node]: ../nodejs-use-node-modules-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="66d9e-543">[use Node modules]: ../nodejs-use-node-modules-azure-apps.md</span></span>
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
<span data-ttu-id="66d9e-544">[Express]: http://expressjs.com/</span><span class="sxs-lookup"><span data-stu-id="66d9e-544">[Express]: http://expressjs.com/</span></span>
<span data-ttu-id="66d9e-545">[Swagger]: http://swagger.io/</span><span class="sxs-lookup"><span data-stu-id="66d9e-545">[Swagger]: http://swagger.io/</span></span>

<span data-ttu-id="66d9e-546">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="66d9e-546">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="66d9e-547">[OData]: http://www.odata.org</span><span class="sxs-lookup"><span data-stu-id="66d9e-547">[OData]: http://www.odata.org</span></span>
<span data-ttu-id="66d9e-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span><span class="sxs-lookup"><span data-stu-id="66d9e-548">[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise</span></span>
<span data-ttu-id="66d9e-549">[ejemplo "basicapp" en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span><span class="sxs-lookup"><span data-stu-id="66d9e-549">[basicapp sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app</span></span>
<span data-ttu-id="66d9e-550">[ejemplo "todo" en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span><span class="sxs-lookup"><span data-stu-id="66d9e-550">[todo sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo</span></span>
<span data-ttu-id="66d9e-551">[directorio de ejemplos de GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="66d9e-551">[samples directory on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples</span></span>
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
<span data-ttu-id="66d9e-552">[QueryJS]: https://github.com/Azure/queryjs</span><span class="sxs-lookup"><span data-stu-id="66d9e-552">[QueryJS]: https://github.com/Azure/queryjs</span></span>
<span data-ttu-id="66d9e-553">[Node.js Tools 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span><span class="sxs-lookup"><span data-stu-id="66d9e-553">[Node.js Tools 1.1 for Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1</span></span>
<span data-ttu-id="66d9e-554">[paquete de mssql para Node.js]: https://www.npmjs.com/package/mssql</span><span class="sxs-lookup"><span data-stu-id="66d9e-554">[mssql Node.js package]: https://www.npmjs.com/package/mssql</span></span>
<span data-ttu-id="66d9e-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span><span class="sxs-lookup"><span data-stu-id="66d9e-555">[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx</span></span>
<span data-ttu-id="66d9e-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span><span class="sxs-lookup"><span data-stu-id="66d9e-556">[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html</span></span>
<span data-ttu-id="66d9e-557">[Winston]: https://github.com/winstonjs/winston</span><span class="sxs-lookup"><span data-stu-id="66d9e-557">[Winston]: https://github.com/winstonjs/winston</span></span>
