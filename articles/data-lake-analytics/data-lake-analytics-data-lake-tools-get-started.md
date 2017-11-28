---
title: las secuencias de comandos de aaaDevelop U-SQL mediante Data Lake Tools para Visual Studio | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooinstall Data Lake Tools para Visual Studio y cómo las secuencias de comandos SQL U toodevelop y prueba."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="84767-103">Desarrollo de scripts U-SQL mediante Data Lake Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84767-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="84767-104">Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake de toocreate de toouse Visual Studio, definir trabajos en [U-SQL](data-lake-analytics-u-sql-get-started.md)y enviar el servicio de análisis de Data Lake toohello de trabajos.</span><span class="sxs-lookup"><span data-stu-id="84767-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="84767-105">Para obtener más información acerca de Análisis de Data Lake, consulte [Información general sobre Análisis de Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84767-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="84767-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="84767-106">Prerequisites</span></span>

* <span data-ttu-id="84767-107">**Visual Studio**: se admiten todas las ediciones, excepto Express.</span><span class="sxs-lookup"><span data-stu-id="84767-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="84767-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="84767-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="84767-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="84767-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="84767-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="84767-110">Visual Studio 2013</span></span>
* <span data-ttu-id="84767-111">**Microsoft Azure SDK para .NET** versión 2.7.1, o posterior.</span><span class="sxs-lookup"><span data-stu-id="84767-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="84767-112">Instalar mediante hello [instalador de plataforma Web](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="84767-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="84767-113">Una cuenta de **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="84767-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="84767-114">toocreate una cuenta, consulte [empezar a trabajar con análisis de Data Lake de Azure mediante el portal de Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84767-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="84767-115">Instalación de Herramientas de Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84767-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="84767-116">Descargue e instale Azure Data Lake Tools para Visual Studio [desde el centro de descarga de hello](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="84767-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="84767-117">Después de la instalación tenga en cuenta que:</span><span class="sxs-lookup"><span data-stu-id="84767-117">After installation, note that:</span></span>
* <span data-ttu-id="84767-118">Hola **Explorador de servidores** > **Azure** nodo contiene un **análisis de Data Lake** nodo.</span><span class="sxs-lookup"><span data-stu-id="84767-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="84767-119">Hola **herramientas** menú tiene un **Data Lake** elemento.</span><span class="sxs-lookup"><span data-stu-id="84767-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="84767-120">Conectar con cuenta de análisis de Azure Data Lake tooan</span><span class="sxs-lookup"><span data-stu-id="84767-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="84767-121">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="84767-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="84767-122">Abra el Explorador de servidores, para lo que debe seleccionar **Vista** > **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="84767-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="84767-123">Haga clic con el botón derecho en **Azure**.</span><span class="sxs-lookup"><span data-stu-id="84767-123">Right-click **Azure**.</span></span> <span data-ttu-id="84767-124">A continuación, seleccione **conectar tooMicrosoft suscripción de Azure** y siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="84767-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="84767-125">En el Explorador de servidores, seleccione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="84767-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="84767-126">Verá una lista de las cuentas de Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="84767-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="84767-127">Escriba el primer script U-SQL</span><span class="sxs-lookup"><span data-stu-id="84767-127">Write your first U-SQL script</span></span>

<span data-ttu-id="84767-128">Hola después de texto es un script U-SQL simple.</span><span class="sxs-lookup"><span data-stu-id="84767-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="84767-129">Define un conjunto de datos pequeño y escrituras de almacén de forma predeterminada Data Lake de conjunto de datos toohello como un archivo denominado `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="84767-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="84767-130">Envío de un trabajo de Análisis de Data Lake</span><span class="sxs-lookup"><span data-stu-id="84767-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="84767-131">Seleccione **Archivo** > **Nuevo** > **Proyecto**.</span><span class="sxs-lookup"><span data-stu-id="84767-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="84767-132">Seleccione hello **U-SQL proyecto** escriba y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="84767-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="84767-133">Visual Studio crea una solución con un archivo **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="84767-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="84767-134">Pegue el script anterior de hello en hello **Script.usql** ventana.</span><span class="sxs-lookup"><span data-stu-id="84767-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="84767-135">En la esquina superior izquierda de Hola de hello **Script.usql** ventana, especifique la cuenta de análisis de Data Lake Hola.</span><span class="sxs-lookup"><span data-stu-id="84767-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Enviar proyecto U-SQL de Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="84767-137">En la esquina superior izquierda de Hola de hello **Script.usql** ventana, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="84767-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="84767-138">Comprobar hello **cuenta Analytics**y, a continuación, seleccione **enviar**.</span><span class="sxs-lookup"><span data-stu-id="84767-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="84767-139">Resultados de envío están disponibles en hello Data Lake Tools para resultados de Visual Studio, una vez completada la presentación de Hola.</span><span class="sxs-lookup"><span data-stu-id="84767-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Enviar proyecto U-SQL de Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="84767-141">toosee hello más reciente trabajo estado y la actualización de pantalla de bienvenida, haga clic en **actualizar**.</span><span class="sxs-lookup"><span data-stu-id="84767-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="84767-142">Cuando se realiza correctamente el trabajo de hello, muestra hello **trabajo gráfico**, **las operaciones de metadatos**, **historial de estado**, y **diagnósticos**:</span><span class="sxs-lookup"><span data-stu-id="84767-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Gráfico de rendimiento del trabajo de Data Lake Analytics de U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="84767-144">**Resumen de trabajo** muestra Hola resumen del trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="84767-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="84767-145">**Detalles del trabajo** muestra información más específica sobre el trabajo de hello, incluidos los script de Hola, los recursos y los vértices.</span><span class="sxs-lookup"><span data-stu-id="84767-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="84767-146">**Gráfico de trabajo** muestra el progreso de Hola de trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="84767-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="84767-147">**Las operaciones de metadatos** muestra todas las acciones de Hola que se realizaron en el catálogo de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="84767-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="84767-148">**Datos** muestra todas las entradas de Hola y salidas.</span><span class="sxs-lookup"><span data-stu-id="84767-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="84767-149">**Diagnósticos** proporciona un análisis avanzado para la optimización de rendimiento y la ejecución del trabajo.</span><span class="sxs-lookup"><span data-stu-id="84767-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="84767-150">estado del trabajo toocheck</span><span class="sxs-lookup"><span data-stu-id="84767-150">toocheck job state</span></span>

1. <span data-ttu-id="84767-151">En el Explorador de servidores, seleccione **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="84767-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="84767-152">Expanda el nombre de la cuenta de hello análisis de Data Lake.</span><span class="sxs-lookup"><span data-stu-id="84767-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="84767-153">Haga doble clic en **Trabajos**.</span><span class="sxs-lookup"><span data-stu-id="84767-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="84767-154">Seleccione el trabajo de Hola que ha enviado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="84767-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="84767-155">salida de hello toosee de un trabajo</span><span class="sxs-lookup"><span data-stu-id="84767-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="84767-156">En el Explorador de servidores, buscar trabajo toohello que ha enviado.</span><span class="sxs-lookup"><span data-stu-id="84767-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="84767-157">Haga clic en hello **datos** ficha.</span><span class="sxs-lookup"><span data-stu-id="84767-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="84767-158">Hola **salidas de trabajo** ficha, seleccione hello `"/data.csv"` archivo.</span><span class="sxs-lookup"><span data-stu-id="84767-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84767-159">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="84767-159">Next steps</span></span>

* [<span data-ttu-id="84767-160">Prueba y depuración de trabajos U-SQL mediante la ejecución local y el SDK de U-SQL para Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="84767-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="84767-161">Depuración de trabajos U-SQL</span><span class="sxs-lookup"><span data-stu-id="84767-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="84767-162">Usar hello Azure Data Lake Tools para Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="84767-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
