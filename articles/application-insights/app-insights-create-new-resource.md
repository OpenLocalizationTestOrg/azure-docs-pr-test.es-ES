---
title: un nuevo recurso de Azure Application Insights aaaCreate | Documentos de Microsoft
description: "Describe la configuración manual de la supervisión de Application Insights para una nueva aplicación activa."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="b942c-103">Creación de recursos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b942c-103">Create an Application Insights resource</span></span>
<span data-ttu-id="b942c-104">Azure Application Insights muestra los datos de la aplicación en un *recurso*de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b942c-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="b942c-105">Crear un nuevo recurso, por tanto, forma parte de [configurar Application Insights toomonitor una nueva aplicación][start].</span><span class="sxs-lookup"><span data-stu-id="b942c-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="b942c-106">En muchos casos, crear un recurso puede realizarse automáticamente Hola IDE.</span><span class="sxs-lookup"><span data-stu-id="b942c-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="b942c-107">Pero en algunos casos, se crea un recurso manualmente, por ejemplo, se genera toohave recursos independientes para el desarrollo y producción de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b942c-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="b942c-108">Después de haber creado el recurso de hello, podrá obtener su clave de instrumentación y utilizar ese hello tooconfigure SDK en la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="b942c-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="b942c-109">enlaces de clave de recursos de Hola Hola recursos toohello de telemetría.</span><span class="sxs-lookup"><span data-stu-id="b942c-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="b942c-110">Suscribirse a Azure tooMicrosoft</span><span class="sxs-lookup"><span data-stu-id="b942c-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="b942c-111">Si todavía no dispone de una [cuenta Microsoft, obtenga una ahora](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="b942c-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="b942c-112">(Si usa servicios como Outlook.com, OneDrive, Windows Phone o XBox Live, ya tiene una cuenta Microsoft).</span><span class="sxs-lookup"><span data-stu-id="b942c-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="b942c-113">También necesita una suscripción demasiado[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="b942c-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="b942c-114">Si su equipo u organización tiene una suscripción de Azure, propietario de hello puede agregarle tooit, con su Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="b942c-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="b942c-115">Solo se le cobrará por lo que use.</span><span class="sxs-lookup"><span data-stu-id="b942c-115">You're only charged for what you use.</span></span> <span data-ttu-id="b942c-116">plan básico de Hello predeterminada permite que una determinada cantidad de uso experimental de forma gratuita.</span><span class="sxs-lookup"><span data-stu-id="b942c-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="b942c-117">Si tienes acceso tooa suscripción, inicie sesión en visión tooApplication en [http://portal.azure.com](https://portal.azure.com)y usar su toologin Live ID.</span><span class="sxs-lookup"><span data-stu-id="b942c-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="b942c-118">Creación de recursos en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b942c-118">Create an Application Insights resource</span></span>
<span data-ttu-id="b942c-119">Hola [portal.azure.com](https://portal.azure.com), agregar un recurso de información de la aplicación:</span><span class="sxs-lookup"><span data-stu-id="b942c-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Haga clic en Nuevo, Application Insights.](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="b942c-121">**Tipo de aplicación** afecta a lo que ve en la hoja de información general de Hola y Hola propiedades [explorer métrica][metrics].</span><span class="sxs-lookup"><span data-stu-id="b942c-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="b942c-122">Si no ve el tipo de aplicación, elija General.</span><span class="sxs-lookup"><span data-stu-id="b942c-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="b942c-123">**suscripción** es su cuenta de pago de Azure.</span><span class="sxs-lookup"><span data-stu-id="b942c-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="b942c-124">**grupo de recursos** resulta práctico para administrar las propiedades, como el control de acceso.</span><span class="sxs-lookup"><span data-stu-id="b942c-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="b942c-125">Si ya ha creado otros recursos de Azure, puede elegir este recurso nuevo tooput Hola mismo grupo.</span><span class="sxs-lookup"><span data-stu-id="b942c-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="b942c-126">**ubicación** es donde se guardan los datos.</span><span class="sxs-lookup"><span data-stu-id="b942c-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="b942c-127">**PIN toodashboard** coloca un icono de acceso rápido para el recurso en la página principal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b942c-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="b942c-128">Se recomienda su uso.</span><span class="sxs-lookup"><span data-stu-id="b942c-128">Recommended.</span></span>

<span data-ttu-id="b942c-129">Cuando se haya creado la aplicación, se abrirá una nueva hoja.</span><span class="sxs-lookup"><span data-stu-id="b942c-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="b942c-130">En esta hoja podrá ver datos de uso y rendimiento sobre la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b942c-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="b942c-131">tooget atrás tooit próxima vez que inicie sesión en tooAzure, busque el icono de inicio rápido de la aplicación en hello iniciar Panel (pantalla principal).</span><span class="sxs-lookup"><span data-stu-id="b942c-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="b942c-132">O haga clic en Examinar toofind lo.</span><span class="sxs-lookup"><span data-stu-id="b942c-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="b942c-133">Copie la clave de instrumentación de Hola</span><span class="sxs-lookup"><span data-stu-id="b942c-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="b942c-134">clave de instrumentación de Hello identifica recursos de Hola que ha creado.</span><span class="sxs-lookup"><span data-stu-id="b942c-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="b942c-135">Necesita toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="b942c-135">You need it toogive toohello SDK.</span></span>

![Haga clic en Essentials, haga clic en hello clave de instrumentación, CTRL + c.](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="b942c-137">Instalar SDK de hello en la aplicación</span><span class="sxs-lookup"><span data-stu-id="b942c-137">Install hello SDK in your app</span></span>
<span data-ttu-id="b942c-138">Instalar Hola Application Insights SDK en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b942c-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="b942c-139">Este paso depende en gran medida en el tipo de saludo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b942c-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="b942c-140">Usar Hola Instrumental clave tooconfigure [Hola SDK que se instala en la aplicación][start].</span><span class="sxs-lookup"><span data-stu-id="b942c-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="b942c-141">Hola SDK incluye módulos estándar que envían telemetría sin necesidad de toowrite cualquier código.</span><span class="sxs-lookup"><span data-stu-id="b942c-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="b942c-142">las acciones del usuario tootrack o diagnosticar problemas con más detalle, [usar API de hello] [ api] toosend su propio telemetría.</span><span class="sxs-lookup"><span data-stu-id="b942c-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="b942c-143"><a name="monitor"></a>Visualización de los datos de telemetría</span><span class="sxs-lookup"><span data-stu-id="b942c-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="b942c-144">Cerrar Hola rápido inicio hoja de aplicaciones de hoja tooreturn tooyour Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="b942c-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="b942c-145">Haga clic en toosee de icono de búsqueda de hello [búsqueda diagnóstico][diagnostic], dónde aparecen los primeros eventos de Hola.</span><span class="sxs-lookup"><span data-stu-id="b942c-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="b942c-146">Si espera más datos, haga clic en **Actualizar** después de unos segundos.</span><span class="sxs-lookup"><span data-stu-id="b942c-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="b942c-147">Creación de un recurso de forma automática</span><span class="sxs-lookup"><span data-stu-id="b942c-147">Creating a resource automatically</span></span>
<span data-ttu-id="b942c-148">Puede escribir un [script de PowerShell](app-insights-powershell.md) toocreate un recurso automáticamente.</span><span class="sxs-lookup"><span data-stu-id="b942c-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b942c-149">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b942c-149">Next steps</span></span>
* [<span data-ttu-id="b942c-150">Creación de un panel</span><span class="sxs-lookup"><span data-stu-id="b942c-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="b942c-151">Búsqueda de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="b942c-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="b942c-152">Exploración de métricas</span><span class="sxs-lookup"><span data-stu-id="b942c-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="b942c-153">Escribir consultas de Analytics</span><span class="sxs-lookup"><span data-stu-id="b942c-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

