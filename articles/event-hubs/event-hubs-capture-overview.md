---
title: "Introducción a Azure Event Hubs Capture | Microsoft Docs"
description: "Captura de datos de telemetría con Event Hubs Capture"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 9ae6aa57200b99f382c6e60565db9cfc69f1d3c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-event-hubs-capture"></a><span data-ttu-id="bd9cd-103">Azure Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="bd9cd-103">Azure Event Hubs Capture</span></span>

<span data-ttu-id="bd9cd-104">Azure Event Hubs Capture permite entregar automáticamente los datos de transmisión de Event Hubs a una cuenta de [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/) o [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) que elija con la flexibilidad añadida de poder especificar un intervalo de tiempo o de tamaño.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-104">Azure Event Hubs Capture enables you to automatically deliver the streaming data in Event Hubs to an [Azure Blob storage](https://azure.microsoft.com/services/storage/blobs/) or [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) account of your choice, with the added flexibility of specifying a time or size interval.</span></span> <span data-ttu-id="bd9cd-105">La configuración de Capture es rápida, su ejecución no tiene costes administrativos y se escala automáticamente con las [unidades de procesamiento](event-hubs-features.md#capacity) de Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-105">Setting up Capture is fast, there are no administrative costs to run it, and it scales automatically with Event Hubs [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="bd9cd-106">El uso de Event Hubs Capture constituye la forma más sencilla de cargar datos de streaming en Azure y permite centrarse en el procesamiento de datos, en lugar de en su captura.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-106">Event Hubs Capture is the easiest way to load streaming data into Azure, and enables you to focus on data processing rather than on data capture.</span></span>

<span data-ttu-id="bd9cd-107">Event Hubs Capture permite procesar las canalizaciones en tiempo real y las basadas en lotes en la misma transmisión,</span><span class="sxs-lookup"><span data-stu-id="bd9cd-107">Event Hubs Capture enables you to process real-time and batch-based pipelines on the same stream.</span></span> <span data-ttu-id="bd9cd-108">lo que permite crear soluciones que crecen a la par que sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-108">This means you can build solutions that grow with your needs over time.</span></span> <span data-ttu-id="bd9cd-109">Si ya está creando sistemas basados en lotes pensando en un futuro procesamiento en tiempo real o desea agregar una ruta de acceso inactiva eficaz a una solución en tiempo real existente, Event Hubs Capture facilita el trabajo con datos de streaming.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-109">Whether you're building batch-based systems today with an eye towards future real-time processing, or you want to add an efficient cold path to an existing real-time solution, Event Hubs Capture makes working with streaming data easier.</span></span>

## <a name="how-event-hubs-capture-works"></a><span data-ttu-id="bd9cd-110">Cómo funciona Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="bd9cd-110">How Event Hubs Capture works</span></span>

<span data-ttu-id="bd9cd-111">Event Hubs es un búfer duradero de retención temporal para la entrada de datos de telemetría, es similar a un registro distribuido.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-111">Event Hubs is a time-retention durable buffer for telemetry ingress, similar to a distributed log.</span></span> <span data-ttu-id="bd9cd-112">La clave para reducir horizontalmente en Event Hubs es el [modelo de consumidor con particiones](event-hubs-features.md#partitions).</span><span class="sxs-lookup"><span data-stu-id="bd9cd-112">The key to scaling in Event Hubs is the [partitioned consumer model](event-hubs-features.md#partitions).</span></span> <span data-ttu-id="bd9cd-113">Cada partición es un segmento de datos independiente y se consume de forma independiente.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-113">Each partition is an independent segment of data and is consumed independently.</span></span> <span data-ttu-id="bd9cd-114">Con el tiempo estos datos envejecen basándose en el período de retención configurable.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-114">Over time this data ages off, based on the configurable retention period.</span></span> <span data-ttu-id="bd9cd-115">Como consecuencia, un centro de eventos determinado nunca llega a estar "demasiado lleno".</span><span class="sxs-lookup"><span data-stu-id="bd9cd-115">As a result, a given event hub never gets "too full."</span></span>

<span data-ttu-id="bd9cd-116">Event Hubs Capture le permite especificar su propia cuenta y contenedor de Azure Blob Storage, o cuenta de Azure Data Lake Store, que se usan para almacenar los datos capturados.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-116">Event Hubs Capture enables you to specify your own Azure Blob storage account and container, or Azure Data Lake Store account, which are used to store the captured data.</span></span> <span data-ttu-id="bd9cd-117">Estas cuentas pueden estar en la misma región que el centro de eventos o en otra, lo que se suma a la flexibilidad de la característica Event Hubs Capture.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-117">These accounts can be in the same region as your event hub or in another region, adding to the flexibility of the Event Hubs Capture feature.</span></span>

<span data-ttu-id="bd9cd-118">Los datos capturados se escriben en el formato de [Apache Avro][Apache Avro], que es un formato compacto, rápido y binario que proporciona estructuras de datos enriquecidos con un esquema insertado.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-118">Captured data is written in [Apache Avro][Apache Avro] format: a compact, fast, binary format that provides rich data structures with inline schema.</span></span> <span data-ttu-id="bd9cd-119">Este formato se usa ampliamente en el ecosistema de Hadoop, en Stream Analytics y en Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-119">This format is widely used in the Hadoop ecosystem, Stream Analytics, and Azure Data Factory.</span></span> <span data-ttu-id="bd9cd-120">En este mismo artículo encontrará más información acerca de cómo trabajar con Avro.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-120">More information about working with Avro is available later in this article.</span></span>

### <a name="capture-windowing"></a><span data-ttu-id="bd9cd-121">Ventanas de captura</span><span class="sxs-lookup"><span data-stu-id="bd9cd-121">Capture windowing</span></span>

<span data-ttu-id="bd9cd-122">Event Hubs Capture permite configurar una ventana para controlar la captura.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-122">Event Hubs Capture enables you to set up a window to control capturing.</span></span> <span data-ttu-id="bd9cd-123">Esta ventana es una configuración mínima de tamaño y tiempo con una "directiva de que el primero gana", lo que significa que el primer desencadenador que se encuentre provocará una operación de captura.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-123">This window is a minimum size and time configuration with a "first wins policy," meaning that the first trigger encountered causes a capture operation.</span></span> <span data-ttu-id="bd9cd-124">Si tiene una ventana de captura de 100 MB cada quince minutos y envía 1 MB/s, la ventana de tamaño se desencadenará antes que la ventana de tiempo.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-124">If you have a fifteen-minute, 100 MB capture window and send 1 MB per second, the size window triggers before the time window.</span></span> <span data-ttu-id="bd9cd-125">Cada partición se captura de forma independiente y escribe un blob en bloques completado en el momento de la captura, denominado como la hora en que se encontró el intervalo de captura.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-125">Each partition captures independently and writes a completed block blob at the time of capture, named for the time at which the capture interval was encountered.</span></span> <span data-ttu-id="bd9cd-126">Esta es la convención de nomenclatura de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="bd9cd-126">The storage naming convention is as follows:</span></span>

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-to-throughput-units"></a><span data-ttu-id="bd9cd-127">Escalado a unidades de procesamiento</span><span class="sxs-lookup"><span data-stu-id="bd9cd-127">Scaling to throughput units</span></span>

<span data-ttu-id="bd9cd-128">El tráfico de los Event Hubs lo controlan las [unidades de procesamiento](event-hubs-features.md#capacity).</span><span class="sxs-lookup"><span data-stu-id="bd9cd-128">Event Hubs traffic is controlled by [throughput units](event-hubs-features.md#capacity).</span></span> <span data-ttu-id="bd9cd-129">Una sola unidad de procesamiento permite una entrada de 1 MB/s o 1000 eventos por segundo y una salida que duplica esas cifras.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-129">A single throughput unit allows 1 MB per second or 1000 events per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="bd9cd-130">Standard Event Hubs se puede configurar con entre 1 y 20 unidades de procesamiento, y puede adquirir más a través de una solicitud de aumento de cuota al [equipo de soporte técnico][support request].</span><span class="sxs-lookup"><span data-stu-id="bd9cd-130">Standard Event Hubs can be configured with 1-20 throughput units, and you can purchase more with a quota increase [support request][support request].</span></span> <span data-ttu-id="bd9cd-131">El uso por encima de las unidades de procesamiento adquiridas está limitado.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-131">Usage beyond your purchased throughput units is throttled.</span></span> <span data-ttu-id="bd9cd-132">Event Hubs Capture copia los datos directamente del almacenamiento interno de Event Hubs, omite las cuotas de salida de unidades de procesamiento y guarda la salida para otros lectores de procesamiento como Stream Analytics o Spark.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-132">Event Hubs Capture copies data directly from the internal Event Hubs storage, bypassing throughput unit egress quotas and saving your egress for other processing readers, such as Stream Analytics or Spark.</span></span>

<span data-ttu-id="bd9cd-133">Una vez configurado, Event Hubs Capture se ejecuta automáticamente cuando se envía el primer evento y continúa ejecutándose.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-133">Once configured, Event Hubs Capture runs automatically when you send your first event, and continues running.</span></span> <span data-ttu-id="bd9cd-134">Para facilitar que el procesamiento de bajada sepa que el proceso funciona, Event Hubs escribe archivos vacíos cuando no hay datos.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-134">To make it easier for your downstream processing to know that the process is working, Event Hubs writes empty files when there is no data.</span></span> <span data-ttu-id="bd9cd-135">Este proceso proporciona un marcador y una cadencia predecibles que puede alimentar sus procesadores de lotes.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-135">This process provides a predictable cadence and marker that can feed your batch processors.</span></span>

## <a name="setting-up-event-hubs-capture"></a><span data-ttu-id="bd9cd-136">Configuración de Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="bd9cd-136">Setting up Event Hubs Capture</span></span>

<span data-ttu-id="bd9cd-137">Puede configurar la funcionalidad de captura en el momento de creación del centro de eventos mediante [Azure Portal](https://portal.azure.com) o con las plantillas de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-137">You can configure Capture at the event hub creation time using the [Azure portal](https://portal.azure.com), or using Azure Resource Manager templates.</span></span> <span data-ttu-id="bd9cd-138">Para más información, consulte los siguientes artículos.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-138">For more information, see the following articles:</span></span>

- [<span data-ttu-id="bd9cd-139">Habilitación de Event Hubs Capture mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bd9cd-139">Enable Event Hubs Capture using the Azure portal</span></span>](event-hubs-capture-enable-through-portal.md)
- [<span data-ttu-id="bd9cd-140">Creación de un espacio de nombres de Event Hubs con un centro de eventos y habilitación de la característica Capture mediante una plantilla de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bd9cd-140">Create an Event Hubs namespace with an event hub and enable Capture using an Azure Resource Manager template</span></span>](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-the-captured-files-and-working-with-avro"></a><span data-ttu-id="bd9cd-141">Exploración de los archivos capturados y trabajo con Avro</span><span class="sxs-lookup"><span data-stu-id="bd9cd-141">Exploring the captured files and working with Avro</span></span>

<span data-ttu-id="bd9cd-142">Event Hubs Capture crea archivos en formato Avro, como se especifica en la ventana de tiempo configurada.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-142">Event Hubs Capture creates files in Avro format, as specified on the configured time window.</span></span> <span data-ttu-id="bd9cd-143">Dichos archivos se pueden ver en cualquier herramienta, como el [Explorador de Azure Storage][Azure Storage Explorer].</span><span class="sxs-lookup"><span data-stu-id="bd9cd-143">You can view these files in any tool such as [Azure Storage Explorer][Azure Storage Explorer].</span></span> <span data-ttu-id="bd9cd-144">Los archivos se pueden descargar de forma local para trabajar con ellos.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-144">You can download the files locally to work on them.</span></span>

<span data-ttu-id="bd9cd-145">Los archivos que genera Event Hubs Capture tienen el siguiente esquema de Avro:</span><span class="sxs-lookup"><span data-stu-id="bd9cd-145">The files produced by Event Hubs Capture have the following Avro schema:</span></span>

![][3]

<span data-ttu-id="bd9cd-146">Para explorar los archivos de Avro fácilmente, utilice el archivo jar [Avro Tools][Avro Tools] desde Apache.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-146">An easy way to explore Avro files is by using the [Avro Tools][Avro Tools] jar from Apache.</span></span> <span data-ttu-id="bd9cd-147">Tras descargar este archivo, para ver el esquema de un archivo específico de Avro, ejecute el comando siguiente:</span><span class="sxs-lookup"><span data-stu-id="bd9cd-147">After downloading this jar, you can see the schema of a specific Avro file by running the following command:</span></span>

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

<span data-ttu-id="bd9cd-148">Este comando devuelve</span><span class="sxs-lookup"><span data-stu-id="bd9cd-148">This command returns</span></span>

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

<span data-ttu-id="bd9cd-149">Avro Tools también puede utilizarse para convertir el archivo al formato JSON y realizar otro procesamiento.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-149">You can also use Avro Tools to convert the file to JSON format and perform other processing.</span></span>

<span data-ttu-id="bd9cd-150">Para realizar un procesamiento más avanzado, descargue e instale Avro para la plataforma que desee.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-150">To perform more advanced processing, download and install Avro for your choice of platform.</span></span> <span data-ttu-id="bd9cd-151">En el momento de redactar este artículo, existen implementaciones para C, C++, C\#, Java, NodeJS, Perl, PHP, Python y Ruby.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-151">At the time of this writing, there are implementations available for C, C++, C\#, Java, NodeJS, Perl, PHP, Python, and Ruby.</span></span>

<span data-ttu-id="bd9cd-152">Apache Avro tiene guías de introducción para [Java][Java] y [Python][Python] muy completas.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-152">Apache Avro has complete Getting Started guides for [Java][Java] and [Python][Python].</span></span> <span data-ttu-id="bd9cd-153">También puede leer el artículo [Getting started with Event Hubs Capture (Introducción a Event Hubs Capture)](event-hubs-capture-python.md).</span><span class="sxs-lookup"><span data-stu-id="bd9cd-153">You can also read the [Getting started with Event Hubs Capture](event-hubs-capture-python.md) article.</span></span>

## <a name="how-event-hubs-capture-is-charged"></a><span data-ttu-id="bd9cd-154">Cómo se factura Event Hubs Capture</span><span class="sxs-lookup"><span data-stu-id="bd9cd-154">How Event Hubs Capture is charged</span></span>

<span data-ttu-id="bd9cd-155">Event Hubs Capture se mide de forma similar a las unidades de procesamiento, por hora.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-155">Event Hubs Capture is metered similarly to throughput units: as an hourly charge.</span></span> <span data-ttu-id="bd9cd-156">El cargo es directamente proporcional al número de unidades de procesamiento que se adquirieron para el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-156">The charge is directly proportional to the number of throughput units purchased for the namespace.</span></span> <span data-ttu-id="bd9cd-157">A medida que las unidades de procesamiento se incrementan y reducen, las mediciones de Event Hubs Capture aumentan y disminuyen, con el fin de proporcionar un rendimiento coincidente.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-157">As throughput units are increased and decreased, Event Hubs Capture meters increase and decrease to provide matching performance.</span></span> <span data-ttu-id="bd9cd-158">Los medidores se ejecutan de manera simultánea.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-158">The meters occur in tandem.</span></span> <span data-ttu-id="bd9cd-159">Para conocer los precios detallados, consulte [Precios de Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="bd9cd-159">For pricing details, see [Event Hubs pricing](https://azure.microsoft.com/pricing/details/event-hubs/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bd9cd-160">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bd9cd-160">Next steps</span></span>

<span data-ttu-id="bd9cd-161">Event Hubs Capture es el modo más sencillo de obtener datos en Azure.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-161">Event Hubs Capture is the easiest way to get data into Azure.</span></span> <span data-ttu-id="bd9cd-162">Con Azure Data Lake, Azure Data Factory y Azure HDInsight, se puede realizar el procesamiento por lotes y cualquier otro análisis mediante las plataformas y herramientas conocidas a la escala que necesite.</span><span class="sxs-lookup"><span data-stu-id="bd9cd-162">Using Azure Data Lake, Azure Data Factory, and Azure HDInsight, you can perform batch processing and other analytics using familiar tools and platforms of your choosing, at any scale you need.</span></span>

<span data-ttu-id="bd9cd-163">Para más información acerca de Event Hubs, visite los vínculos siguientes:</span><span class="sxs-lookup"><span data-stu-id="bd9cd-163">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="bd9cd-164">Get started sending and receiving events (Introducción al envío y la recepción de eventos)</span><span class="sxs-lookup"><span data-stu-id="bd9cd-164">Get started sending and receiving events</span></span>](event-hubs-dotnet-framework-getstarted-send.md)
* <span data-ttu-id="bd9cd-165">Una [aplicación de ejemplo completa que usa Event Hubs][sample application that uses Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="bd9cd-165">A complete [sample application that uses Event Hubs][sample application that uses Event Hubs]</span></span>
* <span data-ttu-id="bd9cd-166">[Información general de Event Hubs][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="bd9cd-166">[Event Hubs overview][Event Hubs overview]</span></span>

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
