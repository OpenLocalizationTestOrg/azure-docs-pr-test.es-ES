---
title: anotaciones de aaaRelease para Application Insights | Documentos de Microsoft
description: "Agregar implementación o crear marcadores gráficos de explorador de métricas de tooyour en Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="b4124-103">Anotaciones sobre gráficos de métricas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="b4124-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="b4124-104">En las anotaciones sobre gráficos del [Explorador de métricas](app-insights-metrics-explorer.md) se muestra donde ha implementado una nueva compilación u otros eventos importantes.</span><span class="sxs-lookup"><span data-stu-id="b4124-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="b4124-105">Hacen fácil toosee si los cambios tenían ningún efecto en el rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4124-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="b4124-106">Se pueden crear automáticamente por hello [sistema de compilación de Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="b4124-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="b4124-107">También puede crear anotaciones tooflag cualquier evento que desee por [crearlos desde PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="b4124-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Ejemplo de anotaciones con correlación visible con el tiempo de respuesta del servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="b4124-109">Publicar anotaciones con una compilación de VSTS</span><span class="sxs-lookup"><span data-stu-id="b4124-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="b4124-110">Anotaciones de versión son una característica de generación de hello en la nube y la versión de servicio de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b4124-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="b4124-111">Instalar extensión de anotaciones de hello (una vez)</span><span class="sxs-lookup"><span data-stu-id="b4124-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="b4124-112">toobe toocreate capaz de versión anotaciones, necesitará tooinstall uno de hello muchas extensiones de servicio de equipo disponibles en Hola Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b4124-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="b4124-113">Inicie sesión en tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) proyecto.</span><span class="sxs-lookup"><span data-stu-id="b4124-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="b4124-114">En Visual Studio Marketplace, [obtener extensión de anotaciones de la versión de Hola](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)y agregar cuenta de Team Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="b4124-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![En la parte superior derecha de página web de Team Services, abra Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="b4124-117">Solo necesita toodo esta vez para la cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b4124-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="b4124-118">Las anotaciones de versión se pueden configurar ahora para cualquier proyecto de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="b4124-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="b4124-119">Configurar anotaciones de versión</span><span class="sxs-lookup"><span data-stu-id="b4124-119">Configure release annotations</span></span>

<span data-ttu-id="b4124-120">Se necesita la clave de tooget una API diferente para cada plantilla de versión VSTS.</span><span class="sxs-lookup"><span data-stu-id="b4124-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="b4124-121">Inicie sesión en toohello [Portal de Microsoft Azure](https://portal.azure.com) y abra el recurso de Application Insights de Hola que supervisa su aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4124-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="b4124-122">(O bien, [cree uno ahora](app-insights-overview.md), si aún no lo ha hecho).</span><span class="sxs-lookup"><span data-stu-id="b4124-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="b4124-123">Abra **Acceso a la API**, **Id. de Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="b4124-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![En portal.azure.com, abra el recurso de Application Insights y elija Configuración.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="b4124-127">En otra ventana del explorador, abra (o cree) plantilla de versión de Hola que administra las implementaciones de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="b4124-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="b4124-128">Agregue una tarea y seleccione una tarea de anotación de versión de información de aplicación de Hola de menú de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4124-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="b4124-129">Hola pegar **identificador de la aplicación** que copió de hello hoja de acceso de la API.</span><span class="sxs-lookup"><span data-stu-id="b4124-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![En Visual Studio Team Services, abra Versión, seleccione una definición de versión y elija Editar.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="b4124-133">Conjunto hello **APIKey** variable del campo de tooa `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="b4124-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="b4124-134">En hello ventana de Azure, cree una nueva clave de API y realizar una copia de él.</span><span class="sxs-lookup"><span data-stu-id="b4124-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Hola hoja de acceso de API en hello Azure ventana, haga clic en crear clave de API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="b4124-138">Abra la ficha de configuración de Hola de plantilla de versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4124-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="b4124-139">Cree una definición de variable para `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="b4124-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="b4124-140">Pegue la definición de variable ApiKey de toohello clave de API.</span><span class="sxs-lookup"><span data-stu-id="b4124-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![En la ventana de Team Services hello, seleccione la ficha de configuración de Hola y haga clic en Agregar Variable.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="b4124-143">Por último, **guardar** Hola definición de versión.</span><span class="sxs-lookup"><span data-stu-id="b4124-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="b4124-144">Ver anotaciones</span><span class="sxs-lookup"><span data-stu-id="b4124-144">View annotations</span></span>
<span data-ttu-id="b4124-145">Ahora, siempre que se use Hola versión plantilla toodeploy una nueva versión, se enviará a una anotación tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="b4124-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="b4124-146">anotaciones de Hello aparecerán en los gráficos en el Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="b4124-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="b4124-147">Haga clic en los detalles de tooopen de marcador de anotación sobre versión hello, así como solicitante, bifurcación de control de código fuente, definición de versión, entorno y mucho más.</span><span class="sxs-lookup"><span data-stu-id="b4124-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Haga clic en cualquier marcador de anotación de la versión.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="b4124-149">Crear anotaciones personalizadas desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4124-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="b4124-150">También puede crear anotaciones desde cualquier proceso que desee (sin usar VS Team System).</span><span class="sxs-lookup"><span data-stu-id="b4124-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="b4124-151">Hacer una copia local de hello [secuencia de comandos de Powershell desde GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="b4124-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="b4124-152">Obtener Id. de aplicación Hola y crear una clave de API de hello hoja de acceso de la API.</span><span class="sxs-lookup"><span data-stu-id="b4124-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="b4124-153">Llamar al script de Hola similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="b4124-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="b4124-154">Es script de Hola toomodify fácil, por ejemplo toocreate anotaciones para hello anterior.</span><span class="sxs-lookup"><span data-stu-id="b4124-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4124-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4124-155">Next steps</span></span>

* [<span data-ttu-id="b4124-156">Crear elementos de trabajo</span><span class="sxs-lookup"><span data-stu-id="b4124-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="b4124-157">Automation con PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4124-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
