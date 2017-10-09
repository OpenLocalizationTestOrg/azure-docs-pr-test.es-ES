---
title: "Exportar tooSQL de visión de la aplicación de Azure | Documentos de Microsoft"
description: "Exportar continuamente tooSQL de datos de Application Insights mediante el análisis de transmisiones."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="a87d0-103">Tutorial: Exportar tooSQL de Application Insights mediante el análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a87d0-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="a87d0-104">Este artículo se muestra cómo toomove los datos de telemetría de [Azure Application Insights] [ start] en una base de datos de SQL Azure mediante el uso de [exportar continua] [ export] y [análisis de transmisiones de Azure](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="a87d0-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="a87d0-105">La Exportación continua traslada los datos de telemetría a Almacenamiento de Azure en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a87d0-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="a87d0-106">Comenzaremos analizar objetos JSON de hello mediante el análisis de transmisiones de Azure y crear filas en una tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="a87d0-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="a87d0-107">(Por lo general, exportar continua es Hola forma toodo su propio análisis de telemetría de hello las aplicaciones enviar tooApplication visión.</span><span class="sxs-lookup"><span data-stu-id="a87d0-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="a87d0-108">Se pueden adaptar este toodo de ejemplo de código otras cosas con la telemetría Hola exportado, como la agregación de datos.)</span><span class="sxs-lookup"><span data-stu-id="a87d0-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="a87d0-109">Comenzaremos con la suposición de Hola que ya tiene la aplicación hello desea toomonitor.</span><span class="sxs-lookup"><span data-stu-id="a87d0-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="a87d0-110">En este ejemplo, vamos a usar datos de vista de página de hello, pero hello mismo patrón se puede ampliar fácilmente los tipos de datos de tooother como eventos personalizados y las excepciones.</span><span class="sxs-lookup"><span data-stu-id="a87d0-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="a87d0-111">Agregar Application Insights tooyour aplicación</span><span class="sxs-lookup"><span data-stu-id="a87d0-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="a87d0-112">tooget iniciado:</span><span class="sxs-lookup"><span data-stu-id="a87d0-112">tooget started:</span></span>

1. <span data-ttu-id="a87d0-113">[Configure Application Insights para sus páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a87d0-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="a87d0-114">(En este ejemplo, nos centraremos en el procesamiento de datos de la vista de página de los exploradores de cliente hello, pero también puede configurar Application Insights para el lado del servidor hello de su [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) solicitud de aplicación y el proceso dependencia y otro servidor de telemetría.)</span><span class="sxs-lookup"><span data-stu-id="a87d0-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="a87d0-115">Publique la aplicación y vea los datos de telemetría que aparecen en el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="a87d0-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="a87d0-116">Creación de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="a87d0-116">Create storage in Azure</span></span>
<span data-ttu-id="a87d0-117">Exportación continua siempre genera cuenta de almacenamiento de Azure de tooan de datos, por lo que necesita almacenamiento de hello toocreate en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="a87d0-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="a87d0-118">Crear una cuenta de almacenamiento en su suscripción en hello [portal de Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="a87d0-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![En el portal de Azure, elija Nuevo, Datos, Almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="a87d0-122">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="a87d0-122">Create a container</span></span>
   
    ![En un almacenamiento nuevo hello, seleccionar contenedores, haga clic en el icono de contenedores de hello y, a continuación, agregar](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="a87d0-124">Copie la clave de acceso de almacenamiento de Hola</span><span class="sxs-lookup"><span data-stu-id="a87d0-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="a87d0-125">Necesitará pronto tooset seguridad de servicio de análisis de secuencia de entrada toohello Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![En el almacenamiento de hello, abra la configuración, claves y realizar una copia de la clave de acceso principal de Hola](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="a87d0-127">Iniciar exportación continua tooAzure almacenamiento</span><span class="sxs-lookup"><span data-stu-id="a87d0-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="a87d0-128">Hola portal de Azure, examinar recursos de Application Insights toohello que creó para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a87d0-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Elija Examinar, Application Insights, su aplicación.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="a87d0-130">Cree una exportación continua.</span><span class="sxs-lookup"><span data-stu-id="a87d0-130">Create a continuous export.</span></span>
   
    ![Elija Configuración, Exportación continua, Agregar.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="a87d0-132">Seleccione la cuenta de almacenamiento de Hola que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a87d0-132">Select hello storage account you created earlier:</span></span>

    ![Establecer el destino de la exportación de Hola](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="a87d0-134">Establecer a tipos de evento de hello que desea toosee:</span><span class="sxs-lookup"><span data-stu-id="a87d0-134">Set hello event types you want toosee:</span></span>

    ![Elija los tipos de evento.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="a87d0-136">Permita que se acumulen algunos datos.</span><span class="sxs-lookup"><span data-stu-id="a87d0-136">Let some data accumulate.</span></span> <span data-ttu-id="a87d0-137">Póngase cómo y deje que los usuarios usen su aplicación durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="a87d0-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="a87d0-138">Así, aparecerá la telemetría y verá gráficos estadísticos en el [explorador de métricas](app-insights-metrics-explorer.md) y eventos individuales en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a87d0-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="a87d0-139">Y además, los datos de hello exportará tooyour almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a87d0-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="a87d0-140">Inspeccionar los datos de hello exportado, ya sea en el portal de hello - elegir **examinar**, seleccione la cuenta de almacenamiento y, a continuación, **contenedores** - o en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a87d0-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="a87d0-141">En Visual Studio, elija **Ver/Cloud Explorer** y abra Azure/Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a87d0-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="a87d0-142">(Si no tiene esta opción de menú, necesita tooinstall hello Azure SDK: abra el cuadro de diálogo de proyecto nuevo de Hola y abra Visual C# / nube / obtener Microsoft Azure SDK para. NET.)</span><span class="sxs-lookup"><span data-stu-id="a87d0-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![En Visual Studio, abra Explorador de servidores, Azure, Almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="a87d0-144">Tome nota de la parte común de Hola de nombre de ruta de acceso de hello, que se deriva de la clave de nombre e instrumentación de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="a87d0-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="a87d0-145">eventos de Hola se escriben tooblob archivos en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="a87d0-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="a87d0-146">Cada archivo puede contener uno o varios eventos.</span><span class="sxs-lookup"><span data-stu-id="a87d0-146">Each file may contain one or more events.</span></span> <span data-ttu-id="a87d0-147">Por lo que nos gustaría datos de eventos de tooread hello y filtrar campos Hola que queremos.</span><span class="sxs-lookup"><span data-stu-id="a87d0-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="a87d0-148">Hay todo tipo de cosas, que podríamos hacer con los datos de hello, pero nuestro plan hoy en día es toouse análisis de transmisiones toomove Hola datos tooa base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a87d0-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="a87d0-149">Que le resultará fácil toorun una gran cantidad de consultas interesantes.</span><span class="sxs-lookup"><span data-stu-id="a87d0-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="a87d0-150">Creación de una Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a87d0-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="a87d0-151">Una vez más a partir de su suscripción en [portal de Azure][portal], crear base de datos de hello (y un servidor nuevo, a menos que ya tiene uno) toowhich escribirá los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Nuevo, Datos, SQL.](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="a87d0-153">Asegúrese de que ese servidor de base de datos de hello permite acceso a los servicios de tooAzure:</span><span class="sxs-lookup"><span data-stu-id="a87d0-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Examinar, los servidores, el servidor, configuración, Firewall, permitir el acceso a tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="a87d0-155">Creación de una tabla en la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a87d0-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="a87d0-156">Conectar la base de datos de toohello creada en la sección anterior de hello con la herramienta de administración preferido.</span><span class="sxs-lookup"><span data-stu-id="a87d0-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="a87d0-157">En este tutorial, usaremos [Herramientas de administración de SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="a87d0-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="a87d0-158">Cree una nueva consulta y ejecute hello después de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="a87d0-158">Create a new query, and execute hello following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="a87d0-159">En este ejemplo, usamos datos de vistas de página.</span><span class="sxs-lookup"><span data-stu-id="a87d0-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="a87d0-160">toosee Hola otros datos disponibles, inspeccionar la salida JSON y vea hello [Exportar modelo de datos](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a87d0-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="a87d0-161">Creación de una instancia de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="a87d0-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="a87d0-162">De hello [Portal de Azure clásico](https://manage.windowsazure.com/), seleccione servicio de análisis de transmisiones de Azure de Hola y crear un nuevo trabajo de análisis de transmisiones:</span><span class="sxs-lookup"><span data-stu-id="a87d0-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="a87d0-163">Cuando se crea el nuevo trabajo de hello, expandir los detalles:</span><span class="sxs-lookup"><span data-stu-id="a87d0-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="a87d0-164">Establecimiento de la ubicación del blob</span><span class="sxs-lookup"><span data-stu-id="a87d0-164">Set blob location</span></span>
<span data-ttu-id="a87d0-165">Establézcalo tootake entrada desde el blob exportar continua:</span><span class="sxs-lookup"><span data-stu-id="a87d0-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="a87d0-166">Ahora deberá Hola clave de acceso principal de la cuenta de almacenamiento, que se ha indicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="a87d0-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="a87d0-167">Utilizar esta configuración como Hola clave de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a87d0-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="a87d0-168">Establecimiento del patrón del prefijo de la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="a87d0-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="a87d0-169">Sea seguro tooset Hola formato de fecha demasiado**aaaa-MM-DD** (con **guiones**).</span><span class="sxs-lookup"><span data-stu-id="a87d0-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="a87d0-170">Hola modelo de prefijo de ruta de acceso especifica cómo el análisis de transmisiones encuentra archivos de entrada de hello en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="a87d0-171">Necesita tooset se toohow toocorrespond exportar continua almacena los datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="a87d0-172">Configúrelo como este caso que se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="a87d0-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="a87d0-173">En este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="a87d0-173">In this example:</span></span>

* <span data-ttu-id="a87d0-174">`webapplication27`es Hola nombre de recurso de Application Insights, hello **todo en minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="a87d0-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="a87d0-175">`1234...`es la clave de instrumentación Hola de hello recursos de Application Insights **con guiones quitados**.</span><span class="sxs-lookup"><span data-stu-id="a87d0-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="a87d0-176">`PageViews`es el tipo de saludo de datos que deseamos tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="a87d0-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="a87d0-177">los tipos disponibles de Hello dependen de filtro de Hola que se establezca en Exportar continua.</span><span class="sxs-lookup"><span data-stu-id="a87d0-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="a87d0-178">Examinar Hola Hola de toosee de los datos exportados en otros tipos disponibles y ver hello [Exportar modelo de datos](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a87d0-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="a87d0-179">`/{date}/{time}` es un patrón escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="a87d0-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="a87d0-180">nombre de hello tooget y iKey de su recurso de Application Insights, abra Essentials en su página de información general, o abra la configuración.</span><span class="sxs-lookup"><span data-stu-id="a87d0-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="a87d0-181">Finalización de la instalación inicial</span><span class="sxs-lookup"><span data-stu-id="a87d0-181">Finish initial setup</span></span>
<span data-ttu-id="a87d0-182">Confirme el formato de serialización de hello:</span><span class="sxs-lookup"><span data-stu-id="a87d0-182">Confirm hello serialization format:</span></span>

![Confirme y cierre el asistente.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="a87d0-184">Cerrar el Asistente de Hola y espere Hola el programa de instalación toocomplete.</span><span class="sxs-lookup"><span data-stu-id="a87d0-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="a87d0-185">Utilice toocheck de función de ejemplo Hola que ha establecido correctamente ruta de acceso de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="a87d0-186">Si se produce un error: Compruebe que hay datos en el almacenamiento de hello para el intervalo de tiempo de ejemplo de Hola que eligió.</span><span class="sxs-lookup"><span data-stu-id="a87d0-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="a87d0-187">Editar definición de entrada de Hola y compruebe que establece la cuenta de almacenamiento de hello, el prefijo de ruta de acceso y correctamente el formato de fecha.</span><span class="sxs-lookup"><span data-stu-id="a87d0-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="a87d0-188">Establecimiento de la consulta</span><span class="sxs-lookup"><span data-stu-id="a87d0-188">Set query</span></span>
<span data-ttu-id="a87d0-189">Abra la sección de la consulta de hello:</span><span class="sxs-lookup"><span data-stu-id="a87d0-189">Open hello query section:</span></span>

![En Análisis de transmisiones, seleccione Consulta.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="a87d0-191">Reemplace la consulta predeterminada de hello con:</span><span class="sxs-lookup"><span data-stu-id="a87d0-191">Replace hello default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="a87d0-192">Tenga en cuenta que primero Hola algunas propiedades son datos de la vista de toopage específico.</span><span class="sxs-lookup"><span data-stu-id="a87d0-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="a87d0-193">Las exportaciones de otros tipos de telemetría tendrán diferentes propiedades.</span><span class="sxs-lookup"><span data-stu-id="a87d0-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="a87d0-194">Vea hello [detallada de la referencia del modelo de datos para los valores y tipos de propiedad Hola.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="a87d0-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="a87d0-195">Configurar la salida toodatabase</span><span class="sxs-lookup"><span data-stu-id="a87d0-195">Set up output toodatabase</span></span>
<span data-ttu-id="a87d0-196">Seleccionar SQL como salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a87d0-196">Select SQL as hello output.</span></span>

![En Análisis de transmisiones, seleccione Salidas.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="a87d0-198">Especifique la base de datos SQL de Hola.</span><span class="sxs-lookup"><span data-stu-id="a87d0-198">Specify hello SQL database.</span></span>

![Rellene los detalles de saludo de la base de datos](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="a87d0-200">Cierre el Asistente de Hola y espere a que una notificación que se configuró la salida de hello.</span><span class="sxs-lookup"><span data-stu-id="a87d0-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="a87d0-201">Inicio del procesamiento</span><span class="sxs-lookup"><span data-stu-id="a87d0-201">Start processing</span></span>
<span data-ttu-id="a87d0-202">Iniciar el trabajo de Hola desde la barra de acciones de hello:</span><span class="sxs-lookup"><span data-stu-id="a87d0-202">Start hello job from hello action bar:</span></span>

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="a87d0-204">Puede elegir si el procesamiento de toostart Hola datos a partir de ahora o toostart con los datos anteriores.</span><span class="sxs-lookup"><span data-stu-id="a87d0-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="a87d0-205">Hola este último resulta útil si han tenido exportar continua ya ejecutando durante algún tiempo.</span><span class="sxs-lookup"><span data-stu-id="a87d0-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="a87d0-207">Después de unos minutos, vuelva atrás tooSQL herramientas de administración de servidor y ver Hola datos que fluyen en.</span><span class="sxs-lookup"><span data-stu-id="a87d0-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="a87d0-208">Por ejemplo, utilice una consulta como esta:</span><span class="sxs-lookup"><span data-stu-id="a87d0-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="a87d0-209">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="a87d0-209">Related articles</span></span>
* [<span data-ttu-id="a87d0-210">Exportar tooPowerBI mediante el análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a87d0-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="a87d0-211">Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.</span><span class="sxs-lookup"><span data-stu-id="a87d0-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="a87d0-212">Exportación continua en Application Insights</span><span class="sxs-lookup"><span data-stu-id="a87d0-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="a87d0-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a87d0-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

