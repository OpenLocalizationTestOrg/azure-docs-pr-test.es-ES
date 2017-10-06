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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Creación e implementación de una aplicación con un servicio de front-end de ASP.NET Core Web API y un servicio back-end con estado
Este tutorial es la primera parte de una serie.  Obtendrá información sobre cómo toocreate una aplicación de Azure Service Fabric con una parte delantera de la API Web de ASP.NET Core finalizar y un servicio back-end con estado toostore los datos. Cuando haya terminado, tiene una aplicación con un front-end que guarda los resultados de la votos en un servicio back-end con estado en el clúster de hello web de ASP.NET Core derecho a voto. Crear hello votos de aplicación, se puede realizar si no desea toomanually [descargar código fuente de hello](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) para hello completado aplicación y pase demasiado[guiarán a través de los votos de la aplicación de ejemplo de Hola](#walkthrough_anchor).

![Diagrama de aplicaciones](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

En la primera parte de la serie de hello, aprenderá cómo:

> [!div class="checklist"]
> * Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado
> * Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado
> * Usar Hola proxy inverso toocommunicate con servicio con estado Hola

En esta serie de tutoriales, se aprende a:
> [!div class="checklist"]
> * Crear una aplicación de .NET Service Fabric
> * [Implementar el clúster remoto de hello aplicación tooa](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [Configurar CI/CD con Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar este tutorial:
- Si no tiene ninguna suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Instalar Visual Studio de 2017](https://www.visualstudio.com/) e instalar hello **desarrollo Azure** y **ASP.NET y desarrollo web** las cargas de trabajo.
- [Instalar Hola SDK del servicio de Fabric](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Creación de un servicio de ASP.NET Web API como un servicio de confianza
En primer lugar, cree web Hola front-end de hello votos de aplicación mediante ASP.NET Core. Núcleo de ASP.NET es un marco de desarrollo web ligera y multiplataforma que puede usar la interfaz de usuario de web moderna toocreate y las API web. tooget una descripción completa de cómo se integra ASP.NET Core con Service Fabric, se recomienda encarecidamente leer hello [ASP.NET Core en servicios de Service Fabric confiable](service-fabric-reliable-services-communication-aspnetcore.md) artículo. Por ahora, puede seguir este tutorial tooget a trabajar rápidamente. toolearn más información sobre ASP.NET Core, vea hello [documentación principal de ASP.NET](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Este tutorial se basa en hello [ASP.NET Core tools para Visual Studio de 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). herramientas de .NET Core Hola para Visual Studio 2015 ya no se están actualizando.

1. Inicie Visual Studio como **administrador**.

2. Cree un proyecto con **Archivo**->**Nuevo**->**Proyecto**.

3. Hola **nuevo proyecto** cuadro de diálogo, elija **en la nube > aplicación de servicio de Fabric**.

4. Nombre de la aplicación hello **votación** y presione **Aceptar**.

   ![Cuadro de diálogo de proyecto nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. En hello **nuevo servicio de Fabric** página, elija **sin estado ASP.NET Core**y el nombre de su servicio **VotingWeb**.
   
   ![Elegir el servicio web ASP.NET en el cuadro de diálogo de hello nuevo servicio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto. Para este tutorial, elija **Web Application**. 
   
   ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio crea una aplicación y un proyecto de servicio, y los muestra en el Explorador de soluciones.

   ![Explorador de soluciones después de la creación de una aplicación con el servicio ASP.NET Core Web API]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>Agregar servicio de AngularJS toohello VotingWeb
Agregar [AngularJS](http://angularjs.org/) servicio tooyour mediante integradas de hello [Bower compatibilidad](/aspnet/core/client-side/bower). Abra *bower.json* y agregue las entradas angular y angular-bootstrap, y guarde los cambios.

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
Al guardar hello *bower.json* archivo, Angular se instala en el proyecto *wwwroot/lib* carpeta. Además, se incluye dentro de hello *dependencias/Bower* carpeta.

### <a name="update-hello-sitejs-file"></a>Archivo de actualización hello site.js
Abra hello *wwwroot/js/site.js* archivo.  Reemplace su contenido con hello JavaScript utilizado en las vistas de hello principal:

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

### <a name="update-hello-indexcshtml-file"></a>Archivo de actualización hello Index.cshtml
Abra hello *Views/Home/Index.cshtml* archivo, Hola vista específicos del controlador principal de toohello.  Reemplazar su contenido con siguiente hello, a continuación, guarde los cambios.

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

### <a name="update-hello-layoutcshtml-file"></a>Archivo de actualización hello _Layout.cshtml
Abra hello *Views/Shared/_Layout.cshtml* archivo, el diseño predeterminado de hello para la aplicación ASP.NET de hello.  Reemplazar su contenido con siguiente hello, a continuación, guarde los cambios.

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

### <a name="update-hello-votingwebcs-file"></a>Archivo de actualización hello VotingWeb.cs
Abra hello *VotingWeb.cs* archivo, que crea Hola ASP.NET Core WebHost dentro de servicio sin estado Hola con servidor web de hello WebListener.  Agregar hello `using System.Net.Http;` parte superior de la directiva toohello del archivo de Hola.  Reemplace hello `CreateServiceInstanceListeners()` funcionando con siguiente hello, a continuación, guarde los cambios.

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

### <a name="add-hello-votescontrollercs-file"></a>Agregar archivo de hello VotesController.cs
Agregue un controlador que defina las acciones de votación. Haga doble clic en hello **controladores** carpeta, a continuación, seleccione **Agregar -> nuevo elemento -> clase**.  Nombre de archivo de hello "VotesController.cs" y haga clic en **agregar**.  Reemplace el contenido del archivo Hola por siguiente de hello, a continuación, guarde los cambios.  Más adelante, en [archivo de actualización hello VotesController.cs](#updatevotecontroller_anchor), este archivo se tooread modificado y escribir datos de votos de servicio de back-end de Hola.  Por ahora, el controlador de hello devuelve la vista de toohello de datos de cadena estática.

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



### <a name="deploy-and-run-hello-application-locally"></a>Implementar y ejecutar la aplicación hello localmente
Ahora puede seguir adelante y ejecutar la aplicación hello. En Visual Studio, presione `F5` toodeploy aplicación de hello para la depuración. `F5` produce un error si previamente no ha abierto Visual Studio como **administrador**.

> [!NOTE]
> Hola la primera vez que se ejecute e implementa aplicación de hello localmente, Visual Studio crea un clúster local para la depuración.  Es posible que la creación del clúster tarde un tiempo. estado de creación de clúster de Hola se muestra en la ventana de salida de Visual Studio de hello.

En este momento, la aplicación web se debe parecer a esta:

![Front-end de ASP.NET Core](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop depurar la aplicación hello, vuelva atrás tooVisual Studio y presione **MAYÚS+F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Agregar una aplicación de servicio de back-end con estado tooyour
Ahora que tenemos un servicio de API Web de ASP.NET que se ejecuta en nuestra aplicación, sigamos adelante y agregue algunos datos de un servicio confiable con estado toostore en nuestra aplicación.

Service Fabric permite tooconsistently y confiable almacenar los datos directamente dentro de su servicio mediante el uso de colecciones confiables. Colecciones de confianza son un conjunto de clases de colección altamente disponible y confiable que están familiarizado tooanyone que ha utilizado las colecciones de C#.

En este tutorial creará un servicio, que almacena un valor de contador en una colección de confianza.

1. En el Explorador de soluciones, haga clic en **servicios** en Hola proyecto de aplicación y elija **Agregar > nuevo servicio de Fabric**.
   
    ![Agregar una nueva aplicación existente de tooan de servicio](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. Hola **nuevo servicio de Fabric** cuadro de diálogo, elija **Stateful ASP.NET Core**y el servicio de nombres de hello **VotingData** y presione **Aceptar**.

    ![Cuadro de diálogo de servicio nuevo en Visual Studio.](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Una vez creado el proyecto de servicio, tendrá dos servicios en la aplicación. A medida que continúa toobuild la aplicación, puede agregar más servicios Hola igual. Cada uno puede tener versiones y actualizaciones independientes.

3. página siguiente de Hello proporciona un conjunto de ASP.NET Core plantillas de proyecto. Para este tutorial, elija **API Web**.

    ![Elección del tipo de proyecto ASP.NET](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio crea un proyecto de servicio y lo muestra en el Explorador de soluciones.

    ![Explorador de soluciones](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Agregar archivo de hello VoteDataController.cs

Hola **VotingData** menú contextual del proyecto en hello **controladores** carpeta, a continuación, seleccione **Agregar -> nuevo elemento -> clase**. Nombre de archivo de hello "VoteDataController.cs" y haga clic en **agregar**. Reemplace el contenido del archivo Hola por siguiente de hello, a continuación, guarde los cambios.

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


## <a name="connect-hello-services"></a>Conectar servicios de Hola
En este paso, agregaremos Hola dos servicios de conexión y hacer Hola front-end Web aplicación get y set votos información de servicio de back-end de Hola.

Service Fabric proporciona una flexibilidad completa en el modo de comunicación con los servicios confiables. Dentro de una única aplicación, es posible que tenga servicios que sean accesibles a través de TCP. Puede haber también otros servicios que podrían estar accesibles a través de una API de REST de HTTP e incluso otros servicios que pueden estar accesibles a través de sockets web. Para obtener información sobre opciones de hello disponibles y los inconvenientes de hello, consulte [comunicarse con servicios](service-fabric-connect-and-communicate-with-services.md).

En este tutorial, vamos a utilizar [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Archivo de actualización hello VotesController.cs
Hola **VotingWeb** proyecto, abra hello *Controllers/VotesController.cs* archivo.  Reemplace hello `VotesController` clase contenido definición por siguiente hello, a continuación, guarde los cambios.

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

## <a name="walk-through-hello-voting-sample-application"></a>Recorrer Hola votos de aplicación de ejemplo
Hola votos aplicación consta de dos servicios:
- Servicio de front-end (VotingWeb) Web: An ASP.NET Core servicio front-end, que sirve de página web de Hola y expone web toocommunicate de API con el servicio back-end de Hola.
- Servicio de back-end (VotingData)-servicio de web de un núcleo de ASP.NET, que expone un voto de hello API toostore da como resultado un diccionario confiable se conserva en el disco.

![Diagrama de aplicaciones](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Eventos se producen cuando votar Hola Hola de aplicaciones siguientes:
1. JavaScript envía API web solicitud toohello para hello voto en el servicio front-end web de hello como una solicitud PUT de HTTP.

2. servicio front-end de Hello web utiliza un proxy toolocate y reenviar un servicio de back-end de toohello de solicitud HTTP PUT.

3. servicio de back-end de Hello toma la solicitud entrante de Hola y Hola almacenes actualiza resultado en un diccionario confiable, que obtiene toomultiple replicada nodos en clúster de Hola y se conserva en el disco. Datos de todas las aplicación Hola se almacenan en el clúster de hello, por lo que no se necesita ninguna base de datos.

## <a name="debug-in-visual-studio"></a>Depurar en Visual Studio
Cuando se depura una aplicación en Visual Studio, se usa un clúster de desarrollo de Service Fabric local. Tener Hola opción tooadjust su escenario de tooyour de experiencia de depuración. En esta aplicación, almacenamos los datos en nuestro servicio back-end mediante un diccionario confiable. Visual Studio quita aplicación hello de forma predeterminada cuando se detiene el depurador Hola. Quitar aplicación hello hace que los datos de hello en hello back-end puede quitar tooalso de servicio. datos de hello toopersist entre las sesiones de depuración, puede cambiar hello **modo de depuración de la aplicación** como una propiedad en hello **votación** proyecto en Visual Studio.

toolook en lo que sucede en el código de hello, Hola completa pasos:
1. Hola abierto **VotesController.cs** de archivos y establecer un punto de interrupción en web Hola API **colocar** método (línea 47): puede buscar archivo Hola Hola el Explorador de soluciones en Visual Studio.

2. Abra hello **VoteDataController.cs** de archivos y establezca un punto de interrupción en esta API de web **colocar** método (línea 50).

3. Volver atrás toohello explorador y haga clic en una opción de votación o agregue una nueva opción de voto. Se alcanza el primer punto de interrupción hello en el controlador de api de hello web front-end.
    
    1. Esto es donde hello JavaScript en el Explorador de hello envía un controlador de API web de solicitud toohello en el servicio front-end de Hola.
    
    ![Incorporación del servicio front-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Primero creamos Hola URL toohello ReverseProxy para nuestro servicio back-end **(1)**.
    3. A continuación, enviamos Hola solicitud PUT de HTTP toohello ReverseProxy **(2)**.
    4. Por último, hello se devuelva la respuesta de Hola de hello servicio back-end toohello cliente **(3)**.

4. Presione **F5** toocontinue
    1. Ya estás hello en punto de interrupción en el servicio de back-end de Hola.
    
    ![Incorporación del servicio back-end de voto](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. Primera línea de hello en método hello **(1)** , usamos hello `StateManager` tooget o agregar un diccionario confiable denominado `counts`.
    3. Todas las interacciones con valores de un diccionario confiable requieren una transacción. Esta instrucción using **(2)** crea dicha transacción.
    4. En transacciones de hello, actualizamos, a continuación, valor de Hola de clave relevante Hola Hola votar la opción y confirmaciones Hola operación **(3)**. Una vez Hola confirme método devuelve, Hola datos se actualizan en el diccionario de Hola y replican tooother nodos de clúster de Hola. datos de Hello ahora se almacenan de forma segura en clúster de Hola y servicio back-end de hello puede conmutar por error nodos tooother, sigue teniendo datos Hola disponibles.
5. Presione **F5** toocontinue

Hola toostop depuración de sesión, presione **MAYÚS+F5**.


## <a name="next-steps"></a>Pasos siguientes
En esta parte del tutorial de hello, ha aprendido cómo:

> [!div class="checklist"]
> * Crear un servicio de ASP.NET Core Web API como un servicio de confianza con estado
> * Crear un servicio de ASP.NET Core Web Application como un servicio de confianza sin estado
> * Usar Hola proxy inverso toocommunicate con servicio con estado Hola

Tutorial de antemano toohello siguiente:
> [!div class="nextstepaction"]
> [Implementar Hola aplicación tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md)
