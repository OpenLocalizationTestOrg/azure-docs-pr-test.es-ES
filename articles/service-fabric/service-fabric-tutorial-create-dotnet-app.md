---
title: "Creación de una aplicación .NET para Service Fabric | Microsoft Docs"
description: "Obtenga información sobre cómo crear una aplicación con un front-end de ASP.NET Core y un back-end de servicio de confianza con estado e implementar la aplicación en un clúster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: ef50adf3af19bce494c3256308b443c8eaccdcea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="43436-103">Creación e implementación de una aplicación con un servicio de front-end de ASP.NET Core Web API y un servicio back-end con estado</span><span class="sxs-lookup"><span data-stu-id="43436-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="43436-104">Este tutorial es la primera parte de una serie.</span><span class="sxs-lookup"><span data-stu-id="43436-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="43436-105">Aprenda a crear una aplicación de Azure Service Fabric con un front-end de ASP.NET Core Web API y un servicio back-end con estado para almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="43436-105">You will learn how to create an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service to store your data.</span></span> <span data-ttu-id="43436-106">Cuando termine, tendrá una aplicación de votación con un front-end web de ASP.NET Core que guarda los resultados de una votación en un servicio back-end con estado en el clúster.</span><span class="sxs-lookup"><span data-stu-id="43436-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span> <span data-ttu-id="43436-107">Si no desea crear manualmente la aplicación de votación, puede [descargar el código fuente](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) de la aplicación terminada y pasar directamente al [Tutorial de la aplicación de ejemplo de votación](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="43436-107">If you don't want to manually create the voting application, you can [download the source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for the completed application and skip ahead to [Walk through the voting sample application](#walkthrough_anchor).</span></span>

![Diagrama de aplicaciones](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="43436-109">En la primera parte de la serie, se aprende a:</span><span class="sxs-lookup"><span data-stu-id="43436-109">In part one of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43436-110">Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado</span><span class="sxs-lookup"><span data-stu-id="43436-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="43436-111">Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado</span><span class="sxs-lookup"><span data-stu-id="43436-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="43436-112">Usar el proxy inverso para comunicarse con el servicio con estado</span><span class="sxs-lookup"><span data-stu-id="43436-112">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="43436-113">En esta serie de tutoriales, se aprende a:</span><span class="sxs-lookup"><span data-stu-id="43436-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="43436-114">Crear una aplicación de .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="43436-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="43436-115">Implementar la aplicación en un clúster remoto</span><span class="sxs-lookup"><span data-stu-id="43436-115">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="43436-116">Configurar CI/CD con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="43436-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="43436-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="43436-117">Prerequisites</span></span>
<span data-ttu-id="43436-118">Antes de empezar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="43436-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="43436-119">Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="43436-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="43436-120">[Instale Visual Studio 2017](https://www.visualstudio.com/) y las cargas de trabajo de **desarrollo de Azure** y de **desarrollo web y de ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="43436-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- <span data-ttu-id="43436-121">[Instale el SDK de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="43436-121">[Install the Service Fabric SDK](service-fabric-get-started.md)</span></span>

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="43436-122">Creación de un servicio de ASP.NET Web API como un servicio de confianza</span><span class="sxs-lookup"><span data-stu-id="43436-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="43436-123">En primer lugar, cree el front-end web de la aplicación de votación mediante ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="43436-123">First, create the web front-end of the voting application using ASP.NET Core.</span></span> <span data-ttu-id="43436-124">ASP.NET Core es un marco de desarrollo web ligero multiplataforma, que puede usar para crear modernas interfaces de usuario web y API web.</span><span class="sxs-lookup"><span data-stu-id="43436-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="43436-125">Para obtener una descripción completa de cómo se integra ASP.NET Core con Service Fabric, se recomienda fehacientemente leer el artículo [ASP.NET Core en Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="43436-125">To get a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through the [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="43436-126">De momento, puede seguir este tutorial para empezar a trabajar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="43436-126">For now, you can follow this tutorial to get started quickly.</span></span> <span data-ttu-id="43436-127">Para más información sobre ASP.NET Core, vea [Documentación de ASP.NET Core](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="43436-127">To learn more about ASP.NET Core, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="43436-128">Este tutorial se basa en las [herramientas de ASP.NET Core para Visual Studio de 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="43436-128">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="43436-129">Las herramientas de .NET Core para Visual Studio 2015 ya no se van a actualizar.</span><span class="sxs-lookup"><span data-stu-id="43436-129">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="43436-130">Inicie Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="43436-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="43436-131">Cree un proyecto con **Archivo**->**Nuevo**->**Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="43436-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="43436-132">En el cuadro de diálogo **Nuevo proyecto**, elija **Nube > Aplicación de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="43436-132">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="43436-133">Asigne el nombre **Voting** a la aplicación y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="43436-133">Name the application **Voting** and press **OK**.</span></span>

   ![Cuadro de diálogo de proyecto nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="43436-135">En la página **Nuevo servicio de Service Fabric**, elija **ASP.NET Core sin estado** y asigne el nombre de **VotingWeb** a su servicio.</span><span class="sxs-lookup"><span data-stu-id="43436-135">On the **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Selección del servicio web ASP.NET en el cuadro de diálogo de nuevo servicio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="43436-137">En la página siguiente se proporciona un conjunto de plantillas de proyecto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="43436-137">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="43436-138">Para este tutorial, elija **Web Application**.</span><span class="sxs-lookup"><span data-stu-id="43436-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="43436-140">Visual Studio crea una aplicación y un proyecto de servicio, y los muestra en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="43436-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Explorador de soluciones después de la creación de una aplicación con el servicio ASP.NET Core Web API]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a><span data-ttu-id="43436-142">Incorporación de AngularJS al servicio VotingWeb</span><span class="sxs-lookup"><span data-stu-id="43436-142">Add AngularJS to the VotingWeb service</span></span>
<span data-ttu-id="43436-143">Agregue [AngularJS](http://angularjs.org/) al servicio mediante el [soporte de Bower](/aspnet/core/client-side/bower) integrado.</span><span class="sxs-lookup"><span data-stu-id="43436-143">Add [AngularJS](http://angularjs.org/) to your service using the built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="43436-144">Abra *bower.json* y agregue las entradas angular y angular-bootstrap, y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="43436-145">Al guardar el archivo *bower.json*, Angular se instala en la carpeta *wwwroot/lib* del proyecto.</span><span class="sxs-lookup"><span data-stu-id="43436-145">Upon saving the *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="43436-146">Además, aparece dentro de la carpeta *Dependencies/Bower*.</span><span class="sxs-lookup"><span data-stu-id="43436-146">Additionally, it is listed within the *Dependencies/Bower* folder.</span></span>

### <a name="update-the-sitejs-file"></a><span data-ttu-id="43436-147">Actualización del archivo site.js</span><span class="sxs-lookup"><span data-stu-id="43436-147">Update the site.js file</span></span>
<span data-ttu-id="43436-148">Abra el archivo *wwwroot/js/site.js*.</span><span class="sxs-lookup"><span data-stu-id="43436-148">Open the *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="43436-149">Reemplace el contenido por el código de JavaScript que usan las vistas de inicio:</span><span class="sxs-lookup"><span data-stu-id="43436-149">Replace its contents with the JavaScript used by the Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-the-indexcshtml-file"></a><span data-ttu-id="43436-150">Actualización del archivo Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="43436-150">Update the Index.cshtml file</span></span>
<span data-ttu-id="43436-151">Abra el archivo *Views/Home/Index.cshtml*, la vista específica para el controlador de inicio.</span><span class="sxs-lookup"><span data-stu-id="43436-151">Open the *Views/Home/Index.cshtml* file, the view specific to the Home controller.</span></span>  <span data-ttu-id="43436-152">Reemplace su contenido por el siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-152">Replace its contents with the following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click to vote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-the-layoutcshtml-file"></a><span data-ttu-id="43436-153">Actualización del archivo _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="43436-153">Update the _Layout.cshtml file</span></span>
<span data-ttu-id="43436-154">Abra el archivo *Views/Shared/_Layout.cshtml*, el diseño predeterminado para la aplicación ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43436-154">Open the *Views/Shared/_Layout.cshtml* file, the default layout for the ASP.NET app.</span></span>  <span data-ttu-id="43436-155">Reemplace su contenido por el siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-155">Replace its contents with the following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-the-votingwebcs-file"></a><span data-ttu-id="43436-156">Actualización del archivo VotingWeb.cs</span><span class="sxs-lookup"><span data-stu-id="43436-156">Update the VotingWeb.cs file</span></span>
<span data-ttu-id="43436-157">Abra el archivo *VotingWeb.cs*, que permite crear el elemento WebHost de ASP.NET Core dentro del servicio sin estado con el servidor web de WebListener.</span><span class="sxs-lookup"><span data-stu-id="43436-157">Open the *VotingWeb.cs* file, which creates the ASP.NET Core WebHost inside the stateless service using the WebListener web server.</span></span>  <span data-ttu-id="43436-158">Agregue la directiva `using System.Net.Http;` en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="43436-158">Add the `using System.Net.Http;` directive to the top of the file.</span></span>  <span data-ttu-id="43436-159">Reemplace la función `CreateServiceInstanceListeners()` por lo siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-159">Replace the `CreateServiceInstanceListeners()` function with the following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-the-votescontrollercs-file"></a><span data-ttu-id="43436-160">Adición del archivo VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="43436-160">Add the VotesController.cs file</span></span>
<span data-ttu-id="43436-161">Agregue un controlador que defina las acciones de votación.</span><span class="sxs-lookup"><span data-stu-id="43436-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="43436-162">Haga clic con el botón derecho en la carpeta **Controladores** y seleccione **Agregar->Nuevo elemento->Clase**.</span><span class="sxs-lookup"><span data-stu-id="43436-162">Right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="43436-163">Asigne al archivo el nombre "VotesController.cs" y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="43436-163">Name the file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="43436-164">Reemplace el contenido del archivo por el siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-164">Replace the file contents with the following, then save your changes.</span></span>  <span data-ttu-id="43436-165">Más adelante, en [Actualización del archivo VotesController.cs](#updatevotecontroller_anchor), este archivo se modificará para leer y escribir los datos de votación desde el servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="43436-165">Later, in [Update the VotesController.cs file](#updatevotecontroller_anchor), this file will be modified to read and write voting data from the back-end service.</span></span>  <span data-ttu-id="43436-166">Por ahora, el controlador devuelve datos de cadena estática a la vista.</span><span class="sxs-lookup"><span data-stu-id="43436-166">For now, the controller returns static string data to the view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-the-application-locally"></a><span data-ttu-id="43436-167">Implementación y ejecución local de la aplicación</span><span class="sxs-lookup"><span data-stu-id="43436-167">Deploy and run the application locally</span></span>
<span data-ttu-id="43436-168">Ya puede continuar y ejecutar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43436-168">You can now go ahead and run the application.</span></span> <span data-ttu-id="43436-169">Presione `F5` en Visual Studio para implementar la aplicación, con el fin de depurarla.</span><span class="sxs-lookup"><span data-stu-id="43436-169">In Visual Studio, press `F5` to deploy the application for debugging.</span></span> <span data-ttu-id="43436-170">`F5` produce un error si previamente no ha abierto Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="43436-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="43436-171">La primera vez que ejecute e implemente la aplicación localmente, Visual Studio creará un clúster local para la depuración.</span><span class="sxs-lookup"><span data-stu-id="43436-171">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="43436-172">Es posible que la creación del clúster tarde un tiempo.</span><span class="sxs-lookup"><span data-stu-id="43436-172">Cluster creation may take some time.</span></span> <span data-ttu-id="43436-173">El estado de creación del clúster se muestra en la ventana de salida de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43436-173">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="43436-174">En este momento, la aplicación web se debe parecer a esta:</span><span class="sxs-lookup"><span data-stu-id="43436-174">At this point, your web app should look like this:</span></span>

![Front-end de ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="43436-176">Para detener la depuración de la aplicación, vuelva a Visual Studio y presione **Mayús+F5**.</span><span class="sxs-lookup"><span data-stu-id="43436-176">To stop debugging the application, go back to Visual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-to-your-application"></a><span data-ttu-id="43436-177">Adición de un servicio back-end con estado a la aplicación</span><span class="sxs-lookup"><span data-stu-id="43436-177">Add a stateful back-end service to your application</span></span>
<span data-ttu-id="43436-178">Ahora que tenemos un servicio de ASP.NET Web API en ejecución en nuestra aplicación, sigamos adelante y agreguemos un servicio de confianza con estado para almacenar algunos datos en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="43436-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service to store some data in our application.</span></span>

<span data-ttu-id="43436-179">Service Fabric permite almacenar de forma coherente y confiable su estado justo dentro de su servicio mediante Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="43436-179">Service Fabric allows you to consistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="43436-180">Reliable Collections es un conjunto de clases de colecciones de alta disponibilidad y confiabilidad que le resultará familiar a cualquiera que haya usado colecciones de C#.</span><span class="sxs-lookup"><span data-stu-id="43436-180">Reliable collections are a set of highly available and reliable collection classes that are familiar to anyone who has used C# collections.</span></span>

<span data-ttu-id="43436-181">En este tutorial creará un servicio, que almacena un valor de contador en una colección de confianza.</span><span class="sxs-lookup"><span data-stu-id="43436-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="43436-182">En el Explorador de soluciones, haga clic con el botón derecho en **Servicios**, en el proyecto de aplicación y seleccione **Agregar > Nuevo servicio de Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="43436-182">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Incorporación de un nuevo servicio a una aplicación existente](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="43436-184">En el cuadro de diálogo **Nuevo servicio de Service Fabric**, elija **ASP.NET Core con estado** y asigne el nombre de **VotingData** al servicio y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="43436-184">In the **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name the service **VotingData** and press **OK**.</span></span>

    ![Cuadro de diálogo de servicio nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="43436-186">Una vez creado el proyecto de servicio, tendrá dos servicios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="43436-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="43436-187">Mientras continúa la creación de la aplicación, puede agregar más servicios de la misma forma.</span><span class="sxs-lookup"><span data-stu-id="43436-187">As you continue to build your application, you can add more services in the same way.</span></span> <span data-ttu-id="43436-188">Cada uno puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="43436-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="43436-189">En la página siguiente se proporciona un conjunto de plantillas de proyecto ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="43436-189">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="43436-190">Para este tutorial, elija **API Web**.</span><span class="sxs-lookup"><span data-stu-id="43436-190">For this tutorial, choose **Web API**.</span></span>

    ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="43436-192">Visual Studio crea un proyecto de servicio y lo muestra en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="43436-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Explorador de soluciones](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-the-votedatacontrollercs-file"></a><span data-ttu-id="43436-194">Adición del archivo VoteDataController.cs</span><span class="sxs-lookup"><span data-stu-id="43436-194">Add the VoteDataController.cs file</span></span>

<span data-ttu-id="43436-195">En el proyecto **VotingData** haga clic con el botón derecho en la carpeta **Controladores** y seleccione **Agregar->Nuevo elemento->Clase**.</span><span class="sxs-lookup"><span data-stu-id="43436-195">In the **VotingData** project right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="43436-196">Asigne al archivo el nombre "VoteDataController.cs" y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="43436-196">Name the file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="43436-197">Reemplace el contenido del archivo por el siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-197">Replace the file contents with the following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-the-services"></a><span data-ttu-id="43436-198">Conexión de los servicios</span><span class="sxs-lookup"><span data-stu-id="43436-198">Connect the services</span></span>
<span data-ttu-id="43436-199">En este paso se van a conectar los dos servicios y hacer que la aplicación web de front-end obtenga y configure la información de votación del servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="43436-199">In this next step, we will connect the two services and make the front-end Web application get and set voting information from the back-end service.</span></span>

<span data-ttu-id="43436-200">Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables.</span><span class="sxs-lookup"><span data-stu-id="43436-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="43436-201">Dentro de una única aplicación, es posible que tenga servicios que sean accesibles a través de TCP.</span><span class="sxs-lookup"><span data-stu-id="43436-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="43436-202">Puede haber también otros servicios que podrían estar accesibles a través de una API de REST de HTTP e incluso otros servicios que pueden estar accesibles a través de sockets web.</span><span class="sxs-lookup"><span data-stu-id="43436-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="43436-203">Para más información sobre las opciones disponibles y sus inconvenientes, consulte [Conexión y comunicación con servicios en Service Fabric](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="43436-203">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="43436-204">En este tutorial, vamos a utilizar [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="43436-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a><span data-ttu-id="43436-205">Actualización del archivo VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="43436-205">Update the VotesController.cs file</span></span>
<span data-ttu-id="43436-206">En el proyecto **VotingWeb**, abra el archivo *Controllers/VotesController.cs*.</span><span class="sxs-lookup"><span data-stu-id="43436-206">In the **VotingWeb** project, open the *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="43436-207">Reemplace el contenido de la definición de clase `VotesController` por el siguiente y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="43436-207">Replace the `VotesController` class definition contents with the following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="43436-208">Tutorial de la aplicación de ejemplo de votación</span><span class="sxs-lookup"><span data-stu-id="43436-208">Walk through the voting sample application</span></span>
<span data-ttu-id="43436-209">La aplicación de votación consta de dos servicios:</span><span class="sxs-lookup"><span data-stu-id="43436-209">The voting application consists of two services:</span></span>
- <span data-ttu-id="43436-210">Servicio front-end web (VotingWeb): front-end web de ASP.NET Core, que ofrece servicio a la página web y expone API web para comunicarse con el servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="43436-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="43436-211">Servicio back-end (VotingData): servicio web de ASP.NET Core, que expone una API para almacenar los resultados de una votación en un diccionario confiable que se conserva en el disco.</span><span class="sxs-lookup"><span data-stu-id="43436-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![Diagrama de la aplicación](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="43436-213">Al votar en la aplicación, se producen los eventos siguientes:</span><span class="sxs-lookup"><span data-stu-id="43436-213">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="43436-214">JavaScript envía la solicitud de votación a la API web del servicio front-end web como una solicitud HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="43436-214">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="43436-215">El servicio front-end web usa un proxy para localizar y reenviar una solicitud HTTP PUT al servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="43436-215">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="43436-216">El servicio back-end recibe la solicitud entrante y almacena el resultado actualizado en un diccionario confiable, que se replica en varios nodos del clúster y se conserva en el disco.</span><span class="sxs-lookup"><span data-stu-id="43436-216">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="43436-217">Todos los datos de la aplicación se almacenan en el clúster, por lo que no se necesita una base de datos.</span><span class="sxs-lookup"><span data-stu-id="43436-217">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="43436-218">Depurar en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43436-218">Debug in Visual Studio</span></span>
<span data-ttu-id="43436-219">Cuando se depura una aplicación en Visual Studio, se usa un clúster de desarrollo de Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="43436-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="43436-220">Tiene la opción de ajustar la experiencia de depuración a su escenario.</span><span class="sxs-lookup"><span data-stu-id="43436-220">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="43436-221">En esta aplicación, almacenamos los datos en nuestro servicio back-end mediante un diccionario confiable.</span><span class="sxs-lookup"><span data-stu-id="43436-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="43436-222">Visual Studio quita la aplicación de forma predeterminada cuando se detiene el depurador.</span><span class="sxs-lookup"><span data-stu-id="43436-222">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="43436-223">Cuando se quita la aplicación, los datos del servicio back-end también se quitan.</span><span class="sxs-lookup"><span data-stu-id="43436-223">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="43436-224">Para conservar los datos entre sesiones de depuración, puede cambiar el **modo de depuración de la aplicación** como una propiedad del proyecto **Voting** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43436-224">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="43436-225">Para ver lo que ocurre en el código, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="43436-225">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="43436-226">Abra el archivo **VotesController.cs** y establezca un punto de interrupción en el método **Put** (línea 47) de la API web. Puede buscar el archivo en el Explorador de soluciones de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="43436-226">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="43436-227">Abra el archivo **VoteDataController.cs** y establezca un punto de interrupción en el método **Put** (línea 50) de esta API web.</span><span class="sxs-lookup"><span data-stu-id="43436-227">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="43436-228">Vuelva al explorador y haga clic en una opción de votación o agregue una nueva opción de votación.</span><span class="sxs-lookup"><span data-stu-id="43436-228">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="43436-229">Alcanzará el primer punto de interrupción del controlador de API del front-end web.</span><span class="sxs-lookup"><span data-stu-id="43436-229">You hit the first breakpoint in the web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="43436-230">Aquí es donde el código JavaScript del explorador envía una solicitud al controlador de API web del servicio front-end.</span><span class="sxs-lookup"><span data-stu-id="43436-230">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![Incorporación del servicio front-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="43436-232">Primero construimos la dirección URL para el valor de ReverseProxy para nuestro servicio back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="43436-232">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="43436-233">A continuación, enviamos la solicitud PUT de HTTP para ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="43436-233">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="43436-234">Por último, devolvemos la respuesta desde el servicio back-end al cliente **(3)**.</span><span class="sxs-lookup"><span data-stu-id="43436-234">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="43436-235">Pulse **F5** para continuar.</span><span class="sxs-lookup"><span data-stu-id="43436-235">Press **F5** to continue</span></span>
    1. <span data-ttu-id="43436-236">Ya está en el punto de interrupción del servicio back-end.</span><span class="sxs-lookup"><span data-stu-id="43436-236">You are now at the break point in the back-end service.</span></span>
    
    ![Incorporación del servicio back-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="43436-238">En la primera línea del método **(1)** usamos `StateManager` para obtener o agregar un diccionario confiable denominado `counts`.</span><span class="sxs-lookup"><span data-stu-id="43436-238">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="43436-239">Todas las interacciones con valores de un diccionario confiable requieren una transacción. Esta instrucción using **(2)** crea dicha transacción.</span><span class="sxs-lookup"><span data-stu-id="43436-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="43436-240">Después, en la transacción, actualizamos el valor de la tecla correspondiente para la opción de votación y la operación se confirma **(3)**.</span><span class="sxs-lookup"><span data-stu-id="43436-240">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="43436-241">Una vez que se devuelve el método Commit, los datos se actualizan en el diccionario y se replican en otros nodos del clúster.</span><span class="sxs-lookup"><span data-stu-id="43436-241">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="43436-242">Los datos ahora están almacenados de forma segura en el clúster y el servicio back-end puede conmutar por error a otros nodos, mientras sigue teniendo los datos disponibles.</span><span class="sxs-lookup"><span data-stu-id="43436-242">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="43436-243">Pulse **F5** para continuar.</span><span class="sxs-lookup"><span data-stu-id="43436-243">Press **F5** to continue</span></span>

<span data-ttu-id="43436-244">Para detener la sesión de depuración, pulse **Maýus+F5**.</span><span class="sxs-lookup"><span data-stu-id="43436-244">To stop the debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="43436-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="43436-245">Next steps</span></span>
<span data-ttu-id="43436-246">En esta parte del tutorial, ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="43436-246">In this part of the tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="43436-247">Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado</span><span class="sxs-lookup"><span data-stu-id="43436-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="43436-248">Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado</span><span class="sxs-lookup"><span data-stu-id="43436-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="43436-249">Usar el proxy inverso para comunicarse con el servicio con estado</span><span class="sxs-lookup"><span data-stu-id="43436-249">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="43436-250">Avance hasta el siguiente tutorial:</span><span class="sxs-lookup"><span data-stu-id="43436-250">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="43436-251">Implementación de la aplicación en Azure</span><span class="sxs-lookup"><span data-stu-id="43436-251">Deploy the application to Azure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)