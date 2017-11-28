---
title: "aaaBuild una aplicación de gran escala en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse distintos servicios de Azure toomaximize Hola rendimiento de una aplicación ASP.NET en Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="7171f-103">Creación de una aplicación web a gran escala en Azure</span><span class="sxs-lookup"><span data-stu-id="7171f-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="7171f-104">Este tutorial muestra cómo tooscale fuera una aplicación web ASP.NET en Azure toomaximize usuario solicita.</span><span class="sxs-lookup"><span data-stu-id="7171f-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="7171f-105">Antes de iniciar este tutorial, asegúrese de que [Hola CLI de Azure está instalado](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) en su equipo.</span><span class="sxs-lookup"><span data-stu-id="7171f-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="7171f-106">Además, necesitará [Visual Studio](https://www.visualstudio.com/vs/) en la aplicación de ejemplo de Hola de toorun de equipo local.</span><span class="sxs-lookup"><span data-stu-id="7171f-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="7171f-107">Paso 1: Obtención de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7171f-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="7171f-108">En este paso, configurar un proyecto ASP.NET local Hola.</span><span class="sxs-lookup"><span data-stu-id="7171f-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="7171f-109">Repositorio de aplicación Hola de clon</span><span class="sxs-lookup"><span data-stu-id="7171f-109">Clone hello application repository</span></span>

<span data-ttu-id="7171f-110">Terminal de línea de comandos de hello abierto de su elección y `CD` tooa directorio de trabajo.</span><span class="sxs-lookup"><span data-stu-id="7171f-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="7171f-111">A continuación, siguiente ejecución Hola comandos tooclone aplicación de ejemplo de Hola.</span><span class="sxs-lookup"><span data-stu-id="7171f-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="7171f-112">Ejecutar la aplicación de ejemplo de Hola en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7171f-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="7171f-113">Abra la solución de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7171f-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="7171f-114">Tipo de `F5` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="7171f-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="7171f-115">Esta aplicación web ASP.NET de ejemplo proviene de la plantilla predeterminada de Hola y continúa usuario sesiones y se utiliza Hola memoria caché de resultados.</span><span class="sxs-lookup"><span data-stu-id="7171f-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="7171f-116">Eche un vistazo a `HighScaleApp\Controllers\HomeController.cs`.</span><span class="sxs-lookup"><span data-stu-id="7171f-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="7171f-117">Hola `Index()` método agrega una parte de la sesión de toohello de datos.</span><span class="sxs-lookup"><span data-stu-id="7171f-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="7171f-118">Hello y `About()` y `Contact()` métodos caché su resultado.</span><span class="sxs-lookup"><span data-stu-id="7171f-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="7171f-119">Paso 2: implementar tooAzure</span><span class="sxs-lookup"><span data-stu-id="7171f-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="7171f-120">En este paso, creará una aplicación web de Azure e implementar su tooit de aplicación de ASP.NET de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7171f-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="7171f-121">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7171f-121">Create a resource group</span></span>   
<span data-ttu-id="7171f-122">Use [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) toocreate una [grupo de recursos](../azure-resource-manager/resource-group-overview.md) en la región de Europa occidental Hola.</span><span class="sxs-lookup"><span data-stu-id="7171f-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="7171f-123">Un grupo de recursos es donde se colocan todas las Hola recursos de Azure que desea toomanage juntos, como aplicación web de hello y cualquier base de datos SQL back-end.</span><span class="sxs-lookup"><span data-stu-id="7171f-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="7171f-124">toosee los posibles valores pueden usar para `---location`, usar hello [az de servicio de aplicaciones enumerar ubicaciones](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) comando.</span><span class="sxs-lookup"><span data-stu-id="7171f-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="7171f-125">Creación de un plan de App Service</span><span class="sxs-lookup"><span data-stu-id="7171f-125">Create an App Service plan</span></span>
<span data-ttu-id="7171f-126">Use [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate un "B1" [plan de servicio de aplicaciones](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7171f-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="7171f-127">Un plan de servicio de aplicaciones es una unidad de escala, que puede incluir cualquier número de aplicaciones que desee tooscale seguridad o out over junto Hola misma infraestructura de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7171f-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="7171f-128">A cada plan se le asigna también un [plan de tarifa](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="7171f-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="7171f-129">Los niveles superiores incluyen mejor hardware y más características, por ejemplo, más instancias de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="7171f-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="7171f-130">Para este tutorial, B1 es el nivel mínimo de Hola que permite escalar horizontalmente toothree instancias.</span><span class="sxs-lookup"><span data-stu-id="7171f-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="7171f-131">La aplicación siempre puede mover hacia arriba o abajo Hola tarifa más adelante mediante la ejecución de [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span><span class="sxs-lookup"><span data-stu-id="7171f-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="7171f-132">Creación de una aplicación web</span><span class="sxs-lookup"><span data-stu-id="7171f-132">Create a web app</span></span>
<span data-ttu-id="7171f-133">Use [crear web de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate una aplicación web con un nombre único en `$appName`.</span><span class="sxs-lookup"><span data-stu-id="7171f-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="7171f-134">Configurar credenciales de implementación</span><span class="sxs-lookup"><span data-stu-id="7171f-134">Set deployment credentials</span></span>
<span data-ttu-id="7171f-135">Use [conjunto de usuarios de implementación de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset las credenciales de la implementación de nivel de la cuenta de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7171f-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="7171f-136">Configuración de la implementación de Git</span><span class="sxs-lookup"><span data-stu-id="7171f-136">Configure Git deployment</span></span>
<span data-ttu-id="7171f-137">Use [control de código fuente de web de servicio de aplicaciones en az config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure implementación de Git local.</span><span class="sxs-lookup"><span data-stu-id="7171f-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="7171f-138">Este comando proporciona una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7171f-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="7171f-139">Hola de uso devuelve URL tooconfigure la Git remoto.</span><span class="sxs-lookup"><span data-stu-id="7171f-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="7171f-140">Hello siguiente comando usa Hola anterior ejemplo de salida.</span><span class="sxs-lookup"><span data-stu-id="7171f-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="7171f-141">Implementar la aplicación de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="7171f-141">Deploy hello sample application</span></span>
<span data-ttu-id="7171f-142">Se está ahora listo toodeploy la aplicación de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="7171f-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="7171f-143">Ejecute `git push`.</span><span class="sxs-lookup"><span data-stu-id="7171f-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="7171f-144">Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="7171f-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="7171f-145">Examinar la aplicación web de tooAzure</span><span class="sxs-lookup"><span data-stu-id="7171f-145">Browse tooAzure web app</span></span>
<span data-ttu-id="7171f-146">Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee la aplicación que se ejecutan en Azure, ejecute este comando.</span><span class="sxs-lookup"><span data-stu-id="7171f-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="7171f-147">Paso 3: conectar tooRedis</span><span class="sxs-lookup"><span data-stu-id="7171f-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="7171f-148">En este paso, configurar caché en Redis de Azure como una aplicación web de Azure de tooyour de memoria caché externo y colocados.</span><span class="sxs-lookup"><span data-stu-id="7171f-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="7171f-149">Puede usar rápidamente Redis toocache el resultado de la página.</span><span class="sxs-lookup"><span data-stu-id="7171f-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="7171f-150">Además, al escalar horizontalmente las aplicaciones web más adelante, Redis le ayuda a conservar las sesiones de usuario entre varias instancias de forma confiable.</span><span class="sxs-lookup"><span data-stu-id="7171f-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="7171f-151">Creación de una instancia de Caché en Redis de Azure</span><span class="sxs-lookup"><span data-stu-id="7171f-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="7171f-152">Use [crear redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate almacenar en caché un Redis de Azure y guardar Hola de salida JSON.</span><span class="sxs-lookup"><span data-stu-id="7171f-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="7171f-153">Use un nombre único en `$cacheName`.</span><span class="sxs-lookup"><span data-stu-id="7171f-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="7171f-154">Configurar toouse de aplicación Hola Redis</span><span class="sxs-lookup"><span data-stu-id="7171f-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="7171f-155">Cadena de conexión de Hola de formato de la memoria caché.</span><span class="sxs-lookup"><span data-stu-id="7171f-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="7171f-156">segunda línea de Hello debe darle una salida similar a esto:</span><span class="sxs-lookup"><span data-stu-id="7171f-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="7171f-157">En Visual Studio, cree un archivo de configuración web en la raíz del proyecto denominado `redis.config` y pegar Hola siguiente código en él.</span><span class="sxs-lookup"><span data-stu-id="7171f-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="7171f-158">En `value`, usar cadena de conexión de Hola de hello salida de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7171f-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="7171f-159">Si observa hello `.gitignore` archivo en el repositorio Git, verá que este archivo está excluido del control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="7171f-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="7171f-160">De este modo se mantiene segura la información confidencial.</span><span class="sxs-lookup"><span data-stu-id="7171f-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="7171f-161">Abra `Web.config`.</span><span class="sxs-lookup"><span data-stu-id="7171f-161">Open `Web.config`.</span></span> <span data-ttu-id="7171f-162">Hola aviso `<appSettings file="redis.config">` elemento, que obtiene la configuración de Hola que creó en `redis.config`.</span><span class="sxs-lookup"><span data-stu-id="7171f-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="7171f-163">Buscar comentarios Hola sección que incluya `<sessionState>` y `<caching>`.</span><span class="sxs-lookup"><span data-stu-id="7171f-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="7171f-164">Quite el comentario de esta sección.</span><span class="sxs-lookup"><span data-stu-id="7171f-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="7171f-165">Este código busca de cadena de conexión de hello Redis ha definido en `RedisConnection`.</span><span class="sxs-lookup"><span data-stu-id="7171f-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="7171f-166">La aplicación ahora usa Redis toomanage sesiones y almacenamiento en caché.</span><span class="sxs-lookup"><span data-stu-id="7171f-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="7171f-167">Tipo de `F5` aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="7171f-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="7171f-168">Si lo desea, puede descargar una Redis administración cliente toovisualize Hola de datos que se guardan toohello caché.</span><span class="sxs-lookup"><span data-stu-id="7171f-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="7171f-169">Configurar la cadena de conexión de hello en Azure</span><span class="sxs-lookup"><span data-stu-id="7171f-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="7171f-170">Para toowork de su aplicación en Azure, necesitará tooconfigure Hola la misma cadena de conexión de Redis en la aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="7171f-171">Puesto que `redis.config` no se mantiene en el control de código fuente, no está implementado tooAzure cuando se ejecuta la implementación de Git.</span><span class="sxs-lookup"><span data-stu-id="7171f-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="7171f-172">Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) cadena de conexión de hello tooadd con hello mismo nombre (`RedisConnection`).</span><span class="sxs-lookup"><span data-stu-id="7171f-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="7171f-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7171f-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="7171f-174">Recuerde que `$connstring` contiene la cadena de conexión de hello con formato.</span><span class="sxs-lookup"><span data-stu-id="7171f-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="7171f-175">Volver a implementar Hola aplicación tooAzure</span><span class="sxs-lookup"><span data-stu-id="7171f-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="7171f-176">Usar Git comandos toopush su tooAzure de cambios</span><span class="sxs-lookup"><span data-stu-id="7171f-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="7171f-177">Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="7171f-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="7171f-178">Examinar la aplicación web de Azure de toohello</span><span class="sxs-lookup"><span data-stu-id="7171f-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="7171f-179">Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) cambios de hello toosee residen en Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="7171f-180">Paso 4: instancias de toomultiple de escala</span><span class="sxs-lookup"><span data-stu-id="7171f-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="7171f-181">Hola plan de servicio de aplicaciones es la unidad de escala de Hola para las aplicaciones web de Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="7171f-182">tooscale horizontalmente su aplicación web, escalar Hola plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7171f-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="7171f-183">Use [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale instancias de toothree de plan de servicio de aplicaciones de hello, que es Hola número máximo permitido por hello B1 nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="7171f-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="7171f-184">Recuerde que B1 es hello que eligió al crear Hola anteriormente el plan de servicio de aplicaciones de nivel de precios.</span><span class="sxs-lookup"><span data-stu-id="7171f-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="7171f-185">Paso 5: Escalado geográfico</span><span class="sxs-lookup"><span data-stu-id="7171f-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="7171f-186">Cuando se escala geográficamente, ejecute la aplicación en varias regiones de hello nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="7171f-187">Equilibra la carga de la aplicación que más se basa en la geografía de este programa de instalación y reduce el tiempo de respuesta de hello mediante la colocación de los exploradores de tooclient más de cerca de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7171f-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="7171f-188">En este paso, escalar su ASP.NET web app tooa segunda región con [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="7171f-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="7171f-189">Al final de Hola de paso de hello, tendrá una aplicación web que se ejecuta en Europa occidental (ya creado) y una aplicación web que se ejecuta en sudeste de Asia (aún no se ha creado).</span><span class="sxs-lookup"><span data-stu-id="7171f-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="7171f-190">Ambas aplicaciones se servirá de hello misma dirección URL del Administrador de tráfico.</span><span class="sxs-lookup"><span data-stu-id="7171f-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="7171f-191">Escalar verticalmente hello tooStandard capa de aplicación de Europa</span><span class="sxs-lookup"><span data-stu-id="7171f-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="7171f-192">En el servicio de aplicaciones, integración con Azure Traffic Manager requiere Hola de tarifa estándar.</span><span class="sxs-lookup"><span data-stu-id="7171f-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="7171f-193">Use [actualización de plan de servicio de aplicaciones de az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale seguridad su tooS1 del plan de servicio de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="7171f-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="7171f-194">Crear un perfil de Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="7171f-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="7171f-195">Use [Crear perfil de administrador de tráfico de red az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate un Traffic Manager cree un perfil y agregar grupo de recursos de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7171f-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="7171f-196">Use un nombre DNS único en $dnsName.</span><span class="sxs-lookup"><span data-stu-id="7171f-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="7171f-197">`--routing-method Performance`Especifica que este perfil [enruta el extremo más cercano de usuario tráfico toohello](../traffic-manager/traffic-manager-routing-methods.md).</span><span class="sxs-lookup"><span data-stu-id="7171f-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="7171f-198">Obtener Id. de recurso de Hola de aplicación de hello Europa</span><span class="sxs-lookup"><span data-stu-id="7171f-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="7171f-199">Use [show de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hola el Id. de recurso de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7171f-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="7171f-200">Agregar un extremo de Traffic Manager para la aplicación de hello Europa</span><span class="sxs-lookup"><span data-stu-id="7171f-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="7171f-201">Usar [crear punto de conexión de administrador de tráfico de red de az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un perfil de Traffic Manager tooyour de punto de conexión y el Id. de recurso de Hola de uso de la aplicación web como Hola destino.</span><span class="sxs-lookup"><span data-stu-id="7171f-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="7171f-202">Obtener dirección URL del extremo de hello Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="7171f-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="7171f-203">El perfil de Traffic Manager tiene ahora un punto de conexión en esa aplicación web de puntos tooyour existente.</span><span class="sxs-lookup"><span data-stu-id="7171f-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="7171f-204">Use [mostrar de perfil de administrador de tráfico de red az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget su dirección URL.</span><span class="sxs-lookup"><span data-stu-id="7171f-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="7171f-205">Copiar el resultado de hello en el explorador.</span><span class="sxs-lookup"><span data-stu-id="7171f-205">Copy hello output into your browser.</span></span> <span data-ttu-id="7171f-206">Debería ver la aplicación web nuevo.</span><span class="sxs-lookup"><span data-stu-id="7171f-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="7171f-207">Creación de una instancia de Azure Redis Cache en Asia</span><span class="sxs-lookup"><span data-stu-id="7171f-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="7171f-208">Ahora, replica su región de Sudeste de Asia de toohello de aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="7171f-209">toostart, use [crear redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate un segundo servicio Azure Redis Cache del sudeste asiático.</span><span class="sxs-lookup"><span data-stu-id="7171f-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="7171f-210">Esta memoria caché debe toobe colocado en su aplicación en Asia.</span><span class="sxs-lookup"><span data-stu-id="7171f-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="7171f-211">`--name $cacheName-asia`Proporciona Hola nombre Hola de caché de hello caché Europa occidental, con hello `-asia` sufijo.</span><span class="sxs-lookup"><span data-stu-id="7171f-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="7171f-212">Creación de un plan de App Service en Asia</span><span class="sxs-lookup"><span data-stu-id="7171f-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="7171f-213">Use [Crear plan de servicio de aplicaciones az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate un segundo servicio de aplicación previsto en la región de hello sudeste de Asia, mediante Hola S1 mismo nivel como plan de hello Europa occidental.</span><span class="sxs-lookup"><span data-stu-id="7171f-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="7171f-214">Creación de una aplicación web en Asia</span><span class="sxs-lookup"><span data-stu-id="7171f-214">Create a web app in Asia</span></span>
<span data-ttu-id="7171f-215">Use [crear web de servicio de aplicaciones az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate una segunda aplicación web.</span><span class="sxs-lookup"><span data-stu-id="7171f-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="7171f-216">`--name $appName-asia`Proporciona Hola nombre de aplicación Hola de aplicación de hello Europa occidental, con hello `-asia` sufijo.</span><span class="sxs-lookup"><span data-stu-id="7171f-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="7171f-217">Configurar la cadena de conexión de Hola para Redis</span><span class="sxs-lookup"><span data-stu-id="7171f-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="7171f-218">Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web aplicación Hola cadena de conexión para hello caché sudeste de Asia.</span><span class="sxs-lookup"><span data-stu-id="7171f-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="7171f-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7171f-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="7171f-220">Configurar la implementación de Git para la aplicación de hello Asia.</span><span class="sxs-lookup"><span data-stu-id="7171f-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="7171f-221">Use [control de código fuente de web de servicio de aplicaciones en az config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure de implementación de Git local para la aplicación web de la segunda Hola.</span><span class="sxs-lookup"><span data-stu-id="7171f-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="7171f-222">Este comando proporciona una salida similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="7171f-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="7171f-223">Hola de uso devuelve URL tooconfigure una segunda Git remoto para el repositorio local.</span><span class="sxs-lookup"><span data-stu-id="7171f-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="7171f-224">Hello siguiente comando usa Hola anterior ejemplo de salida.</span><span class="sxs-lookup"><span data-stu-id="7171f-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="7171f-225">Implementación de la aplicación de ejemplo</span><span class="sxs-lookup"><span data-stu-id="7171f-225">Deploy your sample application</span></span>
<span data-ttu-id="7171f-226">Ejecutar `git push` toodeploy el ejemplo aplicación toohello segundo Git control remoto.</span><span class="sxs-lookup"><span data-stu-id="7171f-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="7171f-227">Cuando se le solicite una contraseña, use la contraseña de Hola que especificó cuando ejecutó `az appservice web deployment user set`.</span><span class="sxs-lookup"><span data-stu-id="7171f-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="7171f-228">Examinar toohello Asia aplicación</span><span class="sxs-lookup"><span data-stu-id="7171f-228">Browse toohello Asia app</span></span>
<span data-ttu-id="7171f-229">Use [explorar el servicio de aplicaciones web az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify que la aplicación se ejecuta en vivo en Azure.</span><span class="sxs-lookup"><span data-stu-id="7171f-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="7171f-230">Obtener Id. de recurso de Hola de aplicación de hello Asia</span><span class="sxs-lookup"><span data-stu-id="7171f-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="7171f-231">Use [show de web de servicio de aplicaciones de az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hola el Id. de recurso de la aplicación web en sudeste de Asia.</span><span class="sxs-lookup"><span data-stu-id="7171f-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="7171f-232">Agregar un extremo de Traffic Manager para la aplicación de hello Asia</span><span class="sxs-lookup"><span data-stu-id="7171f-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="7171f-233">Use [crear punto de conexión de administrador de tráfico de red de az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd un toohello de punto de conexión segundo perfil de Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="7171f-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="7171f-234">Agregar aplicaciones de tooweb de identificador de región</span><span class="sxs-lookup"><span data-stu-id="7171f-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="7171f-235">Use [actualizar az servicio de aplicaciones web configuración appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd una variable de entorno específicas de la región.</span><span class="sxs-lookup"><span data-stu-id="7171f-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="7171f-236">El código de aplicación ya usa esta configuración de aplicación.</span><span class="sxs-lookup"><span data-stu-id="7171f-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="7171f-237">Eche un vistazo a `HighScaleApp\Views\Home\Index.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="7171f-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="7171f-238">¡Listo!</span><span class="sxs-lookup"><span data-stu-id="7171f-238">Complete!</span></span>

<span data-ttu-id="7171f-239">Ahora, intente tooaccess Hola URL de su perfil de Traffic Manager de exploradores en regiones geográficas diferentes.</span><span class="sxs-lookup"><span data-stu-id="7171f-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="7171f-240">Los exploradores de cliente de Europa deben mostrar "ASP.NET Europa Occidental" y el explorador de cliente de Asia debe mostrar "ASP.NET "Sudeste Asiático".</span><span class="sxs-lookup"><span data-stu-id="7171f-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="7171f-241">Más recursos</span><span class="sxs-lookup"><span data-stu-id="7171f-241">More resources</span></span>
