---
title: "Solución de problemas de trabajos de Azure Data Lake Analytics mediante Azure Portal | Microsoft Docs"
description: "Aprenda a usar el Portal de Azure para solucionar problemas de trabajos de Análisis de Data Lake. "
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
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="a64a8-103">Solución de problemas de trabajos de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a64a8-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="a64a8-104">Aprenda a usar el Portal de Azure para solucionar problemas de trabajos de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a64a8-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="a64a8-105">En este tutorial, configurará un problema con un archivo de origen que falta y usará el Portal de Azure para solucionar el problema.</span><span class="sxs-lookup"><span data-stu-id="a64a8-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="a64a8-106">Envío de un trabajo de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="a64a8-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="a64a8-107">Envíe el siguiente trabajo de U-SQL:</span><span class="sxs-lookup"><span data-stu-id="a64a8-107">Submit the following U-SQL job:</span></span>

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
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="a64a8-108">El archivo de origen definido en el script es **/Samples/Data/SearchLog.tsv1**, pero debería ser **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="a64a8-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="a64a8-109">Solución de problemas del trabajo</span><span class="sxs-lookup"><span data-stu-id="a64a8-109">Troubleshoot the job</span></span>

<span data-ttu-id="a64a8-110">**Para ver todos los trabajos**</span><span class="sxs-lookup"><span data-stu-id="a64a8-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="a64a8-111">En el Portal de Azure, haga clic en **Microsoft Azure** en la esquina superior izquierda.</span><span class="sxs-lookup"><span data-stu-id="a64a8-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="a64a8-112">Haga clic en el icono con el nombre de la cuenta de Análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a64a8-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="a64a8-113">Se muestra el resumen del trabajo en el icono **Administración de trabajos** .</span><span class="sxs-lookup"><span data-stu-id="a64a8-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Administración de trabajos de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="a64a8-115">La administración de trabajos ofrece información general del estado del trabajo.</span><span class="sxs-lookup"><span data-stu-id="a64a8-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="a64a8-116">Observe que hay un trabajo con error.</span><span class="sxs-lookup"><span data-stu-id="a64a8-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="a64a8-117">Haga clic en el icono **Administración de trabajo** para ver los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a64a8-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="a64a8-118">Los trabajos se organizan por las categorías **En ejecución**, **En cola** y **Terminado**.</span><span class="sxs-lookup"><span data-stu-id="a64a8-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="a64a8-119">Verá el trabajo con error en el **Terminado** .</span><span class="sxs-lookup"><span data-stu-id="a64a8-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="a64a8-120">Deberá ser el primero de la lista.</span><span class="sxs-lookup"><span data-stu-id="a64a8-120">It shall be first one in the list.</span></span> <span data-ttu-id="a64a8-121">Si tiene una gran cantidad de trabajos, haga clic en **Filtro** para ayudarle a localizar los trabajos.</span><span class="sxs-lookup"><span data-stu-id="a64a8-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Trabajos de filtro de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="a64a8-123">Haga clic en el trabajo con error en la lista para abrir los detalles de dicho trabajo en una nueva hoja:</span><span class="sxs-lookup"><span data-stu-id="a64a8-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="a64a8-125">Observe el **Reenviar** botón.</span><span class="sxs-lookup"><span data-stu-id="a64a8-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="a64a8-126">Después de corregir el problema, puede volver a enviar el trabajo.</span><span class="sxs-lookup"><span data-stu-id="a64a8-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="a64a8-127">Haga clic en la parte resaltada de la captura de pantalla anterior para abrir los detalles del error.</span><span class="sxs-lookup"><span data-stu-id="a64a8-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="a64a8-128">Verá algo parecido a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a64a8-128">You shall see something like:</span></span>

    ![Detalles de trabajos con error de Análisis de Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="a64a8-130">Indica que no se encuentra la carpeta de origen.</span><span class="sxs-lookup"><span data-stu-id="a64a8-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="a64a8-131">Haga clic en **Duplicar script**.</span><span class="sxs-lookup"><span data-stu-id="a64a8-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="a64a8-132">Actualización de la ruta de acceso **DESDE** a lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a64a8-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="a64a8-133">"/ Samples/Data/SearchLog.tsv"</span><span class="sxs-lookup"><span data-stu-id="a64a8-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="a64a8-134">Haga clic en **Enviar trabajo**.</span><span class="sxs-lookup"><span data-stu-id="a64a8-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="a64a8-135">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a64a8-135">See also</span></span>
* [<span data-ttu-id="a64a8-136">Información general de Análisis de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a64a8-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="a64a8-137">Introducción a Análisis de Azure Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a64a8-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="a64a8-138">Introducción a Análisis de Azure Data Lake y a U-SQL mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a64a8-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="a64a8-139">Administración de Análisis de Azure Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a64a8-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
