---
title: "trabajos de análisis de Azure Data Lake aaaTroubleshoot mediante el Portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tootroubleshoot de Portal de Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="8034f-103">Solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8034f-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="8034f-104">Obtenga información acerca de cómo toouse Hola trabajos de análisis de Data Lake tootroubleshoot de Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="8034f-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="8034f-105">En este tutorial, se la instalación de un problema de archivo de origen que faltan y utilizar hello Azure Portal tootroubleshoot Hola problema.</span><span class="sxs-lookup"><span data-stu-id="8034f-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="8034f-106">Envío de un trabajo de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="8034f-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="8034f-107">Enviar Hola después de trabajo U-SQL:</span><span class="sxs-lookup"><span data-stu-id="8034f-107">Submit hello following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="8034f-108">Hola definido en el script de Hola de archivo de origen es **/Samples/Data/SearchLog.tsv1**, donde debería ser **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="8034f-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="8034f-109">Solucionar problemas de trabajo de Hola</span><span class="sxs-lookup"><span data-stu-id="8034f-109">Troubleshoot hello job</span></span>

<span data-ttu-id="8034f-110">**toosee Hola a todos los trabajos**</span><span class="sxs-lookup"><span data-stu-id="8034f-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="8034f-111">En el portal de Azure hello, haga clic en **Microsoft Azure** en la esquina superior izquierda de Hola.</span><span class="sxs-lookup"><span data-stu-id="8034f-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="8034f-112">Haga clic en el icono de hello con su nombre de cuenta de análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="8034f-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="8034f-113">Resumen de trabajos de Hola se muestra en hello **administración del trabajo** icono.</span><span class="sxs-lookup"><span data-stu-id="8034f-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Administración de trabajos de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="8034f-115">trabajo de Hello administración le ofrece una vista de estado del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8034f-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="8034f-116">Observe que hay un trabajo con error.</span><span class="sxs-lookup"><span data-stu-id="8034f-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="8034f-117">Haga clic en hello **administración del trabajo** icono trabajos de hello toosee.</span><span class="sxs-lookup"><span data-stu-id="8034f-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="8034f-118">trabajos de Hola se clasifican en **ejecutando**, **en cola**, y **finalizado**.</span><span class="sxs-lookup"><span data-stu-id="8034f-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="8034f-119">Verá que el trabajo con errores en hello **finalizado** sección.</span><span class="sxs-lookup"><span data-stu-id="8034f-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="8034f-120">Deberá ser primera de ellas en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="8034f-120">It shall be first one in hello list.</span></span> <span data-ttu-id="8034f-121">Cuando tiene una gran cantidad de trabajos, haga clic en **filtro** toohelp se toolocate trabajos.</span><span class="sxs-lookup"><span data-stu-id="8034f-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Trabajos de filtro de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="8034f-123">Haga clic en trabajo con error Hola de detalles del trabajo de Hola Hola lista tooopen en una nueva hoja:</span><span class="sxs-lookup"><span data-stu-id="8034f-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="8034f-125">Hola aviso **reenviar** botón.</span><span class="sxs-lookup"><span data-stu-id="8034f-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="8034f-126">Después de corregir el problema de hello, puede volver a enviar el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8034f-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="8034f-127">Haga clic en la parte resaltada de detalles de hello anterior captura de pantalla tooopen Hola error.</span><span class="sxs-lookup"><span data-stu-id="8034f-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="8034f-128">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8034f-128">You shall see something like:</span></span>

    ![Detalles de trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="8034f-130">Indica que no se encuentra la carpeta de origen de Hola.</span><span class="sxs-lookup"><span data-stu-id="8034f-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="8034f-131">Haga clic en **Duplicar script**.</span><span class="sxs-lookup"><span data-stu-id="8034f-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="8034f-132">Hola de actualización **FROM** siguiente toohello de ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="8034f-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="8034f-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="8034f-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="8034f-134">Haga clic en **Enviar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="8034f-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="8034f-135">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="8034f-135">See also</span></span>
* [<span data-ttu-id="8034f-136">Información general de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="8034f-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8034f-137">Introducción a Análisis de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8034f-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="8034f-138">Introducción a Análisis de Azure Data Lake y a U-SQL mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8034f-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="8034f-139">Administración de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8034f-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
