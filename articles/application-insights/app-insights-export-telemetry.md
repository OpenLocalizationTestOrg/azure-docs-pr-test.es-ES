---
title: "exportación de aaaContinuous de telemetría de Application Insights | Documentos de Microsoft"
description: "Exportar toostorage de datos de diagnóstico y uso de Microsoft Azure y descargarla desde allí."
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="d3c87-103">Exportación de telemetría desde Application Insights</span><span class="sxs-lookup"><span data-stu-id="d3c87-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="d3c87-104">¿Desea tookeep la telemetría durante más tiempo que el período de retención estándar de hello?</span><span class="sxs-lookup"><span data-stu-id="d3c87-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="d3c87-105">¿O quiere procesarla de algún modo especializado?</span><span class="sxs-lookup"><span data-stu-id="d3c87-105">Or process it in some specialized way?</span></span> <span data-ttu-id="d3c87-106">La exportación continua es lo más conveniente para ello.</span><span class="sxs-lookup"><span data-stu-id="d3c87-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="d3c87-107">eventos de Hola que se ven en el portal de Application Insights Hola pueden ser exportado toostorage en Microsoft Azure en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d3c87-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="d3c87-108">Desde allí se puede descargar los datos y escribir cualquier código que se necesita tooprocess lo.</span><span class="sxs-lookup"><span data-stu-id="d3c87-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="d3c87-109">El uso de la exportación continua puede conllevar un cargo adicional.</span><span class="sxs-lookup"><span data-stu-id="d3c87-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="d3c87-110">Consulte su [modelo de fijación de precios](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="d3c87-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="d3c87-111">Antes de configurar la exportación continua, hay algunas alternativas que puede querer tooconsider:</span><span class="sxs-lookup"><span data-stu-id="d3c87-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="d3c87-112">botón de exportación de Hello en parte superior de Hola de una hoja de métricas o buscar permite transferir spreadsheet de Excel tooan de tablas y gráficos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="d3c87-113">[Analytics](app-insights-analytics.md) proporciona un lenguaje de consulta eficaz para telemetría.</span><span class="sxs-lookup"><span data-stu-id="d3c87-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="d3c87-114">También puede exportar los resultados.</span><span class="sxs-lookup"><span data-stu-id="d3c87-114">It can also export results.</span></span>
* <span data-ttu-id="d3c87-115">Si está pensando demasiado[explorar los datos en Power BI](app-insights-export-power-bi.md), puede hacerlo sin usar exportar continua.</span><span class="sxs-lookup"><span data-stu-id="d3c87-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="d3c87-116">Hola [API de REST de acceso a datos](https://dev.applicationinsights.io/) le permite tener acceso mediante programación a la telemetría.</span><span class="sxs-lookup"><span data-stu-id="d3c87-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="d3c87-117">Después de exportar continua copia su toostorage de datos (donde puede permanecer siempre como sea necesario), está todavía disponible en Application Insights para saludo habitual [período de retención](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="d3c87-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="d3c87-118"><a name="setup"></a>Creación de una exportación continua.</span><span class="sxs-lookup"><span data-stu-id="d3c87-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="d3c87-119">En hello recurso de Application Insights para su aplicación, abra exportar continua y elija **agregar**:</span><span class="sxs-lookup"><span data-stu-id="d3c87-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Desplácese hacia abajo y haga clic en Exportación continua.](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="d3c87-121">Elegir tipos de datos de telemetría de hello desea tooexport.</span><span class="sxs-lookup"><span data-stu-id="d3c87-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="d3c87-122">Cree o seleccione un [cuenta de almacenamiento de Azure](../storage/common/storage-introduction.md) donde desea toostore Hola datos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="d3c87-123">De forma predeterminada, la ubicación de almacenamiento de Hola se establecerá toohello misma región geográfica que el recurso de Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3c87-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="d3c87-124">Si los almacena en una región diferente, puede conllevar gastos de transferencia.</span><span class="sxs-lookup"><span data-stu-id="d3c87-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Haga clic en Agregar, Destino de exportación, Cuenta de almacenamiento y cree un nuevo almacén o elija uno almacén.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="d3c87-126">Cree o seleccione un contenedor de almacenamiento de hello:</span><span class="sxs-lookup"><span data-stu-id="d3c87-126">Create or select a container in hello storage:</span></span>

    ![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="d3c87-128">Una vez que ha creado la exportación, comienza el proceso.</span><span class="sxs-lookup"><span data-stu-id="d3c87-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="d3c87-129">Solo obtiene los datos que llegan después de crear la exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="d3c87-130">Puede haber un retraso de aproximadamente una hora antes de que los datos aparecen en el almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="d3c87-131">exportación de tooedit continua</span><span class="sxs-lookup"><span data-stu-id="d3c87-131">tooedit continuous export</span></span>

<span data-ttu-id="d3c87-132">Si desea que los tipos de evento de hello toochange más tarde, edite exportación hello:</span><span class="sxs-lookup"><span data-stu-id="d3c87-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Haga clic en Elegir tipos de evento.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="d3c87-134">exportación de toostop continua</span><span class="sxs-lookup"><span data-stu-id="d3c87-134">toostop continuous export</span></span>

<span data-ttu-id="d3c87-135">exportación de hello toostop, haga clic en deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="d3c87-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="d3c87-136">Al hacer clic en habilitar de nuevo, se reiniciará exportación Hola con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="d3c87-137">No obtendrá datos Hola que han llegado en el portal de hello mientras estaba deshabilitada la exportación.</span><span class="sxs-lookup"><span data-stu-id="d3c87-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="d3c87-138">exportación de hello toostop, eliminarlo de forma permanente.</span><span class="sxs-lookup"><span data-stu-id="d3c87-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="d3c87-139">Al realizar esta acción no se eliminan los datos del almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="d3c87-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="d3c87-140">¿No puede agregar o cambiar una exportación?</span><span class="sxs-lookup"><span data-stu-id="d3c87-140">Can't add or change an export?</span></span>
* <span data-ttu-id="d3c87-141">exportaciones de tooadd o cambiar, necesita derechos de acceso de propietario, Colaborador o colaborador de la información de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d3c87-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="d3c87-142">[Más información sobre los roles][roles].</span><span class="sxs-lookup"><span data-stu-id="d3c87-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="d3c87-143"><a name="analyze"></a> ¿Qué eventos obtiene?</span><span class="sxs-lookup"><span data-stu-id="d3c87-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="d3c87-144">Hello datos exportados están telemetría sin procesar de Hola que recibimos desde su aplicación, salvo que se agregue datos de ubicación que se calculan Hola dirección IP de cliente.</span><span class="sxs-lookup"><span data-stu-id="d3c87-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="d3c87-145">Datos que se ha descartado por [muestreo](app-insights-sampling.md) no se incluye en hello exportan datos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="d3c87-146">No se incluyen otras métricas calculadas.</span><span class="sxs-lookup"><span data-stu-id="d3c87-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="d3c87-147">Por ejemplo, no Exportamos uso promedio de la CPU, pero Exportamos telemetría de hello sin formato desde el que se calcula la media de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="d3c87-148">Hello datos también incluyen los resultados de Hola de cualquier [disponibilidad las pruebas web](app-insights-monitor-web-app-availability.md) que ha configurado.</span><span class="sxs-lookup"><span data-stu-id="d3c87-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="d3c87-149">**Muestreo.**</span><span class="sxs-lookup"><span data-stu-id="d3c87-149">**Sampling.**</span></span> <span data-ttu-id="d3c87-150">Si la aplicación envía una gran cantidad de datos, característica de muestreo de Hola puede operar y enviar sólo una fracción de telemetría de hello generado.</span><span class="sxs-lookup"><span data-stu-id="d3c87-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="d3c87-151">Aprenda más sobre el muestreo.</span><span class="sxs-lookup"><span data-stu-id="d3c87-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="d3c87-152"><a name="get"></a>Inspeccionar los datos de Hola</span><span class="sxs-lookup"><span data-stu-id="d3c87-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="d3c87-153">Puede inspeccionar almacenamiento Hola directamente en el portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="d3c87-154">Haga clic en **Examinar**, seleccione la cuenta de almacenamiento y abra **Contenedores**.</span><span class="sxs-lookup"><span data-stu-id="d3c87-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="d3c87-155">tooinspect almacenamiento de Azure en Visual Studio, abra **vista**, **nube explorador**.</span><span class="sxs-lookup"><span data-stu-id="d3c87-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="d3c87-156">(Si no tiene ese comando de menú, necesita tooinstall hello Azure SDK: Hola abierto **nuevo proyecto** cuadro de diálogo, expanda Visual C# y de la nube y elija **obtener Microsoft Azure SDK para .NET**.)</span><span class="sxs-lookup"><span data-stu-id="d3c87-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="d3c87-157">Al abrir el almacén de blobs, verá un contenedor con un conjunto de archivos blob.</span><span class="sxs-lookup"><span data-stu-id="d3c87-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="d3c87-158">Hola URI de cada archivo que se deriva de su nombre de recurso de Application Insights, su clave de instrumentación, telemetría-tipo, fecha y hora.</span><span class="sxs-lookup"><span data-stu-id="d3c87-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="d3c87-159">(nombre de recurso de hello está en minúsculas y clave de instrumentación de hello omite guiones).</span><span class="sxs-lookup"><span data-stu-id="d3c87-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Inspeccionar Hola el almacén de blobs con una herramienta apropiada](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="d3c87-161">Hola fecha y hora son UTC y cuando telemetría Hola se deposita en almacén de hello: tiempo de presentación no se generó.</span><span class="sxs-lookup"><span data-stu-id="d3c87-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="d3c87-162">Por lo que si se escribe código toodownload Hola dato, puede mover a través de los datos de Hola linealmente.</span><span class="sxs-lookup"><span data-stu-id="d3c87-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="d3c87-163">A continuación aparece el formulario de Hola de ruta de acceso de hello:</span><span class="sxs-lookup"><span data-stu-id="d3c87-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="d3c87-164">Where</span><span class="sxs-lookup"><span data-stu-id="d3c87-164">Where</span></span>

* <span data-ttu-id="d3c87-165">`blobCreationTimeUtc`es hora blob se creó en hello interno de almacenamiento provisional almacenamiento</span><span class="sxs-lookup"><span data-stu-id="d3c87-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="d3c87-166">`blobDeliveryTimeUtc`es el momento de hello cuando está copiada toohello exportación destino almacenamiento blob</span><span class="sxs-lookup"><span data-stu-id="d3c87-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="d3c87-167"><a name="format"></a> Formato de datos</span><span class="sxs-lookup"><span data-stu-id="d3c87-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="d3c87-168">Cada blob es un archivo de texto que contiene varias filas separadas por' \n'.</span><span class="sxs-lookup"><span data-stu-id="d3c87-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="d3c87-169">Contiene telemetría Hola procesado durante un período de tiempo de aproximadamente la mitad de un minuto.</span><span class="sxs-lookup"><span data-stu-id="d3c87-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="d3c87-170">Cada fila representa un punto de datos de telemetría, como una vista de página o una solicitud.</span><span class="sxs-lookup"><span data-stu-id="d3c87-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="d3c87-171">Cada fila es un documento JSON sin formato.</span><span class="sxs-lookup"><span data-stu-id="d3c87-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="d3c87-172">Si desea toosit y te quedas mirando en él, ábralo en Visual Studio y elija Editar, avanzadas, archivo de formato:</span><span class="sxs-lookup"><span data-stu-id="d3c87-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Vista Hola telemetría con una herramienta apropiada](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="d3c87-174">Las duraciones de tiempo son tics, donde 10 000 tics = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="d3c87-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="d3c87-175">Por ejemplo, estos valores muestran un tiempo de 1 ms toosend una solicitud de explorador hello, 3ms tooreceive y 1.8s tooprocess Hola página en el Explorador de hello:</span><span class="sxs-lookup"><span data-stu-id="d3c87-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="d3c87-176">Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.</span><span class="sxs-lookup"><span data-stu-id="d3c87-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="d3c87-177">Procesamiento de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="d3c87-177">Processing hello data</span></span>
<span data-ttu-id="d3c87-178">En una escala pequeña, puede escribir algunas toopull código alejados de los datos, leer en una hoja de cálculo y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="d3c87-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="d3c87-179">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d3c87-179">For example:</span></span>

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

<span data-ttu-id="d3c87-180">Para obtener un ejemplo de código más grande, consulte el [uso de un rol de trabajo][exportasa].</span><span class="sxs-lookup"><span data-stu-id="d3c87-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="d3c87-181"><a name="delete"></a>Eliminación de los datos antiguos</span><span class="sxs-lookup"><span data-stu-id="d3c87-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="d3c87-182">Tenga en cuenta que usted es responsable de administrar la capacidad de almacenamiento y eliminar datos antiguos de hello si es necesario.</span><span class="sxs-lookup"><span data-stu-id="d3c87-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="d3c87-183">Si vuelve a generar la clave de almacenamiento...</span><span class="sxs-lookup"><span data-stu-id="d3c87-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="d3c87-184">Si cambia el almacenamiento de claves tooyour hello, exportación continua dejará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="d3c87-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="d3c87-185">Verá una notificación en su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c87-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="d3c87-186">Abra hoja exportar continua de Hola y edite la exportación.</span><span class="sxs-lookup"><span data-stu-id="d3c87-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="d3c87-187">Editar Hola exportar destino, pero deje Hola mismo almacenamiento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="d3c87-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="d3c87-188">Haga clic en Aceptar tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d3c87-188">Click OK tooconfirm.</span></span>

![Editar Hola continua exportar, abra y cierre tres destino de exportación.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="d3c87-190">exportación continua Hola se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="d3c87-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="d3c87-191">Ejemplos de exportación</span><span class="sxs-lookup"><span data-stu-id="d3c87-191">Export samples</span></span>

* <span data-ttu-id="d3c87-192">[Exportar tooSQL mediante el análisis de transmisiones][exportasa]</span><span class="sxs-lookup"><span data-stu-id="d3c87-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="d3c87-193">Ejemplo 2 de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3c87-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="d3c87-194">En escalas más grandes, considere la posibilidad de [HDInsight](https://azure.microsoft.com/services/hdinsight/) -clústeres de Hadoop en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="d3c87-195">HDInsight proporciona una variedad de tecnologías para administrar y analizar grandes cantidades de datos y podría utilizar tooprocess datos que se han exportado desde Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d3c87-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="d3c87-196">Preguntas y respuestas</span><span class="sxs-lookup"><span data-stu-id="d3c87-196">Q & A</span></span>
* <span data-ttu-id="d3c87-197">*Lo único que quiero es una descarga única de un gráfico.*</span><span class="sxs-lookup"><span data-stu-id="d3c87-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="d3c87-198">Sí, puede hacerlo.</span><span class="sxs-lookup"><span data-stu-id="d3c87-198">Yes, you can do that.</span></span> <span data-ttu-id="d3c87-199">En la parte superior de Hola de hoja de hello, haga clic en **exportar datos**.</span><span class="sxs-lookup"><span data-stu-id="d3c87-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="d3c87-200">*Configuro una exportación, pero no hay ningún dato en el almacén.*</span><span class="sxs-lookup"><span data-stu-id="d3c87-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="d3c87-201">¿Application Insights recibió cualquier telemetría de la aplicación desde que ha configurado la exportación de hello?</span><span class="sxs-lookup"><span data-stu-id="d3c87-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="d3c87-202">Solo recibirá datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-202">You'll only receive new data.</span></span>
* <span data-ttu-id="d3c87-203">*Intentó tooset de una exportación, pero se denegó el acceso*</span><span class="sxs-lookup"><span data-stu-id="d3c87-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="d3c87-204">Si cuenta Hola pertenece a su organización, deberá toobe un miembro de los grupos de los propietarios o colaboradores de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="d3c87-205">*¿Se pueden exportar un almacén local propio toomy recta?*</span><span class="sxs-lookup"><span data-stu-id="d3c87-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="d3c87-206">Lamentablemente, no.</span><span class="sxs-lookup"><span data-stu-id="d3c87-206">No, sorry.</span></span> <span data-ttu-id="d3c87-207">Nuestro motor de exportación actualmente solo funciona con el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="d3c87-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="d3c87-208">*¿Hay cualquier cantidad de toohello límite de datos que pone en el almacén my?*</span><span class="sxs-lookup"><span data-stu-id="d3c87-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="d3c87-209">No.</span><span class="sxs-lookup"><span data-stu-id="d3c87-209">No.</span></span> <span data-ttu-id="d3c87-210">Le mantenemos datos hasta que se elimina la exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="d3c87-211">Se detendrá si encontramos límites hello para el almacenamiento de blobs, pero esto es bastante grande.</span><span class="sxs-lookup"><span data-stu-id="d3c87-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="d3c87-212">Es una tooyou toocontrol cuánto almacenamiento usa.</span><span class="sxs-lookup"><span data-stu-id="d3c87-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="d3c87-213">*¿Blobs cuántos debo ver en el almacenamiento de hello?*</span><span class="sxs-lookup"><span data-stu-id="d3c87-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="d3c87-214">Para el tipo de datos de cada tooexport seleccionada, un nuevo blob se crea cada minuto (si los datos están disponibles).</span><span class="sxs-lookup"><span data-stu-id="d3c87-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="d3c87-215">Además, para las aplicaciones con mucho tráfico, se asignan unidades de partición adicionales.</span><span class="sxs-lookup"><span data-stu-id="d3c87-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="d3c87-216">En este caso, cada unidad crea un blob cada minuto.</span><span class="sxs-lookup"><span data-stu-id="d3c87-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="d3c87-217">*Volver a generar almacenamiento de claves toomy de Hola o ha cambiado el nombre de Hola de contenedor de Hola y ahora no funciona la exportación de Hola.*</span><span class="sxs-lookup"><span data-stu-id="d3c87-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="d3c87-218">Editar exportación hello y abra la hoja de destino de exportación de Hola.</span><span class="sxs-lookup"><span data-stu-id="d3c87-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="d3c87-219">Dejar Hola mismo almacenamiento seleccionado como antes y haga clic en Aceptar tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="d3c87-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="d3c87-220">La exportación se reiniciará.</span><span class="sxs-lookup"><span data-stu-id="d3c87-220">Export will restart.</span></span> <span data-ttu-id="d3c87-221">Si cambió de hello en hello pocos días pasados, no perderá los datos.</span><span class="sxs-lookup"><span data-stu-id="d3c87-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="d3c87-222">*¿Puedo hacer una pausa de exportación de hello?*</span><span class="sxs-lookup"><span data-stu-id="d3c87-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="d3c87-223">Sí.</span><span class="sxs-lookup"><span data-stu-id="d3c87-223">Yes.</span></span> <span data-ttu-id="d3c87-224">Haga clic en Deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="d3c87-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="d3c87-225">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="d3c87-225">Code samples</span></span>

* [<span data-ttu-id="d3c87-226">Ejemplo de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d3c87-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="d3c87-227">[Exportar tooSQL mediante el análisis de transmisiones][exportasa]</span><span class="sxs-lookup"><span data-stu-id="d3c87-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="d3c87-228">Referencia para tipos de propiedad de Hola y valores del modelo de datos detallados.</span><span class="sxs-lookup"><span data-stu-id="d3c87-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
