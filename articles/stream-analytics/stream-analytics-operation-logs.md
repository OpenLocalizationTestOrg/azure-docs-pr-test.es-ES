---
title: "aaaDebug mediante registros de operación y el servicio de análisis de transmisiones | Documentos de Microsoft"
description: "Flujo de cómo toouse registros de operaciones de análisis"
keywords: registros de servicios
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: a2ed9676-f0bd-4398-87c8-a592779ac728
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3dd27706ccc879a724e1894b33d47021d972f31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="debug-stream-analytics-jobs-using-service-and-operation-logs"></a><span data-ttu-id="39d5c-104">Depuración de los trabajos de Análisis de transmisiones mediante registros de operaciones y servicios</span><span class="sxs-lookup"><span data-stu-id="39d5c-104">Debug Stream Analytics jobs using service and operation logs</span></span>
<span data-ttu-id="39d5c-105">Todos los servicios de Azure de alimentación operativa mensajes toousers toorecord detalles de registro a relacionados con operaciones de toomanagement.</span><span class="sxs-lookup"><span data-stu-id="39d5c-105">All Azure services supply operational logging messages toousers toorecord details related toomanagement operations.</span></span> <span data-ttu-id="39d5c-106">En el análisis de transmisiones de Azure, esta información puede usarse para fines de depuración como ver el estado del trabajo, el progreso del trabajo y el progreso de Hola de tootrack de mensajes de error de un trabajo con el tiempo de inicio tooprocessing toooutput.</span><span class="sxs-lookup"><span data-stu-id="39d5c-106">In Azure Stream Analytics, this information can be used for debugging purposes such as viewing job status, job progress, and failure messages tootrack hello progress of a job over time, from start tooprocessing toooutput.</span></span>

## <a name="find-operation-logs-in-hello-azure-management-portal"></a><span data-ttu-id="39d5c-107">Buscar registros de operaciones en el portal de administración de Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="39d5c-107">Find operation logs in hello Azure Management portal</span></span>
<span data-ttu-id="39d5c-108">A los registros de operaciones se puede acceder de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="39d5c-108">Operation Logs can be accessed in two ways:</span></span>  

* <span data-ttu-id="39d5c-109">Panel de trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="39d5c-109">Dashboard of hello Stream Analytics job</span></span>  
* <span data-ttu-id="39d5c-110">Servicios de administración de portal de Azure clásico de Hola</span><span class="sxs-lookup"><span data-stu-id="39d5c-110">Management Services in hello Azure Classic portal</span></span>  

## <a name="dashboard-of-hello-stream-analytics-job"></a><span data-ttu-id="39d5c-111">Panel de trabajo de análisis de transmisiones de Hola</span><span class="sxs-lookup"><span data-stu-id="39d5c-111">Dashboard of hello Stream Analytics job</span></span>
<span data-ttu-id="39d5c-112">Un toohello de vínculo correspondiente registros de un trabajo de análisis de transmisiones se muestra en la pestaña del panel del trabajo de Hola. Si hace clic en ese vínculo, establece filtros Hola de una manera que muestra registros más recientes para ese trabajo.</span><span class="sxs-lookup"><span data-stu-id="39d5c-112">A link toohello corresponding logs of a Stream Analytics job is displayed on hello job’s Dashboard tab. If you click on that link, it will set hello filters in a way that it shows latest logs for that specific job.</span></span>

  ![Selección de registros de servicios de administración](./media/stream-analytics-operation-logs/01-stream-analytics-operation-logs.png)  

## <a name="management-services"></a><span data-ttu-id="39d5c-114">Servicios de administración</span><span class="sxs-lookup"><span data-stu-id="39d5c-114">Management Services</span></span>
<span data-ttu-id="39d5c-115">toomanually navegar toohello registros de operaciones de análisis de transmisiones y otros servicios en el portal de Azure clásico de hello:</span><span class="sxs-lookup"><span data-stu-id="39d5c-115">toomanually navigate toohello Operation Logs for Stream Analytics and other services in hello Azure Classic portal:</span></span>

1. <span data-ttu-id="39d5c-116">Haga clic en **servicios de administración de** en hello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="39d5c-116">Click on **Management Services** in hello [Azure Classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="39d5c-117">Seleccione **análisis de transmisiones** para **tipo** y el nombre de Hola Hola del trabajo de para **nombre del servicio**.</span><span class="sxs-lookup"><span data-stu-id="39d5c-117">Select **Stream Analytics** for **Type** and hello name of hello job for **Service Name**.</span></span>  
   
   ![Seleccionar el Análisis de transmisiones](./media/stream-analytics-operation-logs/02-stream-analytics-operation-logs.png)  

## <a name="find-audit-logs-in-hello-azure-portal"></a><span data-ttu-id="39d5c-119">Buscar registros de auditoría en hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="39d5c-119">Find audit logs in hello Azure portal</span></span>
<span data-ttu-id="39d5c-120">toofind registros operativos para el trabajo de análisis de transmisiones en hello portal de Azure, haga clic en **examinar** y, a continuación, seleccione **registros de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="39d5c-120">toofind operational logs for your Stream Analytics job in hello Azure portal, Click **Browse** and then select **Audit logs**.</span></span>

  ![Selección de Stream Analytics en Azure Portal](./media/stream-analytics-operation-logs/06-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-122">Se abrirá una hoja con los últimos 7 días para todos los recursos de eventos de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="39d5c-122">This will open a blade showing events from hello last 7 days for all resources in your subscription.</span></span>  <span data-ttu-id="39d5c-123">Puede filtrar eventos de toosee de un tipo de especificar o el período de tiempo, haga clic en hello **filtro** comando.</span><span class="sxs-lookup"><span data-stu-id="39d5c-123">You can filter toosee events of a specify type or time frame by clicking hello **Filter** command.</span></span>

  ![Selección de Stream Analytics en Azure Portal](./media/stream-analytics-operation-logs/07-stream-analytics-operation-logs.png)  

## <a name="get-log-details"></a><span data-ttu-id="39d5c-125">Obtención de detalles de registro</span><span class="sxs-lookup"><span data-stu-id="39d5c-125">Get log details</span></span>
<span data-ttu-id="39d5c-126">Puede filtrar por intervalo de tiempo y registros de estado tooview hello para el trabajo.</span><span class="sxs-lookup"><span data-stu-id="39d5c-126">You can filter by Time Range and Status tooview hello logs for your job.</span></span>

<span data-ttu-id="39d5c-127">En el portal de administración de Azure de hello, haga clic en hello **detalles** situado en la parte inferior de Hola de hello ventana tooview más detalles sobre un evento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="39d5c-127">In hello Azure Management portal, click on hello **Details** button at hello bottom of hello window tooview more details about a selected event.</span></span> 

  ![Seleccionar detalles](./media/stream-analytics-operation-logs/03-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-129">Hola portal de Azure, haga clic en un toosee de entrada de registro Hola eventos detallados dentro de él.</span><span class="sxs-lookup"><span data-stu-id="39d5c-129">In hello Azure portal, click on a log entry toosee hello detailed events inside it.</span></span>

  ![Selección de detalles en Azure Portal](./media/stream-analytics-operation-logs/08-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-131">Desde aquí, puede abrir hello **detalle** hoja haciendo clic en el evento de Hola.</span><span class="sxs-lookup"><span data-stu-id="39d5c-131">From there, you can open hello **Detail** blade by clicking on hello event.</span></span>

  ![Selección de detalles en Azure Portal](./media/stream-analytics-operation-logs/09-stream-analytics-operation-logs.png)  

## <a name="debug-a-failed-job"></a><span data-ttu-id="39d5c-133">Depuración de un trabajo con error</span><span class="sxs-lookup"><span data-stu-id="39d5c-133">Debug a failed job</span></span>
<span data-ttu-id="39d5c-134">En el portal de administración de Azure de hello, haga clic en el icono de búsqueda de Hola y escriba 'Error'.</span><span class="sxs-lookup"><span data-stu-id="39d5c-134">In hello Azure Management portal, click on hello Search icon and type ‘failed’.</span></span> <span data-ttu-id="39d5c-135">Esto genera todos los registros con errores.</span><span class="sxs-lookup"><span data-stu-id="39d5c-135">This gives a result of all logs with failures.</span></span> 

  ![Depuración de un trabajo con error](./media/stream-analytics-operation-logs/04-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-137">Hola portal de Azure, puede filtrar por nivel de mensaje tooview **crítico** eventos.</span><span class="sxs-lookup"><span data-stu-id="39d5c-137">In hello Azure portal, you can filter by level of message tooview **Critical** events.</span></span>

  ![Depuración en Azure Portal](./media/stream-analytics-operation-logs/10-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-139">Puede seleccionar cualquiera de los errores de Hola y haga clic en hello **detalles** para obtener más información sobre el error de Hola.</span><span class="sxs-lookup"><span data-stu-id="39d5c-139">You can select any one of hello failures, and click on hello **Details** for more information on hello error.</span></span>  <span data-ttu-id="39d5c-140">Algunos mensajes de error también proporcionan información acerca de cómo toomitigate Hola problema.</span><span class="sxs-lookup"><span data-stu-id="39d5c-140">Some error messages also provide information about how toomitigate hello issue.</span></span> 

  ![Detalles de la operación](./media/stream-analytics-operation-logs/05-stream-analytics-operation-logs.png)  

<span data-ttu-id="39d5c-142">Si necesita toocontact [compatibilidad](https://azure.microsoft.com/support/options/) o proporcionar información toohello equipo a través de hello [foro de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), detalles de la operación de hello, tenga en cuenta específicamente Hola **Id. de correlación**.</span><span class="sxs-lookup"><span data-stu-id="39d5c-142">In case you need toocontact [Support](https://azure.microsoft.com/support/options/) or provide information toohello team via hello [MSDN forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics), please note hello Operation Details, specifically hello **Correlation ID**.</span></span> 

## <a name="get-help"></a><span data-ttu-id="39d5c-143">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="39d5c-143">Get help</span></span>
<span data-ttu-id="39d5c-144">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="39d5c-144">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="39d5c-145">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="39d5c-145">Next steps</span></span>
* [<span data-ttu-id="39d5c-146">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="39d5c-146">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="39d5c-147">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="39d5c-147">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="39d5c-148">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="39d5c-148">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="39d5c-149">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="39d5c-149">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="39d5c-150">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="39d5c-150">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

