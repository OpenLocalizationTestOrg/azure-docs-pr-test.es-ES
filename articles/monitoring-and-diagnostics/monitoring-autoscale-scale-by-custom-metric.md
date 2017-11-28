---
title: "aaaGet iniciada con escalado automático por métrica personalizada en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooscale el recurso por métrica personalizado en Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="ff83a-103">Introducción al escalado automático mediante métricas personalizadas en Azure</span><span class="sxs-lookup"><span data-stu-id="ff83a-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="ff83a-104">Este artículo se describe cómo tooscale el recurso por una métrica personalizada en el portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ff83a-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="ff83a-105">Azure Autoescala de Monitor aplica solo tooVirtual conjuntos de escala de máquina (VMSS), servicios en la nube, planes de servicio de aplicaciones y entornos del servicio de aplicación.</span><span class="sxs-lookup"><span data-stu-id="ff83a-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="ff83a-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="ff83a-106">Lets get started</span></span>
<span data-ttu-id="ff83a-107">En este artículo se presupone que tiene una aplicación web con Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="ff83a-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="ff83a-108">Si aún no la tiene, puede [configurar Application Insights para el sitio web ASP.NET][1].</span><span class="sxs-lookup"><span data-stu-id="ff83a-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="ff83a-109">Abra [Azure Portal][2].</span><span class="sxs-lookup"><span data-stu-id="ff83a-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="ff83a-110">Haga clic en el icono de Monitor de Azure en el panel de navegación izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ff83a-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="ff83a-111">![Inicio de Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="ff83a-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="ff83a-112">Haga clic en configuración tooview todos los recursos de Hola para que automáticamente la escala es aplicable, junto con su estado actual de escalado automático de escalado automático ![detectar Autoescala en el monitor de Azure][4]</span><span class="sxs-lookup"><span data-stu-id="ff83a-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="ff83a-113">Abrir la hoja de 'Escalado automático' en el Monitor de Azure y seleccione un recurso que desee tooscale</span><span class="sxs-lookup"><span data-stu-id="ff83a-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="ff83a-114">Nota: estos pasos Hola usan un plan de servicio de aplicación asociado a una aplicación web que tiene detalles de aplicaciones configurados.</span><span class="sxs-lookup"><span data-stu-id="ff83a-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="ff83a-115">En la hoja de configuración de la escala de hello para el recurso de hello, tenga en cuenta que el recuento de instancias actual de hello es 1.</span><span class="sxs-lookup"><span data-stu-id="ff83a-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="ff83a-116">Haga clic en "Enable autoscale" (Habilitar escalado automático).</span><span class="sxs-lookup"><span data-stu-id="ff83a-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="ff83a-117">![Configuración de escalado para la nueva aplicación web][5]</span><span class="sxs-lookup"><span data-stu-id="ff83a-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="ff83a-118">Proporcione un nombre para la configuración de escala de Hola y Hola, haga clic en "Agregar una regla de".</span><span class="sxs-lookup"><span data-stu-id="ff83a-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="ff83a-119">Observe las opciones de regla de escala de Hola que se abre como un panel de contexto en hello del lado derecho.</span><span class="sxs-lookup"><span data-stu-id="ff83a-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="ff83a-120">De forma predeterminada, Establece la instancia de recuento en 1 si Hola CPU percetage del recurso de hello supera el 70% de hello opción tooscale.</span><span class="sxs-lookup"><span data-stu-id="ff83a-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="ff83a-121">Origen de métricas de Hola de cambio en la parte superior de hello demasiado "Application Insights", seleccione Hola recursos de información de aplicación en lista desplegable de 'Resource' hello y métrica de hello, a continuación, seleccione personalizada basada en la que desea tooscale.</span><span class="sxs-lookup"><span data-stu-id="ff83a-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="ff83a-122">![Escalar por métrica personalizada][6]</span><span class="sxs-lookup"><span data-stu-id="ff83a-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="ff83a-123">Paso de toohello similar anterior, agregar una regla de escala que se escale en y reduzca el recuento de escala de hello en 1 si la métrica personalizada hello está por debajo del umbral.</span><span class="sxs-lookup"><span data-stu-id="ff83a-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="ff83a-124">![Escala en función de la CPU][7]</span><span class="sxs-lookup"><span data-stu-id="ff83a-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="ff83a-125">Establecer hello para la instancia de límites.</span><span class="sxs-lookup"><span data-stu-id="ff83a-125">Set hello you instance limits.</span></span> <span data-ttu-id="ff83a-126">Por ejemplo, si desea tooscale entre 2 y 5 instancias según las fluctuaciones de métrica personalizada hello, establezca 'mínimo"demasiado '2', 'máximo' demasiado '5' y 'default' demasiado '2'</span><span class="sxs-lookup"><span data-stu-id="ff83a-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="ff83a-127">Nota: en caso de que hay un problema al leer las métricas de recursos de Hola y capacidad actual de hello está por debajo de la capacidad predeterminada de hello, a continuación, disponibilidad de hello tooensure del recurso de hello, escalado automático se espera el valor predeterminado de toohello.</span><span class="sxs-lookup"><span data-stu-id="ff83a-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="ff83a-128">Si la capacidad actual de hello ya es mayor que la capacidad predeterminada, escalado automático no se ajusta en.</span><span class="sxs-lookup"><span data-stu-id="ff83a-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="ff83a-129">Haga clic en "Guardar".</span><span class="sxs-lookup"><span data-stu-id="ff83a-129">Click on 'Save'</span></span>

<span data-ttu-id="ff83a-130">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="ff83a-130">Congratulations.</span></span> <span data-ttu-id="ff83a-131">Es ahora correctamente una vez creado el tooauto de configuración de escala escalar la aplicación web en función de una métrica personalizada.</span><span class="sxs-lookup"><span data-stu-id="ff83a-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="ff83a-132">Nota: hello mismos pasos son aplicable tooget a trabajar con un rol de servicio VMSS o en la nube.</span><span class="sxs-lookup"><span data-stu-id="ff83a-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
