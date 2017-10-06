---
title: "una aplicación .NET para Service Fabric aaaCreate | Documentos de Microsoft"
description: "Conozca cómo toocreate una aplicación con un front-end ASP.NET Core y un confiable servicio back-end con estado e implementar clústeres de tooa aplicación Hola."
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
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="4216f-103">Creación e implementación de una aplicación con un servicio de front-end de ASP.NET Core Web API y un servicio back-end con estado</span><span class="sxs-lookup"><span data-stu-id="4216f-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="4216f-104">Este tutorial es la primera parte de una serie.</span><span class="sxs-lookup"><span data-stu-id="4216f-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="4216f-105">Obtendrá información sobre cómo toocreate una aplicación de Azure Service Fabric con una parte delantera de la API Web de ASP.NET Core finalizar y un servicio back-end con estado toostore los datos.</span><span class="sxs-lookup"><span data-stu-id="4216f-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="4216f-106">Cuando haya terminado, tiene una aplicación con un front-end que guarda los resultados de la votos en un servicio back-end con estado en el clúster de hello web de ASP.NET Core derecho a voto.</span><span class="sxs-lookup"><span data-stu-id="4216f-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="4216f-107">Crear hello votos de aplicación, se puede realizar si no desea toomanually [descargar código fuente de hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) para hello completado aplicación y pase demasiado[guiarán a través de los votos de la aplicación de ejemplo de Hola](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="4216f-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagrama de aplicaciones](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="4216f-109">En la primera parte de la serie de hello, aprenderá cómo:</span><span class="sxs-lookup"><span data-stu-id="4216f-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4216f-110">Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado</span><span class="sxs-lookup"><span data-stu-id="4216f-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="4216f-111">Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado</span><span class="sxs-lookup"><span data-stu-id="4216f-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="4216f-112">Usar Hola proxy inverso toocommunicate con servicio con estado Hola</span><span class="sxs-lookup"><span data-stu-id="4216f-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="4216f-113">En esta serie de tutoriales, se aprende a:</span><span class="sxs-lookup"><span data-stu-id="4216f-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="4216f-114">Crear una aplicación de .NET Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4216f-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="4216f-115">Implementar el clúster remoto de hello aplicación tooa</span><span class="sxs-lookup"><span data-stu-id="4216f-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="4216f-116">Configurar CI/CD con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="4216f-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="4216f-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4216f-117">Prerequisites</span></span>
<span data-ttu-id="4216f-118">Antes de empezar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="4216f-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="4216f-119">Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="4216f-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="4216f-120">[Instalar Visual Studio de 2017](https://www.visualstudio.com/) e instalar hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4216f-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="4216f-121">Instalar Hola SDK del servicio de Fabric</span><span class="sxs-lookup"><span data-stu-id="4216f-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="4216f-122">Creación de un servicio de ASP.NET Web API como un servicio de confianza</span><span class="sxs-lookup"><span data-stu-id="4216f-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="4216f-123">En primer lugar, cree web Hola front-end de hello votos de aplicación mediante ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4216f-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="4216f-124">Núcleo de ASP.NET es un marco de desarrollo web ligera y multiplataforma que puede usar la interfaz de usuario de web moderna toocreate y las API web.</span><span class="sxs-lookup"><span data-stu-id="4216f-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="4216f-125">tooget una descripción completa de cómo se integra ASP.NET Core con Service Fabric, se recomienda encarecidamente leer hello [ASP.NET Core en servicios de Service Fabric confiable](service-fabric-reliable-services-communication-aspnetcore.md) artículo.</span><span class="sxs-lookup"><span data-stu-id="4216f-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="4216f-126">Por ahora, puede seguir este tutorial tooget a trabajar rápidamente.</span><span class="sxs-lookup"><span data-stu-id="4216f-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="4216f-127">toolearn más información sobre ASP.NET Core, vea hello [documentación principal de ASP.NET](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="4216f-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="4216f-128">Este tutorial se basa en hello [ASP.NET Core tools para Visual Studio de 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="4216f-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="4216f-129">herramientas de .NET Core Hola para Visual Studio 2015 ya no se están actualizando.</span><span class="sxs-lookup"><span data-stu-id="4216f-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="4216f-130">Inicie Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="4216f-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="4216f-131">Cree un proyecto con **Archivo**->**Nuevo**->**Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="4216f-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="4216f-132">Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4216f-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="4216f-133">Nombre de la aplicación hello **votación** y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4216f-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Cuadro de diálogo de proyecto nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="4216f-135">En hello **nuevo servicio de Fabric** página, elija **sin estado ASP.NET Core**y el nombre de su servicio **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="4216f-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![Elegir el servicio web ASP.NET en el cuadro de diálogo de hello nuevo servicio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="4216f-137">página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="4216f-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="4216f-138">Para este tutorial, elija **Web Application**.</span><span class="sxs-lookup"><span data-stu-id="4216f-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="4216f-140">Visual Studio crea una aplicación y un proyecto de servicio, y los muestra en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="4216f-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Explorador de soluciones después de la creación de una aplicación con el servicio ASP.NET Core Web API]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="4216f-142">Agregar servicio de AngularJS toohello VotingWeb</span><span class="sxs-lookup"><span data-stu-id="4216f-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="4216f-143">Agregar [AngularJS](http://angularjs.org/) servicio tooyour mediante integradas de hello [Bower compatibilidad](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="4216f-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="4216f-144">Abra *bower.json* y agregue las entradas angular y angular-bootstrap, y guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="4216f-145">Al guardar hello *bower.json* archivo, Angular se instala en el proyecto *wwwroot/lib* carpeta.</span><span class="sxs-lookup"><span data-stu-id="4216f-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="4216f-146">Además, se incluye dentro de hello *dependencias/Bower* carpeta.</span><span class="sxs-lookup"><span data-stu-id="4216f-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="4216f-147">Archivo de actualización hello site.js</span><span class="sxs-lookup"><span data-stu-id="4216f-147">Update hello site.js file</span></span>
<span data-ttu-id="4216f-148">Abra hello *wwwroot/js/site.js* archivo.</span><span class="sxs-lookup"><span data-stu-id="4216f-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="4216f-149">Reemplace su contenido con hello JavaScript utilizado en las vistas de hello principal:</span><span class="sxs-lookup"><span data-stu-id="4216f-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="4216f-150">Archivo de actualización hello Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4216f-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="4216f-151">Abra hello *Views/Home/Index.cshtml* archivo, Hola vista específicos del controlador principal de toohello.</span><span class="sxs-lookup"><span data-stu-id="4216f-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="4216f-152">Reemplazar su contenido con siguiente hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-152">Replace its contents with hello following, then save your changes.</span></span>

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
                        Click toovote
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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="4216f-153">Archivo de actualización hello _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="4216f-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="4216f-154">Abra hello *Views/Shared/_Layout.cshtml* archivo, el diseño predeterminado de hello para la aplicación ASP.NET de hello.</span><span class="sxs-lookup"><span data-stu-id="4216f-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="4216f-155">Reemplazar su contenido con siguiente hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="4216f-156">Archivo de actualización hello VotingWeb.cs</span><span class="sxs-lookup"><span data-stu-id="4216f-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="4216f-157">Abra hello *VotingWeb.cs* archivo, que crea Hola ASP.NET Core WebHost dentro de servicio sin estado Hola con servidor web de hello WebListener.</span><span class="sxs-lookup"><span data-stu-id="4216f-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="4216f-158">Agregar hello `using System.Net.Http;` parte superior de la directiva toohello del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="4216f-159">Reemplace hello `CreateServiceInstanceListeners()` funcionando con siguiente hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="4216f-160">Agregar archivo de hello VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="4216f-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="4216f-161">Agregue un controlador que defina las acciones de votación.</span><span class="sxs-lookup"><span data-stu-id="4216f-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="4216f-162">Haga doble clic en hello **controladores** carpeta, a continuación, seleccione **Agregar -> nuevo elemento -> clase**.</span><span class="sxs-lookup"><span data-stu-id="4216f-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="4216f-163">Nombre de archivo de hello "VotesController.cs" y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="4216f-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="4216f-164">Reemplace el contenido del archivo Hola por siguiente de hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="4216f-165">Más adelante, en [archivo de actualización hello VotesController.cs](#updatevotecontroller_anchor), este archivo se tooread modificado y escribir datos de votos de servicio de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="4216f-166">Por ahora, el controlador de hello devuelve la vista de toohello de datos de cadena estática.</span><span class="sxs-lookup"><span data-stu-id="4216f-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="4216f-167">Implementar y ejecutar la aplicación hello localmente</span><span class="sxs-lookup"><span data-stu-id="4216f-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="4216f-168">Ahora puede seguir adelante y ejecutar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="4216f-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="4216f-169">En Visual Studio, presione `F5` toodeploy aplicación de hello para la depuración.</span><span class="sxs-lookup"><span data-stu-id="4216f-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="4216f-170">`F5` produce un error si previamente no ha abierto Visual Studio como **administrador**.</span><span class="sxs-lookup"><span data-stu-id="4216f-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="4216f-171">Hola la primera vez que se ejecute e implementa aplicación de hello localmente, Visual Studio crea un clúster local para la depuración.</span><span class="sxs-lookup"><span data-stu-id="4216f-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="4216f-172">Es posible que la creación del clúster tarde un tiempo.</span><span class="sxs-lookup"><span data-stu-id="4216f-172">Cluster creation may take some time.</span></span> <span data-ttu-id="4216f-173">estado de creación de clúster de Hola se muestra en la ventana de salida de Visual Studio de hello.</span><span class="sxs-lookup"><span data-stu-id="4216f-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="4216f-174">En este momento, la aplicación web se debe parecer a esta:</span><span class="sxs-lookup"><span data-stu-id="4216f-174">At this point, your web app should look like this:</span></span>

![Front-end de ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="4216f-176">toostop depurar la aplicación hello, vuelva atrás tooVisual Studio y presione **MAYÚS+F5**.</span><span class="sxs-lookup"><span data-stu-id="4216f-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="4216f-177">Agregar una aplicación de servicio de back-end con estado tooyour</span><span class="sxs-lookup"><span data-stu-id="4216f-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="4216f-178">Ahora que tenemos un servicio de API Web de ASP.NET que se ejecuta en nuestra aplicación, sigamos adelante y agregue algunos datos de un servicio confiable con estado toostore en nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="4216f-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="4216f-179">Service Fabric permite tooconsistently y confiable almacenar los datos directamente dentro de su servicio mediante el uso de colecciones confiables.</span><span class="sxs-lookup"><span data-stu-id="4216f-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="4216f-180">Colecciones de confianza son un conjunto de clases de colección altamente disponible y confiable que están familiarizado tooanyone que ha utilizado las colecciones de C#.</span><span class="sxs-lookup"><span data-stu-id="4216f-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="4216f-181">En este tutorial creará un servicio, que almacena un valor de contador en una colección de confianza.</span><span class="sxs-lookup"><span data-stu-id="4216f-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="4216f-182">En el Explorador de soluciones, haga clic en **servicios** en Hola proyecto de aplicación y elija **Agregar > nuevo servicio de Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4216f-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Agregar una nueva aplicación existente de tooan de servicio](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="4216f-184">Hola **nuevo servicio de Fabric** cuadro de diálogo, elija **Stateful ASP.NET Core**y el servicio de nombres de hello **VotingData** y presione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4216f-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Cuadro de diálogo de servicio nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="4216f-186">Una vez creado el proyecto de servicio, tendrá dos servicios en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4216f-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="4216f-187">A medida que continúa toobuild la aplicación, puede agregar más servicios Hola igual.</span><span class="sxs-lookup"><span data-stu-id="4216f-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="4216f-188">Cada uno puede tener versiones y actualizaciones independientes.</span><span class="sxs-lookup"><span data-stu-id="4216f-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="4216f-189">página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto.</span><span class="sxs-lookup"><span data-stu-id="4216f-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="4216f-190">Para este tutorial, elija **API Web**.</span><span class="sxs-lookup"><span data-stu-id="4216f-190">For this tutorial, choose **Web API**.</span></span>

    ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="4216f-192">Visual Studio crea un proyecto de servicio y lo muestra en el Explorador de soluciones.</span><span class="sxs-lookup"><span data-stu-id="4216f-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Explorador de soluciones](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="4216f-194">Agregar archivo de hello VoteDataController.cs</span><span class="sxs-lookup"><span data-stu-id="4216f-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="4216f-195">Hola **VotingData** menú contextual del proyecto en hello **controladores** carpeta, a continuación, seleccione **Agregar -> nuevo elemento -> clase**.</span><span class="sxs-lookup"><span data-stu-id="4216f-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="4216f-196">Nombre de archivo de hello "VoteDataController.cs" y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="4216f-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="4216f-197">Reemplace el contenido del archivo Hola por siguiente de hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="4216f-198">Conectar servicios de Hola</span><span class="sxs-lookup"><span data-stu-id="4216f-198">Connect hello services</span></span>
<span data-ttu-id="4216f-199">En este paso, agregaremos Hola dos servicios de conexión y hacer Hola front-end Web aplicación get y set votos información de servicio de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="4216f-200">Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables.</span><span class="sxs-lookup"><span data-stu-id="4216f-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="4216f-201">Dentro de una única aplicación, es posible que tenga servicios que sean accesibles a través de TCP.</span><span class="sxs-lookup"><span data-stu-id="4216f-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="4216f-202">Puede haber también otros servicios que podrían estar accesibles a través de una API de REST de HTTP e incluso otros servicios que pueden estar accesibles a través de sockets web.</span><span class="sxs-lookup"><span data-stu-id="4216f-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="4216f-203">Para obtener información sobre opciones de hello disponibles y los inconvenientes de hello, consulte [comunicarse con servicios](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="4216f-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="4216f-204">En este tutorial, vamos a utilizar [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="4216f-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="4216f-205">Archivo de actualización hello VotesController.cs</span><span class="sxs-lookup"><span data-stu-id="4216f-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="4216f-206">Hola **VotingWeb** proyecto, abra hello *Controllers/VotesController.cs* archivo.</span><span class="sxs-lookup"><span data-stu-id="4216f-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="4216f-207">Reemplace hello `VotesController` clase contenido definición por siguiente hello, a continuación, guarde los cambios.</span><span class="sxs-lookup"><span data-stu-id="4216f-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="4216f-208">Recorrer Hola votos de aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="4216f-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="4216f-209">Hola votos aplicación consta de dos servicios:</span><span class="sxs-lookup"><span data-stu-id="4216f-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="4216f-210">Servicio de front-end (VotingWeb) Web: An ASP.NET Core servicio front-end, que sirve de página web de Hola y expone web toocommunicate de API con el servicio back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="4216f-211">Servicio de back-end (VotingData)-servicio de web de un núcleo de ASP.NET, que expone un voto de hello API toostore da como resultado un diccionario confiable se conserva en el disco.</span><span class="sxs-lookup"><span data-stu-id="4216f-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagrama de aplicaciones](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="4216f-213">Eventos se producen cuando votar Hola Hola de aplicaciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="4216f-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="4216f-214">JavaScript envía API web solicitud toohello para hello voto en el servicio front-end web de hello como una solicitud PUT de HTTP.</span><span class="sxs-lookup"><span data-stu-id="4216f-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="4216f-215">servicio front-end de Hello web utiliza un proxy toolocate y reenviar un servicio de back-end de toohello de solicitud HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="4216f-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="4216f-216">servicio de back-end de Hello toma la solicitud entrante de Hola y Hola almacenes actualiza resultado en un diccionario confiable, que obtiene toomultiple replicada nodos en clúster de Hola y se conserva en el disco.</span><span class="sxs-lookup"><span data-stu-id="4216f-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="4216f-217">Datos de todas las aplicación Hola se almacenan en el clúster de hello, por lo que no se necesita ninguna base de datos.</span><span class="sxs-lookup"><span data-stu-id="4216f-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="4216f-218">Depurar en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4216f-218">Debug in Visual Studio</span></span>
<span data-ttu-id="4216f-219">Cuando se depura una aplicación en Visual Studio, se usa un clúster de desarrollo de Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="4216f-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="4216f-220">Tener Hola opción tooadjust su escenario de tooyour de experiencia de depuración.</span><span class="sxs-lookup"><span data-stu-id="4216f-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="4216f-221">En esta aplicación, almacenamos los datos en nuestro servicio back-end mediante un diccionario confiable.</span><span class="sxs-lookup"><span data-stu-id="4216f-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="4216f-222">Visual Studio quita aplicación hello de forma predeterminada cuando se detiene el depurador Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="4216f-223">Quitar aplicación hello hace que los datos de hello en hello back-end puede quitar tooalso de servicio.</span><span class="sxs-lookup"><span data-stu-id="4216f-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="4216f-224">datos de hello toopersist entre las sesiones de depuración, puede cambiar hello **modo de depuración de la aplicación** como una propiedad en hello **votación** proyecto en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4216f-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="4216f-225">toolook en lo que sucede en el código de hello, Hola completa pasos:</span><span class="sxs-lookup"><span data-stu-id="4216f-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="4216f-226">Hola abierto **VotesController.cs** de archivos y establecer un punto de interrupción en web Hola API **colocar** método (línea 47): puede buscar archivo Hola Hola el Explorador de soluciones en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4216f-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="4216f-227">Abra hello **VoteDataController.cs** de archivos y establezca un punto de interrupción en esta API de web **colocar** método (línea 50).</span><span class="sxs-lookup"><span data-stu-id="4216f-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="4216f-228">Volver atrás toohello explorador y haga clic en una opción de votación o agregue una nueva opción de voto.</span><span class="sxs-lookup"><span data-stu-id="4216f-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="4216f-229">Se alcanza el primer punto de interrupción hello en el controlador de api de hello web front-end.</span><span class="sxs-lookup"><span data-stu-id="4216f-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="4216f-230">Esto es donde hello JavaScript en el Explorador de hello envía un controlador de API web de solicitud toohello en el servicio front-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Incorporación del servicio front-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="4216f-232">Primero creamos Hola URL toohello ReverseProxy para nuestro servicio back-end **(1)**.</span><span class="sxs-lookup"><span data-stu-id="4216f-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="4216f-233">A continuación, enviamos Hola solicitud PUT de HTTP toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="4216f-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="4216f-234">Por último, hello se devuelva la respuesta de Hola de hello servicio back-end toohello cliente **(3)**.</span><span class="sxs-lookup"><span data-stu-id="4216f-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="4216f-235">Presione **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="4216f-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="4216f-236">Ya estás hello en punto de interrupción en el servicio de back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Incorporación del servicio back-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="4216f-238">Primera línea de hello en método hello **(1)** , usamos hello `StateManager` tooget o agregar un diccionario confiable denominado `counts`.</span><span class="sxs-lookup"><span data-stu-id="4216f-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="4216f-239">Todas las interacciones con valores de un diccionario confiable requieren una transacción. Esta instrucción using **(2)** crea dicha transacción.</span><span class="sxs-lookup"><span data-stu-id="4216f-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="4216f-240">En transacciones de hello, actualizamos, a continuación, valor de Hola de clave relevante Hola Hola votar la opción y confirmaciones Hola operación **(3)**.</span><span class="sxs-lookup"><span data-stu-id="4216f-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="4216f-241">Una vez Hola confirme método devuelve, Hola datos se actualizan en el diccionario de Hola y replican tooother nodos de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="4216f-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="4216f-242">datos de Hello ahora se almacenan de forma segura en clúster de Hola y servicio back-end de hello puede conmutar por error nodos tooother, sigue teniendo datos Hola disponibles.</span><span class="sxs-lookup"><span data-stu-id="4216f-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="4216f-243">Presione **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="4216f-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="4216f-244">Hola toostop depuración de sesión, presione **MAYÚS+F5**.</span><span class="sxs-lookup"><span data-stu-id="4216f-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="4216f-245">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4216f-245">Next steps</span></span>
<span data-ttu-id="4216f-246">En esta parte del tutorial de hello, ha aprendido cómo:</span><span class="sxs-lookup"><span data-stu-id="4216f-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4216f-247">Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado</span><span class="sxs-lookup"><span data-stu-id="4216f-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="4216f-248">Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado</span><span class="sxs-lookup"><span data-stu-id="4216f-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="4216f-249">Usar Hola proxy inverso toocommunicate con servicio con estado Hola</span><span class="sxs-lookup"><span data-stu-id="4216f-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="4216f-250">Tutorial de antemano toohello siguiente:</span><span class="sxs-lookup"><span data-stu-id="4216f-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4216f-251">Implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="4216f-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
