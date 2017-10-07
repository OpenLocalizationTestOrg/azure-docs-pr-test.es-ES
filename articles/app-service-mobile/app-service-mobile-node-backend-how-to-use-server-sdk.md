---
title: "aaaHow toowork con el servidor back-end de Node.js Hola SDK para aplicaciones móviles | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowork con Hola servidor back-end de Node.js SDK para aplicaciones de Mobile de servicio de aplicación de Azure."
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
ms.openlocfilehash: 2b1ea5fda6f6ca422b92fe29ff8d16bf035018d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-nodejs-sdk"></a><span data-ttu-id="489d5-103">¿Cómo toouse Hola SDK de Node.js de aplicaciones móviles de Azure</span><span class="sxs-lookup"><span data-stu-id="489d5-103">How toouse hello Azure Mobile Apps Node.js SDK</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="489d5-104">Este artículo proporciona información detallada y ejemplos que muestran cómo toowork con un back-end de Node.js en aplicaciones de Mobile de servicio de aplicación de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d5-104">This article provides detailed information and examples showing how toowork with a Node.js backend in Azure App Service Mobile Apps.</span></span>

## <span data-ttu-id="489d5-105"><a name="Introduction"></a>Introducción</span><span class="sxs-lookup"><span data-stu-id="489d5-105"><a name="Introduction"></a>Introduction</span></span>
<span data-ttu-id="489d5-106">Aplicaciones móviles de Azure aplicación de servicio proporciona acceso de datos de tooadd optimizadas para el móvil de capacidad de hello aplicación de API Web tooa web.</span><span class="sxs-lookup"><span data-stu-id="489d5-106">Azure App Service Mobile Apps provides hello capability tooadd a mobile-optimized data access Web API tooa web application.</span></span>  <span data-ttu-id="489d5-107">Hola SDK de aplicaciones de Mobile de servicio de aplicaciones de Azure se proporciona para aplicaciones web ASP.NET y Node.js.</span><span class="sxs-lookup"><span data-stu-id="489d5-107">hello Azure App Service Mobile Apps SDK is provided for ASP.NET and Node.js web applications.</span></span>  <span data-ttu-id="489d5-108">Hola SDK proporciona hello las siguientes operaciones:</span><span class="sxs-lookup"><span data-stu-id="489d5-108">hello SDK provides hello following operations:</span></span>

* <span data-ttu-id="489d5-109">Operaciones de tabla (lectura, inserción, actualización, eliminación) para el acceso a datos</span><span class="sxs-lookup"><span data-stu-id="489d5-109">Table operations (Read, Insert, Update, Delete) for data access</span></span>
* <span data-ttu-id="489d5-110">Operaciones API personalizadas</span><span class="sxs-lookup"><span data-stu-id="489d5-110">Custom API operations</span></span>

<span data-ttu-id="489d5-111">Ambas operaciones se incluyen para autenticación en todos los proveedores de identidades permitidos por el Servicio de aplicaciones de Azure, incluidos los proveedores de identidades sociales, como Facebook, Twitter, Google y Microsoft, así como Azure Active Directory para la identidad de empresa.</span><span class="sxs-lookup"><span data-stu-id="489d5-111">Both operations provide for authentication across all identity providers allowed by Azure App Service, including social identity providers such as Facebook, Twitter, Google and Microsoft as well as Azure Active Directory for enterprise identity.</span></span>

<span data-ttu-id="489d5-112">Puede encontrar ejemplos para cada caso de uso en hello [directorio de ejemplos en GitHub].</span><span class="sxs-lookup"><span data-stu-id="489d5-112">You can find samples for each use case in hello [samples directory on GitHub].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="489d5-113">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="489d5-113">Supported Platforms</span></span>
<span data-ttu-id="489d5-114">Hola SDK de nodo de aplicaciones móviles de Azure admite hello que LTS actuales de la versión del nodo y versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="489d5-114">hello Azure Mobile Apps Node SDK supports hello current LTS release of Node and later.</span></span>  <span data-ttu-id="489d5-115">Redactar, versión más reciente de LTS de hello es v4.5.0 de nodo.</span><span class="sxs-lookup"><span data-stu-id="489d5-115">As of writing, hello latest LTS version is Node v4.5.0.</span></span>  <span data-ttu-id="489d5-116">Aunque es posible que funcionen otras versiones de Node, no son compatibles.</span><span class="sxs-lookup"><span data-stu-id="489d5-116">Other versions of Node may work, but are not supported.</span></span>

<span data-ttu-id="489d5-117">Hola SDK de nodo de aplicaciones móviles de Azure es compatible con dos controladores de base de datos: hello nodo mssql controlador es compatible con SQL Azure y las instancias de SQL Server locales.</span><span class="sxs-lookup"><span data-stu-id="489d5-117">hello Azure Mobile Apps Node SDK supports two database drivers - hello node-mssql driver supports SQL Azure and local SQL Server instances.</span></span>  <span data-ttu-id="489d5-118">controlador de sqlite3 de Hello es compatible con las bases de datos de SQLite en una sola instancia.</span><span class="sxs-lookup"><span data-stu-id="489d5-118">hello sqlite3 driver supports SQLite databases on a single instance only.</span></span>

### <span data-ttu-id="489d5-119"><a name="howto-cmdline-basicapp"></a>Cómo: crear un back-end de Node.js básico mediante la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-119"><a name="howto-cmdline-basicapp"></a>How to: Create a Basic Node.js backend using hello Command Line</span></span>
<span data-ttu-id="489d5-120">Cada back-end de Node.js de aplicación móvil del Servicio de aplicaciones de Azure se inicia como una aplicación ExpressJS.</span><span class="sxs-lookup"><span data-stu-id="489d5-120">Every Azure App Service Mobile App Node.js backend starts as an ExpressJS application.</span></span>  <span data-ttu-id="489d5-121">ExpressJS es hello más popular marco del servicio web disponible para Node.js.</span><span class="sxs-lookup"><span data-stu-id="489d5-121">ExpressJS is hello most popular web service framework available for Node.js.</span></span>  <span data-ttu-id="489d5-122">Puede crear una aplicación [Express] básica de la forma siguiente:</span><span class="sxs-lookup"><span data-stu-id="489d5-122">You can create a basic [Express] application as follows:</span></span>

1. <span data-ttu-id="489d5-123">En una ventana de comandos o de PowerShell, cree un directorio para el proyecto.</span><span class="sxs-lookup"><span data-stu-id="489d5-123">In a command or PowerShell window, create a directory for your project.</span></span>

        mkdir basicapp
2. <span data-ttu-id="489d5-124">Ejecute la estructura del paquete de npm init tooinitialize Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-124">Run npm init tooinitialize hello package structure.</span></span>

        cd basicapp
        npm init

    <span data-ttu-id="489d5-125">comando de Hello npm init solicita un conjunto de proyectos de hello tooinitialize preguntas.</span><span class="sxs-lookup"><span data-stu-id="489d5-125">hello npm init command asks a set of questions tooinitialize hello project.</span></span>  <span data-ttu-id="489d5-126">Ver un resultado de ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="489d5-126">See hello example output:</span></span>

    ![salida de Hello npm init][0]
3. <span data-ttu-id="489d5-128">Instalar bibliotecas de express y aplicaciones móviles de azure de Hola de repositorio de npm Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-128">Install hello express and azure-mobile-apps libraries from hello npm repository.</span></span>

        npm install --save express azure-mobile-apps
4. <span data-ttu-id="489d5-129">Crear un app.js tooimplement hello básico móviles servidor de archivos.</span><span class="sxs-lookup"><span data-stu-id="489d5-129">Create an app.js file tooimplement hello basic mobile server.</span></span>

        var express = require('express'),
            azureMobileApps = require('azure-mobile-apps');

        var app = express(),
            mobile = azureMobileApps();

        // Define a TodoItem table
        mobile.tables.add('TodoItem');

        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);

<span data-ttu-id="489d5-130">Esta aplicación crea una WebAPI móvil optimizada con un solo punto de conexión (`/tables/TodoItem`) que proporciona tooan de acceso no autenticado subyacente de almacén de datos SQL mediante un esquema dinámico.</span><span class="sxs-lookup"><span data-stu-id="489d5-130">This application creates a mobile-optimized WebAPI with a single endpoint (`/tables/TodoItem`) that provides unauthenticated access tooan underlying SQL data store using a dynamic schema.</span></span>  <span data-ttu-id="489d5-131">Es adecuado para los siguientes inicios rápidos de la biblioteca de cliente:</span><span class="sxs-lookup"><span data-stu-id="489d5-131">It is suitable for following the client library quick starts:</span></span>

* <span data-ttu-id="489d5-132">[Inicio rápido de cliente de Android]</span><span class="sxs-lookup"><span data-stu-id="489d5-132">[Android Client QuickStart]</span></span>
* <span data-ttu-id="489d5-133">[Inicio rápido de cliente de Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="489d5-133">[Apache Cordova Client QuickStart]</span></span>
* <span data-ttu-id="489d5-134">[Inicio rápido de cliente de iOS]</span><span class="sxs-lookup"><span data-stu-id="489d5-134">[iOS Client QuickStart]</span></span>
* <span data-ttu-id="489d5-135">[Inicio rápido de cliente de Windows]</span><span class="sxs-lookup"><span data-stu-id="489d5-135">[Windows Store Client QuickStart]</span></span>
* <span data-ttu-id="489d5-136">[Inicio rápido de cliente de Xamarin.iOS]</span><span class="sxs-lookup"><span data-stu-id="489d5-136">[Xamarin.iOS Client QuickStart]</span></span>
* <span data-ttu-id="489d5-137">[Inicio rápido de cliente de Xamarin.Android]</span><span class="sxs-lookup"><span data-stu-id="489d5-137">[Xamarin.Android Client QuickStart]</span></span>
* <span data-ttu-id="489d5-138">[Inicio rápido de cliente de Xamarin.Forms]</span><span class="sxs-lookup"><span data-stu-id="489d5-138">[Xamarin.Forms Client QuickStart]</span></span>

<span data-ttu-id="489d5-139">Puede encontrar código de hello para esta aplicación básica de hello [ejemplo basicapp en GitHub].</span><span class="sxs-lookup"><span data-stu-id="489d5-139">You can find hello code for this basic application in hello [basicapp sample on GitHub].</span></span>

### <span data-ttu-id="489d5-140"><a name="howto-vs2015-basicapp"></a>Creación de un back-end de Node con Visual Studio de 2015</span><span class="sxs-lookup"><span data-stu-id="489d5-140"><a name="howto-vs2015-basicapp"></a>How to: Create a Node backend with Visual Studio 2015</span></span>
<span data-ttu-id="489d5-141">Visual Studio 2015 requiere una aplicación de extensión toodevelop Node.js en hello IDE.</span><span class="sxs-lookup"><span data-stu-id="489d5-141">Visual Studio 2015 requires an extension toodevelop Node.js applications within hello IDE.</span></span>  <span data-ttu-id="489d5-142">toostart, instalar hello [Node.js Tools 1.1 para Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="489d5-142">toostart, install hello [Node.js Tools 1.1 for Visual Studio].</span></span>  <span data-ttu-id="489d5-143">Una vez que se instalan hello Node.js Tools para Visual Studio, cree una aplicación de 4.x Express:</span><span class="sxs-lookup"><span data-stu-id="489d5-143">Once hello Node.js Tools for Visual Studio are installed, create an Express 4.x application:</span></span>

1. <span data-ttu-id="489d5-144">Abra hello **nuevo proyecto** diálogo (desde **archivo** > **New** > **proyecto...** ).</span><span class="sxs-lookup"><span data-stu-id="489d5-144">Open hello **New Project** dialog (from **File** > **New** > **Project...**).</span></span>
2. <span data-ttu-id="489d5-145">Expanda **Plantillas** > **JavaScript** > **Node.js**.</span><span class="sxs-lookup"><span data-stu-id="489d5-145">Expand **Templates** > **JavaScript** > **Node.js**.</span></span>
3. <span data-ttu-id="489d5-146">Seleccione hello **básica Node.js de Azure Express 4 aplicación**.</span><span class="sxs-lookup"><span data-stu-id="489d5-146">Select hello **Basic Azure Node.js Express 4 Application**.</span></span>
4. <span data-ttu-id="489d5-147">Rellene el nombre del proyecto de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-147">Fill in hello project name.</span></span>  <span data-ttu-id="489d5-148">Haga clic en *Aceptar*.</span><span class="sxs-lookup"><span data-stu-id="489d5-148">Click *OK*.</span></span>

    ![Nuevo proyecto de Visual Studio de 2015][1]
5. <span data-ttu-id="489d5-150">Menú contextual hello **npm** nodo y seleccione **instalar nuevos paquetes de npm...** .</span><span class="sxs-lookup"><span data-stu-id="489d5-150">Right-click hello **npm** node and select **Install New npm packages...**.</span></span>
6. <span data-ttu-id="489d5-151">Puede que necesite toorefresh catálogo de npm Hola acerca de cómo crear su primera aplicación Node.js.</span><span class="sxs-lookup"><span data-stu-id="489d5-151">You may need toorefresh hello npm catalog on creating your first Node.js application.</span></span>  <span data-ttu-id="489d5-152">Haga clic en **Actualizar** si es necesario.</span><span class="sxs-lookup"><span data-stu-id="489d5-152">Click **Refresh** if necessary.</span></span>
7. <span data-ttu-id="489d5-153">Escriba *aplicaciones móviles de azure* en el cuadro de búsqueda de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-153">Enter *azure-mobile-apps* in hello search box.</span></span>  <span data-ttu-id="489d5-154">Haga clic en hello **azure-mobile-apps 2.0.0** del paquete, a continuación, haga clic en **Instalar paquete**.</span><span class="sxs-lookup"><span data-stu-id="489d5-154">Click hello **azure-mobile-apps 2.0.0** package, then click **Install Package**.</span></span>

    ![Instalar nuevos paquetes npm][2]
8. <span data-ttu-id="489d5-156">Haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-156">Click **Close**.</span></span>
9. <span data-ttu-id="489d5-157">Abra hello *app.js* tooadd compatibilidad para hello SDK de aplicaciones móviles de Azure de archivos.</span><span class="sxs-lookup"><span data-stu-id="489d5-157">Open hello *app.js* file tooadd support for hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="489d5-158">En parte inferior de línea de 6 at Hola de biblioteca de hello requieren instrucciones, agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="489d5-158">At line 6 at hello bottom of hello library require statements, add hello following code:</span></span>

        var bodyParser = require('body-parser');
        var azureMobileApps = require('azure-mobile-apps');

    <span data-ttu-id="489d5-159">En aproximadamente línea 27 después Hola otras instrucciones app.use, agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="489d5-159">At approximately line 27 after hello other app.use statements, add hello following code:</span></span>

        app.use('/users', users);

        // Azure Mobile Apps Initialization
        var mobile = azureMobileApps();
        mobile.tables.add('TodoItem');
        app.use(mobile);

    <span data-ttu-id="489d5-160">Guarde el archivo hello.</span><span class="sxs-lookup"><span data-stu-id="489d5-160">Save hello file.</span></span>
10. <span data-ttu-id="489d5-161">Ejecutar aplicación de hello localmente (Hola API se sirve en http://localhost:3000) o publicar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="489d5-161">Either run hello application locally (hello API is served on http://localhost:3000) or publish tooAzure.</span></span>

### <span data-ttu-id="489d5-162"><a name="create-node-backend-portal"></a>Cómo: crear un back-end de Node.js con hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="489d5-162"><a name="create-node-backend-portal"></a>How to: Create a Node.js backend using hello Azure portal</span></span>
<span data-ttu-id="489d5-163">Puede crear un derecho de back-end de la aplicación móvil en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-163">You can create a Mobile App backend right in hello [Azure portal].</span></span> <span data-ttu-id="489d5-164">O bien puede seguir Hola siguientes pasos o crear un cliente y servidor juntos Hola después [crear una aplicación móvil](app-service-mobile-ios-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="489d5-164">You can either follow hello following steps or create a client and server together by following hello [Create a mobile app](app-service-mobile-ios-get-started.md) tutorial.</span></span> <span data-ttu-id="489d5-165">tutorial de Hello contiene una versión simplificada de estas instrucciones y es más adecuado para la prueba de proyectos de concepto.</span><span class="sxs-lookup"><span data-stu-id="489d5-165">hello tutorial contains a simplified version of these instructions and is best for proof of concept projects.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="489d5-166">En hello *Introducción* hoja, en **crear una tabla API**, elija **Node.js** como su **idioma de back-end**.</span><span class="sxs-lookup"><span data-stu-id="489d5-166">Back in hello *Get started* blade, under **Create a table API**, choose **Node.js** as your **Backend language**.</span></span>
<span data-ttu-id="489d5-167">Casilla de Hola para "**reconozco que esta acción sobrescribirá todo contenido de sitio.**", a continuación, haga clic en **TodoItem crear tabla**.</span><span class="sxs-lookup"><span data-stu-id="489d5-167">Check hello box for "**I acknowledge that this will overwrite all site contents.**", then click **Create TodoItem table**.</span></span>

### <span data-ttu-id="489d5-168"><a name="download-quickstart"></a>Cómo: Descargar proyecto de código de la inicio rápido de hello Node.js back-end mediante Git</span><span class="sxs-lookup"><span data-stu-id="489d5-168"><a name="download-quickstart"></a>How to: Download hello Node.js backend quickstart code project using Git</span></span>
<span data-ttu-id="489d5-169">Cuando se crea un aplicación de Node.js móvil de back-end mediante el portal de hello **inicio rápido** hoja, se crea un proyecto de Node.js para usted y sitio tooyour implementado.</span><span class="sxs-lookup"><span data-stu-id="489d5-169">When you create a Node.js Mobile App backend by using hello portal **Quick start** blade, a Node.js project is created for you and deployed tooyour site.</span></span> <span data-ttu-id="489d5-170">Puede agregar tablas y las API y editar archivos de código de back-end de hello Node.js en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-170">You can add tables and APIs and edit code files for hello Node.js backend in hello portal.</span></span> <span data-ttu-id="489d5-171">También puede utilizar el proyecto de back-end de hello toodownload de herramientas de implementación distintos por lo que puede agregar o modificar las tablas y las API y luego volver a publicar proyecto Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-171">You can also use various deployment tools toodownload hello backend project so that you can add or modify tables and APIs, then republish hello project.</span></span> <span data-ttu-id="489d5-172">Para obtener más información, consulte la [guía de implementación de Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="489d5-172">For more information, see the [Azure App Service Deployment Guide].</span></span> <span data-ttu-id="489d5-173">Hello siguiente procedimiento usa un código de proyecto de inicio rápido de Git repositorio toodownload Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-173">hello following procedure uses a Git repository toodownload hello quickstart project code.</span></span>

1. <span data-ttu-id="489d5-174">Si aún no lo ha hecho, instale Git.</span><span class="sxs-lookup"><span data-stu-id="489d5-174">Install Git, if you haven't already done so.</span></span> <span data-ttu-id="489d5-175">Hola pasos necesarios tooinstall Git varían entre los sistemas operativos.</span><span class="sxs-lookup"><span data-stu-id="489d5-175">hello steps required tooinstall Git vary between operating systems.</span></span> <span data-ttu-id="489d5-176">Consulte el artículo de [instalación de Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) para obtener una guía sobre la instalación y las distribuciones específicas del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="489d5-176">See [Installing Git](http://git-scm.com/book/en/Getting-Started-Installing-Git) for operating system-specific distributions and installation guidance.</span></span>
2. <span data-ttu-id="489d5-177">Siga los pasos de hello en [Enable Hola repositorio de aplicación de servicio de aplicaciones](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable repositorio de Git de hello para el sitio de back-end, que realiza una nota del nombre de usuario de implementación de Hola y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="489d5-177">Follow hello steps in [Enable hello App Service app repository](../app-service-web/app-service-deploy-local-git.md#Step3) tooenable hello Git repository for your backend site, making a note of hello deployment username and password.</span></span>
3. <span data-ttu-id="489d5-178">En la hoja de Hola para su aplicación móvil de back-end, tome nota de hello **dirección URL de clonación de Git** configuración.</span><span class="sxs-lookup"><span data-stu-id="489d5-178">In hello blade for your Mobile App backend, make a note of hello **Git clone URL** setting.</span></span>
4. <span data-ttu-id="489d5-179">Ejecute hello `git clone` comando mediante la dirección URL de clonación de Git hello, escribir la contraseña cuando sea necesario, como en el ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="489d5-179">Execute hello `git clone` command using hello Git clone URL, entering your password when required, as in the following example:</span></span>

        $ git clone https://username@todolist.scm.azurewebsites.net:443/todolist.git
5. <span data-ttu-id="489d5-180">Directorio de toolocal examinar, que en el anterior ejemplo de Hola es /todolist y tenga en cuenta que los archivos de proyecto se han descargado.</span><span class="sxs-lookup"><span data-stu-id="489d5-180">Browse toolocal directory, which in hello preceding example is /todolist, and notice that project files have been downloaded.</span></span> <span data-ttu-id="489d5-181">Busque hello `todoitem.json` archivo Hola `/tables` directory.</span><span class="sxs-lookup"><span data-stu-id="489d5-181">Locate hello `todoitem.json` file in hello `/tables` directory.</span></span>  <span data-ttu-id="489d5-182">Este archivo define permisos en la tabla.</span><span class="sxs-lookup"><span data-stu-id="489d5-182">This file defines permissions on the table.</span></span>  <span data-ttu-id="489d5-183">También encontrará hello `todoitem.js` en el archivo hello mismo directorio, que define que operación CRUD secuencias de comandos para la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-183">Also find hello `todoitem.js` file in hello same directory, which defines that CRUD operation scripts for hello table.</span></span>
6. <span data-ttu-id="489d5-184">Después de realizar cambios tooproject archivos, ejecute hello siga los comandos tooadd, confirmar, a continuación, cargar el sitio de toohello de cambios:</span><span class="sxs-lookup"><span data-stu-id="489d5-184">After you have made changes tooproject files, execute hello following commands tooadd, commit, then upload the changes toohello site:</span></span>

        $ git commit -m "updated hello table script"
        $ git push origin master

    <span data-ttu-id="489d5-185">Cuando se agrega el nuevo proyecto de archivos toohello, primero debe hello tooexecute `git add .` comando.</span><span class="sxs-lookup"><span data-stu-id="489d5-185">When you add new files toohello project, you first need tooexecute hello `git add .` command.</span></span>

<span data-ttu-id="489d5-186">sitio de Hola se vuelve a publicar cada vez que se inserta un nuevo conjunto de confirmaciones de toohello sitio.</span><span class="sxs-lookup"><span data-stu-id="489d5-186">hello site is republished every time a new set of commits is pushed toohello site.</span></span>

### <span data-ttu-id="489d5-187"><a name="howto-publish-to-azure"></a>Cómo: publicar su tooAzure de back-end de Node.js</span><span class="sxs-lookup"><span data-stu-id="489d5-187"><a name="howto-publish-to-azure"></a>How to: Publish your Node.js backend tooAzure</span></span>
<span data-ttu-id="489d5-188">Microsoft Azure proporciona varios mecanismos para publicar su Node.js de aplicaciones de Azure aplicación Servicio móvil de back-end para Hola servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d5-188">Microsoft Azure provides many mechanisms for publishing your Azure App Service Mobile Apps Node.js backend to hello Azure service.</span></span>  <span data-ttu-id="489d5-189">Incluyen el uso de herramientas de implementación integradas en Visual Studio, herramientas de línea de comandos y opciones de implementación continua basadas en control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="489d5-189">These include utilizing deployment tools integrated into Visual Studio, command-line tools, and continuous deployment options based on source control.</span></span>  <span data-ttu-id="489d5-190">Para obtener más información sobre este tema, consulte la [guía de implementación de Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="489d5-190">For more information on this topic, see the [Azure App Service Deployment Guide].</span></span>

<span data-ttu-id="489d5-191">El Servicio de aplicaciones de Azure tiene instrucciones específicas para la aplicación de Node.js que usted debe revisar antes de realizar la implementación:</span><span class="sxs-lookup"><span data-stu-id="489d5-191">Azure App Service has specific advice for Node.js application that you should review before deploying:</span></span>

* <span data-ttu-id="489d5-192">Cómo demasiado[especificar Hola versión del nodo]</span><span class="sxs-lookup"><span data-stu-id="489d5-192">How too[specify hello Node Version]</span></span>
* <span data-ttu-id="489d5-193">Cómo demasiado[usar módulos de nodo]</span><span class="sxs-lookup"><span data-stu-id="489d5-193">How too[use Node modules]</span></span>

### <span data-ttu-id="489d5-194"><a name="howto-enable-homepage"></a>Habilitación de una página de inicio para la aplicación</span><span class="sxs-lookup"><span data-stu-id="489d5-194"><a name="howto-enable-homepage"></a>How to: Enable a Home Page for your application</span></span>
<span data-ttu-id="489d5-195">Muchas aplicaciones son una combinación de aplicaciones móviles y web y el marco de trabajo de hello ExpressJS permite toocombine los dos facetas.</span><span class="sxs-lookup"><span data-stu-id="489d5-195">Many applications are a combination of web and mobile apps and hello ExpressJS framework allows you toocombine the two facets.</span></span>  <span data-ttu-id="489d5-196">A veces, sin embargo, es recomendable tooonly implemente una interfaz móvil.</span><span class="sxs-lookup"><span data-stu-id="489d5-196">Sometimes, however, you may wish tooonly implement a mobile interface.</span></span>  <span data-ttu-id="489d5-197">Resulta útil tooprovide que un servicio de aplicaciones de aterrizaje página tooensure Hola está en funcionamiento.</span><span class="sxs-lookup"><span data-stu-id="489d5-197">It is useful tooprovide a landing page tooensure hello app service is up and running.</span></span>  <span data-ttu-id="489d5-198">Puede proporcionar su propia página de inicio o habilitar una de carácter temporal.</span><span class="sxs-lookup"><span data-stu-id="489d5-198">You can either provide your own home page or enable a temporary home page.</span></span>  <span data-ttu-id="489d5-199">tooenable una página principal temporal, utilice Hola después de aplicaciones móviles de Azure de tooinstantiate:</span><span class="sxs-lookup"><span data-stu-id="489d5-199">tooenable a temporary home page, use hello following tooinstantiate Azure Mobile Apps:</span></span>

    var mobile = azureMobileApps({ homePage: true });

<span data-ttu-id="489d5-200">Si solo desea que esta opción está disponible al desarrollar de forma local, puede agregar esta configuración tooyour `azureMobile.js` archivo.</span><span class="sxs-lookup"><span data-stu-id="489d5-200">If you only want this option available when developing locally, you can add this setting tooyour `azureMobile.js` file.</span></span>

## <span data-ttu-id="489d5-201"><a name="TableOperations"></a>Operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="489d5-201"><a name="TableOperations"></a>Table operations</span></span>
<span data-ttu-id="489d5-202">Hello SDK de servidor de aplicaciones móviles de azure Node.js proporciona mecanismos tooexpose datos las tablas almacenadas en la base de datos de SQL de Azure como un WebAPI.</span><span class="sxs-lookup"><span data-stu-id="489d5-202">hello azure-mobile-apps Node.js Server SDK provides mechanisms tooexpose data tables stored in Azure SQL Database as a WebAPI.</span></span>  <span data-ttu-id="489d5-203">Se proporcionan cinco operaciones.</span><span class="sxs-lookup"><span data-stu-id="489d5-203">Five operations are provided.</span></span>

| <span data-ttu-id="489d5-204">Operación</span><span class="sxs-lookup"><span data-stu-id="489d5-204">Operation</span></span> | <span data-ttu-id="489d5-205">Descripción</span><span class="sxs-lookup"><span data-stu-id="489d5-205">Description</span></span> |
| --- | --- |
| <span data-ttu-id="489d5-206">GET /tables/*nombredelatabla*</span><span class="sxs-lookup"><span data-stu-id="489d5-206">GET /tables/*tablename*</span></span> |<span data-ttu-id="489d5-207">Obtener todos los registros en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-207">Get all records in hello table</span></span> |
| <span data-ttu-id="489d5-208">GET /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="489d5-208">GET /tables/*tablename*/:id</span></span> |<span data-ttu-id="489d5-209">Obtener un registro específico en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-209">Get a specific record in hello table</span></span> |
| <span data-ttu-id="489d5-210">POST /tables/*nombredelatabla*</span><span class="sxs-lookup"><span data-stu-id="489d5-210">POST /tables/*tablename*</span></span> |<span data-ttu-id="489d5-211">Crear un registro en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-211">Create a record in hello table</span></span> |
| <span data-ttu-id="489d5-212">PATCH /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="489d5-212">PATCH /tables/*tablename*/:id</span></span> |<span data-ttu-id="489d5-213">Actualizar un registro en la tabla Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-213">Update a record in hello table</span></span> |
| <span data-ttu-id="489d5-214">DELETE /tables/*nombredelatabla*/:id</span><span class="sxs-lookup"><span data-stu-id="489d5-214">DELETE /tables/*tablename*/:id</span></span> |<span data-ttu-id="489d5-215">Eliminar un registro de la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-215">Delete a record in hello table</span></span> |

<span data-ttu-id="489d5-216">Es compatible con esta WebAPI [OData] y extiende Hola tabla esquema toosupport [sincronización de datos sin conexión].</span><span class="sxs-lookup"><span data-stu-id="489d5-216">This WebAPI supports [OData] and extends hello table schema toosupport [offline data sync].</span></span>

### <span data-ttu-id="489d5-217"><a name="howto-dynamicschema"></a>Definición de tablas con un esquema dinámico</span><span class="sxs-lookup"><span data-stu-id="489d5-217"><a name="howto-dynamicschema"></a>How to: Define tables using a dynamic schema</span></span>
<span data-ttu-id="489d5-218">Antes de usar una tabla, esta debe definirse.</span><span class="sxs-lookup"><span data-stu-id="489d5-218">Before a table can be used, it must be defined.</span></span>  <span data-ttu-id="489d5-219">Las tablas pueden definirse con un esquema estático (donde desarrollador Hola define columnas hello en el esquema de hello) o dinámicamente (donde hello SDK controla el esquema de hello en función de las solicitudes entrantes).</span><span class="sxs-lookup"><span data-stu-id="489d5-219">Tables can be defined with a static schema (where hello developer defines hello columns within hello schema) or dynamically (where hello SDK controls hello schema based on incoming requests).</span></span> <span data-ttu-id="489d5-220">Además, para desarrolladores de hello pueden controlar aspectos específicos de hello WebAPI mediante la adición de definición de toohello de código de Javascript.</span><span class="sxs-lookup"><span data-stu-id="489d5-220">In addition, hello developer can control specific aspects of hello WebAPI by adding Javascript code toohello definition.</span></span>

<span data-ttu-id="489d5-221">Como práctica recomendada, se debe definir cada tabla en un archivo de Javascript en el directorio de tablas de hello, utilice las tablas de hello tables.import() método tooimport.</span><span class="sxs-lookup"><span data-stu-id="489d5-221">As a best practice, you should define each table in a Javascript file in hello tables directory, then use the tables.import() method tooimport hello tables.</span></span>  <span data-ttu-id="489d5-222">Extender la aplicación hello basic, se ajustaría archivo app.js de hello:</span><span class="sxs-lookup"><span data-stu-id="489d5-222">Extending hello basic-app, hello app.js file would be adjusted:</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Define hello database schema that is exposed
    mobile.tables.import('./tables');

    // Provide initialization of any tables that are statically defined
    mobile.tables.initialize().then(function () {
        // Add hello mobile API so it is accessible as a Web API
        app.use(mobile);

        // Start listening on HTTP
        app.listen(process.env.PORT || 3000);
    });

<span data-ttu-id="489d5-223">Definir la tabla de hello en. / tables/TodoItem.js:</span><span class="sxs-lookup"><span data-stu-id="489d5-223">Define hello table in ./tables/TodoItem.js:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Additional configuration for hello table goes here

    module.exports = table;

<span data-ttu-id="489d5-224">Las tablas usan el esquema dinámico de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="489d5-224">Tables use dynamic schema by default.</span></span>  <span data-ttu-id="489d5-225">tooturn desactivar esquema dinámico globalmente, Establece configuración de la aplicación hello **MS_DynamicSchema** toofalse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d5-225">tooturn off dynamic schema globally, set hello App Setting **MS_DynamicSchema** toofalse within hello Azure portal.</span></span>

<span data-ttu-id="489d5-226">Puede encontrar un ejemplo completo en hello [ejemplo de lista de tareas en GitHub].</span><span class="sxs-lookup"><span data-stu-id="489d5-226">You can find a complete example in hello [todo sample on GitHub].</span></span>

### <span data-ttu-id="489d5-227"><a name="howto-staticschema"></a>Definición de tablas con un esquema estático</span><span class="sxs-lookup"><span data-stu-id="489d5-227"><a name="howto-staticschema"></a>How to: Define tables using a static schema</span></span>
<span data-ttu-id="489d5-228">Puede definir explícitamente Hola columnas tooexpose a través de hello WebAPI.</span><span class="sxs-lookup"><span data-stu-id="489d5-228">You can explicitly define hello columns tooexpose via hello WebAPI.</span></span>  <span data-ttu-id="489d5-229">Hola que SDK de Node.js de aplicaciones móviles de azure agrega automáticamente las columnas adicionales necesarias para la lista de toohello de sincronización de datos sin conexión que proporcione.</span><span class="sxs-lookup"><span data-stu-id="489d5-229">hello azure-mobile-apps Node.js SDK automatically adds any additional columns required for offline data sync toohello list that you provide.</span></span>  <span data-ttu-id="489d5-230">Por ejemplo, las aplicaciones de cliente de inicio rápido requieren una tabla con dos columnas: text (una cadena) y complete (un booleano).</span><span class="sxs-lookup"><span data-stu-id="489d5-230">For example, the QuickStart client applications require a table with two columns: text (a string) and complete (a boolean).</span></span>  
<span data-ttu-id="489d5-231">tabla de Hola se puede definir en la tabla definición JavaScript archivo hello (que se encuentra en el directorio de tablas de hello) como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="489d5-231">hello table can be defined in hello table definition JavaScript file (located in hello tables directory) as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    module.exports = table;

<span data-ttu-id="489d5-232">Si define las tablas estáticamente, también debe llamar esquema de base de datos de hello tables.initialize() método toocreate Hola durante el inicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-232">If you define tables statically, then you must also call hello tables.initialize() method toocreate hello database schema on startup.</span></span>  <span data-ttu-id="489d5-233">Hola tables.initialize() método devuelve un [Promise] para que el servicio web de hello no sirve a las solicitudes antes de la base de datos de Hola que se está inicializando.</span><span class="sxs-lookup"><span data-stu-id="489d5-233">hello tables.initialize() method returns a [Promise] so that hello web service does not serve requests before hello database being initialized.</span></span>

### <span data-ttu-id="489d5-234"><a name="howto-sqlexpress-setup"></a>Uso de SQL Express como almacén de datos de desarrollo en el equipo local</span><span class="sxs-lookup"><span data-stu-id="489d5-234"><a name="howto-sqlexpress-setup"></a>How to: Use SQL Express as a development data store on your local machine</span></span>
<span data-ttu-id="489d5-235">Hola Hola AzureMobile aplicaciones nodo SDK de aplicaciones móviles de Azure proporciona tres opciones para servir datos fuera del cuadro de hello: SDK proporciona tres opciones para enviar datos desde el principio de hello:</span><span class="sxs-lookup"><span data-stu-id="489d5-235">hello Azure Mobile Apps hello AzureMobile Apps Node SDK provides three options for serving data out of hello box: SDK provides three options for serving data out of hello box:</span></span>

* <span data-ttu-id="489d5-236">Hola de uso **memoria** almacén de controladores de ejemplo tooprovide no persistentes</span><span class="sxs-lookup"><span data-stu-id="489d5-236">Use hello **memory** driver tooprovide a non-persistent example store</span></span>
* <span data-ttu-id="489d5-237">Hola de uso **mssql** tooprovide controlador para el desarrollo de un almacén de datos SQL Express</span><span class="sxs-lookup"><span data-stu-id="489d5-237">Use hello **mssql** driver tooprovide a SQL Express data store for development</span></span>
* <span data-ttu-id="489d5-238">Hola de uso **mssql** controlador tooprovide un almacén de datos de la base de datos de SQL Azure para la producción</span><span class="sxs-lookup"><span data-stu-id="489d5-238">Use hello **mssql** driver tooprovide an Azure SQL Database data store for production</span></span>

<span data-ttu-id="489d5-239">Hola SDK de Node.js de aplicaciones móviles de Azure usa hello [mssql Node.js paquete] tooestablish y utilizar una base de datos de SQL y tooboth de conexión SQL Express.</span><span class="sxs-lookup"><span data-stu-id="489d5-239">hello Azure Mobile Apps Node.js SDK uses hello [mssql Node.js package] tooestablish and use a connection tooboth SQL Express and SQL Database.</span></span>  <span data-ttu-id="489d5-240">Este paquete requiere que habilite las conexiones TCP en la instancia de SQL Express.</span><span class="sxs-lookup"><span data-stu-id="489d5-240">This package requires that you enable TCP connections on your SQL Express instance.</span></span>

> [!TIP]
> <span data-ttu-id="489d5-241">controlador de memoria de Hello no proporciona un conjunto completo de servicios para probar.</span><span class="sxs-lookup"><span data-stu-id="489d5-241">hello memory driver does not provide a complete set of facilities for testing.</span></span>  <span data-ttu-id="489d5-242">Si desea tootest el back-end de forma local, se recomienda usar Hola de un almacén de datos de SQL Express y Hola mssql controlador.</span><span class="sxs-lookup"><span data-stu-id="489d5-242">If you wish tootest your backend locally, we recommend hello use of a SQL Express data store and hello mssql driver.</span></span>
>
>

1. <span data-ttu-id="489d5-243">Descargue e instale [Microsoft SQL Server 2014 Express].</span><span class="sxs-lookup"><span data-stu-id="489d5-243">Download and install [Microsoft SQL Server 2014 Express].</span></span>  <span data-ttu-id="489d5-244">Asegúrese de que instalar SQL Server 2014 Express de hello con la edición de herramientas.</span><span class="sxs-lookup"><span data-stu-id="489d5-244">Ensure you install hello SQL Server 2014 Express with Tools edition.</span></span>  <span data-ttu-id="489d5-245">A menos que necesite explícitamente la compatibilidad con 64 bits, versión de 32 bits de hello consume menos memoria cuando se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="489d5-245">Unless you explicitly require 64-bit support, hello 32-bit version consumes less memory when running.</span></span>
2. <span data-ttu-id="489d5-246">Ejecute hello Administrador de configuración de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="489d5-246">Run hello SQL Server 2014 Configuration Manager.</span></span>

   1. <span data-ttu-id="489d5-247">Expanda hello **configuración de red de SQL Server** nodo en el menú de árbol de la izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-247">Expand hello **SQL Server Network Configuration** node in hello left-hand tree menu.</span></span>
   2. <span data-ttu-id="489d5-248">Haga clic en **Protocolos para SQLEXPRESS**.</span><span class="sxs-lookup"><span data-stu-id="489d5-248">Click **Protocols for SQLEXPRESS**.</span></span>
   3. <span data-ttu-id="489d5-249">Haga clic con el botón derecho en **TCP/IP** y seleccione **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-249">Right-click **TCP/IP** and select **Enable**.</span></span>  <span data-ttu-id="489d5-250">Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-250">Click **OK** in hello pop-up dialog.</span></span>
   4. <span data-ttu-id="489d5-251">Haga clic con el botón derecho en **TCP/IP** y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="489d5-251">Right-click **TCP/IP** and select **Properties**.</span></span>
   5. <span data-ttu-id="489d5-252">Haga clic en hello **direcciones IP** ficha.</span><span class="sxs-lookup"><span data-stu-id="489d5-252">Click hello **IP Addresses** tab.</span></span>
   6. <span data-ttu-id="489d5-253">Buscar hello **IPAll** nodo.</span><span class="sxs-lookup"><span data-stu-id="489d5-253">Find hello **IPAll** node.</span></span>  <span data-ttu-id="489d5-254">Hola **el puerto TCP** , escriba **1433**.</span><span class="sxs-lookup"><span data-stu-id="489d5-254">In hello **TCP Port** field, enter **1433**.</span></span>

          ![Configure SQL Express for TCP/IP][3]
   7. <span data-ttu-id="489d5-255">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-255">Click **OK**.</span></span>  <span data-ttu-id="489d5-256">Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-256">Click **OK** in hello pop-up dialog.</span></span>
   8. <span data-ttu-id="489d5-257">Haga clic en **Services de SQL Server** en el menú de árbol de la izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-257">Click **SQL Server Services** in hello left-hand tree menu.</span></span>
   9. <span data-ttu-id="489d5-258">Haga clic con el botón derecho en **SQL Server (SQLEXPRESS)** y seleccione **Reiniciar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-258">Right-click **SQL Server (SQLEXPRESS)** and select **Restart**</span></span>
   10. <span data-ttu-id="489d5-259">Hola cerrar el Administrador de configuración de SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="489d5-259">Close hello SQL Server 2014 Configuration Manager.</span></span>
3. <span data-ttu-id="489d5-260">Ejecute hello SQL Server 2014 Management Studio y conéctese tooyour instancia de SQL Express local</span><span class="sxs-lookup"><span data-stu-id="489d5-260">Run hello SQL Server 2014 Management Studio and connect tooyour local SQL Express instance</span></span>

   1. <span data-ttu-id="489d5-261">Haga clic en la instancia en el Explorador de objetos de Hola y seleccione **propiedades**</span><span class="sxs-lookup"><span data-stu-id="489d5-261">Right-click your instance in hello Object Explorer and select **Properties**</span></span>
   2. <span data-ttu-id="489d5-262">Seleccione hello **seguridad** página.</span><span class="sxs-lookup"><span data-stu-id="489d5-262">Select hello **Security** page.</span></span>
   3. <span data-ttu-id="489d5-263">Asegúrese de hello **modo autenticación de Windows y SQL Server** está seleccionada</span><span class="sxs-lookup"><span data-stu-id="489d5-263">Ensure hello **SQL Server and Windows Authentication mode** is selected</span></span>
   4. <span data-ttu-id="489d5-264">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="489d5-264">Click **OK**</span></span>

          ![Configure SQL Express Authentication][4]
   5. <span data-ttu-id="489d5-265">Expanda **seguridad** > **inicios de sesión** Hola Explorador de objetos</span><span class="sxs-lookup"><span data-stu-id="489d5-265">Expand **Security** > **Logins** in hello Object Explorer</span></span>
   6. <span data-ttu-id="489d5-266">Haga clic con el botón derecho en **Inicios de sesión** y seleccione **Nuevo inicio de sesión...**</span><span class="sxs-lookup"><span data-stu-id="489d5-266">Right-click **Logins** and select **New Login...**</span></span>
   7. <span data-ttu-id="489d5-267">Escriba un nombre de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="489d5-267">Enter a Login name.</span></span>  <span data-ttu-id="489d5-268">Seleccione **Autenticación de SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="489d5-268">Select **SQL Server authentication**.</span></span>  <span data-ttu-id="489d5-269">Escriba una contraseña, a continuación, escriba Hola misma contraseña en **Confirmar contraseña**.</span><span class="sxs-lookup"><span data-stu-id="489d5-269">Enter a Password, then enter hello same password in **Confirm password**.</span></span>  <span data-ttu-id="489d5-270">contraseña de Hello debe cumplir los requisitos de complejidad de Windows.</span><span class="sxs-lookup"><span data-stu-id="489d5-270">hello password must meet Windows complexity requirements.</span></span>
   8. <span data-ttu-id="489d5-271">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="489d5-271">Click **OK**</span></span>

          ![Add a new user tooSQL Express][5]
   9. <span data-ttu-id="489d5-272">Haga clic con el botón derecho en el nuevo inicio de sesión y seleccione **Propiedades**</span><span class="sxs-lookup"><span data-stu-id="489d5-272">Right-click your new login and select **Properties**</span></span>
   10. <span data-ttu-id="489d5-273">Seleccione hello **Roles de servidor** página</span><span class="sxs-lookup"><span data-stu-id="489d5-273">Select hello **Server Roles** page</span></span>
   11. <span data-ttu-id="489d5-274">Comprobar Hola cuadro siguiente toohello **dbcreator** rol de servidor</span><span class="sxs-lookup"><span data-stu-id="489d5-274">Check hello box next toohello **dbcreator** server role</span></span>
   12. <span data-ttu-id="489d5-275">Haga clic en **Aceptar**</span><span class="sxs-lookup"><span data-stu-id="489d5-275">Click **OK**</span></span>
   13. <span data-ttu-id="489d5-276">Cerrar Hola 2015 de SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="489d5-276">Close hello SQL Server 2015 Management Studio</span></span>

<span data-ttu-id="489d5-277">Asegurarse de que el nombre de usuario de registro hello y contraseña que has seleccionado.</span><span class="sxs-lookup"><span data-stu-id="489d5-277">Ensure you record hello username and password you selected.</span></span>  <span data-ttu-id="489d5-278">Puede que tenga permisos o roles de servidor adicionales tooassign dependiendo de los requisitos de base de datos específica.</span><span class="sxs-lookup"><span data-stu-id="489d5-278">You may need tooassign additional server roles or permissions depending on your specific database requirements.</span></span>

<span data-ttu-id="489d5-279">Hola aplicación Node.js lee hello **SQLCONNSTR_MS_TableConnectionString** variable de entorno para la cadena de conexión de Hola para esta base de datos.</span><span class="sxs-lookup"><span data-stu-id="489d5-279">hello Node.js application reads hello **SQLCONNSTR_MS_TableConnectionString** environment variable for hello connection string for this database.</span></span>  <span data-ttu-id="489d5-280">Se puede establecer en el entorno.</span><span class="sxs-lookup"><span data-stu-id="489d5-280">You can set this variable within your environment.</span></span>  <span data-ttu-id="489d5-281">Por ejemplo, puede usar esta variable de entorno tooset de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="489d5-281">For example, you can use PowerShell tooset this environment variable:</span></span>

    $env:SQLCONNSTR_MS_TableConnectionString = "Server=127.0.0.1; Database=mytestdatabase; User Id=azuremobile; Password=T3stPa55word;"

<span data-ttu-id="489d5-282">Hola de acceso a la base de datos a través de una conexión TCP/IP y proporcionar un nombre de usuario y una contraseña para la conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-282">Access hello database through a TCP/IP connection and provide a username and password for hello connection.</span></span>

### <span data-ttu-id="489d5-283"><a name="howto-config-localdev"></a>Configuración del proyecto para el desarrollo local</span><span class="sxs-lookup"><span data-stu-id="489d5-283"><a name="howto-config-localdev"></a>How to: Configure your project for local development</span></span>
<span data-ttu-id="489d5-284">Aplicaciones móviles de Azure lee un archivo JavaScript denominado *azureMobile.js* de sistema de archivos local Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-284">Azure Mobile Apps reads a JavaScript file called *azureMobile.js* from hello local filesystem.</span></span>  <span data-ttu-id="489d5-285">No usar este hello de tooconfigure archivo SDK de aplicaciones móviles de Azure en producción: usar la configuración de aplicación dentro de hello [portal de Azure] en su lugar.</span><span class="sxs-lookup"><span data-stu-id="489d5-285">Do not use this file tooconfigure hello Azure Mobile Apps SDK in production - use App Settings within hello [Azure portal] instead.</span></span>  <span data-ttu-id="489d5-286">Hola *azureMobile.js* archivo debe exportar un objeto de configuración.</span><span class="sxs-lookup"><span data-stu-id="489d5-286">hello *azureMobile.js* file should export a configuration object.</span></span>  <span data-ttu-id="489d5-287">valores de Hello más comunes son:</span><span class="sxs-lookup"><span data-stu-id="489d5-287">hello most common settings are:</span></span>

* <span data-ttu-id="489d5-288">Database Settings</span><span class="sxs-lookup"><span data-stu-id="489d5-288">Database Settings</span></span>
* <span data-ttu-id="489d5-289">Configuración del registro de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="489d5-289">Diagnostic Logging Settings</span></span>
* <span data-ttu-id="489d5-290">Configuración de CORS alternativa</span><span class="sxs-lookup"><span data-stu-id="489d5-290">Alternate CORS Settings</span></span>

<span data-ttu-id="489d5-291">Un ejemplo *azureMobile.js* archivo implementa Hola anterior sigue de configuración de base de datos:</span><span class="sxs-lookup"><span data-stu-id="489d5-291">An example *azureMobile.js* file implementing hello preceding database settings follows:</span></span>

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

<span data-ttu-id="489d5-292">Se recomienda que agregue *azureMobile.js* tooyour *.gitignore* archivo (o en otro control de código fuente Omitir archivo) tooprevent contraseñas se almacenen en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-292">We recommend that you add *azureMobile.js* tooyour *.gitignore* file (or other source code control ignore file) tooprevent passwords from being stored in hello cloud.</span></span>  <span data-ttu-id="489d5-293">Configure siempre la configuración de producción en la configuración de la aplicación dentro de hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-293">Always configure production settings in App Settings within hello [Azure portal].</span></span>

### <span data-ttu-id="489d5-294"><a name="howto-appsettings"></a>Configuración de aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="489d5-294"><a name="howto-appsettings"></a>How: Configure App Settings for your Mobile App</span></span>
<span data-ttu-id="489d5-295">Mayoría de las configuraciones de hello *azureMobile.js* archivo tiene una configuración de aplicación equivalente en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-295">Most settings in hello *azureMobile.js* file have an equivalent App Setting in hello [Azure portal].</span></span>  <span data-ttu-id="489d5-296">Usar hello sigue lista tooconfigure la aplicación en la configuración de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="489d5-296">Use hello following list tooconfigure your app in App Settings:</span></span>

| <span data-ttu-id="489d5-297">Configuración de aplicación</span><span class="sxs-lookup"><span data-stu-id="489d5-297">App Setting</span></span> | <span data-ttu-id="489d5-298">*azureMobile.js*</span><span class="sxs-lookup"><span data-stu-id="489d5-298">*azureMobile.js* Setting</span></span> | <span data-ttu-id="489d5-299">Descripción</span><span class="sxs-lookup"><span data-stu-id="489d5-299">Description</span></span> | <span data-ttu-id="489d5-300">Valores válidos</span><span class="sxs-lookup"><span data-stu-id="489d5-300">Valid Values</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="489d5-301">**MS_MobileAppName**</span><span class="sxs-lookup"><span data-stu-id="489d5-301">**MS_MobileAppName**</span></span> |<span data-ttu-id="489d5-302">name</span><span class="sxs-lookup"><span data-stu-id="489d5-302">name</span></span> |<span data-ttu-id="489d5-303">nombre de Hola de aplicación hello</span><span class="sxs-lookup"><span data-stu-id="489d5-303">hello name of hello app</span></span> |<span data-ttu-id="489d5-304">cadena</span><span class="sxs-lookup"><span data-stu-id="489d5-304">string</span></span> |
| <span data-ttu-id="489d5-305">**MS_MobileLoggingLevel**</span><span class="sxs-lookup"><span data-stu-id="489d5-305">**MS_MobileLoggingLevel**</span></span> |<span data-ttu-id="489d5-306">logging.level</span><span class="sxs-lookup"><span data-stu-id="489d5-306">logging.level</span></span> |<span data-ttu-id="489d5-307">Nivel de registro mínimo de mensajes toolog</span><span class="sxs-lookup"><span data-stu-id="489d5-307">Minimum log level of messages toolog</span></span> |<span data-ttu-id="489d5-308">error, advertencia, información, detallado, depuración, absurdo</span><span class="sxs-lookup"><span data-stu-id="489d5-308">error, warning, info, verbose, debug, silly</span></span> |
| <span data-ttu-id="489d5-309">**MS_DebugMode**</span><span class="sxs-lookup"><span data-stu-id="489d5-309">**MS_DebugMode**</span></span> |<span data-ttu-id="489d5-310">debug</span><span class="sxs-lookup"><span data-stu-id="489d5-310">debug</span></span> |<span data-ttu-id="489d5-311">Habilitar o deshabilitar el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="489d5-311">Enable or Disable debug mode</span></span> |<span data-ttu-id="489d5-312">true, false</span><span class="sxs-lookup"><span data-stu-id="489d5-312">true, false</span></span> |
| <span data-ttu-id="489d5-313">**MS_TableSchema**</span><span class="sxs-lookup"><span data-stu-id="489d5-313">**MS_TableSchema**</span></span> |<span data-ttu-id="489d5-314">data.schema</span><span class="sxs-lookup"><span data-stu-id="489d5-314">data.schema</span></span> |<span data-ttu-id="489d5-315">Nombre del esquema predeterminado para tablas SQL</span><span class="sxs-lookup"><span data-stu-id="489d5-315">Default schema name for SQL tables</span></span> |<span data-ttu-id="489d5-316">cadena (valor predeterminado: dbo)</span><span class="sxs-lookup"><span data-stu-id="489d5-316">string (default: dbo)</span></span> |
| <span data-ttu-id="489d5-317">**MS_DynamicSchema**</span><span class="sxs-lookup"><span data-stu-id="489d5-317">**MS_DynamicSchema**</span></span> |<span data-ttu-id="489d5-318">data.dynamicSchema</span><span class="sxs-lookup"><span data-stu-id="489d5-318">data.dynamicSchema</span></span> |<span data-ttu-id="489d5-319">Habilitar o deshabilitar el modo de depuración</span><span class="sxs-lookup"><span data-stu-id="489d5-319">Enable or Disable debug mode</span></span> |<span data-ttu-id="489d5-320">true, false</span><span class="sxs-lookup"><span data-stu-id="489d5-320">true, false</span></span> |
| <span data-ttu-id="489d5-321">**MS_DisableVersionHeader**</span><span class="sxs-lookup"><span data-stu-id="489d5-321">**MS_DisableVersionHeader**</span></span> |<span data-ttu-id="489d5-322">versión (conjunto tooundefined)</span><span class="sxs-lookup"><span data-stu-id="489d5-322">version (set tooundefined)</span></span> |<span data-ttu-id="489d5-323">Deshabilita el encabezado X-ZUMO-Server-Version Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-323">Disables hello X-ZUMO-Server-Version header</span></span> |<span data-ttu-id="489d5-324">true, false</span><span class="sxs-lookup"><span data-stu-id="489d5-324">true, false</span></span> |
| <span data-ttu-id="489d5-325">**MS_SkipVersionCheck**</span><span class="sxs-lookup"><span data-stu-id="489d5-325">**MS_SkipVersionCheck**</span></span> |<span data-ttu-id="489d5-326">skipversioncheck</span><span class="sxs-lookup"><span data-stu-id="489d5-326">skipversioncheck</span></span> |<span data-ttu-id="489d5-327">Deshabilita la comprobación de la versión de Hola API de cliente</span><span class="sxs-lookup"><span data-stu-id="489d5-327">Disables hello client API version check</span></span> |<span data-ttu-id="489d5-328">true, false</span><span class="sxs-lookup"><span data-stu-id="489d5-328">true, false</span></span> |

<span data-ttu-id="489d5-329">tooset una configuración de aplicación:</span><span class="sxs-lookup"><span data-stu-id="489d5-329">tooset an App Setting:</span></span>

1. <span data-ttu-id="489d5-330">Inicie sesión en toohello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-330">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="489d5-331">Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de saludo de la aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="489d5-331">Select **All resources** or **App Services** then click hello name of your Mobile App.</span></span>
3. <span data-ttu-id="489d5-332">hoja de configuración de Hola se abre de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="489d5-332">hello Settings blade opens by default.</span></span> <span data-ttu-id="489d5-333">En caso contrario, haga clic en **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="489d5-333">If it doesn't, click **Settings**.</span></span>
4. <span data-ttu-id="489d5-334">Haga clic en **configuración de la aplicación** menú GENERAL Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-334">Click **Application settings** in hello GENERAL menu.</span></span>
5. <span data-ttu-id="489d5-335">Desplácese toohello sección de configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="489d5-335">Scroll toohello App Settings section.</span></span>
6. <span data-ttu-id="489d5-336">Si la aplicación si se establece ya existe, haga clic en valor de Hola de hello aplicación tooedit Hola valor.</span><span class="sxs-lookup"><span data-stu-id="489d5-336">If your app setting already exists, click hello value of hello app setting tooedit hello value.</span></span>
7. <span data-ttu-id="489d5-337">Si la configuración de la aplicación no existe, escriba Hola configuración de la aplicación en el cuadro clave de Hola y el valor de hello en el cuadro del valor de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-337">If your app setting does not exist, enter hello App Setting in hello Key box and hello value in hello Value box.</span></span>
8. <span data-ttu-id="489d5-338">Cuando termine, haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-338">Once you are complete, click **Save**.</span></span>

<span data-ttu-id="489d5-339">Si cambia la mayoría de las opciones de configuración de la aplicación habrá que reiniciar el servicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-339">Changing most app settings requires a service restart.</span></span>

### <span data-ttu-id="489d5-340"><a name="howto-use-sqlazure"></a>Uso de Base de datos SQL como almacén de datos de producción</span><span class="sxs-lookup"><span data-stu-id="489d5-340"><a name="howto-use-sqlazure"></a>How to: Use SQL Database as your production data store</span></span>
<!--- ALTERNATE INCLUDE - we can't use ../includes/app-service-mobile-dotnet-backend-create-new-service.md - slightly different semantics -->

<span data-ttu-id="489d5-341">El uso de Base de datos SQL de Azure como almacén de datos es idéntico en todos los tipos de aplicaciones del Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d5-341">Using Azure SQL Database as a data store is identical across all Azure App Service application types.</span></span> <span data-ttu-id="489d5-342">Si aún no lo ha hecho, siga estas toocreate pasos un aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="489d5-342">If you have not done so already, follow these steps toocreate a Mobile App backend.</span></span>

1. <span data-ttu-id="489d5-343">Inicie sesión en toohello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-343">Log in toohello [Azure portal].</span></span>
2. <span data-ttu-id="489d5-344">Hello parte superior izquierda de la ventana hello en, haga clic en hello **+ nuevo** botón > **Web y móvil** > **aplicación móvil**, a continuación, proporcione un nombre para su aplicación móvil de back-end.</span><span class="sxs-lookup"><span data-stu-id="489d5-344">In hello top left of hello window, click hello **+NEW** button > **Web + Mobile** > **Mobile App**, then provide a name for your Mobile App backend.</span></span>
3. <span data-ttu-id="489d5-345">Hola **grupo de recursos** cuadro, escriba Hola mismo nombre que su aplicación.</span><span class="sxs-lookup"><span data-stu-id="489d5-345">In hello **Resource Group** box, enter hello same name as your app.</span></span>
4. <span data-ttu-id="489d5-346">plan de servicio de aplicaciones predeterminado de Hello está seleccionado.</span><span class="sxs-lookup"><span data-stu-id="489d5-346">hello Default App Service plan is selected.</span></span>  <span data-ttu-id="489d5-347">Si desea que toochange su plan de servicio de aplicaciones, puede hacerlo haciendo clic en el Plan de servicio de aplicación Hola > **+ crear nuevos**.</span><span class="sxs-lookup"><span data-stu-id="489d5-347">If you wish toochange your App Service plan, you can do so by clicking hello App Service Plan > **+ Create New**.</span></span>  <span data-ttu-id="489d5-348">Proporcione un nombre del nuevo plan de servicio de aplicaciones de Hola y seleccione una ubicación adecuada.</span><span class="sxs-lookup"><span data-stu-id="489d5-348">Provide a name of hello new App Service plan and select an appropriate location.</span></span>  <span data-ttu-id="489d5-349">Haga clic en el nivel de precios de Hola y seleccione un nivel de precios adecuado para el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-349">Click hello Pricing tier and select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="489d5-350">Seleccione **todas las ver** tooview más precios opciones, como **libre** y **Shared**.</span><span class="sxs-lookup"><span data-stu-id="489d5-350">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span>  <span data-ttu-id="489d5-351">Una vez haya seleccionado el nivel de precios, haga clic en hello **seleccione** botón.</span><span class="sxs-lookup"><span data-stu-id="489d5-351">Once you have selected the pricing tier, click hello **Select** button.</span></span>  <span data-ttu-id="489d5-352">Nuevo en hello **plan de servicio de aplicaciones** hoja, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-352">Back in hello **App Service plan** blade, click **OK**.</span></span>
5. <span data-ttu-id="489d5-353">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="489d5-353">Click **Create**.</span></span> <span data-ttu-id="489d5-354">El aprovisionamiento de un back-end de la aplicación móvil puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="489d5-354">Provisioning a Mobile App backend can take a couple of minutes.</span></span>  <span data-ttu-id="489d5-355">Cuando se aprovisiona la aplicación móvil de hello back-end, el portal de hello abre hello **configuración** hoja para aplicación móvil de hello back-end.</span><span class="sxs-lookup"><span data-stu-id="489d5-355">Once hello Mobile App backend is provisioned, hello portal opens hello **Settings** blade for hello Mobile App backend.</span></span>

<span data-ttu-id="489d5-356">Una vez creado el back-end de hello aplicación móvil, puede elegir tooeither conectarse un backend de la aplicación móvil de tooyour de base de datos SQL existente o crear una nueva base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="489d5-356">Once hello Mobile App backend is created, you can choose tooeither connect an existing SQL database tooyour Mobile App backend or create a new SQL database.</span></span>  <span data-ttu-id="489d5-357">En esta sección, crearemos una nueva base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="489d5-357">In this section, we create a SQL database.</span></span>

> [!NOTE]
> <span data-ttu-id="489d5-358">Si ya tiene una base de datos en hello misma ubicación que el back-end de hello aplicación móvil, puede elegir en su lugar **usar una base de datos** y, a continuación, seleccione esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="489d5-358">If you already have a database in hello same location as hello mobile app backend, you can instead choose **Use an existing database** and then select that database.</span></span> <span data-ttu-id="489d5-359">no se recomienda el uso de Hola de una base de datos en una ubicación diferente debido a latencias más altas.</span><span class="sxs-lookup"><span data-stu-id="489d5-359">hello use of a database in a different location is not recommended because of higher latencies.</span></span>
>
>

1. <span data-ttu-id="489d5-360">En hello nueva aplicación móvil back-end, haga clic en **configuración** > **aplicación móvil** > **datos** > **+ agregar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-360">In hello new Mobile App backend, click **Settings** > **Mobile App** > **Data** > **+Add**.</span></span>
2. <span data-ttu-id="489d5-361">Hola **Agregar conexión de datos** hoja, haga clic en **base de datos de SQL - configurar los valores obligatorios** > **crear una nueva base de datos**.</span><span class="sxs-lookup"><span data-stu-id="489d5-361">In hello **Add data connection** blade, click **SQL Database - Configure required settings** > **Create a new database**.</span></span>  <span data-ttu-id="489d5-362">Escriba el nombre de Hola de base de datos nueva Hola Hola **nombre** campo.</span><span class="sxs-lookup"><span data-stu-id="489d5-362">Enter hello name of hello new database in hello **Name** field.</span></span>
3. <span data-ttu-id="489d5-363">Haga clic en **Servidor**.</span><span class="sxs-lookup"><span data-stu-id="489d5-363">Click **Server**.</span></span>  <span data-ttu-id="489d5-364">Hola **nuevo servidor** hoja, escriba un nombre de servidor único en hello **nombre del servidor** campo y proporcionar un adecuado **inicio de sesión de administrador de servidor** y **contraseña**.</span><span class="sxs-lookup"><span data-stu-id="489d5-364">In hello **New server** blade, enter a unique server name in hello **Server name** field, and provide a suitable **Server admin login** and **Password**.</span></span>  <span data-ttu-id="489d5-365">Asegúrese de **server tooaccess de permitir que los servicios de azure** está activada.</span><span class="sxs-lookup"><span data-stu-id="489d5-365">Ensure **Allow azure services tooaccess server** is checked.</span></span>  <span data-ttu-id="489d5-366">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-366">Click **OK**.</span></span>

    ![Creación de una Base de datos SQL de Azure][6]
4. <span data-ttu-id="489d5-368">En hello **nueva base de datos** hoja, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-368">On hello **New database** blade, click **OK**.</span></span>
5. <span data-ttu-id="489d5-369">En hello **Agregar conexión de datos** hoja, seleccione **cadena de conexión**, escriba el inicio de sesión de Hola y la contraseña que proporcionó al crear la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-369">Back on hello **Add data connection** blade, select **Connection string**, enter hello login and password that you provided when creating hello database.</span></span>  <span data-ttu-id="489d5-370">Si utiliza una base de datos existente, proporcione las credenciales de inicio de sesión de Hola para esa base de datos.</span><span class="sxs-lookup"><span data-stu-id="489d5-370">If you use an existing database, provide hello login credentials for that database.</span></span>  <span data-ttu-id="489d5-371">Cuando las especifique, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="489d5-371">Once entered, click **OK**.</span></span>
6. <span data-ttu-id="489d5-372">En hello **Agregar conexión de datos** de nuevo, haga clic en la hoja **Aceptar** base de datos de toocreate Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-372">Back on hello **Add data connection** blade again, click **OK** toocreate hello database.</span></span>

<!--- END OF ALTERNATE INCLUDE -->

<span data-ttu-id="489d5-373">Creación de base de datos de hello puede tardar unos minutos.</span><span class="sxs-lookup"><span data-stu-id="489d5-373">Creation of hello database can take a few minutes.</span></span>  <span data-ttu-id="489d5-374">Hola de uso **notificaciones** progreso de hello toomonitor de área de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-374">Use hello **Notifications** area toomonitor hello progress of hello deployment.</span></span>  <span data-ttu-id="489d5-375">No se avanza hasta que la base de datos de Hola se ha implementado correctamente.</span><span class="sxs-lookup"><span data-stu-id="489d5-375">Do not progress until hello database has been deployed successfully.</span></span>  <span data-ttu-id="489d5-376">Una vez implementado correctamente, se crea una cadena de conexión para la instancia de base de datos SQL de hello en la configuración de la aplicación de back-end móvil.</span><span class="sxs-lookup"><span data-stu-id="489d5-376">Once successfully deployed, a Connection String is created for hello SQL Database instance in your Mobile backend App Settings.</span></span>  <span data-ttu-id="489d5-377">Puede ver esta configuración de aplicación Hola **configuración** > **configuración de la aplicación** > **las cadenas de conexión**.</span><span class="sxs-lookup"><span data-stu-id="489d5-377">You can see this app setting in hello **Settings** > **Application settings** > **Connection strings**.</span></span>

### <span data-ttu-id="489d5-378"><a name="howto-tables-auth"></a>Cómo: requerir la autenticación para acceso tootables</span><span class="sxs-lookup"><span data-stu-id="489d5-378"><a name="howto-tables-auth"></a>How to: Require authentication for access tootables</span></span>
<span data-ttu-id="489d5-379">Si desea toouse autenticación del servicio de aplicación con el punto de conexión de hello tablas, debe configurar autenticación de servicio de aplicación Hola [portal de Azure] primero.</span><span class="sxs-lookup"><span data-stu-id="489d5-379">If you wish toouse App Service Authentication with hello tables endpoint, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="489d5-380">Para obtener más información acerca de cómo configurar la autenticación en un servicio de aplicaciones de Azure, revise hello Guía de configuración para el proveedor de identidades de hello piensa toouse:</span><span class="sxs-lookup"><span data-stu-id="489d5-380">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="489d5-381">[¿Cómo tooconfigure autenticación de Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="489d5-381">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="489d5-382">[¿Cómo tooconfigure autenticación de Facebook]</span><span class="sxs-lookup"><span data-stu-id="489d5-382">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="489d5-383">[¿Cómo tooconfigure autenticación de Google]</span><span class="sxs-lookup"><span data-stu-id="489d5-383">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="489d5-384">[¿Cómo tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="489d5-384">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="489d5-385">[¿Cómo tooconfigure autenticación de Twitter]</span><span class="sxs-lookup"><span data-stu-id="489d5-385">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="489d5-386">Cada tabla tiene una propiedad de access que puede ser usado toocontrol acceso toohello tabla.</span><span class="sxs-lookup"><span data-stu-id="489d5-386">Each table has an access property that can be used toocontrol access toohello table.</span></span>  <span data-ttu-id="489d5-387">Hola siguiente ejemplo muestra una tabla definida de forma estática con requiere autenticación.</span><span class="sxs-lookup"><span data-stu-id="489d5-387">hello following sample shows a statically defined table with authentication required.</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="489d5-388">propiedad de acceso de Hello puede tomar uno de estos tres valores</span><span class="sxs-lookup"><span data-stu-id="489d5-388">hello access property can take one of three values</span></span>

* <span data-ttu-id="489d5-389">*anónimo* indica que aplicación de cliente hello tooread datos sin autenticación</span><span class="sxs-lookup"><span data-stu-id="489d5-389">*anonymous* indicates that hello client application is allowed tooread data without authentication</span></span>
* <span data-ttu-id="489d5-390">*autenticado* indica que la aplicación de cliente de hello debe enviar un token de autenticación válido con la solicitud de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-390">*authenticated* indicates that hello client application must send a valid authentication token with hello request</span></span>
* <span data-ttu-id="489d5-391">*disabled* indica que esta tabla está deshabilitada actualmente</span><span class="sxs-lookup"><span data-stu-id="489d5-391">*disabled* indicates that this table is currently disabled</span></span>

<span data-ttu-id="489d5-392">Si la propiedad de acceso de hello no está definido, se permite el acceso no autenticado.</span><span class="sxs-lookup"><span data-stu-id="489d5-392">If hello access property is undefined, unauthenticated access is allowed.</span></span>

### <span data-ttu-id="489d5-393"><a name="howto-tables-getidentity"></a>Uso de notificaciones de autenticación con las tablas</span><span class="sxs-lookup"><span data-stu-id="489d5-393"><a name="howto-tables-getidentity"></a>How to: Use authentication claims with your tables</span></span>
<span data-ttu-id="489d5-394">Puede configurar varias notificaciones que se solicitan cuando se configura la autenticación.</span><span class="sxs-lookup"><span data-stu-id="489d5-394">You can set up various claims that are requested when authentication is set up.</span></span>  <span data-ttu-id="489d5-395">Estas notificaciones normalmente no están disponibles a través de hello `context.user` objeto.</span><span class="sxs-lookup"><span data-stu-id="489d5-395">These claims are not normally available through hello `context.user` object.</span></span>  <span data-ttu-id="489d5-396">Sin embargo, se pueden recuperar mediante hello `context.user.getIdentity()` método.</span><span class="sxs-lookup"><span data-stu-id="489d5-396">However, they can be retrieved using hello `context.user.getIdentity()` method.</span></span>  <span data-ttu-id="489d5-397">Hola `getIdentity()` método devuelve una promesa que se resuelve el objeto tooan.</span><span class="sxs-lookup"><span data-stu-id="489d5-397">hello `getIdentity()` method returns a Promise that resolves tooan object.</span></span>  <span data-ttu-id="489d5-398">objeto de Hello es ordenado por el método de autenticación (facebook, google, twitter, cuenta de Microsoft o aad).</span><span class="sxs-lookup"><span data-stu-id="489d5-398">hello object is keyed by the authentication method (facebook, google, twitter, microsoftaccount, or aad).</span></span>

<span data-ttu-id="489d5-399">Por ejemplo, si establece la autenticación de Microsoft Account y notificación de direcciones de correo electrónico de solicitud hello, puede agregar registro de toohello de dirección de correo electrónico de hello con hello siguiente controlador de tabla:</span><span class="sxs-lookup"><span data-stu-id="489d5-399">For example, if you set up Microsoft Account authentication and request hello email addresses claim, you can add hello email address toohello record with hello following table controller:</span></span>

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
    * Limit hello context query toothose records with hello authenticated user email address
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function queryContextForEmail(context) {
        return context.user.getIdentity().then((data) => {
            context.query.where({ emailAddress: data.microsoftaccount.claims.emailaddress });
            return context.execute();
        });
    }

    /**
    * Adds hello email address from hello claims toohello context item - used for
    * insert operations
    * @param {Context} context hello operation context
    * @returns {Promise} context execution Promise
    */
    function addEmailToContext(context) {
        return context.user.getIdentity().then((data) => {
            context.item.emailAddress = data.microsoftaccount.claims.emailaddress;
            return context.execute();
        });
    }

    // Configure specific code when hello client does a request
    // READ - only return records belonging toohello authenticated user
    table.read(queryContextForEmail);

    // CREATE - add or overwrite hello userId based on hello authenticated user
    table.insert(addEmailToContext);

    // UPDATE - only allow updating of record belong toohello authenticated user
    table.update(queryContextForEmail);

    // DELETE - only allow deletion of records belong toohello authenticated uer
    table.delete(queryContextForEmail);

    module.exports = table;

<span data-ttu-id="489d5-400">toosee qué notificaciones están disponibles, use un Hola de tooview de explorador web `/.auth/me` punto de conexión del sitio.</span><span class="sxs-lookup"><span data-stu-id="489d5-400">toosee what claims are available, use a web browser tooview hello `/.auth/me` endpoint of your site.</span></span>

### <span data-ttu-id="489d5-401"><a name="howto-tables-disabled"></a>Cómo: deshabilitar la tabla de toospecific operaciones de acceso</span><span class="sxs-lookup"><span data-stu-id="489d5-401"><a name="howto-tables-disabled"></a>How to: Disable access toospecific table operations</span></span>
<span data-ttu-id="489d5-402">En suma tooappearing en la tabla de hello, propiedad de acceso de hello puede ser usado toocontrol las operaciones individuales.</span><span class="sxs-lookup"><span data-stu-id="489d5-402">In addition tooappearing on hello table, hello access property can be used toocontrol individual operations.</span></span>  <span data-ttu-id="489d5-403">Hay cuatro operaciones:</span><span class="sxs-lookup"><span data-stu-id="489d5-403">There are four operations:</span></span>

* <span data-ttu-id="489d5-404">*leer* es Hola obtener RESTful operación en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-404">*read* is hello RESTful GET operation on hello table</span></span>
* <span data-ttu-id="489d5-405">*Insertar* es Hola POST RESTful operación en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-405">*insert* is hello RESTful POST operation on hello table</span></span>
* <span data-ttu-id="489d5-406">*actualizar* es operación PATCH RESTful de hello en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-406">*update* is hello RESTful PATCH operation on hello table</span></span>
* <span data-ttu-id="489d5-407">*eliminar* es Hola eliminar RESTful operación en la tabla de Hola</span><span class="sxs-lookup"><span data-stu-id="489d5-407">*delete* is hello RESTful DELETE operation on hello table</span></span>

<span data-ttu-id="489d5-408">Por ejemplo, podría desear tooprovide una tabla de solo lectura no autenticada:</span><span class="sxs-lookup"><span data-stu-id="489d5-408">For example, you may wish tooprovide a read-only unauthenticated table:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Read-Only table - only allow READ operations
    table.read.access = 'anonymous';
    table.insert.access = 'disabled';
    table.update.access = 'disabled';
    table.delete.access = 'disabled';

    module.exports = table;

### <span data-ttu-id="489d5-409"><a name="howto-tables-query"></a>Cómo: ajustar Hola consulta que se usa con las operaciones de tabla</span><span class="sxs-lookup"><span data-stu-id="489d5-409"><a name="howto-tables-query"></a>How to: Adjust hello query that is used with table operations</span></span>
<span data-ttu-id="489d5-410">Un requisito común de las operaciones de tabla es una vista restringida de datos de hello tooprovide.</span><span class="sxs-lookup"><span data-stu-id="489d5-410">A common requirement for table operations is tooprovide a restricted view of hello data.</span></span>  <span data-ttu-id="489d5-411">Por ejemplo, puede proporcionar una tabla que tiene una etiqueta con hello autenticado Id. de usuario de forma que sólo puede leer o actualizar sus propios registros.</span><span class="sxs-lookup"><span data-stu-id="489d5-411">For example, you may provide a table that is tagged with hello authenticated user ID such that you can only read or update your own records.</span></span>  <span data-ttu-id="489d5-412">Hola después de la definición de la tabla proporciona la siguiente funcionalidad:</span><span class="sxs-lookup"><span data-stu-id="489d5-412">hello following table definition provides this functionality:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define a static schema for hello table
    table.columns = {
        "userId": "string",
        "text": "string",
        "complete": "boolean"
    };
    table.dynamicSchema = false;

    // Require authentication for this table
    table.access = 'authenticated';

    // Ensure that only records for hello authenticated user are retrieved
    table.read(function (context) {
        context.query.where({ userId: context.user.id });
        return context.execute();
    });

    // When adding records, add or overwrite hello userId with hello authenticated user
    table.insert(function (context) {
        context.item.userId = context.user.id;
        return context.execute();
    });

    module.exports = table;

<span data-ttu-id="489d5-413">Las operaciones que normalmente ejecutan una consulta tendrán una propiedad de consulta que se puede ajustar con una cláusula where.</span><span class="sxs-lookup"><span data-stu-id="489d5-413">Operations that normally execute a query have a query property that you can adjust with a where clause.</span></span> <span data-ttu-id="489d5-414">propiedad de la consulta de Hello es un [QueryJS] objeto que se puede procesar tooconvert usado un toosomething de consulta de OData que Hola datos back-end.</span><span class="sxs-lookup"><span data-stu-id="489d5-414">hello query property is a [QueryJS] object that is used tooconvert an OData query toosomething that hello data backend can process.</span></span>  <span data-ttu-id="489d5-415">Para los casos de igualdad simple (por ejemplo, Hola anteriores), puede utilizarse un mapa.</span><span class="sxs-lookup"><span data-stu-id="489d5-415">For simple equality cases (like hello preceding one), a map can be used.</span></span> <span data-ttu-id="489d5-416">También puede agregar cláusulas SQL específicas:</span><span class="sxs-lookup"><span data-stu-id="489d5-416">You can also add specific SQL clauses:</span></span>

    context.query.where('myfield eq ?', 'value');

### <span data-ttu-id="489d5-417"><a name="howto-tables-softdelete"></a>Configuración de una eliminación temporal en una tabla</span><span class="sxs-lookup"><span data-stu-id="489d5-417"><a name="howto-tables-softdelete"></a>How to: Configure soft delete on a table</span></span>
<span data-ttu-id="489d5-418">La eliminación temporal no elimina realmente los registros.</span><span class="sxs-lookup"><span data-stu-id="489d5-418">Soft Delete does not actually delete records.</span></span>  <span data-ttu-id="489d5-419">En su lugar, marca como eliminados en base de datos de hello estableciendo Hola eliminar columna tootrue.</span><span class="sxs-lookup"><span data-stu-id="489d5-419">Instead it marks them as deleted within hello database by setting hello deleted column tootrue.</span></span>  <span data-ttu-id="489d5-420">Hola SDK de aplicaciones móviles de Azure quita automáticamente los registros eliminados temporalmente de resultados a menos que Hola SDK del cliente móvil use IncludeDeleted().</span><span class="sxs-lookup"><span data-stu-id="489d5-420">hello Azure Mobile Apps SDK automatically removes soft-deleted records from results unless hello Mobile Client SDK uses IncludeDeleted().</span></span>  <span data-ttu-id="489d5-421">tooconfigure eliminar una tabla de software, establezca hello `softDelete` propiedad en el archivo de definición de tabla de hello:</span><span class="sxs-lookup"><span data-stu-id="489d5-421">tooconfigure a table for soft delete, set hello `softDelete` property in hello table definition file:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
    table.columns = {
        "text": "string",
        "complete": "boolean"
    };

    // Turn off dynamic schema
    table.dynamicSchema = false;

    // Turn on Soft Delete
    table.softDelete = true;

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="489d5-422">Debe establecer un mecanismo para depurar registros, ya sea desde una aplicación cliente a través de un trabajo web, una función de Azure o mediante una API personalizada.</span><span class="sxs-lookup"><span data-stu-id="489d5-422">You should establish a mechanism for purging records - either from a client application, via a WebJob, Azure Function or through a custom API.</span></span>

### <span data-ttu-id="489d5-423"><a name="howto-tables-seeding"></a>Inicialización de la base de datos con datos</span><span class="sxs-lookup"><span data-stu-id="489d5-423"><a name="howto-tables-seeding"></a>How to: Seed your database with data</span></span>
<span data-ttu-id="489d5-424">Al crear una nueva aplicación, puede llamar a tooseed una tabla con datos.</span><span class="sxs-lookup"><span data-stu-id="489d5-424">When creating a new application, you may wish tooseed a table with data.</span></span>  <span data-ttu-id="489d5-425">Esto puede hacerse en archivo de JavaScript de definición de tabla de hello como sigue:</span><span class="sxs-lookup"><span data-stu-id="489d5-425">This can be done within hello table definition JavaScript file as follows:</span></span>

    var azureMobileApps = require('azure-mobile-apps');

    var table = azureMobileApps.table();

    // Define hello columns within hello table
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

    // Require authentication tooaccess hello table
    table.access = 'authenticated';

    module.exports = table;

<span data-ttu-id="489d5-426">La propagación de datos solo se realiza cuando se crea la tabla de Hola por hello SDK de aplicaciones móviles de Azure.</span><span class="sxs-lookup"><span data-stu-id="489d5-426">Seeding of data is only done when hello table is created by hello Azure Mobile Apps SDK.</span></span>  <span data-ttu-id="489d5-427">Si la tabla Hola ya existe en la base de datos de hello, no se aplica ningún dato en tabla Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-427">If hello table already exists within hello database, no data is injected into hello table.</span></span>  <span data-ttu-id="489d5-428">Si un esquema dinámico está activado, se deducirá el esquema de datos de hello propagado.</span><span class="sxs-lookup"><span data-stu-id="489d5-428">If dynamic schema is turned on, then the schema is inferred from hello seeded data.</span></span>

<span data-ttu-id="489d5-429">Se recomienda que se llame explícitamente a hello `tables.initialize()` tabla de hello toocreate del método al servicio de hello comienza a ejecutarse.</span><span class="sxs-lookup"><span data-stu-id="489d5-429">We recommend that you explicitly call hello `tables.initialize()` method toocreate hello table when hello service starts running.</span></span>

### <span data-ttu-id="489d5-430"><a name="Swagger"></a>Habilitación de la compatibilidad con Swagger</span><span class="sxs-lookup"><span data-stu-id="489d5-430"><a name="Swagger"></a>How to: Enable Swagger support</span></span>
<span data-ttu-id="489d5-431">Aplicaciones móviles del Servicio de aplicaciones de Azure incorpora compatibilidad con [Swagger] .</span><span class="sxs-lookup"><span data-stu-id="489d5-431">Azure App Service Mobile Apps comes with built-in [Swagger] support.</span></span>  <span data-ttu-id="489d5-432">tooenable Swagger compatibilidad, instale primero Hola de interfaz de usuario swagger como una dependencia:</span><span class="sxs-lookup"><span data-stu-id="489d5-432">tooenable Swagger support, first install hello swagger-ui as a dependency:</span></span>

    npm install --save swagger-ui

<span data-ttu-id="489d5-433">Una vez instalado, puede habilitar la compatibilidad de Swagger en el constructor de hello aplicaciones móviles de Azure:</span><span class="sxs-lookup"><span data-stu-id="489d5-433">Once installed, you can enable Swagger support in hello Azure Mobile Apps constructor:</span></span>

    var mobile = azureMobileApps({ swagger: true });

<span data-ttu-id="489d5-434">Probablemente solo desea tooenable compatibilidad de Swagger en las ediciones de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="489d5-434">You probably only want tooenable Swagger support in development editions.</span></span>  <span data-ttu-id="489d5-435">Puede hacerlo mediante la configuración de aplicación `NODE_ENV` :</span><span class="sxs-lookup"><span data-stu-id="489d5-435">You can do this by utilizing the `NODE_ENV` app setting:</span></span>

    var mobile = azureMobileApps({ swagger: process.env.NODE_ENV !== 'production' });

<span data-ttu-id="489d5-436">Hello extremo de swagger se encuentra en http://*su sitio*.azurewebsites.net/swagger.</span><span class="sxs-lookup"><span data-stu-id="489d5-436">hello swagger endpoint is located at http://*yoursite*.azurewebsites.net/swagger.</span></span>  <span data-ttu-id="489d5-437">Puede tener acceso a hello Swagger de interfaz de usuario a través de hello `/swagger/ui` punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="489d5-437">You can access hello Swagger UI via hello `/swagger/ui` endpoint.</span></span>  <span data-ttu-id="489d5-438">Si elige la autenticación de toorequire en toda la aplicación, Swagger genera un error.</span><span class="sxs-lookup"><span data-stu-id="489d5-438">if you choose toorequire authentication across your entire application, Swagger produces an error.</span></span>  <span data-ttu-id="489d5-439">Para obtener mejores resultados, elija tooallow sin autenticar solicitudes a través de Hola autenticación del servicio de aplicación de Azure / configuración de autorización, a continuación, controlar la autenticación mediante hello `table.access` propiedad.</span><span class="sxs-lookup"><span data-stu-id="489d5-439">For best results, choose tooallow unauthenticated requests through in hello Azure App Service Authentication / Authorization settings, then control authentication using hello `table.access` property.</span></span>

<span data-ttu-id="489d5-440">También puede agregar hello Swagger opción tooyour `azureMobile.js` archivo si solo desea soporte técnico de Swagger al desarrollar de forma local.</span><span class="sxs-lookup"><span data-stu-id="489d5-440">You can also add hello Swagger option tooyour `azureMobile.js` file if you only want Swagger support when developing locally.</span></span>

## <a name="a-namepushpush-notifications"></a><span data-ttu-id="489d5-441"><a name="push">Notificaciones push</span><span class="sxs-lookup"><span data-stu-id="489d5-441"><a name="push">Push notifications</span></span>
<span data-ttu-id="489d5-442">Aplicaciones móviles se integra con centros de notificaciones de Azure tooenable se toosend destinada toomillions de notificaciones de inserción de dispositivos en todas las plataformas principales.</span><span class="sxs-lookup"><span data-stu-id="489d5-442">Mobile Apps integrates with Azure Notification Hubs tooenable you toosend targeted push notifications toomillions of devices across all major platforms.</span></span> <span data-ttu-id="489d5-443">Mediante el uso de los centros de notificaciones, puede enviar inserción tooiOS de notificaciones, dispositivos Android y Windows.</span><span class="sxs-lookup"><span data-stu-id="489d5-443">By using Notification Hubs, you can send push notifications tooiOS, Android and Windows devices.</span></span> <span data-ttu-id="489d5-444">toolearn más información acerca de todo lo que pueden hacer con los centros de notificaciones, consulte [información general de los centros de notificación](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="489d5-444">toolearn more about all that you can do with Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

### <span data-ttu-id="489d5-445"></a><a name="send-push"></a>Envío de notificaciones push</span><span class="sxs-lookup"><span data-stu-id="489d5-445"></a><a name="send-push"></a>How to: Send push notifications</span></span>
<span data-ttu-id="489d5-446">Hola siguiente código muestra cómo toouse Hola inserción objeto toosend una difusión push dispositivos iOS de tooregistered de notificación:</span><span class="sxs-lookup"><span data-stu-id="489d5-446">hello following code shows how toouse hello push object toosend a broadcast push notification tooregistered iOS devices:</span></span>

    // Create an APNS payload.
    var payload = '{"aps": {"alert": "This is an APNS payload."}}';

    // Only do hello push if configured
    if (context.push) {
        // Send a push notification using APNS.
        context.push.apns.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="489d5-447">Mediante la creación de un registro de plantilla de inserción de cliente hello, puede enviar en su lugar un toodevices de mensaje de inserción de plantilla en todas las plataformas admitidas.</span><span class="sxs-lookup"><span data-stu-id="489d5-447">By creating a template push registration from hello client, you can instead send a template push message toodevices on all supported platforms.</span></span> <span data-ttu-id="489d5-448">Hola el siguiente código muestra cómo toosend una notificación de plantilla:</span><span class="sxs-lookup"><span data-stu-id="489d5-448">hello following code shows how toosend a template notification:</span></span>

    // Define hello template payload.
    var payload = '{"messageParam": "This is a template payload."}';

    // Only do hello push if configured
    if (context.push) {
        // Send a template notification.
        context.push.send(null, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }


### <span data-ttu-id="489d5-449"><a name="push-user"></a>Cómo: tooan de notificaciones de inserción de envío autentica usuarios mediante etiquetas</span><span class="sxs-lookup"><span data-stu-id="489d5-449"><a name="push-user"></a>How to: Send push notifications tooan authenticated user using tags</span></span>
<span data-ttu-id="489d5-450">Cuando un usuario autenticado se registra para las notificaciones de inserción, una etiqueta de Id. de usuario se agrega automáticamente el registro de toohello.</span><span class="sxs-lookup"><span data-stu-id="489d5-450">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="489d5-451">Mediante el uso de esta etiqueta, puede enviar inserción dispositivos de tooall notificaciones registrados por un usuario específico.</span><span class="sxs-lookup"><span data-stu-id="489d5-451">By using this tag, you can send push notifications tooall devices registered by a specific user.</span></span> <span data-ttu-id="489d5-452">Hello código siguiente obtiene el SID del usuario que realiza la solicitud de Hola Hola y envía un registro de dispositivos plantilla tooevery de notificación de inserción para que el usuario:</span><span class="sxs-lookup"><span data-stu-id="489d5-452">hello following code gets hello SID of user making hello request and sends a template push notification tooevery device registration for that user:</span></span>

    // Only do hello push if configured
    if (context.push) {
        // Send a notification toohello current user.
        context.push.send(context.user.id, payload, function (error) {
            if (error) {
                // Do something or log hello error.
            }
        });
    }

<span data-ttu-id="489d5-453">Cuando se registre para notificaciones push desde un cliente autenticado, asegúrese de que la autenticación se ha completado antes de intentar el registro.</span><span class="sxs-lookup"><span data-stu-id="489d5-453">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span>

## <span data-ttu-id="489d5-454"><a name="CustomAPI"></a> API personalizadas</span><span class="sxs-lookup"><span data-stu-id="489d5-454"><a name="CustomAPI"></a> Custom APIs</span></span>
### <span data-ttu-id="489d5-455"><a name="howto-customapi-basic"></a>Definición de una API personalizada</span><span class="sxs-lookup"><span data-stu-id="489d5-455"><a name="howto-customapi-basic"></a>How to: Define a custom API</span></span>
<span data-ttu-id="489d5-456">Además toohello de acceso a datos API a través de punto de conexión de hello /tables, aplicaciones móviles de Azure puede proporcionar cobertura de API personalizada.</span><span class="sxs-lookup"><span data-stu-id="489d5-456">In addition toohello data access API via hello /tables endpoint, Azure Mobile Apps can provide custom API coverage.</span></span>  <span data-ttu-id="489d5-457">Las API personalizadas se definen en un definiciones de tabla de toohello de manera similar y puede tener acceso a toda Hola facilidades, incluida la autenticación.</span><span class="sxs-lookup"><span data-stu-id="489d5-457">Custom APIs are defined in a similar way toohello table definitions and can access all hello same facilities, including authentication.</span></span>

<span data-ttu-id="489d5-458">Si desea toouse autenticación de servicio de la aplicación con una API personalizada, debe configurar la autenticación del servicio de aplicación Hola [portal de Azure] primero.</span><span class="sxs-lookup"><span data-stu-id="489d5-458">If you wish toouse App Service Authentication with a Custom API, you must configure App Service Authentication in hello [Azure portal] first.</span></span>  <span data-ttu-id="489d5-459">Para obtener más información acerca de cómo configurar la autenticación en un servicio de aplicaciones de Azure, revise hello Guía de configuración para el proveedor de identidades de hello piensa toouse:</span><span class="sxs-lookup"><span data-stu-id="489d5-459">For more details about configuring authentication in an Azure App Service, review hello Configuration Guide for hello identity provider you intend toouse:</span></span>

* <span data-ttu-id="489d5-460">[¿Cómo tooconfigure autenticación de Azure Active Directory]</span><span class="sxs-lookup"><span data-stu-id="489d5-460">[How tooconfigure Azure Active Directory Authentication]</span></span>
* <span data-ttu-id="489d5-461">[¿Cómo tooconfigure autenticación de Facebook]</span><span class="sxs-lookup"><span data-stu-id="489d5-461">[How tooconfigure Facebook Authentication]</span></span>
* <span data-ttu-id="489d5-462">[¿Cómo tooconfigure autenticación de Google]</span><span class="sxs-lookup"><span data-stu-id="489d5-462">[How tooconfigure Google Authentication]</span></span>
* <span data-ttu-id="489d5-463">[¿Cómo tooconfigure Microsoft Authentication]</span><span class="sxs-lookup"><span data-stu-id="489d5-463">[How tooconfigure Microsoft Authentication]</span></span>
* <span data-ttu-id="489d5-464">[¿Cómo tooconfigure autenticación de Twitter]</span><span class="sxs-lookup"><span data-stu-id="489d5-464">[How tooconfigure Twitter Authentication]</span></span>

<span data-ttu-id="489d5-465">Las API personalizadas se definen en gran parte Hola la misma manera que Hola API de tablas.</span><span class="sxs-lookup"><span data-stu-id="489d5-465">Custom APIs are defined in much hello same way as hello Tables API.</span></span>

1. <span data-ttu-id="489d5-466">Crear un directorio **api** .</span><span class="sxs-lookup"><span data-stu-id="489d5-466">Create an **api** directory</span></span>
2. <span data-ttu-id="489d5-467">Crear un archivo de JavaScript de la definición de API en hello **api** directory.</span><span class="sxs-lookup"><span data-stu-id="489d5-467">Create an API definition JavaScript file in hello **api** directory.</span></span>
3. <span data-ttu-id="489d5-468">Use Hola importación método tooimport Hola **api** directory.</span><span class="sxs-lookup"><span data-stu-id="489d5-468">Use hello import method tooimport hello **api** directory.</span></span>

<span data-ttu-id="489d5-469">Aquí es la definición de la api de prototipo Hola basada en hello basic aplicación ejemplo que hemos usado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="489d5-469">Here is hello prototype api definition based on hello basic-app sample we used earlier.</span></span>

    var express = require('express'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="489d5-470">Veamos un ejemplo de API que devuelven la fecha de servidor de hello con hello *Date.now()* método.</span><span class="sxs-lookup"><span data-stu-id="489d5-470">Let's take an example API that returns hello server date using hello *Date.now()* method.</span></span>  <span data-ttu-id="489d5-471">Este es el archivo de hello api/date.js:</span><span class="sxs-lookup"><span data-stu-id="489d5-471">Here is hello api/date.js file:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };

    module.exports = api;

<span data-ttu-id="489d5-472">Cada parámetro es uno de hello RESTful verbos estándar: GET, POST, PATCH o DELETE.</span><span class="sxs-lookup"><span data-stu-id="489d5-472">Each parameter is one of hello standard RESTful verbs - GET, POST, PATCH, or DELETE.</span></span>  <span data-ttu-id="489d5-473">método Hello es un estándar [ExpressJS Middleware] función que envía el resultado de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="489d5-473">hello method is a standard [ExpressJS Middleware] function that sends hello required output.</span></span>

### <span data-ttu-id="489d5-474"><a name="howto-customapi-auth"></a>Cómo: solicitar autenticación para la API de acceso tooa personalizada</span><span class="sxs-lookup"><span data-stu-id="489d5-474"><a name="howto-customapi-auth"></a>How to: Require authentication for access tooa custom API</span></span>
<span data-ttu-id="489d5-475">SDK de aplicaciones móviles Azure implementa la autenticación en hello igual en el punto de conexión de hello las tablas y las API personalizadas.</span><span class="sxs-lookup"><span data-stu-id="489d5-475">Azure Mobile Apps SDK implements authentication in hello same way for both hello tables endpoint and custom APIs.</span></span>  <span data-ttu-id="489d5-476">Para agregar autenticación toohello API desarrollado en la sección anterior de hello, agregue un **acceso** propiedad:</span><span class="sxs-lookup"><span data-stu-id="489d5-476">To add authentication toohello API developed in hello previous section, add an **access** property:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        });
    };
    // All methods must be authenticated.
    api.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="489d5-477">También puede especificar la autenticación en operaciones específicas:</span><span class="sxs-lookup"><span data-stu-id="489d5-477">You can also specify authentication on specific operations:</span></span>

    var api = {
        get: function (req, res, next) {
            var date = { currentTime: Date.now() };
            res.status(200).type('application/json').send(date);
        }
    };
    // hello GET methods must be authenticated.
    api.get.access = 'authenticated';

    module.exports = api;

<span data-ttu-id="489d5-478">Hello mismo token que se utiliza para el punto de conexión de hello tablas debe utilizarse para las API personalizadas que requiera autenticación.</span><span class="sxs-lookup"><span data-stu-id="489d5-478">hello same token that is used for hello tables endpoint must be used for custom APIs requiring authentication.</span></span>

### <span data-ttu-id="489d5-479"><a name="howto-customapi-auth"></a>Control de cargas de archivos de gran tamaño</span><span class="sxs-lookup"><span data-stu-id="489d5-479"><a name="howto-customapi-auth"></a>How to: Handle large file uploads</span></span>
<span data-ttu-id="489d5-480">SDK de aplicaciones de Azure Mobile usa hello [cuerpo analizador middleware](https://github.com/expressjs/body-parser) tooaccept y descodificar el contenido del cuerpo en el envío.</span><span class="sxs-lookup"><span data-stu-id="489d5-480">Azure Mobile Apps SDK uses hello [body-parser middleware](https://github.com/expressjs/body-parser) tooaccept and decode body content in your submission.</span></span>  <span data-ttu-id="489d5-481">Puede configurar previamente cargas de archivos mayores de cuerpo analizador tooaccept:</span><span class="sxs-lookup"><span data-stu-id="489d5-481">You can pre-configure body-parser tooaccept larger file uploads:</span></span>

    var express = require('express'),
        bodyParser = require('body-parser'),
        azureMobileApps = require('azure-mobile-apps');

    var app = express(),
        mobile = azureMobileApps();

    // Set up large body content handling
    app.use(bodyParser.json({ limit: '50mb' }));
    app.use(bodyParser.urlencoded({ limit: '50mb', extended: true }));

    // Import hello Custom API
    mobile.api.import('./api');

    // Add hello mobile API so it is accessible as a Web API
    app.use(mobile);

    // Start listening on HTTP
    app.listen(process.env.PORT || 3000);

<span data-ttu-id="489d5-482">archivo Hello es codificados antes de la transmisión en base 64.</span><span class="sxs-lookup"><span data-stu-id="489d5-482">hello file is base-64 encoded before transmission.</span></span>  <span data-ttu-id="489d5-483">Esto aumenta el tamaño de Hola de carga real de hello (y Hola, por lo que debe tener en cuenta para el tamaño).</span><span class="sxs-lookup"><span data-stu-id="489d5-483">This increases hello size of hello actual upload (and hence hello size you must account for).</span></span>

### <span data-ttu-id="489d5-484"><a name="howto-customapi-sql"></a>Ejecución de instrucciones SQL personalizadas</span><span class="sxs-lookup"><span data-stu-id="489d5-484"><a name="howto-customapi-sql"></a>How to: Execute custom SQL statements</span></span>
<span data-ttu-id="489d5-485">Hola SDK de aplicaciones móviles de Azure permite acceso toohello todo contexto a través del objeto de solicitud de hello, permitiéndole tooexecute parámetros proveedor de datos definidos de toohello de instrucciones SQL fácilmente:</span><span class="sxs-lookup"><span data-stu-id="489d5-485">hello Azure Mobile Apps SDK allows access toohello entire Context through hello request object, allowing you tooexecute parameterized SQL statements toohello defined data provider easily:</span></span>

    var api = {
        get: function (request, response, next) {
            // Check for parameters - if not there, pass on tooa later API call
            if (typeof request.params.completed === 'undefined')
                return next();

            // Define hello query - anything that can be handled by hello mssql
            // driver is allowed.
            var query = {
                sql: 'UPDATE TodoItem SET complete=@completed',
                parameters: [{
                    completed: request.params.completed
                }]
            };

            // Execute hello query.  hello context for Azure Mobile Apps is available through
            // request.azureMobile - hello data object contains hello configured data provider.
            request.azureMobile.data.execute(query)
            .then(function (results) {
                response.json(results);
            });
        }
    };

    api.get.access = 'authenticated';
    module.exports = api;

## <span data-ttu-id="489d5-486"><a name="Debugging"></a>Depuración, y tablas y API fáciles</span><span class="sxs-lookup"><span data-stu-id="489d5-486"><a name="Debugging"></a>Debugging, Easy Tables, and Easy APIs</span></span>
### <span data-ttu-id="489d5-487"><a name="howto-diagnostic-logs"></a>Depuración, diagnóstico y solución de problemas de Mobile Apps de Azure</span><span class="sxs-lookup"><span data-stu-id="489d5-487"><a name="howto-diagnostic-logs"></a>How to: Debug, diagnose, and troubleshoot Azure Mobile apps</span></span>
<span data-ttu-id="489d5-488">Hola servicio de aplicaciones de Azure proporciona varias depuración y solución de problemas de técnicas para aplicaciones Node.js.</span><span class="sxs-lookup"><span data-stu-id="489d5-488">hello Azure App Service provides several debugging and troubleshooting techniques for Node.js applications.</span></span>
<span data-ttu-id="489d5-489">Consulte toohello después tooget artículos iniciado en el back-end de Node.js Mobile de solución de problemas:</span><span class="sxs-lookup"><span data-stu-id="489d5-489">Refer toohello following articles tooget started in troubleshooting your Node.js Mobile backend:</span></span>

* <span data-ttu-id="489d5-490">[Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="489d5-490">[Monitoring an Azure App Service]</span></span>
* <span data-ttu-id="489d5-491">[Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]</span><span class="sxs-lookup"><span data-stu-id="489d5-491">[Enable Diagnostic Logging in Azure App Service]</span></span>
* <span data-ttu-id="489d5-492">[Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="489d5-492">[Troubleshoot an Azure App Service in Visual Studio]</span></span>

<span data-ttu-id="489d5-493">Las aplicaciones Node.js tienen acceso tooa amplia gama de herramientas de registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="489d5-493">Node.js applications have access tooa wide range of diagnostic log tools.</span></span>  <span data-ttu-id="489d5-494">Internamente, se usa el SDK de Node.js de aplicaciones móviles de Azure hello [Winston] para el registro de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="489d5-494">Internally, hello Azure Mobile Apps Node.js SDK uses [Winston] for diagnostic logging.</span></span>  <span data-ttu-id="489d5-495">El registro se habilita automáticamente al habilitar el modo de depuración o establecer hello **MS_DebugMode** tootrue de configuración de aplicación Hola [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-495">Logging is automatically enabled by enabling debug mode or by setting hello **MS_DebugMode** app setting tootrue in hello [Azure portal].</span></span> <span data-ttu-id="489d5-496">Registros generados aparecen en registros de diagnóstico de hello en hello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="489d5-496">Generated logs appear in hello Diagnostic Logs on hello [Azure portal].</span></span>

### <span data-ttu-id="489d5-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>Cómo: trabajar con tablas fácil Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="489d5-497"><a name="in-portal-editing"></a><a name="work-easy-tables"></a>How to: Work with Easy Tables in hello Azure portal</span></span>
<span data-ttu-id="489d5-498">Tablas fácil en el portal de hello le permiten crear y trabajar con el derecho de tablas en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-498">Easy Tables in hello portal let you create and work with tables right in hello portal.</span></span> <span data-ttu-id="489d5-499">Incluso puede editar las operaciones de tabla mediante Hola Editor de aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-499">You can even edit table operations using hello App Service Editor.</span></span>

<span data-ttu-id="489d5-500">Al hacer clic en **Tablas fáciles** en la configuración del sitio del back-end, puede agregar, modificar o eliminar una tabla.</span><span class="sxs-lookup"><span data-stu-id="489d5-500">When you click **Easy tables** in your backend site settings, you can add, modify, or delete a table.</span></span> <span data-ttu-id="489d5-501">También puede ver datos de tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-501">You can also see data in hello table.</span></span>

![Trabajo con tablas fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-tables.png)

<span data-ttu-id="489d5-503">Hello comandos siguientes están disponibles en la barra de comandos de Hola para una tabla:</span><span class="sxs-lookup"><span data-stu-id="489d5-503">hello following commands are available on hello command bar for a table:</span></span>

* <span data-ttu-id="489d5-504">**Cambiar los permisos** : Hola permiso de lectura de modificación, inserciones, actualizaciones y operaciones delete en la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-504">**Change permissions** - modify hello permission for read, insert, update and delete operations on hello table.</span></span>
  <span data-ttu-id="489d5-505">Las opciones son tooallow el acceso anónimo, autenticación toorequire o toodisable todos los accesos toohello operación.</span><span class="sxs-lookup"><span data-stu-id="489d5-505">Options are tooallow anonymous access, toorequire authentication, or toodisable all access toohello operation.</span></span>
* <span data-ttu-id="489d5-506">**Editar script** -se abre el archivo de script de Hola para la tabla de Hola Hola Editor de aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-506">**Edit script** - hello script file for hello table is opened in hello App Service Editor.</span></span>
* <span data-ttu-id="489d5-507">**Administrar el esquema** : agregar o eliminar columnas o cambiar el índice de la tabla de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-507">**Manage schema** - add or delete columns or change hello table index.</span></span>
* <span data-ttu-id="489d5-508">**Borrar tabla** -trunca una tabla existente se elimina todas las filas de datos, pero deja el esquema de hello sin cambios.</span><span class="sxs-lookup"><span data-stu-id="489d5-508">**Clear table** - truncates an existing table be deleting all data rows but leaving hello schema unchanged.</span></span>
* <span data-ttu-id="489d5-509">**Eliminar filas** : elimina filas individuales de datos.</span><span class="sxs-lookup"><span data-stu-id="489d5-509">**Delete rows** - delete individual rows of data.</span></span>
* <span data-ttu-id="489d5-510">**Ver los registros de streaming** -conecta toohello servicio de registro para el sitio de streaming.</span><span class="sxs-lookup"><span data-stu-id="489d5-510">**View streaming logs** - connects you toohello streaming log service for your site.</span></span>

### <span data-ttu-id="489d5-511"><a name="work-easy-apis"></a>Cómo: trabajar con las API sencilla de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="489d5-511"><a name="work-easy-apis"></a>How to: Work with Easy APIs in hello Azure portal</span></span>
<span data-ttu-id="489d5-512">API sencilla en el portal de hello permiten crear y trabajar con derecho personalizado de las API en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-512">Easy APIs in hello portal let you create and work with custom APIs right in hello portal.</span></span> <span data-ttu-id="489d5-513">Puede editar los scripts de API con hello Editor de aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-513">You can edit API scripts using hello App Service Editor.</span></span>

<span data-ttu-id="489d5-514">Al hacer clic en **API fáciles** en la configuración del sitio del back-end, puede agregar un nuevo punto de conexión de API personalizado, así como modificar o eliminar un punto de conexión de API existente.</span><span class="sxs-lookup"><span data-stu-id="489d5-514">When you click **Easy APIs** in your backend site settings, you can add, modify, or delete a custom API endpoint.</span></span>

![Trabajo con API fáciles](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-easy-apis.png)

<span data-ttu-id="489d5-516">En el portal de hello, puede cambiar los permisos de acceso de Hola para una acción determinada de HTTP, editar el archivo de script de API de hello en el Editor del servicio de aplicación o ver registros de streaming de Hola.</span><span class="sxs-lookup"><span data-stu-id="489d5-516">In hello portal, you can change hello access permissions for a given HTTP action, edit hello API script file in the App Service Editor, or view hello streaming logs.</span></span>

### <span data-ttu-id="489d5-517"><a name="online-editor"></a>Cómo: editar código de hello Editor de aplicación de servicio</span><span class="sxs-lookup"><span data-stu-id="489d5-517"><a name="online-editor"></a>How to: Edit code in hello App Service Editor</span></span>
<span data-ttu-id="489d5-518">Hola portal de Azure le permite modificar los archivos de script de back-end de Node.js en hello Editor de aplicación de servicio sin tener que descargar el equipo local de hello proyecto tooyour.</span><span class="sxs-lookup"><span data-stu-id="489d5-518">hello Azure portal lets you edit your Node.js backend script files in hello App Service Editor without having to download hello project tooyour local computer.</span></span> <span data-ttu-id="489d5-519">archivos de script tooedit en el editor de hello en línea:</span><span class="sxs-lookup"><span data-stu-id="489d5-519">tooedit script files in hello online editor:</span></span>

1. <span data-ttu-id="489d5-520">En la hoja de back-end de la aplicación móvil, haga clic en **Toda la configuración** > **Tablas fáciles** o **API fáciles**, haga clic en una tabla o API y luego en **Editar script**.</span><span class="sxs-lookup"><span data-stu-id="489d5-520">In your Mobile App backend blade, click **All settings** > either **Easy tables** or **Easy APIs**, click a table or API, then click **Edit script**.</span></span> <span data-ttu-id="489d5-521">se abre el archivo de script de Hola en hello Editor de aplicación de servicio.</span><span class="sxs-lookup"><span data-stu-id="489d5-521">hello script file is opened in hello App Service Editor.</span></span>

    ![Editor del Servicio de aplicaciones](./media/app-service-mobile-node-backend-how-to-use-server-sdk/mobile-apps-visual-studio-editor.png)
2. <span data-ttu-id="489d5-523">Hacer que el archivo de código de toohello de cambios en el editor en línea hello.</span><span class="sxs-lookup"><span data-stu-id="489d5-523">Make your changes toohello code file in hello online editor.</span></span> <span data-ttu-id="489d5-524">Los cambios se guardan automáticamente a medida que se escriben.</span><span class="sxs-lookup"><span data-stu-id="489d5-524">Changes are saved automatically as you type.</span></span>

<!-- Images -->
[0]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/npm-init.png
[1]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-new-project.png
[2]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/vs2015-install-npm.png
[3]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-config.png
[4]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-authconfig.png
[5]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/sqlexpress-newuser-1.png
[6]: ./media/app-service-mobile-node-backend-how-to-use-server-sdk/dotnet-backend-create-db.png

<!-- URLs -->
[Inicio rápido de cliente de Android]: app-service-mobile-android-get-started.md
[Inicio rápido de cliente de Apache Cordova]: app-service-mobile-cordova-get-started.md
[Inicio rápido de cliente de iOS]: app-service-mobile-ios-get-started.md
[Inicio rápido de cliente de Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md
[Inicio rápido de cliente de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md
[Inicio rápido de cliente de Xamarin.Forms]: app-service-mobile-xamarin-forms-get-started.md
[Inicio rápido de cliente de Windows]: app-service-mobile-windows-store-dotnet-get-started.md
[HTML/Javascript Client QuickStart]: app-service-html-get-started.md
[sincronización de datos sin conexión]: app-service-mobile-offline-data-sync.md
[¿Cómo tooconfigure autenticación de Azure Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md
[¿Cómo tooconfigure autenticación de Facebook]: app-service-mobile-how-to-configure-facebook-authentication.md
[¿Cómo tooconfigure autenticación de Google]: app-service-mobile-how-to-configure-google-authentication.md
[¿Cómo tooconfigure Microsoft Authentication]: app-service-mobile-how-to-configure-microsoft-authentication.md
[¿Cómo tooconfigure autenticación de Twitter]: app-service-mobile-how-to-configure-twitter-authentication.md
[guía de implementación de Azure App Service]: ../app-service-web/web-sites-deploy.md
[Supervisión de Aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-monitor.md
[Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Solución de problemas del Servicio de aplicaciones de Azure en Visual Studio]: ../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md
[especificar Hola versión del nodo]: ../nodejs-specify-node-version-azure-apps.md
[usar módulos de nodo]: ../nodejs-use-node-modules-azure-apps.md
[Create a new Azure App Service]: ../app-service-web/
[azure-mobile-apps]: https://www.npmjs.com/package/azure-mobile-apps
[Express]: http://expressjs.com/
[Swagger]: http://swagger.io/

[portal de Azure]: https://portal.azure.com/
[OData]: http://www.odata.org
[Promise]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise
[ejemplo basicapp en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/basic-app
[ejemplo de lista de tareas en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/todo
[directorio de ejemplos en GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples
[static-schema sample on GitHub]: https://github.com/azure/azure-mobile-apps-node/tree/master/samples/static-schema
[QueryJS]: https://github.com/Azure/queryjs
[Node.js Tools 1.1 para Visual Studio]: https://github.com/Microsoft/nodejstools/releases/tag/v1.1-RC.2.1
[mssql Node.js paquete]: https://www.npmjs.com/package/mssql
[Microsoft SQL Server 2014 Express]: http://www.microsoft.com/en-us/server-cloud/Products/sql-server-editions/sql-server-express.aspx
[ExpressJS Middleware]: http://expressjs.com/guide/using-middleware.html
[Winston]: https://github.com/winstonjs/winston
