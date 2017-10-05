---
title: "Introducción al escalado automático mediante métricas personalizadas en Azure | Microsoft Docs"
description: "Obtenga información sobre cómo escalar recursos mediante métricas personalizadas en Azure."
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
ms.openlocfilehash: de8f7acadc282e4b81c657b1723f00fd3e5fd4f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="b4a51-103">Introducción al escalado automático mediante métricas personalizadas en Azure</span><span class="sxs-lookup"><span data-stu-id="b4a51-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="b4a51-104">En este artículo se describe cómo escalar el recurso mediante una métrica personalizada en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b4a51-104">This article describes how to scale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="b4a51-105">El escalado automático de Azure Monitor solo se aplica a Conjuntos de escalado de máquinas virtuales, Cloud Services, planes de App Service y App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="b4a51-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="b4a51-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="b4a51-106">Lets get started</span></span>
<span data-ttu-id="b4a51-107">En este artículo se presupone que tiene una aplicación web con Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="b4a51-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="b4a51-108">Si aún no la tiene, puede [configurar Application Insights para el sitio web ASP.NET][1].</span><span class="sxs-lookup"><span data-stu-id="b4a51-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="b4a51-109">Abra [Azure Portal][2].</span><span class="sxs-lookup"><span data-stu-id="b4a51-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="b4a51-110">Haga clic en el icono de Azure Monitor en el panel de navegación izquierdo.</span><span class="sxs-lookup"><span data-stu-id="b4a51-110">Click on Azure Monitor icon in the left navigation pane.</span></span>
  <span data-ttu-id="b4a51-111">![Inicio de Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="b4a51-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="b4a51-112">Haga clic en la opción Escalado automático para ver todos los recursos a los que se aplica el escalado automático, junto con su estado de escalado automático actual ![Detección de escalado automático en Azure Monitor][4]</span><span class="sxs-lookup"><span data-stu-id="b4a51-112">Click on Autoscale setting to view all the resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="b4a51-113">Abra la hoja "Escalado automático" en Azure Monitor y seleccione un recurso que desee escalar.</span><span class="sxs-lookup"><span data-stu-id="b4a51-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want to scale</span></span>
> <span data-ttu-id="b4a51-114">Nota: En los pasos siguientes se usa un plan de App Service asociado con una aplicación web con Application Insights configurado.</span><span class="sxs-lookup"><span data-stu-id="b4a51-114">Note: The steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="b4a51-115">En la hoja de configuración de escalado del recurso, tenga en cuenta que el recuento de la instancia actual es 1.</span><span class="sxs-lookup"><span data-stu-id="b4a51-115">In the scale setting blade for the resource, notice that the current instance count is 1.</span></span> <span data-ttu-id="b4a51-116">Haga clic en "Enable autoscale" (Habilitar escalado automático).</span><span class="sxs-lookup"><span data-stu-id="b4a51-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="b4a51-117">![Configuración de escalado para la nueva aplicación web][5]</span><span class="sxs-lookup"><span data-stu-id="b4a51-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="b4a51-118">Proporcione un nombre para la configuración de escalado y haga clic en "Agregar una regla".</span><span class="sxs-lookup"><span data-stu-id="b4a51-118">Provide a name for the scale setting, and the click on "Add a rule".</span></span> <span data-ttu-id="b4a51-119">Tenga en cuenta que las opciones de la regla de escalado se abren como un panel Contexto en el lado derecho.</span><span class="sxs-lookup"><span data-stu-id="b4a51-119">Notice the scale rule options that opens as a context pane in the right hand side.</span></span> <span data-ttu-id="b4a51-120">De forma predeterminada, establece la opción para escalar el recuento de instancias en 1 si el porcentaje de CPU del recurso supera el 70 %.</span><span class="sxs-lookup"><span data-stu-id="b4a51-120">By default, it sets the option to scale your instance count by 1 if the CPU percetage of the resource exceeds 70%.</span></span> <span data-ttu-id="b4a51-121">Cambie el origen de métricas en la parte superior a "Application Insights", seleccione el recurso de Application Insights en el menú desplegable "Recurso" y luego seleccione la métrica personalizada en la que quiere basar el escalado.</span><span class="sxs-lookup"><span data-stu-id="b4a51-121">Change the metric source at the top to "Application Insights", select the app insights resource in the 'Resource' dropdown and then select the custom metric based on which you want to scale.</span></span>
  <span data-ttu-id="b4a51-122">![Escalar por métrica personalizada][6]</span><span class="sxs-lookup"><span data-stu-id="b4a51-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="b4a51-123">De forma similar al paso anterior, agregue una regla de escalado que reduzca horizontalmente y disminuya el recuento de escala en 1 si la métrica personalizada está por debajo del umbral.</span><span class="sxs-lookup"><span data-stu-id="b4a51-123">Similar to the step above, add a scale rule that will scale in and decrease the scale count by 1 if the custom metric is below a threshold.</span></span>
  <span data-ttu-id="b4a51-124">![Escala en función de la CPU][7]</span><span class="sxs-lookup"><span data-stu-id="b4a51-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="b4a51-125">Establezca los límites de instancias.</span><span class="sxs-lookup"><span data-stu-id="b4a51-125">Set the you instance limits.</span></span> <span data-ttu-id="b4a51-126">Por ejemplo, si desea escalar entre 2-5 instancias en función de las fluctuaciones de la métrica personalizada, establezca el "mínimo" en "2", el "máximo" en "5" y el "valor predeterminado" en "2".</span><span class="sxs-lookup"><span data-stu-id="b4a51-126">For example, if you want to scale between 2-5 instances depending on the custom metric fluctuations, set 'minimum' to '2', 'maximum' to '5' and 'default' to '2'</span></span>
> <span data-ttu-id="b4a51-127">Nota: En caso de que haya algún problema al leer las métricas de recursos y la capacidad actual sea inferior a la predeterminada, el escalado automático escalará horizontalmente al valor predeterminado a fin de garantizar la disponibilidad del recurso.</span><span class="sxs-lookup"><span data-stu-id="b4a51-127">Note: In case there is a problem reading the resource metrics and the current capacity is below the default capacity, then to ensure the availability of the resource, Autoscale will scale out to the default value.</span></span> <span data-ttu-id="b4a51-128">Si la capacidad actual ya es mayor que la predeterminada, el escalado automático no reducirá horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="b4a51-128">If the current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="b4a51-129">Haga clic en "Guardar".</span><span class="sxs-lookup"><span data-stu-id="b4a51-129">Click on 'Save'</span></span>

<span data-ttu-id="b4a51-130">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="b4a51-130">Congratulations.</span></span> <span data-ttu-id="b4a51-131">Ya ha establecido correctamente la configuración del escalado para escalar automáticamente la aplicación web en función de una métrica personalizada.</span><span class="sxs-lookup"><span data-stu-id="b4a51-131">You now now succesfully created your scale setting to auto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="b4a51-132">Nota: Los mismos pasos son aplicables para empezar a trabajar con un rol de servicio en la nube o VMSS.</span><span class="sxs-lookup"><span data-stu-id="b4a51-132">Note: The same steps are applicable to get started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
