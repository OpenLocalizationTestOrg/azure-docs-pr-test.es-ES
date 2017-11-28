---
title: "Exportación a SQL desde Azure Application Insights | Microsoft Docs"
description: "Exportación continua de datos de Application Insights a mediante el Análisis de transmisiones"
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
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="7b199-103">Tutorial: exportación a SQL desde Application Insights mediante Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7b199-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="7b199-104">En este artículo se muestra cómo trasladar los datos de telemetría desde [Azure Application Insights][start] a una instancia de Azure SQL Database mediante la [Exportación continua][export] y [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="7b199-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="7b199-105">La Exportación continua traslada los datos de telemetría a Almacenamiento de Azure en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="7b199-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="7b199-106">Analizaremos los objetos JSON mediante Análisis de transmisiones de Azure y crearemos filas en una tabla de base de datos.</span><span class="sxs-lookup"><span data-stu-id="7b199-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="7b199-107">(De manera más general, la Exportación continua es la forma de realizar su propio análisis de la telemetría que las aplicaciones envían a Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b199-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="7b199-108">Se puede adaptar este ejemplo de código para realizar otras operaciones con la telemetría exportada, como la adición de datos).</span><span class="sxs-lookup"><span data-stu-id="7b199-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="7b199-109">Comenzaremos con la suposición de que ya dispone de la aplicación que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="7b199-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="7b199-110">En este ejemplo, vamos a usar los datos de la vista de página, pero se puede ampliar fácilmente el mismo patrón a otros tipos de datos, como eventos y excepciones personalizados.</span><span class="sxs-lookup"><span data-stu-id="7b199-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="7b199-111">Agregar Application Insights a una aplicación</span><span class="sxs-lookup"><span data-stu-id="7b199-111">Add Application Insights to your application</span></span>
<span data-ttu-id="7b199-112">Primeros pasos:</span><span class="sxs-lookup"><span data-stu-id="7b199-112">To get started:</span></span>

1. <span data-ttu-id="7b199-113">[Configure Application Insights para sus páginas web](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="7b199-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="7b199-114">(En este ejemplo, nos centraremos en el procesamiento de datos de vistas de página de los exploradores cliente, pero también puede configurar Application Insights para el lado servidor de una aplicación [Java](app-insights-java-get-started.md) o [ASP.NET](app-insights-asp-net.md) y procesar peticiones, dependencias y otra telemetría de servidor).</span><span class="sxs-lookup"><span data-stu-id="7b199-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="7b199-115">Publique la aplicación y vea los datos de telemetría que aparecen en el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7b199-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="7b199-116">Creación de almacenamiento en Azure</span><span class="sxs-lookup"><span data-stu-id="7b199-116">Create storage in Azure</span></span>
<span data-ttu-id="7b199-117">La exportación continua siempre envía los datos a una cuenta de almacenamiento de Azure, por lo que necesitará crear primero el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="7b199-118">Cree una cuenta de almacenamiento en su suscripción en [Azure Portal][portal].</span><span class="sxs-lookup"><span data-stu-id="7b199-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![En el portal de Azure, elija Nuevo, Datos, Almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="7b199-122">Crear un contenedor</span><span class="sxs-lookup"><span data-stu-id="7b199-122">Create a container</span></span>
   
    ![En el nuevo almacenamiento, seleccione Contenedores, haga clic en el icono Contenedores y luego, en Agregar.](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="7b199-124">Copie la clave de acceso de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="7b199-125">La necesitará en seguida para configurar la entrada para el servicio de análisis de transmisiones.</span><span class="sxs-lookup"><span data-stu-id="7b199-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![En el almacenamiento, abra Configuración, Claves y realice una copia de la clave de acceso principal.](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="7b199-127">Inicio de la exportación continua al almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="7b199-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="7b199-128">En el portal de Azure, busque el recurso de Application Insights que ha creado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7b199-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Elija Examinar, Application Insights, su aplicación.](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="7b199-130">Cree una exportación continua.</span><span class="sxs-lookup"><span data-stu-id="7b199-130">Create a continuous export.</span></span>
   
    ![Elija Configuración, Exportación continua, Agregar.](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="7b199-132">Seleccione la cuenta de almacenamiento que creó anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7b199-132">Select the storage account you created earlier:</span></span>

    ![Establezca el destino de exportación.](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="7b199-134">Configure los tipos de eventos que desea ver:</span><span class="sxs-lookup"><span data-stu-id="7b199-134">Set the event types you want to see:</span></span>

    ![Elija los tipos de evento.](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="7b199-136">Permita que se acumulen algunos datos.</span><span class="sxs-lookup"><span data-stu-id="7b199-136">Let some data accumulate.</span></span> <span data-ttu-id="7b199-137">Póngase cómo y deje que los usuarios usen su aplicación durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="7b199-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="7b199-138">Así, aparecerá la telemetría y verá gráficos estadísticos en el [explorador de métricas](app-insights-metrics-explorer.md) y eventos individuales en la [búsqueda de diagnóstico](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="7b199-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="7b199-139">Y, además, exportará los datos en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="7b199-140">Inspeccione los datos exportados, ya sea en el portal (seleccione **Examinar**, seleccione la cuenta de almacenamiento y, después, **Contenedores**) o bien en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b199-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="7b199-141">En Visual Studio, elija **Ver/Cloud Explorer** y abra Azure/Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="7b199-142">(Si no dispone de esta opción de menú, deberá instalar el SDK de Azure: abra el cuadro de diálogo Nuevo proyecto y Visual C#/Nube/Obtener el SDK de Microsoft Azure para. NET.)</span><span class="sxs-lookup"><span data-stu-id="7b199-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![En Visual Studio, abra Explorador de servidores, Azure, Almacenamiento.](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="7b199-144">Tome nota de la parte común del nombre de la ruta de acceso, que se deriva del nombre de la aplicación y de la clave de instrumentación.</span><span class="sxs-lookup"><span data-stu-id="7b199-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="7b199-145">Los eventos se escriben en archivos de blob en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="7b199-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="7b199-146">Cada archivo puede contener uno o varios eventos.</span><span class="sxs-lookup"><span data-stu-id="7b199-146">Each file may contain one or more events.</span></span> <span data-ttu-id="7b199-147">Así, es probable que queramos leer los datos de eventos y filtrar por los campos que deseemos.</span><span class="sxs-lookup"><span data-stu-id="7b199-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="7b199-148">Se pueden realizar multitud de acciones con los datos, pero nuestro plan de hoy consiste en usar Stream Analytics para trasladar los datos a una base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="7b199-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="7b199-149">De este modo, será más sencillo ejecutar muchas consultas interesantes.</span><span class="sxs-lookup"><span data-stu-id="7b199-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="7b199-150">Creación de una Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="7b199-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="7b199-151">De nuevo, empiece desde su suscripción en [Azure Portal][portal], cree la base de datos (y un servidor, a menos que ya tenga uno) donde escribirá los datos.</span><span class="sxs-lookup"><span data-stu-id="7b199-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Nuevo, Datos, SQL.](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="7b199-153">Asegúrese de que el servidor de base de datos permite el acceso a servicios de Azure:</span><span class="sxs-lookup"><span data-stu-id="7b199-153">Make sure that the database server allows access to Azure services:</span></span>

![Examinar, Servidores, su servidor, Configuración, Firewall, Permitir acceso a Azure.](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="7b199-155">Creación de una tabla en la base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="7b199-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="7b199-156">Conéctese a la base de datos creada en la sección anterior con su herramienta preferida de administración.</span><span class="sxs-lookup"><span data-stu-id="7b199-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="7b199-157">En este tutorial, usaremos [Herramientas de administración de SQL Server](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="7b199-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="7b199-158">Cree una nueva consulta y ejecute la siguiente instrucción T-SQL:</span><span class="sxs-lookup"><span data-stu-id="7b199-158">Create a new query, and execute the following T-SQL:</span></span>

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

<span data-ttu-id="7b199-159">En este ejemplo, usamos datos de vistas de página.</span><span class="sxs-lookup"><span data-stu-id="7b199-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="7b199-160">Para ver los demás datos disponibles, observe el resultado de JSON y consulte el [modelo de exportación de datos](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b199-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="7b199-161">Creación de una instancia de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="7b199-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="7b199-162">Desde el [Portal de Azure clásico](https://manage.windowsazure.com/), seleccione el servicio Análisis de transmisiones de Azure y cree un nuevo trabajo de Análisis de transmisiones:</span><span class="sxs-lookup"><span data-stu-id="7b199-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="7b199-163">Cuando se cree el nuevo trabajo, expanda los detalles:</span><span class="sxs-lookup"><span data-stu-id="7b199-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="7b199-164">Establecimiento de la ubicación del blob</span><span class="sxs-lookup"><span data-stu-id="7b199-164">Set blob location</span></span>
<span data-ttu-id="7b199-165">Configúrelo de manera que tome los datos del blob de Exportación continua:</span><span class="sxs-lookup"><span data-stu-id="7b199-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="7b199-166">Ahora, necesitará la clave de acceso principal de la cuenta de almacenamiento, que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7b199-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="7b199-167">Establézcala como la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="7b199-168">Establecimiento del patrón del prefijo de la ruta de acceso</span><span class="sxs-lookup"><span data-stu-id="7b199-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="7b199-169">Asegúrese de establecer el formato de fecha en **AAAA-MM-DD** (con **guiones**).</span><span class="sxs-lookup"><span data-stu-id="7b199-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="7b199-170">El patrón del prefijo de la ruta de acceso especifica cómo busca el Análisis de transmisiones los archivos de entrada en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="7b199-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="7b199-171">Deberá establecerlo para que coincida con el modo en que la Exportación continua almacena los datos.</span><span class="sxs-lookup"><span data-stu-id="7b199-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="7b199-172">Configúrelo como este caso que se muestra a continuación:</span><span class="sxs-lookup"><span data-stu-id="7b199-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="7b199-173">En este ejemplo:</span><span class="sxs-lookup"><span data-stu-id="7b199-173">In this example:</span></span>

* <span data-ttu-id="7b199-174">`webapplication27` es el nombre del recurso de Application Insights, **todo en minúsculas**.</span><span class="sxs-lookup"><span data-stu-id="7b199-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="7b199-175">`1234...` es la clave de instrumentación del recurso de Application Insights **con los guiones quitados**.</span><span class="sxs-lookup"><span data-stu-id="7b199-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="7b199-176">`PageViews` es el tipo de datos que se van a analizar.</span><span class="sxs-lookup"><span data-stu-id="7b199-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="7b199-177">Los tipos disponibles dependen del filtro definido en la Exportación continua.</span><span class="sxs-lookup"><span data-stu-id="7b199-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="7b199-178">Examine los datos exportados para ver los demás tipos disponibles y vea el [modelo de exportación de datos](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b199-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="7b199-179">`/{date}/{time}` es un patrón escrito literalmente.</span><span class="sxs-lookup"><span data-stu-id="7b199-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="7b199-180">Para obtener el nombre y el valor iKey del recurso de Application Insights, abra Essentials en su página de información general o bien abra la Configuración.</span><span class="sxs-lookup"><span data-stu-id="7b199-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="7b199-181">Finalización de la instalación inicial</span><span class="sxs-lookup"><span data-stu-id="7b199-181">Finish initial setup</span></span>
<span data-ttu-id="7b199-182">Confirme el formato de serialización:</span><span class="sxs-lookup"><span data-stu-id="7b199-182">Confirm the serialization format:</span></span>

![Confirme y cierre el asistente.](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="7b199-184">Cierre el asistente y espere a que el programa de instalación finalice.</span><span class="sxs-lookup"><span data-stu-id="7b199-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="7b199-185">Use la función Sample para comprobar que estableció correctamente la ruta de acceso de entrada.</span><span class="sxs-lookup"><span data-stu-id="7b199-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="7b199-186">Si se produce un error: compruebe que hay datos en el almacenamiento para el intervalo de tiempo de muestreo que eligió.</span><span class="sxs-lookup"><span data-stu-id="7b199-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="7b199-187">Modifique la definición de entrada y compruebe que establece correctamente la cuenta de almacenamiento, el prefijo de ruta de acceso y el formato de fecha.</span><span class="sxs-lookup"><span data-stu-id="7b199-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="7b199-188">Establecimiento de la consulta</span><span class="sxs-lookup"><span data-stu-id="7b199-188">Set query</span></span>
<span data-ttu-id="7b199-189">Abra la sección de consulta:</span><span class="sxs-lookup"><span data-stu-id="7b199-189">Open the query section:</span></span>

![En Análisis de transmisiones, seleccione Consulta.](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="7b199-191">Reemplace la consulta predeterminada por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="7b199-191">Replace the default query with:</span></span>

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

<span data-ttu-id="7b199-192">Observe que las primeras propiedades son específicas de los datos de la vista de página.</span><span class="sxs-lookup"><span data-stu-id="7b199-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="7b199-193">Las exportaciones de otros tipos de telemetría tendrán diferentes propiedades.</span><span class="sxs-lookup"><span data-stu-id="7b199-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="7b199-194">Vea la [referencia detallada del modelo de datos para los tipos y valores de propiedad](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="7b199-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="7b199-195">Configuración de la salida a la base de datos</span><span class="sxs-lookup"><span data-stu-id="7b199-195">Set up output to database</span></span>
<span data-ttu-id="7b199-196">Seleccione SQL como salida.</span><span class="sxs-lookup"><span data-stu-id="7b199-196">Select SQL as the output.</span></span>

![En Análisis de transmisiones, seleccione Salidas.](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="7b199-198">Especifique la base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="7b199-198">Specify the SQL database.</span></span>

![Rellene los detalles de la base de datos.](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="7b199-200">Cierre el asistente y espere una notificación que indica que se ha configurado la salida.</span><span class="sxs-lookup"><span data-stu-id="7b199-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="7b199-201">Inicio del procesamiento</span><span class="sxs-lookup"><span data-stu-id="7b199-201">Start processing</span></span>
<span data-ttu-id="7b199-202">Inicie el trabajo desde la barra de acción:</span><span class="sxs-lookup"><span data-stu-id="7b199-202">Start the job from the action bar:</span></span>

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="7b199-204">Puede elegir si desea iniciar el procesamiento de los datos a partir de ahora o bien empezar con datos anteriores.</span><span class="sxs-lookup"><span data-stu-id="7b199-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="7b199-205">Lo segundo resulta útil si la Exportación continua ya se ha estado ejecutando durante un tiempo.</span><span class="sxs-lookup"><span data-stu-id="7b199-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![En Stream Analytics, haga clic en Inicio.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="7b199-207">Después de unos minutos, vuelva a las herramientas de administración de SQL Server y consulte los datos que están entrando.</span><span class="sxs-lookup"><span data-stu-id="7b199-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="7b199-208">Por ejemplo, utilice una consulta como esta:</span><span class="sxs-lookup"><span data-stu-id="7b199-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="7b199-209">Artículos relacionados</span><span class="sxs-lookup"><span data-stu-id="7b199-209">Related articles</span></span>
* [<span data-ttu-id="7b199-210">Exportación a PowerBI mediante Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="7b199-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="7b199-211">Referencia detallada del modelo de datos para los tipos y valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="7b199-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="7b199-212">Exportación continua en Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b199-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="7b199-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="7b199-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

