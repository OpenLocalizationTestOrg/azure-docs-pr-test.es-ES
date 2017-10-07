---
title: "aaaAzure SQL datos de almacenamiento de las preguntas más frecuentes | Documentos de Microsoft"
description: "En este artículo se muestran las preguntas más frecuentes sobre Azure SQL Data Warehouse para clientes y desarrolladores"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: 812CA525-3BF3-49DF-8DF3-FB4342464F4F
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 3/1/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 09fd3f65d9507b09fcb8f477742c7d020add2755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-frequently-asked-questions"></a><span data-ttu-id="b3a95-103">Preguntas más frecuentes de SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b3a95-103">SQL Data Warehouse Frequently asked questions</span></span>

## <a name="general"></a><span data-ttu-id="b3a95-104">General</span><span class="sxs-lookup"><span data-stu-id="b3a95-104">General</span></span>

<span data-ttu-id="b3a95-105">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-105">Q.</span></span> <span data-ttu-id="b3a95-106">¿Qué ofrece SQL Data Warehouse en cuanto a seguridad de datos?</span><span class="sxs-lookup"><span data-stu-id="b3a95-106">What does SQL DW offer for data security?</span></span>

<span data-ttu-id="b3a95-107">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-107">A.</span></span> <span data-ttu-id="b3a95-108">SQL Data Warehouse ofrece varias soluciones para proteger datos, como TDE y la auditoría.</span><span class="sxs-lookup"><span data-stu-id="b3a95-108">SQL DW offers several solutions for protecting data such as TDE and auditing.</span></span> <span data-ttu-id="b3a95-109">Para obtener más información, consulte [Seguridad].</span><span class="sxs-lookup"><span data-stu-id="b3a95-109">For more information, see [Security].</span></span>

<span data-ttu-id="b3a95-110">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-110">Q.</span></span> <span data-ttu-id="b3a95-111">¿Dónde puedo encontrar los estándares empresariales o legales que cumple SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="b3a95-111">Where can I find out what legal or business standards is SQL DW compliant with?</span></span>

<span data-ttu-id="b3a95-112">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-112">A.</span></span> <span data-ttu-id="b3a95-113">Visite hello [Microsoft Compliance] página para diversas ofertas de cumplimiento por producto como SOC e ISO.</span><span class="sxs-lookup"><span data-stu-id="b3a95-113">Visit hello [Microsoft Compliance] page for various compliance offerings by product such as SOC and ISO.</span></span> <span data-ttu-id="b3a95-114">Primero elija por título de cumplimiento de normas, a continuación, expanda Azure en hello Microsoft en el ámbito en la nube servicios en el lado derecho de Hola de hello página toosee qué servicios son servicios de Azure es compatibles.</span><span class="sxs-lookup"><span data-stu-id="b3a95-114">First choose by Compliance title, then expand Azure in hello Microsoft in-scope cloud services section on hello right side of hello page toosee what services are Azure services are compliant.</span></span>

<span data-ttu-id="b3a95-115">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-115">Q.</span></span> <span data-ttu-id="b3a95-116">¿Puedo conectar Power BI?</span><span class="sxs-lookup"><span data-stu-id="b3a95-116">Can I connect PowerBI?</span></span>

<span data-ttu-id="b3a95-117">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-117">A.</span></span> <span data-ttu-id="b3a95-118">Sí.</span><span class="sxs-lookup"><span data-stu-id="b3a95-118">Yes!</span></span> <span data-ttu-id="b3a95-119">Aunque Power BI admite la consulta directa con SQL Data Warehouse, no se ha diseñado para administrar gran cantidad de usuarios o datos en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="b3a95-119">Though PowerBI supports direct query with SQL DW, it’s not intended for large number of users or real-time data.</span></span> <span data-ttu-id="b3a95-120">Para usar Power BI con fines de producción, se recomienda usar Power BI sobre IaaS de servicio de análisis o Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="b3a95-120">For production use of PowerBI, we recommend using PowerBI on top of Azure Analysis Services or Analysis Service IaaS.</span></span> 

<span data-ttu-id="b3a95-121">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-121">Q.</span></span> <span data-ttu-id="b3a95-122">¿Qué son los límites de capacidad de SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="b3a95-122">What are SQL Data Warehouse Capacity Limits?</span></span>

<span data-ttu-id="b3a95-123">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-123">A.</span></span> <span data-ttu-id="b3a95-124">Consulte nuestra página de [límites de capacidad] actuales.</span><span class="sxs-lookup"><span data-stu-id="b3a95-124">See our current [capacity limits] page.</span></span> 

<span data-ttu-id="b3a95-125">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-125">Q.</span></span> <span data-ttu-id="b3a95-126">¿Por qué tardan tanto tiempo en completarse las operaciones de escalado, pausar y reanudación?</span><span class="sxs-lookup"><span data-stu-id="b3a95-126">Why is my Scale/Pause/Resume taking so long?</span></span>

<span data-ttu-id="b3a95-127">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-127">A.</span></span> <span data-ttu-id="b3a95-128">Una serie de factores puede influir en tiempo de presentación para las operaciones de administración de proceso.</span><span class="sxs-lookup"><span data-stu-id="b3a95-128">A variety of factors can influence hello time for compute management operations.</span></span> <span data-ttu-id="b3a95-129">Un caso habitual de operaciones de ejecución prolongada es la reversión de transacciones.</span><span class="sxs-lookup"><span data-stu-id="b3a95-129">A common case for  long running operations is transactional rollback.</span></span> <span data-ttu-id="b3a95-130">Cuando se inicia una operación de escalado o pausa, se bloquean todas las sesiones entrantes y se purgan las consultas.</span><span class="sxs-lookup"><span data-stu-id="b3a95-130">When a scale or pause operation is initiated, all incoming sessions are blocked and queries are drained.</span></span> <span data-ttu-id="b3a95-131">En el sistema de hello pedidos tooleave en un estado estable, se deben poner las transacciones antes de que pueda comenzar una operación.</span><span class="sxs-lookup"><span data-stu-id="b3a95-131">In order tooleave hello system in a stable state, transactions must be rolled back before an operation can commence.</span></span> <span data-ttu-id="b3a95-132">Hola mayor número de Hola y de mayor tamaño del registro de hello de transacciones, se detenido a operación de hello más hello de restaurar el estado estable de hello sistema tooa.</span><span class="sxs-lookup"><span data-stu-id="b3a95-132">hello greater hello number and larger hello log size of transactions, hello longer hello operation will be stalled restoring hello system tooa stable state.</span></span>

## <a name="user-support"></a><span data-ttu-id="b3a95-133">Asistencia técnica de usuario</span><span class="sxs-lookup"><span data-stu-id="b3a95-133">User support</span></span>

<span data-ttu-id="b3a95-134">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-134">Q.</span></span> <span data-ttu-id="b3a95-135">Tengo una solicitud de característica, ¿dónde puede enviarla?</span><span class="sxs-lookup"><span data-stu-id="b3a95-135">I have a feature request, where do I submit it?</span></span>

<span data-ttu-id="b3a95-136">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-136">A.</span></span> <span data-ttu-id="b3a95-137">Si tiene una solicitud de característica, envíala a nuestra página [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="b3a95-137">If you have a feature request, submit it on our [UserVoice] page</span></span>

<span data-ttu-id="b3a95-138">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-138">Q.</span></span> <span data-ttu-id="b3a95-139">¿Cómo puedo hacer una determinada acción?</span><span class="sxs-lookup"><span data-stu-id="b3a95-139">How can I do x?</span></span>

<span data-ttu-id="b3a95-140">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-140">A.</span></span> <span data-ttu-id="b3a95-141">Para obtener ayuda con las tareas de desarrollo con SQL Data Warehouse, puede hacer preguntas en nuestra [Stack Overflow].</span><span class="sxs-lookup"><span data-stu-id="b3a95-141">For help in developing with SQL Data Warehouse, you can ask questions on our [Stack Overflow] page.</span></span> 

<span data-ttu-id="b3a95-142">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-142">Q.</span></span> <span data-ttu-id="b3a95-143">¿Cómo puedo enviar una vale de asistencia técnica?</span><span class="sxs-lookup"><span data-stu-id="b3a95-143">How do I submit a support ticket?</span></span>

<span data-ttu-id="b3a95-144">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-144">A.</span></span> <span data-ttu-id="b3a95-145">Los [vales de asistencia técnica] puede presentarse a través de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="b3a95-145">[Support Tickets] can be filed through Azure portal.</span></span>

## <a name="sql-languagefeature-support"></a><span data-ttu-id="b3a95-146">Compatibilidad con características o lenguajes de SQL</span><span class="sxs-lookup"><span data-stu-id="b3a95-146">SQL language/feature support</span></span> 

<span data-ttu-id="b3a95-147">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-147">Q.</span></span> <span data-ttu-id="b3a95-148">¿Qué tipos de datos admite SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="b3a95-148">What datatypes does SQL Data Warehouse support?</span></span>

<span data-ttu-id="b3a95-149">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-149">A.</span></span> <span data-ttu-id="b3a95-150">Vea los [tipos de datos] de SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b3a95-150">See SQL Data Warehouse [data types].</span></span>

<span data-ttu-id="b3a95-151">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-151">Q.</span></span> <span data-ttu-id="b3a95-152">¿Qué características de tablas se admiten?</span><span class="sxs-lookup"><span data-stu-id="b3a95-152">What table features do you support?</span></span>

<span data-ttu-id="b3a95-153">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-153">A.</span></span> <span data-ttu-id="b3a95-154">Aunque SQL Data Warehouse es compatible con muchas características, algunas no se admiten y se documentan en la página sobre [características de tablas no admitidas].</span><span class="sxs-lookup"><span data-stu-id="b3a95-154">While SQL Data Warehouse supports many features, some are not supported and are documented in [Unsupported Table Features].</span></span>

## <a name="tooling-and-administration"></a><span data-ttu-id="b3a95-155">Administración y herramientas</span><span class="sxs-lookup"><span data-stu-id="b3a95-155">Tooling and administration</span></span>

<span data-ttu-id="b3a95-156">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-156">Q.</span></span> <span data-ttu-id="b3a95-157">¿Se admiten proyectos de bases de datos en Visual Studio?</span><span class="sxs-lookup"><span data-stu-id="b3a95-157">Do you support Database projects in Visual Studio.</span></span>

<span data-ttu-id="b3a95-158">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-158">A.</span></span> <span data-ttu-id="b3a95-159">En estos momentos, no admitimos proyectos de bases de datos en Visual Studio para SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b3a95-159">We currently do not support Database projects in Visual Studio for SQL Data Warehouse.</span></span> <span data-ttu-id="b3a95-160">Si desea que toocast un voto tooget esta característica, visite nuestro User Voice [solicitud de características de proyectos de base de datos].</span><span class="sxs-lookup"><span data-stu-id="b3a95-160">If you'd like toocast a vote tooget this feature, visit our User Voice [Database projects feature request].</span></span>

<span data-ttu-id="b3a95-161">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-161">Q.</span></span> <span data-ttu-id="b3a95-162">¿SQL Data Warehouse admite las API de REST?</span><span class="sxs-lookup"><span data-stu-id="b3a95-162">Does SQL Data Warehouse support REST APIs?</span></span>

<span data-ttu-id="b3a95-163">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-163">A.</span></span> <span data-ttu-id="b3a95-164">Sí.</span><span class="sxs-lookup"><span data-stu-id="b3a95-164">Yes.</span></span> <span data-ttu-id="b3a95-165">La mayoría de las funciones REST que se pueden utilizar con la base de datos SQL también están disponibles con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b3a95-165">Most REST functionality that can be used with SQL Database is also available with SQL Data Warehouse.</span></span> <span data-ttu-id="b3a95-166">Puede encontrar información sobre las API en las páginas de documentación de REST o [MSDN].</span><span class="sxs-lookup"><span data-stu-id="b3a95-166">You can find API information within REST documentation pages or [MSDN].</span></span>


## <a name="loading"></a><span data-ttu-id="b3a95-167">Carga</span><span class="sxs-lookup"><span data-stu-id="b3a95-167">Loading</span></span>

<span data-ttu-id="b3a95-168">P:</span><span class="sxs-lookup"><span data-stu-id="b3a95-168">Q.</span></span> <span data-ttu-id="b3a95-169">¿Qué controladores de cliente se admiten?</span><span class="sxs-lookup"><span data-stu-id="b3a95-169">What client drivers do you support?</span></span>

<span data-ttu-id="b3a95-170">A.</span><span class="sxs-lookup"><span data-stu-id="b3a95-170">A.</span></span> <span data-ttu-id="b3a95-171">Compatibilidad con controladores de almacenamiento de datos puede encontrarse en hello [las cadenas de conexión] página</span><span class="sxs-lookup"><span data-stu-id="b3a95-171">Driver support for DW can be found on hello [Connection Strings] page</span></span>

<span data-ttu-id="b3a95-172">P.: ¿Qué formatos de archivo admite PolyBase con SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="b3a95-172">Q: What file formats are supported by PolyBase with SQL Data Warehouse?</span></span>

<span data-ttu-id="b3a95-173">R.: Orc, RC, Parquet y texto delimitado sin formato.</span><span class="sxs-lookup"><span data-stu-id="b3a95-173">A: Orc, RC, Parquet, and flat delimited text</span></span>

<span data-ttu-id="b3a95-174">P: ¿qué puede conectar toofrom de almacenamiento de datos de SQL con PolyBase?</span><span class="sxs-lookup"><span data-stu-id="b3a95-174">Q: What can I connect toofrom SQL DW using PolyBase?</span></span> 

<span data-ttu-id="b3a95-175">R.: [Azure Data Lake Store] e instancias de [Azure Storage Blobs].</span><span class="sxs-lookup"><span data-stu-id="b3a95-175">A: [Azure Data Lake Store] and [Azure Storage Blobs]</span></span>

<span data-ttu-id="b3a95-176">P: ¿es posible aplicación de cálculo cuando se conecte tooAzure Blobs de almacenamiento o ADLS?</span><span class="sxs-lookup"><span data-stu-id="b3a95-176">Q: Is computation pushdown possible  when connecting tooAzure Storage Blobs or ADLS?</span></span> 

<span data-ttu-id="b3a95-177">R: no, PolyBase de almacenamiento de datos de SQL interactúa sólo los componentes de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="b3a95-177">A: No, SQL DW PolyBase only interacts hello storage components.</span></span> 

<span data-ttu-id="b3a95-178">P: ¿puedo conectarme tooHDI?</span><span class="sxs-lookup"><span data-stu-id="b3a95-178">Q: Can I connect tooHDI?</span></span>

<span data-ttu-id="b3a95-179">R: HDI sirve como capa HDFS hello ADLS o WASB.</span><span class="sxs-lookup"><span data-stu-id="b3a95-179">A: HDI can use either ADLS or WASB as hello HDFS layer.</span></span> <span data-ttu-id="b3a95-180">Si tiene uno de los dos como la capa HDFS, puede cargar datos en SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b3a95-180">If you have either as your HDFS layer, then you can load that data into SQL DW.</span></span> <span data-ttu-id="b3a95-181">Sin embargo, no se puede generar la instancia HDI de toohello de cálculo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b3a95-181">However, you cannot generate pushdown computation toohello HDI instance.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b3a95-182">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b3a95-182">Next steps</span></span>
<span data-ttu-id="b3a95-183">Para obtener más información sobre SQL Data Warehouse, vea nuestra página [Introducción].</span><span class="sxs-lookup"><span data-stu-id="b3a95-183">For more information on SQL Data Warehouse as a whole, see our [Overview] page.</span></span>


<!-- Article references -->
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[las cadenas de conexión]: ./sql-data-warehouse-connection-strings.md
[Stack Overflow]: http://stackoverflow.com/questions/tagged/azure-sqldw
[vales de asistencia técnica]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Seguridad]: ./sql-data-warehouse-overview-manage-security.md
[Microsoft Compliance]: https://www.microsoft.com/en-us/trustcenter/compliance/complianceofferings
[límites de capacidad]: ./sql-data-warehouse-service-capacity-limits.md
[tipos de datos]: ./sql-data-warehouse-tables-data-types.md
[características de tablas no admitidas]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Azure Data Lake Store]: ./sql-data-warehouse-load-from-azure-data-lake-store.md
[Azure Storage Blobs]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[solicitud de características de proyectos de base de datos]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
[MSDN]: https://msdn.microsoft.com/en-us/library/azure/mt163685.aspx
[Introducción]: ./sql-data-warehouse-overview-faq.md