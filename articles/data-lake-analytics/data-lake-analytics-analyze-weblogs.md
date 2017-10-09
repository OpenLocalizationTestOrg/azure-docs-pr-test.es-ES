---
title: "registros de sitio Web de aaaAnalyze con análisis de Data Lake de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo sitio Web de tooanalyze registros con análisis de Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="e2f91-103">Análisis de registros de sitios web mediante Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e2f91-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="e2f91-104">Obtenga información acerca de cómo tooanalyze registros de sitio Web mediante el análisis de Data Lake, especialmente en averiguar qué remitentes tuvo errores cuando prueba los sitios Web de hello toovisit.</span><span class="sxs-lookup"><span data-stu-id="e2f91-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2f91-105">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e2f91-105">Prerequisites</span></span>
* <span data-ttu-id="e2f91-106">**Visual Studio 2015 o Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="e2f91-107">**[Data Lake Tools para Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="e2f91-108">Una vez instalado Data Lake Tools para Visual Studio, verá un **Data Lake** elemento Hola **herramientas** menú en Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e2f91-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![Menú de Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="e2f91-110">**Conocimientos básicos de hello Data Lake Tools para Visual Studio y análisis de Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="e2f91-111">tooget iniciado, vea:</span><span class="sxs-lookup"><span data-stu-id="e2f91-111">tooget started, see:</span></span>

  * <span data-ttu-id="e2f91-112">[Desarrollo de scripts U-SQL mediante Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="e2f91-113">**Una cuenta de Análisis de Data Lake.**</span><span class="sxs-lookup"><span data-stu-id="e2f91-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="e2f91-114">Consulte [Creación de una cuenta de Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="e2f91-115">**Cargar la cuenta de análisis de Data Lake de toohello de datos de ejemplo de Hola.**</span><span class="sxs-lookup"><span data-stu-id="e2f91-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="e2f91-116">Vea [archivos de datos de ejemplo de toocopy](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="e2f91-117">un trabajo de análisis de Data Lake toorun, necesitará algunos datos.</span><span class="sxs-lookup"><span data-stu-id="e2f91-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="e2f91-118">Aunque Hola Data Lake Tools es compatible con la carga de datos, utilizará toomake de datos de ejemplo de Hola tooupload portal Hola este tutorial toofollow más fácil.</span><span class="sxs-lookup"><span data-stu-id="e2f91-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="e2f91-119">Conectar tooAzure</span><span class="sxs-lookup"><span data-stu-id="e2f91-119">Connect tooAzure</span></span>
<span data-ttu-id="e2f91-120">Antes de que puede compilar y probar cualquier script U-SQL, debe conectarse primero tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e2f91-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="e2f91-121">**tooconnect tooData Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="e2f91-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="e2f91-122">Abra Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e2f91-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="e2f91-123">Haga clic en **Data Lake > Opciones y configuración**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="e2f91-124">Haga clic en **inicio de sesión**, o **Cambiar usuario** si alguien ha iniciado sesión en y siga las instrucciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="e2f91-125">Haga clic en **Aceptar** tooclose diálogo de opciones y configuración de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="e2f91-126">**toobrowse sus cuentas de análisis de Data Lake**</span><span class="sxs-lookup"><span data-stu-id="e2f91-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="e2f91-127">En Visual Studio, presione **CTRL+ALT+S** para abrir el **Explorador de servidores**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="e2f91-128">En el **Explorador de servidores**, expanda **Azure** y después **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="e2f91-129">Verá una lista de las cuentas de Análisis de Data Lake, si las hay.</span><span class="sxs-lookup"><span data-stu-id="e2f91-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="e2f91-130">No se puede crear cuentas de análisis de Data Lake de studio Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="e2f91-131">toocreate una cuenta, consulte [empezar a trabajar con análisis de Data Lake de Azure mediante el Portal de Azure](data-lake-analytics-get-started-portal.md) o [empezar a trabajar con análisis de Data Lake de Azure con Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="e2f91-132">Desarrollo de aplicaciones U-SQL</span><span class="sxs-lookup"><span data-stu-id="e2f91-132">Develop U-SQL application</span></span>
<span data-ttu-id="e2f91-133">Una aplicación U-SQL es principalmente un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="e2f91-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="e2f91-134">toolearn más información acerca de T-SQL, consulte [empezar a trabajar con U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="e2f91-135">Puede agregar aplicación toohello de adición operadores definidos por el usuario.</span><span class="sxs-lookup"><span data-stu-id="e2f91-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="e2f91-136">Para obtener más información, consulte [Desarrollo de operadores U-SQL definidos por el usuario para trabajos de Análisis de Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="e2f91-137">**toocreate y enviar un trabajo de análisis de Data Lake**</span><span class="sxs-lookup"><span data-stu-id="e2f91-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="e2f91-138">Haga clic en hello **archivo > Nuevo > proyecto**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="e2f91-139">Seleccione el tipo de proyecto de U-SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-139">Select hello U-SQL Project type.</span></span>

    ![nuevo proyecto de Visual Studio U-SQL](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="e2f91-141">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-141">Click **OK**.</span></span> <span data-ttu-id="e2f91-142">Visual Studio crea una solución con un archivo Script.usql.</span><span class="sxs-lookup"><span data-stu-id="e2f91-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="e2f91-143">Escriba Hola siguiente secuencia de comandos en el archivo de hello Script.usql:</span><span class="sxs-lookup"><span data-stu-id="e2f91-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="e2f91-144">Hola toounderstand T-SQL, vea [empezar a trabajar con el idioma de Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="e2f91-145">Agregue un nuevo proyecto de tooyour de script U-SQL y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e2f91-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="e2f91-146">Cambiar script U-SQL de la primera toohello atrás y siguiente toohello **enviar** botón, especifique la cuenta de análisis.</span><span class="sxs-lookup"><span data-stu-id="e2f91-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="e2f91-147">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Build Script** (Compilar script).</span><span class="sxs-lookup"><span data-stu-id="e2f91-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="e2f91-148">Comprobar los resultados de hello en el panel de salida de hello.</span><span class="sxs-lookup"><span data-stu-id="e2f91-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="e2f91-149">En el **Explorador de soluciones**, haga clic con el botón derecho en **Script.usql** y después haga clic en **Submit Script** (Enviar script).</span><span class="sxs-lookup"><span data-stu-id="e2f91-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="e2f91-150">Comprobar hello **cuenta Analytics** es hello uno donde desea toorun Hola trabajo y, a continuación, haga clic en **enviar**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="e2f91-151">Resultados de envío y vínculo de trabajo están disponibles en hello Data Lake Tools para la ventana de resultados de Visual Studio cuando se completa el envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="e2f91-152">Espere hasta que el trabajo de Hola se completa correctamente.</span><span class="sxs-lookup"><span data-stu-id="e2f91-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="e2f91-153">Si se produce un error en el trabajo de hello, probablemente falta archivo de código fuente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e2f91-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="e2f91-154">Vea la sección Requisitos previos de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="e2f91-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="e2f91-155">Para obtener más información sobre la solución de problemas, consulte [Supervisión y solución de problemas con trabajos de Análisis de Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e2f91-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="e2f91-156">Cuando se completa el trabajo de hello, verá Hola después de pantalla:</span><span class="sxs-lookup"><span data-stu-id="e2f91-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![análisis de data lake analizar registros web registros de sitios web](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="e2f91-158">Ahora repita los pasos del 7 al 10 para **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="e2f91-159">**salida del trabajo hello toosee**</span><span class="sxs-lookup"><span data-stu-id="e2f91-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="e2f91-160">De **Explorador de servidores**, expanda **Azure**, expanda **análisis de Data Lake**, expanda y su cuenta de análisis de Data Lake **decuentasdealmacenamiento**, haga clic en la cuenta de almacenamiento de datos Lake Hola predeterminada y, a continuación, haga clic en **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="e2f91-161">Haga doble clic en **ejemplos** tooopen Hola carpeta y, a continuación, haga doble clic en **salidas**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="e2f91-162">Haga doble clic en **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="e2f91-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="e2f91-163">También puede hacer doble clic archivo de salida de hello dentro de la vista de gráfico de Hola de trabajo de hello en orden toonavigate directamente toohello de salida.</span><span class="sxs-lookup"><span data-stu-id="e2f91-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="e2f91-164">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="e2f91-164">See also</span></span>
<span data-ttu-id="e2f91-165">tooget a trabajar con análisis de Data Lake con herramientas diferentes, vea:</span><span class="sxs-lookup"><span data-stu-id="e2f91-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="e2f91-166">Introducción a Análisis de Data Lake mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="e2f91-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e2f91-167">Introducción a Análisis de Data Lake mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2f91-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="e2f91-168">Introducción a Análisis de Data Lake mediante .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e2f91-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
