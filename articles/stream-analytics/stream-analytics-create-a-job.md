---
title: "aaaHow toocreate un trabajo de procesamiento de análisis de datos para análisis de transmisiones | Documentos de Microsoft"
description: "Creación de un trabajo de procesamiento de análisis de datos para Análisis de transmisiones | segmento de ruta de aprendizaje."
keywords: "procesamiento de análisis de datos"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: e825fbcf-69e9-443f-b402-3b7a4568f415
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: d4a3c89d8862d59688d06a1719b063efa2ab1c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-data-analytics-processing-job-for-stream-analytics"></a><span data-ttu-id="47bdc-104">¿Cómo toocreate trabajo de un procesamiento de análisis de datos para análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="47bdc-104">How toocreate a data analytics processing job for Stream Analytics</span></span>
<span data-ttu-id="47bdc-105">recurso de nivel superior de Hello en análisis de transmisiones de Azure es un trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="47bdc-105">hello top-level resource in Azure Stream Analytics is a Stream Analytics Job.</span></span>  <span data-ttu-id="47bdc-106">Consta de uno o más orígenes de datos, una consulta de expresar la transformación de datos de Hola y uno o varios destinos de salida que se escriben los resultados en de la entrada.</span><span class="sxs-lookup"><span data-stu-id="47bdc-106">It consists of one or more input data sources, a query expressing hello data transformation, and one or more output targets that results are written to.</span></span> <span data-ttu-id="47bdc-107">Conjuntamente estas instrucciones permiten analizar los datos Hola usuarios tooperform escenarios de procesamiento de datos de transmisión por secuencias.</span><span class="sxs-lookup"><span data-stu-id="47bdc-107">Together these enable hello user tooperform data analytics processing for streaming data scenarios.</span></span>

<span data-ttu-id="47bdc-108">toostart mediante el análisis de transmisiones, empiece por crear un nuevo trabajo de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="47bdc-108">toostart using Stream Analytics, begin by creating a new Stream Analytics job.</span></span>  <span data-ttu-id="47bdc-109">Tenga en cuenta que esta acción no tendrá ningún implicaciones de facturación hasta que se inicie el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-109">Note this action has no billing implications until hello job is started.</span></span>

1. <span data-ttu-id="47bdc-110">Inicie sesión en hello en línea [portal de Azure clásico](http://manage.windowsazure.com) o hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="47bdc-110">Sign in on hello online [Azure classic portal](http://manage.windowsazure.com) or hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="47bdc-111">En el portal de hello: **haga clic en nuevo**, a continuación, haga clic en **Data Services** o **análisis de datos** según el portal y, a continuación, haga clic en **análisis de transmisiones de Azure** o **transmitir análisis** y, a continuación, **creación rápida**.</span><span class="sxs-lookup"><span data-stu-id="47bdc-111">In hello portal: **Click New**, then click **Data Services** or **Data Analytics** depending on your portal and then click **Azure Stream Analytics** or **Stream Analytics** and then **Quick Create**.</span></span>
   
   ![Asistente para trabajos de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/1-stream-analytics-create-a-job.png)  
   
   ![Creación de un trabajo de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/4-stream-analytics-create-a-job.png)  
3. <span data-ttu-id="47bdc-114">Especificar configuración deseada de hello para el trabajo de análisis de transmisiones de Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-114">Specify hello desired configuration for hello Stream Analytics job.</span></span>
   
   * <span data-ttu-id="47bdc-115">Hola **nombre del trabajo** cuadro, escriba un trabajo de análisis de transmisiones de nombre tooidentify Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-115">In hello **Job Name** box, enter a name tooidentify hello Stream Analytics job.</span></span> <span data-ttu-id="47bdc-116">Cuando Hola **nombre del trabajo** se valida, aparece una marca de verificación verde en el cuadro Nombre del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-116">When hello **Job Name** is validated, a green check mark appears in hello Job Name box.</span></span> <span data-ttu-id="47bdc-117">Hola **nombre del trabajo** solo pueden contener caracteres alfanuméricos y hello '-' caracteres y debe tener entre 3 y 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="47bdc-117">hello **Job Name** may contain only alphanumeric characters and hello '-' character, and must be between 3 and 63 characters.</span></span>
   * <span data-ttu-id="47bdc-118">Use **región** Hola portal de Azure o **ubicación** en hello Azure portal toospecify Hola ubicación geográfica donde desea que el trabajo de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="47bdc-118">Use **Region** in hello Azure portal or **Location** in hello Azure portal toospecify hello geographic location where you want toorun hello job.</span></span>
   * <span data-ttu-id="47bdc-119">Si utiliza hello portal de Azure, seleccione o cree una toouse de cuenta de almacenamiento como hello **cuenta de almacenamiento de supervisión Regional**.</span><span class="sxs-lookup"><span data-stu-id="47bdc-119">If using hello Azure portal, select or create a storage account toouse as hello **Regional Monitoring Storage Account**.</span></span> <span data-ttu-id="47bdc-120">Esta cuenta de almacenamiento es toostore usa datos de supervisión de todos los trabajos de análisis de transmisiones que se ejecutan en esta región.</span><span class="sxs-lookup"><span data-stu-id="47bdc-120">This storage account is used toostore monitoring data for all Stream Analytics jobs running in this region.</span></span>
   * <span data-ttu-id="47bdc-121">Si utiliza hello portal de Azure, especifique un nuevo o existente **grupo de recursos** toohold relacionados con recursos para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="47bdc-121">If using hello Azure portal, specify a new or existing **Resource Group** toohold related resources for your application.</span></span>
4. <span data-ttu-id="47bdc-122">Después de configuran nuevas opciones de trabajo de análisis de transmisiones hello, haga clic en **crear trabajo de Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="47bdc-122">Once hello new Stream Analytics job options are configured, click **Create Stream Analytics Job**.</span></span> <span data-ttu-id="47bdc-123">Puede tardar unos minutos para toobe de trabajo de análisis de transmisiones de hello creado.</span><span class="sxs-lookup"><span data-stu-id="47bdc-123">It can take a few minutes for hello Stream Analytics job toobe created.</span></span> <span data-ttu-id="47bdc-124">estado de hello toocheck, puede supervisar el progreso de hello en Centro de notificaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-124">toocheck hello status, you can monitor hello progress in hello Notifications hub.</span></span>
   
   ![Centro de notificaciones del trabajo de procesamiento de análisis de datos](./media/stream-analytics-create-a-job/2-stream-analytics-create-a-job.png)  
   
   ![Trabajo de procesamiento de análisis de datos en Azure Portal: creación del trabajo](./media/stream-analytics-create-a-job/5-stream-analytics-create-a-job.png)  
5. <span data-ttu-id="47bdc-127">nuevo trabajo de Hola mostrará el estado de **creado**.</span><span class="sxs-lookup"><span data-stu-id="47bdc-127">hello new job will show a status of **Created**.</span></span> <span data-ttu-id="47bdc-128">Tenga en cuenta que hello **iniciar** botón está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="47bdc-128">Notice that hello **Start** button is disabled.</span></span> <span data-ttu-id="47bdc-129">Configurar entrada de trabajo de hello, consulta y salida antes de iniciar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="47bdc-129">Configure hello job input, query, and output before you start hello job.</span></span>
   
   ![Trabajo de procesamiento de análisis de datos: estado del trabajo](./media/stream-analytics-create-a-job/3-stream-analytics-create-a-job.png)  
   
   ![Trabajo de procesamiento de análisis de datos en Azure Portal: estado del trabajo](./media/stream-analytics-create-a-job/6-stream-analytics-create-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="47bdc-132">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="47bdc-132">Get help</span></span>
<span data-ttu-id="47bdc-133">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="47bdc-133">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="47bdc-134">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="47bdc-134">Next steps</span></span>
* [<span data-ttu-id="47bdc-135">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="47bdc-135">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="47bdc-136">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="47bdc-136">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="47bdc-137">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="47bdc-137">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="47bdc-138">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="47bdc-138">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="47bdc-139">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="47bdc-139">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

