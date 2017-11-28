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
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="cf667-103">Consumo de una aplicación de API desde JavaScript con CORS</span><span class="sxs-lookup"><span data-stu-id="cf667-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="cf667-104">Servicio de aplicaciones ofrece compatibilidad integrada para [de uso compartido de recursos de orígenes de entre (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), lo que permite JavaScript clientes toomake entre dominios llama tooAPIs que se hospedan en aplicaciones de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="cf667-105">Servicio de aplicaciones le permite configurar CORS acceso tooyour API sin escribir ningún código en la API.</span><span class="sxs-lookup"><span data-stu-id="cf667-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="cf667-106">Este artículo contiene dos secciones:</span><span class="sxs-lookup"><span data-stu-id="cf667-106">This article contains two sections:</span></span>

* <span data-ttu-id="cf667-107">Hola [cómo tooconfigure CORS](#corsconfig) sección se explica cómo general tooconfigure CORS para cualquier aplicación de API, una aplicación web o una aplicación móvil.</span><span class="sxs-lookup"><span data-stu-id="cf667-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="cf667-108">Se aplica igualmente tooall marcos que son compatibles con el servicio de aplicaciones, incluido. NET, Node.js y Java.</span><span class="sxs-lookup"><span data-stu-id="cf667-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="cf667-109">A partir de hello [continuar tutoriales de introducción a .NET de hello](#tutorialstart) sección, artículo hello es un tutorial que muestra la compatibilidad con CORS a partir de lo que hizo [Hola primera aplicaciones de API Ver tutorial introductorio ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cf667-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="cf667-110"><a id="corsconfig"></a>Cómo tooconfigure CORS en el servicio de aplicación de Azure</span><span class="sxs-lookup"><span data-stu-id="cf667-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="cf667-111">Puede configurar CORS en hello portal de Azure o mediante [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) herramientas.</span><span class="sxs-lookup"><span data-stu-id="cf667-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="cf667-112">Configurar CORS en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="cf667-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="cf667-113">En un explorador, vaya toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf667-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf667-114">Haga clic en **servicios de aplicaciones**y, a continuación, haga clic en nombre de saludo de la aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![Seleccione la aplicación de API en el portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="cf667-116">Hola **configuración** hoja que se abre toohello derecha de hello **aplicación de API** hoja, buscar hello **API** sección y, a continuación, haga clic en **CORS**.</span><span class="sxs-lookup"><span data-stu-id="cf667-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Seleccione CORS en la hoja Configuración](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="cf667-118">En el cuadro de texto hello escriba Hola o direcciones URL que desea tooallow toocome de llamadas de JavaScript desde.</span><span class="sxs-lookup"><span data-stu-id="cf667-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="cf667-119">Por ejemplo, si ha implementado la aplicación web de JavaScript aplicación tooa denominada todolistangular, escriba "https://todolistangular.azurewebsites.net".</span><span class="sxs-lookup"><span data-stu-id="cf667-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="cf667-120">Como alternativa, puede especificar un toospecify de asterisco (*) que se aceptan todos los dominios de origen.</span><span class="sxs-lookup"><span data-stu-id="cf667-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="cf667-121">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf667-121">Click **Save**.</span></span>
   
   ![Haga clic en Guardar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="cf667-123">Tras hacer clic en **guardar**, aplicación hello API aceptará JavaScript llamadas de hello especifica las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="cf667-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="cf667-124">Configuración de CORS mediante las herramientas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="cf667-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="cf667-125">También puede configurar CORS para una aplicación de API mediante [plantillas de Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) en herramientas de línea de comandos como [Azure PowerShell](/powershell/azureps-cmdlets-docs) hello y [CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cf667-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="cf667-126">Para obtener un ejemplo de una plantilla de Azure Resource Manager que establece la propiedad CORS de hello, abra hello [azuredeploy.json archivo en el repositorio de hello para la aplicación de ejemplo de este tutorial](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="cf667-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="cf667-127">Busque la sección de Hola de plantilla de hello como el siguiente ejemplo de Hola:</span><span class="sxs-lookup"><span data-stu-id="cf667-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="cf667-128"><a id="tutorialstart"></a>Continuar el tutorial de introducción a .NET de Hola</span><span class="sxs-lookup"><span data-stu-id="cf667-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="cf667-129">Si está siguiendo hello Node.js o Java-Introducción series para aplicaciones de API, tiene completada Hola obtener serie iniciada.</span><span class="sxs-lookup"><span data-stu-id="cf667-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="cf667-130">Omitir toohello [pasos siguientes](#next-steps) sección toofind sugerencias para aprender más acerca de las aplicaciones de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="cf667-131">es una continuación de hello serie de introducción a .NET Hello resto de este artículo y se da por supuesto que haya completado correctamente [primer tutorial de hello](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cf667-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="cf667-132">Implementar hello ToDoListAngular proyecto tooa nueva aplicación web</span><span class="sxs-lookup"><span data-stu-id="cf667-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="cf667-133">En [primer tutorial de hello](app-service-api-dotnet-get-started.md), creó una aplicación de API de nivel intermedio y una aplicación de API de la capa de datos.</span><span class="sxs-lookup"><span data-stu-id="cf667-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="cf667-134">En este tutorial creará una aplicación web de aplicación de página (SPA) esa aplicación de API de nivel intermedio de hello de llamadas.</span><span class="sxs-lookup"><span data-stu-id="cf667-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="cf667-135">Hola SPA toowork hay tooenable CORS en el nivel intermedio de hello aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="cf667-136">Hola [aplicación de ejemplo ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), proyecto de hello ToDoListAngular es un cliente de AngularJS simple que llama a proyecto de API de Web ToDoListAPI de nivel intermedio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf667-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="cf667-137">Hola código JavaScript de hello *app/scripts/todoListSvc.js* archivo llama a API de hello mediante hello AngularJS HTTP proveedor.</span><span class="sxs-lookup"><span data-stu-id="cf667-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="cf667-138">Crear una nueva aplicación web para el proyecto de hello ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="cf667-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="cf667-139">Hola procedimiento toocreate una nueva aplicación web de servicio de aplicaciones e implementar un proyecto tooit es toowhat similar que vio para [crear e implementar una aplicación de API en el primer tutorial de esta serie de hello](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="cf667-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="cf667-140">Hola solo diferencia es ese tipo de aplicación hello es **aplicación Web** en lugar de **API App**.</span><span class="sxs-lookup"><span data-stu-id="cf667-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="cf667-141">Para las capturas de pantalla de los cuadros de diálogo de hello, vea</span><span class="sxs-lookup"><span data-stu-id="cf667-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="cf667-142">En **el Explorador de soluciones**, haga clic en proyecto de hello ToDoListAngular y, a continuación, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cf667-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="cf667-143">Hola **perfil** ficha de hello **Publicar Web** asistente, haga clic en **servicio de aplicaciones de Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf667-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="cf667-144">Hola **servicio de aplicaciones** cuadro de diálogo, haga clic en **nuevo**.</span><span class="sxs-lookup"><span data-stu-id="cf667-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="cf667-145">Hola **hospedaje** ficha de hello **crear servicio en la aplicación** diálogo cuadro, escriba un **nombre de la aplicación Web** que es único en hello *azurewebsites.net* dominio.</span><span class="sxs-lookup"><span data-stu-id="cf667-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="cf667-146">Elija hello Azure **suscripción** desea toowork con.</span><span class="sxs-lookup"><span data-stu-id="cf667-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="cf667-147">Hola **grupo de recursos** desplegable Elija Hola mismo grupo de recursos que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf667-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="cf667-148">Hola **Plan de servicio de aplicaciones** desplegable Elija Hola mismo plan que creó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cf667-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="cf667-149">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="cf667-149">Click **Create**.</span></span>
   
    <span data-ttu-id="cf667-150">Visual Studio crea la aplicación web de hello, crea un perfil de publicación para él y se muestra hello **conexión** paso de hello **Publicar Web** asistente.</span><span class="sxs-lookup"><span data-stu-id="cf667-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="cf667-151">No haga clic en **Publicar** todavía.</span><span class="sxs-lookup"><span data-stu-id="cf667-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="cf667-152">Hola la siguiente sección, configurará Hola nueva aplicación toocall Hola nivel intermedio API de aplicación web que se ejecuta en el servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cf667-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="cf667-153">Establecer la dirección URL de nivel intermedio de hello en configuración de aplicación web</span><span class="sxs-lookup"><span data-stu-id="cf667-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="cf667-154">Vaya toohello [portal de Azure](https://portal.azure.com/)y, a continuación, navegue toohello **aplicación Web** hoja para la aplicación web de Hola que creó el proyecto de toohost hello TodoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="cf667-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="cf667-155">Haga clic en **Configuración > Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="cf667-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="cf667-156">Hola **configuración de la aplicación** sección, agregue Hola siguientes clave y valor:</span><span class="sxs-lookup"><span data-stu-id="cf667-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="cf667-157">Clave</span><span class="sxs-lookup"><span data-stu-id="cf667-157">Key</span></span> | <span data-ttu-id="cf667-158">Valor</span><span class="sxs-lookup"><span data-stu-id="cf667-158">Value</span></span> | <span data-ttu-id="cf667-159">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cf667-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="cf667-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="cf667-160">toDoListAPIURL</span></span> |<span data-ttu-id="cf667-161">https://{nombre de la aplicación de API de nivel intermedio}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cf667-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="cf667-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="cf667-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="cf667-163">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf667-163">Click **Save**.</span></span>
   
    <span data-ttu-id="cf667-164">Cuando se ejecuta código de hello en Azure, este valor invalida la dirección URL de localhost de Hola que se encuentra en hello *Web.config* archivo.</span><span class="sxs-lookup"><span data-stu-id="cf667-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="cf667-165">código de Hello que obtiene el valor de la configuración de Hola se encuentra en *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="cf667-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="cf667-166">Hola código en *todoListSvc.js* usa Hola configuración:</span><span class="sxs-lookup"><span data-stu-id="cf667-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="cf667-167">Implementar hello ToDoListAngular web proyecto toohello nueva aplicación web</span><span class="sxs-lookup"><span data-stu-id="cf667-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="cf667-168">En Visual Studio, en hello **conexión** paso de hello **Publicar Web** asistente, haga clic en **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cf667-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="cf667-169">Visual Studio implementa hello ToDoListAngular proyecto toohello nueva aplicación web y abre una dirección URL toohello del explorador de la aplicación web de hello.</span><span class="sxs-lookup"><span data-stu-id="cf667-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="cf667-170">Probar la aplicación hello sin CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="cf667-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="cf667-171">En el explorador, herramientas de desarrollo, abra la ventana de consola de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf667-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="cf667-172">En la ventana del explorador de Hola que muestra hello AngularJS UI, haga clic en hello **tooDo lista** vínculo.</span><span class="sxs-lookup"><span data-stu-id="cf667-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="cf667-173">Hola código de JavaScript intenta toocall nivel intermedio de hello aplicación de API, pero se produce un error en la llamada de Hola porque front-end de Hola está ejecutando en un dominio distinto al nuevo Hola final.</span><span class="sxs-lookup"><span data-stu-id="cf667-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="cf667-174">ventana de la consola para desarrolladores de herramientas del explorador de Hello muestra un mensaje de error entre orígenes.</span><span class="sxs-lookup"><span data-stu-id="cf667-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Mensaje de error de origen cruzado](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="cf667-176">Configurar CORS para el nivel intermedio de hello aplicación de API</span><span class="sxs-lookup"><span data-stu-id="cf667-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="cf667-177">En esta sección, configurar configuración de CORS de hello en Azure de nivel intermedio de hello aplicación de API de ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="cf667-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="cf667-178">Este valor permitirá que Hola nivel intermedio aplicación tooreceive JavaScript llamadas a API de la aplicación web de Hola que ha creado para el proyecto de ToDoListAngular Hola.</span><span class="sxs-lookup"><span data-stu-id="cf667-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="cf667-179">En un explorador, vaya toohello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cf667-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="cf667-180">Haga clic en **servicios de aplicaciones**y, a continuación, haga clic en aplicación hello API ToDoListAPI (nivel intermedio).</span><span class="sxs-lookup"><span data-stu-id="cf667-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![Seleccione la aplicación de API en el portal](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="cf667-182">Hola **configuración** hoja que se abre toohello derecha de hello **aplicación de API** hoja, buscar hello **API** sección y, a continuación, haga clic en **CORS**.</span><span class="sxs-lookup"><span data-stu-id="cf667-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![Seleccione CORS en el portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="cf667-184">En el cuadro de texto hello, escriba Hola URL para la aplicación web de hello ToDoListAngular (front-end).</span><span class="sxs-lookup"><span data-stu-id="cf667-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="cf667-185">Por ejemplo, si ha implementado la aplicación hello ToDoListAngular proyecto tooa web denominada todolistangular0121, permiten llamadas de dirección URL de hello `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="cf667-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="cf667-186">Como alternativa, puede especificar un toospecify de asterisco (*) que se aceptan todos los dominios de origen.</span><span class="sxs-lookup"><span data-stu-id="cf667-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="cf667-187">Haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="cf667-187">Click **Save**.</span></span>
   
   ![Haga clic en Guardar](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="cf667-189">Tras hacer clic en **guardar**, aplicación hello API aceptará JavaScript llamadas de hello especifica la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="cf667-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="cf667-190">En esta captura de pantalla, hello ToDoListAPI0223 API aplicación aceptará llamadas de cliente de JavaScript de la aplicación web de hello ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="cf667-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="cf667-191">Probar la aplicación hello con CORS habilitado</span><span class="sxs-lookup"><span data-stu-id="cf667-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="cf667-192">Abra una dirección URL HTTPS de aplicación web de hello toohello de explorador.</span><span class="sxs-lookup"><span data-stu-id="cf667-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="cf667-193">Esta aplicación Hola de tiempo permite ver, agregar, editar y eliminar elementos pendientes.</span><span class="sxs-lookup"><span data-stu-id="cf667-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![página de lista tooDo de aplicación de ejemplo](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="cf667-195">CORS de Servicio de aplicaciones frente a CORS de API web </span><span class="sxs-lookup"><span data-stu-id="cf667-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="cf667-196">En un proyecto de API Web, puede instalar hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) toospecify de paquete de NuGet en los dominios que se va a aceptar su API JavaScript llama desde el código.</span><span class="sxs-lookup"><span data-stu-id="cf667-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="cf667-197">La compatibilidad con Web API CORS es más flexible que la compatibilidad con CORS de Servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="cf667-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="cf667-198">Por ejemplo, en el código puede especificar diferentes orígenes aceptados para diferentes métodos de acción, mientras que para CORS del servicio de aplicaciones especifica un conjunto de orígenes aceptados para todos los métodos de una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="cf667-199">No intente toouse Web API CORS y CORS del servicio de aplicación en una aplicación de API.</span><span class="sxs-lookup"><span data-stu-id="cf667-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="cf667-200">CORS de Servicio de aplicaciones tendrá prioridad y Web API CORS no tendrá ningún efecto.</span><span class="sxs-lookup"><span data-stu-id="cf667-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="cf667-201">Por ejemplo, si habilita un dominio de origen en servicio de aplicaciones y habilitar todos los dominios de origen en el código de la API Web, la aplicación de API de Azure solo aceptará llamadas de dominio de Hola que especificó en Azure.</span><span class="sxs-lookup"><span data-stu-id="cf667-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="cf667-202">Cómo tooenable CORS en el código de la API de Web</span><span class="sxs-lookup"><span data-stu-id="cf667-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="cf667-203">Hola pasos resume proceso Hola para habilitar la compatibilidad de Web API CORS.</span><span class="sxs-lookup"><span data-stu-id="cf667-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="cf667-204">Para más información, consulte [Enabling Cross-Origin Requests in ASP.NET Web API 2 (Habilitación de solicitudes entre orígenes en API web de ASP.NET)](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span><span class="sxs-lookup"><span data-stu-id="cf667-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="cf667-205">En un proyecto de API Web, instale hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) paquete NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf667-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="cf667-206">Incluir un `config.EnableCors()` línea de código de hello **registrar** método de hello **WebApiConfig** (clase), como en el siguiente ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cf667-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
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
3. <span data-ttu-id="cf667-207">En el controlador de API Web, agregue un `using` instrucción para hello `System.Web.Http.Cors` espacio de nombres y agregue hello `EnableCors` atributo métodos de acción de clase o tooindividual del controlador toohello.</span><span class="sxs-lookup"><span data-stu-id="cf667-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="cf667-208">En el siguiente ejemplo de Hola, compatibilidad con CORS aplica toohello todo controlador.</span><span class="sxs-lookup"><span data-stu-id="cf667-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="cf667-209">Uso de Administración de API de Azure con aplicaciones de API</span><span class="sxs-lookup"><span data-stu-id="cf667-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="cf667-210">Si usa administración de API de Azure con una aplicación de API, configurar CORS administración de API en lugar de en la aplicación de API de hello.</span><span class="sxs-lookup"><span data-stu-id="cf667-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="cf667-211">Para obtener más información, vea Hola recursos siguientes:</span><span class="sxs-lookup"><span data-stu-id="cf667-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="cf667-212">Azure API Management Overview (vídeo: CORS empieza en 12:10)</span><span class="sxs-lookup"><span data-stu-id="cf667-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="cf667-213">Directivas entre dominios de Administración de API</span><span class="sxs-lookup"><span data-stu-id="cf667-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="cf667-214">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="cf667-214">Troubleshooting</span></span>
<span data-ttu-id="cf667-215">Si experimenta algún problema mientras lleva a cabo este tutorial, aquí se ofrecen ideas para solucionarlo.</span><span class="sxs-lookup"><span data-stu-id="cf667-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="cf667-216">Asegúrese de que está usando la versión más reciente de Hola de hello [Azure SDK para .NET para Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="cf667-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="cf667-217">Asegúrese de que escribió `https` en Hola configuración de CORS y asegúrese de que está usando `https` toorun Hola front-end web app.</span><span class="sxs-lookup"><span data-stu-id="cf667-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="cf667-218">Asegúrese de que escribió la configuración de CORS de hello en aplicación de API de nivel intermedio de hello, no en la aplicación web front-end de hello.</span><span class="sxs-lookup"><span data-stu-id="cf667-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="cf667-219">Si va a configurar CORS en el código de la aplicación y el servicio de aplicaciones de Azure, tenga en cuenta que configuración de CORS del servicio de aplicación Hola reemplazará lo que se está realizando en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="cf667-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="cf667-220">toolearn más información acerca de las características de Visual Studio que simplifican la solución de problemas, consulte [aplicaciones de la solución de problemas de servicio de aplicaciones de Azure en Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="cf667-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf667-221">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cf667-221">Next steps</span></span>
<span data-ttu-id="cf667-222">En este artículo, ha visto cómo tooenable CORS del servicio de aplicación son compatibles con el modo que el código de JavaScript de cliente puede llamar a una API en un dominio diferente.</span><span class="sxs-lookup"><span data-stu-id="cf667-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="cf667-223">más información acerca de las aplicaciones de API, leer hello toolearn [tooauthentication de introducción en el servicio de aplicaciones](../app-service/app-service-authentication-overview.md), y, a continuación, vaya toohello [autenticación de usuario para las aplicaciones de API](app-service-api-dotnet-user-principal-auth.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf667-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>

