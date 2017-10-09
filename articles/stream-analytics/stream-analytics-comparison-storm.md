---
title: "Plataformas de análisis: Apache Storm comparación tooStream análisis | Documentos de Microsoft"
description: "Obtenga información orientativa elegir una plataforma de análisis en la nube mediante el uso de un tooStream de comparación de Apache Storm análisis. Comprenda las características y diferencias."
keywords: "plataforma de análisis, plataformas de análisis, plataforma de análisis de la nube, comparación de storm"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="70d07-105">Elección de una plataforma de Stream Analytics: comparación de Apache Storm con Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="70d07-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="70d07-106">Azure ofrece varias soluciones para analizar datos de streaming: [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) y [Apache Storm en HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="70d07-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="70d07-107">Ambas plataformas de análisis ofrecen ventajas de Hola de una solución de PaaS.</span><span class="sxs-lookup"><span data-stu-id="70d07-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="70d07-108">Pero Hola plataformas cuentan con algunas diferencias significativas en sus capacidades, así como en cómo configurar y administrarlos.</span><span class="sxs-lookup"><span data-stu-id="70d07-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="70d07-109">Este artículo proporciona una comparación en paralelo de toohelp características que elija entre Apache Storm y análisis de transmisiones de Azure como una plataforma de análisis en la nube.</span><span class="sxs-lookup"><span data-stu-id="70d07-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="70d07-110">Características generales</span><span class="sxs-lookup"><span data-stu-id="70d07-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-111">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="70d07-113">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-114">
                    <strong>¿Código abierto?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-115">No.</span><span class="sxs-lookup"><span data-stu-id="70d07-115">No.</span></span> <span data-ttu-id="70d07-116">Azure Stream Analytics es una oferta propiedad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="70d07-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-117">Sí.</span><span class="sxs-lookup"><span data-stu-id="70d07-117">Yes.</span></span> <span data-ttu-id="70d07-118">Apache Storm es una tecnología con licencia de Apache.</span><span class="sxs-lookup"><span data-stu-id="70d07-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-119">
                    <strong>¿Soporte técnico de Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-120">Sí</span><span class="sxs-lookup"><span data-stu-id="70d07-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-121">Sí</span><span class="sxs-lookup"><span data-stu-id="70d07-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-122">
                    <strong>Requisitos de hardware</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-123">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="70d07-123">None.</span></span> <span data-ttu-id="70d07-124">Análisis de transmisiones de Azure es un servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="70d07-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-125">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="70d07-125">None.</span></span> <span data-ttu-id="70d07-126">Apache Storm es un servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="70d07-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-127">
                    <strong>Unidad de nivel superior</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-128">Los usuarios implementan y supervisan trabajos de streaming.</span><span class="sxs-lookup"><span data-stu-id="70d07-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-129">Los usuarios implementan y supervisan todo un clúster, que puede hospedar varios trabajos de Storm y otras cargas de trabajo (de Batch incluidas).</span><span class="sxs-lookup"><span data-stu-id="70d07-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-130">
                    <strong>Precios</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-131">Precio por volumen de datos procesados y Hola número de unidades de streaming necesario por hora que Hola trabajo se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="70d07-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="70d07-132">Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">precios de Stream Analytics</a>.</span><span class="sxs-lookup"><span data-stu-id="70d07-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-133">unidad de Hola de compra está basado en el clúster y se cobra puntualmente Hola Hola clúster se está ejecutando, independientemente de los trabajos que se implementa.</span><span class="sxs-lookup"><span data-stu-id="70d07-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="70d07-134">Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/hdinsight/">precios de HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="70d07-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="70d07-135">Creación</span><span class="sxs-lookup"><span data-stu-id="70d07-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-136">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="70d07-138">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-139">
                    <strong>¿Funcionalidades: SQL DSL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-140">Sí.</span><span class="sxs-lookup"><span data-stu-id="70d07-140">Yes.</span></span> <span data-ttu-id="70d07-141">Stream Analytics ofrece un lenguaje de tipo SQL para crear las transformaciones.</span><span class="sxs-lookup"><span data-stu-id="70d07-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-142">No.</span><span class="sxs-lookup"><span data-stu-id="70d07-142">No.</span></span> <span data-ttu-id="70d07-143">Los usuarios escriben el código en Java o C# o usan las API de Trident.</span><span class="sxs-lookup"><span data-stu-id="70d07-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-144">
                    <strong>¿Funcionalidades: operadores temporales?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-145">Compatible de manera predeterminada con agregados de ventana y uniones temporales.</span><span class="sxs-lookup"><span data-stu-id="70d07-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-146">Deben implementarse operadores temporales por usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-147">
                    <strong>Experiencia de desarrollo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-148">Los usuarios pueden crear, depurar y supervisar trabajos a través del portal de Azure, hello mediante datos de ejemplo que se deriva de una secuencia en directo.</span><span class="sxs-lookup"><span data-stu-id="70d07-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-149">Los usuarios que utilizan .NET pueden desarrollar, depurar y supervisar a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="70d07-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="70d07-150">Los usuarios con Java u otros lenguajes pueden usar Hola IDE de su elección.</span><span class="sxs-lookup"><span data-stu-id="70d07-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-151">
                    <strong>Compatibilidad con la depuración</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-152">Registros de estado y las operaciones básicas de trabajo son depuración toohelp disponible.</span><span class="sxs-lookup"><span data-stu-id="70d07-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="70d07-153">Análisis de transmisiones actualmente no permiten a los usuarios especificar el contenido o la cantidad de contenido se incluye en los registros de hello (es decir, el modo detallado).</span><span class="sxs-lookup"><span data-stu-id="70d07-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-154">Hay registros detallados disponibles.</span><span class="sxs-lookup"><span data-stu-id="70d07-154">Detailed logs are available.</span></span> <span data-ttu-id="70d07-155">Los usuarios pueden obtener acceso a registros en Visual Studio o iniciando sesión en el clúster toohello y tener acceso directamente a los registros de Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-156">
                    <strong>¿Extensibilidad con código personalizado?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-157">Se admite parcialmente con UDF de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="70d07-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="70d07-158">Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integración de UDF de JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="70d07-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-159">Sí.</span><span class="sxs-lookup"><span data-stu-id="70d07-159">Yes.</span></span> <span data-ttu-id="70d07-160">Los usuarios pueden escribir código personalizado en C#, Java o en cualquier otro lenguaje compatible con Storm.</span><span class="sxs-lookup"><span data-stu-id="70d07-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="70d07-161">Orígenes de datos (entradas) y salidas</span><span class="sxs-lookup"><span data-stu-id="70d07-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-162">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="70d07-164">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-165">
                 <strong>Orígenes de datos de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-166">Azure Event Hubs y Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="70d07-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-167">Hay conectores disponibles para Azure Event Hubs, Azure Service Bus, Kafka y otros más.</span><span class="sxs-lookup"><span data-stu-id="70d07-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="70d07-168">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-169">
                    <strong>Formatos de datos de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-170">Avro, JSON y CSV</span><span class="sxs-lookup"><span data-stu-id="70d07-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-171">Los usuarios pueden implementar cualquier formato mediante código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-172">
                    <strong>Salidas</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-173">Un trabajo de streaming puede tener varias salidas.</span><span class="sxs-lookup"><span data-stu-id="70d07-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="70d07-174">Las salidas compatibles son Azure Event Hubs, Azure Blob Storage, Azure Table Storage, Azure SQL DB y Power BI.</span><span class="sxs-lookup"><span data-stu-id="70d07-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-175">Storm admite muchas salidas en una topología y cada una puede tener una lógica personalizada para el procesamiento de bajada.</span><span class="sxs-lookup"><span data-stu-id="70d07-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="70d07-176">Storm incluye conectores para Power BI, Azure Event Hubs, Azure Blob Storage, Azure Cosmos DB, SQL y HBase.</span><span class="sxs-lookup"><span data-stu-id="70d07-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="70d07-177">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-178">
                    <strong>Formatos de codificación de datos</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-179">Los datos deben tener formato UTF-8.</span><span class="sxs-lookup"><span data-stu-id="70d07-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-180">Los usuarios pueden implementar cualquier formato de codificación de datos mediante código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="70d07-181">Administración y operaciones</span><span class="sxs-lookup"><span data-stu-id="70d07-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-182">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="70d07-184">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-185">
                    <strong>Modelo de implementación del trabajo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-186">Azure Portal, PowerShell y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="70d07-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-187">Azure Portal, PowerShell, Visual Studio y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="70d07-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-188">
                    <strong>Supervisión (estadísticas, contadores, etc.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-189">La supervisión se implementa mediante Azure Portal y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="70d07-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="70d07-190">Los usuarios también pueden configurar alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="70d07-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-191">Supervisión se implementa mediante hello aluvión de interfaz de usuario y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="70d07-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-192">
                    <strong>Escalabilidad</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-193">Escalabilidad viene determinada por el número de Hola de Streaming Units (SUs) para cada trabajo.</span><span class="sxs-lookup"><span data-stu-id="70d07-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="70d07-194">Cada unidad de transmisión por secuencias se procesa la too1 MB/segundo, con un máximo de 50 unidades.</span><span class="sxs-lookup"><span data-stu-id="70d07-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="70d07-195">Para obtener más información, consulte <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">rendimiento tooincrease de escala</a>.</span><span class="sxs-lookup"><span data-stu-id="70d07-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-196">Escalabilidad se determina mediante el número de nodos de clúster de HDInsight Storm Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="70d07-197">límite superior de Hello en número de Hola de nodos se define por la cuota de Azure del usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-198">
                    <strong>Límites de procesamiento de datos</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-199">Los usuarios pueden aumentar el procesamiento de datos u optimizar los costos aumentando o reduciendo el número de Hola de unidades de Streaming, con un límite de 1 GB/segundo.</span><span class="sxs-lookup"><span data-stu-id="70d07-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-200">Los usuarios pueden escalar o reducir verticalmente el tamaño del clúster.</span><span class="sxs-lookup"><span data-stu-id="70d07-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-201">
                    <strong>Detener o reanudar</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-202">Puede detenerlo y reanudarlo en el punto donde lo detuvo.</span><span class="sxs-lookup"><span data-stu-id="70d07-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-203">Se puede detener y reanudar en el punto donde se detuvo en función de la marca de agua.</span><span class="sxs-lookup"><span data-stu-id="70d07-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-204">
                    <strong>Actualización de servicio y marco</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-205">Revisión automática sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="70d07-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-206">Revisión automática sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="70d07-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-207">
                    <strong>Continuidad empresarial mediante un servicio de alta disponibilidad con acuerdos de nivel de servicio garantizados</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="70d07-208">Contrato de nivel de servicio con un tiempo de actividad del 99,9%</span><span class="sxs-lookup"><span data-stu-id="70d07-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="70d07-209">Recuperación automática de errores</span><span class="sxs-lookup"><span data-stu-id="70d07-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="70d07-210">Recuperación integrada de los operadores temporales con estado.</span><span class="sxs-lookup"><span data-stu-id="70d07-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-211">SLA de tiempo de actividad del 99,9% de clúster de Storm Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="70d07-212">Apache Storm es una plataforma de streaming con tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="70d07-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="70d07-213">Sin embargo, resulta tooensure de responsabilidad del usuario de Hola que streaming ejecutan los trabajos sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="70d07-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="70d07-214">Características avanzadas</span><span class="sxs-lookup"><span data-stu-id="70d07-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-215">
                    <strong></strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="70d07-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="70d07-217">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-218">
                    <strong>Control de eventos desordenados y llegada tardía</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-219">Directivas configurables integradas pueden reordenar los eventos, quitar eventos o ajustar la hora del evento.</span><span class="sxs-lookup"><span data-stu-id="70d07-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-220">Los usuarios deben implementar lógica toohandle este escenario.</span><span class="sxs-lookup"><span data-stu-id="70d07-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-221">
                    <strong>Datos de referencia</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-222">Hay datos de referencia disponibles de Azure Blob Storage con un máximo de 100 MB de caché en memoria.</span><span class="sxs-lookup"><span data-stu-id="70d07-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="70d07-223">Datos de referencia se actualizan por servicio Hola.</span><span class="sxs-lookup"><span data-stu-id="70d07-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-224">Sin límites en el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="70d07-224">No limits on data size.</span></span> <span data-ttu-id="70d07-225">Hay conectores disponibles para HBase, Azure Cosmos DB, SQL Server y Azure.</span><span class="sxs-lookup"><span data-stu-id="70d07-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="70d07-226">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="70d07-227">Los datos de referencia deben actualizarse con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="70d07-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="70d07-228">
                    <strong>Integración con Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="70d07-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="70d07-229">Los modelos de Azure Machine Learning publicados se pueden configurar a modo de funciones durante la creación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="70d07-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="70d07-230">Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Escalado con funciones de Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="70d07-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="70d07-231">Disponible a través de Storm Bolts.</span><span class="sxs-lookup"><span data-stu-id="70d07-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
