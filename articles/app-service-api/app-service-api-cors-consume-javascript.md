---
title: aaaCORS se admite en el servicio de aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo son compatibles con toouse CORS en el servicio de aplicación de Azure de Azure."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Consumo de una aplicación de API desde JavaScript con CORS
Servicio de aplicaciones ofrece compatibilidad integrada para [de uso compartido de recursos de orígenes de entre (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), lo que permite JavaScript clientes toomake entre dominios llama tooAPIs que se hospedan en aplicaciones de API. Servicio de aplicaciones le permite configurar CORS acceso tooyour API sin escribir ningún código en la API.

Este artículo contiene dos secciones:

* Hola [cómo tooconfigure CORS](#corsconfig) sección se explica cómo general tooconfigure CORS para cualquier aplicación de API, una aplicación web o una aplicación móvil. Se aplica igualmente tooall marcos que son compatibles con el servicio de aplicaciones, incluido. NET, Node.js y Java. 
* A partir de hello [continuar tutoriales de introducción a .NET de hello](#tutorialstart) sección, artículo hello es un tutorial que muestra la compatibilidad con CORS a partir de lo que hizo [Hola primera aplicaciones de API Ver tutorial introductorio ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Cómo tooconfigure CORS en el servicio de aplicación de Azure
Puede configurar CORS en hello portal de Azure o mediante [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) herramientas.

#### <a name="configure-cors-in-hello-azure-portal"></a>Configurar CORS en hello portal de Azure
1. En un explorador, vaya toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación de API.
   
    ![Seleccione la aplicación de API en el portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Hola **configuración** hoja que se abre toohello derecha de hello **aplicación de API** hoja, buscar hello **API** sección y, a continuación, haga clic en **CORS**.
   
   ![Seleccione CORS en la hoja Configuración](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. En el cuadro de texto hello escriba Hola o direcciones URL que desea tooallow toocome de llamadas de JavaScript desde.

    Por ejemplo, si ha implementado la aplicación web de JavaScript aplicación tooa denominada todolistangular, escriba "https://todolistangular.azurewebsites.net". Como alternativa, puede especificar un toospecify de asterisco (*) que se aceptan todos los dominios de origen.


1. Haga clic en **Guardar**.
   
   ![Haga clic en Guardar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Tras hacer clic en **guardar**, aplicación hello API aceptará JavaScript llamadas de hello especifica las direcciones URL.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>Configuración de CORS mediante las herramientas del Administrador de recursos de Azure
También puede configurar CORS para una aplicación de API mediante [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) en herramientas de línea de comandos como [Azure PowerShell](/powershell/azureps-cmdlets-docs) hello y [CLI de Azure](../cli-install-nodejs.md). 

Para obtener un ejemplo de una plantilla de Azure Resource Manager que establece la propiedad CORS de hello, abra hello [azuredeploy.json archivo en el repositorio de hello para la aplicación de ejemplo de este tutorial](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Busque la sección de Hola de plantilla de hello como el siguiente ejemplo de Hola:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>Continuar el tutorial de introducción a .NET de Hola
Si está siguiendo hello Node.js o Java-Introducción series para aplicaciones de API, tiene completada Hola obtener serie iniciada. Omitir toohello [pasos siguientes](#next-steps) sección toofind sugerencias para aprender más acerca de las aplicaciones de API.

es una continuación de hello serie de introducción a .NET Hello resto de este artículo y se da por supuesto que haya completado correctamente [primer tutorial de hello](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Implementar hello ToDoListAngular proyecto tooa nueva aplicación web
En [primer tutorial de hello](app-service-api-dotnet-get-started.md), creó una aplicación de API de nivel intermedio y una aplicación de API de la capa de datos. En este tutorial creará una aplicación web de aplicación de página (SPA) esa aplicación de API de nivel intermedio de hello de llamadas. Hola SPA toowork hay tooenable CORS en el nivel intermedio de hello aplicación de API. 

Hola [aplicación de ejemplo ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), proyecto de hello ToDoListAngular es un cliente de AngularJS simple que llama a proyecto de API de Web ToDoListAPI de nivel intermedio de Hola. Hola código JavaScript de hello *app/scripts/todoListSvc.js* archivo llama a API de hello mediante hello AngularJS HTTP proveedor. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Crear una nueva aplicación web para el proyecto de hello ToDoListAngular
Hola procedimiento toocreate una nueva aplicación web de servicio de aplicaciones e implementar un proyecto tooit es toowhat similar que vio para [crear e implementar una aplicación de API en el primer tutorial de esta serie de hello](app-service-api-dotnet-get-started.md#createapiapp). Hola solo diferencia es ese tipo de aplicación hello es **aplicación Web** en lugar de **API App**.  Para las capturas de pantalla de los cuadros de diálogo de hello, vea 

1. En **el Explorador de soluciones**, haga clic en proyecto de hello ToDoListAngular y, a continuación, haga clic en **publicar**.
2. Hola **perfil** ficha de hello **Publicar Web** asistente, haga clic en **servicio de aplicaciones de Microsoft Azure**.
3. Hola **servicio de aplicaciones** cuadro de diálogo, haga clic en **nuevo**.
4. Hola **hospedaje** ficha de hello **crear servicio en la aplicación** diálogo cuadro, escriba un **nombre de la aplicación Web** que es único en hello *azurewebsites.net* dominio. 
5. Elija hello Azure **suscripción** desea toowork con.
6. Hola **grupo de recursos** desplegable Elija Hola mismo grupo de recursos que creó anteriormente.
7. Hola **Plan de servicio de aplicaciones** desplegable Elija Hola mismo plan que creó anteriormente. 
8. Haga clic en **Crear**.
   
    Visual Studio crea la aplicación web de hello, crea un perfil de publicación para él y se muestra hello **conexión** paso de hello **Publicar Web** asistente.
   
    No haga clic en **Publicar** todavía. Hola la siguiente sección, configurará Hola nueva aplicación toocall Hola nivel intermedio API de aplicación web que se ejecuta en el servicio de aplicaciones. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Establecer la dirección URL de nivel intermedio de hello en configuración de aplicación web
1. Vaya toohello [portal de Azure](https://portal.azure.com/)y, a continuación, navegue toohello **aplicación Web** hoja para la aplicación web de Hola que creó el proyecto de toohost hello TodoListAngular (front-end).
2. Haga clic en **Configuración > Configuración de la aplicación**.
3. Hola **configuración de la aplicación** sección, agregue Hola siguientes clave y valor:
   
   | Clave | Valor | Ejemplo |
   | --- | --- | --- |
   | toDoListAPIURL |https://{nombre de la aplicación de API de nivel intermedio}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Haga clic en **Guardar**.
   
    Cuando se ejecuta código de hello en Azure, este valor invalida la dirección URL de localhost de Hola que se encuentra en hello *Web.config* archivo. 
   
    código de Hello que obtiene el valor de la configuración de Hola se encuentra en *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Hola código en *todoListSvc.js* usa Hola configuración:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Implementar hello ToDoListAngular web proyecto toohello nueva aplicación web
* En Visual Studio, en hello **conexión** paso de hello **Publicar Web** asistente, haga clic en **publicar**.
  
   Visual Studio implementa hello ToDoListAngular proyecto toohello nueva aplicación web y abre una dirección URL toohello del explorador de la aplicación web de hello. 

### <a name="test-hello-application-without-cors-enabled"></a>Probar la aplicación hello sin CORS habilitado
1. En el explorador, herramientas de desarrollo, abra la ventana de consola de Hola.
2. En la ventana del explorador de Hola que muestra hello AngularJS UI, haga clic en hello **tooDo lista** vínculo.
   
    Hola código de JavaScript intenta toocall nivel intermedio de hello aplicación de API, pero se produce un error en la llamada de Hola porque front-end de Hola está ejecutando en un dominio distinto al nuevo Hola final. ventana de la consola para desarrolladores de herramientas del explorador de Hello muestra un mensaje de error entre orígenes.
   
    ![Mensaje de error de origen cruzado](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>Configurar CORS para el nivel intermedio de hello aplicación de API
En esta sección, configurar configuración de CORS de hello en Azure de nivel intermedio de hello aplicación de API de ToDoListAPI. Este valor permitirá que Hola nivel intermedio aplicación tooreceive JavaScript llamadas a API de la aplicación web de Hola que ha creado para el proyecto de ToDoListAngular Hola.

1. En un explorador, vaya toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **servicios de aplicaciones**y, a continuación, haga clic en aplicación hello API ToDoListAPI (nivel intermedio).
   
    ![Seleccione la aplicación de API en el portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. Hola **configuración** hoja que se abre toohello derecha de hello **aplicación de API** hoja, buscar hello **API** sección y, a continuación, haga clic en **CORS**.
   
   ![Seleccione CORS en el portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. En el cuadro de texto hello, escriba Hola URL para la aplicación web de hello ToDoListAngular (front-end). Por ejemplo, si ha implementado la aplicación hello ToDoListAngular proyecto tooa web denominada todolistangular0121, permiten llamadas de dirección URL de hello `https://todolistangular0121.azurewebsites.net`.
   
   Como alternativa, puede especificar un toospecify de asterisco (*) que se aceptan todos los dominios de origen.
5. Haga clic en **Guardar**.
   
   ![Haga clic en Guardar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Tras hacer clic en **guardar**, aplicación hello API aceptará JavaScript llamadas de hello especifica la dirección URL. En esta captura de pantalla, hello ToDoListAPI0223 API aplicación aceptará llamadas de cliente de JavaScript de la aplicación web de hello ToDoListAngular.

### <a name="test-hello-application-with-cors-enabled"></a>Probar la aplicación hello con CORS habilitado
* Abra una dirección URL HTTPS de aplicación web de hello toohello de explorador. 
  
    Esta aplicación Hola de tiempo permite ver, agregar, editar y eliminar elementos pendientes. 
  
    ![página de lista tooDo de aplicación de ejemplo](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>CORS de Servicio de aplicaciones frente a CORS de API web 
En un proyecto de API Web, puede instalar hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de paquete de NuGet en los dominios que se va a aceptar su API JavaScript llama desde el código.

La compatibilidad con Web API CORS es más flexible que la compatibilidad con CORS de Servicio de aplicaciones. Por ejemplo, en el código puede especificar diferentes orígenes aceptados para diferentes métodos de acción, mientras que para CORS del servicio de aplicaciones especifica un conjunto de orígenes aceptados para todos los métodos de una aplicación de API.

> [!NOTE]
> No intente toouse Web API CORS y CORS del servicio de aplicación en una aplicación de API. CORS de Servicio de aplicaciones tendrá prioridad y Web API CORS no tendrá ningún efecto. Por ejemplo, si habilita un dominio de origen en servicio de aplicaciones y habilitar todos los dominios de origen en el código de la API Web, la aplicación de API de Azure solo aceptará llamadas de dominio de Hola que especificó en Azure.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Cómo tooenable CORS en el código de la API de Web
Hola pasos resume proceso Hola para habilitar la compatibilidad de Web API CORS. Para más información, consulte [Enabling Cross-Origin Requests in ASP.NET Web API 2 (Habilitación de solicitudes entre orígenes en API web de ASP.NET)](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).

1. En un proyecto de API Web, instale hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) paquete NuGet.
2. Incluir un `config.EnableCors()` línea de código de hello **registrar** método de hello **WebApiConfig** (clase), como en el siguiente ejemplo de Hola. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. En el controlador de API Web, agregue un `using` instrucción para hello `System.Web.Http.Cors` espacio de nombres y agregue hello `EnableCors` atributo métodos de acción de clase o tooindividual del controlador toohello. En el siguiente ejemplo de Hola, compatibilidad con CORS aplica toohello todo controlador.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Uso de Administración de API de Azure con aplicaciones de API
Si usa administración de API de Azure con una aplicación de API, configurar CORS administración de API en lugar de en la aplicación de API de hello. Para obtener más información, vea Hola recursos siguientes:

* [Azure API Management Overview (vídeo: CORS empieza en 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [Directivas entre dominios de Administración de API](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Solución de problemas
Si experimenta algún problema mientras lleva a cabo este tutorial, aquí se ofrecen ideas para solucionarlo.

* Asegúrese de que está usando la versión más reciente de Hola de hello [Azure SDK para .NET para Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Asegúrese de que escribió `https` en Hola configuración de CORS y asegúrese de que está usando `https` toorun Hola front-end web app.
* Asegúrese de que escribió la configuración de CORS de hello en aplicación de API de nivel intermedio de hello, no en la aplicación web front-end de hello.
* Si va a configurar CORS en el código de la aplicación y el servicio de aplicaciones de Azure, tenga en cuenta que configuración de CORS del servicio de aplicación Hola reemplazará lo que se está realizando en el código de aplicación. 

toolearn más información acerca de las características de Visual Studio que simplifican la solución de problemas, consulte [aplicaciones de la solución de problemas de servicio de aplicaciones de Azure en Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha visto cómo tooenable CORS del servicio de aplicación son compatibles con el modo que el código de JavaScript de cliente puede llamar a una API en un dominio diferente. más información acerca de las aplicaciones de API, leer hello toolearn [tooauthentication de introducción en el servicio de aplicaciones](../app-service/app-service-authentication-overview.md), y, a continuación, vaya toohello [autenticación de usuario para las aplicaciones de API](app-service-api-dotnet-user-principal-auth.md) tutorial.

