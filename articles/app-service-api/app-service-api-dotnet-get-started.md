---
title: "Introducción a API Apps y ASP.NET en App Service | Microsoft Docs"
description: "Obtenga información acerca de cómo crear, implementar y consumir una aplicación de API de ASP.NET en el Servicio de aplicaciones de Azure con Visual Studio 2015."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="89e8d-103">Introducción a Aplicaciones de API, ASP.NET y Swagger en el Servicio de aplicaciones de Azure</span><span class="sxs-lookup"><span data-stu-id="89e8d-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="89e8d-104">Este es el primero de una serie de tutoriales que muestran cómo utilizar las características del Servicio de aplicaciones de Azure que resultan útiles para el desarrollo y el hospedaje de API de RESTful:</span><span class="sxs-lookup"><span data-stu-id="89e8d-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="89e8d-105">En este tutorial se explica la compatibilidad con los metadatos de la API en formato Swagger.</span><span class="sxs-lookup"><span data-stu-id="89e8d-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="89e8d-106">Aprenderá a realizar los siguientes procedimientos:</span><span class="sxs-lookup"><span data-stu-id="89e8d-106">You'll learn:</span></span>

* <span data-ttu-id="89e8d-107">Crear e implementar [aplicaciones de API](app-service-api-apps-why-best-platform.md) en el Servicio de aplicaciones de Azure mediante las herramientas integradas en Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="89e8d-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="89e8d-108">Automatizar la detección de la API mediante el paquete NuGet Swashbuckle para generar dinámicamente metadatos de la API de Swagger.</span><span class="sxs-lookup"><span data-stu-id="89e8d-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="89e8d-109">Usar los metadatos de la API de Swagger para generar automáticamente el código de cliente para una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="89e8d-110">Información general de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89e8d-110">Sample application overview</span></span>
<span data-ttu-id="89e8d-111">En este tutorial, se trabaja con una aplicación de ejemplo de lista de tareas pendientes sencilla.</span><span class="sxs-lookup"><span data-stu-id="89e8d-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="89e8d-112">La aplicación tiene un front-end de aplicación de una sola página (SPA), un nivel intermedio de ASP.NET Web API y una capa de datos de ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagrama de la aplicación de ejemplo de Aplicaciones de API](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="89e8d-114">Esta es una captura de pantalla del front-end de [AngularJS](https://angularjs.org/) .</span><span class="sxs-lookup"><span data-stu-id="89e8d-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Lista de tareas pendientes de la aplicación de ejemplo de Aplicaciones de API](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="89e8d-116">La solución de Visual Studio incluye tres proyectos:</span><span class="sxs-lookup"><span data-stu-id="89e8d-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="89e8d-117">**ToDoListAngular** : el front-end, una SPA de AngularJS que llama al nivel intermedio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="89e8d-118">**ToDoListAPI** : el nivel intermedio, un proyecto de ASP.NET Web API que llama a la capa de datos para realizar operaciones CRUD en tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="89e8d-119">**ToDoListDataAPI**: la capa de datos, un proyecto de ASP.NET Web API que realiza operaciones CRUD en tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="89e8d-120">La arquitectura de tres niveles es una de las muchas que puede implementar mediante Aplicaciones de API y se utiliza aquí únicamente como demostración.</span><span class="sxs-lookup"><span data-stu-id="89e8d-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="89e8d-121">El código de cada nivel es lo más simple posible para mostrar las características de Aplicaciones de API. Por ejemplo, la capa de datos utiliza memoria del servidor en lugar de una base de datos como mecanismo de persistencia.</span><span class="sxs-lookup"><span data-stu-id="89e8d-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="89e8d-122">Al finalizar este tutorial, tendrá los dos proyectos de Web API funcionando en la nube en Aplicaciones de API del Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="89e8d-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="89e8d-123">En el siguiente tutorial de la serie, se implementa el front-end de SPA en la nube.</span><span class="sxs-lookup"><span data-stu-id="89e8d-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89e8d-124">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="89e8d-124">Prerequisites</span></span>
* <span data-ttu-id="89e8d-125">ASP.NET Web API: en las instrucciones del tutorial se da por sentado que tiene conocimientos básicos sobre cómo trabajar con ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="89e8d-126">Cuenta de Azure: puede [abrir una cuenta gratuita de Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) o [activar las ventajas de las que disfrutan los suscriptores de Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="89e8d-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="89e8d-127">Si desea empezar a usar el Servicio de aplicaciones de Azure antes de suscribirse para obtener una cuenta de Azure, vaya a la [prueba gratuita del Servicio de aplicaciones](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="89e8d-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="89e8d-128">Ahí puede crear de forma inmediata una aplicación de inicio de corta duración en App Service ( **no se requiere tarjeta de crédito**ni se establece ningún compromiso).</span><span class="sxs-lookup"><span data-stu-id="89e8d-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="89e8d-129">Visual Studio 2015 con [Azure SDK para .NET](https://azure.microsoft.com/downloads/archive-net-downloads/): el SDK instala automáticamente Visual Studio 2015 si aún no lo tiene.</span><span class="sxs-lookup"><span data-stu-id="89e8d-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="89e8d-130">En Visual Studio, haga clic en Ayuda -> Acerca de Microsoft Visual Studio y asegúrese de que tiene instalado "Azure App Service Tools v2.9.1", o una versión superior.</span><span class="sxs-lookup"><span data-stu-id="89e8d-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versión de Azure App Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="89e8d-132">Según la cantidad de dependencias de SDK que tenga ya en la máquina, la instalación del SDK puede tardar un período largo, desde unos minutos a media hora o más.</span><span class="sxs-lookup"><span data-stu-id="89e8d-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="89e8d-133">Descarga de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="89e8d-133">Download the sample application</span></span>
1. <span data-ttu-id="89e8d-134">Descargue el repositorio [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) .</span><span class="sxs-lookup"><span data-stu-id="89e8d-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="89e8d-135">Puede hacer clic en el botón **Descargar zip** o clonar el repositorio en la máquina local.</span><span class="sxs-lookup"><span data-stu-id="89e8d-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="89e8d-136">Abra la solución ToDoList en Visual Studio 2015 o 2013.</span><span class="sxs-lookup"><span data-stu-id="89e8d-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="89e8d-137">Tendrá que confiar en todas las soluciones.</span><span class="sxs-lookup"><span data-stu-id="89e8d-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="89e8d-138">![Advertencia de seguridad](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="89e8d-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="89e8d-139">Compile la solución (CTRL + MAYÚS + B) para restaurar los paquetes NuGet.</span><span class="sxs-lookup"><span data-stu-id="89e8d-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="89e8d-140">Si desea ver la aplicación en funcionamiento antes de implementarla, puede ejecutarla localmente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="89e8d-141">Asegúrese de que ToDoListDataAPI es el proyecto de inicio y ejecute la solución.</span><span class="sxs-lookup"><span data-stu-id="89e8d-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="89e8d-142">Debería ver un error HTTP 403 en el explorador.</span><span class="sxs-lookup"><span data-stu-id="89e8d-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="89e8d-143">Uso de la interfaz de usuario y los metadatos de la API de Swagger</span><span class="sxs-lookup"><span data-stu-id="89e8d-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="89e8d-144">La compatibilidad con los metadatos de la API de [Swagger 2.0](http://swagger.io/) está integrada en el Servicio de aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="89e8d-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="89e8d-145">Cada aplicación de API puede especificar un punto de conexión de URL que devuelve los metadatos de la API en formato JSON de Swagger.</span><span class="sxs-lookup"><span data-stu-id="89e8d-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="89e8d-146">Los metadatos que devuelve dicho punto de conexión pueden utilizarse para generar código de cliente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="89e8d-147">Un proyecto de ASP.NET Web API puede generar de forma dinámica los metadatos de Swagger mediante el paquete NuGet [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) .</span><span class="sxs-lookup"><span data-stu-id="89e8d-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="89e8d-148">El paquete NuGet Swashbuckle ya está instalado en los proyectos ToDoListDataAPI y ToDoListAPI que descargó.</span><span class="sxs-lookup"><span data-stu-id="89e8d-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="89e8d-149">En esta sección del tutorial verá los metadatos de Swagger 2.0 generados y, después, probará una interfaz de usuario que se basa en dichos metadatos.</span><span class="sxs-lookup"><span data-stu-id="89e8d-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="89e8d-150">Establezca el proyecto ToDoListDataAPI (**no** ToDoListAP) como proyecto de inicio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![Establezca ToDoDataAPI como proyecto de inicio](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="89e8d-152">Presione F5 o haga clic en **Depurar > Iniciar depuración** para ejecutar el proyecto en modo de depuración.</span><span class="sxs-lookup"><span data-stu-id="89e8d-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="89e8d-153">El explorador se abre y muestra la página de error HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="89e8d-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="89e8d-154">En la barra de direcciones del explorador, agregue `swagger/docs/v1` al final de la línea y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="89e8d-155">(La dirección URL es `http://localhost:45914/swagger/docs/v1`).</span><span class="sxs-lookup"><span data-stu-id="89e8d-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="89e8d-156">Esta es la dirección URL predeterminada que Swashbuckle usa para devolver los metadatos JSON de Swagger 2.0 para la API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="89e8d-157">Si usa Internet Explorer, se le pide que descargue un archivo *v1.json* .</span><span class="sxs-lookup"><span data-stu-id="89e8d-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![Descargar metadatos de JSON en Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="89e8d-159">Si usa Chrome, Firefox o Edge, el explorador muestra el archivo JSON en la ventana del explorador.</span><span class="sxs-lookup"><span data-stu-id="89e8d-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="89e8d-160">Los distintos exploradores controlan JSON de forma diferente y la ventana del explorador puede no ser exactamente igual que en el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="89e8d-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![Metadatos de JSON en Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="89e8d-162">El ejemplo siguiente muestra la primera sección de los metadatos de Swagger para la API, con la definición del método Get.</span><span class="sxs-lookup"><span data-stu-id="89e8d-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="89e8d-163">Estos metadatos son el motor de la interfaz de usuario de Swagger que usará en los pasos siguientes, y los utilizará en una sección posterior del tutorial para generar automáticamente el código de cliente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="89e8d-164">Cierre el explorador y detenga la depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="89e8d-165">En el proyecto ToDoListDataAPI, en el **Explorador de soluciones**, abra el archivo *App_Start\SwaggerConfig.cs*, desplácese hacia abajo hasta la línea 174 y quite las marcas de comentarios del siguiente código.</span><span class="sxs-lookup"><span data-stu-id="89e8d-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="89e8d-166">El archivo *SwaggerConfig.cs* se crea cuando se instala el paquete Swashbuckle en un proyecto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="89e8d-167">El archivo ofrece varias maneras de configurar Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="89e8d-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="89e8d-168">El código cuyas marcas de comentarios ha quitado habilita la interfaz de usuario de Swagger que usará en los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="89e8d-169">Al crear un proyecto de Web API con la plantilla de proyecto de aplicación de API, este código aparece como comentarios de forma predeterminada como medida de seguridad.</span><span class="sxs-lookup"><span data-stu-id="89e8d-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="89e8d-170">Vuelva a ejecutar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-170">Run the project again.</span></span>
7. <span data-ttu-id="89e8d-171">En la barra de direcciones del explorador, agregue `swagger` al final de la línea y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="89e8d-172">(La dirección URL es `http://localhost:45914/swagger`).</span><span class="sxs-lookup"><span data-stu-id="89e8d-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="89e8d-173">Cuando aparezca la página de la interfaz de usuario de Swagger, haga clic en **ToDoList** para ver los métodos disponibles.</span><span class="sxs-lookup"><span data-stu-id="89e8d-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Métodos disponibles en la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="89e8d-175">Haga clic en el primer botón **Get** (Obtener) en la lista.</span><span class="sxs-lookup"><span data-stu-id="89e8d-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="89e8d-176">En la sección **Parameters** (Parámetros), escriba un asterisco como valor del parámetro `owner` y haga clic en **Try it out** (Probar).</span><span class="sxs-lookup"><span data-stu-id="89e8d-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="89e8d-177">Cuando agregue autenticación en tutoriales posteriores, el nivel intermedio proporcionará el id. de usuario real a la capa de datos.</span><span class="sxs-lookup"><span data-stu-id="89e8d-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="89e8d-178">Por ahora, todas las tareas tendrán asterisco como identificador de propietario mientras la aplicación se ejecuta sin la autenticación habilitada.</span><span class="sxs-lookup"><span data-stu-id="89e8d-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="89e8d-180">La interfaz de usuario de Swagger llama al método Get de ToDoList y muestra la respuesta del código y los resultados de JSON.</span><span class="sxs-lookup"><span data-stu-id="89e8d-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Resultado de hacer clic en el botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="89e8d-182">Haga clic en **Post** (Publicar) y, a continuación, haga clic en el cuadro situado debajo de **Model Schema** (Esquema de modelo).</span><span class="sxs-lookup"><span data-stu-id="89e8d-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="89e8d-183">Al hacer clic en el esquema del modelo se rellena el cuadro de entrada donde puede especificar el valor del parámetro para el método Post.</span><span class="sxs-lookup"><span data-stu-id="89e8d-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="89e8d-184">(Si esto no funciona en Internet Explorer, use un explorador diferente o escriba el valor del parámetro en el paso siguiente de forma manual).</span><span class="sxs-lookup"><span data-stu-id="89e8d-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Publicación tras hacer clic en el botón Try it out (Probar) de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="89e8d-186">Cambie el código JSON en el cuadro de entrada del parámetro `todo` para que se parezca al ejemplo siguiente o sustitúyalo por el texto descriptivo que desee:</span><span class="sxs-lookup"><span data-stu-id="89e8d-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="89e8d-187">Haga clic en **Try it out**(Probar).</span><span class="sxs-lookup"><span data-stu-id="89e8d-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="89e8d-188">La API de ToDoList devuelve un código de respuesta HTTP 204 que indica que todo es correcto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="89e8d-189">Haga clic en el primer botón **Get** (Obtener) y, en esa sección de la página, haga clic en el botón **Try it out** (Probar).</span><span class="sxs-lookup"><span data-stu-id="89e8d-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="89e8d-190">La respuesta del método Get ahora incluye el nuevo elemento de tareas pendientes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="89e8d-191">Opcional: pruebe también los métodos Put, Delete y Get by ID.</span><span class="sxs-lookup"><span data-stu-id="89e8d-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="89e8d-192">Cierre el explorador y detenga la depuración de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="89e8d-193">Swashbuckle funciona con cualquier proyecto de ASP.NET Web API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="89e8d-194">Si desea agregar generación de metadatos de Swagger a un proyecto existente, simplemente instale el paquete de Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="89e8d-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="89e8d-195">Los metadatos de Swagger incluyen un identificador único para cada operación de la API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="89e8d-196">De manera predeterminada, Swashbuckle puede generar identificadores de operación de Swagger duplicados para los métodos del controlador de la API web.</span><span class="sxs-lookup"><span data-stu-id="89e8d-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="89e8d-197">Esto sucede si el controlador tiene métodos HTTP sobrecargados, tales como `Get()` y `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="89e8d-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="89e8d-198">Para obtener información sobre cómo controlar las sobrecargas, consulte [Personalización de definiciones de API generadas por Swashbuckle](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="89e8d-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="89e8d-199">Si crea un proyecto de API web en Visual Studio con la plantilla Aplicación de API de Azure, el código que genera identificadores de operaciones únicos se agrega automáticamente al archivo *SwaggerConfig.cs* .</span><span class="sxs-lookup"><span data-stu-id="89e8d-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="89e8d-200"><a id="createapiapp"></a> Creación de una aplicación de API en Azure e implementación de código en ella</span><span class="sxs-lookup"><span data-stu-id="89e8d-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="89e8d-201">En esta sección, se usan las herramientas de Azure integradas en el Asistente para **publicación web** de Visual Studio para crear una aplicación de API en Azure.</span><span class="sxs-lookup"><span data-stu-id="89e8d-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="89e8d-202">A continuación, se implementa el proyecto ToDoListDataAPI en la nueva aplicación de API y se llama a la API, para lo que se ejecuta la interfaz de usuario de Swagger.</span><span class="sxs-lookup"><span data-stu-id="89e8d-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="89e8d-203">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto ToDoListDataAPI y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Haga clic en Publicar en Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="89e8d-205">En el paso **Perfil** del Asistente para **publicación web**, haga clic en **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Haga clic en Servicio de aplicaciones de Azure en Publicación web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="89e8d-207">Inicie sesión en su cuenta de Azure si aún no lo hizo o actualice sus credenciales si expiraron.</span><span class="sxs-lookup"><span data-stu-id="89e8d-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="89e8d-208">En el cuadro de diálogo Servicio de aplicaciones, elija la **suscripción** de Azure que desee usar y haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Haga clic en Nuevo en el cuadro de diálogo Servicio de aplicaciones](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="89e8d-210">Se muestra la pestaña **Hospedaje** del cuadro de diálogo **Crear servicio de aplicaciones**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="89e8d-211">Dado que va a implementar un proyecto de Web API que tiene instalado Swashbuckle, Visual Studio asume que quiere crear una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="89e8d-212">Esto se indica con el título **API App Name** (Nombre de aplicación de API) y con el hecho de que la lista desplegable **Cambiar tipo** está establecida en **Aplicación de API**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![Tipo de aplicación en el cuadro de diálogo Servicio de aplicaciones](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="89e8d-214">En **Nombre de aplicación de API** , escriba un nombre que sea único en el dominio *azurewebsites.net* .</span><span class="sxs-lookup"><span data-stu-id="89e8d-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="89e8d-215">Puede aceptar el nombre predeterminado que Visual Studio proporciona.</span><span class="sxs-lookup"><span data-stu-id="89e8d-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="89e8d-216">Si escribe un nombre que alguien haya usado, aparecerá un signo de exclamación rojo a la derecha.</span><span class="sxs-lookup"><span data-stu-id="89e8d-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="89e8d-217">La dirección URL de la aplicación de API será `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="89e8d-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="89e8d-218">En la lista desplegable **Grupo de recursos**, haga clic en **Nuevo** y escriba "ToDoListGroup" u otro nombre que prefiera.</span><span class="sxs-lookup"><span data-stu-id="89e8d-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="89e8d-219">Un grupo de recursos es una colección de recursos de Azure tales como aplicaciones de API, bases de datos, máquinas virtuales, etc.</span><span class="sxs-lookup"><span data-stu-id="89e8d-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="89e8d-220">Para este tutorial, se recomienda crear un nuevo grupo de recursos, ya que así podrá eliminar fácilmente y en un solo paso todos los recursos de Azure que cree para el tutorial.</span><span class="sxs-lookup"><span data-stu-id="89e8d-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="89e8d-221">Este cuadro permite seleccionar un [grupo de recursos](../azure-resource-manager/resource-group-overview.md) existente o crear uno nuevo, para lo que se debe escribir un nombre de grupo recursos que no exista en la suscripción.</span><span class="sxs-lookup"><span data-stu-id="89e8d-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="89e8d-222">Haga clic en el botón **Nuevo** situado junto a la lista desplegable **Plan de App Service**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="89e8d-223">La captura de pantalla muestra los valores de ejemplo de **API App Name** (Nombre de aplicación de API), **Suscripción** y **Grupo de recursos**, pero sus valores serán diferentes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="89e8d-225">En los siguientes pasos se crea un plan del Servicio de aplicaciones para el nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="89e8d-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="89e8d-226">Un plan del Servicio de aplicaciones especifica los recursos de proceso en los que se ejecuta la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="89e8d-227">Por ejemplo, si elige el nivel Gratis, la aplicación de API se ejecuta en máquinas virtuales compartidas, mientras que para algunos niveles de pago, se ejecuta en máquinas virtuales dedicadas.</span><span class="sxs-lookup"><span data-stu-id="89e8d-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="89e8d-228">Para más información sobre los planes del Servicio de aplicaciones, consulte [Introducción detallada sobre los planes del Servicio de aplicaciones de Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="89e8d-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="89e8d-229">En el cuadro de diálogo **Configurar el plan de servicio de aplicaciones** , escriba "ToDoListPlan" u otro nombre que prefiera.</span><span class="sxs-lookup"><span data-stu-id="89e8d-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="89e8d-230">En la lista desplegable **Ubicación** , elija la ubicación más cercana.</span><span class="sxs-lookup"><span data-stu-id="89e8d-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="89e8d-231">Esta opción especifica en qué centro de datos de Azure se ejecutará su aplicación.</span><span class="sxs-lookup"><span data-stu-id="89e8d-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="89e8d-232">Elija una ubicación cercana para minimizar la [latencia](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="89e8d-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="89e8d-233">En la lista desplegable **Tamaño**, haga clic en **Gratis**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="89e8d-234">Para este tutorial, el plan de tarifa gratis proporcionará un rendimiento suficiente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="89e8d-235">En el cuadro de diálogo **Configurar el plan de servicio de aplicaciones**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Haga clic en Aceptar en Configurar el plan de servicio de aplicaciones](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="89e8d-237">En el cuadro de diálogo **Crear servicio de aplicaciones**, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Haga clic en Crear en el cuadro de diálogo Crear servicio de aplicaciones](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="89e8d-239">Visual Studio crea la aplicación de API y un perfil de publicación que tiene toda la configuración necesaria para la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="89e8d-240">Después, se abre el Asistente para **publicación web** , que se usará para implementar el proyecto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="89e8d-241">Se abre el Asistente para **publicación web** en la pestaña **Conexión**, tal como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="89e8d-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="89e8d-242">En la pestaña **Conexión**, los valores de **Servidor** y **Nombre del sitio** apuntan a la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="89e8d-243">**Nombre de usuario** y **Contraseña** son credenciales de implementación que Azure crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="89e8d-244">Después de la implementación, Visual Studio abre un explorador en la **Dirección URL de destino** (esta es la única finalidad de la **Dirección URL de destino**).</span><span class="sxs-lookup"><span data-stu-id="89e8d-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="89e8d-245">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-245">Click **Next**.</span></span>
    
    ![Haga clic en Siguiente en la pestaña Conexión de Publicación web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="89e8d-247">La pestaña siguiente es la de **Configuración** (como se muestra a continuación).</span><span class="sxs-lookup"><span data-stu-id="89e8d-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="89e8d-248">Aquí puede cambiar la pestaña de configuración de compilación para implementar una compilación de depuración para la [depuración remota](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="89e8d-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="89e8d-249">En la pestaña también se encuentran varias **Opciones de publicación de archivos**:</span><span class="sxs-lookup"><span data-stu-id="89e8d-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="89e8d-250">Quitar archivos adicionales en el destino.</span><span class="sxs-lookup"><span data-stu-id="89e8d-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="89e8d-251">Precompilar durante la publicación.</span><span class="sxs-lookup"><span data-stu-id="89e8d-251">Precompile during publishing</span></span>
    * <span data-ttu-id="89e8d-252">Excluir archivos de la carpeta App_Data.</span><span class="sxs-lookup"><span data-stu-id="89e8d-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="89e8d-253">Para este tutorial no necesita ninguna de ellas.</span><span class="sxs-lookup"><span data-stu-id="89e8d-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="89e8d-254">Para información más detallada de lo que hacen, consulte [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx)(Implementación de un proyecto web mediante publicación con un solo clic en Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="89e8d-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="89e8d-255">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-255">Click **Next**.</span></span>
    
    ![Haga clic en Siguiente en la pestaña Configuración de Publicación web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="89e8d-257">A continuación, la pestaña **Vista previa** (que se muestra aquí) ofrece la posibilidad de ver qué archivos se van a copiar desde el proyecto a la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="89e8d-258">Al implementar un proyecto en una aplicación de API para la que ya implementó anteriormente, solo se copian los archivos modificados.</span><span class="sxs-lookup"><span data-stu-id="89e8d-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="89e8d-259">Si desea ver una lista de lo que se va a copiar, haga clic en el botón **Comenzar previsualización** .</span><span class="sxs-lookup"><span data-stu-id="89e8d-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="89e8d-260">Haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-260">Click **Publish**.</span></span>
    
    ![Haga clic en Publicar en la pestaña Vista previa de Publicación web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="89e8d-262">Visual Studio implementa el proyecto ToDoListDataAPI en la nueva aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="89e8d-263">La ventana **Salida** registra la implementación correcta y aparece una página "se creó correctamente" en una ventana del explorador que se abre con la dirección URL de la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Implementación correcta en la ventana Salida](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Página nueva que indica que la aplicación de API se creó correctamente](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="89e8d-266">En la barra de direcciones del explorador, agregue "swagger" a la URL y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="89e8d-267">(La dirección URL es `http://{apiappname}.azurewebsites.net/swagger`).</span><span class="sxs-lookup"><span data-stu-id="89e8d-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="89e8d-268">El explorador muestra la misma interfaz de usuario de Swagger que vio anteriormente, pero ahora se ejecuta en la nube.</span><span class="sxs-lookup"><span data-stu-id="89e8d-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="89e8d-269">Pruebe el método Get y verá que vuelve a las dos tareas predeterminadas.</span><span class="sxs-lookup"><span data-stu-id="89e8d-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="89e8d-270">Los cambios realizados anteriormente se guardaron en la memoria del equipo local.</span><span class="sxs-lookup"><span data-stu-id="89e8d-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="89e8d-271">Abra el [Portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="89e8d-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="89e8d-272">El Portal de Azure es una interfaz web para administrar recursos de Azure tales como aplicaciones de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="89e8d-273">Haga clic en **Más servicios > App Services**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-273">Click **More Services > App Services**.</span></span>
    
    ![Examinar Servicios de aplicaciones](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="89e8d-275">En la hoja **Servicios de aplicaciones** , busque la nueva aplicación de API y haga clic en ella.</span><span class="sxs-lookup"><span data-stu-id="89e8d-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="89e8d-276">(En el Portal de Azure, las ventanas que se abren a la derecha se llaman *hojas*).</span><span class="sxs-lookup"><span data-stu-id="89e8d-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![Hoja Servicios de aplicaciones](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="89e8d-278">Se abren dos hojas:</span><span class="sxs-lookup"><span data-stu-id="89e8d-278">Two blades open.</span></span> <span data-ttu-id="89e8d-279">una con información general sobre la aplicación de API y otra con una larga lista de valores que puede ver y cambiar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="89e8d-280">En la hoja **Configuración**, busque la sección **API** y haga clic en **Definición de API**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![Definición de la API en hoja Configuración](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="89e8d-282">La hoja **Definición de la API** le permite especificar la dirección URL que devuelve los metadatos de Swagger 2.0 en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="89e8d-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="89e8d-283">Cuando Visual Studio crea la aplicación de API, establece la dirección URL de la definición de API en el valor predeterminado de los metadatos generados por Swashbuckle que vio antes, que es la URL base de la aplicación de API más `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="89e8d-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![Dirección URL de definición de la API](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="89e8d-285">Cuando se selecciona una aplicación de API para la que se va a generar código de cliente, Visual Studio recupera los metadatos de esta dirección URL.</span><span class="sxs-lookup"><span data-stu-id="89e8d-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="89e8d-286"><a id="codegen"></a> Generación de código de cliente para la capa de datos</span><span class="sxs-lookup"><span data-stu-id="89e8d-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="89e8d-287">Una de las ventajas de integrar Swagger en aplicaciones de API de Azure es la generación automática de código.</span><span class="sxs-lookup"><span data-stu-id="89e8d-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="89e8d-288">Las clases de cliente generadas hacen que sea más fácil escribir código que llame a una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="89e8d-289">El proyecto ToDoListAPI ya tiene el código de cliente generado, pero en los siguientes pasos lo eliminará y lo volverá a crear para ver cómo se genera código.</span><span class="sxs-lookup"><span data-stu-id="89e8d-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="89e8d-290">En el **Explorador de soluciones**de Visual Studio, en el proyecto ToDoListAPI, elimine la carpeta *ToDoListDataAPI* .</span><span class="sxs-lookup"><span data-stu-id="89e8d-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="89e8d-291">**Precaución: Elimine solamente la carpeta, no el proyecto ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="89e8d-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Eliminar código de cliente generado](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="89e8d-293">Esta carpeta se creó mediante el proceso de generación de código que está punto de recorrer.</span><span class="sxs-lookup"><span data-stu-id="89e8d-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="89e8d-294">Haga clic con el botón derecho en el proyecto ToDoListAPI y, después, en **Agregar > Cliente de API de REST**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Agregar cliente de API de REST en Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="89e8d-296">En el cuadro de diálogo **Agregar cliente de API de REST**, haga clic en **URL de Swagger** y en **Seleccionar recurso de Azure**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Seleccionar recurso de Azure](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="89e8d-298">En el cuadro de diálogo **App Service**, expanda el grupo de recursos que usa en este tutorial, seleccione la aplicación de API y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![Seleccione aplicación de API para la generación de código](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="89e8d-300">Observe que al volver al cuadro de diálogo **Agregar cliente de API de REST** , el cuadro de texto se rellenó con la dirección URL de la definición de API que vio anteriormente en el portal.</span><span class="sxs-lookup"><span data-stu-id="89e8d-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![Dirección URL de definición de la API](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="89e8d-302">Como alternativa para obtener los metadatos para la generación del código, puede escribir la dirección URL directamente en lugar de utilizar el cuadro de diálogo Examinar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="89e8d-303">Por otra parte, si desea generar el código de cliente antes de implementarlo en Azure, puede ejecutar el proyecto de Web API localmente, ir a la dirección URL que proporciona el archivo JSON de Swagger, guardar el archivo y usar la opción **Seleccionar un archivo de metadatos de Swagger existente** .</span><span class="sxs-lookup"><span data-stu-id="89e8d-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="89e8d-304">En el cuadro de diálogo **Agregar cliente de API de REST**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="89e8d-305">Visual Studio crea una carpeta con el nombre de la aplicación de API y genera clases cliente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Archivos de código para cliente generado](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="89e8d-307">En el proyecto ToDoListAPI, abra *Controllers\ToDoListController.cs* para ver el código de la línea 40 que llama a la API mediante el cliente generado.</span><span class="sxs-lookup"><span data-stu-id="89e8d-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="89e8d-308">El siguiente fragmento de código muestra cómo el código crea instancias del objeto de cliente y llama al método Get.</span><span class="sxs-lookup"><span data-stu-id="89e8d-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="89e8d-309">El parámetro de constructor obtiene la dirección URL del punto de conexión en la configuración de la aplicación `toDoListDataAPIURL`.</span><span class="sxs-lookup"><span data-stu-id="89e8d-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="89e8d-310">En el archivo Web.config, dicho valor se establece en la dirección URL local de IIS Express del proyecto de la API para que pueda ejecutar la aplicación localmente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="89e8d-311">Si se omite el parámetro del constructor, el punto de conexión predeterminado es la dirección URL a partir de la cual se genera el código.</span><span class="sxs-lookup"><span data-stu-id="89e8d-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="89e8d-312">La clase de cliente se generará con un nombre diferente según el nombre de la aplicación de API; cambie el código en *Controllers\ToDoListController.cs* para que el nombre del tipo coincida con el que se generó en el proyecto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="89e8d-313">Por ejemplo, si el nombre de la aplicación de API es ToDoListDataAPI071316, cambiaría este código:</span><span class="sxs-lookup"><span data-stu-id="89e8d-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="89e8d-314">a este:</span><span class="sxs-lookup"><span data-stu-id="89e8d-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="89e8d-315">Creación de una aplicación de API para hospedar el nivel intermedio</span><span class="sxs-lookup"><span data-stu-id="89e8d-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="89e8d-316">Antes [creó la aplicación de API de la capa de datos e implementó código en ella](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="89e8d-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="89e8d-317">Siga ahora el mismo procedimiento para la aplicación de API de nivel intermedio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="89e8d-318">En el **Explorador de soluciones**, haga clic con el botón derecho en el proyecto ToDoListAPI de nivel intermedio (no en ToDoListDataAPI de la capa de datos) y haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Haga clic en Publicar en Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="89e8d-320">En la pestaña **Perfil** del Asistente para **publicación web**, haga clic en **Servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="89e8d-321">En el cuadro de diálogo **App Service**, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="89e8d-322">En la pestaña **Hospedaje** del cuadro de diálogo **Crear servicio de aplicaciones**, acepte el nombre predeterminado en **Nombre de la aplicación de API** o escriba uno único en el dominio *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="89e8d-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="89e8d-323">Elija la **suscripción** de Azure que ha usado.</span><span class="sxs-lookup"><span data-stu-id="89e8d-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="89e8d-324">En la lista desplegable **Grupo de recursos** , elija el grupo de recursos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="89e8d-325">En la lista desplegable **Plan del Servicio de aplicaciones** , elija el plan que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="89e8d-326">Usará ese valor de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="89e8d-326">It will default to that value.</span></span>
8. <span data-ttu-id="89e8d-327">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-327">Click **Create**.</span></span>
   
    <span data-ttu-id="89e8d-328">Visual Studio crea la aplicación de API, crea un perfil de publicación para ella y muestra el paso **Conexión** del Asistente para **publicación web**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="89e8d-329">En el paso **Conexión** del Asistente para **publicación web**, haga clic en **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="89e8d-330">Visual Studio implementa el proyecto ToDoListAPI en la nueva aplicación de API y abre un explorador en la dirección URL de la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="89e8d-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="89e8d-331">Aparece una página "creado correctamente".</span><span class="sxs-lookup"><span data-stu-id="89e8d-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="89e8d-332">Configuración del nivel intermedio para llamar a la capa de datos</span><span class="sxs-lookup"><span data-stu-id="89e8d-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="89e8d-333">Si llamara ahora a la aplicación de API de nivel intermedio, intentaría llamar a la capa de datos usando la dirección URL localhost que todavía está en el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="89e8d-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="89e8d-334">En esta sección agregará la dirección URL de la aplicación de API de nivel de datos a una configuración del entorno de la aplicación de API de nivel intermedio.</span><span class="sxs-lookup"><span data-stu-id="89e8d-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="89e8d-335">Cuando el código de la aplicación de API de nivel medio recupera la configuración de URL del nivel de datos, la configuración del entorno invalida lo que hay en el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="89e8d-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="89e8d-336">Vaya al [Portal de Azure](https://portal.azure.com/)y después a la hoja **Aplicación de API** de la aplicación de API que creó para hospedar el proyecto TodoListAPI (nivel intermedio).</span><span class="sxs-lookup"><span data-stu-id="89e8d-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="89e8d-337">En la hoja **Configuración** de la aplicación de API, haga clic en **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="89e8d-338">En la hoja **Configuración de la aplicación** de la aplicación de API, desplácese hacia abajo hasta la sección **Configuración de aplicación** y agregue la clave y el valor siguientes.</span><span class="sxs-lookup"><span data-stu-id="89e8d-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="89e8d-339">El valor será la dirección URL de la primera aplicación de API que publicó en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="89e8d-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="89e8d-340">**Clave**</span><span class="sxs-lookup"><span data-stu-id="89e8d-340">**Key**</span></span> | <span data-ttu-id="89e8d-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="89e8d-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="89e8d-342">**Valor**</span><span class="sxs-lookup"><span data-stu-id="89e8d-342">**Value**</span></span> |<span data-ttu-id="89e8d-343">https://{nombre de la aplicación de API de capa de datos}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="89e8d-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="89e8d-344">**Ejemplo**</span><span class="sxs-lookup"><span data-stu-id="89e8d-344">**Example**</span></span> |<span data-ttu-id="89e8d-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="89e8d-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="89e8d-346">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-346">Click **Save**.</span></span>
   
    ![Haga clic en Guardar en Configuración de aplicaciones](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="89e8d-348">Cuando el código se ejecuta en Azure, este valor anulará ahora la dirección URL de host local que se encuentra en el archivo Web.config.</span><span class="sxs-lookup"><span data-stu-id="89e8d-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="89e8d-349">Prueba</span><span class="sxs-lookup"><span data-stu-id="89e8d-349">Test</span></span>
1. <span data-ttu-id="89e8d-350">En una ventana del explorador, vaya a la dirección URL de la aplicación de API de nivel intermedio que acaba de crear para ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="89e8d-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="89e8d-351">Para ello, haga clic en la dirección URL en la hoja principal de la aplicación de API en el portal.</span><span class="sxs-lookup"><span data-stu-id="89e8d-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="89e8d-352">En la barra de direcciones del explorador, agregue "swagger" a la URL y presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="89e8d-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="89e8d-353">(La dirección URL es `http://{apiappname}.azurewebsites.net/swagger`).</span><span class="sxs-lookup"><span data-stu-id="89e8d-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="89e8d-354">El explorador muestra la misma interfaz de usuario de Swagger que vio antes para ToDoListDataAPI, pero ahora `owner` no es un campo obligatorio para la operación Get. Esto se debe a que la aplicación de API de nivel intermedio envía dicho valor a la aplicación de API de capa de datos automáticamente.</span><span class="sxs-lookup"><span data-stu-id="89e8d-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="89e8d-355">(Al realizar los tutoriales de autenticación, el nivel intermedio enviará identificadores de usuario reales para el parámetro `owner`; por ahora, se incluye un asterisco en el código).</span><span class="sxs-lookup"><span data-stu-id="89e8d-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="89e8d-356">Pruebe el método Get y los otros métodos para validar que la aplicación de API de nivel intermedio llama correctamente a la aplicación de API de capa de datos.</span><span class="sxs-lookup"><span data-stu-id="89e8d-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Método Get de la interfaz de usuario de Swagger](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="89e8d-358">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="89e8d-358">Troubleshooting</span></span>
<span data-ttu-id="89e8d-359">Si experimenta algún problema mientras lleva a cabo este tutorial, aquí se ofrecen ideas para solucionarlo:</span><span class="sxs-lookup"><span data-stu-id="89e8d-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="89e8d-360">Asegúrese de que usa la versión más reciente de [Azure SDK para .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="89e8d-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="89e8d-361">Dos de los nombres de proyecto son similares (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="89e8d-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="89e8d-362">Si lo que ve no se parece a lo que se describe en las instrucciones cuando trabaje con un proyecto, asegúrese de que ha abierto el proyecto correcto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="89e8d-363">Si está en una red corporativa y está intentando realizar la implementación en el Servicio de aplicaciones de Azure mediante un firewall, asegúrese de que los puertos 443 y 8172 estén abiertos para Web Deploy.</span><span class="sxs-lookup"><span data-stu-id="89e8d-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="89e8d-364">Si no puede abrir estos puertos, puede usar otros métodos de implementación.</span><span class="sxs-lookup"><span data-stu-id="89e8d-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="89e8d-365">Consulte [Documentación de implementación del Servicio de aplicaciones de Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="89e8d-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="89e8d-366">Errores "Los nombres de ruta deben ser únicos": pueden aparecer si implementa accidentalmente el proyecto incorrecto en una aplicación de API y después implementa el correcto.</span><span class="sxs-lookup"><span data-stu-id="89e8d-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="89e8d-367">Para corregir este problema, vuelva a implementar el proyecto correcto en la aplicación de API y, en la pestaña **Configuración** del Asistente para **publicación web**, seleccione **Quitar archivos adicionales en el destino**.</span><span class="sxs-lookup"><span data-stu-id="89e8d-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="89e8d-368">Una vez que la aplicación de API de ASP.NET se esté ejecutando en el Servicio de aplicaciones de Azure, podrá obtener más información acerca de las características de Visual Studio que simplifican la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="89e8d-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="89e8d-369">Para más información sobre el registro o la depuración remota, entre otros temas, consulte [Solución de problemas de una aplicación web en Azure App Service con Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="89e8d-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89e8d-370">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89e8d-370">Next steps</span></span>
<span data-ttu-id="89e8d-371">Ha visto cómo implementar proyectos de Web API existentes en aplicaciones de API, cómo generar código de cliente para aplicaciones de API y cómo consumir aplicaciones de API desde clientes .NET.</span><span class="sxs-lookup"><span data-stu-id="89e8d-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="89e8d-372">El siguiente tutorial de esta serie muestra cómo [usar CORS para consumir aplicaciones de API desde clientes de JavaScript](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="89e8d-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="89e8d-373">Para más información acerca de la generación de código de cliente, consulte el repositorio [Azure/AutoRest](https://github.com/azure/autorest) en GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="89e8d-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="89e8d-374">Si necesita ayuda con los problemas de uso del cliente generado, abra un [incidente en el repositorio de AutoRest](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="89e8d-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="89e8d-375">Si desea crear proyectos de aplicación de API desde cero, use la plantilla **Aplicación de API de Azure** .</span><span class="sxs-lookup"><span data-stu-id="89e8d-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![Plantilla Aplicación de API en Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="89e8d-377">La elección de la plantilla de proyecto **Azure API App** equivale a elegir la plantilla **vacía** de ASP.NET 4.5.2, hacer clic en la casilla para agregar compatibilidad con Web API e instalar el paquete NuGet Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="89e8d-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="89e8d-378">Además, la plantilla agrega algún código de configuración de Swashbuckle diseñado para evitar la creación de identificadores de operación de Swagger duplicados.</span><span class="sxs-lookup"><span data-stu-id="89e8d-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="89e8d-379">Una vez que haya creado un proyecto de aplicación de API, puede implementarlo en una aplicación de API del mismo modo que el mostrado en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="89e8d-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>

