---
title: "aaaSet las alertas para las consultas de análisis de transmisiones | Documentos de Microsoft"
description: "Descripción de las entradas del Análisis de transmisiones"
keywords: "configuración de alertas"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/26/2017
ms.author: jeffstok
ms.openlocfilehash: 7b1d90d1468311186567c8518e0283ea6b88c3f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-alerts-for-azure-stream-analytics-jobs"></a><span data-ttu-id="d1b68-104">Configuración de alertas en Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b68-104">Set up alerts for Azure Stream Analytics jobs</span></span>
## <a name="introduction-monitor-page"></a><span data-ttu-id="d1b68-105">Introducción: Página de supervisión</span><span class="sxs-lookup"><span data-stu-id="d1b68-105">Introduction: Monitor page</span></span>
<span data-ttu-id="d1b68-106">Puede configurar alertas tootrigger una alerta cuando una métrica alcanza una condición que especifique.</span><span class="sxs-lookup"><span data-stu-id="d1b68-106">You can set up alerts tootrigger an alert when a metric reaches a condition that you specify.</span></span> <span data-ttu-id="d1b68-107">Por ejemplo, puede configurar una alerta para una condición como Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="d1b68-107">For example, you might set up an alert for a condition like hello following:</span></span>

`If there are zero input events in hello last 5 minutes, send email notification toosa-admin@example.com`

<span data-ttu-id="d1b68-108">Las reglas se puede configurar las métricas a través del portal de Hola o pueden configurarse [mediante programación](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) sobre datos de registros de operaciones.</span><span class="sxs-lookup"><span data-stu-id="d1b68-108">Rules can be set up on metrics through hello portal, or can be configured [programmatically](https://code.msdn.microsoft.com/windowsazure/Receive-Email-Notifications-199e2c9a) over Operation Logs data.</span></span>

## <a name="set-up-alerts-in-hello-azure-portal"></a><span data-ttu-id="d1b68-109">Configurar alertas en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b68-109">Set up alerts in hello Azure portal</span></span>
1. <span data-ttu-id="d1b68-110">Hola portal de Azure, abra el trabajo de análisis de transmisiones de hello para que desea toocreate una alerta.</span><span class="sxs-lookup"><span data-stu-id="d1b68-110">In hello Azure portal, open hello Stream Analytics job you want toocreate an alert for.</span></span> 

2. <span data-ttu-id="d1b68-111">Hola **trabajo** hoja, haga clic en hello **supervisión** sección.</span><span class="sxs-lookup"><span data-stu-id="d1b68-111">In hello **Job** blade, click hello **Monitoring** section.</span></span>  

3. <span data-ttu-id="d1b68-112">Hola **métrica** hoja, haga clic en hello **Agregar alerta** comando.</span><span class="sxs-lookup"><span data-stu-id="d1b68-112">In hello **Metric** blade, click hello **Add alert** command.</span></span>

      ![Configuración de Azure Portal](./media/stream-analytics-set-up-alerts/06-stream-analytics-set-up-alerts.png)  

4. <span data-ttu-id="d1b68-114">Escriba un nombre y una descripción.</span><span class="sxs-lookup"><span data-stu-id="d1b68-114">Enter a name and a description.</span></span>

5. <span data-ttu-id="d1b68-115">Usar Hola selectores toodefine Hola condición bajo qué Hola se envía la alerta.</span><span class="sxs-lookup"><span data-stu-id="d1b68-115">Use hello selectors toodefine hello condition under which hello alert will be sent.</span></span>

6. <span data-ttu-id="d1b68-116">Proporciona información sobre dónde debe ir alerta Hola.</span><span class="sxs-lookup"><span data-stu-id="d1b68-116">Provide information about where hello alert should go.</span></span>

      ![Configuración de una alerta para un trabajo Azure Stream Analytics](./media/stream-analytics-set-up-alerts/stream-analytics-add-alert.png)  

<span data-ttu-id="d1b68-118">Para obtener más información acerca de cómo configurar alertas en hello portal de Azure, consulte [recibir notificaciones de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="d1b68-118">For more detail on configuring alerts in hello Azure portal, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).</span></span>  


## <a name="get-help"></a><span data-ttu-id="d1b68-119">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="d1b68-119">Get help</span></span>
<span data-ttu-id="d1b68-120">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="d1b68-120">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1b68-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d1b68-121">Next steps</span></span>
* [<span data-ttu-id="d1b68-122">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="d1b68-122">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d1b68-123">Introducción al uso de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b68-123">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="d1b68-124">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b68-124">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d1b68-125">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="d1b68-125">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d1b68-126">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d1b68-126">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

