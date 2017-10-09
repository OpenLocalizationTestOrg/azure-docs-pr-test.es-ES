---
title: aaaInteract con informes utilizando la API de JavaScript de hello | Documentos de Microsoft
description: Power BI Embedded, interactuar con informes utilizando Hola API de JavaScript
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a><span data-ttu-id="f2636-103">Interactuar con informes de Power BI con hello API de JavaScript</span><span class="sxs-lookup"><span data-stu-id="f2636-103">Interact with Power BI reports using hello JavaScript API</span></span>
<span data-ttu-id="f2636-104">habilita la API de JavaScript de Power BI Hola se tooeasily incrustar informes de Power BI en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f2636-104">hello Power BI JavaScript API enables you tooeasily embed Power BI reports into your applications.</span></span> <span data-ttu-id="f2636-105">Con hello API, las aplicaciones pueden interactuar mediante programación con elementos de informe diferente como páginas y filtros.</span><span class="sxs-lookup"><span data-stu-id="f2636-105">With hello API, your applications can programmatically interact with different report elements like pages and filters.</span></span> <span data-ttu-id="f2636-106">Esta interactividad hace que los informes Power BI se integren mejor en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f2636-106">This interactivity makes Power BI reports a more integrated part of your application.</span></span>

<span data-ttu-id="f2636-107">Incrustar un informe de Power BI en su aplicación mediante un iframe en el que se hospeda como parte de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f2636-107">You embed a Power BI report in your application by using an iframe that is hosted as part of hello application.</span></span> <span data-ttu-id="f2636-108">Hola iframe actúa como un límite entre la aplicación y el informe de hello, como puede ver en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f2636-108">hello iframe acts as a boundary between your application and hello report, as you can see in hello following image.</span></span> 

![iframe de Power BI Embedded sin la API de Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

<span data-ttu-id="f2636-110">Hola iframe hace Hola incrustar proceso mucho más sencillo, pero sin Hola Hola de API de JavaScript informes y la aplicación no pueden interactuar entre sí.</span><span class="sxs-lookup"><span data-stu-id="f2636-110">hello iframe makes hello embedding process a lot easier, but without hello JavaScript API hello report and your application can't interact with each other.</span></span> <span data-ttu-id="f2636-111">Esta falta de interacción puede hacer que la sensación de que el informe de hello no es realmente parte de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="f2636-111">This lack of interaction can make it feel like hello report is not really part of hello application.</span></span> <span data-ttu-id="f2636-112">informe de Hola y de aplicación sea realmente necesitan toocommunicate y hacia atrás, como en hello después de la imagen.</span><span class="sxs-lookup"><span data-stu-id="f2636-112">hello report and application really need toocommunicate back and forth, as in hello following image.</span></span>

![iframe de Power BI Embedded con la API de Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

<span data-ttu-id="f2636-114">Hola API de JavaScript de Power BI permite código toowrite que puede pasar de manera segura a través de límites de iframe Hola.</span><span class="sxs-lookup"><span data-stu-id="f2636-114">hello Power BI JavaScript API enables you toowrite code that can securely pass through hello iframe boundary.</span></span> <span data-ttu-id="f2636-115">Esto permite que su aplicación tooprogrammatically realizar una acción en un informe y toolisten para eventos de acciones que realizan los usuarios en el informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="f2636-115">This enables your application tooprogrammatically perform an action in a report, and toolisten for events from actions that users make within hello report.</span></span>

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a><span data-ttu-id="f2636-116">¿Qué puede hacer con hello API de JavaScript de Power BI?</span><span class="sxs-lookup"><span data-stu-id="f2636-116">What can you do with hello Power BI JavaScript API?</span></span>
<span data-ttu-id="f2636-117">Con hello API de JavaScript puede administrar informes, navegue toopages en un informe, filtrar un informe y controlar los eventos de incrustación.</span><span class="sxs-lookup"><span data-stu-id="f2636-117">With hello JavaScript API you can manage reports, navigate toopages in a report, filter a report, and handle embedding events.</span></span> <span data-ttu-id="f2636-118">Hello siguiente diagrama muestra la estructura de Hola de hello API.</span><span class="sxs-lookup"><span data-stu-id="f2636-118">hello following diagram shows hello structure of hello API.</span></span>

![Diagrama de la API de JavaScript de Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a><span data-ttu-id="f2636-120">Administración de informes</span><span class="sxs-lookup"><span data-stu-id="f2636-120">Manage reports</span></span>
<span data-ttu-id="f2636-121">Hola API de Javascript habilita el comportamiento de toomanage a nivel de página y el informe de hello:</span><span class="sxs-lookup"><span data-stu-id="f2636-121">hello Javascript API enables you toomanage behavior at hello report and page level:</span></span>

* <span data-ttu-id="f2636-122">Incrustar un informe de BI de energía específico de forma segura en la aplicación: intente hello [incrustar la aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span><span class="sxs-lookup"><span data-stu-id="f2636-122">Embed a specific Power BI Report securely in your application - try hello [embed demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)</span></span>
  * <span data-ttu-id="f2636-123">Establecer un token de acceso</span><span class="sxs-lookup"><span data-stu-id="f2636-123">Set access token</span></span>
* <span data-ttu-id="f2636-124">Configurar informes de Hola</span><span class="sxs-lookup"><span data-stu-id="f2636-124">Configure hello report</span></span>
  * <span data-ttu-id="f2636-125">Habilitar y deshabilitar el panel de filtro de Hola y el panel de navegación de página; intente hello [actualizar configuración de la aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span><span class="sxs-lookup"><span data-stu-id="f2636-125">Enable and disable hello filter pane and page navigation pane - try hello [update settings demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)</span></span>
  * <span data-ttu-id="f2636-126">Establecer valores predeterminados para las páginas y los filtros - intente hello [demostración de conjunto de valores predeterminados](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span><span class="sxs-lookup"><span data-stu-id="f2636-126">Set defaults for pages and filters - try hello [set defaults demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)</span></span>
* <span data-ttu-id="f2636-127">Entrar y salir de modo de pantalla completa</span><span class="sxs-lookup"><span data-stu-id="f2636-127">Enter and exit full screen mode</span></span>

[<span data-ttu-id="f2636-128">Más información acerca de cómo insertar informes</span><span class="sxs-lookup"><span data-stu-id="f2636-128">Learn more about embedding a report</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a><span data-ttu-id="f2636-129">Navegue toopages en un informe</span><span class="sxs-lookup"><span data-stu-id="f2636-129">Navigate toopages in a report</span></span>
<span data-ttu-id="f2636-130">Hola API JavaScript enbales toodiscover todas las páginas de un informe y tooset Hola actual una página.</span><span class="sxs-lookup"><span data-stu-id="f2636-130">hello JavaScript API enbales you toodiscover all pages in a report and tooset hello current page.</span></span> <span data-ttu-id="f2636-131">Intente hello [aplicación de demostración de navegación](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span><span class="sxs-lookup"><span data-stu-id="f2636-131">Try hello [navigation demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).</span></span>

[<span data-ttu-id="f2636-132">Más información acerca de la navegación por la página</span><span class="sxs-lookup"><span data-stu-id="f2636-132">Learn more about page navigation</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a><span data-ttu-id="f2636-133">Filtro de un informe</span><span class="sxs-lookup"><span data-stu-id="f2636-133">Filter a report</span></span>
<span data-ttu-id="f2636-134">Hola API de JavaScript proporciona básicas y avanzadas capacidades de filtrado de informes incrustados y páginas del informe.</span><span class="sxs-lookup"><span data-stu-id="f2636-134">hello JavaScript API provides basic and advanced filtering capabilities for embedded reports and report pages.</span></span> <span data-ttu-id="f2636-135">Intente hello [filtrado de aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)y revise el código introducción aquí.</span><span class="sxs-lookup"><span data-stu-id="f2636-135">Try hello [filtering demo application](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), and review some introductory code here.</span></span>  

#### <a name="basic-filters"></a><span data-ttu-id="f2636-136">Filtros básicos</span><span class="sxs-lookup"><span data-stu-id="f2636-136">Basic filters</span></span>
<span data-ttu-id="f2636-137">Un filtro básico se coloca en un nivel de jerarquía o de columna y contiene una lista de valores tooinclude o exclude.</span><span class="sxs-lookup"><span data-stu-id="f2636-137">A basic filter is placed on a column or hierarchy level and contains a list of values tooinclude or exclude.</span></span>

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a><span data-ttu-id="f2636-138">Filtros avanzados</span><span class="sxs-lookup"><span data-stu-id="f2636-138">Advanced filters</span></span>
<span data-ttu-id="f2636-139">Filtros avanzados utilizan el operador lógico de Hola y OR y aceptar uno o dos condiciones, cada uno con su propio operador y valor.</span><span class="sxs-lookup"><span data-stu-id="f2636-139">Advanced filters use hello logical operator AND or OR, and accept one or two conditions, each with their own operator and value.</span></span> <span data-ttu-id="f2636-140">Estas son las condiciones que se admiten:</span><span class="sxs-lookup"><span data-stu-id="f2636-140">Supported conditions are:</span></span>

* <span data-ttu-id="f2636-141">None</span><span class="sxs-lookup"><span data-stu-id="f2636-141">None</span></span>
* <span data-ttu-id="f2636-142">LessThan</span><span class="sxs-lookup"><span data-stu-id="f2636-142">LessThan</span></span>
* <span data-ttu-id="f2636-143">LessThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="f2636-143">LessThanOrEqual</span></span>
* <span data-ttu-id="f2636-144">GreaterThan</span><span class="sxs-lookup"><span data-stu-id="f2636-144">GreaterThan</span></span>
* <span data-ttu-id="f2636-145">GreaterThanOrEqual</span><span class="sxs-lookup"><span data-stu-id="f2636-145">GreaterThanOrEqual</span></span>
* <span data-ttu-id="f2636-146">Contains</span><span class="sxs-lookup"><span data-stu-id="f2636-146">Contains</span></span>
* <span data-ttu-id="f2636-147">DoesNotContain</span><span class="sxs-lookup"><span data-stu-id="f2636-147">DoesNotContain</span></span>
* <span data-ttu-id="f2636-148">StartsWith</span><span class="sxs-lookup"><span data-stu-id="f2636-148">StartsWith</span></span>
* <span data-ttu-id="f2636-149">DoesNotStartWith</span><span class="sxs-lookup"><span data-stu-id="f2636-149">DoesNotStartWith</span></span>
* <span data-ttu-id="f2636-150">Is</span><span class="sxs-lookup"><span data-stu-id="f2636-150">Is</span></span>
* <span data-ttu-id="f2636-151">IsNot</span><span class="sxs-lookup"><span data-stu-id="f2636-151">IsNot</span></span>
* <span data-ttu-id="f2636-152">IsBlank</span><span class="sxs-lookup"><span data-stu-id="f2636-152">IsBlank</span></span>
* <span data-ttu-id="f2636-153">IsNotBlank</span><span class="sxs-lookup"><span data-stu-id="f2636-153">IsNotBlank</span></span>

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[<span data-ttu-id="f2636-154">Más información acerca de los filtros</span><span class="sxs-lookup"><span data-stu-id="f2636-154">Learn more about filtering</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a><span data-ttu-id="f2636-155">Control de eventos</span><span class="sxs-lookup"><span data-stu-id="f2636-155">Handling events</span></span>
<span data-ttu-id="f2636-156">Además toosending información en hello iframe, la aplicación puede también recibe información de hello después de eventos procedentes de hello iframe:</span><span class="sxs-lookup"><span data-stu-id="f2636-156">In addition toosending information into hello iframe, your application can also receive information on hello following events coming from hello iframe:</span></span>

* <span data-ttu-id="f2636-157">Insertar</span><span class="sxs-lookup"><span data-stu-id="f2636-157">Embed</span></span>
  * <span data-ttu-id="f2636-158">loaded</span><span class="sxs-lookup"><span data-stu-id="f2636-158">loaded</span></span>
  * <span data-ttu-id="f2636-159">error</span><span class="sxs-lookup"><span data-stu-id="f2636-159">error</span></span>
* <span data-ttu-id="f2636-160">Informes</span><span class="sxs-lookup"><span data-stu-id="f2636-160">Reports</span></span>
  * <span data-ttu-id="f2636-161">pageChanged</span><span class="sxs-lookup"><span data-stu-id="f2636-161">pageChanged</span></span>
  * <span data-ttu-id="f2636-162">dataSelected (próximamente)</span><span class="sxs-lookup"><span data-stu-id="f2636-162">dataSelected (coming soon)</span></span>

[<span data-ttu-id="f2636-163">Más información sobre el control de eventos</span><span class="sxs-lookup"><span data-stu-id="f2636-163">Learn more about handling events</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a><span data-ttu-id="f2636-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f2636-164">Next steps</span></span>
<span data-ttu-id="f2636-165">Para obtener más información acerca de la API de JavaScript de Power BI Hola, consulte Hola siguientes vínculos:</span><span class="sxs-lookup"><span data-stu-id="f2636-165">For more information about hello Power BI JavaScript API, check out hello following links:</span></span>

* [<span data-ttu-id="f2636-166">Wiki de API de JavaScript</span><span class="sxs-lookup"><span data-stu-id="f2636-166">JavaScript API Wiki</span></span>](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [<span data-ttu-id="f2636-167">Referencia de modelo de objeto</span><span class="sxs-lookup"><span data-stu-id="f2636-167">Object model reference</span></span>](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* <span data-ttu-id="f2636-168">Muestras</span><span class="sxs-lookup"><span data-stu-id="f2636-168">Samples</span></span>
  * [<span data-ttu-id="f2636-169">Angular</span><span class="sxs-lookup"><span data-stu-id="f2636-169">Angular</span></span>](http://azure-samples.github.io/powerbi-angular-client)
  * [<span data-ttu-id="f2636-170">Ember</span><span class="sxs-lookup"><span data-stu-id="f2636-170">Ember</span></span>](https://github.com/Microsoft/powerbi-ember)
* [<span data-ttu-id="f2636-171">Demostración en directo</span><span class="sxs-lookup"><span data-stu-id="f2636-171">Live demo</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)

