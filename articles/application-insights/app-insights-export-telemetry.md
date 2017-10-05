---
title: "Exportación de telemetría desde Application Insights | Microsoft Docs"
description: "Exporte datos de diagnóstico y uso al almacenamiento en Microsoft Azure y descárguelos desde allí."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="ef8bb-103">Exportación de telemetría desde Application Insights</span><span class="sxs-lookup"><span data-stu-id="ef8bb-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="ef8bb-104">¿Desea mantener la telemetría durante más tiempo que el período de retención estándar?</span><span class="sxs-lookup"><span data-stu-id="ef8bb-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="ef8bb-105">¿O quiere procesarla de algún modo especializado?</span><span class="sxs-lookup"><span data-stu-id="ef8bb-105">Or process it in some specialized way?</span></span> <span data-ttu-id="ef8bb-106">La exportación continua es lo más conveniente para ello.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="ef8bb-107">Los eventos que se ven en el portal de Application Insights pueden exportarse a almacenamiento en Microsoft Azure en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="ef8bb-108">Desde allí puede descargar los datos y escribir cualquier código necesario para procesarlos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="ef8bb-109">El uso de la exportación continua puede conllevar un cargo adicional.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="ef8bb-110">Consulte su [modelo de fijación de precios](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ef8bb-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="ef8bb-111">Antes de configurar la exportación continua, hay algunas alternativas que conviene tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="ef8bb-112">El botón Exportar de la parte superior de una hoja de búsqueda o métricas permite transferir tablas y gráficos a una hoja de cálculo de Excel.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="ef8bb-113">[Analytics](app-insights-analytics.md) proporciona un lenguaje de consulta eficaz para telemetría.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="ef8bb-114">También puede exportar los resultados.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-114">It can also export results.</span></span>
* <span data-ttu-id="ef8bb-115">Si lo que le interesa es [explorar los datos en Power BI](app-insights-export-power-bi.md), puede hacerlo sin usar la exportación continua.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="ef8bb-116">La [API de REST de acceso a datos](https://dev.applicationinsights.io/) le permite acceder a datos de telemetría con programación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="ef8bb-117">Cuando la exportación continua copie sus datos en el almacenamiento (donde pueden permanecer tanto tiempo como quiera), seguirán estando disponibles en Application Insights durante el [período de retención](app-insights-data-retention-privacy.md) habitual.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="ef8bb-118"><a name="setup"></a>Creación de una exportación continua.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="ef8bb-119">En el recurso de Application Insights de su aplicación, abra Exportación continua y elija **Agregar**:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Desplácese hacia abajo y haga clic en Exportación continua.](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="ef8bb-121">Elija los tipos de datos de telemetría que quiere exportar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="ef8bb-122">Cree o seleccione una [cuenta de almacenamiento de Azure](../storage/common/storage-introduction.md) donde quiera almacenar los datos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="ef8bb-123">De forma predeterminada, la ubicación de almacenamiento se establecerá en la misma región geográfica que el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="ef8bb-124">Si los almacena en una región diferente, puede conllevar gastos de transferencia.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Haga clic en Agregar, Destino de exportación, Cuenta de almacenamiento y cree un nuevo almacén o elija uno almacén.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="ef8bb-126">Cree o seleccione un contenedor en el almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-126">Create or select a container in the storage:</span></span>

    ![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="ef8bb-128">Una vez que ha creado la exportación, comienza el proceso.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="ef8bb-129">Solo obtendrá los datos que lleguen después de crear la exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="ef8bb-130">Puede haber un retraso de aproximadamente una hora antes de que aparezcan los datos en el almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="ef8bb-131">Para editar la exportación continua</span><span class="sxs-lookup"><span data-stu-id="ef8bb-131">To edit continuous export</span></span>

<span data-ttu-id="ef8bb-132">Si desea cambiar los tipos de evento más tarde, simplemente edite la exportación:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-132">If you want to change the event types later, just edit the export:</span></span>

![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="ef8bb-134">Para detener la exportación continua</span><span class="sxs-lookup"><span data-stu-id="ef8bb-134">To stop continuous export</span></span>

<span data-ttu-id="ef8bb-135">Para detener la exportación, haga clic en Deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-135">To stop the export, click Disable.</span></span> <span data-ttu-id="ef8bb-136">Al hacer clic en Habilitar de nuevo, la exportación se reinicia con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="ef8bb-137">No obtendrá los datos que llegaron al portal mientras estaba deshabilitada la exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="ef8bb-138">Para detener la exportación de forma permanente, elimínela.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="ef8bb-139">Al realizar esta acción no se eliminan los datos del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="ef8bb-140">¿No puede agregar o cambiar una exportación?</span><span class="sxs-lookup"><span data-stu-id="ef8bb-140">Can't add or change an export?</span></span>
* <span data-ttu-id="ef8bb-141">Para agregar o cambiar las exportaciones, necesita derechos de propietario, colaborador o colaborador de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="ef8bb-142">[Más información sobre los roles][roles].</span><span class="sxs-lookup"><span data-stu-id="ef8bb-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="ef8bb-143"><a name="analyze"></a> ¿Qué eventos obtiene?</span><span class="sxs-lookup"><span data-stu-id="ef8bb-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="ef8bb-144">Los datos exportados son la telemetría sin procesar que recibimos de la aplicación, aunque también agregamos los datos de ubicación que calculamos a partir de la dirección IP del cliente.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="ef8bb-145">Los datos que se han descartado por [muestreo](app-insights-sampling.md) no se incluyen en los datos exportados.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="ef8bb-146">No se incluyen otras métricas calculadas.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="ef8bb-147">Por ejemplo, no exportamos el uso medio de la CPU, pero sí la telemetría sin procesar a partir de la que se calcula la media.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="ef8bb-148">Los datos también incluyen los resultados de cualquier [prueba web de disponibilidad](app-insights-monitor-web-app-availability.md) que haya configurado.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="ef8bb-149">**Muestreo.**</span><span class="sxs-lookup"><span data-stu-id="ef8bb-149">**Sampling.**</span></span> <span data-ttu-id="ef8bb-150">Si la aplicación envía muchos datos, la característica de muestreo puede operar y enviar solamente una fracción de la telemetría generada.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="ef8bb-151">Obtenga más información sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="ef8bb-152"><a name="get"></a> Inspección de los datos</span><span class="sxs-lookup"><span data-stu-id="ef8bb-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="ef8bb-153">Puede inspeccionar el almacenamiento directamente en el portal.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="ef8bb-154">Haga clic en **Examinar**, seleccione la cuenta de almacenamiento y abra **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="ef8bb-155">Para inspeccionar Azure Storage en Visual Studio, abra **Ver**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="ef8bb-156">(Si no dispone de ese comando de menú, deberá instalar el SDK de Azure: abra el cuadro de diálogo **Nuevo proyecto**, expanda Visual C#/Cloud y elija **Obtener el SDK de Microsoft Azure para. NET**).</span><span class="sxs-lookup"><span data-stu-id="ef8bb-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="ef8bb-157">Al abrir el almacén de blobs, verá un contenedor con un conjunto de archivos blob.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="ef8bb-158">El URI de cada archivo que se deriva del nombre del recurso de Application Insights, su clave de instrumentación, y el tipo, fecha y hora de telemetría.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="ef8bb-159">(El nombre del recurso está todo en minúsculas y la clave de instrumentación omite guiones).</span><span class="sxs-lookup"><span data-stu-id="ef8bb-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Inspección del almacén de blobs con una herramienta apropiada](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="ef8bb-161">La fecha y hora son UTC e indican cuándo se depositó la telemetría en el almacén, no la hora en que se generó.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="ef8bb-162">De modo que si escribe código para descargar los datos, se puede mover linealmente a través de los datos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="ef8bb-163">Este es el formato de la ruta de acceso:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="ef8bb-164">Where</span><span class="sxs-lookup"><span data-stu-id="ef8bb-164">Where</span></span>

* <span data-ttu-id="ef8bb-165">`blobCreationTimeUtc` es la hora de creación del blob en el almacenamiento provisional interno.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="ef8bb-166">`blobDeliveryTimeUtc` es la hora de copia del blob en el almacenamiento de destino de exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="ef8bb-167"><a name="format"></a> Formato de datos</span><span class="sxs-lookup"><span data-stu-id="ef8bb-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="ef8bb-168">Cada blob es un archivo de texto que contiene varias filas separadas por' \n'.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="ef8bb-169">Contiene la telemetría procesada durante un período de aproximadamente la mitad de un minuto.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="ef8bb-170">Cada fila representa un punto de datos de telemetría, como una vista de página o una solicitud.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="ef8bb-171">Cada fila es un documento JSON sin formato.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="ef8bb-172">Si quiere sentarse a mirarlo, ábralo en Visual Studio y elija Editar, Avanzadas, Archivo de formato:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Visualización de la telemetría con una herramienta apropiada](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="ef8bb-174">Las duraciones de tiempo son tics, donde 10 000 tics = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="ef8bb-175">Por ejemplo, estos valores muestran un tiempo de 1 ms para enviar una solicitud desde el explorador, 3 ms para recibirla y 1,8 s para procesar la página en el explorador:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="ef8bb-176">Referencia detallada del modelo de datos para los tipos y valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="ef8bb-177">Procesamiento de los datos</span><span class="sxs-lookup"><span data-stu-id="ef8bb-177">Processing the data</span></span>
<span data-ttu-id="ef8bb-178">En una pequeña escala, puede escribir código para separar sus datos, leerlos en una hoja de cálculo, etc.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="ef8bb-179">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="ef8bb-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="ef8bb-180">Para obtener un ejemplo de código más grande, consulte el [uso de un rol de trabajo][exportasa].</span><span class="sxs-lookup"><span data-stu-id="ef8bb-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="ef8bb-181"><a name="delete"></a>Eliminación de los datos antiguos</span><span class="sxs-lookup"><span data-stu-id="ef8bb-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="ef8bb-182">Tenga en cuenta que usted es responsable de administrar su capacidad de almacenamiento y eliminar los datos antiguos si es necesario.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="ef8bb-183">Si vuelve a generar la clave de almacenamiento...</span><span class="sxs-lookup"><span data-stu-id="ef8bb-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="ef8bb-184">Si cambia la clave para el almacenamiento, la exportación continua dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="ef8bb-185">Verá una notificación en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="ef8bb-186">Abra la hoja Exportación continua y edite la exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="ef8bb-187">Modifique el destino de exportación, pero deje el mismo almacenamiento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="ef8bb-188">Haga clic en Aceptar para confirmar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-188">Click OK to confirm.</span></span>

![Edite la exportación continua y abra y cierre el destino de exportación.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="ef8bb-190">La exportación continua se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="ef8bb-191">Ejemplos de exportación</span><span class="sxs-lookup"><span data-stu-id="ef8bb-191">Export samples</span></span>

* <span data-ttu-id="ef8bb-192">[Exportación a SQL con Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ef8bb-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ef8bb-193">Ejemplo 2 de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ef8bb-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="ef8bb-194">En escalas más grandes, considere la posibilidad de clústeres de Hadoop en [HDInsight](https://azure.microsoft.com/services/hdinsight/) en la nube.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="ef8bb-195">HDInsight ofrece una amplia variedad de tecnologías para administrar y analizar macrodatos, y puede usarlo para procesar datos que se han exportado desde Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="ef8bb-196">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="ef8bb-196">Q & A</span></span>
* <span data-ttu-id="ef8bb-197">*Lo único que quiero es una descarga única de un gráfico.*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="ef8bb-198">Sí, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-198">Yes, you can do that.</span></span> <span data-ttu-id="ef8bb-199">En la parte superior de la hoja, haga clic en **Exportar datos**.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="ef8bb-200">*Configuro una exportación, pero no hay ningún dato en el almacén.*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="ef8bb-201">¿Recibió Application Insights alguna telemetría de su aplicación desde que configuró la exportación?</span><span class="sxs-lookup"><span data-stu-id="ef8bb-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="ef8bb-202">Solo recibirá datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-202">You'll only receive new data.</span></span>
* <span data-ttu-id="ef8bb-203">*Intenté configurar una exportación, pero se deniega el acceso.*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="ef8bb-204">Si la cuenta pertenece a su organización, debe ser miembro de los grupos de propietarios o colaboradores.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="ef8bb-205">*¿Puedo exportar directamente a mi propio almacén local?*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="ef8bb-206">Lamentablemente, no.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-206">No, sorry.</span></span> <span data-ttu-id="ef8bb-207">Nuestro motor de exportación actualmente solo funciona con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="ef8bb-208">*¿Hay ningún límite para la cantidad de datos que puedo colocar en mi almacén?*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="ef8bb-209">No.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-209">No.</span></span> <span data-ttu-id="ef8bb-210">Seguiremos insertando datos hasta que elimine la exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="ef8bb-211">Pararemos si alcanzamos los límites externos del almacenamiento de blobs, pero hasta llegar ahí falta mucho.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="ef8bb-212">Depende de usted controlar la cantidad de almacenamiento que usa.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="ef8bb-213">*¿Cuántos blobs debería ver en el almacenamiento?*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="ef8bb-214">Para cada tipo de datos que seleccionó para exportar, se crea un blob nuevo cada minuto (si los datos están disponibles).</span><span class="sxs-lookup"><span data-stu-id="ef8bb-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="ef8bb-215">Además, para las aplicaciones con mucho tráfico, se asignan unidades de partición adicionales.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="ef8bb-216">En este caso, cada unidad crea un blob cada minuto.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="ef8bb-217">*Volví a generar la clave de mi almacenamiento o cambié el nombre del contenedor, y ahora no funciona la exportación.*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="ef8bb-218">Edite la exportación y abra la hoja de destino de la exportación.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="ef8bb-219">Deje el mismo almacenamiento seleccionado que antes y haga clic en Aceptar para confirmar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="ef8bb-220">La exportación se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-220">Export will restart.</span></span> <span data-ttu-id="ef8bb-221">Si el cambio estaba dentro de los últimos días, no perderá datos.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="ef8bb-222">*¿Puedo detener la exportación?*</span><span class="sxs-lookup"><span data-stu-id="ef8bb-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="ef8bb-223">Sí.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-223">Yes.</span></span> <span data-ttu-id="ef8bb-224">Haga clic en Deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ef8bb-225">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="ef8bb-225">Code samples</span></span>

* [<span data-ttu-id="ef8bb-226">Ejemplo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ef8bb-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="ef8bb-227">[Exportación a SQL con Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ef8bb-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ef8bb-228">Referencia detallada del modelo de datos para los tipos y valores de propiedad.</span><span class="sxs-lookup"><span data-stu-id="ef8bb-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
