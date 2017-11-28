---
title: "Anotaciones de la versión de Application Insights | Microsoft Docs"
description: "Agregue marcadores de implementación o compilación a sus gráficos del Explorador de métricas en Application Insights."
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
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="569ca-103">Anotaciones sobre gráficos de métricas en Application Insights</span><span class="sxs-lookup"><span data-stu-id="569ca-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="569ca-104">En las anotaciones sobre gráficos del [Explorador de métricas](app-insights-metrics-explorer.md) se muestra donde ha implementado una nueva compilación u otros eventos importantes.</span><span class="sxs-lookup"><span data-stu-id="569ca-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="569ca-105">Permiten ver fácilmente si los cambios tuvieron algún efecto en el rendimiento de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="569ca-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="569ca-106">Se pueden crear automáticamente con el [sistema de compilación de Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="569ca-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="569ca-107">También puede crear anotaciones para marcar los eventos que prefiera si los [crea desde PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="569ca-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Ejemplo de anotaciones con correlación visible con el tiempo de respuesta del servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="569ca-109">Publicar anotaciones con una compilación de VSTS</span><span class="sxs-lookup"><span data-stu-id="569ca-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="569ca-110">Las anotaciones de versión son una característica del servicio de versiones y compilaciones basado en la nube de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="569ca-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="569ca-111">Instalación de la extensión Anotaciones (una vez)</span><span class="sxs-lookup"><span data-stu-id="569ca-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="569ca-112">Para poder crear anotaciones de versión, debe instalar una de las muchas extensiones de Team Service disponibles en Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="569ca-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="569ca-113">Inicie sesión en su proyecto de [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online).</span><span class="sxs-lookup"><span data-stu-id="569ca-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="569ca-114">En Visual Studio Marketplace, [obtenga la extensión de anotaciones de la versión](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)y agréguela a su cuenta de Team Services.</span><span class="sxs-lookup"><span data-stu-id="569ca-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![En la parte superior derecha de página web de Team Services, abra Marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="569ca-117">Esto solo lo tiene que hacer una vez en su cuenta de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="569ca-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="569ca-118">Las anotaciones de versión se pueden configurar ahora para cualquier proyecto de su cuenta.</span><span class="sxs-lookup"><span data-stu-id="569ca-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="569ca-119">Configurar anotaciones de versión</span><span class="sxs-lookup"><span data-stu-id="569ca-119">Configure release annotations</span></span>

<span data-ttu-id="569ca-120">Necesita obtener una clave de API separada para cada plantilla de versión de VSTS.</span><span class="sxs-lookup"><span data-stu-id="569ca-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="569ca-121">Inicie sesión en el [Portal de Microsoft Azure](https://portal.azure.com) y abra el recurso de Application Insights que supervisa su aplicación.</span><span class="sxs-lookup"><span data-stu-id="569ca-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="569ca-122">(O bien, [cree uno ahora](app-insights-overview.md), si aún no lo ha hecho).</span><span class="sxs-lookup"><span data-stu-id="569ca-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="569ca-123">Abra **Acceso a la API**, **Id. de Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="569ca-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![En portal.azure.com, abra el recurso de Application Insights y elija Configuración.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="569ca-127">En una ventana de explorador independiente, abra (o cree) la plantilla de versión que administra sus implementaciones de Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="569ca-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="569ca-128">Agregue una tarea y seleccione la tarea de anotación de versión de Application Insights en el menú.</span><span class="sxs-lookup"><span data-stu-id="569ca-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="569ca-129">Pegue el **Id. de la aplicación** que ha copiado de la hoja Acceso de API.</span><span class="sxs-lookup"><span data-stu-id="569ca-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![En Visual Studio Team Services, abra Versión, seleccione una definición de versión y elija Editar.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="569ca-133">Establezca el campo **APIKey** en una variable `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="569ca-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="569ca-134">Vuelva a la ventana de Azure, cree una clave de API y realice una copia de esta.</span><span class="sxs-lookup"><span data-stu-id="569ca-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![En la hoja Acceso a la API de la ventana de Azure, haga clic en Crear clave de API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="569ca-138">Abra la pestaña Configuración de la plantilla de la versión.</span><span class="sxs-lookup"><span data-stu-id="569ca-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="569ca-139">Cree una definición de variable para `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="569ca-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="569ca-140">Pegue su clave de API a la definición de la variable de ApiKey.</span><span class="sxs-lookup"><span data-stu-id="569ca-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![En la ventana de Team Services, seleccione la pestaña Configuración y haga clic en Agregar variable.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="569ca-143">Por último, haga clic en **Guardar** para guardar la definición de versión.</span><span class="sxs-lookup"><span data-stu-id="569ca-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="569ca-144">Ver anotaciones</span><span class="sxs-lookup"><span data-stu-id="569ca-144">View annotations</span></span>
<span data-ttu-id="569ca-145">Ahora, cuando se utilice la plantilla de versión para implementar una nueva versión, se enviará una anotación a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="569ca-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="569ca-146">Las anotaciones se mostrarán en los gráficos del Explorador de métricas.</span><span class="sxs-lookup"><span data-stu-id="569ca-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="569ca-147">Haga clic en cualquier marcador de anotación para abrir los detalles de la versión, incluidos el solicitante, la bifurcación de control de código fuente, la definición de la versión, el entorno y mucho más.</span><span class="sxs-lookup"><span data-stu-id="569ca-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Haga clic en cualquier marcador de anotación de la versión.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="569ca-149">Crear anotaciones personalizadas desde PowerShell</span><span class="sxs-lookup"><span data-stu-id="569ca-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="569ca-150">También puede crear anotaciones desde cualquier proceso que desee (sin usar VS Team System).</span><span class="sxs-lookup"><span data-stu-id="569ca-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="569ca-151">Realice una copia local del [script de PowerShell en GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="569ca-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="569ca-152">Obtenga el id. de la aplicación y cree una clave de API desde la hoja Acceso a la API.</span><span class="sxs-lookup"><span data-stu-id="569ca-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="569ca-153">Llame al script de esta forma:</span><span class="sxs-lookup"><span data-stu-id="569ca-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="569ca-154">El script se puede modificar fácilmente (por ejemplo, para crear anotaciones para el pasado).</span><span class="sxs-lookup"><span data-stu-id="569ca-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="569ca-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="569ca-155">Next steps</span></span>

* [<span data-ttu-id="569ca-156">Crear elementos de trabajo</span><span class="sxs-lookup"><span data-stu-id="569ca-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="569ca-157">Automation con PowerShell</span><span class="sxs-lookup"><span data-stu-id="569ca-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
