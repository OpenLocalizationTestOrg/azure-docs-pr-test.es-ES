---
title: "Plataformas de Analytics: Comparación de Apache Storm con Stream Analytics | Microsoft Docs"
description: "Obtenga instrucciones para seleccionar una plataforma de análisis en la nube mediante una comparación de Apache Storm con Análisis de transmisiones. Comprenda las características y diferencias."
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
ms.openlocfilehash: 97044cb5d7b0b3fcb3b85328df618a265bc59b61
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="6d5a7-105">Elección de una plataforma de Stream Analytics: comparación de Apache Storm con Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6d5a7-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="6d5a7-106">Azure ofrece varias soluciones para analizar datos de streaming: [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/) y [Apache Storm en HDInsight de Azure](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="6d5a7-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="6d5a7-107">Ambas plataformas de análisis ofrecen las ventajas de una solución PaaS.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-107">Both analytics platforms provide the benefits of a PaaS solution.</span></span> <span data-ttu-id="6d5a7-108">Pero las plataformas presentan algunas diferencias importantes en cuanto a funcionalidades, así como en la forma en que se configuran y administran.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-108">But the platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="6d5a7-109">En este artículo se ofrece una comparación de características en paralelo para ayudarle a elegir entre Apache Storm y Azure Stream Analytics como plataforma de análisis en la nube.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-109">This article provides a side-by-side comparison of features to help you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="6d5a7-110">Características generales</span><span class="sxs-lookup"><span data-stu-id="6d5a7-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-112">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="6d5a7-113">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-114">
                    <strong>¿Código abierto?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-115">No.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-115">No.</span></span> <span data-ttu-id="6d5a7-116">Azure Stream Analytics es una oferta propiedad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-117">Sí.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-117">Yes.</span></span> <span data-ttu-id="6d5a7-118">Apache Storm es una tecnología con licencia de Apache.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-119">
                    <strong>¿Soporte técnico de Microsoft?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-120">Sí</span><span class="sxs-lookup"><span data-stu-id="6d5a7-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-121">Sí</span><span class="sxs-lookup"><span data-stu-id="6d5a7-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-122">
                    <strong>Requisitos de hardware</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-123">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-123">None.</span></span> <span data-ttu-id="6d5a7-124">Análisis de transmisiones de Azure es un servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-125">Ninguno.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-125">None.</span></span> <span data-ttu-id="6d5a7-126">Apache Storm es un servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-127">
                    <strong>Unidad de nivel superior</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-128">Los usuarios implementan y supervisan trabajos de streaming.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-129">Los usuarios implementan y supervisan todo un clúster, que puede hospedar varios trabajos de Storm y otras cargas de trabajo (de Batch incluidas).</span><span class="sxs-lookup"><span data-stu-id="6d5a7-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-130">
                    <strong>Precios</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-131">El precio varía por volumen de datos procesados y el número de unidades de streaming necesarias por cada hora en la que se ejecuta el trabajo.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-131">Priced by volume of data processed and the number of streaming units required per hour that the job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="6d5a7-132">Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">precios de Stream Analytics</a>.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-133">La unidad de compra se basa en el clúster y se cobra por el tiempo durante el que el clúster se ejecuta, independientemente de los trabajos implementados.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-133">The unit of purchase is cluster-based, and is charged based on the time the cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="6d5a7-134">Para más información, vea los <a href="http://azure.microsoft.com/pricing/details/hdinsight/">precios de HDInsight</a>.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="6d5a7-135">Creación</span><span class="sxs-lookup"><span data-stu-id="6d5a7-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-137">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="6d5a7-138">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-139">
                    <strong>¿Funcionalidades: SQL DSL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-140">Sí.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-140">Yes.</span></span> <span data-ttu-id="6d5a7-141">Stream Analytics ofrece un lenguaje de tipo SQL para crear las transformaciones.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-142">No.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-142">No.</span></span> <span data-ttu-id="6d5a7-143">Los usuarios escriben el código en Java o C# o usan las API de Trident.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-144">
                    <strong>¿Funcionalidades: operadores temporales?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-145">Compatible de manera predeterminada con agregados de ventana y uniones temporales.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-146">Los operadores temporales debe implementarlos el usuario.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-146">Temporal operators must be implemented by the user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-147">
                    <strong>Experiencia de desarrollo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-148">Los usuarios pueden crear, depurar y supervisar trabajos a través de Azure Portal, con datos de muestra procedentes de Live Stream.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-148">Users can create, debug, and monitor jobs through the Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-149">Los usuarios que utilizan .NET pueden desarrollar, depurar y supervisar a través de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="6d5a7-150">Los usuarios que utilizan Java u otros lenguajes pueden usar el IDE que prefieran.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-150">Users using Java or other languages can use the IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-151">
                    <strong>Compatibilidad con la depuración</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-152">Existen registros de operaciones y estados del trabajo básicos disponibles que ayudan a depurar.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-152">Basic job status and operations logs are available to help debug.</span></span> <span data-ttu-id="6d5a7-153">Stream Analytics actualmente no permite a los usuarios especificar qué contenido ni cuánto contenido se incluye en los registros (es decir, el modo detallado).</span><span class="sxs-lookup"><span data-stu-id="6d5a7-153">Stream Analytics currently does not let users specify what content or how much content is included in the logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-154">Hay registros detallados disponibles.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-154">Detailed logs are available.</span></span> <span data-ttu-id="6d5a7-155">Los usuarios pueden acceder a los registros en Visual Studio o iniciar sesión en el clúster y acceder directamente a los registros.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-155">Users can access logs in Visual Studio or by logging in to the cluster and accessing the logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-156">
                    <strong>¿Extensibilidad con código personalizado?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-157">Se admite parcialmente con UDF de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="6d5a7-158">Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">Integración de UDF de JavaScript</a>.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-159">Sí.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-159">Yes.</span></span> <span data-ttu-id="6d5a7-160">Los usuarios pueden escribir código personalizado en C#, Java o en cualquier otro lenguaje compatible con Storm.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="6d5a7-161">Orígenes de datos (entradas) y salidas</span><span class="sxs-lookup"><span data-stu-id="6d5a7-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-163">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="6d5a7-164">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-165">
                 <strong>Orígenes de datos de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-166">Azure Event Hubs y Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-167">Hay conectores disponibles para Azure Event Hubs, Azure Service Bus, Kafka y otros más.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="6d5a7-168">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-169">
                    <strong>Formatos de datos de entrada</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-170">Avro, JSON y CSV</span><span class="sxs-lookup"><span data-stu-id="6d5a7-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-171">Los usuarios pueden implementar cualquier formato mediante código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-172">
                    <strong>Salidas</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-173">Un trabajo de streaming puede tener varias salidas.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="6d5a7-174">Las salidas compatibles son Azure Event Hubs, Azure Blob Storage, Azure Table Storage, Azure SQL DB y Power BI.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-175">Storm admite muchas salidas en una topología y cada una puede tener una lógica personalizada para el procesamiento de bajada.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="6d5a7-176">Storm incluye conectores para Power BI, Azure Event Hubs, Azure Blob Storage, Azure Cosmos DB, SQL y HBase.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="6d5a7-177">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-178">
                    <strong>Formatos de codificación de datos</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-179">Los datos deben tener formato UTF-8.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-180">Los usuarios pueden implementar cualquier formato de codificación de datos mediante código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="6d5a7-181">Administración y operaciones</span><span class="sxs-lookup"><span data-stu-id="6d5a7-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-183">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="6d5a7-184">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-185">
                    <strong>Modelo de implementación del trabajo</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-186">Azure Portal, PowerShell y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-187">Azure Portal, PowerShell, Visual Studio y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-188">
                    <strong>Supervisión (estadísticas, contadores, etc.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-189">La supervisión se implementa mediante Azure Portal y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="6d5a7-190">Los usuarios también pueden configurar alertas de Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-191">La supervisión se implementa mediante la interfaz de usuario de Storm y las API de REST.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-191">Monitoring is implemented using the Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-192">
                    <strong>Escalabilidad</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-193">La escalabilidad viene determinada por el número de unidades de streaming (SU) para cada trabajo.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-193">Scalability is determined by the number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="6d5a7-194">Cada unidad de streaming procesa hasta 1 MB/segundo, con un máximo de 50 unidades.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-194">Each Streaming Unit processes up to 1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="6d5a7-195">Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Escalado para aumentar el rendimiento</a>.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale to increase throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-196">La escalabilidad viene determinada por el número de nodos de clúster de Storm en HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-196">Scalability is determined by the number of nodes in the HDInsight Storm cluster.</span></span> <span data-ttu-id="6d5a7-197">El límite superior en el número de nodos se define por la cuota de Azure del usuario.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-197">The top limit on the number of nodes is defined by the user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-198">
                    <strong>Límites de procesamiento de datos</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-199">Los usuarios pueden aumentar el procesamiento de datos u optimizar los costos aumentando o reduciendo el número de unidades de streaming, con un límite superior de 1 GB/segundo.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-199">Users can increase data processing or optimize costs by increasing or decreasing the number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-200">Los usuarios pueden escalar o reducir verticalmente el tamaño del clúster.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-201">
                    <strong>Detener o reanudar</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-202">Puede detenerlo y reanudarlo en el punto donde lo detuvo.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-203">Se puede detener y reanudar en el punto donde se detuvo en función de la marca de agua.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-204">
                    <strong>Actualización de servicio y marco</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-205">Revisión automática sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-206">Revisión automática sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-207">
                    <strong>Continuidad empresarial mediante un servicio de alta disponibilidad con acuerdos de nivel de servicio garantizados</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="6d5a7-208">Contrato de nivel de servicio con un tiempo de actividad del 99,9%</span><span class="sxs-lookup"><span data-stu-id="6d5a7-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="6d5a7-209">Recuperación automática de errores</span><span class="sxs-lookup"><span data-stu-id="6d5a7-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="6d5a7-210">Recuperación integrada de los operadores temporales con estado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-211">Contrato de nivel de servicio con un tiempo de actividad del clúster de Storm del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-211">SLA of 99.9% uptime of the Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="6d5a7-212">Apache Storm es una plataforma de streaming con tolerancia a errores.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="6d5a7-213">Pero, es responsabilidad del usuario garantizar que los trabajos de streaming se ejecutan sin interrupciones.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-213">However, it is the user's responsibility to ensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="6d5a7-214">Características avanzadas</span><span class="sxs-lookup"><span data-stu-id="6d5a7-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="6d5a7-216">
                    <strong>Azure Stream Analytics</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="6d5a7-217">
                    <strong>Apache Storm en HDInsight</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-218">
                    <strong>Control de eventos desordenados y llegada tardía</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-219">Directivas configurables integradas pueden reordenar los eventos, quitar eventos o ajustar la hora del evento.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-220">Los usuarios deben implementar la lógica para administrar este escenario.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-220">Users must implement logic to handle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-221">
                    <strong>Datos de referencia</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-222">Hay datos de referencia disponibles de Azure Blob Storage con un máximo de 100 MB de caché en memoria.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="6d5a7-223">El servicio actualiza los datos de referencia.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-223">Reference data is refreshed by the service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-224">Sin límites en el tamaño de los datos.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-224">No limits on data size.</span></span> <span data-ttu-id="6d5a7-225">Hay conectores disponibles para HBase, Azure Cosmos DB, SQL Server y Azure.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="6d5a7-226">Los usuarios pueden crear conectores adicionales con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="6d5a7-227">Los datos de referencia deben actualizarse con código personalizado.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="6d5a7-228">
                    <strong>Integración con Machine Learning</strong>
                </span><span class="sxs-lookup"><span data-stu-id="6d5a7-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="6d5a7-229">Los modelos de Azure Machine Learning publicados se pueden configurar a modo de funciones durante la creación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="6d5a7-230">Para más información, vea <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Escalado con funciones de Machine Learning</a>.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="6d5a7-231">Disponible a través de Storm Bolts.</span><span class="sxs-lookup"><span data-stu-id="6d5a7-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
